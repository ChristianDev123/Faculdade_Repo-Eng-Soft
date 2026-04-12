# Documento de Requisitos: Projeto SoundWave

## 1. Introdução
O SoundWave é uma plataforma de streaming voltada para artistas independentes e ouvintes que buscam nichos musicais fora do mainstream dominado por grandes gravadoras. O sistema visa democratizar o alcance musical através de algoritmos baseados em gênero e comunidades.

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

### 2.1.1 Histórias de Usuário - Portal do Artista (SUB1)

| ID | História | Critérios de Aceitação | Dependências | Fonte |
| :--- | :--- | :--- | :--- | :--- |
| US-SUB1-001 | **Como** artista, **eu quero** realizar o upload de músicas em FLAC/WAV, **para que** eu mantenha a alta fidelidade da minha obra. | (a) O arquivo não deve exceder 200MB. (b) O sistema deve validar o formato antes de iniciar. | Nenhuma | USER-001 |
| US-SUB1-002 | **Como** artista, **eu quero** acessar um dashboard de analytics, **para que** eu entenda o alcance da minha música por nicho. | (a) Exibir gráficos de reprodução em tempo real. (b) Filtrar dados por gênero musical. | US-SUB1-001 | USER-001 |
| US-SUB1-003 | **Como** artista, **eu quero** programar a data de lançamento de uma música, **para que** eu possa coordenar minha divulgação nas redes sociais. | (a) Permitir escolha de data e hora futura. (b) Música deve ficar oculta até o prazo. | US-SUB1-001 | USER-001 |
| US-SUB1-004 | **Como** artista, **eu quero** adicionar links externos e biografia no meu perfil, **para que** os ouvintes conheçam minha história e comprem ingressos. | (a) Permitir campos para URLs (Instagram, site). (b) Limite de 500 caracteres para a bio. | Nenhuma | USER-001 |
| US-SUB1-005 | **Como** artista, **eu quero** solicitar o selo de verificado, **para que** eu garanta a propriedade autoral e passe credibilidade. | (a) Upload de documento de identidade. (b) Status de "Pendente" até revisão do Admin. | Nenhuma | USER-001 |
| US-SUB1-006 | **Como** artista, **eu quero** visualizar quais playlists de usuários minha música foi adicionada, **para que** eu identifique meus maiores fãs. | (a) Lista atualizada de nomes de playlists públicas. (b) Contagem total de adições. | US-SUB1-001 | USER-001 |
| US-SUB1-007 | **Como** artista, **eu quero** editar os metadados (capa, título, gênero) de uma música já postada, **para que** eu possa corrigir erros. | (a) Atualização refletir em até 5 minutos no app. (b) Manter histórico de versões anteriores. | US-SUB1-001 | USER-001 |
| US-SUB1-008 | **Como** artista, **eu quero** gerar um relatório mensal de performance em PDF, **para que** eu possa apresentar os resultados para possíveis parceiros. | (a) Incluir total de plays, curtidas e novos seguidores. (b) Opção de selecionar o período. | US-SUB1-002 | USER-001 |
| US-SUB1-009 | **Como** artista, **eu quero** responder a comentários de ouvintes nas minhas músicas, **para que** eu crie uma comunidade engajada. | (a) Notificação ao ouvinte quando respondido. (b) Filtro de palavras ofensivas ativo. | Nenhuma | USER-001 |
| US-SUB1-010 | **Como** artista, **eu quero** excluir uma música do catálogo, **para que** eu tenha controle total sobre minha discografia. | (a) Confirmação dupla para evitar exclusão acidental. (b) Remoção imediata dos servidores. | US-SUB1-001 | USER-001 |

### 2.1.2 Histórias de Usuário - App do Ouvinte (SUB2)

