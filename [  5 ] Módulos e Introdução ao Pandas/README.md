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
    language: python
    name: python3
---

<!-- #region id="view-in-github" colab_type="text" -->
<a href="https://colab.research.google.com/github/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/blob/main/%5B%20%205%20%5D%20M%C3%B3dulos%20e%20Introdu%C3%A7%C3%A3o%20ao%20Pandas/M%C3%B3dulos%20e%20Introdu%C3%A7%C3%A3o%20ao%20Pandas.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<!-- #endregion -->

<!-- #region id="0a098fa7" -->
# Aula 5: O Kit do Treinador Pokémon: Capturando e Inspecionando Dados

Hoje vamos dar um salto gigantesco em nossas habilidades. Vamos aprender a usar "poderes" que outros programadores criaram e a trabalhar com dados de verdade, que ficam salvos no computador!
<!-- #endregion -->

<!-- #region id="13472bb4" -->
### 1. O que são Módulos (ou Bibliotecas)?

Imagine que você quer construir um robô. Você não precisa inventar o parafuso, a roda ou o motor do zero, certo? Você usa peças que já existem!

Na programação, é a mesma coisa. Um **módulo** (ou **biblioteca**) é um conjunto de "peças" — funções e ferramentas prontas — que outros programadores criaram e disponibilizaram para nós. Em vez de reinventar a roda, nós importamos uma biblioteca e usamos suas ferramentas.

Um dos principais motivos para a popularidade do Python é a enorme quantidade de bibliotecas disponíveis para praticamente qualquer tarefa que você possa imaginar: desde análise de dados, inteligência artificial, até desenvolvimento web e jogos.

Hoje, vamos usar a biblioteca mais famosa para análise de dados: o **Pandas**.

<!-- #endregion -->

<!-- #region id="7876aded" -->
### 2. O que é o Pandas?

O **Pandas** é uma biblioteca focada em trabalhar com **dados tabulares** (pense em tabelas do Excel ou do Google Sheets). Ele vem com dezenas de funções prontas que nos ajudam a ler, manipular, analisar e até salvar esses dados de forma muito fácil e eficiente.

Para começar a usá-lo, nosso primeiro passo é sempre o mesmo: importar a biblioteca.
<!-- #endregion -->

```python id="570a7f08"
# Vamos importar a biblioteca pandas e dar a ela o apelido de 'pd'
# Este é um padrão universal, todo cientista de dados faz isso!
import pandas as pd
```

<!-- #region id="98aeecb6" -->
### 3. De onde vêm os dados? O formato CSV

Nossos programas até agora só guardavam informações enquanto estavam rodando (na memória RAM). Se fechássemos o programa, tudo era perdido. Para trabalhar com dados de verdade, precisamos salvá-los de forma permanente (no HD).

Uma das formas mais comuns de salvar dados tabulares é no formato **CSV** (_Comma-Separated Values_, ou Valores Separados por Vírgula).

Abra um arquivo CSV no bloco de notas e você verá algo assim:
<!-- #endregion -->

<!-- #region id="b2724672" -->
```csv
Name,National Dex #,Primary Typing,Secondary Typing,Secondary Typing Flag,Generation,Legendary Status,Form,Alt Form Flag,Evolution Stage,Number of Evolution,Color ID,Catch Rate,Height (dm),Weight (hg),Height (in),Weight (lbs),Base Stat Total,Health,Attack,Defense,Special Attack,Special Defense,Speed
bulbasaur,1,grass,poison,True,generation-i,False,Base,False,1,3,green,45,7,69,28,15,318,45,49,49,65,65,45
ivysaur,2,grass,poison,True,generation-i,False,Base,False,2,3,green,45,10,130,39,29,405,60,62,63,80,80,60
venusaur,3,grass,poison,True,generation-i,False,Base,False,3,3,green,45,20,1000,79,220,525,80,82,83,100,100,80
venusaur-mega,3,grass,poison,True,generation-i,True,Mega,True,3,3,green,45,24,1555,94,343,625,80,100,123,122,120,80
charmander,4,fire,,False,generation-i,False,Base,False,1,3,red,45,6,85,24,19,309,39,52,43,60,50,65
charmeleon,5,fire,,False,generation-i,False,Base,False,2,3,red,45,11,190,43,42,405,58,64,58,80,65,80
charizard,6,fire,flying,True,generation-i,False,Base,False,3,3,red,45,17,905,67,200,534,78,84,78,109,85,100
charizard-mega-x,6,fire,dragon,True,generation-i,True,Mega X,True,3,3,red,45,17,1105,67,244,634,78,130,111,130,85,100
charizard-mega-y,6,fire,flying,True,generation-i,True,Mega Y,True,3,3,red,45,17,1005,67,222,634,78,104,78,159,115,100
squirtle,7,water,,False,generation-i,False,Base,False,1,3,blue,45,5,90,20,20,314,44,48,65,50,64,43
wartortle,8,water,,False,generation-i,False,Base,False,2,3,blue,45,10,225,39,50,405,59,63,80,65,80,58
blastoise,9,water,,False,generation-i,False,Base,False,3,3,blue,45,16,855,63,188,530,79,83,100,85,105,78
blastoise-mega,9,water,,False,generation-i,True,Mega,True,3,3,blue,45,16,1011,63,223,630,79,103,120,135,115,78
```
<!-- #endregion -->

