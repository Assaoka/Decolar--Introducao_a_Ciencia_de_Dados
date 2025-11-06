## 4. Tarefa 2: Prevendo Poder de Ataque (Regressão)

- **Objetivo:** Prever o `Ataque` (y) usando `Defesa` e `HP` (X).
    

Nosso modelo de IA possui 2 conjuntos, X e Y. X representa nosso conjunto de características (features), nossa entrada, nesse caso composta por Defesa e HP. Y representa a resposta final que queremos, ou seja, o ataque do Pokémon. Quando Y é um **número contínuo**, chamamos esse modelo de **Regressão**.

Nosso objetivo é achar a "função" (operações sobre X) que nos leva à previsão com o menor erro possível em Y.

### 4.1. Começando Simples (1 Variável)

Se fôssemos usar só 1 variável (ex: `Defesa`) para prever o `Ataque`, o que faríamos?



```
# Plotar Defesa vs Ataque
plt.figure(figsize=(10, 6))
sns.scatterplot(data=df, x='Defense', y='Attack', alpha=0.5)
plt.title("Ataque vs. Defesa")
plt.xlabel("Defesa")
plt.ylabel("Ataque")
plt.show()
```

Parece que existe uma relação, certo? A **Regressão Linear** tenta encontrar a **linha** que melhor 'corta' esses pontos, minimizando a distância entre a reta e cada ponto.

Essa distância é nosso **erro**. Existem diversas métricas de erro para regressão, sendo as mais famosas:

- **MAE (Mean Absolute Error):** Erro absoluto médio. "Em média, meu modelo erra por X pontos."
    
- **RMSE (Root Mean Squared Error):** Raiz do erro quadrático médio. (É a que vamos usar). Ela penaliza mais os erros grandes.
    

A equação da reta é: $y = ax + b$. O 'Aprendizado' aqui é encontrar o `a` (inclinação) e o `b` (intercepto) ideais.

### 4.2. Treinando o Modelo 1 (1 Variável)

```
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
import numpy as np

# 1. Definir X e y (novos)
# (Idealmente, faríamos o train/test_split aqui também, mas vamos simplificar pela intuição)
X_reg1 = df[['Defense']] # X precisa ser um DataFrame (2 colchetes)
y_reg1 = df['Attack']

# 2. Criar e Treinar
modelo_reg1 = LinearRegression()
modelo_reg1.fit(X_reg1, y_reg1)

# 3. Fazer Previsões
y_pred_reg1 = modelo_reg1.predict(X_reg1)

# 4. Calcular o Erro
rmse = np.sqrt(mean_squared_error(y_reg1, y_pred_reg1))
print(f"RMSE (1 Variável): {rmse:.2f}")

# 5. Plotar a Reta
plt.figure(figsize=(10, 6))
sns.scatterplot(data=df, x='Defense', y='Attack', alpha=0.3, label='Dados Reais')
plt.plot(X_reg1, y_pred_reg1, color='red', linewidth=3, label='Reta de Regressão')
plt.title(f"Regressão Linear (RMSE: {rmse:.2f})")
plt.legend()
plt.show()
```

### 4.3. Modelo 2 (2 Variáveis)

Nosso objetivo final era um pouco diferente: usar 2 variáveis (`Defesa` e `HP`) para encontrar o ataque. Dessa forma, não queremos mais uma reta, e sim um **plano** que minimize o erro, mas a ideia é a mesma:

$Ataque = a \cdot Defesa + b \cdot HP + c$

```
# 1. Definir X e y
X_reg2 = df[['Defense', 'Health']] # Usando duas features
y_reg2 = df['Attack']

# 2. Criar e Treinar
modelo_reg2 = LinearRegression()
modelo_reg2.fit(X_reg2, y_reg2)

# 3. Fazer Previsões
y_pred_reg2 = modelo_reg2.predict(X_reg2)

# 4. Calcular o Erro
rmse_2 = np.sqrt(mean_squared_error(y_reg2, y_pred_reg2))
print(f"RMSE (1 Variável - Defesa): {rmse:.2f}")
print(f"RMSE (2 Variáveis - Defesa e HP): {rmse_2:.2f}") # (O erro deve diminuir!)

# 5. Plotar o Plano 3D
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(12, 8))
ax = fig.add_subplot(111, projection='3d')

# Pontos reais
ax.scatter(
    df['Defense'], df['Health'], df['Attack'], 
    c='blue', alpha=0.5, label='Dados Reais'
)

# Criando a superfície do plano
xx, yy = np.meshgrid(range(0, 250, 25), range(0, 250, 25))
zz = modelo_reg2.coef_[0] * xx + modelo_reg2.coef_[1] * yy + modelo_reg2.intercept_
ax.plot_surface(xx, yy, zz, alpha=0.3, color='red', label='Plano de Regressão')

ax.set_xlabel('Defesa')
ax.set_ylabel('HP')
ax.set_zlabel('Ataque (Previsto)')
plt.title("Regressão Linear com 2 Variáveis (Plano)")
plt.show()
```