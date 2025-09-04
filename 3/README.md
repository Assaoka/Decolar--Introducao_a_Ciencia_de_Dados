# 📦 Guardando Múltiplos Dados: Listas e Dicionários
Até agora, nossas variáveis eram como caixinhas que guardavam uma única informação. Mas e se quiséssemos guardar uma lista de compras, as notas de todos os alunos da turma ou os contatos da sua agenda? Para isso, usamos as **estruturas de dados**. As duas mais comuns em Python são as listas e os dicionários.

## Listas `[valor1, valor2]`: Uma Coleção Organizada por Posição
Pense em uma lista como uma estante com várias prateleiras numeradas. Você pode guardar um item em cada prateleira e, para pegar um item de volta, basta saber o número da sua prateleira.
- **Posição (Índice):** A numeração das "prateleiras" em programação começa sempre do **zero**! Isso é super importante. 
- **⚠️ Ponto de Atenção:** O primeiro item está na posição 0, o segundo na posição 1, e assim por diante.
Veja como criar e usar uma lista de convidados para uma festa:

```python
# Uma lista de strings (textos)
convidados = ["Beatriz", "Carlos", "Diana", "Adriano"]

# Para acessar um item, usamos seu índice entre colchetes
primeiro_convidado = convidados[0] # Pega o item na posição 0
terceiro_convidado = convidados[2] # Pega o item na posição 2

print(f"O primeiro da lista é: {primeiro_convidado}") # Saída: Beatriz
print(f"O terceiro da lista é: {terceiro_convidado}") # Saída: Diana
```

Você também pode usar índices negativos para acessar elementos de trás para frente:
```python
ultimo_convidado = convidados[-1]
penultimo_convidado = convidados[2]

print(f"O ultimo...")
print(f"O penultimo...")
```

Uma lista é mutável, você pode alterar os elementos que participam dela:
```python
convidados[0] = "Ana Beatriz"
print(f"Lista atualizada: {convidados}")
```

E se alguém confirmar de última hora? Usamos o .append() para adicionar no final!
```python
convidados.append("Fernanda")
print(f"Lista atualizada: {convidados}")
```

Um comando muito útil para esse tipo de estrutura é o `len()`, ele retorna quantos elementos existe nessas estruturas:
```python
print(f"Existem {len(convidados)} convidados na lista")
```
## Dicionários `{chave: valor}`: Uma Coleção Organizada por Rótulos

Agora, imagine uma agenda de contatos. Você não procura um amigo pelo "número da página", mas sim pelo **nome** dele. Dicionários funcionam assim: em vez de uma posição numérica, cada valor é guardado com um **rótulo** único, que chamamos de **chave**.
- **Chave-Valor:** Todo item em um dicionário é um par `chave: valor`. A chave é o rótulo que usamos para encontrar a informação.
Vamos criar um dicionário para guardar as informações de um aluno:

```python
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

Podemos adicionar novas informações facilmente
```python
aluno["turma"] = "8A"
print(f"O aluno agora tem a informação da turma: {aluno}")
```

#### Mão na Massa:
Observe que essas duas estruturas tem algo interessante, ao combina-las elas funcionam como tabelas... Podemos acessar o nome do indivíduo 3 por exemplo. Seu objetivo é criar um objeto que funcione como a tabela abaixo:

| Nome    | Idade | Turma |
| ------- | ----- | ----- |
| Beatriz | 12    | A     |
| Carlos  | 13    | A     |
| Diana   | 13    | B     |
```python
alunos = [
	{"Nome": "Beatriz", "Idade": 12, "Turma": "A"}
	{"Nome": "Carlos", "Idade": 13, "Turma": "A"}
	{"Nome": "Diana", "Idade": 13, "Turma": "B"}
]
```

Agora imprima o Nome, Idade e Turma do segundo aluno.
```python
print(f"Nome: {alunos[1]['Nome']}")
print(f"Idade: {alunos[1]['Idade']}")
print(f"Turma: {alunos[1]['Turma']}")
```

## Outras Estruturas:
Além das listas e dicionários, o python possui outras estruturas compostas interessantes que merecem ser citadas:
- Set (Conjunto) `{valor1, valor2}`: Essa estrutura contém um conjunto não ordenado e que não permite repetição de valores. Pode ser útil na ciência de dados quando...
- Tupla `(valor1, valor2)`: Essas estruturas são muito similares as listas, porém são imutáveis. Após definir seu conteúdo, ele só pode ser acessado.
Fica como tarefa opcional pesquisar sobre essas estruturas.
# 🔁 Automação de Tarefas: Estruturas de Repetição
Imagine que você precisa dar "bom dia" para todos os 5 convidados da sua lista. Escrever `print()` 5 vezes funciona, mas e se fossem 100 convidados? Seria um pesadelo!

Os **laços (ou loops)** servem para repetir um bloco de código uma certa quantidade de vezes pré-definida, de forma automática.
## O Laço `for`: Repetindo para Cada Item de uma Sequência
O uso mais simples do for, é percorrer uma sequência de números. Para isso usamos a função `range()`! `range(5)` cria uma sequência de números de 0 a 4 (0, 1, 2, 3, 4).

```python
# Este loop vai repetir 5 vezes
for numero in range(5):
    print(f"Esta é a repetição número {numero + 1}")