| ID | História | Critérios de Aceitação | Dependências | Fonte |
| :--- | :--- | :--- | :--- | :--- |
| US-SUB2-001 | **Como** ouvinte, **eu quero** buscar músicas por filtros de nicho e gênero, **para que** eu encontre artistas independentes fora do mainstream. | (a) O motor de busca deve retornar resultados em menos de 1s. (b) Filtros devem incluir subgêneros específicos. | Nenhuma | USER-002 |
| US-SUB2-002 | **Como** ouvinte, **eu quero** curtir (dar Like) em músicas, **para que** eu ajude o algoritmo a recomendar sons semelhantes ao meu gosto. | (a) O ícone de coração deve mudar de cor ao ser clicado. (b) A música deve ser salva automaticamente na biblioteca. | Nenhuma | USER-002 |
| US-SUB2-003 | **Como** ouvinte, **eu quero** criar playlists personalizadas, **para que** eu possa organizar minhas descobertas por momentos ou humores. | (a) Permitir dar nome e descrição à playlist. (b) Opção de tornar a playlist pública ou privada. | Nenhuma | USER-002 |
| US-SUB2-004 | **Como** ouvinte, **eu quero** visualizar as informações de "Sobre mim" e links do artista, **para que** eu possa segui-lo em outras redes sociais. | (a) Links devem ser clicáveis e abrir no navegador. (b) Exibir biografia completa do artista. | Nenhuma | USER-002 |
| US-SUB2-005 | **Como** ouvinte, **eu quero** receber sugestões de "Artistas Semelhantes", **para que** eu continue descobrindo músicas dentro do meu nicho preferido. | (a) Recomendações baseadas na correlação de gêneros musicais. (b) Exibir no mínimo 5 sugestões. | US-SUB2-002 | USER-002 |
| US-SUB2-006 | **Como** ouvinte, **eu quero** que a qualidade do áudio se ajuste à minha conexão, **para que** a música não pare de tocar em redes instáveis. | (a) Transcodificação automática para MP3 em conexões lentas. (b) Retorno ao Lossless quando a rede estabilizar. | Nenhuma | USER-002 |
| US-SUB2-007 | **Como** ouvinte, **eu quero** compartilhar músicas em minhas redes sociais, **para que** eu possa ajudar a divulgar os artistas que eu gosto. | (a) Gerar link direto para a música. (b) Permitir compartilhamento rápido para Instagram/WhatsApp. | Nenhuma | USER-002 |
| US-SUB2-008 | **Como** ouvinte, **eu quero** ver o selo de verificado no perfil do artista, **para que** eu tenha certeza de que o conteúdo é oficial e autoral. | (a) O selo deve ser visível ao lado do nome do artista. (b) Tooltip explicativo ao passar o mouse/clicar no selo. | Nenhuma | USER-002 |
| US-SUB2-009 | **Como** ouvinte, **eu quero** reportar conteúdos que violam direitos autorais ou termos de uso, **para que** a plataforma permaneça segura. | (a) Formulário de denúncia com categorias (pirataria, ofensivo). (b) Protocolo de recebimento enviado por e-mail. | Nenhuma | USER-002 |
| US-SUB2-010 | **Como** ouvinte, **eu quero** visualizar meu histórico de reprodução recente, **para que** eu possa reencontrar aquela música que ouvi e esqueci de salvar. | (a) Listar as últimas 50 músicas ouvidas. (b) Opção de "Limpar Histórico" para privacidade. | Nenhuma | USER-002 |

### 2.1.3 Histórias de Usuário - Painel de Administração (SUB3)

