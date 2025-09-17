Vamos explorar as funções em Python, abordando vários conceitos importantes como definição de funções, argumentos nomeados, tipagem de dados e mais.

### 1. Definição de Funções

Uma função em Python é definida usando a palavra-chave `def` seguida pelo nome da função e parênteses, que podem conter parâmetros. O bloco de código dentro de uma função é indentado.

```python
def minha_funcao():
    print("Olá, mundo!")

```

### 2. Argumentos e Parâmetros

Uma função pode receber argumentos, que são valores passados para a função. Estes argumentos são utilizados dentro da função como variáveis.

```python
def saudar(nome):
    print(f"Olá, {nome}!")

```

### 3. Argumentos Nomeados (Keyword Arguments)

Em Python, você pode passar argumentos usando o nome dos parâmetros, o que permite que eles sejam passados fora de ordem.

```python
def descrever_animal(tipo, nome):
    print(f"Eu tenho um {tipo} chamado {nome}.")

descrever_animal(nome="Rex", tipo="cachorro")

```

### 4. Argumentos Padrão

Você pode definir um valor padrão para argumentos na definição da função. Se o argumento não for passado, o valor padrão é usado.

```python
def descrever_animal(tipo, nome="Sem nome"):
    print(f"Eu tenho um {tipo} chamado {nome}.")

descrever_animal("gato")

```

### 5. Retorno de Valores

Funções podem retornar valores usando a palavra-chave `return`. Isso permite que a função envie de volta um resultado ao seu chamador.

```python
def soma(a, b):
    return a + b

resultado = soma(5, 3)
print(resultado)

```

### 6. Print com valor atribuido

Para atribuir o parametro na forma de string é possível fazer isso:

```python
def soma(a, b):
    print(f"{a=} + {b=} = {a+b}")

soma(10,4)

```

### 7. Argumentos Arbitrários

Se você não sabe quantos argumentos serão passados para sua função, adicione um asterisco (*) antes do nome do parâmetro na definição da função. Isso cria uma tupla de argumentos.

```python
def fazer_pizza(*ingredientes):
    print("Fazendo uma pizza com os seguintes ingredientes:")
    for ingrediente in ingredientes:
        print(f"- {ingrediente}")

fazer_pizza("queijo", "tomate", "orégano")

```

### 8. Argumentos de Palavras-chave Arbitrárias

Para aceitar um número arbitrário de argumentos de palavra-chave, use dois asteriscos (**) antes do nome do parâmetro. Isso cria um dicionário de argumentos.

```python
def configurar_perfil(**dados):
    print("Perfil:")
    for chave, valor in dados.items():
        print(f"{chave}: {valor}")

configurar_perfil(nome="João", idade=30, cidade="São Paulo")

```

### 9. Tipagem de Dados em Funções

Python é uma linguagem de tipagem dinâmica, mas o Python 3.5 introduziu uma sintaxe para adicionar anotações de tipo. Embora não afetem a execução do programa, elas podem ser úteis para documentação e ferramentas de análise estática.

```python
def soma(a: int, b: int) -> int:
    return a + b

```

Essas anotações de tipo ajudam a documentar o código e podem ser úteis em ambientes de desenvolvimento para verificação de tipo estático, especialmente usando ferramentas como Mypy.

### Conclusão

Funções em Python são uma ferramenta poderosa que permite a reutilização de código, organização e modularidade. Usar funções corretamente pode ajudar a tornar o código mais claro, testável e fácil de manter.

[[Manipulação de Funções]]

[[Clojures]]

[[Lambda]]

[[Escopo de variáveis]]

[[Decoradores]]
