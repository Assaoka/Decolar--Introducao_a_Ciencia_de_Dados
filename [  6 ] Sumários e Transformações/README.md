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
<a href="https://colab.research.google.com/github/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/blob/main/%5B%20%206%20%5D%20Sum%C3%A1rios%20e%20Transforma%C3%A7%C3%B5es/Sum%C3%A1rios%20e%20Transforma%C3%A7%C3%B5es.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<!-- #endregion -->

<!-- #region id="IimZrzh18Es1" -->
# Aula 6: A Análise do Mestre de Dados: Sumários, Filtros Avançados e Transformações

Na nossa última jornada (Aula 5), você deu um passo gigante: aprendeu a usar o Pandas para capturar Pokémon (ou seja, carregar dados de um arquivo) e a dar uma primeira espiada neles com comandos como `.head()` e `.tail()`.

Hoje, vamos aprofundar nossas habilidades de análise. Você vai aprender a fazer perguntas muito mais inteligentes e específicas para a nossa Pokédex e até a criar novas informações sobre os Pokémon que não existiam no arquivo original. Vamos lá!

### **1. Revisão Rápida: Relembrando nossos Poderes**

Antes de aprender novos movimentos, todo bom treinador revisa os que já conhece. Vamos relembrar o que fizemos na última aula:

1. **Importamos o Pandas:** O nosso kit de ferramentas. `import pandas as pd`
    
2. **Carregamos a Pokédex:** Usamos o `pd.read_csv('pokemon.csv')` para ler o arquivo.
    
3. **Inspecionamos os Dados:** Usamos `.head()` para ver o começo, `.tail()` para ver o fim e `.info()` para ver a estrutura da nossa tabela.
    
4. **Fizemos Filtros Simples:** Aprendemos a encontrar Pokémon com uma característica específica, como `df[df['Primary Typing'] == 'fire']`.
    

Vamos começar carregando nossa Pokédex novamente. Execute o código abaixo:
<!-- #endregion -->

```python id="9PlQc16c8OYx"
# Importando nossa biblioteca principal e dando o apelido de 'pd'
import pandas as pd
```

```python id="FwifVEg-8QFu"
# Endereço do nosso arquivo de dados
endereco = 'https://raw.githubusercontent.com/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/refs/heads/main/pokemon.csv'

# Lendo o arquivo CSV e guardando na variável 'df' (nosso DataFrame)
df = pd.read_csv(endereco)
```

```python colab={"base_uri": "https://localhost:8080/", "height": 287} id="9wAbhg088KPR" outputId="91a7af17-2cd7-4efc-bcfa-62ce7835a55b"
# Mostrando os 5 primeiros Pokémon para garantir que tudo deu certo
display(df.head())
```

<!-- #region id="2ncNJ1s58e_I" -->
### **2. A Ficha Técnica da Pokédex (`.describe()`)**

Imagine que você pudesse pedir ao Professor Carvalho um resumo completo sobre os poderes de todos os Pokémon de uma só vez. Em vez de olhar um por um, ele te entregaria uma ficha com a **média** de força, o Pokémon **mais forte**, o **mais fraco** e muito mais.

