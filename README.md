# data-science2026

## Exploracao inicial dos dados

O notebook `notebook/exploracao_inicial.ipynb` apresenta uma primeira analise exploratoria dos tres datasets do projeto:

- `customer_data.xlsx`
- `sales_data.xlsx`
- `shopping_mall_data.xlsx`

Nesta etapa, foram realizadas as seguintes atividades:

1. Carregamento dos dados com `pandas`.
2. Visualizacao inicial das tabelas com `head()`, para entender o formato e o conteudo das colunas.
3. Inspecao da estrutura dos datasets com `info()`, verificando tipos de dados e valores ausentes.
4. Geracao de estatisticas descritivas com `describe()` para resumir as variaveis numericas.
5. Criacao de um grafico de dispersao entre `quantity` e `price` no conjunto de vendas, para observar a relacao entre quantidade comprada e preco.
6. Criacao de um grafico de linhas com os valores de `price`, para visualizar a variacao dos precos ao longo das observacoes.
7. Criacao de um boxplot das idades dos clientes, permitindo identificar dispersao, mediana e possiveis outliers.
8. Contagem das categorias de produtos em `sales_df["category"]`.
9. Criacao de um grafico de barras com a frequencia de vendas por categoria.
10. Cruzamento entre os dados de vendas e de shopping centers por meio da coluna `shopping_mall`, seguido da criacao de um grafico de dispersao com:
    - eixo x: area do shopping
    - eixo y: preco medio das vendas
    - cor: localizacao
    - tamanho da bolha: quantidade de lojas

Essa exploracao inicial ajuda a entender a composicao dos dados, o comportamento das variaveis numericas e algumas relacoes importantes entre vendas, clientes e shopping centers.
