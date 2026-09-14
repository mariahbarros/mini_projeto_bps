
1) INFORMAÇÕES

---

1.1) Objetivo do projeto:
Analisar as aquisições de medicamentos e dispositivos médicos pelo Ministério da Saúde entre os anos de 2020 e 2026 por meio dos dados registrados no Banco de Preços em Saúde (BPS), obtidos no site https://dadosabertos.saude.gov.br/dataset/bps.


1.2) Contextualização do problema:
Sumariamente, o BPS contém informações relativas à data, instituições beneficiárias localizadas em diversos municípios do país, o tipo de medicamento e/ou dispositivo médico, o fabricante, distribuidor, quantidade adquirida e preços.
O banco de dados está criado com as seguintes colunas: ano_compra, nome_instituição, esfera, cnpj_instituicao, municipio_instituicao, uf, compra, insercao, codigo_br, descricao_catmat, unidade_fornecimento, generico, anvisa, modalidade_compra, capacidade, unidade_medida, unidade_fornecimento_capacidade, cnpj_fornecedor, fornecedor, cnpj_fabricante, fabricante, qtd_itens_comprador, preco_unitario e preco_total.


1.3) Fonte dos dados:
Os dados e o dicionário foram obtidos no site do Ministério da Saúde (https://dadosabertos.saude.gov.br/dataset/bps).


1.4) Procedimentos utilizados para baixar e concatenar as bases anuais:

- as planilhas de todos os anos foram baixadas no computador;
- a concatenação dos dados foi realizada em um notebook via Python;
- como o dataset concatenado tinha tamanho superior ao suportado pelo GitHub, foi utilizado o comando GIT LFS para inseri-lo no depositório https://github.com/mariahbarros/mini_projeto_bps.git
- arquivo que concatenou os dados: projeto_bps__concatenacao.ipynb.



1.5) Tratamentos e transformações realizados nos dados:

- a análise e o tratamento dos dados foram realizados no arquivo: projeto_bps_AED.



1.6) Descrição das principais colunas utilizadas:

- colunas mais utilizadas: 'compra', 'descricao_catmat', 'qtd_itens_comprados', 'preco_unitario'.



1.7) Definição dos KPIs e das métricas:

Em uma primeira análise: quais os produtos mais vendidos, os produtos mais caros e a soma do preço total. Foi observada a inserção equivocada de valores (tanto na coluna 'preco_unitario', quanto na 'preco_total'), o que gerou a criação de outliers que, ao meu ver, descaracterizaram a realidade. A soma dos gastos totais (com outliers), durante os 7 anos analisados, resultou no valor aproximado de R$ 1,5 milhão de reais, mas são as exceções. Assim, por se tratar de um banco de dados públicos, gerados pelo governo federal, optei por não tratar esses outliers. Se estivéssemos em um caso concreto, solicitaria a revisão dos valores declarados para, somente após as devidas retificações, ser realizada uma análise para gerar resultados mais críveis. Portanto, o dashboard foi elaborado com foco na quantidade de produtos, não no valor.



1.8) Links ou imagens:

- link repositório: https://github.com/mariahbarros/mini_projeto_bps.git
- link banco de dados utilizado para a criação do dashboard: https://docs.google.com/spreadsheets/d/1CXoSEo5r89a_VyIkNETBd7gtd6b25JFkZ7cJo4lBFd8/edit?usp=sharing
- link dashboard: https://datastudio.google.com/reporting/22c1d190-f3b1-4f01-8944-8f75f511415b



1.9) Principais análises e descobertas:

- após carregamento da base de dados, foram analisadas as informações sobre o tipo dos dados, nulidades e duplicatas;
- tratamento das informações: (a) alteração das colunas 'compra' e 'insercao' para datetime, (b) alteração da coluna 'anvisa' para string;
- remoção de 19 linhas duplicadas;
- tratamento das nulidades: (a) nenhuma coluna foi deletada, (b) alteração para "Não informado" nas colunas tipo string (para visualização no dashboard) / "Nan" para colunas numéricas / "Nat" para colunas datetime, (c) inclusão do CNPJ na coluna 'nome_instituição', conforme cruzamento de dados;
- informações estatísticas das colunas 'preco_unitario', 'preco_total' e 'qtd_itens_comprados':
- obtenção dos IQR's para lidar com outliers:
  	'preco_unitario': 47654 outliers (13.91%)
  		Limites: [-9.87, 17.40]
  	'preco_total': 52006 outliers (15.18%)
  		Limites: [-17750.00, 31450.00]
  	'qtd_itens_comprados': 58503 outliers (17.07%)
  		Limites: [-17375.00, 29625.00]

* Por se tratar de contratos públicos, que são firmados por licitação, dispensa fundamentada, critérios de melhor preco, entre outras características especificas, optei por não tratar os outliers. É possível verificar que muitos valores estão dentro do razoável, mas foram inseridos no sistema de maneira equivocada (sem casa decimal, com dígitos a mais, etc.). Por outro lado, verificou-se a razoabilidade de medicamentos que ultrapassam R$ 1,5 milhão, conforme rápida pesquisa de mercado. Esses valores, embora 'corretos', também influenciam negativamente no desvio padrão do conjunto analisado. Assim, conclui-se não ser conveniente alterar qualquer valor, mas excluído da análise em geral, deixando clara essa informação. o ideal, neste caso, seria revisar todos os valores e atualizar o conjunto de dados para que se possa ter uma analise mais fidedigna. Assim, decidiu-se, no presente estudo, realizar uma análise mais conservadora, justamente por se tratar de órgãos públicos.



