<!-- #region id="view-in-github" colab_type="text" -->
<a href="https://colab.research.google.com/github/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/blob/main/%5B%20%203%20%5D%20Vari%C3%A1veis%20Compostas%20e%20Loops/Vari%C3%A1veis_Compostas_e_Loops.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<!-- #endregion -->

<!-- #region id="cKEH-ImLwD6J" -->
# 📦 Guardando Múltiplos Dados: Listas e Dicionários
<!-- #endregion -->

<!-- #region id="-4kGGmMSwCco" -->

Até agora, nossas variáveis eram como caixinhas que guardavam uma única informação. Mas e se quiséssemos guardar uma lista de compras, as notas de todos os alunos da turma ou os contatos da sua agenda? Para isso, usamos as **estruturas de dados**. As duas mais comuns em Python são as listas e os dicionários.
<!-- #endregion -->

<!-- #region id="kvfBScYuwGaF" -->
## Listas `[valor1, valor2]`: Uma Coleção Organizada por Posição
<!-- #endregion -->

<!-- #region id="-KXibOwkwJr7" -->

Pense em uma lista como uma estante com várias prateleiras numeradas. Você pode guardar um item em cada prateleira e, para pegar um item de volta, basta saber o número da sua prateleira.
- **Posição (Índice):** A numeração das "prateleiras" em programação começa sempre do **zero**! Isso é super importante.
- **⚠️ Ponto de Atenção:** O primeiro item está na posição 0, o segundo na posição 1, e assim por diante.
Veja como criar e usar uma lista de convidados para uma festa:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="Pchr3Uh8wMLa" outputId="f27647d2-18bc-4827-fcfb-1fd0c64f19ea"
# Uma lista de strings (textos)
convidados = ["Beatriz", "Carlos", "Diana", "Adriano"]

# Para acessar um item, usamos seu índice entre colchetes
primeiro_convidado = convidados[0] # Pega o item na posição 0
terceiro_convidado = convidados[2] # Pega o item na posição 2

print(f"O primeiro da lista é: {primeiro_convidado}") # Saída: Beatriz
print(f"O terceiro da lista é: {terceiro_convidado}") # Saída: Diana
```

<!-- #region id="h4HPZvOwwcai" -->

Você também pode usar índices negativos para acessar elementos de trás para frente:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="km5EIBziwkBD" outputId="d575d102-1353-474b-e0ac-dc95d3b40928"
ultimo_convidado = convidados[-1] # -1 é sempre o último
penultimo_convidado = convidados[-2] # -2 é o penúltimo

print(f"O último convidado da lista é: {ultimo_convidado}")
print(f"O penúltimo convidado da lista é: {penultimo_convidado}")
```

<!-- #region id="TvbBNgvSwoMl" -->
Uma lista é mutável, ou seja, você pode alterar os elementos que participam dela a qualquer momento.

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="TK-cLJzywpu-" outputId="1cda3a2d-8982-40d7-8c9c-4a4b51e1ac36"
# O Adriano não pode vir, vamos trocá-lo pelo Bruno
print(f"Lista original: {convidados}")
convidados[3] = "Bruno" # Atribui um novo valor para a posição 3
print(f"Lista atualizada: {convidados}")
```

<!-- #region id="gYDDI-_0wu8i" -->
E se alguém confirmar de última hora? Usamos o .append() para adicionar no final da lista!
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="VoJoHxqjwwFy" outputId="02cb95b3-cd4c-45e3-e8dd-fa376c92dafe"
convidados.append("Fernanda")
print(f"A Fernanda confirmou presença! Nova lista: {convidados}")
```

