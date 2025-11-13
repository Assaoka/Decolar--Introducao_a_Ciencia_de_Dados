<!-- #region id="view-in-github" colab_type="text" -->
<a href="https://colab.research.google.com/github/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/blob/main/%5B%20%201%20%5D%20L%C3%B3gica%20de%20Programa%C3%A7%C3%A3o/C%C3%B3digo.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<!-- #endregion -->

<!-- #region id="ZkLWA_8YmLbr" -->
# 🚀 Aula 1: Lógica de Programação com Python
<!-- #endregion -->

<!-- #region id="6LZ_ePSJmP3f" -->
Olá! Bem-vindos à nossa primeira aula de programação. Hoje, vamos aprender os blocos de construção essenciais de qualquer programa de computador: **variáveis**, como **ler dados** do usuário e como **mostrar informações** na tela.

Vamos usar Python, uma linguagem de programação conhecida por ser clara e fácil de aprender!
<!-- #endregion -->

<!-- #region id="rHwWrBQKmVKH" -->
## 📝 1. Escrevendo na Tela (Saída de Dados)
<!-- #endregion -->

<!-- #region id="eVwRo27fmX5m" -->
O primeiro passo em programação é geralmente fazer o computador "falar". Em Python, usamos o comando `print()` para isso. Tudo o que você colocar entre os parênteses e aspas será exibido na tela.

**Exemplo:**
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="YYiZm2VPmXc8" outputId="951af673-40ac-4748-f810-f2f652118ebb"
print("Olá, turma!")
print("Vamos começar a programar em Python!")
```

<!-- #region id="1wZSWAaYmoej" -->
Use a célula de código abaixo para se apresentar. Escreva seu nome e um hobby que você gosta.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="dh_FbmU7mraB" outputId="85dfe77d-d51b-4f80-a04f-2dcd30ee52ec"
# Escreva seu código aqui. Use o comando print()
print("Meu nome é [Seu Nome] e eu gosto de [Seu Hobby]!")
```

<!-- #region id="4s-5sJC3m1C6" -->
## 📦 2. Variáveis: As Caixinhas da Memória
<!-- #endregion -->

<!-- #region id="FVlR-cKBm5nX" -->
Imagine que você precisa guardar uma informação para usar depois, como a idade de alguém ou o nome de um personagem de jogo. Para isso, usamos **variáveis**.

Uma variável é como uma caixinha com uma etiqueta (o nome da variável) onde guardamos um valor.

Em Python, criar uma variável é muito simples. Você só precisa dar um nome e usar o sinal de igual (`=`) para guardar algo nela.

**Tipos de Variáveis Comuns:**
* **Texto (`string` ou `str`):** Qualquer texto, sempre entre aspas.
* **Números Inteiros (`int`):** Números sem parte decimal (ex: 10, -5, 1500).
* **Números Decimais (`float`):** Números com ponto decimal (ex: 1.99, 3.14, -25.5).

**Regras para Nomes de Variáveis:**
1.  Deve começar com uma letra ou `_`.
2.  Não pode conter espaços ou caracteres especiais (como `!`, `@`, `#`, `?`).
3.  Pode conter números, mas não no início.
4.  Python diferencia maiúsculas de minúsculas (`nome` é diferente de `Nome`).

**Exemplo:**
<!-- #endregion -->

```python id="MopPCNFinHI-"
nome_personagem = "Pikachu"  # Uma variável do tipo string
nivel = 10                  # Uma variável do tipo int
altura = 0.4                # Uma variável do tipo float
```

```python colab={"base_uri": "https://localhost:8080/"} id="A7mihSmMnPUG" outputId="4de1d781-ef70-4d25-e04f-7a00554bbf86"
# Vamos mostrar o que guardamos usando print()
print("O nome do personagem é:", nome_personagem)
print("Ele está no nível:", nivel)
print("Sua altura é:", altura, "metros")
```

```python colab={"base_uri": "https://localhost:8080/"} id="uxu1yMmTnleF" outputId="5a2fa837-b105-4d28-b38a-75324cf633f5"
# Outra forma de formatar a saída usando f-strings (maneira mais moderna e legível)
print(f"O nome do personagem é: {nome_personagem}")
print(f"Ele está no nível: {nivel}")
print(f"Sua altura é: {altura} metros")
```

```python colab={"base_uri": "https://localhost:8080/"} id="d28f41f5" outputId="c25af769-ecac-492e-b545-6e7d1057f184"
# Usando string multilinha com um único print
print(f"""O nome do personagem é: {nome_personagem}
Ele está no nível: {nivel}
Sua altura é: {altura} metros""")
```

<!-- #region id="L3ib9dnbobwl" -->
## ⌨️ 3. Lendo Dados do Teclado (Entrada de Dados)
<!-- #endregion -->

<!-- #region id="tmvfWw7poehJ" -->
Agora, vamos deixar nossos programas interativos! Podemos pedir para o usuário digitar informações usando a função `input()`.

A função `input()` mostra uma mensagem para o usuário e espera que ele digite algo e pressione Enter.

**Atenção:** O `input()` sempre guarda a informação como **texto (`string`)**. Se precisarmos que seja um número, temos que converter!