É exatamente isso que o comando `.describe()` faz para as colunas que têm números.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 300} id="iDsnTgxb8hzw" outputId="8ffc7787-2b65-43d7-c0a7-e377af1ae04f"
# Usando .describe() para analisar os stats de batalha
# Selecionamos apenas as colunas que queremos analisar
df[['Attack', 'Defense', 'Speed', 'Base Stat Total']].describe()
```

<!-- #region id="z2QJpaAD84Db" -->
**O que significa cada linha desse resumo?**

- `count`: A contagem de quantos Pokémon têm um valor para aquele stat. Se o número for igual para todos, significa que não temos dados faltando!
    
- `mean` (**Média**): Se a gente somasse o "Attack" de TODOS os Pokémon e dividisse pelo número de Pokémon, chegaríamos nesse valor. É o valor "típico" de ataque.
    
- `std` (**Desvio Padrão**): Esse nome é um pouco assustador, mas a ideia é simples!
    
    - **Se o número for baixo:** Significa que a maioria dos Pokémon tem um "Attack" bem parecido com a média. Não há muita variação.
        
    - **Se o número for alto:** Significa que os valores de "Attack" são muito espalhados. Existem Pokémon super fracos e outros super fortes, bem longe da média.
        
- `min`: O menor valor encontrado. É o "Attack" do Pokémon mais fraco.
    
- `25%` (Primeiro Quartil): Se a gente colocar todos os Pokémon em uma fila, do mais fraco ao mais forte, este é o valor do Pokémon que está a um quarto do caminho. Ele é mais forte que 25% de todos os outros.
    
- `50%` (Mediana): Este é o Pokémon que está EXATAMENTE no meio da fila. Metade dos Pokémon é mais fraca que ele, e a outra metade é mais forte.
    
- `75%` (Terceiro Quartil): É o valor do Pokémon que está a três quartos do caminho na fila. Ele é mais forte que 75% de todos os outros.
    
- `max`: O maior valor encontrado. É o "Attack" do Pokémon mais forte de todos!
    

### **3. Contando Tipos de Pokémon (`.value_counts()`)**

Você já se perguntou qual o tipo de Pokémon mais comum? Água? Grama? Normal? Contar isso na mão seria impossível!

Para nossa sorte, temos o poder `.value_counts()`, que conta quantas vezes cada valor aparece em uma coluna. É perfeito para colunas de texto, como 'Primary Typing'.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 679} id="vJKQa0lA86yD" outputId="e7abf461-7b16-4782-ab82-c12b88e047b3"
# Contando quantos Pokémon existem para cada tipo primário
df['Primary Typing'].value_counts()
```

<!-- #region id="G34ZMXu79HKu" -->
Agora sabemos que o tipo "Water" (Água) é o mais comum de todos!
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 679} id="X9Us6K7w9AoI" outputId="1f30e359-ab40-40ea-ede1-f500de238355"
# Também podemos ver em porcentagem, para ter uma ideia da proporção
# O 'normalize=True' calcula a proporção (um número de 0 a 1)
# e nós multiplicamos por 100 para ver em porcentagem.
df['Primary Typing'].value_counts(normalize=True) * 100
```

<!-- #region id="ZyEid7op938N" -->
### **4. Filtros Avançados: Fazendo Perguntas de Mestre (`&`, `|`)**

Na última aula, você fez perguntas simples, como "Quais Pokémon são do tipo Fogo?".

Um Mestre de Dados faz perguntas mais complexas! Por exemplo:

- "Quais Pokémon são do tipo 'Grama' **E** também do tipo 'Veneno'?"
    
- "Quais Pokémon são Lendários **OU** têm um 'Base Stat Total' maior que 600?"
    

Para isso, usamos dois operadores mágicos:

- `&` (significa **E**): As duas condições precisam ser verdadeiras.
    
- `|` (significa **OU**): Pelo menos uma das condições precisa ser verdadeira.
    

**IMPORTANTE:** Cada condição que você cria precisa estar dentro de parênteses `()`!
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 439} id="hH92SvwU9_sn" outputId="31f90a73-94cf-430d-9aa4-8ab0843aa7d7"
# Exemplo com E (&): Pokémon de Fogo E Voadores
condicao_fogo = (df['Primary Typing'] == 'fire')
condicao_voador = (df['Secondary Typing'] == 'flying')

df[condicao_fogo & condicao_voador]
```

```python colab={"base_uri": "https://localhost:8080/", "height": 439} id="kMHOyGKI-XR-" outputId="aaa60e9d-cb07-4a5b-f804-bd8ef42b9a19"
# Versão resumida:
# Exemplo com E (&): Pokémon de Fogo E Voadores
df[(df['Primary Typing'] == 'fire') & (df['Secondary Typing'] == 'flying')]
```

```python colab={"base_uri": "https://localhost:8080/", "height": 1000} id="sdPX5Wwr-qlp" outputId="f18291f3-a919-431b-bf71-caa572a46967"
# Exemplo com OU (|): Pokémon com ataque MUITO alto OU defesa MUITO alta
df[(df['Attack'] > 150) | (df['Defense'] > 150)]
```

<!-- #region id="4f2k4kU-_Ftv" -->
### **5. Transformando Dados: Criando Novas Informações (`.map` e `.apply`)**

E se a gente quisesse criar uma informação nova que não existe na Pokédex? Por exemplo, traduzir a coluna `Legendary Status` (que está como `True` ou `False`) para textos mais amigáveis como "Sim" e "Não"?

Para isso, temos dois poderes incríveis: `.map()` e `.apply()`.

#### **5.1. Usando `.map()` para "Traduzir" Valores**

