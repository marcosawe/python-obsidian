Os decoradores em Python são uma ferramenta poderosa que permite modificar o comportamento de funções ou métodos. Eles são usados para estender ou alterar a funcionalidade de funções ou métodos de forma elegante e reutilizável. Decoradores são muitas vezes utilizados em frameworks web como Flask e Django para adicionar funcionalidades a rotas, e em testes para setup e teardown de testes.

### Conceito Básico de Decoradores

Um decorador é uma função que recebe outra função como argumento e retorna uma função. Isso permite adicionar funcionalidades antes e depois da função original ser chamada, sem modificar a função em si.

### Estrutura de um Decorador

Um decorador típico em Python pode ser escrito como uma função que define uma função interna:

```python
def my_decorator(func):
    def wrapper():
        print("Algo é executado antes da função.")
        func()
        print("Algo é executado depois da função.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()

```

Neste exemplo, `my_decorator` é um decorador que envolve a função `say_hello()`. Quando você chama `say_hello()`, a saída será:

```
Algo é executado antes da função.
Hello!
Algo é executado depois da função.

```

### Decoradores com Argumentos

Se a função original precisa de argumentos, o `wrapper` deve ser definido com esses argumentos:

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Algo é executado antes da função.")
        result = func(*args, **kwargs)
        print("Algo é executado depois da função.")
        return result
    return wrapper

@my_decorator
def greet(name):
    print(f"Hello {name}!")

greet("Alice")

```

### Decoradores com Argumentos Próprios

Você também pode criar decoradores que aceitam seus próprios argumentos:

```python
def repeat(num_times):
    def decorator_repeat(func):
        def wrapper(*args, **kwargs):
            for _ in range(num_times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator_repeat

@repeat(num_times=3)
def greet(name):
    print(f"Hello {name}!")

greet("Alice")

```

### Usando Decoradores em Métodos de Classe

Decoradores também podem ser aplicados a métodos de classe. Para isso, apenas certifique-se de incluir `self` como um argumento no `wrapper`:

```python
def my_decorator(func):
    def wrapper(self):
        print("Algo é executado antes do método.")
        func(self)
        print("Algo é executado depois do método.")
    return wrapper

class MyClass:
    @my_decorator
    def my_method(self):
        print("Método da classe.")

obj = MyClass()
obj.my_method()

```

### Decoradores Integrados em Python

Python tem vários decoradores integrados, como @[[staticmethod]], @[[classmethod]], e @[[property]]. Eles são usados para definir métodos que operam no nível da classe, transformar métodos em propriedades, e mais.

### Uso de Functools.wraps

Quando você cria decoradores, é uma boa prática usar `functools.wraps` dentro de sua função `wrapper`. Isso é importante para preservar a metainformação da função original, como o nome e a documentação:

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Algo é executado antes da função.")
        return func(*args, **kwargs)
    return wrapper

```

Decoradores são uma forma poderosa e expressiva de adicionar funcionalidades repetitivas ou padrões de lógica de negócios a funções e métodos em Python, mantendo o código limpo e bem organizado.