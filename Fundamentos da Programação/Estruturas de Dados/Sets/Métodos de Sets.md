Com certeza! 👍 Vamos criar uma lista de consulta completa com **todos os métodos** disponíveis para `sets` em Python.

```
numeros = {1, 2, 3, 4}
```

---

### **1. Métodos para Adicionar Elementos ➕**

Estes métodos modificam o `set` original, adicionando novos itens.

|Método|Descrição|
|---|---|
|`add()`|Adiciona um único elemento ao set.|
|`update()`|Adiciona todos os elementos de um ou mais iteráveis ao set.|

#### **`.add(elemento)`**

- **O que faz:** Adiciona um único elemento. Se o elemento já estiver presente, o `set` não é alterado.
    
- **Sintaxe:** `meu_set.add(novo_elemento)`
    
- **Exemplo:**
    
    Python
    
    ```
    numeros.add(5)
    print(numeros)  # Saída: {1, 2, 3, 4, 5}
    
    numeros.add(2)  # Tentando adicionar um elemento que já existe
    print(numeros)  # Saída: {1, 2, 3, 4, 5} (sem mudanças)
    ```
    

#### **`.update(*outros_iteraveis)`**

- **O que faz:** "Funde" o `set` com um ou mais iteráveis (como listas, tuplas, ou outros sets), adicionando todos os seus itens. Duplicatas são ignoradas.
    
- **Sintaxe:** `meu_set.update(iteravel1, iteravel2, ...)`
    
- **Exemplo:**
    
    Python
    
    ```
    numeros.update([4, 5, 6], {7, 8})
    print(numeros)
    # Saída: {1, 2, 3, 4, 5, 6, 7, 8}
    ```
    

---

### **2. Métodos para Remover Elementos ➖**

Estes métodos modificam o `set` original, removendo itens. A principal diferença entre eles é o comportamento quando o item não é encontrado.

|Método|Descrição|Comportamento se o item não existe|
|---|---|---|
|`remove()`|Remove um elemento específico.|Lança um erro `KeyError` 💥.|
|`discard()`|Remove um elemento específico.|Não faz nada ✅.|
|`pop()`|Remove e retorna um elemento aleatório.|Lança um erro `KeyError` se o set estiver vazio.|
|`clear()`|Remove **todos** os elementos do set.|N/A.|

#### **`.remove(elemento)`**

- **O que faz:** Remove o elemento especificado. Use quando você tem certeza que o elemento existe ou quer que o programa pare caso ele não exista.
    
- **Sintaxe:** `meu_set.remove(elemento_a_remover)`
    
- **Exemplo:**
    
    Python
    
    ```
    numeros = {1, 2, 3, 4}
    numeros.remove(3)
    print(numeros)  # Saída: {1, 2, 4}
    
    # numeros.remove(99) # Isto causaria um KeyError
    ```
    

#### **`.discard(elemento)`**

- **O que faz:** Remove o elemento especificado. É a forma "segura" de remover, pois não causa erro se o item não estiver no `set`.
    
- **Sintaxe:** `meu_set.discard(elemento_a_remover)`
    
- **Exemplo:**
    
    Python
    
    ```
    numeros = {1, 2, 3, 4}
    numeros.discard(4)
    print(numeros)  # Saída: {1, 2, 3}
    
    numeros.discard(99) # Nenhuma exceção é lançada
    print(numeros)  # Saída: {1, 2, 3}
    ```
    

#### **`.pop()`**

- **O que faz:** Remove e retorna um membro arbitrário (aleatório) do `set`. Como os sets não têm ordem, você não sabe qual elemento será removido. Útil quando você só quer pegar e remover "qualquer" item.
    
- **Sintaxe:** `elemento_removido = meu_set.pop()`
    
- **Exemplo:**

    ```python
    letras = {'a', 'b', 'c'}
    letra_removida = letras.pop()
    print(f"Letra removida: {letra_removida}")
    print(f"Set restante: {letras}")
    # A saída pode variar, ex:
    # Letra removida: c
    # Set restante: {'a', 'b'}
    ```
    

#### **`.clear()`**

- **O que faz:** Esvazia o `set`, removendo todos os seus elementos.
    
- **Sintaxe:** `meu_set.clear()`
    
- **Exemplo:**

    ```python
    numeros = {1, 2, 3, 4}
    numeros.clear()
    print(numeros)  # Saída: set()
    ```
    

---

### **3. Operações de Conjuntos (Retornam um Novo Set) 🪄**

Estes são os métodos que implementam as operações matemáticas de conjuntos. Eles **não modificam** o `set` original, mas sim **retornam um novo `set`** com o resultado.

Vamos usar estes dois sets para os exemplos:

Python

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
````

|Método|Operador Equivalente|Descrição|
|---|---|---|
|`union()`|`|`|
|`intersection()`|`&`|Retorna um novo set com os elementos presentes em ambos os sets.|
|`difference()`|`-`|Retorna um novo set com elementos em `A` mas não em `B`.|
|`symmetric_difference()`|`^`|Retorna um novo set com elementos que estão em `A` ou `B`, mas não em ambos.|

#### **`.union(*outros_sets)`**

- **Sintaxe:** `A.union(B, C, ...)`
    
- **Exemplo:**
    
    ```python
    uniao = A.union(B)
    print(uniao) # Saída: {1, 2, 3, 4, 5, 6}
    ```
    

#### **`.intersection(*outros_sets)`**

- **Sintaxe:** `A.intersection(B, C, ...)`
    
- **Exemplo:**
    
    ```python
    intersecao = A.intersection(B)
    print(intersecao) # Saída: {3, 4}
    ```
    

