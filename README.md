# MVP_PUC
# MVP Sprint: Engenharia de Dados

## Objetivo
### O Objetivo é ter a resposta de:   
1 - Qual o Preço médio dos últimos 6 meses do produtos hortifruti nos Principais Estados do Brasil  
2 - Qual o valor médio dos produtos hortifruti mês a mês no ano de 2024   
3 - Qual o Estado com os maiores custos de produtos unitários de hortifruti do brasil  
4 - Qual a variação mês a mês dos produtos de hortifruti no ano de 2024  
5 - Qual Ceasa com o maior Preço médio dos últimos 6 meses da Maça no brasil  
6 - Qual o item com maior variação em junho de 2024  
7 - Qual a correlação do Dolar nos custos dos produtos de hortifrut  
8 - Qual insumo foi mais impactado com as movimentações do dolar 


## Coleta dos Dados


## Armazenamento na nuvem dos dados coletados


## Modelagem

### Para essa Modelagem utilizo a Arquitetura Medalhão

### CAMADA BRONZE


#### Criação da Camada Bronze 


#### Tratamento Base Bronze

##### Carregamento dos arquivos armazenados no Datalake na pasta bronze para modelagem 

##### Tratamento na Base para inserção na tabela bronze

#### Salvando arquivo Bronze no Data Lake

##### Para salvar um arquivo no Azure Data Lake como um Delta Table usando Spark, é necessário converter o DataFrame pandas em um DataFrame Spark.  
##### Isso ocorre porque as operações de leitura e escrita no Azure Data Lake são realizadas utilizando a API do Spark.

#### Criação da tabela bronze

#### Inserindo dados na tabela bronze

##### Algumas consultas de teste das tabelas


#### Catálogo de Dados (CAMADA BRONZE)

##### Tabela Bronze: Fato_hortigrangeiros

| Coluna        | Descrição                                 | Tipo   |linhas   |Valores Nulos| Comentário                                      |
| ------------- | ----------------------------------------- | ------ |---------|-------------|----------------------------------------------- |
| Produto       | Nome do produto (FK para dimensao_produto)| string | 279.283 | 0           |Nome do Produto de Hortifruti Chave estrangeira referenciando dimensao_produto pelo nome |
| Fornecedor    | Nome do fornecedor                        | string | 279.283 | 0           |Nome do Ceasa que pratica aquele preço                     |
| UF            | Unidade Federativa do fornecedor          | string | 279.283 | 0           |Estado (UF) do fornecedor (ex: SP, RJ)                     |
| Data          | Data do Preço Preço do produto            | string | 279.283 | 0           |Data no formato string / Data do preço praticado no dia |
| Preco_Medio   | Preço médio do produto                    | string | 279.283 |163.699      |Preço médio em reais (R$), com duas casas decimais/ Preço do Produto praticado pelo Ceasa no Dia / Contém valores Nulos, pois nem todos os dias os Ceasas enviam seus Preços práticados|

##### Tabela Bronze: dimensao_produto

| Coluna        | Descrição         | Tipo   |linhas   |Valores Nulos| Comentário                                      |
| ------------- | ----------------- | ------ |---------|-------------| ----------------------------------------------- |
| Nome_Produto  | Nome do produto (PK para Fato_hortigrangeiros)   | string | 48 | 0           | Chave Primária referenciando dimensao_produto pelo nome        |
| Unidade       | Unidade de Medida | string | 48 | 0           | Unidade de Medida do Produto (Untilizado para identificar na tabela Fato qual unidade de medida o Preço está se referenciando)    |


#### Exemplo de Dados

##### Tabela Bronze: Fato_hortigrangeiros

| Produto     | Fornecedor  | UF  | Data       | Preco_Medio |
| ----------- | ----------- | --- | ---------- | ----------- |
| Produto A   | Fornecedor A | SP  | 2024-07-01 | 10.00       |
| Produto B   | Fornecedor B | RJ  | 2024-07-02 | 20.00       |
| Produto C   | Fornecedor C | MG  | 2024-07-03 | 30.00       |
| Produto D   | Fornecedor D | ES  | 2024-07-04 | 40.00       |

