# Documento de Requisitos: Projeto SoundWave

## 1. Introdução
Este documento apresenta o levantamento de requisitos para a startup **SoundWave**, uma plataforma de streaming focada em dar visibilidade a artistas independentes através de nichos musicais, fugindo dos algoritmos tendenciosos das grandes gravadoras.

### 1.1 Identificação de Subsistemas e Grupos de Usuários
Conforme as capacidades do produto, o sistema foi dividido nos seguintes subsistemas:

1.  **Portal do Artista (SUB1):** Destinado ao gerenciamento de carreira, uploads e análise de métricas.
    * **Grupo de Usuários:** Artista Independente (USER-001).
2.  **App do Ouvinte (SUB2):** Destinado à descoberta de músicas, criação de playlists e consumo de áudio.
    * **Grupo de Usuários:** Ouvinte (USER-002).
3.  **Painel de Administração (SUB3):** Destinado à moderação de conteúdo, suporte e gestão de segurança.
    * **Grupo de Usuários:** Administrador (USER-003).

---

## 2. Levantamento de Requisitos Funcionais

### 2.1 Histórias de Usuário
As histórias seguem o padrão solicitado. Abaixo, apresentamos exemplos cruciais para o core do negócio:

| ID | História | Critérios de Aceitação | Dependências | Fonte |
| :--- | :--- | :--- | :--- | :--- |
| US-SUB1-001 | **Como** artista, **eu quero** realizar o upload de músicas em FLAC/WAV, **para que** eu mantenha a alta fidelidade da minha obra. | (a) O arquivo não deve exceder 200MB. (b) O sistema deve validar o formato antes de iniciar. | Nenhuma | USER-001 |
| US-SUB1-002 | **Como** artista, **eu quero** acessar um dashboard de analytics, **para que** eu entenda o alcance da minha música por nicho. | (a) Exibir gráficos de reprodução em tempo real. (b) Filtrar dados por gênero musical. | US-SUB1-001 | USER-001 |
| US-SUB2-001 | **Como** ouvinte, **eu quero** buscar músicas por filtros de nicho, **para que** eu descubra artistas fora do mainstream. | (a) Permitir busca por gênero e tags de comunidade. (b) Resultados devem priorizar afinidade sonora. | Nenhuma | USER-002 |
| US-SUB3-001 | **Como** admin, **eu quero** acessar logs de auditoria de uploads, **para que** eu garanta a integridade e segurança do catálogo. | (a) Registrar data, hora e IP do upload. (b) Permitir busca por ID de artista. | US-SUB1-001 | USER-003 |

> **Nota:** Conforme o requisito do trabalho, o grupo deve completar 10 histórias para cada subsistema (total de 30).

### 2.2 Estimativa de Tamanho
**Metodologia:** Story Points (Escala Fibonacci: 1, 2, 3, 5, 8, 13, 21).

**Justificativa:** A escala Fibonacci foi escolhida por refletir a incerteza e a complexidade técnica inerente a um sistema de áudio. Tarefas como o processamento de arquivos Lossless (FLAC) possuem maior incerteza que a criação de formulários, justificando uma pontuação relativa mais precisa para o contexto de startup.

### 2.3 Priorização MoSCoW (Tabela Consolidada)
Abaixo, a organização das funcionalidades conforme impacto no negócio:

| ID | Subsistema | Prioridade | Estimativa | Justificativa |
| :--- | :--- | :--- | :--- | :--- |
| US-SUB1-001 | Portal Artista | **Must Have** | 13 | Sem upload não há produto. É o requisito essencial. |
| US-SUB2-001 | App Ouvinte | **Must Have** | 8 | Core do negócio: a descoberta por nicho é o diferencial competitivo. |
| US-SUB1-002 | Portal Artista | **Should Have** | 5 | Importante para o engajamento do artista, mas não impede o play. |
| US-SUB2-005 | App Ouvinte | **Could Have** | 3 | Customização estética do perfil do ouvinte (valor agregado secundário). |

---

## 3. Requisitos Não Funcionais (Padronização IEEE-830)

### 3.1 Mapeamento e Justificativa
Os requisitos abaixo foram mapeados com base nos aprendizados de arquitetura de software e restrições de produto:

1.  **Segurança (Conformidade LGPD):** O sistema deve anonimizar dados de ouvintes após exclusão de conta. **Justificativa:** Atendimento à restrição NF-CONST-002 e normas éticas de software.
2.  **Desempenho (Streaming):** O buffering inicial não deve exceder 2 segundos em conexões 4G. **Justificativa:** Baseado na norma ISO/IEC 25010 para garantir a qualidade de experiência (QoE).

### 3.2 Detalhamento de Requisito Não Funcional

| Campo | Descrição |
| :--- | :--- |
| Requisito ID | NF-SUB2-001 |
| Título | **Desempenho de Resposta no Streaming** |
| Descrição | O sistema deve iniciar a reprodução de áudio (incluindo FLAC) em até 2 segundos. |
| Entrada | Solicitação de reprodução (clique no Play). |
| Processamento | O sistema requisita o pacote de áudio via CDN e inicia o pre-buffering. |
| Saída | Áudio audível e início da barra de progresso. |
| Restrições | Dependência da estabilidade da rede do usuário final. |
| Critérios de Aceitação | (a) O tempo de resposta não excede 2 segundos em 95% das tentativas. (b) Ausência de engasgos após o play inicial. |

---

## 4. Referências
* **IEEE-830:** Práticas recomendadas para especificação de requisitos de software.
* **ISO/IEC 25010:** Modelos de qualidade de produto de software.
* **LGPD:** Lei Geral de Proteção de Dados (Brasil).
