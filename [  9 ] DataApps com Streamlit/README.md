# Aula 9: Construindo sua Primeira Aplicação Web com Streamlit
Nas últimas aulas, nos tornamos mestres em analisar dados com Pandas e visualizar padrões com Matplotlib/Seaborn. Hoje, vamos dar o passo mais empolgante: aprender a construir uma **aplicação web interativa** para exibir nossas análises para o mundo, usando o **Streamlit**.

Nosso foco hoje será em dois pilares:
1. **Inputs:** Os componentes que permitem ao usuário interagir com nosso app (botões, caixas de seleção, sliders).
2. **Layout:** As ferramentas para organizar nosso app e não deixar tudo em uma única coluna (barras laterais, colunas).

Nosso projeto final da aula será construir a "Vitrine" da nossa Pokédex, exibindo os Pokémon em um grid com filtros interativos.

## 1. O que é o Streamlit?
Streamlit é uma biblioteca que transforma scripts de dados em aplicações web em minutos. A "mágica" dele é simples: **toda vez que o usuário interage com um "widget" (um botão, um slider), o script Python inteiro roda de cima a baixo.**

Isso torna o desenvolvimento incrivelmente rápido e intuitivo.

### 1.1. Instalação
Se você ainda não o tem, abra seu terminal (no VS Code, vá em `Terminal > New Terminal`) e instale o Streamlit e o Pandas:

```cmd
pip install streamlit pandas
```

### 1.2. Como Rodar seu Primeiro App
1. Crie um novo arquivo chamado `app.py`.   
2. Digite o seguinte código nele:

```python
import streamlit as st
st.write("Olá, Mundo!")
```

3. Salve o arquivo.
4. No seu terminal, digite:
 
```cmd
streamlit run app.py
```

5. Seu navegador vai abrir automaticamente com sua aplicação!
6. **Teste a Mágica:** Mude o texto no seu código (ex: `st.write("Olá, Pokémon!")`) e **salve o arquivo**.
7. Veja o app no navegador se atualizar instantaneamente (na barra superior, talvez seja preciso clicar em "Rerun" ou "Always rerun").

## 2. Texto e Markdown

O comando `st.write()` é um "canivete suíço": ele tenta exibir o que você passar da melhor forma possível. Quando ele recebe uma string, ele a interpreta usando a linguagem de marcação **Markdown**, o que nos permite formatar o texto facilmente, sem precisar saber HTML.
### 2.1. Títulos e Subtítulos
Para organizar seu texto de forma hierárquica, utilizamos o caractere `#`. A quantidade dele representa o nível daquele texto.
```markdown
# Título (Nível 1)
## Subtítulo (Nível 2)
### Subsubtítulo (Nível 3)
#### ...
```

### 2.2. Negrito, Itálico e Destaque
Para usar essas variações nós colocamos o texto dentro de certos caracteres
```markdown
**Negrito**
*Itálico*
`Destaque`
```

### 2.3. Listas ou Enumerações
Para usar esse tipo de marcação, utilizamos hifens, asteriscos ou números no começo da linha:
```markdown
- Elemento 1
- Elemento 2
	- Subelemento 2.1
	- Subelemento 2.2 
- Elemento 3
  
- [ ] Tarefa 1
- [x] Tarefa 2 (Concluida)
- [ ] Tarefa 3
      
1. Tópico 1
2. Tópico 2
3. Tópico 3
```

### 2.4. Divisão:
Para criar uma linha que separa 2 blocos você pode usar os caracteres `___`

```markdown
---
```

### 2.5. Links
Para criar um link, basta adicionar o texto entre colchetes seguido do link entre parênteses:
```markdown
[Texto do Link](https://streamlit.io)
```

## 3. Widgets de Input

Vamos adicionar os widgets mais importantes ao nosso `app.py`. A parte mais importante é entender que **cada widget retorna um valor** para uma variável.

### 3.1. Botão
Esse widget retorna um valor Booleano (`True` ou `False`). Ele será `True` **apenas** na execução do script que foi causada pelo clique no botão.
```python
import streamlit as st

clicou = st.button("Clique-me!")
if clicou:
    st.write("Você clicou no botão! 🎉")
    st.balloons() # Comemoração!
```

### 3.2. Checkbox
Similar ao botão, retorna um Booleano (`True` se marcado, `False` se desmarcado). A grande diferença é que o estado do checkbox **persiste** entre as execuções do script. O botão só é `True` no exato momento do clique.

```python
aceito = st.checkbox("Eu aceito os termos e condições")
if aceito:
    st.write("Termos aceitos!")
```

### 3.3. Caixa de Seleção:
Exibe uma lista de opções para o usuário escolher apenas uma. O valor da opção selecionada é retornado para a variável.

```python
opcao_sb = st.selectbox(
    "Qual seu Pokémon inicial favorito?",
    ("Nenhum", "Bulbasaur", "Charmander", "Squirtle")
)
st.write(f"Você escolheu: **{opcao_sb}**")
```

