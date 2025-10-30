O bloco `try/except` é o mecanismo de tratamento de exceções (erros em tempo de execução) em Python. Ele permite detectar erros sem quebrar o programa, responder de forma controlada e opcionalmente “limpar” recursos.

#### Por que usar?

- Evitar que o programa encerre ao ocorrer um erro.
- Tratar casos excepcionais (arquivos ausentes, conexão caída, input inválido).
- Separar o fluxo “feliz” do fluxo de erro.
- Registrar/logar problemas de forma consistente.

---

### Estrutura básica

try: # código que pode lançar exceção resultado = 10 / x except ZeroDivisionError: # tratamento quando a exceção específica ocorre print("Não é possível dividir por zero.")

- Código dentro de `try` é executado normalmente.
- Se ocorrer uma exceção que corresponda ao `except`, o fluxo salta para aquele bloco.
- Se nada der errado, o `except` é ignorado.

---

### Capturando múltiplas exceções

```python
try:
    x = int(input("Digite um número: "))
    print(10 / x)
except (ValueError, ZeroDivisionError) as e:
    print(f"Erro de entrada ou divisão: {e}")
```

- Você pode agrupar tipos diferentes de exceção em uma tupla.
- Usar `as e` captura o objeto da exceção para mensagem, log ou inspeção.

---

### Múltiplos excepts separados

```python
try:
    abrir_arquivo("dados.txt")
except FileNotFoundError:
    print("Arquivo não encontrado.")
except PermissionError:
    print("Sem permissão para ler o arquivo.")
```

- O primeiro `except` compatível é executado; os demais são ignorados.

---

### Capturando qualquer exceção

```python
try:
    faz_algo()
except Exception as e:
    print(f"Falhou: {e}")
```

- `Exception` cobre praticamente todas as exceções usuais.
- Use com parcimônia: capturar tudo pode mascarar bugs e dificultar depuração.
- Evite `except:` sem tipo (captura até `SystemExit`, `KeyboardInterrupt`), a menos que você saiba exatamente o que está fazendo.

---

### Bloco else

```python
try:
    resultado = operacao_risco()
except ErroEsperado as e:
    tratar(e)
else:
    usar(resultado)  # executa somente se não houve exceção
```

- `else` roda apenas quando o `try` não gerou exceção.
- Bom para separar o caminho de sucesso do tratamento de erro.

---

### Bloco finally

```python
arquivo = open("dados.txt", "w")
try:
    arquivo.write("oi")
finally:
    arquivo.close()  # sempre executa, com ou sem erro
```

- `finally` sempre é executado (com sucesso, com exceção tratada ou não).
- Útil para liberar recursos: fechar arquivos, conexões, locks.

Combinações comuns:

- try/except
- try/except/else
- try/finally
- try/except/finally
- try/except/else/finally

---

### Encadeamento e re-lançamento

```python
try:
    valida_dados(d)
except ValueError as e:
    raise ValueError(f"Dado inválido: {d}") from e
```

- `raise ... from e` preserva o encadeamento da causa (traceback mais claro).
- Você também pode apenas `raise` dentro de um `except` para repropagar a mesma exceção.

---

### Criar e lançar exceções

```python
class SaldoInsuficienteError(Exception):
    pass

def sacar(conta, valor):
    if valor > conta.saldo:
        raise SaldoInsuficienteError("Saldo insuficiente.")
```

- Crie exceções específicas para seu domínio (herde de `Exception`).
- Fornece semântica clara e tratamento preciso.

---

### Boas práticas

- Seja específico nos `except`: capture tipos concretos que você espera.
- Não engula exceções silenciosamente. Pelo menos logue:
    
    ```python
    import logging
    logging.exception("Falha ao processar pedido")  # preserva traceback
    ```
    
- Use `else` para código que depende do sucesso do `try`.
- Use `finally` (ou context managers) para liberar recursos.
- Prefira context managers (`with`) a `try/finally` quando possível.

---

### Context managers (with) vs try/finally

```python
# Em vez de:
arquivo = open("dados.txt")
try:
    dados = arquivo.read()
finally:
    arquivo.close()

# Use:
with open("dados.txt") as arquivo:
    dados = arquivo.read()
```

- `with` garante `__enter__/__exit__` e libera recursos automaticamente.
- Você ainda pode combinar com `try/except` dentro do bloco `with`.

---

### Escopo de variáveis e fluxo

- Se uma exceção ocorre dentro do `try` antes de uma variável ser atribuída, ela não existirá fora do `try`.
- O fluxo salta para o `except` correspondente; linhas restantes do `try` são ignoradas.
- Se nenhum `except` corresponder, a exceção “sobe” para o chamador.

---

### Hierarquia de exceções (visão rápida)

- `BaseException`
    - `Exception` ← capture normalmente a partir daqui
        - `ArithmeticError` → `ZeroDivisionError`, `OverflowError`
        - `LookupError` → `IndexError`, `KeyError`
        - `ValueError`, `TypeError`, `AttributeError`, `IOError`/`OSError`, `FileNotFoundError`, `TimeoutError`, etc.
    - `SystemExit`, `KeyboardInterrupt` ← evite capturar

Capturar um tipo base (ex.: `LookupError`) cobre seus filhos (`IndexError`, `KeyError`).

---

### Exemplos práticos

- Validação de input:

```python
while True:
    try:
        x = int(input("Número: "))
        break
    except ValueError:
        print("Digite um inteiro válido.")
```

- Acesso a dicionário com fallback:

```python
try:
    valor = d[chave]
except KeyError:
    valor = padrao
```

- Chamada de API com repetição e logs:

```python
import logging, time, requests

for tentativa in range(3):
    try:
        r = requests.get(url, timeout=3)
        r.raise_for_status()
        dados = r.json()
        break
    except (requests.Timeout, requests.HTTPError) as e:
        logging.warning(f"Tentativa {tentativa+1} falhou: {e}")
        time.sleep(1)
else:
    raise RuntimeError("API indisponível após 3 tentativas")
```

- Tratamento diferenciando erros:

```python
try:
    processar(pedido)
except ValidacaoError as e:
    return {"erro": "dados inválidos", "detalhe": str(e)}, 400
except IntegracaoError:
    return {"erro": "serviço externo indisponível"}, 503
```

---

### Anti-padrões comuns

- `except Exception: pass` (engole erro sem registrar).
- Capturar exceções muito genéricas cedo demais.
- Usar exceções para fluxo normal (quando um if basta).
- Lançar strings ou tipos não-Exception (em Python não é permitido; sempre use subclasses de `BaseException`).

---

### Depuração e testes

- Use `pytest.raises` para testar que uma função lança exceção:
    
    ```python
    import pytest
    with pytest.raises(ValueError):
        parse_int("abc")
    ```
    
- Logue com `logging.exception` ou `traceback.print_exc()` para entender a causa.

---

### Resumo mental

- try: onde pode dar errado
- except: como reagir a erros esperados
- else: o que fazer quando deu certo
- finally: o que fazer sempre (limpeza)
- Especifique exceções, não abuse de “pegar tudo”, e prefira context managers para recursos

Se quiser, posso adaptar esses exemplos ao seu caso específico (arquivo, rede, parsing, etc.).