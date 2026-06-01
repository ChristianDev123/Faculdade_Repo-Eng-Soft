## 0. Seleção de Escopo
---------------------

Neste trabalho, optou-se por não modelar o sistema SoundWave em sua totalidade, priorizando a profundidade técnica em três fluxos centrais que representam a essência da plataforma e os desafios de arquitetura mapeados nos trabalhos anteriores.

### 0.1 Fatias Selecionadas

**Fatia 1 — Artista realiza upload de música lossless (FLAC/WAV)**

*   **Casos de uso cobertos:** US-SUB1-001 (Upload FLAC/WAV), US-SUB1-007 (Editar metadados).
    
*   **Por que é representativa:** Trata-se de um requisito _Must Have_ absoluto (sem músicas, não há plataforma). Além disso, carrega a principal restrição técnica do projeto (NF-CONST-001 e NF-CONST-003): o processamento de arquivos grandes (até 200MB) e a validação estrita de formato.
    
*   **O que se espera aprender:** A modelagem de fluxos com decisões de validação rigorosas e atividades assíncronas (o upload do arquivo versus a disponibilidade da música na plataforma).
    

**Fatia 2 — Ouvinte reproduz música com transcodificação adaptativa**

*   **Casos de uso cobertos:** US-SUB2-001 (Busca), US-SUB2-006 (Ajuste de qualidade por conexão).
    
*   **Por que é representativa:** Atravessa o aplicativo do ouvinte e a infraestrutura de streaming. Contém a regra de negócio mais complexa de performance: monitorar a rede e degradar graciosamente o arquivo (Lossless para MP3) caso a conexão oscile, garantindo o requisito NF-SUB2-001 (Latência < 2s).
    
*   **O que se espera aprender:** A representação de um fluxo síncrono distribuído com caminhos de exceção (queda de rede) e requisições a serviços externos (CDN/Transcoder).
    

**Fatia 3 — Ciclo de vida do Selo de Verificado**

*   **Casos de uso cobertos:** US-SUB1-005 (Solicitar selo), US-SUB3-001 (Admin analisa selo), US-SUB2-008 (Ouvinte visualiza selo).
    
*   **Por que é representativa:** Constitui a fatia ideal para exercitar a interação entre múltiplos atores (Artista solicita, Administrador modera, Ouvinte consome). Possui transições de estado bem definidas e dependências inter-subsistemas.
    
*   **O que se espera aprender:** A expressão do ciclo de vida de uma entidade através de um diagrama de estados, mapeando eventos, guardas e ações de notificação.
    

### 0.2 Cobertura dos Critérios

| Critério | Fatia 1 (Upload) | Fatia 2 (Streaming) | Fatia 3 (Verificação) |
| :--- | :--- | :--- | :--- |
| Must Have do MoSCoW | Sim | Sim | Could Have| 
| Múltiplos subsistemas/atores | Foco no Artista/Sistema | Ouvinte / Infra / CDN | Artista / Admin / Ouvinte |
| Regras de negócio não-triviais | Validação e tamanho de arquivo |Transcodificação adaptativa | Ciclo de aprovação/rejeição |


### 0.3 Casos de uso não modelados

Os seguintes casos de uso foram explicitamente deixados fora do escopo de modelagem:

*   **CRUDs de Playlists e Perfis (US-SUB2-003, US-SUB1-004):** Operações triviais de banco de dados que não agregam aprendizado na modelagem de domínio complexo.
    
*   **Sistema de Recomendação (US-SUB2-005):** Por depender de algoritmos de correlação heurística, foge do escopo de modelagem UML clássica, sendo tratado como caixa preta.
    
*   **Autenticação e LGPD (US-SUB3-003, US-SUB3-005):** Embora cruciais para o projeto, são fluxos padrões. A modelagem focou nas regras inerentes ao domínio de _streaming_ de áudio.