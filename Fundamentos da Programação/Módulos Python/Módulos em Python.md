### Trabalhando com módulos em Python

Em Python, “módulo” é qualquer arquivo `.py` que contém código (funções, classes, variáveis). Organizar seu código em módulos e pacotes melhora a reutilização, a legibilidade e os testes.

#### Conceitos-chave

- Módulo: arquivo `arquivo.py`.
- Pacote: diretório com código Python. Desde Python 3.3, não é obrigatório ter `__init__.py`, mas é recomendado para controle explícito.
- Import: mecanismo para carregar nomes de um módulo/pacote para o seu namespace.

---

### Criando e importando módulos

Suponha um arquivo `util.py`:

# util.py
```python

PI = 3.14159

def area_circulo(r): 
return PI * (r ** 2)

Usando em outro arquivo:

# app.py
```python
import util

print(util.PI) 
print(util.area_circulo(3))
```
Outras formas de import: from util import area_circulo, PI # importa nomes específicos from util import * # importa tudo (evite em produção) import util as u # alias from math import sqrt as raiz

Boas práticas:

- Prefira `import modulo` ou `from modulo import nome`.
- Evite `from modulo import *` (polui namespace, dificulta leitura).

---

### Estrutura de pacotes

Exemplo:

```
meu_projeto/
  app.py
  utils/
    __init__.py
    texto.py
    numerico.py
```

- `__init__.py` torna o diretório um pacote e pode expor uma API:
    
    ```python
    # utils/__init__.py
    from .texto import slugify
    from .numerico import media
    __all__ = ["slugify", "media"]  # controla import *
    ```
    
- Importando:
    
    ```python
    import utils
    from utils import slugify
    from utils.numerico import media
    ```
    
- Imports relativos (dentro do pacote):
    
    ```python
    # utils/texto.py
    from .numerico import media       # relativo ao mesmo pacote
    from ..outro_pacote import algo   # sobe um nível (evite excesso)
    ```
    

Use import relativo apenas dentro do próprio pacote. Em scripts de topo (executados diretamente), prefira import absoluto.

---

### O que acontece durante o import

1. O Python busca o módulo no `sys.meta_path` e no `sys.path` (lista de diretórios a procurar).
2. Compila e executa o arquivo do módulo uma única vez, gerando um objeto módulo.
3. Cacheia em `sys.modules`.

Implicações:

- Código no topo do módulo roda na importação.
- Importar novamente não executa de novo, a menos que use `importlib.reload`.

Ver caminhos de busca:

```python
import sys
print(sys.path)
```

Adicionar caminho (temporário, não recomendado para produção):

```python
import sys
sys.path.append("/caminho/para/modulos")
```

Em projetos, use pacotes instaláveis e ambientes virtuais ao invés de mexer no `sys.path`.

---

### Guardião de execução: if **name** == "**main**"

Dentro de um módulo, você pode incluir um bloco para rodar apenas quando o arquivo for executado diretamente:

```python
def main():
    print("rodando como script")

if __name__ == "__main__":
    main()
```

- Ao rodar `python arquivo.py`, `__name__` será `"__main__"`.
- Ao importar `arquivo`, esse bloco não executa.

---

### Módulos padrão, de terceiros e seus próprios

- Padrão (stdlib): `os`, `sys`, `math`, `pathlib`, `json`, `datetime`, `re`, etc.
    
- Terceiros: instale com `pip` em um ambiente virtual (venv/conda).
    
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # Windows: .venv\Scripts\activate
    pip install requests
    ```
    
    E então:
    
    ```python
    import requests
    ```
    
- Seus módulos: organize em pacotes e, se quiser instalar localmente durante o dev, use:
    
    - `pip install -e .` com um `pyproject.toml` configurado.

---

### pyproject.toml (empacotando seu pacote)

Exemplo simples com Hatchling:

```toml
[build-system]
requires = ["hatchling>=1.18"]
build-backend = "hatchling.build"

[project]
name = "meu-pacote"
version = "0.1.0"
description = "Exemplo de pacote"
readme = "README.md"
requires-python = ">=3.10"
dependencies = []

[project.urls]
homepage = "https://exemplo.com"
```

Instalação em modo editável:

```bash
pip install -e .
```

Então o pacote pode ser importado de qualquer lugar do ambiente.

---

### Convenções e organização

- Uma função/ideia por módulo quando fizer sentido; agrupe por domínio.
- Nomes de módulos e pacotes em minúsculas, com underscore se necessário: `data_loader.py`, `text_utils`.
- Evite efeitos colaterais ao importar (não rode tarefas pesadas no topo do módulo).
- Exporte uma API clara no `__init__.py` quando construir pacotes.

---

### Recarregar um módulo em tempo de execução

Útil em REPL:

```python
import importlib, meu_modulo
importlib.reload(meu_modulo)
```

---

### Inspeção e ajuda

```python
import math
dir(math)          # lista de nomes
help(math.sin)     # docstring
math.__file__      # caminho do arquivo (quando aplicável)
```

---

### Evitando importações circulares

Import circular ocorre quando `a.py` importa `b.py` e `b.py` importa `a.py`. Sintomas: AttributeError durante import, nomes ausentes.

Soluções:

- Reestruture: mova funções comuns para um terceiro módulo.
- Atrasar import dentro da função:
    
    ```python
    def usar_b():
        from . import b
        return b.func()
    ```
    
- Use interfaces mais estáveis e APIs no `__init__.py` para reduzir dependências cruzadas.

---

### Exemplo completo

Estrutura:

```
calc/
  __init__.py
  basico.py
  avancado.py
app.py
```

`calc/basico.py`:

```python
def soma(a, b): return a + b
def sub(a, b): return a - b
```

`calc/avancado.py`:

```python
from .basico import soma

def media(valores):
    if not valores:
        raise ValueError("lista vazia")
    return soma(*divmod(sum(valores), len(valores)))  # apenas ilustrativo
```

`calc/__init__.py`:

```python
from .basico import soma, sub
from .avancado import media
__all__ = ["soma", "sub", "media"]
```

`app.py`:

```python
from calc import soma, media

print(soma(2, 3))
print(media([1, 2, 3, 4]))
```

---

### Erros comuns

- ModuleNotFoundError: pacote não instalado ou caminho não no `sys.path`.
- ImportError: nome não exportado pelo módulo/pacote.
- Efeitos colaterais no import: código executado no topo causa lentidão ou falhas.
- Imports circulares: dependências cruzadas sem organização.

---

Se quiser, posso:

- Montar a estrutura de pastas do seu projeto.
- Criar um `pyproject.toml` pronto para você instalar com `pip install -e .`.
- Ajudar a resolver um erro específico de import no seu código.