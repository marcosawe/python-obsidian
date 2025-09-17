### **Métodos Tradicionais (Presentes desde versões antigas)**
1. **`clear()`**  
   Remove todos os itens do dicionário.  
   Exemplo: `d.clear()`

2. **`copy()`**  
   Retorna uma cópia superficial do dicionário.  
   Exemplo: `d2 = d.copy()`

3. **`get(key[, default])`**  
   Retorna o valor de `key`. Se não existir, retorna `default` (ou `None` se omitido).  
   Exemplo: `valor = d.get("chave", 0)`

4. **`items()`**  
   Retorna uma visão (view) dos pares `(chave, valor)`.  
   Exemplo: `for chave, valor in d.items(): ...`

5. **`keys()`**  
   Retorna uma visão das chaves do dicionário.  
   Exemplo: `chaves = list(d.keys())`

6. **`values()`**  
   Retorna uma visão dos valores do dicionário.  
   Exemplo: `valores = list(d.values())`

7. **`pop(key[, default])`**  
   Remove `key` e retorna seu valor. Se `key` não existir e `default` for fornecido, retorna `default`; caso contrário, levanta `KeyError`.  
   Exemplo: `valor = d.pop("chave")`

8. **`popitem()`**  
   Remove e retorna um par `(chave, valor)` na ordem **LIFO (Last In, First Out)**. Levanta `KeyError` se o dicionário estiver vazio.  
   Exemplo: `chave, valor = d.popitem()`

9. **`setdefault(key[, default])`**  
   Se `key` existir, retorna seu valor. Caso contrário, insere `key` com valor `default` (padrão: `None`) e retorna `default`.  
   Exemplo: `d.setdefault("nova_chave", 10)`

10. **`update([other])`**  
    Atualiza o dicionário com pares `chave:valor` de `other` (outro dicionário ou iterável). Sobrescreve chaves existentes.  
    Exemplo: `d.update({"a": 1, "b": 2})`

11. **`fromkeys(iterable[, value])`** (método de classe)  
    Cria um novo dicionário com chaves de `iterable` e valores iguais a `value` (padrão: `None`).  
    Exemplo: `d = dict.fromkeys(["a", "b"], 0)`

---

### **Novos Métodos e Funcionalidades (Adicionados a partir do Python 3.8+)**

12. **`__reversed__()`** (Python 3.8+)  
    Suporta a função `reversed()` para iterar chaves na ordem **reversa de inserção**.  
    Exemplo: `for chave in reversed(d): ...`

13. **Operador `|` (União)** (Python 3.9+)  
    Combina dois dicionários em um novo (`d1 | d2`). Em conflitos, prevalecem valores de `d2`.  
    Exemplo: `d3 = d1 | d2`

14. **Operador `|=` (Atualização)** (Python 3.9+)  
    Atualiza o dicionário in-place com pares de outro (`d1 |= d2`).  
    Exemplo: `d1 |= {"novo": 99}`

---

### **Métodos de Visualização (Views)**
As visões retornadas por `.items()`, `.keys()` e `.values()` possuem métodos adicionais:

- **`mapping`** (Python 3.10+)  
  Retorna o dicionário original associado à visão.  
  Exemplo: `dicionario_original = d.keys().mapping`

- **Operações de Conjunto** (Disponíveis para **`keys()`** e **`items()`**):  
  `&` (interseção), `|` (união), `-` (diferença), `^` (diferença simétrica).  
  Exemplo: `chaves_comuns = d1.keys() & d2.keys()`

---

### **Exemplos de Uso**
```python
# Operador | (Python 3.9+)
d1 = {"a": 1, "b": 2}
d2 = {"b": 3, "c": 4}
d3 = d1 | d2  # {"a": 1, "b": 3, "c": 4}

# reversed() (Python 3.8+)
for chave in reversed(d3):
    print(chave)  # Saída: "c", "b", "a"

# .mapping (Python 3.10+)
view = d3.keys()
print(view.mapping is d3)  # True
```

Esta lista cobre todos os métodos disponíveis até o Python 3.13. Para mais detalhes, consulte a [documentação oficial](https://docs.python.org/3.13/library/stdtypes.html#mapping-types-dict).