Listas em Python são estruturas de dados flexíveis e dinâmicas que permitem armazenar coleções ordenadas de itens, que podem ser de diferentes tipos. Elas são muito versáteis e úteis em muitos contextos de programação. Aqui estão algumas das principais características e funcionalidades das listas em Python:

### Criação de Lista

Você pode criar uma lista simplesmente colocando elementos entre colchetes `[]` e separando-os por vírgulas. Exemplo:

```python
minha_lista = [1, 2, 3]
lista_de_strings = ["hello", "world"]
lista_mista = [1, "hello", 3.14, True]

```

### Acessando Elementos

Os elementos de uma lista podem ser acessados pelo índice, começando do zero para o primeiro elemento. Exemplo:

```python
primeiro_elemento = minha_lista[0]  # Retorna 1
ultimo_elemento = minha_lista[-1]  # Retorna 3

```

### Slicing (Fatiamento)

Você pode acessar uma subparte de uma lista usando a sintaxe de slicing:

```python
numeros = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
sub_lista = numeros[2:5]  # Retorna [2, 3, 4]

```

### Modificando Listas

Listas são mutáveis, ou seja, você pode modificar seus elementos:

```python
numeros[0] = -1  # Modifica o primeiro elemento para -1
numeros.append(10)  # Adiciona 10 ao final da lista
numeros.extend([11, 12])  # Adiciona múltiplos elementos ao final
numeros.insert(1, 'novo')  # Insere 'novo' na posição 1

```

### Removendo Elementos

Você pode remover elementos de uma lista de várias maneiras:

```python
numeros.remove('novo')  # Remove a primeira ocorrência de 'novo'
del numeros[0]  # Remove o elemento na posição 0
ultimo = numeros.pop()  # Remove e retorna o último elemento da lista

```

### List Comprehension

Uma forma concisa de criar listas a partir de outras listas, aplicando uma expressão a cada elemento:

```python
quadrados = [x**2 for x in range(10)]  # Cria uma lista de quadrados dos números de 0 a 9

```

### Operações Comuns

Listas em Python suportam várias operações que facilitam o trabalho com elas:

```python
len(numeros)  # Retorna o número de elementos na lista
sum(numeros)  # Retorna a soma dos elementos
sorted(numeros)  # Retorna uma nova lista com elementos ordenados
min(numeros)  # Retorna o menor elemento
max(numeros)  # Retorna o maior elemento

```

### Iterando sobre Listas

Você pode iterar sobre os elementos de uma lista usando um loop `for`:

```python
for numero in numeros:
    print(numero)

```

Essas são algumas das funcionalidades básicas das listas em Python. Elas são extremamente úteis e amplamente utilizadas em todos os tipos de programas Python, de scripts simples a sistemas complexos.

[[Métodos de Lista]]
