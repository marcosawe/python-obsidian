Em Python, não há um mecanismo embutido específico para definir constantes da mesma forma que outras linguagens como C ou Java possuem (usando palavras-chave como `const` ou `final`). No entanto, Python segue uma convenção para indicar que um valor deve ser tratado como constante: nomear a variável em letras maiúsculas, com sublinhados separando palavras se necessário.

### Convenções para Constantes

Aqui está como você geralmente declara constantes em Python:

```python
PI = 3.14159
GRAVITY = 9.81
MAX_USERS = 100
DATABASE_NAME = "production_db"

```

Essas constantes são apenas variáveis normais e podem tecnicamente ser alteradas, mas a convenção diz que elas não devem ser modificadas após sua inicialização. A comunidade Python segue essa convenção e espera que outras pessoas também a respeitem.

### Uso Prático de Constantes

As constantes são úteis em vários contextos, especialmente para definir valores que não devem mudar durante a execução de um programa. Aqui estão algumas situações comuns:

- Definições de configuração que permanecem constantes em todo o código, como URLs de API, senhas específicas de ambiente, etc.
- Valores científicos ou matemáticos que são invariantes, como o valor de Pi, a aceleração devido à gravidade, etc.
- Limites fixos usados para controle de loops, condições ou alocações de recursos, como o número máximo de usuários, o tamanho máximo de upload, etc.

### Módulos para Constantes

Para garantir uma maior imutabilidade e organizar constantes de maneira mais estruturada, você pode usar um módulo separado apenas para constantes em um projeto maior. Por exemplo:

```python
# constants.py
PI = 3.14159
GRAVITY = 9.81

```

E então em outro arquivo, você importaria essas constantes:

```python
from constants import PI, GRAVITY

def calcular_circunferencia(raio):
    return 2 * PI * raio

def calcular_peso(massa):
    return massa * GRAVITY

```

### Enforçando Imutabilidade

Embora o Python não ofereça suporte nativo para imutabilidade estrita de variáveis, você pode utilizar a biblioteca `const` de alguns frameworks ou definir suas próprias classes que lançam erros quando alguém tenta alterar uma "constante".

Um exemplo simplificado de uma classe de constante poderia ser:

```python
class Constant:
    def __init__(self, value):
        self._value = value

    def __get__(self, instance, owner):
        return self._value

    def __set__(self, instance, value):
        raise TypeError("Cannot modify a constant value")

class Constants:
    PI = Constant(3.14159)
    GRAVITY = Constant(9.81)

# Uso
c = Constants()
print(c.PI)  # 3.14159
c.PI = 3.14  # TypeError: Cannot modify a constant value

```

Essa abordagem garante que as "constantes" não possam ser modificadas, aproximando-se da funcionalidade de constantes reais em outras linguagens.