#### **`.difference(*outros_sets)`**

- **Sintaxe:** `A.difference(B, C, ...)`
    
- **Exemplo:**
    
    ```python
    diferenca = A.difference(B)
    print(diferenca) # Saída: {1, 2}
    ```
    

#### **`.symmetric_difference(outro_set)`**

- **Sintaxe:** `A.symmetric_difference(B)`
    
- **Exemplo:**

    ```python
    dif_simetrica = A.symmetric_difference(B)
    print(dif_simetrica) # Saída: {1, 2, 5, 6}
    ```
    

---

### **4. Operações de Conjuntos (Modificam o Set Original) 🔄**

Estes métodos realizam as mesmas operações matemáticas, mas em vez de retornarem um novo `set`, eles **modificam o `set` original**. Seus nomes geralmente terminam com `_update`.

|Método|Operador Equivalente|Descrição|
|---|---|---|
|`update()` (já visto)|`|=`|
|`intersection_update()`|`&=`|Mantém apenas os elementos que também estão no outro set.|
|`difference_update()`|`-=`|Remove todos os elementos que também estão no outro set.|
|`symmetric_difference_update()`|`^=`|Atualiza o set para conter a diferença simétrica.|

#### **`.intersection_update(*outros_sets)`**

- **Sintaxe:** `A.intersection_update(B, C, ...)`
    
- **Exemplo:**
    
    Python
    
    ```python
    A = {1, 2, 3, 4}
    B = {3, 4, 5, 6}
    A.intersection_update(B) # Modifica A
    print(A) # Saída: {3, 4}
    ```
    

#### **`.difference_update(*outros_sets)`**

- **Sintaxe:** `A.difference_update(B, C, ...)`
    
- **Exemplo:**
    
    Python
    
    ```python
    A = {1, 2, 3, 4}
    B = {3, 4, 5, 6}
    A.difference_update(B) # Modifica A
    print(A) # Saída: {1, 2}
    ```
    

#### **`.symmetric_difference_update(outro_set)`**

- **Sintaxe:** `A.symmetric_difference_update(B)`
    
- **Exemplo:**
    
    Python
    
    ```python
    A = {1, 2, 3, 4}
    B = {3, 4, 5, 6}
    A.symmetric_difference_update(B) # Modifica A
    print(A) # Saída: {1, 2, 5, 6}
    ```
    

---

### **5. Métodos de Comparação e Verificação (Retornam `True` ou `False`)❓**

Estes métodos não alteram os sets, apenas os comparam e retornam um valor booleano.

|Método|Operador Equivalente|Descrição|
|---|---|---|
|`issubset()`|`<=`|Retorna `True` se todos os elementos do set estiverem no outro.|
|`issuperset()`|`>=`|Retorna `True` se o set contiver todos os elementos do outro.|
|`isdisjoint()`|N/A|Retorna `True` se os sets não tiverem nenhum elemento em comum.|

#### **`.issubset(outro_set)`**

- **Sintaxe:** `A.issubset(B)`
    
- **Exemplo:**
    
    Python
    
    ```python
    subset = {1, 2}
    superset = {1, 2, 3, 4}
    print(subset.issubset(superset)) # Saída: True
    print(superset.issubset(subset)) # Saída: False
    ```
    

#### **`.issuperset(outro_set)`**

- **Sintaxe:** `A.issuperset(B)`
    
- **Exemplo:**

    ```python
    subset = {1, 2}
    superset = {1, 2, 3, 4}
    print(superset.issuperset(subset)) # Saída: True
    print(subset.issuperset(superset)) # Saída: False
    ```
    

#### **`.isdisjoint(outro_set)`**

- **Sintaxe:** `A.isdisjoint(B)`
    
- **Exemplo:**

    ```python
    set1 = {1, 2}
    set2 = {3, 4}
    set3 = {2, 5}
    print(set1.isdisjoint(set2)) # Saída: True (nenhum elemento em comum)
    print(set1.isdisjoint(set3)) # Saída: False (o '2' é comum)
    ```
    

---

### **6. Outros Métodos Úteis ✨**

#### **`.copy()`**

- **O que faz:** Retorna uma cópia rasa (_shallow copy_) do `set`. Útil quando você quer modificar uma cópia sem alterar o original.
    
- **Sintaxe:** `novo_set = meu_set.copy()`
    
- **Exemplo:**
    
    Python
    
    ```python
    original = {1, 2, 3}
    copia = original.copy()
    copia.add(4)
    
    print(f"Original: {original}") # Saída: Original: {1, 2, 3}
    print(f"Cópia: {copia}")     # Saída: Cópia: {1, 2, 3, 4}
    ```
    

### **E o `frozenset`? 🧊**

O `frozenset` é a versão imutável de um set. Por ser imutável, ele **não possui** nenhum dos métodos que modificam o set original.

✅ **Métodos que `frozenset` POSSUI (os que não alteram o original):**

- `union()`
    
- `intersection()`
    
- `difference()`
    
- `symmetric_difference()`
    
- `issubset()`
    
- `issuperset()`
    
- `isdisjoint()`
    
- `copy()`
    

❌ **Métodos que `frozenset` NÃO POSSUI (os que alteram o original):**

- `add()`
    
- `remove()`
    
- `discard()`
    
- `pop()`
    
- `clear()`
    
- `update()`
    
- `intersection_update()`
    
- `difference_update()`
    
- `symmetric_difference_update()`
    

Esta lista cobre todos os métodos disponíveis para sets. É uma "cola" excelente para se ter à mão! 🚀