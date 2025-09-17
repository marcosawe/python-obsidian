Para tornar os métodos de manipulação de listas multidimensionais mais funcionais e genéricos, podemos utilizar comprehensions de lista (list comprehensions), a tipagem do Python com annotations e outras técnicas para melhorar a clareza e a reusabilidade do código. Vamos refatorar os exemplos anteriores utilizando essas práticas.

### 1. Criação de Matrizes com Tipagem

Primeiro, vamos adicionar annotations de tipo para tornar claro o tipo dos parâmetros e dos retornos das funções.

```python
from typing import List, Tuple

def zeros(shape: Tuple[int, ...]) -> List[List]:
    """ Cria uma matriz de zeros com a forma especificada. """
    if len(shape) == 1:
        return [0] * shape[0]
    return [zeros(shape[1:]) for _ in range(shape[0])]

def ones(shape: Tuple[int, ...]) -> List[List]:
    """ Cria uma matriz de uns com a forma especificada. """
    if len(shape) == 1:
        return [1] * shape[0]
    return [ones(shape[1:]) for _ in range(shape[0])]

```

### 2. Funções Genéricas para Operações Matriciais

Agora vamos refatorar as funções de adição e multiplicação de matrizes para aceitarem qualquer função de operação binária entre elementos. Isso tornará o código mais flexível e reutilizável.

```python
from typing import Callable

def elementwise_operation(a: List[List], b: List[List], op: Callable[[int, int], int]) -> List[List]:
    """ Aplica uma operação elementar entre duas matrizes. """
    return [
        [op(a[i][j], b[i][j]) for j in range(len(a[0]))]
        for i in range(len(a))
    ]

def add(x: int, y: int) -> int:
    return x + y

def multiply(x: int, y: int) -> int:
    return x * y

# Exemplo de uso
matriz_a = ones((2, 2))
matriz_b = ones((2, 2))
print("Soma de matrizes:", elementwise_operation(matriz_a, matriz_b, add))
print("Multiplicação de matrizes:", elementwise_operation(matriz_a, matriz_b, multiply))

```

### 3. Transposição de Matriz

Para a transposição, vamos garantir que a função seja capaz de lidar com listas de qualquer dimensão que representem matrizes retangulares.

```python
def transpose(matrix: List[List]) -> List[List]:
    """ Transpõe a matriz dada. """
    return list(map(list, zip(*matrix)))

# Exemplo de uso
matriz = ones((3, 2))
print("Transposição de matriz:", transpose(matriz))

```

### Conclusão

Utilizando annotations de tipo, list comprehensions e abstrações como passar funções como argumentos, conseguimos criar um conjunto de funções mais limpo, claro e flexível para trabalhar com matrizes usando listas em Python. Estas melhorias não apenas aumentam a reusabilidade do código mas também facilitam a manutenção e o entendimento para outros desenvolvedores ou para futuras revisões do próprio código.