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
<a href="https://colab.research.google.com/github/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/blob/main/%5B%20%208%20%5D%20Decifrando%20Padr%C3%B5es%20e%20Rela%C3%A7%C3%B5es%20com%20Gr%C3%A1ficos%20/%20Decifrando%20Padr%C3%B5es%20e%20Rela%C3%A7%C3%B5es%20com%20Gr%C3%A1ficos.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<!-- #endregion -->

<!-- #region id="bbxFTR0qIxP9" -->
# Aula 8: Decifrando Padrões e Relações com Gráficos
<!-- #endregion -->

<!-- #region id="4aHwyu0MI13d" -->
Na aula passada, dominamos a arte de limpar, agrupar e preparar nossos dados. Agora que eles estão prontos, vamos aprender a fazê-los "falar". A melhor forma de entender a história que os dados contam é através da **visualização**.

Hoje, vamos aprender a criar os gráficos essenciais para qualquer análise de dados. Começaremos com os gráficos de **Barra** e **Pizza** para entender categorias. Depois, mergulharemos no **Histograma** para analisar distribuições e, por fim, no **Gráfico de Dispersão** para descobrir relações entre as variáveis.

<!-- #endregion -->

<!-- #region id="YJ7IZlFPI56W" -->
## 1. Preparando o Ambiente
<!-- #endregion -->

<!-- #region id="cNCZ43SKI-m4" -->
Vamos importar todas as bibliotecas que precisaremos hoje, incluindo o `Numpy` para criar dados artificiais para as nossas explicações teóricas.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 322} id="0xoaylahIwkc" outputId="dca0d10b-5e1c-4a83-d998-94693a05fbeb"
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from statistics import mean, median, mode

# Configurações para melhorar a aparência dos gráficos
sns.set_style('whitegrid')
plt.rcParams['figure.figsize'] = (10, 6) # Define um tamanho padrão para os gráficos

# Carregando nossos dados
endereco = 'https://raw.githubusercontent.com/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/refs/heads/main/pokemon.csv'
df = pd.read_csv(endereco)
df.sample(5)
```

<!-- #region id="8wRoM5tPJLzr" -->
## 2. Revisão Rápida: Poderes da Aula 7
<!-- #endregion -->

<!-- #region id="mPg0SDSmJKlr" -->
Na última aula, aprendemos a:

1. **`.fillna()`**: Tratar valores ausentes em nosso DataFrame.
    
2. **`.groupby()`**: Agrupar dados com base em uma ou mais colunas para aplicar funções de agregação (`.mean()`, `.max()`, `.size()`, etc.).
    
3. **`.agg()`**: Aplicar múltiplas agregações de uma só vez.
    
4. **`pd.get_dummies()`**: Transformar variáveis categóricas em um formato numérico, essencial para Machine Learning.
<!-- #endregion -->

<!-- #region id="wkNIkoKzJOq4" -->
## 3. Visualizando Categorias


<!-- #endregion -->

<!-- #region id="JovzYMHcJQGv" -->
Vamos começar com os gráficos mais diretos, usados para contar e comparar categorias.


<!-- #endregion -->

<!-- #region id="IFy_uoA9JTKM" -->
### 3.1. Gráfico de Barras e Gráfico de Pizza
<!-- #endregion -->

<!-- #region id="GLmtxK5hJSE_" -->


- **Gráfico de Barras:** Perfeito para **comparar** a contagem entre diferentes categorias. É fácil ver qual categoria tem mais ou menos itens.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 676} id="kRu6tRetJVw8" outputId="e78b4441-6a5d-4f97-b9f6-bb960e020e9d"
# --- Gráfico de Barras: Contagem de Pokémon por Tipo Primário ---
plt.figure(figsize=(12, 7))
contagem_tipos = df['Primary Typing'].value_counts()
sns.barplot(x=contagem_tipos.index, y=contagem_tipos.values)
plt.title('Contagem de Pokémon por Tipo Primário')
plt.xlabel('Tipo Primário')
plt.ylabel('Número de Pokémon')
plt.xticks(rotation=45)
plt.show()
```

