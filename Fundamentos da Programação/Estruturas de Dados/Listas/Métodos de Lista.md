Em Python, a classe `list` oferece diversos métodos que facilitam a manipulação de listas. Aqui estão todos os métodos disponíveis para um objeto `list`:

1. **append(`x`)**: Adiciona um item ao fim da lista.
2. **extend(`iterable`)**: Estende a lista adicionando todos os itens do iterável fornecido.
3. **insert(`i`, `x`)**: Insere um item em uma posição especificada.
4. **remove(x)**: Remove o primeiro item da lista cujo valor é igual a x. Lança um `ValueError` se o valor não for encontrado.
5. **pop([i])**: Remove o item na posição dada e o retorna. Se nenhum índice é especificado, `pop()` remove e retorna o último item da lista.
6. **clear()**: Remove todos os itens da lista.
7. **index(x[, start[, end]])**: Retorna o índice do primeiro item cujo valor é igual a x. Os argumentos opcionais start e end são usados para limitar a busca a uma subseção específica da lista.
8. **count(x)**: Retorna o número de vezes que x aparece na lista.
9. **sort(*, key=None, reverse=False)**: Ordena os itens da lista in-place (os itens são modificados na própria lista). Você pode usar os argumentos `key` e `reverse` para personalizar a ordenação.
10. **reverse()**: Inverte a ordem dos elementos na lista in-place.
11. **copy()**: Retorna uma cópia rasa da lista.

Esses métodos proporcionam uma ampla gama de operações que você pode realizar com listas em Python, tornando-as extremamente versáteis para manipulação de dados.

## Exemplos

```python
# Criando uma lista inicial
frutas = ["maçã", "banana", "cereja"]

# append() - Adicionando uma fruta ao final
frutas.append("laranja")
print("Após append:", frutas)

# extend() - Adicionando múltiplas frutas
frutas.extend(["manga", "uva"])
print("Após extend:", frutas)

# insert() - Inserindo uma fruta em uma posição específica
frutas.insert(1, "kiwi")
print("Após insert:", frutas)

# remove() - Removendo uma fruta pelo nome
frutas.remove("banana")
print("Após remove:", frutas)

# pop() - Removendo uma fruta pela posição e retornando-a
removida = frutas.pop(2)  # Remove "cereja"
print("Após pop:", frutas, "(removida:", removida + ")")

# clear() - Limpando todas as frutas da lista
frutas.clear()
print("Após clear:", frutas)

# Recriando a lista para mais exemplos
frutas = ["maçã", "banana", "cereja", "banana", "manga"]

# index() - Encontrando o índice da primeira 'banana'
indice_banana = frutas.index("banana")
print("Índice da primeira banana:", indice_banana)

# count() - Contando quantas vezes 'banana' aparece
contagem_banana = frutas.count("banana")
print("Contagem de banana:", contagem_banana)

# sort() - Ordenando a lista (in-place)
frutas.sort()
print("Após sort:", frutas)

# reverse() - Revertendo a ordem da lista
frutas.reverse()
print("Após reverse:", frutas)

# copy() - Fazendo uma cópia da lista
copia_frutas = frutas.copy()
print("Cópia das frutas:", copia_frutas)

```