1.10) Recomendações baseadas nos dados:

- realização de uma auditoria em relação aos valores das compras;
- realização de uma padronização rigorosa nas operações de inclusão e manutenção de informações no banco de dados.



1.11) Limitações identificadas na base ou na análise:
o data studio não aceita arquivos maiores que 100MB. Para tanto, foi efetuada a divisão do arquivo em 2 e a devida mesclagem no google sheets.



1.12) Instruções para reprodução do projeto:
*** IMPORTANTE:
Este repositório utiliza **Git LFS (Large File Storage)** para versionar o arquivo de dados unificado, que ultrapassa 100MB.
Como abrir a base de dados:

1. Instale o Git LFS: https://git-lfs.github.com
2. Clone o repositório:
   bash
   git lfs install
   git clone https://github.com/mariahbarros/mini_projeto_bps.git
3. Abra o notebook em notebook/projeto_bps.ipynb — a base de dados já estará disponível em dados/BPS_20_26_MariaHelena.csv.
   Se você já clonou o repositório **sem** ter o Git LFS instalado, rode o comando abaixo dentro da pasta clonada para baixar o conteúdo real dos arquivos:
   bash
   git lfs pull

==================================================================================

2) QUESTIONAMENTOS

---

2.1) Qual é o objetivo do dashboard?
Em um primeiro momento, o objetivo é analisar os gastos com a saúde pela Administração Pública (Ministério da Saúde) entre os anos de 2020 e 2026.



2.2) Qual problema de análise ou gestão pública está sendo investigado?
A ideia seria investigar como o dinheiro público está sendo gasto na saúde pela Administração Federal. No entanto, a falta de padronização na inserção das informações no banco de dados, principalmente as relacionadas aos valores das aquisições, restou prejudicada a intenção inicial.



2.3) Como os arquivos do BPS de 2020 a 2026 foram obtidos e consolidados?
Os arquivos foram obtidos diretamente do site do BPS/Ministério da Saúde, concatenados e tratados em Python, salvos no google sheets para, finalmente, serem analisados no data studio.



2.4) Quais tratamentos foram realizados na base?
Em Python: tratados os tipos (dados das colunas de data transformados em datetime e da coluna 'anvisa' em string), excluídas as duplicatas (19 linhas) e tratadas as nulidades. Durante a AED, foram descobertos os outliers e calculados os IQR's para obtenção de valores de referência para filtragem da somatória do total dos preços no dashboard (somatório sem outliers).



2.5) Como o usuário deve utilizar os filtros e visuais?
Passar o mouse sobre os gráficos para obtenção de informação sobre valores.



2.6) Quais KPIs foram desenvolvidos?

- maioria das aquisições foram feitas via licitação;
- preferência pela aquisição de medicamentos genéricos.



2.7) Quais foram os principais resultados encontrados?

- tabela "Os 5 produtos com os maiores preços" já demonstra de antemão a inconsistência dos valores;
- os 2 cards nos mostram a somatória (e diferença significativa) dos valores com e sem os outliers;
- verifica-se que o pregão é a modalidade mais utilizada pela Administração Pública para a aquisição de insumos para a Saúde. A dispensa e outras formas são exceção. Isso é importante para corroborar com a regularidade dos processos licitatórios;
- a tabela "Os 5 produtos mais adquiridos" nos traz uma noção dos produtos mais adquiridos, e seus respectivos valores, pelo Ministério da Saúde;
- o mapa nos traz informações sobre as regiões mais beneficiadas. O Estado de São Paulo e a região sul do país são os que mais adquiriram medicamentos e insumos médicos. Interessante observar que nenhum ente do Estado do Amazonas foi beneficiado;
- a farmacêutica Prati é a maior fabricante e fornecedora de produtos durante o período analisado, embora sua participação não ultrapasse 15% dos contratos firmados;
- os medicamentos genéricos foram mais adquiridos que os medicamentos de referência (de marca). É um bom sinal, pois aqueles tendem a ser mais baratos. Os valores não informados podem se referir aos insumos médicos, que não entram nessa divisão.



2.8) Quais recomendações podem ser elaboradas a partir dos dados?
Padronização e maior atenção à manipulação e manutenção dos dados relativos aos gastos públicos.



2.9) Como as tarefas foram organizadas antes do início do desenvolvimento?
Análise geral das planilhas, tratamento em python, análise em data studio, versionamento concomitante das ações no GitHub.



2.10) Você acha que faltou algo no seu código que você poderia melhorar?
Com certeza! Principalmente, a análise de valores, que seria fundamental. A falta de padronização na inserção dos valores do preços (unitário e total) prejudicou de sobremaneira o presente estudo, pois são informações essenciais para a verificação dos gastos públicos. Ademais, gostaria também de verificar se as contratações com a Prati foram por meio de licitação (para esclarecimentos em relação à sua "hegemonia" no fornecimento dos produtos).
