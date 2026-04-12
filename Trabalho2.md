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

---

### 2.3 Priorização MoSCoW (Tabela Consolidada)

Abaixo, a organização das funcionalidades conforme impacto no negócio. A priorização foi revisada para garantir **coerência entre dependências**: funcionalidades relacionadas à feature de verificação (US-SUB1-005, US-SUB2-008, US-SUB3-001) foram agrupadas na mesma categoria, pois dependem umas das outras para entregar valor.

| Categoria | IDs | Critério |
| :--- | :--- | :--- |
| **M — Must Have** | US-SUB1-001, US-SUB1-004, US-SUB2-001, US-SUB2-002, US-SUB2-006, US-SUB2-009, US-SUB3-002, US-SUB3-003, US-SUB3-005, US-SUB3-006 | Funcionalidades sem as quais a plataforma não opera ou viola obrigações legais (LGPD, segurança). |
| **S — Should Have** | US-SUB1-002, US-SUB1-003, US-SUB1-007, US-SUB1-010, US-SUB2-003, US-SUB2-004, US-SUB2-010, US-SUB3-004, US-SUB3-010 | Funcionalidades de alto valor que fortalecem a proposta central, mas não impedem o lançamento inicial. |
| **C — Could Have** | US-SUB1-005, US-SUB1-006, US-SUB1-008, US-SUB1-009, US-SUB2-005, US-SUB2-007, US-SUB2-008, US-SUB3-001, US-SUB3-007, US-SUB3-008 | Funcionalidades desejáveis que agregam diferencial competitivo, implementadas se houver capacidade no sprint. |
| **W — Won't Have** | US-SUB3-009 | Fora do escopo do MVP; pode ser considerada em versões futuras mediante validação de modelo de negócio. |

---

## 3. Levantamento de Requisitos Não Funcionais

### 3.1 Mapeamento de Requisitos Não Funcionais

Os requisitos não funcionais do SoundWave foram mapeados com base nas categorias da norma ISO/IEC 25010 (modelo de qualidade de produto de software) e nas restrições de negócio e legais identificadas durante o levantamento. A tabela abaixo apresenta o mapeamento consolidado por categoria e por subsistema, evidenciando as diferenças de exigência entre os perfis de usuário.

| ID | Categoria | Subsistema(s) | Título | Justificativa |
| :--- | :--- | :--- | :--- | :--- |
| NF-SUB2-001 | Desempenho | SUB2 | Latência de início de streaming | Experiência central do ouvinte; atrasos acima de 2s causam abandono da sessão (ISO/IEC 25010 — Eficiência de Desempenho). |
| NF-SUB1-001 | Desempenho | SUB1 | Throughput de upload de áudio | Pipeline de ingestão de arquivos FLAC/WAV de até 200 MB deve ser eficiente para não frustrar o artista durante publicação. |
| NF-ALL-001 | Escalabilidade | SUB1, SUB2, SUB3 | Suporte a acessos simultâneos | Plataforma de streaming está sujeita a picos de acesso em lançamentos; arquitetura deve escalar horizontalmente. |
| NF-SUB3-001 | Segurança | SUB3 | Autenticação multifator obrigatória | O painel administrativo acessa dados sensíveis e operações críticas (take-down, banimentos, LGPD); exige nível de segurança superior aos demais subsistemas. |
| NF-ALL-002 | Segurança | SUB1, SUB2, SUB3 | Conformidade com LGPD | Obrigação legal brasileira; impacta coleta, armazenamento e exclusão de dados de todos os usuários. |
| NF-SUB2-002 | Disponibilidade | SUB2 | Uptime do serviço de streaming | Indisponibilidade do app do ouvinte impacta diretamente a receita e a retenção de usuários. |
| NF-SUB3-002 | Disponibilidade | SUB3 | Disponibilidade do painel administrativo | Painel pode ter SLA ligeiramente inferior ao app do ouvinte, pois seu uso é interno e não contínuo. |
| NF-SUB2-003 | Usabilidade | SUB2 | Acessibilidade e curva de aprendizado | O app deve ser acessível a diferentes perfis de ouvinte, incluindo usuários com deficiência visual (WCAG 2.1). |
| NF-SUB1-002 | Usabilidade | SUB1 | Interface intuitiva para artistas | Artistas independentes podem não ter perfil técnico; o portal deve minimizar a curva de aprendizado. |
| NF-ALL-003 | Portabilidade | SUB1, SUB2 | Suporte multiplataforma | SUB2 deve funcionar em mobile (iOS/Android) e web; SUB1 prioritariamente em web desktop. SUB3 exclusivamente em web. |
| NF-SUB2-004 | Portabilidade | SUB2 | Adaptação de qualidade offline/rede instável | Mobile está sujeito a conexões instáveis; o app deve degradar graciosamente a qualidade do áudio (relacionado a US-SUB2-006). |
| NF-ALL-004 | Manutenibilidade | SUB1, SUB2, SUB3 | Integração e entrega contínua (CI/CD) | Reduz tempo de lançamento de novas features e minimiza risco de regressões em produção. |