Uma variante é o `multiselect`, que permite ao usuário selecionar _várias_ opções de uma lista.

```python
opcoes_ms = st.multiselect(
    "Quais tipos de Pokémon você mais gosta?",
    ["Fire", "Water", "Grass", "Electric", "Psychic", "Dragon"],
    default=["Fire", "Dragon"] # Opções padrão
)
st.write(f"Você selecionou: **{opcoes_ms}**")
```

### 3.4. Controle Deslizante
Permite ao usuário selecionar um valor (ou um intervalo) arrastando um controle deslizante. É ótimo para filtros numéricos.
```python
nivel = st.slider("Qual o nível do seu Pokémon?", 1, 100, 25) # min, max, default
st.write(f"Nível selecionado: **{nivel}**")
```

### 3.5. Texto Livre
Um campo clássico para o usuário digitar um texto como entrada do programa.
```python
nome_treinador = st.text_input("Qual o seu nome?", "Ash Ketchum")
st.write(f"Olá, **{nome_treinador}**!")
```

**Salve o arquivo** e brinque com os widgets no seu app. Veja como o texto de resposta muda a cada interação.

## 4. Layout da Página
Além de adicionar widgets, podemos controlar _onde_ eles aparecem na tela, criando layouts mais organizados e profissionais.

### 4.1. Configurações de Página
Este comando **deve ser a primeira instrução `st`** no seu script, caso contrário, causará um erro. Ele nos permite definir o título da aba do navegador, um ícone e o layout (largura) padrão da página.

```python
st.set_page_config(
    page_title="Aula 9 - Playground",
    page_icon="🤖",
    layout="centered" # "wide" ou "centered"
)
````

### 4.2. Barra Lateral
A barra lateral (`sidebar`) é o local ideal para colocar filtros e controles, deixando a área principal livre para exibir os dados. Para adicionar elementos a ela, usamos a sintaxe `with st.sidebar:`, e tudo que estiver _indentado_ (recuado) abaixo dele aparecerá na lateral.
```python
with st.sidebar:
	clicou = st.button("Clique aqui!")
	if clicou:
		st.write("Você **CLICOU**")
```

### 4.3. Colunas
As colunas são fundamentais para organizar elementos lado a lado, ao invés de empilhá-los verticalmente. Elas serão **essenciais** para a nossa vitrine.

Nós podemos criar as colunas usando o comando `st.columns(n)`. Esse comando recebe _quantas_ colunas queremos criar e retorna uma lista de objetos de coluna.
```python
cols = st.columns(2) # Cria duas colunas de tamanho igual

# Você pode usar o "with" para adicionar conteúdo a cada coluna
with cols[0]:
    st.write("Coluna 1")
with cols[1]:
    st.write("Coluna 2")
```

**Salve e veja o resultado.** Brinque mudando o número (ex: `st.columns(3)`).

## 5. Projeto Pokédex: A Vitrine (Exercícios)

**Nosso objetivo:** Criar a vitrine de Pokémon com filtros interativos para selecionar os Pokémon.

**Lembrete:** Estamos usando o arquivo `pokemon.csv`. Ele agora possui uma coluna `Image` que contém a URL da foto de cada Pokémon.

### 5.1. Carregue os Dados

Faça o carregamento dos dados (`pokemon.csv`) em um DataFrame do Pandas e imprima a tabela na tela com `st.dataframe(df)`.

### 5.2. Faça as Configurações Iniciais

Use `st.set_page_config` para dar um título e um ícone à sua página. Adicione um título principal com `st.title()` e um texto de descrição na `st.sidebar`.

### 5.3. Pokédex (Grid)

Use `st.columns(3)` para exibir os Pokémon em um grid de 3 colunas. Dentro de cada coluna, mostre o nome (`st.subheader`) e o tipo (`st.write`) de um Pokémon. (Por enquanto, pode fazer na mão os 6 primeiros).

### 5.4. Filtro por Tipo

Na `sidebar`, adicione um `st.selectbox` para que o usuário possa filtrar os Pokémon por tipo (Use a coluna `Type 1`). A tabela principal deve ser atualizada para mostrar apenas os Pokémon do tipo selecionado.

### 5.5. Resumo

Acima da tabela de Pokémon filtrados, adicione um resumo sobre eles:

1. Qual o tipo (`Type 1`) mais comum entre os filtrados?
    
2. Qual a média de `Attack` dos Pokémon filtrados?
    
3. Quantos Pokémon existem no total (filtrados)?
    

### 5.6. Faça a Vitrine Responsiva

Na `sidebar`, adicione um `st.slider` que permita ao usuário escolher o número de colunas (de 1 a 5). Use esse valor para criar o grid da "Vitrine" (substituindo o `st.columns(3)`).

### 5.7. Filtro por Nome

Na `sidebar`, adicione um `st.text_input` para o usuário digitar um nome. Filtre o DataFrame para que ele mostre apenas os Pokémon cujos nomes contenham o texto digitado (ex: digitar "Pika" deve encontrar "Pikachu").