<!-- #region id="979dbc57" -->
Cada linha é uma linha da tabela, e as vírgulas separam os valores de cada coluna. Simples, mas poderoso!

O Pandas consegue ler esses arquivos e transformá-los magicamente em uma tabela superpoderosa chamada **DataFrame**.
<!-- #endregion -->

```python id="9eaba190" outputId="260dd8d4-164f-4b0a-c27a-426ddb80d6fb"
# O Pandas lê o arquivo CSV e cria nosso DataFrame.
# Vamos usar o comando display() para visualizá-lo de forma mais bonita no Colab.
endereco = '../pokemon.csv'
df = pd.read_csv(endereco)
print(df)
```

<!-- #region id="5bb05925" -->
O comando `display()` é usado para mostrar o DataFrame de uma forma mais bonita, especialmente em ambientes como o Jupyter Notebook ou Google Colab. Ele formata a saída para que pareça uma tabela, facilitando a visualização dos dados.
<!-- #endregion -->

```python id="92415011" outputId="6a73ba20-d51a-4717-a4db-ae8c58cdc045"
display(df)
```

<!-- #region id="b7e4e428" -->
### 4. Inspeção Inicial e Manipulação de Dados

Agora que a nossa Pokédex está carregada no DataFrame `df`, vamos aprender os movimentos de um verdadeiro Mestre de Dados.
<!-- #endregion -->

<!-- #region id="71fc4615" -->
#### 4.1. Espiando os Dados: `head`, `tail` e `sample`
- `.head(n)`: Mostra as `n` primeiras linhas (ótimo para ver o começo).   
- `.tail(n)`: Mostra as `n` últimas linhas (ótimo para ver o final).
- `.sample(n)`: Mostra `n` linhas aleatórias (ótimo para ter uma ideia geral).
<!-- #endregion -->

```python id="25dce3c2" outputId="eb2f0772-f9ab-4683-d6a3-a2201eb25f99"
# Vendo os 5 primeiros Pokémon
print("--- Início da Pokédex (Head) ---")
display(df.head())
```

```python id="efb40f20" outputId="4e85da8d-5bac-44b3-b286-cb531b8c0675"
# Vendo os 5 últimos Pokémon
print("\n--- Final da Pokédex (Tail) ---")
display(df.tail())
```

```python id="c15a3a95" outputId="63267daf-6aa3-485b-9631-969dd93550f1"
# Vendo 5 Pokémon aleatórios
print("\n--- Amostra Aleatória da Pokédex (Sample) ---")
display(df.sample(5))
```

<!-- #region id="6e3c4cb1" -->
#### 4.2. Informações Técnicas: `info` e `shape`
- `.shape`: Nos diz as dimensões da tabela (linhas, colunas).
- `.info()`: Nos dá um raio-x completo, incluindo o tipo de dado de cada coluna e o uso de memória (muito útil para ver se há dados faltando!).
<!-- #endregion -->

```python id="307949f2" outputId="91a1384d-3d6d-4d94-9a0f-7117dc6b102a"
# Mostra uma tupla com (número_de_linhas, número_de_colunas)
print(f"Nossa Pokédex tem {df.shape[0]} Pokémon e {df.shape[1]} atributos.")
```

```python id="3c80de89" outputId="4e39ce61-40c3-4a0a-a81c-c3c9cddeba8e"
# Exibe o resumo técnico. memory_usage='deep' nos dá um cálculo de memória mais preciso.
print("\n--- Raio-X da Pokédex (Info) ---")
df.info(memory_usage="deep")
```