<!-- #region id="JRoLGxhnw466" -->
Um comando muito útil para esse tipo de estrutura é o `len()`, ele retorna quantos elementos existe nessas estruturas:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="c_L-DBBWw3fW" outputId="48261eec-8e51-43ff-9ae1-b54749ef401c"
print(f"Existem {len(convidados)} convidados na lista")
```

<!-- #region id="Wh9hJhcJxG23" -->
## Dicionários `{chave: valor}`: Uma Coleção Organizada por Rótulos

Agora, imagine uma agenda de contatos. Você não procura um amigo pelo "número da página", mas sim pelo **nome** dele. Dicionários funcionam assim: em vez de uma posição numérica, cada valor é guardado com um **rótulo** único, que chamamos de **chave**.
- **Chave-Valor:** Todo item em um dicionário é um par `chave: valor`. A chave é o rótulo que usamos para encontrar a informação.
Vamos criar um dicionário para guardar as informações de um aluno:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="qnBdVzOPxMWb" outputId="23a6187f-f3cf-4af2-d2c2-fa0f12f40fe2"
# As chaves são "nome", "idade" e "nota". Os valores são o que vem depois dos dois pontos.
aluno = {
    "nome": "Carlos",
    "idade": 13,
    "nota_final": 9.5,
    "passou_de_ano": True
}

# Para acessar um valor, usamos a sua chave entre colchetes
print(f"O nome do aluno é {aluno['nome']}") # Saída: Carlos
print(f"Sua nota foi {aluno['nota_final']}") # Saída: 9.5
```

<!-- #region id="h9nQpl6-xQgx" -->
Podemos adicionar novas informações facilmente
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="_E--SfDpxTYE" outputId="e918639a-f09b-48d0-d608-42f4c0a9eaad"
aluno["turma"] = "8A"
print(f"O aluno agora tem a informação da turma: {aluno}")
```

<!-- #region id="jipSTKuPx0Ua" -->
## O Poder da Combinação: Listas de Dicionários!
<!-- #endregion -->

<!-- #region id="_dG2KOqgx60R" -->
Aqui é onde a Ciência de Dados começa a brilhar. E se tivermos vários alunos? Podemos criar uma lista, onde cada item da lista é um dicionário com as informações de um aluno. Isso organiza nossos dados como uma tabela ou uma planilha!

| Nome    | Idade | Turma |
| ------- | ----- | ----- |
| Beatriz | 12    | A     |
| Carlos  | 13    | A     |
| Diana   | 13    | B     |
<!-- #endregion -->

```python id="S4ldHE0Jx7kd"
alunos = [
	{"Nome": "Beatriz", "Idade": 12, "Turma": "A"},
	{"Nome": "Carlos", "Idade": 13, "Turma": "A"},
	{"Nome": "Diana", "Idade": 13, "Turma": "B"}
]
```

```python colab={"base_uri": "https://localhost:8080/"} id="oKw4tIINyUM-" outputId="3ed18d5b-1b93-488f-fc87-866a5ccfe6af"
alunos[0]
```

```python colab={"base_uri": "https://localhost:8080/"} id="64TiA7SfyMlN" outputId="370db2df-984f-47ec-a9c7-413ae4d3579c"
print(f"Nome: {alunos[1]['Nome']}")
print(f"Idade: {alunos[1]['Idade']}")
print(f"Turma: {alunos[1]['Turma']}")
```

<!-- #region id="nz5KsTd_yuaK" -->
# 🔁 Automação de Tarefas: Estruturas de Repetição

Imagine que você precisa dar "bom dia" para todos os 3 alunos da sua lista. Escrever `print()` 3 vezes funciona, mas e se fossem 100 convidados ou a lista mudasse constantemente? Seria um pesadelo!

Os **laços (ou loops)** servem para repetir um bloco de código várias vezes, de forma automática.
<!-- #endregion -->

<!-- #region id="Qbgyc_eby2xl" -->
## O Laço `for`: Repetindo para Cada Item de uma Coleção

O `for` é o nosso laço "para cada". A lógica dele é: "**Para cada** item **dentro de** uma coleção, faça alguma coisa". É perfeito para percorrer listas!

O uso mais simples do for, é percorrer uma sequência de números. Para isso usamos a função `range()`! `range(5)` cria uma sequência de números de 0 a 4 (0, 1, 2, 3, 4).
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="GUVX-mjsyz42" outputId="21c29bdc-0ad8-49d0-9ae0-395a05f797f3"
n = 5
for i in range(n):
    print(i)
```