##### Tabela Bronze: dimensao_produto

| Produto | Unidade |
| ------------ | --------- |
| Produto A    | KG
| Produto B    | DZ
| Produto C    | UND
| Produto D    | KG

### CAMADA SILVER

#### Criação da camada Silver

#### Tratamento Base Silver

#### Criação da tabela Silver

#### Salvando Base no Directory Silver da Azure Datalake

#### Inserindo dados na tabela Silver

##### Algumas consultas de teste das tabelas

#### Catálogo de Dados (CAMADA SILVER)

##### Tabela Silver: Fato_hortigrangeiros

| Coluna        | Descrição                                 | Tipo   |linhas   |Valores Nulos| Comentário                                      |
| ------------- | ----------------------------------------- | ------ |---------|-------------|----------------------------------------------- |
| Produto       | Nome do produto (FK para dimensao_produto)| string | 115.584 | 0           |Nome do Produto de Hortifruti Chave estrangeira referenciando dimensao_produto pelo nome |
| Fornecedor    | Nome do fornecedor                        | string | 115.584 | 0           |Nome do Ceasa que pratica aquele preço                     |
| UF            | Unidade Federativa do fornecedor          | string | 115.584 | 0           |Estado (UF) do fornecedor (ex: SP, RJ)                     |
| Data          | Data do Preço Preço do produto            | Date   | 115.584 | 0           |Data no formato YYYY-MM-DD / Data do preço praticado no dia/ Dados do dia 2024-01-02 a 2024-06-26|
| Preco_Medio   | Preço médio do produto                    | Double | 115.584 | 0           |Preço médio em reais (R$), com duas casas decimais/ Preço do Produto praticado pelo Ceasa no Dia /Valores Nulos Retirados /Min = 0,5 e Max = 364 |

##### Tabela Silver: dimensao_produto

| Coluna        | Descrição         | Tipo   |linhas   |Valores Nulos| Comentário                                      |
| ------------- | ----------------- | ------ |---------|-------------| ----------------------------------------------- |
| Nome_Produto  | Nome do produto (PK para Fato_hortigrangeiros)   | string | 48 | 0           | Chave Primária referenciando dimensao_produto pelo nome        |
| Unidade       | Unidade de Medida | string | 48 | 0           | Unidade de Medida do Produto (Untilizado para identificar na tabela Fato qual unidade de medida o Preço está se referenciando)    |


#### Exemplo de Dados

##### Tabela Silver: Fato_hortigrangeiros

| Produto     | Fornecedor  | UF  | Data       | Preco_Medio |
| ----------- | ----------- | --- | ---------- | ----------- |
| Produto A   | Fornecedor A | SP  | 2024-07-01 | 10.00       |
| Produto B   | Fornecedor B | RJ  | 2024-07-02 | 20.00       |
| Produto C   | Fornecedor C | MG  | 2024-07-03 | 30.00       |
| Produto D   | Fornecedor D | ES  | 2024-07-04 | 40.00       |

##### Tabela Silver: dimensao_produto

| Produto | Unidade |
| ------------ | --------- |
| Produto A    | KG
| Produto B    | DZ
| Produto C    | UND
| Produto D    | KG


### CAMADA GOLD

#### Criação da camada GOLD

#### Tratamento Base Gold

#### Criação da tabela Gold

#### Salvando Base no Directory Gold da Azure Datalake

#### Inserindo dados na tabela Gold

##### Algumas consultas de teste das tabelas

#### Catálogo de Dados (CAMADA GOLD)

##### Tabela Gold: Fato_hortigrangeiros