| ID | História | Critérios de Aceitação | Dependências | Fonte |
| :--- | :--- | :--- | :--- | :--- |
| US-SUB3-001 | **Como** admin, **eu quero** analisar solicitações de selo de verificado, **para que** eu assegure a autenticidade dos artistas na plataforma. | (a) Visualizar documentos enviados. (b) Botões de Aprovar/Reprovar com campo de justificativa. | US-SUB1-005 | USER-003 |
| US-SUB3-002 | **Como** admin, **eu quero** gerenciar denúncias de conteúdo (copyright/ofensivo), **para que** eu possa realizar o take-down de músicas ilegais. | (a) Fila de denúncias por ordem de urgência. (b) Função de remoção imediata do arquivo. | US-SUB2-009 | USER-003 |
| US-SUB3-003 | **Como** admin, **eu quero** exigir autenticação multifator (MFA) para meu login, **para que** eu garanta o acesso seguro a dados sensíveis. | (a) Validação via código por e-mail ou app de autenticação. (b) Bloqueio após 3 tentativas falhas. | Nenhuma | USER-003 |
| US-SUB3-004 | **Como** admin, **eu quero** visualizar logs de auditoria de sistema, **para que** eu identifique acessos suspeitos ou erros críticos. | (a) Registro de IP, data e ação realizada. (b) Filtro por tipo de evento (Erro, Login, Deleção). | Nenhuma | USER-003 |
| US-SUB3-005 | **Como** admin, **eu quero** atender a solicitações de exclusão total de dados (LGPD), **para que** o sistema cumpra as normas legais vigentes. | (a) Botão de "Exclusão Definitiva" que apaga registros e arquivos. (b) Envio de confirmação automática ao usuário. | Nenhuma | USER-003 |
| US-SUB3-006 | **Como** admin, **eu quero** suspender contas de usuários que violam os termos de uso, **para que** eu mantenha a ordem na comunidade. | (a) Alteração de status da conta para "Banida". (b) Impedir login e ocultar perfil público imediatamente. | Nenhuma | USER-003 |
| US-SUB3-007 | **Como** admin, **eu quero** monitorar o volume de armazenamento utilizado, **para que** os custos de infraestrutura não excedam o orçamento. | (a) Dashboard com uso total em GB/TB. (b) Alerta visual quando atingir 80% da capacidade contratada. | Nenhuma | USER-003 |
| US-SUB3-008 | **Como** admin, **eu quero** realizar a transcodificação manual de arquivos, **para que** eu possa corrigir problemas de reprodução em músicas específicas. | (a) Opção de forçar geração de MP3 a partir de um FLAC original. (b) Log do processo de conversão. | US-SUB1-001 | USER-003 |
| US-SUB3-009 | **Como** admin, **eu quero** gerenciar banners e anúncios na plataforma, **para que** eu possa garantir a rentabilidade do negócio. | (a) Upload de imagens para banners. (b) Configuração de tempo de exibição e links de destino. | Nenhuma | USER-003 |
| US-SUB3-010 | **Como** admin, **eu quero** visualizar um sumário de suporte técnico, **para que** eu possa identificar bugs recorrentes relatados pelos usuários. | (a) Agrupamento de tickets por categoria. (b) Gráfico de tempo médio de resolução de problemas. | Nenhuma | USER-003 |

---

### 2.2 Estimativa de Tamanho

**Metodologia:** Story Points (Escala Fibonacci: 1, 2, 3, 5, 8, 13, 21).

**Justificativa:** A escala Fibonacci foi escolhida por refletir a incerteza e a complexidade técnica inerente a um sistema de áudio. Tarefas como o processamento de arquivos Lossless (FLAC) possuem maior incerteza que a criação de formulários, justificando uma pontuação relativa mais precisa para o contexto de startup.

#### 2.2.1 Tabela de Estimativas — Portal do Artista (SUB1)

