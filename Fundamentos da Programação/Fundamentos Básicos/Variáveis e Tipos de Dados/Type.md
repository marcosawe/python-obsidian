Em Python, você pode usar a função `type()` para descobrir o tipo de uma variável. Basta passar a variável como argumento para a função `type()`, e ela retornará o tipo de dados da variável. Aqui está um exemplo:

```python
# Definindo algumas variáveis
idade = 25
altura = 1.75
nome = "João"
tem_carro = True
numeros = [1, 2, 3, 4, 5]
coordenadas = (10, 20)
aluno = {"nome": "Maria", "idade": 20, "curso": "Engenharia"}
vogais = {'a', 'e', 'i', 'o', 'u'}

# Usando type() para descobrir o tipo de cada variável
print(type(idade))        # <class 'int'>
print(type(altura))       # <class 'float'>
print(type(nome))         # <class 'str'>
print(type(tem_carro))    # <class 'bool'>
print(type(numeros))      # <class 'list'>
print(type(coordenadas))  # <class 'tuple'>
print(type(aluno))        # <class 'dict'>
print(type(vogais))       # <class 'set'>

```

Este código imprimirá na tela o tipo de cada variável, indicado entre `<class '...'>`. Isso permite que você saiba com precisão o tipo de dados que está lidando em seu programa.