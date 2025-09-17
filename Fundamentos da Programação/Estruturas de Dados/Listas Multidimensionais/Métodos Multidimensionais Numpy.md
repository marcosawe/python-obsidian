NumPy oferece uma vasta gama de métodos que podem ser aplicados a arrays multidimensionais, possibilitando manipulações complexas de forma eficiente. Aqui está uma lista abrangente de métodos disponíveis para objetos do tipo array no NumPy, com uma breve descrição de suas funcionalidades:

### Métodos de Arrays em NumPy

1. **all()**: Verifica se todos os elementos são avaliados como True.
2. **any()**: Verifica se algum dos elementos é avaliado como True.
3. **argmax()**: Retorna os índices dos valores máximos ao longo de um eixo.
4. **argmin()**: Retorna os índices dos valores mínimos ao longo de um eixo.
5. **argsort()**: Retorna os índices que ordenariam o array.
6. **astype()**: Copia o array e o converte para um tipo especificado.
7. **clip()**: Limita os valores em um intervalo.
8. **compress()**: Retorna os elementos selecionados por uma condição.
9. **conj()**, **conjugate()**: Retorna o conjugado complexo de todos os elementos.
10. **copy()**: Retorna uma cópia do array.
11. **cumprod()**: Retorna o produto cumulativo dos elementos ao longo de um eixo.
12. **cumsum()**: Retorna a soma cumulativa dos elementos ao longo de um eixo.
13. **diagonal()**: Retorna a diagonal especificada.
14. **dot()**: Produto escalar entre dois arrays.
15. **dtype()**: Retorna o tipo de dados dos elementos do array.
16. **fill()**: Preenche o array com um valor escalar.
17. **flatten()**: Retorna uma cópia do array colapsada em uma dimensão.
18. **getfield()**: Retorna um campo do array como um certo tipo.
19. **item()**: Copia um elemento do array como um tipo Python escalonável.
20. **itemset()**: Insere um valor escalar em um array.
21. **max()**: Retorna o valor máximo ao longo de um eixo.
22. **mean()**: Retorna a média dos elementos ao longo de um eixo.
23. **min()**: Retorna o valor mínimo ao longo de um eixo.
24. **nbytes()**: Retorna o número total de bytes ocupados pelo array.
25. **ndim()**: Retorna o número de dimensões do array.
26. **nonzero()**: Retorna os índices dos elementos que não são zero.
27. **prod()**: Retorna o produto dos elementos ao longo de um eixo.
28. **ptp()**: Retorna a diferença entre o máximo e o mínimo ao longo de um eixo.
29. **put()**: Substitui elementos especificados do array por valores dados.
30. **ravel()**: Retorna uma visão achatada do array.
31. **repeat()**: Repete os elementos do array.
32. **reshape()**: Dá uma nova forma ao array sem alterar seus dados.
33. **resize()**: Altera a forma e o tamanho do array.
34. **round()**: Arredonda os elementos do array a uma precisão dada.
35. **searchsorted()**: Encontra índices onde elementos devem ser inseridos para manter a ordem.
36. **setfield()**: Define o campo do array como um certo tipo.
37. **setflags()**: Define atributos de flags do array.
38. **shape()**: Retorna a forma do array.
39. **size()**: Retorna o número de elementos do array.
40. **sort()**: Ordena o array.
41. **squeeze()**: Remove eixos de tamanho um do array.
42. **std()**: Calcula o desvio padrão ao longo de um eixo.
43. **sum()**: Soma os elementos ao longo de um eixo.
44. **swapaxes()**: Troca dois eixos do array.
45. **take()**: Retorna elementos de um array ao longo de um eixo.
46. **tobytes()**: Retorna o array como uma string de bytes.
47. **tofile()**: Escreve o array para um arquivo em formato binário.
48. **tolist()**: Converte o array para uma lista Python.
49. **tostring()**: Similar a tobytes(), para compatibilidade com versões anteriores.
50. **trace()**: Retorna a soma da diagonal.
51. **transpose()**: Permuta as dimensões do array.
52. **var()**: Calcula a variância ao longo de um eixo.
53. **view()**: Retorna uma

nova visão do array sem modificar os dados originais.

Esses métodos são extremamente úteis para manipulação e análise de dados em arrays. NumPy é projetado para lidar com grandes volumes de dados de maneira eficiente, e esses métodos são otimizados para operar diretamente em arrays sem a necessidade de loops explícitos em Python, o que melhora significativamente a performance.

