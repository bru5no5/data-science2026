# data-science2026

Aluno: Bruno Gustavo Rocha

RA: 10400926

[Link para o GitHub](https://github.com/bru5no5/data-science2026)

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

## Limpeza e transformacao dos dados

O notebook `notebook/limpeza_transformacao.ipynb` aprofunda o trabalho iniciado na exploracao inicial. Antes de aplicar os tratamentos, ele cria visualizacoes para destacar problemas potenciais nos dados, como valores ausentes, discrepancias, duplicatas, inconsistencias de formato e diferencas de escala entre variaveis numericas.

Nesta etapa, foram realizadas as seguintes atividades:

1. Carregamento dos tres datasets a partir de `data/raw`.
2. Diagnostico inicial com contagem de nulos, duplicatas, tipos de dados e dimensoes das tabelas.
3. Visualizacao dos problemas antes da limpeza, com:
   - heatmaps e graficos de barras para valores ausentes
   - boxplots e histogramas para valores discrepantes
   - grafico de barras para duplicatas por dataset
   - verificacao de inconsistencias entre `shopping_mall` em `sales` e `shopping`
   - comparacao de escalas numericas e cardinalidade de variaveis categoricas
4. Remocao de duplicatas completas em cada dataset.
5. Padronizacao de formatos e nomes de colunas.
6. Tratamento de valores discrepantes com regras explicitas.
7. Tratamento de valores ausentes e inconsistencias remanescentes.
8. Validacao entre os datasets para garantir consistencia das chaves.
9. Aplicacao de transformacoes para preparar os dados para etapas futuras de analise ou modelagem.
10. Exportacao dos arquivos finais tratados em `data/processed`.

### Logica adotada para a limpeza

As decisoes de limpeza seguiram uma logica simples, objetiva e reproduzivel:

- Duplicatas: qualquer linha completamente repetida foi removida com `drop_duplicates()`.
- Padronizacao textual: identificadores como `customer_id` e `invoice_no` foram convertidos para maiusculas; colunas categoricas textuais foram normalizadas com remocao de espacos extras e padronizacao de capitalizacao.
- Padronizacao de colunas: `invoice date` foi renomeada para `invoice_date` e `area (sqm)` para `area_sqm`, facilitando a manipulacao posterior.
- Conversao de tipos: colunas numericas foram convertidas com `pd.to_numeric()` e datas com `pd.to_datetime()`.
- Correcao de inconsistencias: o valor `Irvine Spectrum` presente em `sales` foi padronizado para `Irvine Spectrum Center`, permitindo o cruzamento correto com o dataset de shopping centers.

### Regras de tratamento adotadas

Os tratamentos foram aplicados com base em regras de plausibilidade e consistencia:

- `age`: valores fora do intervalo de `0` a `100` foram considerados invalidos e convertidos para nulo antes do preenchimento.
- `quantity`: valores menores ou iguais a zero foram tratados como invalidos e removidos.
- `price`: valores menores ou iguais a zero foram tratados como invalidos e removidos.
- `construction_year`: valores fora do intervalo entre `1900` e o ano atual foram tratados como invalidos.
- `area_sqm` e `store_count`: valores menores ou iguais a zero foram tratados como invalidos.
- Nulos em `age`: foram preenchidos com a mediana da coluna, preservando uma medida robusta da distribuicao.
- Nulos em colunas essenciais de vendas e shopping centers: linhas com campos criticos ausentes foram removidas.

### Transformacoes aplicadas

Depois da limpeza, o notebook tambem aplica transformacoes para enriquecer os datasets:

- Escalonamento e normalizacao:
  - `age`, `quantity`, `price`, `area_sqm` e `store_count` receberam versoes em `min-max` e `z-score`.
- Codificacao de categorias:
  - variaveis como `gender`, `payment_method`, `category` e `location` foram convertidas em colunas binarias com `pd.get_dummies()`.
- Geracao de novas variaveis:
  - em `sales`, foram criadas as colunas `valor_total_compra`, `preco_unitario_estimado`, `ano_compra`, `mes_compra` e `trimestre_compra`.
  - foi gerado um resumo agregado de vendas por shopping, e a coluna `vendas_por_shopping` foi incorporada ao arquivo final `shopping_mall_data_clean.xlsx`.

### Arquivos finais gerados

Ao final do notebook, os tres datasets consolidados sao exportados em `data/processed`:

- `customer_data_clean.xlsx`
- `sales_data_clean.xlsx`
- `shopping_mall_data_clean.xlsx`

Esses arquivos finais ja reunem tanto as etapas de limpeza quanto as transformacoes aplicadas em cada dataset.
