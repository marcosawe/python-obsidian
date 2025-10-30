Em Python, os **operadores de pertencimento** servem para verificar se um elemento está (ou não está) presente dentro de uma sequência ou coleção, como **listas**, **tuplas**, **strings**, **sets** ou **dicionários**.

Existem dois:

---

### 1. `in` – verifica se o elemento está presente

Retorna `True` se o valor especificado for encontrado no objeto, caso contrário `False`.

```python
# Em lista
frutas = ["maçã", "banana", "uva"]
print("banana" in frutas)   # True
print("laranja" in frutas)  # False

# Em string
texto = "Python é incrível"
print("Python" in texto)    # True
print("java" in texto)      # False

# Em dicionário (verifica apenas chaves por padrão)
dados = {"nome": "Ana", "idade": 25}
print("nome" in dados)      # True
print("Ana" in dados)       # False
```

---

### 2. `not in` – verifica se o elemento **não** está presente

É o inverso do `in`.

```python
animais = ["gato", "cachorro", "pássaro"]
print("tigre" not in animais)   # True
print("gato" not in animais)    # False
```

---

### Resumo da lógica

|Operador|Significado|Exemplo|
|---|---|---|
|`in`|Verdadeiro se o valor existir na coleção|`"a" in "abc"` → `True`|
|`not in`|Verdadeiro se o valor **não** existir na coleção|`"x" not in "abc"` → `True`|

---

💡 **Dica:**

- Com **dicionários**, `in` e `not in` verificam **somente as chaves**, não os valores.
    
- Para testar valores, use:
    

```python
"João" in meu_dicionario.values()
```

---

Se quiser, posso te mostrar **um diagrama visual** de como o Python processa o `in` internamente. Isso ajuda a entender melhor a performance. Quer que eu faça?