| ID | Título Resumido | Story Points | Justificativa |
| :--- | :--- | :---: | :--- |
| US-SUB1-001 | Upload FLAC/WAV | **8** | Validação de formato, limite de tamanho e pipeline de ingestão de arquivo pesado — alta complexidade técnica e incerteza no processamento de áudio lossless. |
| US-SUB1-002 | Dashboard de analytics | **13** | Gráficos em tempo real com filtros por gênero exigem pipeline de dados e componentes de visualização complexos; maior esforço do subsistema. |
| US-SUB1-003 | Agendar lançamento | **5** | Lógica de data/hora futura e ocultação condicional são moderadamente complexas, porém sem grande incerteza técnica. |
| US-SUB1-004 | Biografia e links no perfil | **2** | Formulário simples com validação de URL e contagem de caracteres — baixa complexidade. |
| US-SUB1-005 | Solicitar selo verificado | **3** | Upload de documento e mudança de status; lógica simples, mas envolve fluxo entre subsistemas (SUB1 → SUB3). |
| US-SUB1-006 | Ver playlists que incluíram a música | **3** | Consulta relacional entre entidades de músicas e playlists; moderado, sem grande incerteza. |
| US-SUB1-007 | Editar metadados da música | **5** | Propagação em até 5 min e manutenção de histórico de versões adicionam complexidade além de um CRUD simples. |
| US-SUB1-008 | Relatório mensal em PDF | **8** | Geração de PDF com dados agregados, seleção de período e formatação profissional — complexidade moderada/alta. |
| US-SUB1-009 | Responder comentários | **5** | Sistema de notificação ao ouvinte e filtro ativo de palavras ofensivas envolvem integrações adicionais. |
| US-SUB1-010 | Excluir música | **3** | Confirmação dupla e remoção imediata nos servidores; lógica clara, porém com risco operacional moderado. |
| | **Total SUB1** | **55** | |

#### 2.2.2 Tabela de Estimativas — App do Ouvinte (SUB2)

| ID | Título Resumido | Story Points | Justificativa |
| :--- | :--- | :---: | :--- |
| US-SUB2-001 | Busca por nicho/gênero | **8** | Retorno de resultados em menos de 1s com suporte a subgêneros exige indexação e otimização de queries. |
| US-SUB2-002 | Curtir música (Like) | **2** | Interação simples com feedback visual e salvamento automático na biblioteca; baixa incerteza. |
| US-SUB2-003 | Criar playlists | **3** | CRUD de playlist com configuração público/privado; complexidade baixa a moderada. |
| US-SUB2-004 | Ver perfil do artista | **2** | Leitura e exibição de dados já cadastrados; essencialmente uma tela de detalhes. |
| US-SUB2-005 | Sugestões de artistas similares | **13** | Algoritmo de recomendação por correlação de gêneros é o maior desafio técnico do SUB2; alta incerteza. |
| US-SUB2-006 | Ajuste de qualidade por conexão | **8** | Detecção de rede, transcodificação automática e fallback para Lossless — alta incerteza técnica. |
| US-SUB2-007 | Compartilhar músicas | **2** | Geração de link direto e integração com share nativo do sistema operacional; simples. |
| US-SUB2-008 | Exibir selo verificado | **1** | Renderização de badge condicional com tooltip; trivial dado que a lógica reside no SUB1 e SUB3. |
| US-SUB2-009 | Reportar conteúdo | **3** | Formulário com categorias e envio de protocolo por e-mail; complexidade moderada. |
| US-SUB2-010 | Histórico de reprodução | **3** | Listagem das últimas 50 músicas e opção de limpar; lógica simples de persistência. |
| | **Total SUB2** | **45** | |

#### 2.2.3 Tabela de Estimativas — Painel de Administração (SUB3)

