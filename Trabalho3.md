## 0. Seleção de Escopo

Neste trabalho, optou-se por não modelar o sistema SoundWave em sua totalidade, priorizando a profundidade técnica em três fluxos centrais que representam a essência da plataforma e os desafios de arquitetura mapeados nos trabalhos anteriores.

### 0.1. Fatias Selecionadas

**Fatia 1 - Artista realiza upload de música lossless (FLAC/WAV)**

*   **Casos de uso cobertos:** `US-SUB1-001` (Upload FLAC/WAV), `US-SUB1-007` (Editar metadados).
    
*   **Por que é representativa:** Trata-se de um requisito _Must Have_ absoluto (sem músicas, não há plataforma). Além disso, carrega a principal restrição técnica do projeto (`NF-CONST-001` e `NF-CONST-003`): o processamento de arquivos grandes (até 200MB) e a validação estrita de formato.
    
*   **O que se espera aprender:** A modelagem de fluxos com decisões de validação rigorosas e atividades assíncronas (o upload do arquivo versus a disponibilidade da música na plataforma).
    

**Fatia 2 - Ouvinte reproduz música com transcodificação adaptativa**

*   **Casos de uso cobertos:** `US-SUB2-001` (Busca), `US-SUB2-006` (Ajuste de qualidade por conexão).
    
*   **Por que é representativa:** Atravessa o aplicativo do ouvinte e a infraestrutura de streaming. Contém a regra de negócio mais complexa de performance: monitorar a rede e degradar graciosamente o arquivo (Lossless para MP3) caso a conexão oscile, garantindo o requisito `NF-SUB2-001` (Latência < 2s).
    
*   **O que se espera aprender:** A representação de um fluxo síncrono distribuído com caminhos de exceção (queda de rede) e requisições a serviços externos (CDN/Transcoder).
    

**Fatia 3 - Ciclo de vida do Selo de Verificado**

*   **Casos de uso cobertos:** `US-SUB1-005` (Solicitar selo), `US-SUB3-001` (Admin analisa selo), `US-SUB2-008` (Ouvinte visualiza selo).
    
*   **Por que é representativa:** Constitui a fatia ideal para exercitar a interação entre múltiplos atores (Artista solicita, Administrador modera, Ouvinte consome). Possui transições de estado bem definidas e dependências inter-subsistemas.
    
*   **O que se espera aprender:** A expressão do ciclo de vida de uma entidade através de um diagrama de estados, mapeando eventos, guardas e ações de notificação.
    

### 0.2. Cobertura dos Critérios

| Critério | Fatia 1 (Upload) | Fatia 2 (Streaming) | Fatia 3 (Verificação) |
| :--- | :--- | :--- | :--- |
| Must Have do MoSCoW | Sim | Sim | Could Have| 
| Múltiplos subsistemas/atores | Foco no Artista/Sistema | Ouvinte / Infra / CDN | Artista / Admin / Ouvinte |
| Regras de negócio não-triviais | Validação e tamanho de arquivo |Transcodificação adaptativa | Ciclo de aprovação/rejeição |


### 0.3. Casos de uso não modelados

Os seguintes casos de uso foram explicitamente deixados fora do escopo de modelagem:

*   **CRUDs de Playlists e Perfis (US-SUB2-003, US-SUB1-004):** Operações triviais de banco de dados que não agregam aprendizado na modelagem de domínio complexo.
    
*   **Sistema de Recomendação (US-SUB2-005):** Por depender de algoritmos de correlação heurística, foge do escopo de modelagem UML clássica, sendo tratado como caixa preta.
    
*   **Autenticação e LGPD (US-SUB3-003, US-SUB3-005):** Embora cruciais para o projeto, são fluxos padrões. A modelagem focou nas regras inerentes ao domínio de _streaming_ de áudio.


## 1. Diagrama de Classes

```
    class Usuario {
        <<abstract>>
        - UUID id
        - String nome
        - String email
        - String senhaHash
        + autenticar() boolean
    }

    class Artista {
        - String biografia
        - String[] linksExternos
        - boolean isVerificado
        + solicitarVerificacao(documento)
        + realizarUpload(arquivo, metadados)
    }

    class Ouvinte {
        - String tipoAssinatura
        + buscarMusica(query)
        + reproduzir(musica)
    }

    class Administrador {
        - String nivelAcesso
        + analisarSolicitacao(solicitacao, decisao)
    }

    class Musica {
        - UUID id
        - String titulo
        - String genero
        - Date dataPublicacao
        - int totalPlays
        + getMelhorFormato(conexaoRede) ArquivoAudio
        + atualizarMetadados(novosDados)
    }

    class ArquivoAudio {
        - UUID id
        - String formato
        - float tamanhoMB
        - int bitrate
        - String urlCDN
        + stream() byte[]
    }

    class SolicitacaoVerificacao {
        - UUID id
        - Date dataSolicitacao
        - String status
        - String documentoUrl
        - String justificativa
        + aprovar()
        + reprovar(motivo)
    }

    Usuario <|-- Artista
    Usuario <|-- Ouvinte
    Usuario <|-- Administrador

    Artista "1" -- "0..*" Musica : publica >
    Musica "1" *-- "1..*" ArquivoAudio : contem >
    Artista "1" -- "0..1" SolicitacaoVerificacao : abre >
    Administrador "1" -- "0..*" SolicitacaoVerificacao : modera >
```

