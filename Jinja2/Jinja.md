## 🧠 O que é o Jinja2

**Jinja2** é uma **engine de templates** para **Python**, desenvolvida por **Armin Ronacher** (mesmo criador do Flask).  
Ela permite **gerar texto dinâmico** (como HTML, XML, JSON, LaTeX, Markdown, etc.) a partir de **templates com placeholders e lógica embutida**.

👉 Em outras palavras, o Jinja2 separa a **lógica da aplicação** da **apresentação dos dados**, seguindo o princípio **MVC (Model-View-Controller)** ou **MVVM**.

---

## 🚀 Instalação

```bash
pip install Jinja2
```

Ou, se estiver usando Flask, ela já vem embutida.

---

## 🧩 Estrutura Básica de um Template Jinja2

Um arquivo de template (ex: `index.html`) pode conter:

```html
<!DOCTYPE html>
<html>
<head><title>{{ titulo }}</title></head>
<body>
  <h1>Olá, {{ usuario }}!</h1>
  {% if tarefas %}
    <ul>
      {% for tarefa in tarefas %}
        <li>{{ tarefa }}</li>
      {% endfor %}
    </ul>
  {% else %}
    <p>Sem tarefas hoje 🎉</p>
  {% endif %}
</body>
</html>
```

### Renderizando o template no Python:

```python
from jinja2 import Template

template = Template(open("index.html").read())

html_renderizado = template.render(
    titulo="Minha Página",
    usuario="Marcos",
    tarefas=["Estudar Java", "Treinar", "Ler"]
)

print(html_renderizado)
```

---

## 🧮 Sintaxe Essencial do Jinja2

|Tipo|Símbolo|Exemplo|
|---|---|---|
|**Variáveis**|`{{ ... }}`|`{{ nome }}`|
|**Blocos lógicos**|`{% ... %}`|`{% if condicao %} ... {% endif %}`|
|**Comentários**|`{# ... #}`|`{# Comentário não renderizado #}`|
|**Filtros**|`{{ var|filtro }}`|

---

## 🔧 Principais Filtros (transformações de variáveis)

| Filtro    | Exemplo         | Resultado                   |
| --------- | --------------- | --------------------------- |
| `upper`   | `{{ "marcos"    | upper }}`                   |
| `lower`   | `{{ "MARCO"     | lower }}`                   |
| `title`   | `{{ "ola mundo" | title }}`                   |
| `length`  | `{{ lista       | length }}`                  |
| `replace` | `{{ nome        | replace("a","@") }}`        |
| `join`    | `{{ lista       | join(", ") }}`              |
| `default` | `{{ valor       | default("desconhecido") }}` |

E você pode criar **filtros personalizados** no Python 👇

```python
from jinja2 import Environment

env = Environment()

def inverter(texto):
    return texto[::-1]

env.filters["reverse"] = inverter
```

---

## 🔄 Estruturas de Controle

### Condicionais

```jinja2
{% if idade >= 18 %}
  Você é maior de idade.
{% elif idade > 12 %}
  Adolescente.
{% else %}
  Criança.
{% endif %}
```

### Loops

```jinja2
<ul>
{% for item in lista %}
  <li>{{ loop.index }} - {{ item }}</li>
{% endfor %}
</ul>
```

🔹 `loop.index` → índice (1-based)  
🔹 `loop.revindex` → índice reverso  
🔹 `loop.first` → `True` se for o primeiro item  
🔹 `loop.last` → `True` se for o último

---

## 🏗️ Trabalhando com Templates e Includes

Você pode **reutilizar componentes** como cabeçalhos, rodapés e menus.

### Exemplo:

`base.html`

```html
<!DOCTYPE html>
<html>
<head>
  <title>{% block title %}Página{% endblock %}</title>
</head>
<body>
  {% block conteudo %}{% endblock %}
</body>
</html>
```

`index.html`

```html
{% extends "base.html" %}

{% block title %}Home{% endblock %}

{% block conteudo %}
  <h1>Bem-vindo, {{ usuario }}!</h1>
{% endblock %}
```

🔁 O `extends` cria **herança de templates**, assim como classes em OOP.  
Ideal para criar uma **estrutura base** de layout reutilizável.