O `.map()` é perfeito para quando você quer substituir valores de uma coluna por outros, usando um **dicionário** como se fosse um tradutor.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 676} id="M4iCf32Z_K-a" outputId="2a4311f3-87b2-4de6-cc27-ae03b06ea131"
# 1. Criamos nosso "dicionário tradutor"
mapa_tradutor = {
    True: 'Sim',
    False: 'Não'
}

# 2. Usamos .map() para criar uma nova coluna "Lendario" com os valores traduzidos
df['Lendario'] = df['Legendary Status'].map(mapa_tradutor)
display(df[['Name', 'Legendary Status', 'Lendario']].sample(20))
```

<!-- #region id="OzFOdJjD_hms" -->
#### **5.2. Usando `.apply()` para Aplicar Regras Complexas**

O `.apply()` é ainda mais poderoso. Ele permite aplicar uma **função** (um conjunto de regras que a gente cria) para cada valor de uma coluna.

Vamos criar uma regra para classificar os Pokémon em "Tiers" de poder, com base no `Base Stat Total`.
<!-- #endregion -->

```python id="v-F-I5oR_lDN"
# 1. Primeiro, criamos nossa função com as regras de classificação
def classificar_poder(total_de_stats):
    if total_de_stats > 550:
        return 'Nível S (Super Raro)'
    elif total_de_stats > 450:
        return 'Nível A (Forte)'
    elif total_de_stats > 300:
        return 'Nível B (Comum)'
    else:
        return 'Nível C (Básico)'
```

```python colab={"base_uri": "https://localhost:8080/", "height": 676} id="D7uaiV_m_pDE" outputId="cb4c3a36-1e10-45e3-ab5e-b5c545265ce4"
# 2. Agora, usamos .apply() para aplicar essa função em cada valor da coluna 'Base Stat Total'
df['Power Tier'] = df['Base Stat Total'].apply(classificar_poder)
df[['Name', 'Base Stat Total', 'Power Tier']].sample(20)
```

<!-- #region id="bgxK-Pjc_48U" -->
### **8. Hora dos Desafios!**

Agora é sua vez de praticar seus novos poderes de Mestre de Dados!

**Desafio 1: A Elite de Kanto** Use um filtro composto (`&`) para criar um novo DataFrame chamado `elite_kanto` que contenha apenas Pokémon da `generation-i` **E** que tenham um `Base Stat Total` maior que 500. Mostre os 5 primeiros desse novo DataFrame.
<!-- #endregion -->

```python id="OgD2JxET_5um"

```

<!-- #region id="avbpXPNv_7Z2" -->
**Desafio 2: Contagem de Gerações** Qual geração (`Generation`) tem o maior número de Pokémon? Use o `.value_counts()` para descobrir e mostrar a lista.
<!-- #endregion -->

```python id="pACBXxxl_8CV"

```

<!-- #region id="TO4wxFhyACUZ" -->
**Desafio 3: O mais Rápido ou o mais Forte?** Crie um DataFrame chamado `rapidos_ou_fortes` que contenha todos os Pokémon que tenham `Speed` maior que 120 **OU** `Attack` maior que 120. Mostre uma amostra aleatória de 5 Pokémon desse grupo.
<!-- #endregion -->

```python id="S2B4yHh_ABjt"

```

<!-- #region id="vSCKipEvAHkY" -->
**Desafio 4: Classificação de Peso** Usando `.apply()` e uma função que você mesmo vai criar, crie uma nova coluna chamada `Categoria de Peso`. As regras são:
- Se `Weight (hg)` for maior que 2000, classifique como "Super Pesado".   
- Se for entre 500 e 2000, classifique como "Pesado".
- Se for menor que 500, classifique como "Leve". Mostre a nova coluna junto com 'Name' e 'Weight (hg)'.
<!-- #endregion -->

```python id="t6BJOt6sAKsU"

```

<!-- #region id="MfiINzpM7_U5" -->

    

**Desafio 5: Análise dos Psíquicos** Use o `.describe()` para ver um resumo estatístico (`Attack`, `Defense`, `Speed`) apenas dos Pokémon do tipo Psíquico (`Primary Typing == 'psychic'`). Será que eles são, em média, mais rápidos ou mais fortes que a média geral que vimos no início da aula?

Parabéns por chegar até aqui! Você está cada vez mais perto de se tornar um verdadeiro Mestre de Análise de Dados!
<!-- #endregion -->

```python id="WjDlNAXe79yB"

```