<!-- #region id="4vHaQQDSzm4p" -->
Conveniente não, é exatamente onde começamos o índice das listas. Podemos imprimir a lista de convidados da seguinte forma então:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="P5OHpHTJzmez" outputId="bacd0f6f-7919-4e93-82f9-588b0af240dc"
n = len(alunos)
for i in range(n):
    print(f'Bom dia, {alunos[i]["Nome"]}!') # Observe que usar 'Nome' dá erro.
```

<!-- #region id="FnhB_z0L0D84" -->
Quando queremos fazer uma tarefa que exige acesso apenas aos elementos de um iteravel (como a lista) e não precisamos saber a posição dele, podemos usar o for para percorrer de forma nativa. A lógica dele é: "**Para cada** item **dentro de** uma coleção, faça alguma coisa".
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="0k1yveNy0H_S" outputId="caaeca83-37ce-40b5-d078-7b6d670b4d89"
for aluno in alunos:
    print(f'Bom dia, {aluno["Nome"]}!')
```

<!-- #region id="io6P950s0n5d" -->
## O Laço `while`: Repetindo Enquanto uma Condição for Verdadeira
<!-- #endregion -->

<!-- #region id="eOdJJEDP0q2K" -->
E se não soubermos exatamente quantas vezes precisamos repetir? E se quisermos que o código repita **enquanto** algo for verdade? Para isso, usamos o `while`.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="_9YwXWuO0nHL" outputId="9f37d0c8-e4e9-4384-d6c3-7c82016f5e05"
n = int(input('Digite um número par: '))
while (n % 2) != 0:
    print('\nVocê não digitou um número par. Tente novamente.')
    n = int(input('Digite um número par: '))
```

<!-- #region id="A1E-eI0Z1Zjy" -->
**⚠️ Ponto de Atenção:** Com o `while`, você precisa garantir que a condição uma hora se torne `False`, senão seu programa entrará em um **loop infinito**!
<!-- #endregion -->

<!-- #region id="-I4L7NSf1nCh" -->
# 💪 Hora dos Exercícios!
<!-- #endregion -->

<!-- #region id="cK2VtEBA2HKY" -->
## Exercício 1: Média da Turma
<!-- #endregion -->

<!-- #region id="o9QhJPH02Inw" -->
Dada uma lista de notas, calcule a média da turma.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="8ZQEUFrI1ZIg" outputId="1ab85c37-2395-4db8-9f9b-cc515c7c461d"
alunos
```

<!-- #region id="k3aGHD5v2VNr" -->
Adicione um novo aluno na lista. Seu código ainda funciona?
<!-- #endregion -->

```python id="Iu_H3bgM2cYU"

```

<!-- #region id="zmtWy2Y92cy9" -->
## Exercício 2: Boletim da Turma
<!-- #endregion -->

<!-- #region id="WqUpZiG62qkm" -->
Dada a lista de alunos abaixo, crie um programa que percorra cada aluno e imprima seu nome e se ele foi "Aprovado" ou "Reprovado". A média para aprovação é 7.0.
<!-- #endregion -->

```python id="hcp3nMGI2vtr"

```

<!-- #region id="RAqeJCPX2zT0" -->
## Exercício 3: Jogo de Adivinhação
<!-- #endregion -->

<!-- #region id="W6s64FhX26tt" -->
Pense em um jogo de adivinhação. Você não sabe quantas tentativas o jogador vai levar. O jogo deve continuar pedindo um palpite **enquanto** o jogador não acertar o número secreto.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="3wv4Xc4R2_Vb" outputId="edf6263d-d6b7-4c62-bb12-8fe7fbeba383"
import random
numero_secreto = random.randint(1, 10) # Gera um número aleatório entre 1 e 10

# -> Seu código:

```