<!-- #region id="YEz162RqJa6h" -->
- **Gráfico de Pizza:** Perfeito para mostrar a **proporção** de cada categoria em relação ao todo. Funciona melhor com poucas categorias.
    
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 675} id="EDA1WQapJcpg" outputId="34e1fbd1-f9fd-4d7a-d94f-78e0a8713284"
# --- Gráfico de Pizza: Proporção de Pokémon Lendários ---
plt.figure(figsize=(8, 8))
contagem_lendarios = df['Legendary Status'].value_counts()
plt.pie(contagem_lendarios, labels=['Comum', 'Lendário'], autopct='%1.1f%%', startangle=90)
plt.title('Proporção de Pokémon Lendários vs. Comuns')
plt.show()
```

<!-- #region id="h-EBD8WGJgsi" -->
## 4. Visualizando Distribuições (Histogramas)
<!-- #endregion -->

<!-- #region id="v_jNFHjfJkVt" -->

### 4.1. Média, Mediana e Moda
<!-- #endregion -->

<!-- #region id="NOGD9yjNJi0e" -->
Imagine os stats de `Attack` de cinco Pokémon: `[10, 20, 25, 25, 100]`.

- **Média:** É o centro de gravidade dos dados. Some tudo e divida pela contagem. `(10+20+25+25+100) / 5 = 36`. A média é muito sensível a valores extremos (outliers), como o Pokémon com 100 de ataque.
    
- **Mediana (Percentil 50):** É o valor que está exatamente no meio da fila, após ordenar os dados. Na nossa fila `[10, 20, **25**, 25, 100]`, a mediana é **25**. Ela não é afetada por outliers.
    
- **Moda:** É o valor que mais se repete. No nosso caso, é **25**.
    
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="C_iUpTWGJnqG" outputId="008eee62-0798-4888-bf80-badde0e931e6"
attack = [10, 20, 25, 25, 100]
print(f'Média: {mean(attack)}')
print(f'Mediana: {median(attack)}')
print(f'Moda: {mode(attack)}')
```

<!-- #region id="Ml6ViE9PJsv9" -->
### 4.2. Tipos de Distribuição
<!-- #endregion -->

<!-- #region id="P-uTnQG2JujY" -->
Vamos criar dados do zero para entender as "formas" mais comuns que eles podem ter.
<!-- #endregion -->

<!-- #region id="mQUUg9dSJvrY" -->
#### a) Distribuição Uniforme
<!-- #endregion -->

<!-- #region id="0hkAWaPfJrRU" -->
Todos os resultados são igualmente prováveis. Pense em um dado perfeito.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 545} id="Ygy09qc1Jyy8" outputId="515ded8c-5903-461a-a759-6b1bb6bc4898"
# Simulação do lançamento de um dado 10.000 vezes
dados_uniformes = np.random.randint(1, 7, 10000)
sns.histplot(dados_uniformes, bins=6, discrete=True)
plt.title('Distribuição Uniforme (Lançamento de um dado)')
plt.show()
```

<!-- #region id="VccoBpbIJ84p" -->
#### b) Distribuição Normal (Curva de Sino)


<!-- #endregion -->

<!-- #region id="Goi1VD1jJ-Cg" -->
É a forma mais comum na natureza. A maioria dos valores se concentra no centro, e valores extremos são raros. **Na distribuição normal perfeita, Média = Mediana = Moda**.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 545} id="NM_jbqCaJ8TU" outputId="53709d6f-8239-42a6-d1ef-8455cb98fa6e"
# Simulação de dados com distribuição normal
dados_normais = np.random.normal(loc=100, scale=15, size=10000) # loc=média, scale=desvio padrão
sns.histplot(dados_normais, kde=True)
plt.title('Distribuição Normal (Curva de Sino)')
plt.axvline(np.mean(dados_normais), color='red', linestyle='--', label=f'Média: {np.mean(dados_normais):.2f}')
plt.axvline(np.median(dados_normais), color='green', linestyle=':', label=f'Mediana: {np.median(dados_normais):.2f}')
plt.legend()
plt.show()
```

<!-- #region id="vcsEVf4GKFzz" -->
#### c) Distribuição Assimétrica (Skewed)
<!-- #endregion -->

<!-- #region id="7DueCtzaKE4M" -->