### 1.1. Critérios de Qualidade Aplicados

*   **Herança e Abstração:** Foi utilizada uma classe abstrata Usuario para isolar propriedades comuns de autenticação, derivando as responsabilidades específicas para as subclasses `Artista`, `Ouvinte` e `Administrador`.

*   **Composição:** A relação entre `Musica` e `ArquivoAudio` foi modelada como composição, dado que um arquivo físico não possui semântica no sistema sem estar vinculado à entidade lógica da música.

*   **Resolução do Domínio:** Uma `Musica` pode conter múltiplos registros de `ArquivoAudio` (e.g., o arquivo **FLAC** original e o **MP3** transcodificado), atendendo à necessidade da transcodificação adaptativa (Fatia 2).

## 2. Modelo Entidade-Relacionamento (MER)

No MER, visando a otimização de consultas em um cenário de alto volume de acessos (streaming), optou-se pela estratégia de Tabela Única (Single Table) com a coluna discriminadora `tipo_usuario`. Atributos específicos ficam nulos para os perfis que não os utilizam.

```
    USUARIO {
        uuid id PK
        string tipo_usuario "DISCRIMINATOR: ARTISTA, OUVINTE, ADMIN"
        string nome
        string email
        string senha_hash
        string biografia
        boolean is_verificado
    }

    MUSICA {
        uuid id PK
        uuid artista_id FK
        string titulo
        string genero
        timestamp data_publicacao
        int total_plays
    }

    ARQUIVO_AUDIO {
        uuid id PK
        uuid musica_id FK
        string formato "FLAC, WAV, MP3"
        float tamanho_mb
        int bitrate
        string url_cdn
    }

    SOLICITACAO_VERIFICACAO {
        uuid id PK
        uuid artista_id FK
        uuid admin_id FK "Nullable"
        string status "PENDENTE, APROVADO, REPROVADO"
        timestamp data_solicitacao
        string documento_url
        string justificativa
    }

    USUARIO ||--o{ MUSICA : publica
    MUSICA ||--|{ ARQUIVO_AUDIO : possui
    USUARIO ||--o| SOLICITACAO_VERIFICACAO : solicita
    USUARIO ||--o{ SOLICITACAO_VERIFICACAO : avalia
```


## 3. Modelagem Comportamental

### 3.1. Fatia 1 - Upload de Áudio Lossless (Diagrama de Atividades)

**Justificativa da escolha:** O Diagrama de Atividades é o mais adequado para esta fatia, pois o upload configura um fluxo de trabalho estruturado por tomadas de decisão (validação de formato e tamanho) distribuídas em raias distintas (Interface do Artista e Servidor).

```
    subgraph Artista [Portal do Artista (Front-end)]
        A([Inicia Upload da Música]) --> B(Seleciona arquivo de áudio)
        B --> C{Tamanho <= 200MB?}
        C -- Não --> D[Exibe erro de limite de tamanho] --> Z([Fim])
        C -- Sim --> E[Preenche Metadados]
        E --> F(Submete formulário)
    end

    subgraph Backend [Servidor SoundWave]
        F --> G{Formato é FLAC/WAV?}
        G -- Não --> H[Retorna erro de formato inválido]
        H --> I[Front: Exibe erro ao artista] --> Z
        G -- Sim --> J[Salva metadados no DB]
        J --> K[Envia arquivo para Storage]
        K --> L[Enfileira job de transcodificação MP3]
    end
    L --> M([Upload Concluído - Música em Processamento])
```

### 3.2. Fatia 2 - Transcodificação Adaptativa no Streaming (Diagrama de Sequência)

**Justificativa da escolha:** A reprodução adaptativa exige troca de mensagens síncronas e assíncronas entre o dispositivo cliente, a **API** e a **CDN**. O diagrama de sequência demonstra o bloco condicional (alt) acionado em cenários de instabilidade de rede.

