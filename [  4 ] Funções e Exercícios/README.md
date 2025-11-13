<!-- #region id="view-in-github" colab_type="text" -->
<a href="https://colab.research.google.com/github/Assaoka/Decolar--Introducao_a_Ciencia_de_Dados/blob/main/%5B%204%20%5D%20Fun%C3%A7%C3%B5es%20e%20Exerc%C3%ADcios/Fun%C3%A7%C3%B5es%20e%20Exerc%C3%ADcios.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<!-- #endregion -->

<!-- #region id="fPecsDep8XNv" -->
# Aula 4: Funções e Desafios de Lógica

**Objetivo da aula:** Hoje vamos dar um passo muito importante na programação: aprender a criar **funções** para organizar nosso código. Depois, vamos resolver uma série de desafios que irão revisar e conectar tudo o que aprendemos nas Aulas 1, 2 e 3, aplicando a lógica de programação para resolver problemas práticos.

### Parte 1: Funções - Organizando seu Código (15 min)

Até agora, escrevemos nossos códigos de forma sequencial. Mas e se quiséssemos calcular a média de notas em várias partes diferentes do nosso programa? Teríamos que repetir o mesmo código várias vezes. Isso não é prático!

**Funções** são como "receitas" ou "caixinhas de ferramentas" que guardam um bloco de código que pode ser reutilizado quantas vezes quisermos.

**Vantagens de usar funções:**

- **Organização:** Deixa o código mais limpo e fácil de ler.
    
- **Reutilização:** Evita repetir o mesmo código várias vezes.
    
- **Manutenção:** Se precisar corrigir um erro, você corrige em um só lugar: dentro da função.
    

#### Como criar uma função em Python?

Usamos a palavra-chave `def` (de "definir"), damos um nome para a função e colocamos parênteses `()`. O código que pertence à função precisa estar indentado (com um "tab" ou 4 espaços).

<!-- #endregion -->

```python id="b5875191"
def dar_boas_vindas():
  print("Olá! Seja bem-vindo(a) ao nosso programa!")
  print("-----------------------------------------")
```

<!-- #region id="1VgYY5PE8_v5" -->
Para usar a função, nós a "chamamos" pelo nome:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="h-dcqwsT8_R5" outputId="a4093a23-de69-4036-e7ec-4d1779ca8c86"
dar_boas_vindas()
dar_boas_vindas()
dar_boas_vindas()
```

<!-- #region id="Pq5j8GH-8sLH" -->
#### Funções com Parâmetros (Entradas) e Retorno (Saídas)

As funções ficam ainda mais poderosas quando podem receber dados para trabalhar e nos devolver um resultado.

- **Parâmetros:** São as informações que a função recebe para trabalhar. Eles são declarados dentro dos parênteses.
    
- **Retorno:** É o resultado que a função nos devolve. Usamos a palavra-chave `return`.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="_qZN0otI8vp0" outputId="0bb3c33f-3aa3-40d3-f8b1-131e425dab28"
def somar(a, b):
    """Soma dois números e retorna o resultado.

    Args:
        a: O primeiro número.
        b: O segundo número.

    Returns:
        A soma de 'a' e 'b'.
    """

    resultado = a + b
    return resultado

print(f"O resultado de 7 + 3 é: {somar(7, 3)}")
```

<!-- #region id="eV766pQB-9WY" -->
### Parte 2: Exercícios de Fixação

Agora, vamos praticar! Resolva os exercícios abaixo, aplicando os conceitos das aulas anteriores. Tente usar funções onde achar que faz sentido!

#### Exercícios - Revisão Aula 1 (Variáveis e Operadores)

**Exercício 1: Calculadora de Juros Compostos**

Juros compostos são "juros sobre juros" e fazem o dinheiro crescer exponencialmente. A fórmula é:

M=C∗(1+i)t

Onde:

- `M` = Montante final
    
- `C` = Capital inicial (o valor que você investiu)
    
- `i` = Taxa de juros (em decimal, ex: 5% = 0.05)
    
