# SalesInsight PY

Análise e visualização de dados de vendas desenvolvida em Python, como mini-projeto avaliativo.

**Autor:** Andres Jeremías Figueredo

## Sobre o projeto

O SalesInsight PY carrega, limpa, transforma, agrega e visualiza um dataset de vendas. O fluxo gera métricas por período, produto, categoria e região, segmenta os clientes por faixa de gasto e exporta os resultados em CSV, JSON e PNG.

Todo o código está organizado em funções reutilizáveis e em uma classe (`AnalisadorDeVendas`), executadas a partir de uma função `main()`.

## O que o projeto analisa

- Receita total, quantidade e número de vendas por mês
- Top 5 produtos por receita
- Receita por categoria
- Receita total e ticket médio por região
- Segmentação de clientes por nível de gasto (Bronze, Prata, Ouro)
- Relação entre quantidade vendida e receita por venda

## Fluxo de execução

```
gerar dataset → carregar CSV → inspecionar → limpar → criar colunas
→ métricas (groupby) → segmentar clientes → gráficos → resumo → exportar
```

A limpeza dos dados acontece **antes** de qualquer transformação, agregação ou gráfico.

## Principais resultados

| Indicador | Valor |
| --- | --- |
| Registros gerados | 200 |
| Registros removidos (data inválida) | 6 |
| Registros analisados | 194 |
| Receita total | R$ 1.380.210,31 |
| Ticket médio | R$ 7.114,49 |
| Clientes únicos | 49 |

- **Produto líder:** Notebook, com R$ 493.242,63 de receita.
- **Categoria líder:** Computadores, com R$ 698.455,24.
- **Região líder em receita:** Centro-Oeste (R$ 342.981,92). Já o **Nordeste** tem o maior ticket médio (R$ 8.653,08): menos vendas, porém de maior valor.
- **Sazonalidade:** picos de receita em fevereiro e outubro; o pior mês foi setembro.
- **Segmentação:** 35 clientes Ouro, 9 Prata e 5 Bronze.
- **Quantidade x receita:** vender mais unidades aumenta a receita, mas o efeito depende da categoria. Computadores crescem muito mais rápido que Periféricos.

## Conceitos aplicados (Módulo 01 - Semanas 01 a 07)

- **Lógica de programação:** variáveis, tipos, operadores, condicionais e laços
- **Estruturas de dados:** listas, tuplas, dicionários e estruturas compostas (dicionário de DataFrames)
- **Funções:** parâmetros, valores padrão, retorno, docstrings, `lambda` e função de ordem superior (`processar_coluna`)
- **Orientação a objetos:** classe `AnalisadorDeVendas` com atributos e métodos
- **Módulo `datetime`:** geração de datas e conversão com `pd.to_datetime(errors="coerce")`
- **Conversão de tipos (cast):** `astype(int)`, `astype(float)`, `float()`
- **Pandas:** DataFrames, filtros, `groupby`, `agg`, `apply`, `map`, `loc`, `value_counts`
- **Operações vetorizadas:** cálculo de `receita_total` sem laço
- **Matplotlib e Seaborn:** gráficos de linha, barra, dispersão e painel com subplots 2×2
- **Arquivos:** leitura e escrita em CSV e JSON
- **Git e GitHub:** branches, commits e GitFlow simplificado

## Como executar

### Google Colab (recomendado)

1. Abra o notebook `salesinsight.ipynb` no Google Colab (ou faça upload de `salesinsight.py`).
2. Execute a célula. Se `vendas.csv` não existir, o próprio código gera o dataset.
3. Alternativa com o arquivo `.py`: execute `!python salesinsight.py` em uma célula.

O Colab já possui todas as bibliotecas instaladas.

### Localmente com VS Code

1. Instale o Python 3.10+ e o VS Code.
2. Instale as dependências:
   ```
   pip install pandas numpy matplotlib seaborn
   ```
3. Execute no terminal:
   ```
   python salesinsight.py
   ```

## Estrutura do projeto

```
salesinsight-py/
├── README.md
├── salesinsight.ipynb          # notebook principal (Colab)
├── salesinsight.py             # mesmo código em script Python
├── vendas.csv                  # dataset gerado pelo código
└── outputs/
    ├── metricas_por_mes.csv
    ├── segmentacao_clientes.csv
    ├── estatisticas_gerais.json
    └── graficos/
        ├── receita_por_mes.png
        ├── top_produtos.png
        ├── quantidade_vs_receita.png
        └── painel_resumo.png
```

## Decisões técnicas

- **Remover as datas inválidas em vez de mantê-las.** O dataset possui 6 vendas com a data `DATA INVALIDA`. Elas foram convertidas para `NaT` com `errors="coerce"` e removidas, porque uma venda sem data não pode entrar na análise por mês ou trimestre. Como representam apenas 3% dos registros, a remoção não compromete o resultado. Imputação de valores não foi usada, conforme orientação do projeto.
- **Dataset sintético com `seed=42`.** Garante que qualquer pessoa obtenha exatamente os mesmos dados e resultados.
- **Classe para organizar o fluxo.** Os resultados de cada etapa ficam guardados como atributos do objeto, evitando passar muitas variáveis soltas entre funções.

## Oportunidades de melhoria

- Salvar as contagens do JSON como inteiros (hoje aparecem como `194.0` por causa da conversão com `float()`).
- Permitir que o usuário informe o caminho de um CSV real na execução.

## Ferramentas utilizadas

- Python 3.10+
- Google Colab
- Bibliotecas: pandas, numpy, matplotlib, seaborn, json, datetime, os, random
- Git e GitHub para versionamento

## Versionamento

Branches utilizadas: `main`, `develop`, `feat/pipeline-dados` e `docs/readme`. Commits seguem o padrão *conventional commits* (`feat:`, `docs:`).

## Vídeo de demonstração

[inserir aqui o link do Google Drive ou do YouTube]
