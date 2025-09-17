Em Python, **iteráveis** são objetos que podem retornar seus membros um de cada vez, permitindo que sejam percorridos, geralmente em um loop. Muitos objetos em Python são iteráveis: listas, tuplas, dicionários, strings e conjuntos são todos exemplos de tipos de dados iteráveis. Além disso, muitos objetos definidos por bibliotecas de terceiros também são iteráveis.

### Conceito de Iteráveis

Um iterável é qualquer objeto em Python que implementa o método `__iter__`, que deve retornar um iterador, ou que define o método `__getitem__` com indexação sequencial começando do zero. Quando você cria um loop sobre um iterável, o Python automaticamente chama `__iter__()` para obter um iterador, que em seguida, é usado para fornecer os elementos um a um durante o ciclo do loop.

### Usando Iteráveis

Você pode iterar sobre um iterável usando um loop `for`, que é uma maneira de acessar cada item do iterável um por um:

```python
# Exemplo com uma lista
minha_lista = [1, 2, 3, 4]
for item in minha_lista:
    print(item)  # Saída: 1, 2, 3, 4

```

### Funções Relacionadas a Iteráveis

Python oferece várias funções que aceitam iteráveis como argumentos. Aqui estão algumas das mais comuns:

1. **`iter()`**: Recebe um iterável e retorna um iterador.
2. **`next()`**: Passa para o próximo item do iterador.
3. **`len()`**: Retorna o número de itens em um iterável.
4. **`sorted()`**: Retorna uma nova lista contendo todos os itens do iterável na ordem ordenada.
5. **`sum()`**: Soma os itens de um iterável.
6. **`max()`** e **`min()`**: Retorna o maior e o menor valor em um iterável, respectivamente.
7. **`enumerate()`**: Retorna uma tupla contendo uma contagem de cada elemento e o valor do elemento do iterável.

### Iteráveis vs Iteradores

É importante distinguir entre iteráveis e iteradores:

- **Iteráveis** são objetos que podem ser iterados.
- **Iteradores** são objetos que realizam a iteração. Eles conhecem o estado atual da iteração (ou seja, qual é o próximo item a ser retornado).

### Criando Iteráveis Personalizados

Você pode criar seus próprios objetos iteráveis implementando o método `__iter__` que deve retornar um iterador. O iterador, por sua vez, deve implementar o método `__next__`, que deve retornar o próximo item ou levantar uma exceção `StopIteration` quando não houver mais itens.

```python
class MinhaRange:
    def __init__(self, start, end):
        self.start = start
        self.end = end

    def __iter__(self):
        return MinhaRangeIterador(self.start, self.end)

class MinhaRangeIterador:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __next__(self):
        if self.current < self.end:
            num = self.current
            self.current += 1
            return num
        raise StopIteration

# Usando o iterável personalizado
for num in MinhaRange(1, 4):
    print(num)  # Saída: 1, 2, 3

```

### Conclusão

Iteráveis são uma parte fundamental do Python e um conceito chave para trabalhar eficientemente com coleções de dados. A habilidade de iterar sobre dados de forma eficiente e intuitiva é uma das razões pelas quais Python é tão popular para processamento de dados e análise.

[[Enumerate]]