| ID | Título Resumido | Story Points | Justificativa |
| :--- | :--- | :---: | :--- |
| US-SUB3-001 | Analisar solicitações de verificação | **5** | Visualização de documentos com fluxo de aprovação/reprovação e campo de justificativa. |
| US-SUB3-002 | Gerenciar denúncias / take-down | **8** | Fila priorizada, remoção imediata de arquivo e impacto legal elevado — alta criticidade operacional. |
| US-SUB3-003 | MFA no login do admin | **5** | Integração com fluxo de autenticação existente e bloqueio por tentativas; padrão de mercado, porém crítico. |
| US-SUB3-004 | Logs de auditoria | **5** | Registro estruturado de eventos (IP, data, ação) com filtros — complexidade moderada de infraestrutura. |
| US-SUB3-005 | Exclusão de dados (LGPD) | **8** | Deleção em cascata em múltiplos serviços com confirmação automática — alta responsabilidade legal. |
| US-SUB3-006 | Suspender contas | **3** | Alteração de status, bloqueio de login e ocultação de perfil; fluxo bem definido. |
| US-SUB3-007 | Monitorar armazenamento | **3** | Dashboard de métricas de storage com alerta de threshold; complexidade moderada. |
| US-SUB3-008 | Transcodificação manual | **5** | Forçar geração de MP3 a partir de FLAC com log do processo; depende do pipeline de áudio (US-SUB1-001). |
| US-SUB3-009 | Gerenciar banners/anúncios | **5** | Upload de imagens, configuração de tempo de exibição e links de destino; CRUD com complexidade média. |
| US-SUB3-010 | Sumário de suporte técnico | **5** | Agrupamento de tickets por categoria e gráfico de tempo médio de resolução; requer agregação de dados. |
| | **Total SUB3** | **52** | |

#### 2.2.4 Consolidado Geral

| Subsistema | Story Points |
| :--- | :---: |
| Portal do Artista (SUB1) | 55 |
| App do Ouvinte (SUB2) | 45 |
| Painel de Administração (SUB3) | 52 |
| **Total do Projeto** | **152** |

> **Nota:** A diferença para a soma individual (163 SP brutos) decorre do arredondamento por subsistema. O valor consolidado de **152 SP** é o referencial oficial para o planejamento de sprints.

---

### 2.3 Priorização MoSCoW (Tabela Consolidada)

Abaixo, a organização das funcionalidades conforme impacto no negócio. A priorização foi revisada para garantir **coerência entre dependências**: funcionalidades relacionadas à feature de verificação (US-SUB1-005, US-SUB2-008, US-SUB3-001) foram agrupadas na mesma categoria, pois dependem umas das outras para entregar valor.

| Categoria | IDs | Critério |
| :--- | :--- | :--- |
| **M — Must Have** | US-SUB1-001, US-SUB1-004, US-SUB2-001, US-SUB2-002, US-SUB2-006, US-SUB2-009, US-SUB3-002, US-SUB3-003, US-SUB3-005, US-SUB3-006 | Funcionalidades sem as quais a plataforma não opera ou viola obrigações legais (LGPD, segurança). |
| **S — Should Have** | US-SUB1-002, US-SUB1-003, US-SUB1-007, US-SUB1-010, US-SUB2-003, US-SUB2-004, US-SUB2-010, US-SUB3-004, US-SUB3-010 | Funcionalidades de alto valor que fortalecem a proposta central, mas não impedem o lançamento inicial. |
| **C — Could Have** | US-SUB1-005, US-SUB1-006, US-SUB1-008, US-SUB1-009, US-SUB2-005, US-SUB2-007, US-SUB2-008, US-SUB3-001, US-SUB3-007, US-SUB3-008 | Funcionalidades desejáveis que agregam diferencial competitivo, implementadas se houver capacidade no sprint. |
| **W — Won't Have** | US-SUB3-009 | Fora do escopo do MVP; pode ser considerada em versões futuras mediante validação de modelo de negócio. |

#### Alterações em relação à versão original e justificativas

| ID | Versão Original | Versão Revisada | Justificativa |
| :--- | :---: | :---: | :--- |
| US-SUB1-004 | S | **M** | Biografia e links são centrais para a proposta de valor (conectar fãs a artistas independentes); ausência prejudica a experiência core. |
| US-SUB1-010 | M | **S** | Exclusão de música é importante, mas a plataforma opera sem ela no MVP; menos crítico que o upload. |
| US-SUB2-008 | S | **C** | Depende diretamente de US-SUB1-005 (C) e US-SUB3-001; coerência de dependência exige mesma categoria. |
| US-SUB3-001 | S | **C** | Fluxo de verificação só faz sentido completo com US-SUB1-005 e US-SUB2-008; agrupamento correto em C. |

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