---

## 🧱 Includes

Permite inserir partes externas (como componentes):

```html
{% include "navbar.html" %}
```

---

## 🧠 Macros (Funções de Template)

Permitem definir **componentes reutilizáveis**:

```jinja2
{% macro botao(texto, cor="blue") %}
  <button style="background-color: {{ cor }};">{{ texto }}</button>
{% endmacro %}

{{ botao("Salvar", "green") }}
{{ botao("Cancelar") }}
```

---

## 🧾 Ambientes e Loaders

Para renderizar múltiplos templates, o ideal é usar o **Environment** com **loaders**.

```python
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader("templates"))

template = env.get_template("index.html")
print(template.render(usuario="Marcos"))
```

### Outros tipos de loaders:

- `DictLoader` → carrega templates de um dicionário
    
- `PackageLoader` → carrega templates de um pacote Python
    
- `ChoiceLoader` → combina múltiplos loaders
    

---

## 🧨 Escapando HTML (Segurança)

Por padrão, o Jinja2 **escapa tags HTML** para evitar XSS:

```jinja2
{{ "<b>Oi</b>" }} → &lt;b&gt;Oi&lt;/b&gt;
```

Se quiser **permitir HTML**, use `|safe`:

```jinja2
{{ "<b>Oi</b>"|safe }} → <b>Oi</b>
```

---

## 🧮 Expressões e Filtros Avançados

```jinja2
{{ 5 + 10 }}
{{ "abc"|length }}
{{ "python"|replace("py","💡") }}
{{ (1,2,3)|sum }}
```

E você pode criar **expressões compostas**, inclusive com `in`, `not in`, etc.

---

## 🧰 Extensões e Customização

Jinja2 permite adicionar **extensões** para sintaxes personalizadas (como Markdown ou YAML).

Exemplo:

```python
env = Environment(extensions=["jinja2.ext.loopcontrols"])
```

Isso adiciona o suporte a:

```jinja2
{% for item in lista %}
  {% if item == "parar" %}
    {% break %}
  {% endif %}
{% endfor %}
```

---

## 🌍 Casos de Uso Comuns

|Contexto|Uso do Jinja2|
|---|---|
|**Flask**|Geração de páginas HTML dinâmicas (`render_template()`)|
|**Ansible**|Substituição de variáveis em arquivos YAML e scripts|
|**Projetos de Data Science**|Geração dinâmica de relatórios HTML/Markdown|
|**APIs e microserviços**|Montagem de payloads JSON dinâmicos|

---

## ⚡ Exemplo Completo

### Estrutura:

```
/meu_app/
 ├── templates/
 │    ├── base.html
 │    ├── index.html
 └── main.py
```

`base.html`

```html
<html>
  <head><title>{% block title %}{% endblock %}</title></head>
  <body>
    <header>Menu Principal</header>
    {% block conteudo %}{% endblock %}
    <footer>© 2025 Marcos</footer>
  </body>
</html>
```

`index.html`

```html
{% extends "base.html" %}
{% block title %}Página Inicial{% endblock %}
{% block conteudo %}
  <h2>Olá, {{ usuario }}!</h2>
  <p>Você tem {{ tarefas|length }} tarefas hoje.</p>
{% endblock %}
```

`main.py`

```python
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader("templates"))
template = env.get_template("index.html")

print(template.render(usuario="Marcos", tarefas=["Estudar", "Treinar"]))
```

---

## 📚 Conclusão

✅ **Jinja2** é extremamente poderoso e versátil:

- suporta **herança**, **macros**, **filtros**, **loops**, **condições**,
    
- é **rápido e seguro**,
    
- e **totalmente extensível**.
    

Ele é o **coração de vários frameworks Python**, e dominar o Jinja2 significa entender profundamente a **camada de apresentação** de sistemas web e scripts de automação.

---

Se quiser, posso te montar:

1. 🔹 Um **guia prático com exemplos avançados** (loops aninhados, macros complexas, filtros customizados, etc.), ou
    
2. 🔹 Um **mini-projeto Flask** que demonstra o uso do Jinja2 na prática.
    

Qual caminho você prefere seguir?