### 3.2 Requisitos Diferenciados por Tipo de Usuário

A tabela abaixo destaca as principais diferenças de exigência entre os subsistemas, justificando por que um mesmo atributo de qualidade pode ter métricas distintas para cada grupo de usuário.

| Atributo | SUB1 — Portal do Artista (USER-001) | SUB2 — App do Ouvinte (USER-002) | SUB3 — Painel de Admin (USER-003) |
| :--- | :--- | :--- | :--- |
| **Segurança** | Autenticação padrão (usuário/senha + e-mail verificado) | Autenticação padrão (usuário/senha ou OAuth social) | **MFA obrigatório** + bloqueio após 3 tentativas + logs de auditoria completos |
| **Disponibilidade** | 99,5% (uso esporádico para uploads e analytics) | **99,9%** (uso contínuo; indisponibilidade impacta receita diretamente) | 99,0% (uso interno, horário comercial) |
| **Desempenho** | Upload assíncrono tolerável em até 30s para 200 MB | **Início de reprodução em até 2s**; adaptação de qualidade em tempo real | Respostas de painel em até 3s; operações de moderação podem tolerar latência maior |
| **Usabilidade** | Interface web desktop, perfil semi-técnico | **Acessibilidade WCAG 2.1**; interface mobile-first para público amplo | Interface web, usuários com treinamento; menor exigência de descobrabilidade |
| **Portabilidade** | Web desktop (Chrome, Firefox, Edge — últimas 2 versões) | **iOS 14+, Android 10+** e web mobile | Web desktop apenas |
| **Manutenibilidade** | Cobertura de testes ≥ 70% | Cobertura de testes ≥ 80% (maior criticidade) | Cobertura de testes ≥ 70% |

### 3.3 Detalhamento dos Requisitos Não Funcionais (Padrão IEEE-830)

---

#### NF-SUB2-001 — Latência de Início de Streaming

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-SUB2-001 |
| **Título** | Desempenho de Resposta no Streaming |
| **Descrição** | O sistema deve iniciar a reprodução de áudio (incluindo arquivos FLAC) em até 2 segundos após a solicitação do ouvinte, em condições de conexão 4G ou superior. |
| **Entrada** | Solicitação de reprodução (clique no botão Play em qualquer música). |
| **Processamento** | O sistema requisita o pacote inicial de áudio via CDN, realiza o pre-buffering dos primeiros segmentos e libera o fluxo de áudio para o player. |
| **Saída** | Áudio audível ao ouvinte e barra de progresso em movimento. |
| **Restrições** | Dependência da estabilidade e velocidade da rede do usuário final. Em conexões abaixo de 4G, aplica-se a degradação de qualidade (ver NF-SUB2-004). |
| **Critérios de Aceitação** | (a) O tempo entre o clique no Play e o início do áudio não excede 2 segundos em 95% das tentativas monitoradas. (b) Ausência de interrupções (engasgos) nos primeiros 10 segundos de reprodução após o play inicial. |

---

#### NF-SUB1-001 — Throughput de Upload de Áudio

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-SUB1-001 |
| **Título** | Desempenho de Upload de Arquivos de Áudio |
| **Descrição** | O sistema deve processar o upload de arquivos de áudio em FLAC ou WAV de até 200 MB em no máximo 30 segundos em conexões de banda larga padrão (≥ 10 Mbps de upload). |
| **Entrada** | Seleção e envio de arquivo de áudio pelo artista no Portal do Artista. |
| **Processamento** | O arquivo é transmitido ao servidor via protocolo multipart, validado quanto ao formato e tamanho, e enfileirado para transcodificação assíncrona. |
| **Saída** | Confirmação de recebimento exibida ao artista; arquivo disponível para publicação após processamento assíncrono. |
| **Restrições** | Arquivos acima de 200 MB devem ser rejeitados antes do início da transferência. O tempo de transcodificação (geração do MP3) não está incluso nos 30 segundos, por ser processo assíncrono. |
| **Critérios de Aceitação** | (a) Upload de arquivo de 200 MB concluído em até 30s em conexão de 10 Mbps em 90% das tentativas. (b) Exibição de barra de progresso durante o upload. (c) Mensagem de erro clara exibida ao artista em caso de falha ou formato inválido. |

---

