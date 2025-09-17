Os dicionários em Python são estruturas de dados muito poderosas e flexíveis, usadas para armazenar e manipular dados de uma forma que permite acesso rápido a valores através de chaves únicas. Eles são parte integrante da linguagem e oferecem uma maneira eficiente de associar pares chave-valor. Aqui está um guia abrangente sobre dicionários em Python:

### Criação de Dicionários

Dicionários são criados usando chaves `{}` ou a função construtora `dict()`. Aqui estão alguns exemplos:

```python
# Criando um dicionário vazio
d1 = {}
d2 = dict()

# Criando um dicionário com pares chave-valor
d3 = {'nome': 'Alice', 'idade': 25}
d4 = dict(nome='Bob', idade=30)

```

### Acessando Elementos

Você pode acessar um valor em um dicionário usando sua chave correspondente colocada entre colchetes `[]` ou com o método `get()`:

```python
d = {'nome': 'Alice', 'idade': 25}
print(d['nome'])  # Saída: Alice

# Usando get, que retorna None se a chave não existir
print(d.get('altura'))  # Saída: None

```

### Adicionando e Modificando Elementos

Você pode adicionar novos elementos ou modificar valores existentes especificando a chave:

```python
d = {'nome': 'Alice', 'idade': 25}
d['altura'] = 165  # Adiciona uma nova chave 'altura' com seu valor
d['nome'] = 'Ana'  # Modifica o valor associado à chave 'nome'

```

### Removendo Elementos

Existem várias formas de remover elementos de um dicionário:

```python
d = {'nome': 'Alice', 'idade': 25, 'altura': 165}
del d['altura']  # Remove a chave 'altura'
valor = d.pop('idade')  # Remove 'idade' e retorna seu valor
d.popitem()  # Remove e retorna um par (chave, valor), geralmente o último adicionado
d.clear()  # Limpa todos os elementos do dicionário

```

### Iterando Sobre Dicionários

Você pode iterar sobre as chaves, valores ou ambos de um dicionário:

```python
d = {'nome': 'Alice', 'idade': 25}

# Iterar sobre chaves
for chave in d:
    print(chave)

# Iterar sobre valores
for valor in d.values():
    print(valor)

# Iterar sobre pares chave-valor
for chave, valor in d.items():
    print(chave, valor)

```

### Métodos Úteis

Dicionários possuem vários métodos úteis para manipulação e consulta:

- `keys()`: retorna uma visualização das chaves no dicionário.
- `values()`: retorna uma visualização dos valores no dicionário.
- `items()`: retorna uma visualização dos pares chave-valor no dicionário.
- `update()`: atualiza o dicionário com elementos de outro dicionário ou iteráveis de pares chave-valor.
- `setdefault()`: retorna o valor de uma chave se ela existir; caso contrário, insere a chave com um valor especificado.

### Considerações de Performance

- **Acesso**: O acesso aos elementos em um dicionário é geralmente muito rápido, independentemente do tamanho do dicionário, porque utiliza uma tabela de hash interna.
- **Ordem**: A partir do Python 3.7, os dicionários mantêm a ordem de inserção como uma característica da linguagem.

Os dicionários são uma ferramenta essencial e potente para qualquer programador Python, ideal para quando você precisa de uma mapeamento eficiente entre pares de chave e valor.

[[Métodos de Dicionários]]