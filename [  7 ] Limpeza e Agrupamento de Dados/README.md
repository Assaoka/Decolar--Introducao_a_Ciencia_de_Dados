---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.18.1
  kernelspec:
    display_name: Python 3
    name: python3
---

<!-- #region id="view-in-github" colab_type="text" -->
<a href="https://colab.research.google.com/github/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/blob/main/%5B%20%207%20%5D%20Limpeza%20e%20Agrupamento%20de%20Dados%20/%20Limpeza%20e%20Agrupamento%20de%20Dados.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<!-- #endregion -->

<!-- #region id="5sIHleMsIo4U" -->
# Aula 7: A Arte da Limpeza e Agrupamento de Dados

<!-- #endregion -->

<!-- #region id="LL6YlENyIq6L" -->
Na última aula, aprendemos a fazer resumos estatísticos, contagens e filtros avançados para fazer perguntas complexas à nossa Pokédex.

Hoje, vamos nos aprofundar em uma das tarefas mais importantes de um cientista de dados: a **limpeza e preparação dos dados**. Vamos aprender a lidar com informações faltantes, a agrupar dados para criar resumos poderosos e a transformar texto em números, um passo essencial para futuros modelos de Inteligência Artificial.

<!-- #endregion -->

<!-- #region id="VZlRIsXnIs5F" -->
## 1. Carregando a Pokédex
<!-- #endregion -->

<!-- #region id="dz3drcluIuAh" -->
Como sempre, nosso primeiro passo é importar o `pandas` e carregar nossos dados.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 287} id="3K_lUdSmIv8O" outputId="366324e0-1218-41d8-f8ba-412047af9fd6"
import pandas as pd

endereco = 'https://raw.githubusercontent.com/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/refs/heads/main/pokemon.csv'
df = pd.read_csv(endereco)
df.head()
```

<!-- #region id="WUKGtkJQI9lF" -->
## 2. Revisão Rápida: Poderes da Aula 6
<!-- #endregion -->

<!-- #region id="epPR9qjJI8P9" -->
Na última aula, você aprendeu a:

1. **`.describe()`**: Gerar um resumo estatístico completo (média, desvio padrão, mínimo, máximo, etc.) para colunas numéricas.


<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 143} id="FgyqcvGBJH9h" outputId="a091bb42-5782-447c-d76c-c7c3f5796f64"
df[['Attack', 'Defense', 'Speed']].describe().T
```

<!-- #region id="bJ9JRPX1JC-t" -->
2. **`.value_counts()`**: Contar a frequência de cada categoria em uma coluna.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 679} id="igxrHLr6JMm4" outputId="17608302-6a29-4798-ef27-0621a046a4ea"
df['Primary Typing'].value_counts()
```

<!-- #region id="CIF-BnixJErx" -->
3. **Filtros Compostos**: Usar `&` (E) e `|` (OU) para criar consultas complexas, como `df[(df['Primary Typing'] == 'grass') & (df['Legendary Status'] == True)]`.
    

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 339} id="hOv3izP3JR7k" outputId="5d8ff7df-5d25-41f1-f9e4-22ac86d89661"
df[(df['Primary Typing'] == 'grass') & (df['Legendary Status'] == True)].head()
```

<!-- #region id="gz6EoB_zJF5j" -->
4. **`.map()` e `.apply()`**: Transformar colunas, aplicando dicionários ou funções customizadas para criar novas informações.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 322} id="LCZKMPRAJZ8i" outputId="c98e504b-0b23-4c1b-94d7-9bf8f1820a02"
def categoria_peso(row):
    if row['Weight (hg)'] > 1000:
        return 'Pesado'
    else:
        return 'Leve'

df['Peso'] = df.apply(categoria_peso, axis=1)
df.sample(5)
```

<!-- #region id="O81O9EobJ1RU" -->
## 3. Tratando Dados Faltantes (`.fillna()`)
<!-- #endregion -->

<!-- #region id="Ba5KDyJCJ3h7" -->
Ao explorar dados, é muito comum encontrar "buracos" ou valores vazios (chamados de `NaN` - _Not a Number_). Modelos de análise e machine learning não sabem como lidar com eles, então precisamos tratá-los.

Primeiro, vamos ver quantos valores faltantes temos em cada coluna:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 867} id="95EoMbECJ6RU" outputId="29f7ef10-a4ca-4cd0-c75f-039232bf177f"
# O comando .isnull() retorna True para cada célula que é NaN.
# O .sum() soma esses Trues (considerando True=1 e False=0)
df.isnull().sum()
```

