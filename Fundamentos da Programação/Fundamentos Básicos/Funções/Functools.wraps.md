Olá\! Dando sequência à nossa jornada pelos conceitos mais profundos de Python, vamos falar sobre `functools.wraps`.

Este é um tópico diretamente ligado à nossa discussão anterior sobre **closures**, e é a ferramenta fundamental para criar **Decorators** (Decoradores) de maneira profissional em Python.

### 1\. O Contexto: O que é um Decorator?

Em Python, um **decorator** é um padrão de projeto. É, em essência, uma função que recebe outra função como argumento, adiciona alguma funcionalidade a ela (sem alterar seu código-fonte) e retorna uma nova função "envolvida" (ou a função original modificada).

Eles são uma aplicação direta de **Closures**. A função "wrapper" interna (que o decorator define) "se lembra" da função original que foi passada como argumento.

A sintaxe `@` é apenas um "açúcar sintático" (syntactic sugar):

```python
@meu_decorator
def minha_funcao():
    print("Corpo da função")

# É exatamente o mesmo que:
# def minha_funcao():
#     print("Corpo da função")
# minha_funcao = meu_decorator(minha_funcao)
```

### 2\. O Problema: Por que `functools.wraps` é Necessário?

Vamos criar um decorator simples que marca o tempo de execução de uma função.

**Primeiro, vamos definir a função que queremos decorar:**

```python
import time

def soma_numeros(a: int, b: int) -> int:
    """
    Esta é uma função muito importante.
    Ela soma dois números inteiros e retorna o resultado.
    """
    print(f"-> Executando a lógica de 'soma_numeros'...")
    time.sleep(1) # Simula um trabalho demorado
    return a + b
```

Esta função tem "metadados" importantes:

  * Seu nome: `soma_numeros` (acessível via `soma_numeros.__name__`)
  * Sua docstring: "Esta é uma função muito importante..." (acessível via `soma_numeros.__doc__`)
  * Suas anotações de tipo: `{'a': <class 'int'>, ...}` (acessível via `soma_numeros.__annotations__`)

**Agora, vamos criar um decorator SEM `functools.wraps`:**

```python
# VERSÃO PROBLEMÁTICA (sem @wraps)

def decorator_timer(func):
    # 'func' aqui é a 'soma_numeros' original
    
    def wrapper_interno(*args, **kwargs):
        """Eu sou a docstring do wrapper!"""
        
        print(f"--- [TIMER] Iniciando execução de '{func.__name__}' ---")
        inicio = time.time()
        
        resultado = func(*args, **kwargs) # Chama a função original
        
        fim = time.time()
        print(f"--- [TIMER] '{func.__name__}' levou {fim - inicio:.4f}s ---")
        return resultado

    # O decorator retorna a função "wrapper"
    return wrapper_interno
```

**Vamos aplicar este decorator e ver o problema:**

```python
@decorator_timer
def soma_decorada_ruim(a: int, b: int) -> int:
    """
    Esta é uma função muito importante.
    Ela soma dois números inteiros e retorna o resultado.
    """
    print(f"-> Executando a lógica de 'soma_decorada_ruim'...")
    time.sleep(1) # Simula um trabalho demorado
    return a + b

print("--- Chamando a função decorada ---")
soma_decorada_ruim(10, 20)

print("\n--- PROBLEMA: Inspecionando os metadados ---")
print(f"Nome da função: {soma_decorada_ruim.__name__}")
print(f"Docstring: {soma_decorada_ruim.__doc__}")
print(f"Anotações: {soma_decorada_ruim.__annotations__}")
```

**Saída do Código Acima:**

```
--- Chamando a função decorada ---
--- [TIMER] Iniciando execução de 'soma_decorada_ruim' ---
-> Executando a lógica de 'soma_decorada_ruim'...
--- [TIMER] 'soma_decorada_ruim' levou 1.0000s ---

--- PROBLEMA: Inspecionando os metadados ---
Nome da função: wrapper_interno
Docstring: Eu sou a docstring do wrapper!
Anotações: {}
```

**Análise do Problema:**
Como o decorator substituiu `soma_decorada_ruim` pela função `wrapper_interno`, todos os metadados originais foram perdidos\!

  * O nome (`__name__`) agora é `wrapper_interno`.
  * A docstring (`__doc__`) agora é a docstring do wrapper.
  * As anotações de tipo (`__annotations__`) desapareceram.

Isso é péssimo para depuração, documentação (a função `help()` pararia de funcionar) e ferramentas de introspecção.

-----

### 3\. A Solução: Usando `functools.wraps`

