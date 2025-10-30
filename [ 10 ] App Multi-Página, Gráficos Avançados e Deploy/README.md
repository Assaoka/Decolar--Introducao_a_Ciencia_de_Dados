# Aula 10: App Multi-Página, Gráficos Avançados e Deploy!

Na aula passada, aprendemos os "blocos de montar" do Streamlit: Inputs e Layout. Hoje, vamos usar tudo isso para construir nossa Pokédex completa e, o mais importante, publicá-la na internet!
## 📋Objetivos de Hoje:
1. **Construir a Vitrine:** Aplicar o que vimos na Aula 9. 
2. **Nova Arquitetura:** Aprender a estrutura de apps multi-página (`st.Page`) e a forma correta de manter dados entre execuções (`st.session_state`).
3. **Gráficos Avançados:** Aprender Boxplot e Heatmap.
4. **Deploy:** Colocar nosso app no ar, usando GitHub e Streamlit Cloud.
5. **Próximo Nível:** Aprender a encontrar dados no Kaggle para o seu projeto final.   
## 🧱 1. A Nova Estrutura do App
Chega de ter um app em um arquivo só. Vamos usar a estrutura profissional.
### 1.1. Crie a Estrutura de Arquivos
No seu VS Code, crie a seguinte estrutura de arquivos. **Crie os arquivos `.py` vazios por enquanto.**

```python
/MeuProjetoPokedex
  |-- app.py                  <-- Nosso arquivo principal
  |-- /pages
  |   |-- 1_vitrine.py        <-- Página da Vitrine
  |   |-- 2_dashboard.py      <-- Página do Dashboard
  |-- pokemon.csv             <-- Nossos Dados
  |-- requirements.txt        <-- (Vamos criar no final)
```

Para iniciar a aplicação execute:
```cmd
streamlit run app.py
```
### 1.2. O Cérebro do App (`app.py`)
O `app.py` vai ser nosso ponto de partida. Toda vez que o site for recarregado, independente da página, ele será executado. Dessa forma, ele é ideal para fazer definições globais.

```python
"""app.py"""
import streamlit as st
import pandas as pd
```
### 1.3. Estado da Sessão: `st.session_state`
Afinal, como podemos salvar dados entre execuções ou páginas? Usamos o `st.session_state`.

Esse é um dicionário próprio do Streamlit que **persiste** durante a sessão de um usuário. Nele ficam salvos, por exemplo, o valor presente nos widgets.

```python
"""app.py"""
st.button(label="Botão", key="b1")
if st.session_state['b1']: # Pode ser st.session_state.b1 também
	st.write("Você clicou!")
```

Nós também podemos adicionar nossas próprias chaves a ele. Vamos usar isso para carregar nossos dados **apenas uma vez**:
```python
"""app.py"""
if 'df' not in st.session_state: # Se a chave 'df' não estiver no dicionário
	st.session_state['df'] = pd.read_csv("pokemon.csv")
```

Com isso, o `pokemon.csv` é lido apenas na primeira execução. Em todas as recargas seguintes, o Streamlit vai pular esse bloco.

Podemos acessar essa "variável" no nosso arquivo `pages/1_vitrine.py`:
```python
"""pages/1_vitrine.py"""
import streamlit as st
import pandas as pd

df = st.session_state['df']
st.write(df.head())
```
### 1.4. Definindo as Páginas de Forma Profissional:
Anteriormente, estávamos aproveitando o padrão de adicionar as abas presentes no `pages/` de forma nativa, mas e se quisermos personalizar essa navegação?

Podemos utilizar o `st.navigation` em conjunto com o `st.Page` para fazer isso:
```python
"""app.py"""

st.navigation([
	st.Page("pages/1_vitrine.py", title="Vitrine", icon="🐉")
	st.Page("pages/2_dashboard.py", title="Dashboard de Análise", icon="📊")
]).run()
```
## 🐉 2. Construindo a Vitrine
Agora, vamos preencher o `pages/1_vitrine.py`.
### Passo 2.1. Acesse os Dados e Crie os Filtros
Nosso objetivo é adicionar esses filtros:
1. Qual tipo?
2. Lendário?
3. Ordenar por:
	- National Dex
	- Ordem alfabética 
```python
"""pages/1_vitrine.py"""
with st.sidebar:
	tipos_unicos = sorted(df_original['Primary Typing'].unique())
	st.multiselect("Tipo:", options=tipos_unicos, key='tipos')
	st.checkbox("Lendário:", key='lendario')
	st.selectbox("Ordem", options=['National Dex', 'Name'])
```
### 2.2. Lógica de Filtragem
Sabendo os dados que queremos, como podemos filtrar esses dados?
```python
"""pages/1_vitrine.py"""
df_filtrado = df.copy()

df_filtrado = df_filtrado[
	df_filtrado['Primary Typing'].isin(st.session_state['tipos'])
	| df_filtrado['Secundary Typing'].isin(st.session_state['tipos'])
]

df_filtrado = df_filtrado # ...

# 5. Exibir a Vitrine
st.subheader(f"Exibindo {df_filtrado.shape[0]} de {df_original.shape[0]} Pokémon")
```

