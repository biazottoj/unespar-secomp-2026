# Cheat Sheet — Oficina de Mining Software Repositories

## Índice

- [2. PyDriller](#2-pydriller)
- [3. Criar um dataset](#3-criar-um-dataset)
- [4. Inspecionar o DataFrame](#4-inspecionar-o-dataframe)
- [5. Filtrar dados](#5-filtrar-dados)
- [6. Agrupar dados](#6-agrupar-dados)
- [7. Ordenar](#7-ordenar)
- [8. Criar novas métricas](#8-criar-novas-metricas)
- [9. Combinar DataFrames](#9-combinar-dataframes)
- [10. Remover duplicatas](#10-remover-duplicatas)
- [11. Visualização com Seaborn](#11-visualizacao-com-seaborn)
- [12. Topic Modelling](#12-topic-modelling)
- [13. NMF](#13-nmf)
- [14. Mostrar palavras dos tópicos](#14-mostrar-palavras-dos-topicos)
- [15. Perguntas úteis para uma análise MSR](#15-perguntas-uteis-para-uma-analise-msr)
- [16. Cuidados de interpretação](#16-cuidados-de-interpretacao)
- [17. Fluxo recomendado](#17-fluxo-recomendado)
- [Comandos mais importantes da oficina](#comandos-mais-importantes-da-oficina)
- [18. Gráficos prontos com Plotly](#18-graficos-prontos-com-plotly)
- [19. Templates prontos de preparação por período](#19-templates-prontos-de-preparacao-por-periodo)
- [20. Template pronto por arquivo](#20-template-pronto-por-arquivo)
- [21. Template pronto por autor](#21-template-pronto-por-autor)
- [22. Regra prática para escolher o gráfico](#22-regra-pratica-para-escolher-o-grafico)

---


## 1. Clonar um repositório

```python
from pathlib import Path
import subprocess

URL = "https://github.com/psf/requests.git"
REPO = Path("/workspace/repositories/requests")

if not REPO.exists():
    subprocess.run(
        ["git", "clone", "--depth", "500", URL, str(REPO)],
        check=True
    )
```

---

# 2. PyDriller

## Percorrer commits

```python
from pydriller import Repository

for commit in Repository(str(REPO)).traverse_commits():
    print(commit.hash)
```

## Informações do commit

```python
commit.hash
commit.author.name
commit.author.email
commit.author_date
commit.msg
commit.modified_files
```

## Percorrer arquivos modificados

```python
for commit in Repository(str(REPO)).traverse_commits():

    for arquivo in commit.modified_files:

        print(arquivo.filename)
```

## Informações úteis de um arquivo modificado

```python
arquivo.filename

arquivo.old_path
arquivo.new_path

arquivo.added_lines
arquivo.deleted_lines

arquivo.nloc
arquivo.complexity
```

Para lidar com arquivos renomeados/removidos:

```python
caminho = arquivo.new_path or arquivo.old_path
```

---

# 3. Criar um dataset

```python
dados = []

for commit in Repository(str(REPO)).traverse_commits():

    for arquivo in commit.modified_files:

        dados.append({
            "commit": commit.hash,
            "autor": commit.author.name,
            "data": commit.author_date,
            "mensagem": commit.msg.splitlines()[0],
            "arquivo": arquivo.new_path or arquivo.old_path,
            "adicionadas": arquivo.added_lines,
            "removidas": arquivo.deleted_lines
        })
```

Converter para pandas:

```python
import pandas as pd

df = pd.DataFrame(dados)
```

---

# 4. Inspecionar o DataFrame

Primeiras linhas:

```python
df.head()
```

Colunas:

```python
df.columns
```

Quantidade de linhas:

```python
len(df)
```

Valores únicos:

```python
df["commit"].nunique()
df["autor"].nunique()
df["arquivo"].nunique()
```

Contagem:

```python
df["autor"].value_counts()
```

Top 10:

```python
df["autor"].value_counts().head(10)
```

---

# 5. Filtrar dados

## Igualdade

```python
df[df["autor"] == "Nome"]
```

## Contém texto

```python
df[
    df["mensagem"].str.contains(
        "fix",
        case=False,
        na=False
    )
]
```

## Remover mensagens de merge

```python
df[
    ~df["mensagem"]
      .str.lower()
      .str.startswith("merge")
]
```

---

# 6. Agrupar dados

## Contar registros por arquivo

```python
frequencia = (
    df.groupby("arquivo")
      .size()
      .reset_index(name="modificacoes")
)
```

## Somar valores

```python
resultado = (
    df.groupby("arquivo")["churn"]
      .sum()
      .reset_index()
)
```

## Múltiplas métricas

```python
resultado = (
    df.groupby("arquivo")
      .agg(
          modificacoes=("commit", "count"),
          autores=("autor", "nunique"),
          adicionadas=("adicionadas", "sum"),
          removidas=("removidas", "sum")
      )
      .reset_index()
)
```

---

# 7. Ordenar

```python
df.sort_values(
    "churn",
    ascending=False
)
```

Top 10:

```python
df.sort_values(
    "churn",
    ascending=False
).head(10)
```

---

# 8. Criar novas métricas

## Churn

```python
df["churn"] = (
    df["adicionadas"]
    + df["removidas"]
)
```

---

# 9. Combinar DataFrames

```python
hotspots = frequencia.merge(
    churn,
    on="arquivo"
)
```

---

# 10. Remover duplicatas

Uma mensagem por commit:

```python
commits = (
    df[["commit", "mensagem"]]
    .drop_duplicates()
)
```

---

# 11. Visualização com Seaborn

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

## Gráfico de barras

```python
sns.barplot(
    data=top10,
    x="modificacoes",
    y="arquivo"
)

plt.show()
```

## Scatter plot

```python
sns.scatterplot(
    data=hotspots,
    x="modificacoes",
    y="churn"
)

plt.show()
```

## Histograma

```python
sns.histplot(
    data=df,
    x="churn"
)

plt.show()
```

## Boxplot

```python
sns.boxplot(
    data=df,
    x="churn"
)

plt.show()
```

---

# 12. Topic Modelling

## Passo 1 — Selecionar mensagens

```python
commits = (
    df[["commit", "mensagem"]]
    .drop_duplicates()
)
```

## Passo 2 — Remover merges

```python
commits = commits[
    ~commits["mensagem"]
      .str.lower()
      .str.startswith("merge")
]
```

## Passo 3 — TF-IDF

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer(
    stop_words="english",
    min_df=2,
    max_df=0.9
)

X = vectorizer.fit_transform(
    commits["mensagem"]
)
```

### Parâmetros importantes

`stop_words="english"`

Remove palavras comuns da língua inglesa.

`min_df=2`

Ignora palavras que aparecem em menos de 2 documentos.

`max_df=0.9`

Ignora palavras que aparecem em mais de 90% dos documentos.

---

# 13. NMF

```python
from sklearn.decomposition import NMF

modelo = NMF(
    n_components=4,
    random_state=42
)

modelo.fit(X)
```

`n_components` define o número de tópicos.

---

# 14. Mostrar palavras dos tópicos

```python
palavras = vectorizer.get_feature_names_out()

for i, topico in enumerate(modelo.components_):

    indices = topico.argsort()[-8:][::-1]

    principais = [
        palavras[j]
        for j in indices
    ]

    print(
        f"Tópico {i + 1}:",
        ", ".join(principais)
    )
```

---

# 15. Perguntas úteis para uma análise MSR

## Evolução

- Quais arquivos mudam com maior frequência?
- Em quais períodos ocorreram mais mudanças?
- O volume de mudanças aumentou ou diminuiu?

## Desenvolvedores

- Quem contribui mais?
- Quantos desenvolvedores modificam cada arquivo?
- Existem arquivos modificados por poucos desenvolvedores?

## Código

- Quais arquivos possuem maior churn?
- Quais arquivos concentram alterações?
- Quais arquivos aparecem repetidamente em commits?

## Texto

- Quais palavras aparecem com maior frequência nas mensagens?
- Quais temas aparecem nas mensagens de commit?
- Existem tópicos relacionados a bugs, testes ou documentação?

---

# 16. Cuidados de interpretação

Não conclua automaticamente que:

```text
muitas modificações = código ruim
```

ou:

```text
muito churn = muitos defeitos
```

ou:

```text
tópico encontrado = verdade objetiva
```

Prefira:

```text
evidência
   ↓
padrão observado
   ↓
hipótese / interpretação
   ↓
investigação adicional
```

---

# 17. Fluxo recomendado

```text
1. Definir a pergunta

2. Identificar os dados necessários

3. Minerar o repositório

4. Criar o DataFrame

5. Limpar os dados

6. Agrupar / transformar

7. Visualizar

8. Interpretar

9. Discutir limitações
```

---

# Comandos mais importantes da oficina

```python
Repository(...).traverse_commits()

commit.author.name
commit.author_date
commit.msg
commit.modified_files

arquivo.added_lines
arquivo.deleted_lines

pd.DataFrame()

df.groupby()
df.value_counts()
df.nunique()
df.sort_values()
df.merge()
df.drop_duplicates()

sns.barplot()
sns.scatterplot()

TfidfVectorizer()
NMF()
```

---

# 18. Gráficos prontos com Plotly

Os exemplos abaixo foram pensados como **templates reutilizáveis**.

A ideia é que você troque apenas:

- o DataFrame;
- a coluna usada no eixo `x`;
- a coluna usada no eixo `y`;
- eventualmente a coluna usada para cor, tamanho ou agrupamento.

Importação:

```python
import plotly.express as px
```

---

## 18.1. Série temporal — uma métrica por período

Use quando quiser observar como alguma medida muda ao longo do tempo.

Exemplos:

- commits por mês;
- churn por mês;
- arquivos modificados por semana;
- desenvolvedores ativos por mês.

```python
fig = px.line(
    dados_periodo,
    x="periodo",
    y="valor",
    markers=True,
    title="Evolução ao longo do tempo"
)

fig.show()
```

### Exemplo: commits por mês

```python
commits_mes = (
    df.assign(
        mes=pd.to_datetime(df["data"]).dt.to_period("M").astype(str)
    )
    .groupby("mes")["commit"]
    .nunique()
    .reset_index(name="commits")
)

fig = px.line(
    commits_mes,
    x="mes",
    y="commits",
    markers=True,
    title="Commits por mês"
)

fig.show()
```

---

## 18.2. Barras — comparar itens

Use quando quiser comparar categorias.

Exemplos:

- arquivos mais modificados;
- autores com mais commits;
- módulos com maior churn;
- tópicos mais frequentes.

```python
fig = px.bar(
    dados,
    x="valor",
    y="categoria",
    orientation="h",
    title="Comparação entre categorias"
)

fig.show()
```

### Exemplo: arquivos mais modificados

```python
top10 = (
    df.groupby("arquivo")
      .size()
      .reset_index(name="modificacoes")
      .sort_values("modificacoes", ascending=False)
      .head(10)
)

fig = px.bar(
    top10,
    x="modificacoes",
    y="arquivo",
    orientation="h",
    title="Arquivos mais modificados"
)

fig.show()
```

---

## 18.3. Scatter plot — relacionar duas métricas

Use quando quiser verificar a relação entre duas medidas.

Exemplos:

- modificações × churn;
- autores × modificações;
- tamanho × número de mudanças;
- commits × quantidade de arquivos.

```python
fig = px.scatter(
    dados,
    x="metrica_x",
    y="metrica_y",
    hover_name="identificador",
    title="Relação entre duas métricas"
)

fig.show()
```

### Exemplo: frequência × churn

```python
fig = px.scatter(
    hotspots,
    x="modificacoes",
    y="churn",
    hover_name="arquivo",
    title="Frequência de modificação × Churn"
)

fig.show()
```

---

## 18.4. Scatter plot com tamanho

Use quando quiser mostrar uma terceira dimensão.

```python
fig = px.scatter(
    dados,
    x="metrica_x",
    y="metrica_y",
    size="metrica_tamanho",
    hover_name="identificador",
    title="Análise multidimensional"
)

fig.show()
```

### Exemplo

```python
fig = px.scatter(
    arquivos,
    x="modificacoes",
    y="churn",
    size="autores",
    hover_name="arquivo",
    title="Modificações × Churn × Autores"
)

fig.show()
```

---

## 18.5. Barras por período

Use quando quiser comparar valores discretos ao longo do tempo.

```python
fig = px.bar(
    dados_periodo,
    x="periodo",
    y="valor",
    title="Métrica por período"
)

fig.show()
```

### Exemplo: churn por mês

```python
churn_mes = (
    df.assign(
        mes=pd.to_datetime(df["data"]).dt.to_period("M").astype(str)
    )
    .groupby("mes")["churn"]
    .sum()
    .reset_index()
)

fig = px.bar(
    churn_mes,
    x="mes",
    y="churn",
    title="Churn por mês"
)

fig.show()
```

---

## 18.6. Barras agrupadas

Use para comparar categorias dentro de cada período.

```python
fig = px.bar(
    dados,
    x="periodo",
    y="valor",
    color="categoria",
    barmode="group",
    title="Comparação por período"
)

fig.show()
```

Exemplos:

```text
mês × quantidade de commits × tipo de atividade
```

```text
mês × churn × módulo
```

---

## 18.7. Barras empilhadas

Use quando quiser visualizar composição.

```python
fig = px.bar(
    dados,
    x="periodo",
    y="valor",
    color="categoria",
    barmode="stack",
    title="Composição por período"
)

fig.show()
```

Exemplo:

```text
mês
↓
quantidade de commits
↓
separados por tópico
```

---

## 18.8. Histograma — distribuição de uma métrica

Use quando quiser entender como os valores estão distribuídos.

Exemplos:

- churn por commit;
- número de arquivos por commit;
- tamanho das mudanças;
- quantidade de commits por autor.

```python
fig = px.histogram(
    dados,
    x="valor",
    nbins=30,
    title="Distribuição da métrica"
)

fig.show()
```

### Exemplo: churn

```python
fig = px.histogram(
    df,
    x="churn",
    nbins=30,
    title="Distribuição do churn"
)

fig.show()
```

---

## 18.9. Boxplot — comparar distribuições

Use para comparar distribuições entre grupos.

```python
fig = px.box(
    dados,
    x="categoria",
    y="valor",
    points="outliers",
    title="Distribuição por categoria"
)

fig.show()
```

Exemplos:

- churn por autor;
- churn por módulo;
- tamanho das mudanças por período.

---

## 18.10. Treemap — visualizar estrutura hierárquica

Útil quando os dados possuem uma estrutura como:

```text
módulo
└── arquivo
```

```python
fig = px.treemap(
    dados,
    path=["modulo", "arquivo"],
    values="valor",
    title="Distribuição por módulo e arquivo"
)

fig.show()
```

Por exemplo:

```text
tamanho do bloco = churn
```

---

# 19. Templates prontos de preparação por período

## Criar coluna de mês

```python
df["mes"] = (
    pd.to_datetime(df["data"])
      .dt.to_period("M")
      .astype(str)
)
```

## Commits por mês

```python
commits_mes = (
    df.groupby("mes")["commit"]
      .nunique()
      .reset_index(name="commits")
)
```

## Churn por mês

```python
churn_mes = (
    df.groupby("mes")["churn"]
      .sum()
      .reset_index()
)
```

## Desenvolvedores ativos por mês

```python
autores_mes = (
    df.groupby("mes")["autor"]
      .nunique()
      .reset_index(name="autores")
)
```

## Arquivos modificados por mês

```python
arquivos_mes = (
    df.groupby("mes")["arquivo"]
      .nunique()
      .reset_index(name="arquivos")
)
```

---

# 20. Template pronto por arquivo

```python
arquivos = (
    df.groupby("arquivo")
      .agg(
          modificacoes=("commit", "count"),
          commits=("commit", "nunique"),
          autores=("autor", "nunique"),
          churn=("churn", "sum")
      )
      .reset_index()
)
```

Com esse único DataFrame:

```python
fig = px.bar(
    arquivos.nlargest(10, "modificacoes"),
    x="modificacoes",
    y="arquivo",
    orientation="h",
    title="Arquivos mais modificados"
)

fig.show()
```

ou:

```python
fig = px.scatter(
    arquivos,
    x="modificacoes",
    y="churn",
    size="autores",
    hover_name="arquivo",
    title="Modificações × Churn × Autores"
)

fig.show()
```

---

# 21. Template pronto por autor

```python
autores = (
    df.groupby("autor")
      .agg(
          commits=("commit", "nunique"),
          arquivos=("arquivo", "nunique"),
          churn=("churn", "sum")
      )
      .reset_index()
)
```

### Autores com mais commits

```python
fig = px.bar(
    autores.nlargest(10, "commits"),
    x="commits",
    y="autor",
    orientation="h",
    title="Autores com mais commits"
)

fig.show()
```

### Relação entre atividade e alcance

```python
fig = px.scatter(
    autores,
    x="commits",
    y="arquivos",
    size="churn",
    hover_name="autor",
    title="Atividade dos desenvolvedores"
)

fig.show()
```

---

# 22. Regra prática para escolher o gráfico

```text
Quero mostrar evolução no tempo
→ px.line()

Quero comparar categorias
→ px.bar()

Quero relacionar duas métricas
→ px.scatter()

Quero analisar distribuição
→ px.histogram() ou px.box()

Quero mostrar composição
→ px.bar(..., barmode="stack")

Quero mostrar hierarquia
→ px.treemap()
```

Em geral, tente reaproveitar o template alterando apenas:

```text
DataFrame
coluna X
coluna Y
categoria
```