#### NF-ALL-001 — Suporte a Acessos Simultâneos

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-ALL-001 |
| **Título** | Escalabilidade Horizontal sob Picos de Acesso |
| **Descrição** | A plataforma deve suportar ao menos 10.000 ouvintes simultâneos em streaming sem degradação perceptível de desempenho, com capacidade de escalonamento automático para absorver picos de até 3x esse volume em lançamentos de alto impacto. |
| **Entrada** | Aumento súbito de requisições ao serviço de streaming (ex.: lançamento de álbum de artista com grande base de fãs). |
| **Processamento** | O sistema aciona políticas de auto-scaling na infraestrutura de nuvem, adicionando instâncias de servidor conforme o volume de requisições ultrapassa thresholds predefinidos. |
| **Saída** | Tempo de resposta e latência de streaming mantidos dentro dos SLAs definidos (NF-SUB2-001) mesmo sob carga elevada. |
| **Restrições** | O escalonamento automático deve ocorrer em até 60 segundos após a detecção do pico. Custo de infraestrutura adicional deve ser monitorado para não ultrapassar o orçamento operacional. |
| **Critérios de Aceitação** | (a) Testes de carga com 10.000 usuários simultâneos não devem elevar a latência de streaming acima de 2s em mais de 5% das sessões. (b) O sistema deve escalar automaticamente sem intervenção manual quando o CPU médio das instâncias ativas ultrapassar 70% por mais de 2 minutos. |

---

#### NF-SUB3-001 — Autenticação Multifator no Painel Administrativo

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-SUB3-001 |
| **Título** | Segurança de Acesso ao Painel de Administração |
| **Descrição** | O acesso ao Painel de Administração deve exigir obrigatoriamente autenticação multifator (MFA), com bloqueio automático da conta após 3 tentativas de login malsucedidas consecutivas. |
| **Entrada** | Tentativa de login de um usuário administrador (USER-003). |
| **Processamento** | Após validação correta de usuário e senha, o sistema exige um segundo fator (código TOTP via app autenticador ou código enviado por e-mail). O sistema registra cada tentativa de login no log de auditoria com IP, timestamp e resultado. |
| **Saída** | Acesso concedido ao painel apenas após validação bem-sucedida dos dois fatores. Em caso de 3 falhas consecutivas, a conta é bloqueada e um alerta é enviado ao e-mail cadastrado. |
| **Restrições** | O bloqueio deve ser manual (requer desbloqueio por outro administrador) para evitar ataques de negação de serviço por reset automático. O segundo fator deve ser renovado a cada sessão. |
| **Critérios de Aceitação** | (a) 100% dos logins administrativos requerem o segundo fator; não há fluxo alternativo sem MFA. (b) Após 3 tentativas falhas, a conta é bloqueada imediatamente e o acesso é negado mesmo com credenciais corretas. (c) Cada tentativa de login (bem-sucedida ou não) é registrada no log de auditoria com IP e timestamp. |

---

#### NF-ALL-002 — Conformidade com LGPD

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-ALL-002 |
| **Título** | Conformidade com a Lei Geral de Proteção de Dados (LGPD) |
| **Descrição** | O sistema deve garantir que todos os dados pessoais de usuários sejam coletados com consentimento explícito, armazenados com criptografia, e definitivamente anonimizados ou eliminados mediante solicitação de exclusão, em conformidade com a Lei nº 13.709/2018. |
| **Entrada** | Cadastro de novo usuário (coleta de dados) ou solicitação formal de exclusão de dados (direito ao esquecimento). |
| **Processamento** | No cadastro: exibição de Política de Privacidade com aceite obrigatório e registro do consentimento com timestamp. Na exclusão: remoção em cascata de todos os registros pessoais identificáveis nos bancos de dados, arquivos de mídia e logs, seguida de anonimização dos dados estatísticos remanescentes. |
| **Saída** | Confirmação de consentimento armazenada. Após exclusão: envio de e-mail de confirmação ao usuário e impossibilidade de recuperação dos dados removidos. |
| **Restrições** | O processo de exclusão completa deve ser concluído em até 72 horas após a solicitação. Dados necessários para obrigações fiscais e legais podem ser retidos pelo prazo legal mínimo, devidamente isolados. |
| **Critérios de Aceitação** | (a) Nenhum dado pessoal é coletado sem registro de consentimento explícito. (b) A exclusão solicitada é concluída em até 72h, com confirmação por e-mail ao usuário. (c) Após a exclusão, nenhuma consulta ao sistema retorna dados identificáveis do usuário excluído. (d) Dados em repouso são armazenados com criptografia AES-256. |

---

