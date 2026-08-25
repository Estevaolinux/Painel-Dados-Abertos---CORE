# Painel-Dados-Abertos---CORE
O Painel de Dados Abertos do Setor Elétrico — CORE é uma aplicação analítica desenvolvida em Jupyter Notebook para consolidar, tratar, validar e apresentar informações públicas relacionadas à operação, ao mercado, à geração, à transmissão, à hidrologia e ao planejamento do setor elétrico brasileiro.

O projeto combina ingestão automatizada de dados públicos, normalização tabular, processamento temporal, indicadores executivos, gráficos interativos, cartões analíticos, filtros, detalhamento por indicador, mecanismos de contingência e exportação de dados. A interface final foi organizada para reproduzir a experiência de um produto corporativo de Business Intelligence, com menu lateral, navegação por módulos, hierarquia visual, status das fontes, visão executiva e áreas especializadas.

A solução também disponibiliza módulos independentes para consulta ao Windy, Denergia e CAMMESA, além de páginas e referências técnicas de EPE, CNPE, CMSE e MegaWhat. Esses módulos externos não substituem a camada de dados do painel; são áreas complementares e isoladas, acessadas por incorporação ou por links oficiais.

# Visão geral da solução

A arquitetura foi desenhada para separar as responsabilidades de configuração, aquisição, tratamento, visualização e apresentação. A coleta acontece nas células Python de infraestrutura e ingestão; a camada de visualização converte os DataFrames em gráficos Plotly e cards HTML; a célula de apresentação monta a aplicação completa, incorporando o HTML, o CSS, o JavaScript de navegação e os módulos externos.