<!-- #region id="f847f624" -->
#### 4.3. Selecionando e Operando com Colunas
Podemos pegar colunas específicas para focar nossa análise e até fazer operações matemáticas com elas!
<!-- #endregion -->

```python id="f27582ab" outputId="017944c6-d7ae-4c67-f427-d40144ce6da2"
# Selecionando uma coluna
df['Name']
```

```python id="5aa4655d" outputId="5b71cc29-cf4e-461e-963d-0a6074b85b19"
# Selecionando múltiplas colunas
stats_essenciais = df[['Name', 'Attack', 'Defense', 'Speed']]
print("--- Stats Essenciais ---")
stats_essenciais.head()
```

```python id="4176311a" outputId="b121bf7a-b134-42d7-805e-0673977eaf7e"
# Podemos criar uma nova coluna! Que tal um 'Total Power' somando Ataque e Defesa?
df['Total Power'] = df['Attack'] + df['Defense'] + df['Speed']
print("\n--- Criamos a coluna 'Total Power' ---")
df[['Name', 'Attack', 'Defense', 'Speed', 'Total Power']].head()
```

<!-- #region id="99920cbb" -->
#### 4.4. Filtrando: A Arte de Fazer Perguntas

E se quisermos encontrar apenas os Pokémon do tipo 'Fire'? Ou os que são da Geração I? Para isso, usamos **filtros**. A sintaxe é: `df[ <condição> ]`.
<!-- #endregion -->

```python id="e4a3cfe0" outputId="783b4c04-8058-4db2-92f2-9036d9f69954"
# Encontrando todos os Pokémon do tipo Fogo
df_fogo = df[df['Primary Typing'] == 'fire']
print("--- Apenas Pokémon do tipo Fogo ---")
df_fogo.head()
```

```python id="6b0060cb" outputId="db4930f6-5f02-4982-c0c8-3dd33abeabdd"
# Encontrando Pokémon com Ataque maior que 150
df_super_ataque = df[df['Attack'] > 150]
print("\n--- Apenas Pokémon com Ataque SUPERIOR a 150 ---")
df_super_ataque
```

<!-- #region id="fa9ca1a4" -->
#### 4.5. Ordenando: Quem é o mais forte?

Depois de filtrar, muitas vezes queremos ordenar os resultados. Usamos `.sort_values()`.

<!-- #endregion -->

```python id="567af18e" outputId="62278e3d-0b67-478d-8efe-47fc27e62d89"
# Pegando os Pokémon de Fogo e ordenando pelo Ataque, do maior para o menor
df_fogo_mais_forte = df_fogo.sort_values(by='Attack', ascending=False)
print("--- Top 5 Pokémon de Fogo, ordenados pelo Ataque ---")
display(df_fogo_mais_forte.head())
```

<!-- #region id="ddb3d60c" -->
### 5. Hora dos Exercícios!

Vamos praticar esses novos movimentos.
<!-- #endregion -->

<!-- #region id="f0f75f22" -->
**1. Os Iniciais da Geração 1:** Crie um DataFrame que contenha apenas Bulbasaur, Charmander e Squirtle.

<!-- #endregion -->

```python id="2971b486"

```

<!-- #region id="cc7fc216" -->
**2. O Pokémon mais Rápido:** Encontre o Pokémon com o maior valor de `Speed` em todo o dataset.
<!-- #endregion -->

```python id="a1252c56"

```

<!-- #region id="3088137d" -->
**3. Pesos Pesados:** Encontre todos os Pokémon que pesam (coluna `Weight (hg)`) mais de 70 kg.

Obs: 1 kg = 10 hg.
<!-- #endregion -->

```python id="631baacb"

```

<!-- #region id="b4292ab7" -->
**4. Fraqueza Psíquica:** Encontre todos os Pokémon do tipo `Bug` que sejam da `generation-i`.
<!-- #endregion -->

```python id="44fd545f"

```

<!-- #region id="c8906c36" -->
**5. Top 5 Defensores:** Crie um DataFrame com os 5 Pokémon com a maior `Defense`.
<!-- #endregion -->

```python id="25cb75a4"

```

<!-- #region id="2f97c94c" -->
**6. Elite Lendária:** Crie um DataFrame com todos os Pokémon lendários (`Legendary Status` igual a `True`), ordene-os pelo `Base Stat Total` (do maior para o menor) e salve esse DataFrame em um novo arquivo CSV chamado `legendary_pokemon.csv`.
<!-- #endregion -->

```python id="aad3e1f9"

```