#### NF-SUB2-002 — Disponibilidade do Serviço de Streaming

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-SUB2-002 |
| **Título** | Disponibilidade e Tolerância a Falhas do App do Ouvinte |
| **Descrição** | O App do Ouvinte (SUB2) deve apresentar disponibilidade mínima de 99,9% ao mês (equivalente a no máximo ~43 minutos de indisponibilidade mensal), com mecanismo de tolerância a falhas que evite interrupção de sessões em andamento. |
| **Entrada** | Qualquer acesso de ouvinte ao serviço de streaming, busca ou playlist. |
| **Processamento** | O sistema utiliza balanceamento de carga entre múltiplas instâncias e regiões de disponibilidade. Em caso de falha de um nó, o tráfego é redirecionado automaticamente para instâncias saudáveis sem interrupção perceptível ao usuário. |
| **Saída** | Serviço disponível e responsivo dentro dos SLAs de desempenho definidos (NF-SUB2-001). |
| **Restrições** | Janelas de manutenção planejadas devem ser realizadas fora do horário de pico (entre 02h e 05h, horário de Brasília) e comunicadas com 48h de antecedência. |
| **Critérios de Aceitação** | (a) Uptime mensal medido por monitoramento externo não inferior a 99,9%. (b) Falha de até 30% das instâncias ativas não deve causar interrupção de sessões de streaming em andamento. (c) Tempo de recuperação automática (failover) não excede 10 segundos. |

---

#### NF-SUB2-003 — Acessibilidade e Usabilidade do App do Ouvinte

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-SUB2-003 |
| **Título** | Acessibilidade e Usabilidade — App do Ouvinte |
| **Descrição** | O App do Ouvinte deve estar em conformidade com as diretrizes WCAG 2.1 nível AA, garantindo acessibilidade a usuários com deficiência visual, auditiva ou motora, e permitindo que um novo usuário realize sua primeira reprodução sem necessidade de tutorial ou suporte. |
| **Entrada** | Acesso de qualquer usuário ao app, incluindo usuários de tecnologias assistivas (leitores de tela, navegação por teclado). |
| **Processamento** | Todos os componentes de interface devem possuir rótulos semânticos acessíveis, contraste de cores adequado (mínimo 4,5:1 para texto normal) e navegação funcional sem uso exclusivo de mouse. |
| **Saída** | Interface utilizável via leitor de tela (VoiceOver/TalkBack) e navegação por teclado; fluxo de primeira reprodução concluído em até 3 cliques a partir da tela inicial. |
| **Restrições** | Conformidade WCAG 2.1 AA aplica-se às telas principais (busca, player, playlist). Funcionalidades secundárias devem atingir ao menos nível A. |
| **Critérios de Aceitação** | (a) Auditoria com ferramenta automatizada (ex.: Axe, Lighthouse) não aponta violações de nível AA nas telas principais. (b) Teste com usuário real utilizando leitor de tela conclui o fluxo de busca e reprodução sem bloqueios. (c) Novo usuário (sem experiência prévia) reproduz sua primeira música em até 3 cliques a partir da tela inicial em teste de usabilidade. |

---

#### NF-ALL-003 — Suporte Multiplataforma

| Campo | Descrição |
| :--- | :--- |
| **Requisito ID** | NF-ALL-003 |
| **Título** | Portabilidade e Compatibilidade Multiplataforma |
| **Descrição** | O SUB2 (App do Ouvinte) deve ser compatível com iOS 14+, Android 10+ e navegadores web modernos. O SUB1 (Portal do Artista) deve funcionar em navegadores web desktop. O SUB3 (Painel Admin) é exclusivo para web desktop. |
| **Entrada** | Acesso de qualquer usuário a partir de seu dispositivo ou navegador. |
| **Processamento** | O front-end do SUB2 é desenvolvido em framework mobile multiplataforma (ou web responsivo); o SUB1 e SUB3 são aplicações web responsivas testadas nos navegadores-alvo. |
| **Saída** | Interface funcional e visualmente consistente em todos os ambientes suportados, sem quebras de layout ou perda de funcionalidade. |
| **Restrições** | SUB3 não precisa ser responsivo para mobile; seu uso em smartphones não é um requisito suportado. Versões de navegadores mais antigas que as 2 últimas versões estáveis não precisam ser suportadas. |
| **Critérios de Aceitação** | (a) Todos os fluxos críticos do SUB2 funcionam sem erros em iOS 14+, Android 10+, Chrome e Safari (últimas 2 versões). (b) SUB1 e SUB3 funcionam sem erros em Chrome, Firefox e Edge (últimas 2 versões) em resolução desktop (≥ 1280px). (c) Nenhum componente de interface depende exclusivamente de tecnologia não suportada pelos ambientes-alvo (ex.: Flash, ActiveX). |

---

## 4. Referências

IEEE STD 830-1998. **IEEE Recommended Practice for Software Requirements Specifications**. New York: Institute of Electrical and Electronics Engineers, 1998.

ISO/IEC 25010:2011. **Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models**. Genebra: International Organization for Standardization, 2011.

BRASIL. **Lei nº 13.709, de 14 de agosto de 2018**. Lei Geral de Proteção de Dados Pessoais (LGPD). Diário Oficial da União, Brasília, DF, 15 ago. 2018. Disponível em: https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm. Acesso em: abr. 2026.