Acontece quando os dados se concentram em um dos lados, deixando uma "cauda" longa no outro. Se a cauda está à direita, a assimetria é à direita.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 545} id="-FL6l97RKI29" outputId="01d17b55-3453-4ef9-8adf-adad5cd34430"
# Simulação de dados com assimetria à direita
dados_assimetricos = np.random.beta(a=2, b=8, size=10000) * 100
sns.histplot(dados_assimetricos, kde=True)
plt.title('Distribuição com Assimetria à Direita')
plt.axvline(np.mean(dados_assimetricos), color='red', linestyle='--', label=f'Média: {np.mean(dados_assimetricos):.2f}')
plt.axvline(np.median(dados_assimetricos), color='green', linestyle=':', label=f'Mediana: {np.median(dados_assimetricos):.2f}')
plt.axvline(pd.Series(dados_assimetricos).mode()[0], color='blue', linestyle='-', label=f'Moda: {pd.Series(dados_assimetricos).mode()[0]:.2f}')
plt.legend()
plt.show()
```

<!-- #region id="lmasg0KwKcBC" -->

Note como a Média é "puxada" pela cauda longa. A ordem geralmente é: **Moda < Mediana < Média**.
<!-- #endregion -->

<!-- #region id="oZR6uX5dKjK_" -->
### 4.3. Aplicação: As Distribuições na Pokédex
<!-- #endregion -->

<!-- #region id="qTYvu-T2Kkyc" -->
#### a) Contagem por Geração:
<!-- #endregion -->

<!-- #region id="bnt9NesaKmeo" -->
- **Quase Uniforme: Contagem por Geração** A quantidade de Pokémon por geração não é perfeitamente uniforme, mas não há uma concentração óbvia em uma única geração.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 631} id="tMQcraLZKp-8" outputId="34319a2e-7678-4d3d-b358-78dcc41051f4"
sns.countplot(data=df, x='Generation', order=sorted(df['Generation'].unique()))
plt.title('Contagem de Pokémon por Geração (Aproximadamente Uniforme)')
plt.xticks(rotation=45)
plt.show()
```

<!-- #region id="etkoDpiLKwA0" -->
#### b) Soma dos Status Base

<!-- #endregion -->

<!-- #region id="HorY0uBtKxJF" -->

- **Normal: O `Base Stat Total`** A soma de vários fatores (Attack, Defense...) tende a uma distribuição normal.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="jhwlf1xyKyRE" outputId="cfcc70c4-2ad1-47f9-f065-5c739084af51"
sns.histplot(data=df, x='Base Stat Total', kde=True)
plt.title('Distribuição do "Base Stat Total" (Aproximadamente Normal)')
plt.axvline(df['Base Stat Total'].mean(), color='red', linestyle='--', label='Média')
plt.axvline(df['Base Stat Total'].median(), color='green', linestyle=':', label='Mediana')
plt.axvline(df['Base Stat Total'].mode()[0], color='blue', linestyle='-', label='Moda')
plt.legend()
plt.show()
```

<!-- #region id="0fCgHQ9OK_z4" -->
##### Teorema do Limite Central:

Por que a soma de stats (`Base Stat Total`) tende a uma distribuição normal? O Teorema do Limite Central diz que, quando somamos muitas variáveis aleatórias, a distribuição da soma se aproxima de uma normal, não importa a forma das distribuições originais! É uma das ideias mais importantes da estatística.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 545} id="MaRlq-PPLFfb" outputId="7b0529c3-91b8-4768-8e6f-797ef02c1534"
# Simulação da soma do resultado de dois dados (2d6)
dados_soma = np.random.randint(1, 7, 10000) + np.random.randint(1, 7, 10000)
sns.histplot(dados_soma, kde=True, bins=11, discrete=True)
plt.title('Soma de Dados - 2d6 (Tendendo à Normal)')
plt.axvline(np.mean(dados_soma), color='red', linestyle='--', label=f'Média: {np.mean(dados_soma):.2f}')
plt.axvline(np.median(dados_soma), color='green', linestyle=':', label=f'Mediana: {np.median(dados_soma):.2f}')
plt.legend()
plt.show()
```

<!-- #region id="bNSXjKpMLLgB" -->
#### c) Peso dos Pokemons


<!-- #endregion -->