| Coluna        | Descrição                                 | Tipo   |linhas   |Valores Nulos| Comentário                                      |
| ------------- | ----------------------------------------- | ------ |---------|-------------|----------------------------------------------- |
| Produto       | Nome do produto (FK para dimensao_produto)| string | 115.584 | 0           |Nome do Produto de Hortifruti Chave estrangeira referenciando dimensao_produto pelo nome |
| Fornecedor    | Nome do fornecedor                        | string | 115.584 | 0           |Nome do Ceasa que pratica aquele preço                     |
| UF            | Unidade Federativa do fornecedor          | string | 115.584 | 0           |Estado (UF) do fornecedor (ex: SP, RJ)                     |
| Data          | Data do Preço Preço do produto            | Date   | 115.584 | 0           |Data no formato YYYY-MM-DD / Data do preço praticado no dia/ Dados do dia 2024-01-02 a 2024-06-26|
| Preco_Medio   | Preço médio do produto                    | Double | 115.584 | 0           |Preço médio em reais (R$), com duas casas decimais/ Preço do Produto praticado pelo Ceasa no Dia /Valores Nulos Retirados /Min = 0,5 e Max = 364 |
| Ano_Mes       | Ano e Mês agrupados                       | string | 115.584 | 0           |Agrupamento das datas em Ano e mês/ Dados de Jan a Jun (Jun até dia 26)               |

##### Tabela Gold: dimensao_produto

| Coluna        | Descrição         | Tipo   |linhas   |Valores Nulos| Comentário                                      |
| ------------- | ----------------- | ------ |---------|-------------| ----------------------------------------------- |
| Nome_Produto  | Nome do produto (PK para Fato_hortigrangeiros)   | string | 48 | 0           | Chave Primária referenciando dimensao_produto pelo nome        |
| Unidade       | Unidade de Medida | string | 48 | 0           | Unidade de Medida do Produto (Untilizado para identificar na tabela Fato qual unidade de medida o Preço está se referenciando)    |

##### Tabela Gold: totalizadora_hortigrangeiros

| Coluna           | Descrição                                 | Tipo   |linhas   |Valores Nulos| Comentário                                      |
| ---------------- | ----------------------------------------- | ------ |---------|-------------|----------------------------------------------- |
| Produto          | Nome do produto (FK para dimensao_produto)| string | 288     | 0           |Nome do Produto de Hortifruti Chave estrangeira referenciando dimensao_produto pelo nome |
| Ano_Mes          | Ano e Mês agrupados                       | string | 288     | 0           |Agrupamento das datas em Ano e mês/ Dados de Jan a Jun (Jun até dia 26)               |
| Preco_Medio_Geral| Preço Médio agrupado por Ano e Mês        | Float  | 288     | 0           |É a Média de Preço de cada Produto agrupando todos os Ceasas de todo o Brasil|
| Variacao_Mes_Anterior| Variação Mês-1                        | Double | 240     | 48          |Variação da coluna Preco_Medio_Geral Mês a Mês/ Variação dos meses de Jan estão Nulas, pois não existia dado antes desse mês /Min = 2,3 e Max = 32,92 |


#### Exemplo de Dados

##### Tabela Gold: Fato_hortigrangeiros

| Produto     | Fornecedor  | UF  | Data       | Preco_Medio | Ano_Mes    |
| ----------- | ----------- | --- | ---------- | ----------- | -----------|
| Produto A   | Fornecedor A | SP  | 2024-07-01 | 10.00      | 2024-01    |
| Produto B   | Fornecedor B | RJ  | 2024-07-02 | 20.00      | 2024-02    |
| Produto C   | Fornecedor C | MG  | 2024-07-03 | 30.00      | 2024-06    |
| Produto D   | Fornecedor D | ES  | 2024-07-04 | 40.00      | 2024-05    |

##### Tabela Gold: dimensao_produto

| Produto | Unidade |
| ------------ | --------- |
| Produto A    | KG
| Produto B    | DZ
| Produto C    | UND
| Produto D    | KG

##### Tabela Gold: totalizadora_hortigrangeiros

| Produto           | Ano_Mes   | Preco_Medio_Geral | Variacao_Mes_Anterior |
| ----------------- | --------- | ----------------- | --------------------- |
| Produto A         | 2024-01   | 15.00             | NULL                  |
| Produto A         | 2024-02   | 16.50             | 10                    |
| Produto A         | 2024-03   | 18.00             | 9.09                  |
| Produto B         | 2024-01   | 25.00             | NULL                  |
| Produto B         | 2024-02   | 24.00             | -4.00                 |
| Produto B         | 2024-03   | 26.50             | 10.42                 |