```python
"""pages/1_vitrine.py"""
colunas = st.columns(5)
for indice, pokemon in df_filtrado.iterrows():
    with colunas[indice % num_colunas]:
        with st.container(border=True):
            st.image(pokemon['Image'], use_column_width=True) 
            st.caption(f"**{pokemon['Name']}**")

if df_filtrado.empty:
    st.warning("Nenhum Pokémon encontrado com esses filtros.")
```
## 📊 3. Criando o Dashboard
Nossa ideia agora é exibir informações relevantes sobre os pokemons selecionados.

```python
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

As bibliotecas matplotlib e seaboarn precisam ser instaladas para poderem ser importadas.
```cmd
pip install matplotlib seaborn
```

### 3.1. Acessar Dados e Adicionar Filtros
Atualmente, nossos filtros são realizados na aba vitrine, mova essa lógica para o app.py utilizando o `Estado da Sessão`.

### 3.2. Adicionando Gráficos ao Streamlit
Vamos gerar um gráfico de pizza da quantidade de lendários que existem no nossos dados. Para isso, basta gerar o gráfico que vimos aula passada e utilizar o comando `st.pyplot`

Precisamos apenas de uma pequena mudança. Precisamos usar o ax ao invés do plt para imprimir no streamlit:

```python
"""2_dashboard.py"""
fig, ax = plt.subplots() # Mudança 1
contagem_lendarios = df_filtrado['Legendary Status'].value_counts()
ax.pie(contagem_lendarios, labels=['Comum', 'Lendário']) # Mudança 2
st.pyplot(fig)
```

### 3.3. Boxplot
O Boxplot é ótimo para comparar a distribuição de poder entre vários grupos.
```python
fig, ax = plt.subplots(figsize=(15, 8))
sns.boxplot(
    data=df_filtrado, 
	x='Primary Typing', 
    y='Base Stat Total', 
    ax=ax
)
```

### 3.4. Heatmap (Correlação)
O Heatmap nos mostra quais status andam juntos (correlação).

```python
fig, ax = plt.subplots(figsize=(10, 8))

corr = df_filtrado[colunas_stats].corr()
sns.heatmap(
	corr, 
	annot=True,     # Escreve os números
	fmt=".2f",      # Formato com 2 casas decimais
	cmap='coolwarm', # Paleta de cores
	ax=ax
)
```

## 🛜 4. Fazendo o Deploy (Colocando na Internet)
Agora, vamos mostrar nosso projeto para o mundo!
### 4.1. Crie uma Conta no GitHub
1. Vá para [github.com](https://github.com "null").
2. Clique em "Sign up".
3. Clique em **"Sign in with Google"**
4. Siga os passos de verificação. Você está dentro!
### 4.2. Crie seu Primeiro Repositório
Um "repositório" é uma pasta de projeto no GitHub.
1. No canto superior direito, clique no ícone `+` e selecione **"New repository"**.
2. Dê um nome ao seu repositório. Ex: `minha-pokedex`.
3. Marque como **"Public"**. Isso é essencial para o deploy gratuito.
4. Clique em **"Create repository"**.
### 4.3. Faça o "Upload" dos Arquivos (O jeito fácil)
Você será levado para a página do seu repositório.
1. Clique no link **"uploading an existing file"**. 
2. Arraste seus 4 arquivos para a janela do navegador:
    - `app.py`
    - `pages/1_vitrine.py`
    - `pages/2_dashboard.py`
    - `pokemon.csv`
3. **Espere!** Ainda falta um arquivo. 
### 4.4. O Arquivo `requirements.txt`
O Streamlit Cloud precisa saber quais bibliotecas seu app usa.
1. No VS Code, crie um novo arquivo chamado `requirements.txt`. 
2. Execute o seguinte código no terminal:
```cmd
pip freeze > requirements.txt
```
3. Agora, **arraste também o `requirements.txt`** para a página de upload do GitHub.
4. Clique em **"Commit changes"**.

Seus 5 arquivos estão agora no GitHub!
### 4.5. Deploy no Streamlit Cloud
1. Vá para [share.streamlit.io](https://share.streamlit.io "null").
2. Faça login **"Continue with GitHub"**. Autorize a conexão.
3. Clique em **"New app"**.
4. Em "Repository", selecione seu repositório.   
5. O "Main file path" deve ser `app.py`.    
6. Clique em **"Deploy!"**.

Aguarde 1 ou 2 minutos. Você verá uma tela de instalação (os "Logs"). Quando terminar, seu app estará no ar, em uma URL pública que você pode compartilhar com qualquer pessoa!
## 5: Onde Achar Dados?
Você está quase pronto para o seu projeto final, mas onde encontrar dados

O [Kaggle](https://www.kaggle.com "null") é o maior site de Ciência de Dados do mundo, e a melhor fonte de datasets.
1. Vá para [kaggle.com](https://www.kaggle.com "null").
2. No menu da esquerda, clique em **"Datasets"**.
3. Use a barra de busca para procurar **qualquer assunto** do seu interesse. 
4. Filtre por arquivos **CSV**.    
5. Ao encontrar um dataset, clique em **"Download"**.

Você agora tem um `seu_dataset.csv` e todo o conhecimento para construir um app Streamlit para analisá-lo, exatamente como fizemos com os Pokémon.