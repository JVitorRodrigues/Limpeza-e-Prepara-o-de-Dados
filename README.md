# Revisão — Limpeza e Preparação de Dados

Projeto acadêmico da disciplina de **Ciência de Dados**, do curso de Bacharelado em Engenharia de Software. O objetivo é aplicar técnicas de limpeza, preparação e análise exploratória de dados, seguindo conceitos da etapa de preparação de dados do processo CRISP-DM.

## Objetivo do projeto

Praticar técnicas de identificação e tratamento de problemas em conjuntos de dados reais, incluindo valores ausentes, duplicatas, inconsistências de tipos e textos, valores extremos (*outliers*) e escalonamento de variáveis numéricas.

## Tecnologias utilizadas

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Glob
- RapidFuzz (desafio opcional do Exercício 2)

## Exercício 1 — Tratamento de valores ausentes

**Dataset:** Melbourne Housing Snapshot

**Arquivo:** `melb_data.csv`

**Fonte:** [Kaggle — Melbourne Housing Snapshot](https://www.kaggle.com/datasets/dansbecker/melbourne-housing-snapshot)

### Atividades realizadas

- Carregamento e diagnóstico inicial do conjunto de dados.
- Verificação das dimensões, dos tipos de dados e dos valores ausentes.
- Criação de uma tabela com a quantidade e a porcentagem de valores ausentes.
- Visualização dos padrões de ausência.
- Comparação entre remoção de registros e imputação por medidas estatísticas.
- Análise do impacto das estratégias sobre a quantidade de registros e a distribuição dos dados.

**Conceitos estudados:** dados ausentes, imputação, remoção de registros, média, mediana e preservação dos dados originais.

## Exercício 2 — Identificação e tratamento de duplicatas

**Dataset:** Customer Transaction Dataset — KPMG

**Arquivo:** `KPMG_VI_New_raw_data_update_final.xlsx`

**Planilha principal:** `Transactions`

**Fonte:** [Kaggle — Customer Transaction Dataset](https://www.kaggle.com/datasets/archit9406/customer-transaction-dataset)

### Atividades realizadas

- Carregamento e inspeção do cabeçalho da planilha.
- Identificação de duplicatas exatas.
- Investigação de duplicatas considerando subconjuntos de colunas.
- Verificação da unicidade dos identificadores das transações.
- Definição e justificativa de estratégias para tratar registros repetidos.
- Avaliação do impacto do tratamento sobre indicadores, como a soma dos preços das transações.

**Conceitos estudados:** duplicatas exatas, duplicatas por chave, unicidade de identificadores e impacto da limpeza em indicadores de negócio.

**Desafio opcional:** utilizar RapidFuzz para identificar valores textuais semelhantes e investigar inconsistências na planilha `CustomerDemographic`.

## Exercício 3 — Padronização e escalonamento

**Dataset:** Adult Census Income

**Arquivo principal:** `adult.data`

**Fonte:** [UCI Machine Learning Repository — Adult](https://archive.ics.uci.edu/dataset/2/adult)

### Atividades realizadas

- Definição dos nomes das colunas conforme a documentação do dataset.
- Inspeção dos valores únicos das colunas categóricas.
- Padronização de textos, espaços e diferenças de capitalização.
- Conversão de marcadores de valores desconhecidos, como `?`, para valores ausentes.
- Aplicação de três técnicas de escalonamento às colunas numéricas:
  - **Min-Max Scaling:** ajusta os valores para uma faixa definida, normalmente entre 0 e 1.
  - **StandardScaler (Z-score):** transforma os dados com base na média e no desvio-padrão.
  - **RobustScaler:** utiliza a mediana e o intervalo interquartil, sendo menos sensível a valores extremos.

### Objetivo da análise

Comparar os resultados das técnicas de escalonamento, observar as diferenças nas distribuições e discutir quando faz sentido escalar cada variável numérica.

## Exercício 4 — Identificação e tratamento de outliers

**Dataset:** Diamonds

**Carregamento:** `sns.load_dataset('diamonds')`

**Fonte:** [Seaborn — Datasets](https://github.com/mwaskom/seaborn-data)

### Atividades realizadas

- Análise das estatísticas descritivas das variáveis numéricas.
- Verificação de dimensões inválidas ou fisicamente impossíveis.
- Identificação de valores extremos utilizando dois métodos:
  - Z-score, com análise de valores cujo módulo do escore é superior a 3.
  - Intervalo interquartil (IQR).
- Comparação da quantidade de registros identificados por cada método.
- Criação de boxplots, histogramas e gráficos de dispersão.
- Diferenciação entre erros de registro e valores extremos legítimos.
- Comparação de três estratégias de tratamento de preços:
  - Remoção de registros extremos.
  - Capping, limitando os valores aos limites definidos.
  - Transformação logarítmica com `log1p`.

### Objetivo da análise

Compreender como a escolha do método de detecção e tratamento de outliers pode alterar as estatísticas e a distribuição dos dados, sem eliminar automaticamente valores extremos que possam ser legítimos.

## Exercício 5 — Pipeline integrado de limpeza de dados

**Dataset:** Dirty E-Commerce Data — SHEIN

**Fonte:** [Kaggle — E-Commerce Data SHEIN](https://www.kaggle.com/datasets/oleksiimartusiuk/e-commerce-data-shein)

### Arquivos selecionados

- `us-shein-mens_clothes-1891.csv` — roupas masculinas.
- `us-shein-jewelry_and_accessories-3548.csv` — acessórios.

### Pergunta de negócio

Existem diferenças nos preços das roupas masculinas e dos acessórios vendidos na SHEIN, e como a limpeza dos dados pode ajudar a comparar essas categorias de forma confiável?

### Atividades realizadas

1. Carregamento e diagnóstico inicial dos dois arquivos.
2. Identificação de valores ausentes, duplicatas e tipos de dados inadequados.
3. Conversão dos preços e descontos para formatos numéricos.
4. Tratamento de registros sem título identificável ou preço válido.
5. Remoção de duplicatas exatas.
6. Padronização de textos e espaços desnecessários.
7. Identificação de outliers pelo método IQR, preservando os preços originais.
8. Criação de novas variáveis para análise.
9. Comparação da qualidade dos dados antes e depois da limpeza.
10. Elaboração de visualizações para comparar as distribuições de preços.

### Novas variáveis

- `faixa_preco`: classifica os produtos em faixas de preço.
- `tem_desconto`: indica se existe informação de desconto disponível.
- `price_outlier`: identifica preços considerados extremos pelo método IQR.

### Objetivo da análise

Construir um pipeline reutilizável para diferentes arquivos de produtos, documentar as decisões de limpeza e facilitar a comparação de preços entre categorias.

## Boas práticas adotadas

- Diagnosticar os dados antes de realizar alterações.
- Preservar cópias dos dados originais.
- Criar funções reutilizáveis para as etapas do pipeline.
- Justificar as decisões de tratamento conforme o objetivo da análise.
- Comparar a qualidade dos dados antes e depois da limpeza.
- Utilizar visualizações para compreender as distribuições.
- Validar os resultados para evitar distorções causadas pelo tratamento.

## Estrutura sugerida do repositório

```text
limpeza-preparacao-dados/
├── README.md
├── exercicio-1-valores-ausentes.ipynb
├── exercicio-2-duplicatas.ipynb
├── exercicio-3-escalonamento.ipynb
├── exercicio-4-outliers.ipynb
├── exercicio-5-pipeline-integrado.ipynb
└── datasets/
    └── instrucoes-dos-datasets.md
```

*Observação:* os nomes dos notebooks e a pasta `datasets/` são uma sugestão de organização. Os arquivos de dados podem ser mantidos fora do repositório e carregados no Google Colab, especialmente quando forem grandes ou sujeitos a restrições de redistribuição.

## Resultados esperados

Ao concluir os exercícios, espera-se compreender como identificar problemas de qualidade dos dados, escolher estratégias adequadas de tratamento, avaliar seus impactos e preparar conjuntos de dados para análises estatísticas e aplicações de ciência de dados.

## Conclusão

Este projeto reúne práticas fundamentais de preparação de dados: tratamento de valores ausentes, remoção de duplicatas, padronização, escalonamento e identificação de outliers. O desenvolvimento dos cinco exercícios reforça a importância de combinar técnicas de programação, análise exploratória e decisões justificadas pelo contexto de negócio.

---

**Projeto acadêmico — Engenharia de Software | Ciência de Dados**
