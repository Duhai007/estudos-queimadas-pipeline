# Estudos de Queimadas

Pipeline de consolidação e análise que cruza dados meteorológicos (INMET) com
focos de calor (INPE/BDQueimadas) para os 645 municípios do estado de São
Paulo (2015-2024), avaliando quais variáveis meteorológicas são
estatisticamente significantes para a ocorrência de focos de calor, via
regressão logística.

## Estrutura do repositório

```
├── Pipeline_estudos_queimadas.ipynb   # notebook com o pipeline completo
├── municipios_brasileiros.csv         # coordenadas dos municípios (IBGE)
├── Focos/                             # focos de calor por ano (INPE/BDQueimadas), 2015-2024
├── figuras/                           # gráficos e tabela resumo gerados pelo notebook
└── INMET/                             # dados brutos das estações meteorológicas (não versionado, ver abaixo)
```

## Dados não incluídos no repositório

Dois itens ficam fora do controle de versão (`.gitignore`) por excederem o
limite de tamanho do GitHub:

- `INMET/` — dados brutos das estações meteorológicas automáticas (~5 GB)
- `dataframe_final_estacao_hora.csv` — dataframe final consolidado (estação x
  hora), gerado pela Etapa 6 do notebook (~500 MB)

Para rodar o pipeline do zero, é necessário obter os dados brutos do INMET
(https://portal.inmet.gov.br/dadoshistoricos) e organizá-los em
`INMET/<ano>/`, um arquivo CSV por estação.

## Como rodar

```bash
pip install pandas numpy requests scikit-learn statsmodels scipy matplotlib
```

Abra `Pipeline_estudos_queimadas.ipynb` e ajuste a variável `PASTA_PROJETO`
no início do notebook para o caminho local do projeto. O pipeline segue 9
etapas, da consolidação dos dados brutos até a geração dos gráficos e da
tabela de resultados usados no TCC:

1. Catálogo de estações automáticas do INMET
2. Estação meteorológica mais próxima de cada município
3. Consolidação dos dados meteorológicos brutos
4. Preenchimento de lacunas curtas (falha de sensor)
5. Consolidação dos focos de calor
6. Montagem do dataframe final (estação x hora)
7. Preparação das variáveis (VIF, anomalia por estação, tendência de pressão)
8. Regressão logística (amostragem caso-controle)
9. Gráficos e tabela resumo

## Resultados

As figuras e a tabela descritiva gerados pela última execução estão em
[`figuras/`](figuras/).