- `t` = Tempo (em meses ou anos, dependendo da taxa)
    

Crie um programa que:

1. Pergunte ao usuário o capital inicial, a taxa de juros (em %) e o tempo do investimento.
    
2. Calcule e mostre o montante final. Preste atenção na ordem das operações e no uso de parênteses!
<!-- #endregion -->

```python id="AGzQfh7t_EOt"

```

<!-- #region id="Vt1qxz0X_En-" -->
**Exercício 2: Conversor de Segundos**

Crie um programa que:

1. Receba um número inteiro que representa uma quantidade total de segundos.
    
2. Converta esse valor para o formato `horas:minutos:segundos`.
    
3. Exiba o resultado na tela. (Ex: 3672 segundos se tornam `1:1:12`)
    

**Dica:** Use o operador de divisão inteira (`//`) e o de resto da divisão (`%`).
<!-- #endregion -->

```python id="oV-6_kki_VuA"

```

<!-- #region id="ZY1oQmT6_WAM" -->
#### Exercícios - Revisão Aula 2 (Condicionais)

**Exercício 3: Tipos de Triângulo**

Crie um programa que:

1. Leia 3 valores de ponto flutuante (`a`, `b`, `c`).
    
2. Ordene os valores em ordem decrescente, de modo que `a` seja sempre o maior lado.
    
3. Com base nos valores ordenados, determine e imprima o tipo de triângulo que eles formam, seguindo as regras:
    
    - Se `a ≥ b + c`, imprima `NAO FORMA TRIANGULO`.
        
    - Se `a² = b² + c²`, imprima `TRIANGULO RETANGULO`.
        
    - Se `a² > b² + c²`, imprima `TRIANGULO OBTUSANGULO`.
        
    - Se `a² < b² + c²`, imprima `TRIANGULO ACUTANGULO`.
        
    - Se os três lados forem iguais, imprima `TRIANGULO EQUILATERO`.
        
    - Se apenas dois lados forem iguais, imprima `TRIANGULO ISOSCELES`.
<!-- #endregion -->

```python id="PRUZP74w_eom"

```

<!-- #region id="hAFhrvpT_fGt" -->
**Exercício 4: Calculadora de IMC (Índice de Massa Corporal)**

O IMC é um indicador de saúde usado para saber se o peso está de acordo com a altura. A fórmula é:

$$IMC=altura^2  peso​$$

Crie um programa que:

1. Peça o peso (em kg) e a altura (em metros) da pessoa.
    
2. Calcule o IMC.
    
3. Mostre a classificação correspondente, de acordo com a tabela:
    
    - Abaixo de 18.5: Abaixo do peso
        
    - Entre 18.5 e 24.9: Peso ideal
        
    - Entre 25.0 e 29.9: Sobrepeso
        
    - Entre 30.0 e 39.9: Obesidade
        
    - Acima de 40.0: Obesidade grave

<!-- #endregion -->

```python id="5Fa-x0OY_vp4"

```

<!-- #region id="1ZGdUJGi_4Fp" -->
#### Exercícios - Revisão Aula 3 (Loops e Estruturas de Dados)

**Exercício 5: Análise de Temperaturas**

Você recebeu uma lista com as temperaturas médias de cada dia da semana.

1. Calcule a **menor** e a **maior** temperatura da semana.
    
2. Calcule a **temperatura média** da semana.
    
3. Conte e mostre **quantos dias** a temperatura ficou acima da média.
<!-- #endregion -->

```python id="dVxDLIZx_8nm"

```

<!-- #region id="ixsVJFZl_82_" -->
**Exercício 6: Boletim da Turma**

Você recebeu os dados da turma em formato de uma **lista de dicionários**.

1. Percorra essa lista com um laço `for`.
    
2. Para cada aluno, calcule a **média final** (média simples das 3 notas).
    
3. Imprima o nome do aluno, sua média e se ele foi "Aprovado" (média >= 7.0) ou "Reprovado".
    


<!-- #endregion -->

