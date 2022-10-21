# Desafio - Engenharia de Dados

Desafio de contratação Khipo. Realize um fork deste repositório e faça as etapas referentes a sua vaga. O intuito desse teste é ser algo simples, porém suficiente para validar a qualidade do seu código.

# Desafio 1

## Tratamento de Dados

Utilizando SQL Oracle ou PySpark, faça o tratamento e remodelagem dos dados disponibilizados nos JSON desse repositório. Os 3 arquivos são dados de proposições legislativas da Assembléia Legislativa de Minas Gerais (mais sobre - dados retirados da API disponibilizada em: https://dadosabertos.almg.gov.br/ws/proposicoes/ajuda) nos anos de 2020, 2021 e 2022. 
Deve-se realizar um *data cleansing* (limpeza de dados) nos campos com itens idesejados (espaçamento desnecessário, "\n", etc) e ajustar esses campos ao formato adequado, seguindo a modelagem a seguir (**Atenção ao formato dos exemplos**):

### Tabela: Proposição
```
id (incremental)
author (string - Autor - ex. Governador Romeu Zema Neto)
presentationDate (timestamp - Data de Apresentação - ex. 2022-10-06T00:00:00Z)
ementa (string - Assunto - ex. Encaminha o Projeto de Lei 4008 2022, que dispõe sobre a revisão do Plano Plurianual de Ação Governamental - PPAG - 2020-2023, para o exercício de 2023.)
regime (string - Regime - ex. Especial)
situation (string - Situação - ex. Publicado)
propositionType (string - Tipo da Proposição - ex. MSG)
number (string - Numero - ex. 300)
year (integer - Ano - ex. 2022)
city (string -> fixo "Belo Horizonte")
state (string -> fixo "Minas Gerais")
```

### Tabela: Tramitação
```
id (incremental)
createdAt (string - Data - ex. 2022-10-04T00:00:00Z)
description (string - Histórico - Proposição lida em Plenário.\nPublicada no DL em 6 10 2022, pág 24.)
local (string - Local - ex. Plenário)
propositionId (chave estrangeira da proposição)
```
Uma proposição tem uma lista (histórico) de tramitações.

Caso opte por realizar em PySaprk (preferível) criar no modelo a seguir:

### Dataframe
```
id (incremental)
author (string - Autor - ex. Governador Romeu Zema Neto)
presentationDate (timestamp - Data de Apresentação - ex. 2022-10-06T00:00:00Z)
ementa (string - Assunto - ex. Encaminha o Projeto de Lei 4008 2022, que dispõe sobre a revisão do Plano Plurianual de Ação Governamental - PPAG - 2020-2023, para o exercício de 2023.)
regime (string - Regime - ex. Especial)
situation (string - Situação - ex. Publicado)
propositionType (string - Tipo da Proposição - ex. MSG)
number (string - Numero - ex. 300)
year (integer - Ano - ex. 2022)
city (string -> fixo "Belo Horizonte")
state (string -> fixo "Minas Gerais")
tramitacoes (array -> struct - Histórico de Tramitações - campo: listaHistoricoTramitacoes)
  {
    createdAt (string - Data - ex. 2022-10-04T00:00:00Z)
    description (string - Histórico - Proposição lida em Plenário.\nPublicada no DL em 6 10 2022, pág 24.)
    local (string - Local - ex. Plenário)
  }
```

# Desafio 2

## Visualização de Dados

Criar um Dashboard no PowerBI no formato disponível abaixo e consumindo os dados tratados.

Deve existir um filtro de Ano e um de Mês.

Um gráfico de pizza mostrando a quantidade de proposições de cada tipo.

Um gráfico de pizza mostrando a quantidade de proposições de cada situação.

Um gráfico de barras com a quantidade de proposições publicadas em cada dia/mês.

![Group 1](https://user-images.githubusercontent.com/30670086/197281071-b5428d8b-9a8f-486b-9097-5bdd85031618.png)
URL: https://www.figma.com/file/WiIAnkH7kweAOHxnXi2utT/DesafioDados?node-id=0%3A1