<!-- #region id="Ae_FchyoLMc2" -->
- **Assimétrica: O Peso (`Weight (hg)`)** A maioria dos Pokémon é leve, mas uma minoria é extremamente pesada, criando uma forte assimetria à direita.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 565} id="BzUV1_4yLOkl" outputId="4807d695-9978-4bbd-fd37-015d7779a960"
sns.histplot(data=df, x='Weight (hg)', bins=50, kde=True)
plt.title('Distribuição do Peso (Forte Assimetria à Direita)')
plt.xlim(0, 2000) # Limitando o eixo X para melhor visualização
plt.axvline(df['Weight (hg)'].mean(), color='red', linestyle='--', label='Média')
plt.axvline(df['Weight (hg)'].median(), color='green', linestyle=':', label='Mediana')
plt.axvline(df['Weight (hg)'].mode()[0], color='blue', linestyle='-', label='Moda')
plt.legend()
plt.show()
```

<!-- #region id="66IUAe4yLTAG" -->
## 5. Visualizando Relações (Gráfico de Dispersão)
<!-- #endregion -->

<!-- #region id="EirXV0MXLRa8" -->


Um gráfico de dispersão nos ajuda a ver se existe e qual é a **correlação** (relação) entre duas variáveis numéricas.

**ATENÇÃO: correlação não significa causalidade!**

- **Mais bombeiros no incêndio -> Maior número de mortes:** Isso é uma **correlação espúria devido a uma variável de confusão**. A variável "escondida" é o **tamanho do incêndio**. Incêndios maiores precisam de mais bombeiros e, infelizmente, podem causar mais danos.
    
- **Número de filmes do Nicolas Cage -> Mortes por afogamento:** Este é um exemplo de **correlação espúria** ou **ilusória**. Duas variáveis podem apresentar uma tendência semelhante ao longo do tempo puramente por coincidência, sem que uma tenha qualquer influência sobre a outra.

<!-- #endregion -->

<!-- #region id="vC-ps_zmLUaM" -->
### 5.1. Tipos de Correlação
<!-- #endregion -->

```python id="P7UKqZNkLWca"
# Gerando dados artificiais para os exemplos
x = np.linspace(0, 10, 100)
ruido_fraco = np.random.normal(0, 1, 100)
ruido_forte = np.random.normal(0, 4, 100)

# Criando um DataFrame para facilitar a plotagem
dados_corr = pd.DataFrame({
    'x': x,
    'Positiva Forte': x + ruido_fraco,
    'Positiva Fraca': x + ruido_forte,
    'Negativa Forte': -x + ruido_fraco,
    'Sem Correlação': np.random.uniform(0, 10, 100),
    'Não Linear': (x-5)**2 + ruido_fraco
})
```

<!-- #region id="05t00p-eLbAl" -->
#### a) Positiva Forte

Quando a variável X aumenta, a variável Y também aumenta, e os pontos estão bem próximos de uma linha reta imaginária.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="Da8JAhBPLcXm" outputId="63e40809-5297-434c-a56b-6158735db04d"
sns.scatterplot(data=dados_corr, x='x', y='Positiva Forte').set_title('Positiva Forte')
plt.show()
```

<!-- #region id="Mlua0Te6LfGd" -->

#### b) Positiva Fraca

Quando a variável X aumenta, a variável Y também tende a aumentar, mas os pontos estão mais espalhados. A tendência ainda é visível, mas menos definida.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="m-7rnnkWLhvC" outputId="1503c233-75f6-4826-d46c-088f69872476"
sns.scatterplot(data=dados_corr, x='x', y='Positiva Fraca').set_title('Positiva Fraca')
plt.show()
```

<!-- #region id="kvlL_-6ILjq5" -->

#### c) Negativa Forte

Quando a variável X aumenta, a variável Y diminui, e os pontos estão bem alinhados. Assim como na correlação positiva, também existe a variante 'Negativa Fraca', onde os pontos estariam mais espalhados.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="xe2GirGSLlgk" outputId="adb7bfc4-cdd3-4b94-e312-fa1b483fef42"
sns.scatterplot(data=dados_corr, x='x', y='Negativa Forte').set_title('Negativa Forte')
plt.show()
```

<!-- #region id="lYiV0mB1LnSX" -->


#### d) Sem Correlação