<!-- #region id="TVkfFpSEKAsW" -->
Vemos que a coluna `Secondary Typing` tem muitos valores faltando. Isso faz sentido, já que muitos Pokémon têm apenas um tipo. Em vez de deixar como `NaN`, vamos preencher esses campos com o texto "Nenhum". Para isso, usamos o método `.fillna()`.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 867} id="eZTnPB6rKC6b" outputId="6566db87-91d9-4a01-c780-4f7a2eb9797c"
# O método .fillna() preenche os valores NaN com o valor que especificarmos.
# O `inplace=True` modifica o DataFrame df diretamente, sem precisar fazer df = df.fillna(...)
df2 = df.copy()
df2['Secondary Typing'] = df['Secondary Typing'].fillna('Nenhum')
df2.isnull().sum()
```

<!-- #region id="aJwl23rwKoeL" -->
## 4. Agrupando Dados para Análise (`.groupby()`)

E se quisermos saber qual o tipo de Pokémon (`Primary Typing`) tem, em média, o maior ataque? Ou a maior defesa? Fazer isso com filtros seria muito trabalhoso.

Para isso, usamos o `.groupby()`, um dos comandos mais poderosos do Pandas. Ele segue uma lógica de **"Separar-Aplicar-Combinar"**:

1. **Separar**: Separa o DataFrame em grupos menores com base em uma ou mais colunas.
    
2. **Aplicar**: Aplica uma função a cada grupo para agregar os dados.
    
3. **Combinar**: Junta os resultados em um novo DataFrame.
    

### Funções de Agregação Comuns

Após o `.groupby()`, você pode aplicar diversas funções, como:

- `.mean()`: Calcula a média.
    
- `.sum()`: Soma os valores.
    
- `.min()`: Retorna o menor valor.
    
- `.max()`: Retorna o maior valor.
    
- `.count()`: Conta os valores não nulos.
    
- `.size()`: Conta o total de itens (incluindo nulos).
    
- `.median()`: Calcula a mediana.
    
- `.std()`: Calcula o desvio padrão.
    

### Agrupando por uma coluna

Vamos agrupar por 'Primary Typing' e calcular a média dos stats de batalha.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 645} id="eSLWYysqKr94" outputId="78a0d86a-1c34-4919-8409-b924e5edb78c"
# Agrupando por uma coluna e aplicando uma função
stats_por_tipo = df.groupby('Primary Typing')[['Attack', 'Defense', 'Speed', 'Base Stat Total']].mean()

# Ordenando pelo 'Base Stat Total' para ver os tipos mais fortes em média
stats_por_tipo.sort_values(by='Base Stat Total', ascending=False)
```

<!-- #region id="NsoUFEKYKyU2" -->
### Agrupando por Múltiplas Colunas

Podemos ser ainda mais específicos. E se quisermos ver a contagem de Pokémon por Geração E se eles são lendários ou não? Basta passar uma lista de colunas para o `.groupby()`.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 679} id="rHomEnqQK0jF" outputId="ac124c19-79f9-4780-b8da-0ae0e3f41f9f"
# Agrupando por múltiplas colunas
# O .size() é ótimo para contar a quantidade de registros em cada subgrupo
contagem_geracao_lendarios = df.groupby(['Generation', 'Legendary Status']).size()
contagem_geracao_lendarios
```

<!-- #region id="IusGdrk1K8sm" -->
### Aplicando Múltiplas Funções com `.agg()`

E se você quiser ver o `min`, o `max` e a `media` do `Attack` para cada tipo, tudo de uma vez? Para isso, usamos o método `.agg()` (de "aggregate"), passando uma lista de funções que queremos aplicar.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 645} id="oGqFJiQtK-uX" outputId="46215a7a-8dd1-4c2f-9792-a58d45a169a4"
# Usando .agg() para aplicar múltiplas funções
stats_detalhados_por_tipo = df.groupby('Primary Typing')['Attack'].agg(['min', 'max', 'mean'])
stats_detalhados_por_tipo
```