* `int()`: converte um texto para número inteiro.
* `float()`: converte um texto para número decimal.

**Exemplo:**
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="b-98r7zwohWb" outputId="755239e5-7020-40be-ce2f-1454e224f920"
# Pergunta o nome do usuário e guarda na variável 'nome'
nome_usuario = input("Qual é o seu nome? ")

# Pergunta a idade, recebe como texto e já converte para inteiro
idade_usuario = int(input("Qual é a sua idade? "))

print(f"Olá, {nome_usuario}!")
print(f"Você tem {idade_usuario} anos.")
```

<!-- #region id="gvh9GKAEpZyl" -->
## ⚙️ 4. Operadores: A Matemática do Computador
<!-- #endregion -->

<!-- #region id="y1z-lp1opeUu" -->
Assim como na matemática, podemos fazer contas em Python.

**Operadores Aritméticos**

| Operador | Descrição | Exemplo | Resultado |
| :---: | :--- | :---: | :---: |
| `+` | Adição | `5 + 3` | `8` |
| `-` | Subtração | `5 - 3` | `2` |
| `*` | Multiplicação | `5 * 3` | `15` |
| `/` | Divisão | `10 / 2` | `5.0` |
| `//` | Divisão Inteira | `11 // 2` | `5` |
| `%` | Resto da Divisão (Módulo) | `11 % 2` | `1` |
| `**` | Potência (Exponenciação) | `2 ** 3` | `8` |

**Exemplo**
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="c7GjyVoMp6Yr" outputId="f9757e56-b465-421e-f3ce-effcc0e5c0ca"
# Exemplo com operadores
numero1 = 15
numero2 = 4

soma = numero1 + numero2
divisao = numero1 / numero2
divisao_inteira = numero1 // numero2
resto = numero1 % numero2

print(f"{numero1} + {numero2} = {soma}")
print(f"{numero1} / {numero2} = {divisao}")
print(f"Divisão inteira de {numero1} por {numero2} é: {divisao_inteira}")
print(f"O resto da divisão de {numero1} por {numero2} é: {resto}")
```

<!-- #region id="RsknBniOqZqs" -->
## 💪 Hora dos Exercícios!
<!-- #endregion -->

<!-- #region id="X5RltAJYqm9R" -->
### Exercício 1: Trocando Valores
<!-- #endregion -->

<!-- #region id="GjcM1uvkqoj1" -->
Leia dois valores para as variáveis A e B. Depois, troque os valores de forma que A passe a ter o valor de B, e B passe a ter o valor de A. No final, mostre os valores trocados.

<!-- #endregion -->

```python id="Mr2a7tgmqo3m"

```

<!-- #region id="f7JfILtyqxU2" -->
### Exercício 2: Conversor de Dólar para Real
<!-- #endregion -->

<!-- #region id="ec-nXoLrq0RM" -->
Faça um programa que pergunta a cotação do dólar hoje e a quantidade de dólares que uma pessoa tem. Em seguida, calcule e mostre o valor correspondente em reais.
<!-- #endregion -->

```python id="yspMNgb8qzy0"

```

<!-- #region id="qGD9B3XWq4Cu" -->
### Exercício 3: Quadrado, Cubo e Raiz Quadrada
<!-- #endregion -->

<!-- #region id="0vQJLpzBq9-3" -->
Leia um valor inteiro e apresente os resultados do quadrado, do cubo e da raiz quadrada do valor lido.
<!-- #endregion -->

```python id="2n4CAHHFq88K"

```

<!-- #region id="6Np4Z_cErFbU" -->
## 🏆 Desafios (Baseados no BeeCrowd)
<!-- #endregion -->

<!-- #region id="8p0Y7VPtrHWP" -->
### Desafio 1: Média 2 (BeeCrowd 1006)
<!-- #endregion -->

<!-- #region id="6y4_LtrtrKjt" -->
Leia 3 valores (A, B e C), que são as notas de um aluno. Calcule a média do aluno, sabendo que a nota A tem peso 2, a nota B tem peso 3 e a nota C tem peso 5.
<!-- #endregion -->

```python id="fSyLFnsqrPDw"

```

<!-- #region id="WEP2YrNRrSE7" -->
### Desafio 2: Idade em Dias (BeeCrowd 1020)
<!-- #endregion -->

<!-- #region id="TLd-wEtcrULf" -->
Leia um valor inteiro, que é a idade de uma pessoa em dias, e informe-a em anos, meses e dias.

Obs: considere todo ano com 365 dias e todo mês com 30 dias.

<!-- #endregion -->

```python id="nRCmH-ihrTvZ"

```

<!-- #region id="7OO3zsUDra0C" -->
### Desafio 3: Cédulas (BeeCrowd 1018)
<!-- #endregion -->

<!-- #region id="u90UZ9cBrcvv" -->
Leia um valor inteiro. A seguir, calcule o menor número de notas possíveis (cédulas) no qual o valor pode ser decomposto. As notas consideradas são de 100, 50, 20, 10, 5, 2 e 1.
<!-- #endregion -->

```python id="6pa1RtkerdY5"

```
