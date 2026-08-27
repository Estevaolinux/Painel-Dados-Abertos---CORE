# Painel-Dados-Abertos---CORE
O Painel de Dados Abertos do Setor Elétrico — CORE é uma aplicação analítica desenvolvida em Jupyter Notebook para consolidar, tratar, validar e apresentar informações públicas relacionadas à operação, ao mercado, à geração, à transmissão, à hidrologia e ao planejamento do setor elétrico brasileiro.

O projeto combina ingestão automatizada de dados públicos, normalização tabular, processamento temporal, indicadores executivos, gráficos interativos, cartões analíticos, filtros, detalhamento por indicador, mecanismos de contingência e exportação de dados. A interface final foi organizada para reproduzir a experiência de um produto corporativo de Business Intelligence, com menu lateral, navegação por módulos, hierarquia visual, status das fontes, visão executiva e áreas especializadas.

A solução também disponibiliza módulos independentes para consulta ao Windy, Denergia e CAMMESA, além de páginas e referências técnicas de EPE, CNPE, CMSE e MegaWhat. Esses módulos externos não substituem a camada de dados do painel; são áreas complementares e isoladas, acessadas por incorporação ou por links oficiais.

# Visão geral da solução

A arquitetura foi desenhada para separar as responsabilidades de configuração, aquisição, tratamento, visualização e apresentação. A coleta acontece nas células Python de infraestrutura e ingestão; a camada de visualização converte os DataFrames em gráficos Plotly e cards HTML; a célula de apresentação monta a aplicação completa, incorporando o HTML, o CSS, o JavaScript de navegação e os módulos externos.

A solução foi estruturada para que a camada de dados permaneça independente da camada de interface. Dessa forma, alterações no layout, na navegação ou na identidade visual dos cards não interferem nos conectores, nos DataFrames, nos filtros temporais ou nos mecanismos de exportação. Essa separação também facilita a manutenção do notebook, a inclusão de novos indicadores e a evolução do painel para outros módulos de dados públicos.

# Aquisição e tratamento dos dados
A aquisição dos dados do Operador Nacional do Sistema Elétrico é realizada por meio do catálogo público CKAN do ONS. O painel utiliza os slugs dos datasets para consultar a API, localizar os recursos tabulares disponíveis e selecionar automaticamente o arquivo mais recente. A camada de aquisição utiliza uma sessão HTTP persistente, com controle de timeout, tentativas de repetição, cache e tratamento individual de falhas para evitar que um recurso indisponível interrompa o processamento dos demais indicadores.

Após o recebimento dos arquivos, os dados são convertidos em DataFrames e submetidos à identificação automática das colunas de data e valor. O pipeline normaliza datas, valores numéricos, nomes de subsistemas, ordenação temporal e registros inválidos. O processamento também calcula o valor mais recente, a variação em relação ao período anterior, o status operacional, a frescura do dado e os textos apresentados nos indicadores executivos.

# Indicadores e organização dos cards
A aba ONS reúne informações de armazenamento, energia natural afluente, carga, custo marginal de operação, intercâmbios, CVU, transmissão, confiabilidade, subestações, capacidade de transformação e outros indicadores operacionais. Os cards foram organizados verticalmente para manter a mesma largura e facilitar a leitura em diferentes tamanhos de tela.

Cada card apresenta título, indicador principal, unidade de medida, variação percentual, status, atualização, controles de período, gráfico interativo, fonte oficial e opções de exportação. O botão Fonte oficial direciona o usuário à página do dataset no catálogo do ONS, onde ficam disponíveis todos os arquivos relacionados ao indicador. Os botões de CSV e Excel permanecem destinados à exportação do conteúdo tratado pelo próprio card.

O card de Custo Variável Unitário de Usinas Térmicas possui uma apresentação consolidada por usina e submercado, utilizando colunas ordenadas e identificação visual por região. O card de Intercâmbios entre Subsistemas foi dividido em dois cards independentes: um para a região Sul e outro para a região Nordeste. Cada um apresenta o fluxo recebendo do Sudeste acima da linha zero e o fluxo enviando para o Sudeste abaixo da linha zero, com unidade MWmed e tooltips direcionados para a região correspondente.

# Filtros, detalhamento e exportação
Os filtros de data funcionam de forma independente em cada card. O histórico necessário é carregado no backend e embutido na página, permitindo que o navegador faça a filtragem local sem depender de novas requisições externas ou de permissões CORS. Ao selecionar o período inicial e final, o painel normaliza as datas, filtra os registros, reconstrói as séries e atualiza o gráfico e a mensagem de status do card.

O painel de detalhamento permite ampliar a análise do indicador selecionado sem retirar o usuário da aba ativa. As informações de origem, período, unidade, status e disponibilidade permanecem associadas ao card. Quando o DataFrame real está disponível, os dados podem ser exportados em CSV e XLSX; em situações de contingência, o painel sinaliza a condição e evita apresentar um arquivo sintético como se fosse oficial.

# Unidades e consistência visual
As unidades são definidas por tema e transmitidas para o KPI, o eixo vertical, a legenda e o tooltip. Indicadores de carga, geração e intercâmbio utilizam unidades de potência ou energia média conforme o dataset; armazenamento utiliza percentual; CVU, CMO e PLD utilizam R$/MWh; e os demais indicadores seguem o mapeamento específico configurado no projeto. Essa abordagem elimina unidades fixas ou incompatíveis e mantém a semântica dos gráficos alinhada ao conteúdo apresentado.

# Navegação e módulos complementares
A navegação utiliza abas e painéis independentes para separar visão geral, dados operacionais, mercado, referências institucionais, meteorologia e portais complementares. O menu lateral pode ser recolhido para ampliar a área de visualização e reaberto por um botão dedicado. A preferência de exibição é preservada no navegador, mantendo uma experiência consistente durante a utilização do painel.

Os módulos Windy, Denergia e CAMMESA permanecem isolados da camada principal de ingestão. Eles oferecem acesso a mapas, índices, curvas, informações de mercado, operação e documentos externos, sempre com identificação da fonte e possibilidade de abertura direta em nova aba. As referências de EPE, CNPE, CMSE e MegaWhat complementam a consulta setorial sem substituir os dados estruturados obtidos pelo pipeline principal.

# Confiabilidade, rastreabilidade e publicação
A aplicação mantém indicação visual de sucesso, contingência, indisponibilidade e defasagem. Os mecanismos de fallback impedem que a falha de um dataset comprometa os demais cards, enquanto os links oficiais permitem verificar diretamente a origem de cada conjunto de dados. A versão final foi organizada para publicação no GitHub, com remoção de saídas temporárias do notebook, preservação das células de código e geração de pacote compactado abaixo do limite de 25 MB.

A execução recomendada deve ocorrer em ambiente Jupyter ou Google Colab com acesso à internet e às fontes oficiais. Após a execução das células de configuração, aquisição, tratamento e apresentação, o painel é montado em HTML com Plotly, CSS e JavaScript. A atualização periódica dos dados depende da disponibilidade dos portais oficiais e da execução do notebook, mantendo a transparência necessária para auditoria, manutenção e evolução do projeto.