Não há nenhuma tendência aparente. Os pontos formam uma nuvem aleatória, indicando que as variáveis não estão relacionadas.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="s3LEWPByLpiz" outputId="0d0ce48a-17d8-4f5f-de71-2e46e6883a5a"
sns.scatterplot(data=dados_corr, x='x', y='Sem Correlação').set_title('Sem Correlação')
plt.show()
```

<!-- #region id="WXO8CV7NLrsj" -->

#### e) Correlação Não Linear

Existe uma relação clara e previsível entre X e Y, mas ela não segue uma linha reta. Neste caso, a relação é parabólica (em forma de "U").

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="l929-BqfLtoO" outputId="6cc5a528-3d44-4e1e-c53e-e304a152088c"
sns.scatterplot(data=dados_corr, x='x', y='Não Linear').set_title('Não Linear')
plt.show()
```

<!-- #region id="g38kjcHHLw8U" -->

### 5.2. Relações na Pokédex

#### a) Ataque e Defesa

- **Correlação Positiva Fraca: `Attack` vs. `Defense`**
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="8ZNuFgmBLy0B" outputId="1906d9b9-430e-49fa-8b8c-d93d931feb8f"
sns.scatterplot(data=df, x='Attack', y='Defense')
plt.title('Relação entre Ataque e Defesa (Positiva Fraca)')
plt.show()
```

<!-- #region id="U-WYEe0aL1-f" -->

Adicionando uma terceira dimensão com **cor**:



<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="_kf6HTCKL3gG" outputId="5d42c8df-3c97-4898-83bc-3a340ac54211"
sns.scatterplot(data=df, x='Attack', y='Defense', hue='Speed', palette='viridis')
plt.title('Relação entre Ataque, Defesa e Velocidade')
plt.show()
```

<!-- #region id="XxW1rjK7L_Y-" -->
#### b) Velocidade e Peso

- **Correlação Negativa Fraca: `Speed` vs. `Weight (hg)`** Nossa hipótese é que Pokémon mais pesados são mais lentos.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 564} id="zoz4f9CbMAjd" outputId="cdcb5edb-3148-46b7-899f-a76ee76465b5"
sns.scatterplot(data=df, x='Weight (hg)', y='Speed')
plt.title('Relação entre Peso e Velocidade (Negativa Fraca)')
plt.xlim(0, 2500) # Limitando o peso para melhor visualização
plt.show()
```

<!-- #region id="dhDB-rLfMCt0" -->
#### c) Número do Pokemon e Ataque

- **Sem Correlação: `National Dex #` vs. `Attack`** O número do Pokémon na Pokédex não deve ter relação com seu poder de ataque.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 565} id="Hzk1mgeJMD3v" outputId="4b16ea53-d8e8-405f-c287-5564da07bf12"
sns.scatterplot(data=df, x='National Dex #', y='Attack')
plt.title('Relação entre Número da Pokédex e Ataque (Sem Correlação)')
plt.show()
```

<!-- #region id="OLtoP9NmMH0p" -->
## 6. Hora dos Exercícios!

### Exercício 1: Distribuição de Velocidade

Crie um **histograma** para a coluna `Speed`. Descreva a forma do gráfico: ele é simétrico? Possui assimetria para algum lado? O que isso nos diz sobre a velocidade da maioria dos Pokémon?

<!-- #endregion -->

```python id="gWfHbObUMIKP"

```

<!-- #region id="3ttFDUfbMKk_" -->
### Exercício 2: Pokémon por Geração

O código deste exercício já foi apresentado na seção 4.3.a). Sua tarefa é executá-lo novamente e responder: Qual geração introduziu mais Pokémon, de acordo com o gráfico?

<!-- #endregion -->

```python id="k9o6S14CMSJa"

```

<!-- #region id="65njqlXOMSa3" -->
### Exercício 3: Proporção de Lendários

O código deste exercício já foi apresentado na seção 3.1. Sua tarefa é executá-lo novamente e responder: Você acha que este é um bom caso de uso para um gráfico de pizza? Justifique.

<!-- #endregion -->

```python id="MHFvaYXFMXz1"

```

<!-- #region id="GgFJpUwMMYED" -->
### Exercício 4: Relação entre Peso e Força

Crie um **gráfico de dispersão** para investigar a relação entre o peso (`Weight (hg)`) e a força total (`Base Stat Total`). Existe uma correlação clara? O que você pode concluir?

<!-- #endregion -->

```python id="EJUaM71JMaBv"

```