`functools.wraps` é, ele mesmo, um **decorator**\! Você o usa para decorar a sua função `wrapper_interno`.

Seu trabalho é copiar todos os metadados importantes (como `__name__`, `__doc__`, `__annotations__`, `__module__`) da função original (`func`) para a função wrapper.

**Vamos reescrever nosso decorator da forma correta:**

```python
import time
from functools import wraps # 1. Importar

# VERSÃO CORRETA (com @wraps)

def decorator_timer_correto(func):
    # 'func' é a função original que queremos decorar
    
    @wraps(func)  # 2. Aplicar @wraps, passando a função original
    def wrapper_interno(*args, **kwargs):
        """Esta docstring será substituída pela original."""
        
        print(f"--- [TIMER] Iniciando execução de '{func.__name__}' ---")
        inicio = time.time()
        
        resultado = func(*args, **kwargs) 
        
        fim = time.time()
        print(f"--- [TIMER] '{func.__name__}' levou {fim - inicio:.4f}s ---")
        return resultado

    return wrapper_interno
```

**Agora, vamos aplicar o decorator correto e inspecionar:**

```python
@decorator_timer_correto
def soma_decorada_boa(a: int, b: int) -> int:
    """
    Esta é uma função muito importante.
    Ela soma dois números inteiros e retorna o resultado.
    """
    print(f"-> Executando a lógica de 'soma_decorada_boa'...")
    time.sleep(1) 
    return a + b

print("--- Chamando a função decorada ---")
soma_decorada_boa(10, 20)

print("\n--- SOLUÇÃO: Inspecionando os metadados ---")
print(f"Nome da função: {soma_decorada_boa.__name__}")
print(f"Docstring: {soma_decorada_boa.__doc__}")
print(f"Anotações: {soma_decorada_boa.__annotations__}")
```

**Saída Desta Vez:**

```
--- Chamando a função decorada ---
--- [TIMER] Iniciando execução de 'soma_decorada_boa' ---
-> Executando a lógica de 'soma_decorada_boa'...
--- [TIMER] 'soma_decorada_boa' levou 1.0000s ---

--- SOLUÇÃO: Inspecionando os metadados ---
Nome da função: soma_decorada_boa
Docstring: 
    Esta é uma função muito importante.
    Ela soma dois números inteiros e retorna o resultado.
    
Anotações: {'a': <class 'int'>, 'b': <class 'int'>, 'return': <class 'int'>}
```

**Perfeito\!** Todos os metadados originais foram preservados.

-----

### 4\. Raciocínio Lógico e Detalhes da Implementação

1.  **O que é `wraps`?** É uma função que retorna um decorator. Quando você faz `@wraps(func)`, você está, na verdade, chamando a função `wraps` que retorna um decorator interno, que por sua vez é aplicado em `wrapper_interno`.
2.  **O que ele faz?** O decorator retornado por `wraps` executa `functools.update_wrapper(wrapper_interno, func)`.
3.  **`update_wrapper`:** Esta é a função que faz o trabalho pesado. Ela copia os seguintes atributos da `func` (original) para a `wrapper_interno` (o wrapper):
      * `__module__`
      * `__name__`
      * `__qualname__`
      * `__doc__`
      * `__annotations__`
4.  **Bônus: O Atributo `__wrapped__`:** Além de copiar os metadados, `functools.wraps` adiciona um atributo especial à função decorada: `__wrapped__`. Ele aponta diretamente para a função original, "desembrulhada".

<!-- end list -->

```python
# Podemos acessar a função original "soma_decorada_boa"
# sem o decorator, se precisarmos:

funcao_original = soma_decorada_boa.__wrapped__

print("\n--- Acessando a função original via __wrapped__ ---")
# Note que isso NÃO imprimirá as linhas do [TIMER]
print(funcao_original(5, 5))
```

### 5\. Resumo e Boas Práticas

**Regra de Ouro:** Ao escrever qualquer decorator, **sempre** use `@functools.wraps` na sua função `wrapper` interna.

Isso garante que sua função decorada mantenha sua "identidade" (seus metadados). Isso é fundamental para:

  * **Depuração (Debugging):** Depuradores saberão o nome correto e o arquivo de origem da função.
  * **Documentação (Documentation):** A função `help()` e ferramentas como Sphinx (para gerar documentação) conseguirão extrair a docstring original.
  * **Introspecção (Introspection):** Outras partes do código (e outras bibliotecas) que verificam os metadados da função (como `pytest` ou `mypy`) funcionarão corretamente.

`functools.wraps` é a ponte que torna os decorators uma ferramenta poderosa e "higiênica", que não "suja" o código que ela decora.