```

Conveniente não, é exatamente onde começamos o índice das listas. Podemos imprimir a lista de convidados da seguinte forma então:
```python
n = len(convidados)
for i in range(n):
	print(f"Convidado {i}: {convidados[i]}")
```

Quando queremos fazer uma tarefa que exige acesso apenas aos elementos de um iteravel (como a lista) e não precisamos saber a posição dele, podemos usar o for para percorrer de forma nativa. A lógica dele é: "**Para cada** item **dentro de** uma coleção, faça alguma coisa".

```python
# A variável "nome" receberá um convidado da lista a cada repetição
for nome in convidados:
    print(f"Olá, {nome}! Seja bem-vindo(a) à festa!")
    # O código indentado aqui dentro se repete para cada nome da lista
```

#### Mão na Massa:
Percorra nossa lista de alunos imprimindo suas informações:
```python
# ...
```

## O Laço `while`: Repetindo Enquanto uma Condição for Verdadeira

O `while` é como um porteiro teimoso. Ele só deixa o código continuar a ser executado **enquanto** uma condição for verdadeira. Para isso, nosso conhecimento de condicionais da aula anterior é essencial.

Pense nele como um videogame: _enquanto_ a vida do chefe for maior que zero, continue atacando.

```python
import random # Biblioteca para gerar números aleatórios

numero_secreto = random.randint(1, 10) # Sorteia um número de 1 a 10
chute = 0 # Inicializamos o chute com um valor que não seja o secreto

print("--- Jogo da Adivinhação ---")

while chute != numero_secreto:
    chute = int(input("Adivinhe o número (entre 1 e 10): "))
    
    if chute < numero_secreto:
        print("Muito baixo! Tente um número maior.")
    elif chute > numero_secreto:
        print("Muito alto! Tente um número menor.")

print(f"Parabéns! Você acertou! O número era {numero_secreto}.")
```

**⚠️ CUIDADO COM O LOOP INFINITO!** Se a condição do `while` nunca se tornar falsa, o programa ficará preso para sempre. Sempre garanta que algo dentro do loop mude para que ele possa terminar.

#### Mão na Massa:
Observe que nossa lista de alunos está ordenada em relação a turma. Faça uma função que percorra nossa lista imprimindo as informações dos alunos da turma A sem percorrer todos os dados:
```python
# ...
```

# 🧩 Empacotando Código: Funções
Até agora viemos usando algumas palavras frequentemente: `print()`, `input()`, `len()`... O nome dessas coisas são funções, blocos de código que podem ser chamados sobre variáveis.

Conforme nossos códigos crescem, começamos a repetir certas lógicas. Por exemplo, calcular uma média, verificar se um número é par, ou exibir um menu. As **funções** são como "caixas de ferramentas" onde guardamos um bloco de código para reutilizá-lo sempre que quisermos, apenas chamando seu nome.

Pense numa função como uma receita de bolo. A receita tem um nome ("Bolo de Chocolate"), precisa de ingredientes (**parâmetros**) e, no final, te dá um resultado (**retorno**).