## Exemplo:

```python
import numpy as np

# Criando um array de exemplo
array = np.array([[1, 2, 0], [4, 5, 6], [7, 8, 9]])

# all()
# Verifica se todos os elementos são True (0 é considerado False)
print("all():", array.all())  # Saída: False porque temos um 0 que é False

# any()
# Verifica se algum elemento é True
print("any():", array.any())  # Saída: True porque temos vários valores não-zero

# argmax()
# Retorna o índice do valor máximo do array
print("argmax():", array.argmax())  # Saída: Índice do valor máximo (flat index)
print("argmax(axis=0):", array.argmax(axis=0))  # Máximos nas colunas
print("argmax(axis=1):", array.argmax(axis=1))  # Máximos nas linhas

# argmin()
# Retorna o índice do valor mínimo do array
print("argmin():", array.argmin())  # Saída: Índice do valor mínimo (flat index)
print("argmin(axis=0):", array.argmin(axis=0))  # Mínimos nas colunas
print("argmin(axis=1):", array.argmin(axis=1))  # Mínimos nas linhas

# argsort()
# Retorna os índices que ordenariam o array
print("argsort():", array.argsort())  # Saída: Índices para cada linha

# astype()
# Copia o array e converte para um tipo especificado
float_array = array.astype(float)
print("astype(float):", float_array)

# clip()
# Limita os valores em um intervalo entre 3 e 6
clipped_array = array.clip(3, 6)
print("clip(3, 6):", clipped_array)

# compress()
# Retorna os elementos onde a condição é True (elementos maiores que 3)
compressed_array = array.compress(array > 3)
print("compress(array > 3):", compressed_array)

# conj(), conjugate()
# Retorna o conjugado complexo de todos os elementos (útil para arrays complexos)
# Demonstrando com um array complexo
complex_array = np.array([1+2j, 3-4j])
print("conj():", complex_array.conj())
print("conjugate():", complex_array.conjugate())

# copy()
# Retorna uma cópia do array
array_copy = array.copy()
print("copy():", array_copy)

# cumprod()
# Retorna o produto cumulativo dos elementos ao longo de um eixo
cumulative_product = array.cumprod()
print("cumprod():", cumulative_product)

# cumsum()
# Retorna a soma cumulativa dos elementos ao longo de um eixo
cumulative_sum = array.cumsum()
print("cumsum():", cumulative_sum)

# diagonal()
# Retorna a diagonal principal do array
diagonal = array.diagonal()
print("diagonal():", diagonal)

# dot()
# Produto escalar entre dois arrays
dot_product = array.dot(array.T)  # produto escalar de array com sua transposta
print("dot():", dot_product)

# dtype()
# Retorna o tipo de dados dos elementos do array
print("dtype():", array.dtype)

# fill()
# Preenche o array com um valor escalar
filled_array = array.copy()
filled_array.fill(10)
print("fill(10):", filled_array)

# flatten()
# Retorna uma cópia do array colapsada em uma dimensão
flattened_array = array.flatten()
print("flatten():", flattened_array)

# getfield()
# Retorna um campo do array como um certo tipo, mais comum em arrays estruturados
# Exemplo simples com um tipo básico
dtype = np.dtype([('x', int), ('y', np.int32)])
structured_array = np.array([(1, 2), (3, 4)], dtype=dtype)
print("getfield(np.int32):", structured_array.getfield(np.int32))

# item()
# Copia um elemento do array como um tipo Python escalonável
single_item = array.item(4)  # Pegando o elemento no índice 4 (considerando a array plana)
print("item(4):", single_item)

# itemset()
# Insere um valor escalar em um índice específico do array
itemset_array = array.copy()
itemset_array.itemset(4, 100)
print("itemset(4, 100):", itemset_array)

# max()
# Retorna o valor máximo ao longo de um eixo
print("max():", array.max())  # Max global
print("max(axis=0):", array.max(axis=0))  # Máximo em cada coluna

# mean()
# Retorna a média dos elementos ao longo de um eixo
print("mean():", array.mean())  # Média global
print("mean(axis=0):", array.mean(axis=0))  # Média em cada coluna

# min()
# Retorna o valor mínimo ao longo de um eixo
print("min():", array.min())  # Min global
print("min(axis=0):", array.min(axis=0))  # Mínimo em cada coluna

# nbytes()
# Retorna o número total de bytes ocupados pelo array
print("nbytes():", array.nbytes)

# ndim()
# Retorna o número de dimensões do array
print("ndim():", array.ndim)

# nonzero()
# Retorna os índices dos elementos que não são zero
non_zero_indices = array.nonzero()
print("nonzero():", non_zero_indices)

# prod()
# Retorna o produto dos elementos ao longo de um eixo
print("prod():", array.prod())  # Produto global
print("prod(axis=0):", array.prod(axis=0))  # Produto em cada coluna

# ptp()
# Retorna a diferença entre o máximo e o mínimo ao longo de um eixo
print("ptp():", array.ptp())  # Diferença global
print("ptp(axis=0):", array.ptp(axis=0))  # Diferença em cada coluna

# put()
# Substitui elementos especificados do array por valores dados
put_array = array.copy()
put_array.put([0, 3, 6], [99, 88, 77])
print("put([0, 3, 6], [99, 88, 77]):", put_array)

# ravel()
# Retorna uma visão achatada do array
raveled_array = array.ravel()
print("ravel():", raveled_array)

# repeat()
# Repete os elementos do array
repeated_array = array.repeat(2)
print("repeat(2):", repeated_array)

# reshape()
# Dá uma nova forma ao array sem alterar seus dados
reshaped_array = array.reshape(1, 9)
print("reshape(1, 9):", reshaped_array)

# resize()
# Altera a forma e o tamanho do array
resized_array = np.resize(array, (2, 6))
print("resize((2, 6)):", resized_array)

# round()
# Arredonda os elementos do array a uma precisão dada
rounded_array = np.array([1.234, 2.345, 3.456])
print("round(1):", rounded_array.round(1))

# searchsorted()
# Encontra índices onde elementos devem ser inseridos para manter a ordem
sorted_array = np.array([1, 3, 5, 7])
print("searchsorted(4):", sorted_array.searchsorted(4))

# setfield()
# Define o campo do array como um certo tipo
# Não aplicável a arrays simples sem campos estruturados

# setflags()
# Define atributos de flags do array
flags_array = array.copy()
flags_array.setflags(write=False)  # Tornando o array somente leitura
# flags_array[0] = 10  # Isso causaria um erro, pois o array está somente leitura agora

# shape()
# Retorna a forma do array
print("shape():", array.shape)

# size()
# Retorna o número de elementos do array
print("size():", array.size)

# sort()
# Ordena o array
sorted_array = array.flatten()
sorted_array.sort()
print("sort():", sorted_array)

# squeeze()
# Remove eixos de tamanho um do array
squeezed_array = np.array([[[1, 2, 3]]])
print("squeeze():", squeezed_array.squeeze())

# std()
# Calcula o desvio padrão ao longo de um eixo
print("std():", array.std())  # Desvio padrão global
print("std(axis=0):", array.std(axis=0))  # Desvio padrão em cada coluna

# sum()
# Soma os elementos ao longo de um eixo
print("sum():", array.sum())  # Soma global
print("sum(axis=0):", array.sum(axis=0))  # Soma em cada coluna

# swapaxes()
# Troca dois eixos do array
swapped_axes_array = array.swapaxes(0, 1)
print("swapaxes(0, 1):", swapped_axes_array)

# take()
# Retorna elementos de um array ao longo de um eixo
taken_elements = array.take([0, 3, 6])
print("take([0, 3, 6]):", taken_elements)

# tobytes()
# Retorna o array como uma string de bytes
bytes_array = array.tobytes()
print("tobytes():", bytes_array)

# tofile()
# Escreve o array para um arquivo em formato binário
# Exemplo comentado, precisa de caminho de arquivo real para funcionar
# array.tofile('array_data.bin')

# tolist()
# Converte o array para uma lista Python
list_array = array.tolist()
print("tolist():", list_array)

# tostring()
# Similar a tobytes(), para compatibilidade com versões anteriores
# tostring está depreciado em favor de tobytes

# trace()
# Retorna a soma da diagonal
trace_value = array.trace()
print("trace():", trace_value)

# transpose()
# Permuta as dimensões do array
transposed_array = array.transpose()
print("transpose():", transposed_array)

# var()
# Calcula a variância ao longo de um eixo
print("var():", array.var())  # Variância global
print("var(axis=0):", array.var(axis=0))  # Variância em cada coluna

# view()
# Retorna uma nova visão do array sem modificar os dados originais
view_array = array.view()
print("view():", view_array)
```