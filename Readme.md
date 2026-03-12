# 1. Visão Geral do Produto
## 1.1 Declaração do Problema e Oportunidade de Negócio 

  Com o amplo domínio de plataformas de streaming de música,
  onde usuários são guiados por um algoritmo tendensioso à eleger artistas de grandes labels como mais influentes e portanto mais recomendável,
  artistas independentes vivenciam dificuldades em disponibilizar suas músicas para o público sem depender de grandes gravadoras. 
  Por outro lado, nichos de ouvintes buscam descobrir novos artistas e músicas de forma simples e organizada.
  
  A SoundWave possui uma proposta diferente, agregando valor aos artistas independentes, 
  difundindo suas músicas em comunidades através do gênero da música e alcançando ouvintes interessados em escutar músicas do mesmo gênero,
  sem se importar com relevância de gravadoras. E para os ouvintes interessados em sempre conhecer novos artistas em seus gêneros de músicas preferidos, 
  este app se torna um prato cheio.

  Em relação ao potêncial comercial, o SoundWave busca se tornar uma plataforma de tamanho médio,
  onde sua receita será oriunda de anúncios e alcance por música,
  assim gerando rentabilidade e crescimento organico no médio/longo prazo.

## 1.2 Perspectiva do Produto 

  Frente à grandes softwares já estabelecidos no mercado, onde grandes labels/gravadoras possuem vantagem competitiva em ranking de sugestão de músicas por serem mais recomendadas por um algoritmo tendencioso, o SoundWave se destaca pela personalização, entregando uma melhor experiência ao artista que não possui uma grande equipe para gerir sua carreira e que deseja alcançar um público através da correlação entre gostos musicais.
  
  O público-alvo a qual desejamos atacar, são artistas independentes com pequenas/média ou nenhuma equipe de apoio, que deseja acompanhar o crescimento de sua carreira de maneira um pouco mais detalhada, recebendo simples relatórios de seus ouvintes, e que deseja alcançar nichos de ouvintes que escutam gêneros músicais semelhantes ao seu estilo.

## 1.3 Capacidades do Produto

* Dashboard de Analytics em Tempo Real
  
>   Através deste dashboard usuários com média/baixa familiaridade com tecnologia conseguirá acompanhar a performance de sua música e entender qual o público impactado.

* Gerenciador de Lançamentos

>  Esta ferramenta auxiliará o usuário a programar lançamentos de forma automática e intuitiva.

* Área para links externos / sobre mim

>  Através desta ferramenta, artistas conseguem divulgar sua história, redes sociais e sites para vendas de ingressos dos seus próximos shows.

* Área/Selo de Verificados

>  Servindo tanto como uma forma de segurança de propriedade autoral como um selo que assegura que tal artista é reconhecido pela plataforma essa feature impacta diretamente na experiência tanto os ouvintes quanto os artistas.

* Motor de Busca com Filtros por Nicho

>   Este sendo o Core do negócio, um motor de buscas otimizado para recomendar ao usuário músicas semelhantes ao seu gosto musical impacta diretamente a experiência de uso do software.

* Sistema de "Curtição" (Like) e Favoritos

>   Auxiliando tanto o usuário, criando uma playlist de favoritos, quanto ao algoritmo de recomendação de músicas essa feature também faz parte do core do negócio.

* Painel de Cadastro de usuário

>    Esta feature impacta diretamente na segurança de uso no aplicativo, e garante a não criação de contas falsas, além de personalizar o uso do app tanto para o caso do artista quanto para o ouvinte.

# 2. Descrição dos Usuários

<table border="1" style="width:100%; border-collapse: collapse; font-family: Arial, sans-serif; font-size: 14px;">
  <thead>
    <tr style="background-color: #2c3e50; color: white;">
      <th style="padding: 10px;">Atributo</th>
      <th style="padding: 10px;">Artista Independente (USER-001)</th>
      <th style="padding: 10px;">Ouvinte (USER-002)</th>
      <th style="padding: 10px;">Administrador (USER-003)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 8px; font-weight: bold; background-color: #f2f2f2;">Descrição</td>
      <td style="padding: 8px;">Músico ou produtor que publica conteúdo autoral.</td>
      <td style="padding: 8px;">Usuário final que consome e organiza músicas.</td>
      <td style="padding: 8px;">Profissional responsável pela manutenção e segurança.</td>
    </tr>
    <tr>
      <td style="padding: 8px; font-weight: bold; background-color: #f2f2f2;">Experiência Técnica</td>
      <td style="padding: 8px;">Média; familiaridade com formatos de áudio e metadados.</td>
      <td style="padding: 8px;">Básica; usuário comum de aplicativos móveis.</td>
      <td style="padding: 8px;">Alta; conhecimento avançado em TI e bancos de dados.</td>
    </tr>
    <tr>
      <td style="padding: 8px; font-weight: bold; background-color: #f2f2f2;">Frequência de Uso</td>
      <td style="padding: 8px;">Ocasional (uploads) a Regular (análise de dados).</td>
      <td style="padding: 8px;">Alta; uso diário para reprodução de áudio.</td>
      <td style="padding: 8px;">Regular; monitoramento e suporte contínuo.</td>
    </tr>
    <tr>
      <td style="padding: 8px; font-weight: bold; background-color: #f2f2f2;">Principais Objetivos</td>
      <td style="padding: 8px;">Divulgar trabalho e analisar métricas de alcance.</td>
      <td style="padding: 8px;">Descobrir novos artistas e organizar playlists.</td>
      <td style="padding: 8px;">Gerenciar permissões e garantir integridade do sistema.</td>
    </tr>
    <tr>
      <td style="padding: 8px; font-weight: bold; background-color: #f2f2f2;">Desafios</td>
      <td style="padding: 8px;">Complexidade no upload de arquivos grandes (WAV/FLAC).</td>
      <td style="padding: 8px;">Encontrar conteúdos novos fora do mainstream.</td>
      <td style="padding: 8px;">Acesso rápido a informações críticas e logs.</td>
    </tr>
    <tr>
      <td style="padding: 8px; font-weight: bold; background-color: #f2f2f2;">Restrições</td>
      <td style="padding: 8px;">Pode gerenciar apenas o próprio catálogo.</td>
      <td style="padding: 8px;">Acesso limitado a funções administrativas.</td>
      <td style="padding: 8px;">Exige autenticação multifator (MFA) para segurança.</td>
    </tr>
    <tr>
      <td style="padding: 8px; font-weight: bold; background-color: #f2f2f2;">Requisitos Principais</td>
      <td style="padding: 8px;">Dashboard de estatísticas e gestor de uploads.</td>
      <td style="padding: 8px;">Player estável e motor de busca eficiente.</td>
      <td style="padding: 8px;">Painel de controle, relatórios e logs de auditoria.</td>
    </tr>
  </tbody>
</table>

# 3. Restrições do Projeto e do Produto


# 4. Tecnologias e Regulamentações
## 4.1 Tecnologia e Padrões 
## 4.2 Legislação e Regulamentações
# 5. Análise de Riscos e Mitigação 