```
    actor Ouvinte
    participant App as App do Ouvinte
    participant API as SoundWave API
    participant CDN as Storage / CDN

    Ouvinte->>App: Clica em "Play" na Música
    App->>API: getStreamInfo(musicaId)
    API-->>App: Retorna URLs (FLAC e MP3)
    App->>CDN: Inicia buffer do FLAC (Lossless)
    
    alt Conexão Estável (4G/Wi-Fi)
        CDN-->>App: Retorna chunks FLAC
        App->>Ouvinte: Reproduz áudio alta fidelidade
    else Conexão Instável (Latência > 2s)
        App->>CDN: Aborta request FLAC
        App->>CDN: Inicia buffer do fallback (MP3)
        CDN-->>App: Retorna chunks MP3
        App->>Ouvinte: Reproduz áudio comprimido sem interrupções
    end
```

### 3.3. Fatia 3 - Ciclo de vida da Verificação (Diagrama de Estados)

**Justificativa da escolha:** A entidade `SolicitacaoVerificacao` possui um ciclo de vida estrito. O diagrama de estados expõe os gatilhos e as transições que alteram o status da aprovação dentro do sistema.

```
    [*] --> Pendente : Artista envia doc
    
    state Pendente {
        %% Aguardando ação na fila do painel administrativo
    }
    
    Pendente --> EmAnalise : Admin abre solicitação [doc legível]
    Pendente --> Cancelada : Artista exclui conta
    
    state EmAnalise {
        %% Admin validando identidade
    }
    
    EmAnalise --> Aprovado : Admin aprova
    EmAnalise --> Reprovado : Admin reprova [com justificativa]
    
    Aprovado --> [*] : Sistema aplica selo
    Reprovado --> [*] : Artista notificado
```

## 4. Casos de Teste das Fatias Modeladas

| ID | Fatia / Caso de Uso | Pré-condições | Dados de entrada | Passos | Resultado esperado | Critério de aprovação | Severidade |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-F1-01** | F1 / US-SUB1-001 | Artista autenticado. | Arquivo "som.flac" (150MB). | 1) Clica em Upload; 2) Anexa arquivo; 3) Clica Salvar. | O arquivo é recebido e o job de transcodificação é criado. | (a) Registro criado no BD; (b) Arquivo alocado no Storage. | Média |
| **TC-F1-02** | F1 / US-SUB1-001 | Artista autenticado. | Arquivo "mix.wav" (201MB). | 1) Clica em Upload; 2) Anexa arquivo. | Upload bloqueado no *client-side*. *(Teste de Fronteira)* | (a) Exibição de aviso "Tamanho excedido"; (b) Tráfego não iniciado. | Baixa |
| **TC-F2-01** | F2 / US-SUB2-006 | Ouvinte logado, conexão Wi-Fi estável. | Música ID #100. | 1) O usuário aciona o Play. | Áudio inicia em FLAC em menos de 2s. | Player reporta consumo de pacotes FLAC sem falhas. | Alta |
| **TC-F2-02** | F2 / US-SUB2-006 | Ouvinte logado, rede simulando alta latência. | Música ID #100. | 1) O usuário aciona o Play; 2) Rede é estrangulada. | Sistema ajusta a requisição para MP3. *(Caminho Crítico)* | Player altera o stream para URL do MP3 sem interromper o áudio. | Crítica |
| **TC-F3-01** | F3 / US-SUB3-001 | Administrador logado. | Solicitação do Artista X. | 1) Acessa a solicitação; 2) Confirma aprovação. | Status alterado para Aprovado; parâmetro `is_verificado` ativado. | O ícone de verificação passa a ser renderizado no perfil. | Alta |
| **TC-F3-02** | F3 / US-SUB1-005 | Artista logado com solicitação pendente. | N/A | 1) Acessa aba Verificação; 2) Tenta anexar novo doc. | Botão de submissão bloqueado. *(Transição inválida)* | (a) O sistema bloqueia duplicidade; (b) Status visualizado como pendente. | Média |

## 5. Rastreabilidade

| Fatia | Casos de Uso (T2) | Classes Envolvidas | Entidades (MER) | Diagrama Comportamental | Casos de Teste |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Fatia 1 (Upload Lossless)** | US-SUB1-001, US-SUB1-007 | `Artista`, `Musica`, `ArquivoAudio` | `USUARIO`, `MUSICA`, `ARQUIVO_AUDIO` | **Atividades** (Seção 3.1) | TC-F1-01, TC-F1-02 |
| **Fatia 2 (Streaming Adaptativo)** | US-SUB2-001, US-SUB2-006 | `Ouvinte`, `Musica`, `ArquivoAudio` | `USUARIO`, `ARQUIVO_AUDIO` | **Sequência** (Seção 3.2) | TC-F2-01, TC-F2-02 |
| **Fatia 3 (Ciclo do Selo)** | US-SUB1-005, US-SUB3-001, US-SUB2-008 | `Artista`, `Administrador`, `SolicitacaoVerificacao` | `USUARIO`, `SOLICITACAO_VERIFICACAO` | **Estados** (Seção 3.3) | TC-F3-01, TC-F3-02 |

---