<!-- #region id="KNCvl0QULCRg" -->
## 5. One-Hot Encoding Avançado: Lidando com Múltiplas Categorias

No mundo real, é comum que um item pertença a várias categorias ao mesmo tempo. Um filme pode ser "Ação", "Aventura" e "Ficção Científica". No nosso caso, um Pokémon pode ser do tipo "grass" e "poison".

O `get_dummies` padrão não funciona bem para isso. Precisamos de uma abordagem mais inteligente.

### Passo 1: Unificar os Tipos em uma Única Coluna

Primeiro, vamos criar uma nova coluna que junta o tipo primário e o secundário, separados por uma vírgula.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 206} id="lNbAld39LGoT" outputId="76783bff-ee39-4a27-fddd-33ebd7371581"
# Juntando as duas colunas de tipo em uma só
def all_types(row):
    if pd.isna(row['Secondary Typing']) or row['Secondary Typing'] == '':
        return row['Primary Typing']
    else:
        return row['Primary Typing'] + ',' + row['Secondary Typing']

df['All_Types'] = df.apply(all_types, axis=1)
display(df[['Name', 'Primary Typing', 'Secondary Typing', 'All_Types']].head())
```

<!-- #region id="oxIXNP07LF5U" -->
### Passo 2: Usar `.str.get_dummies()` para Separar as Categorias

Agora que temos uma única coluna com os tipos separados por vírgula, podemos usar uma função especial: `.str.get_dummies()`. Ela entende que precisa quebrar a string no separador e criar as colunas a partir daí.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 206} id="MH9pq65CLetB" outputId="04d4a873-cb57-4956-9317-311846ce82db"
# O argumento `sep=','` diz à função para quebrar a string toda vez que encontrar uma vírgula
tipos_dummies = df['All_Types'].str.get_dummies(sep=',')

# Vamos ver o resultado para os primeiros Pokémon.
# Repare como o Bulbasaur tem '1' nas colunas 'grass' e 'poison', enquanto o Charmander só tem em 'fire'.
tipos_dummies.head()
```

<!-- #region id="DDm_b7baLjRM" -->
Essa técnica é extremamente poderosa e prepara os dados da forma correta para algoritmos de Machine Learning quando temos múltiplas categorias por item.

<!-- #endregion -->

<!-- #region id="IbLDqQcDLkrV" -->
## 6. Hora dos Exercícios!

Vamos praticar os novos conceitos.
<!-- #endregion -->

<!-- #region id="BTHOY2ffLmu-" -->
### Exercício 1: Contagem de Tipos Secundários

Antes da limpeza, quantos Pokémon **não tinham** um `Secondary Typing`? (Dica: use o DataFrame original ou reconte os `NaN` antes do `.fillna()`).
<!-- #endregion -->

```python id="kaC8LJyHLmQp"

```

<!-- #region id="E8m7OZrJLprE" -->
### Exercício 2: O Pokémon mais pesado de cada tipo

Use `.groupby()` para encontrar o Pokémon com o maior peso (`Weight (hg)`) para cada `Primary Typing`. (Dica: use `.max()` após o groupby).
<!-- #endregion -->

```python id="P3RPNOLALuOZ"

```

<!-- #region id="qJ1JGjV3LvjI" -->

### Exercício 3: Análise dos Lendários

Use `.groupby()` na coluna `Legendary Status` para comparar a média de `Attack`, `Defense` e `Speed` entre Pokémon lendários e não lendários.
<!-- #endregion -->

```python id="uHzyo2UGLyuX"

```

<!-- #region id="d6wIkWcRLyUa" -->
### Exercício 4: Agrupando por duas colunas

Agrupe o DataFrame por `Generation` e `Legendary Status` para ver a contagem de Pokémon em cada categoria. (Dica: use `.size()` após o groupby para contar).

<!-- #endregion -->

```python id="tq1PchHjL2Nn"

```

<!-- #region id="m82UISAKL00d" -->
### Exercício 5: Juntando os Resultados

Para criar um DataFrame final pronto para Machine Learning, precisamos juntar nosso DataFrame original com as `tipos_dummies` que criamos. Use `pd.concat()` para isso.

<!-- #endregion -->

```python id="_-y-yWM4L19L"

```