```python id="YPGzSTct_-7K"
# Dados
turma = [
    {"nome": "Ana", "notas": [8.0, 9.0, 9.5]},
    {"nome": "Bruno", "notas": [5.0, 6.5, 4.0]},
    {"nome": "Carla", "notas": [7.0, 7.5, 8.0]},
    {"nome": "Daniel", "notas": [10.0, 9.5, 9.8]},
]
```

<!-- #region id="z77bBropAdiF" -->
**Exercício 7: Jogo de Adivinhação**

Crie um jogo simples:

1. Defina um número secreto (ex: `numero_secreto = 42`).
    
2. Use um laço `while` para pedir ao jogador que adivinhe o número.
    
3. A cada palpite, informe se o número é "Muito alto!" ou "Muito baixo!".
    
4. Quando o jogador acertar, dê os parabéns e encerre o jogo.
    
5. **Bônus:** Conte e mostre quantas tentativas o jogador levou.
<!-- #endregion -->

```python id="ZvSdyx0OAeU_"

```

<!-- #region id="7WYDs0dxAiDH" -->
**Exercício 8: Análise de Dados de Vendas**

Dada uma lista de dicionários com dados de vendas, calcule:

1. O **valor total** vendido (soma de `quantidade * preco` de todos os produtos).
    
2. O nome do produto **mais vendido** (em quantidade).
    
3. Uma nova lista contendo apenas as vendas com valor total ( `quantidade * preco` ) **acima de R$ 500,00**.
    
<!-- #endregion -->

```python id="hQ2y-h2hAi04"
# Dados de Vendas
vendas = [
    {"produto": "Notebook Gamer", "quantidade": 8, "preco": 5500.00},
    {"produto": "Mouse sem fio", "quantidade": 50, "preco": 120.50},
    {"produto": "Teclado Mecânico", "quantidade": 25, "preco": 350.00},
    {"produto": "Monitor 4K", "quantidade": 12, "preco": 2200.00},
    {"produto": "Cadeira Gamer", "quantidade": 15, "preco": 1300.00},
    {"produto": "Headset 7.1", "quantidade": 30, "preco": 450.00},
]
```

<!-- #region id="r6F62PyK8SpB" -->


    






    





### Parte 4: Trabalho 1 - Gerenciador de Livraria (Simplificado)

**Objetivo:** Criar um programa de menu para gerenciar o estoque de uma livraria. Este trabalho combina laços, listas, dicionários e condicionais.

**Requisitos:**

1. Crie uma lista vazia chamada `estoque` para armazenar os livros. Cada livro será um dicionário.
    
2. Crie um laço `while True` que exiba um menu de opções para o usuário e só pare quando ele escolher "Sair".
    
3. Implemente as seguintes opções no menu:
    
    - **1. Adicionar Livro:**
        
        - Peça ao usuário o `título`, `autor`, `preço` e `quantidade` em estoque.
            
        - Crie um dicionário com essas informações.
            
        - Adicione o dicionário à lista `estoque`.
            
    - **2. Listar Livros:**
        
        - Se o estoque estiver vazio, mostre a mensagem "Estoque vazio.".
            
        - Caso contrário, percorra a lista `estoque` e imprima os dados de cada livro de forma organizada.
            
    - **3. Vender Livro:**
        
        - Peça o `título` do livro a ser vendido.
            
        - Procure na lista `estoque` pelo livro com esse título.
            
        - Se encontrar e a quantidade for maior que 0:
            
            - Diminua a quantidade em 1.
                
            - Mostre a mensagem "Venda realizada com sucesso!".
                
        - Se encontrar, mas a quantidade for 0, mostre "Livro fora de estoque.".
            
        - Se não encontrar o livro, mostre "Livro não encontrado.".
            
    - **4. Sair:**
        
        - Encerre o programa.
            

> **Dica:** Para procurar o livro na lista, você precisará de um laço `for` dentro da opção 3 e um `if` para comparar os títulos. Pode ser útil usar uma variável "flag" para saber se o livro foi encontrado ou não.
<!-- #endregion -->
