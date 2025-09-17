# Linguagem Python 🐍

# Oque é o Python?

Python é uma linguagem de programação de alto nível, interpretada e de propósito geral, conhecida por sua simplicidade e legibilidade. Desenvolvida por Guido van Rossum e lançada pela primeira vez em 1991, Python suporta múltiplos paradigmas de programação, incluindo procedural, orientado a objetos e funcional. É amplamente utilizada em diversos campos, como desenvolvimento web, análise de dados, inteligência artificial, ciência de dados, automação, entre outros.

A linguagem é projetada para ser fácil de entender e escrever, com uma sintaxe clara que enfatiza a legibilidade. Isso reduz o custo de manutenção do código e permite que os programadores expressem conceitos complexos de forma concisa. Python vem com uma biblioteca padrão extensa que fornece ferramentas e módulos prontos para uso que facilitam a realização de uma vasta gama de tarefas. Além disso, a comunidade Python é muito ativa e oferece um grande número de pacotes adicionais para estender ainda mais as capacidades da linguagem.

# Criando Ambiente de Desenvolvimento

## Ambiente Linux

Instalar Python em um sistema Linux é geralmente um processo simples, pois muitas distribuições já vêm com Python instalado. No entanto, se você precisa instalar uma versão específica ou quer garantir que tem o ambiente configurado adequadamente, aqui estão os passos gerais que você pode seguir:

### 1. Verificar a versão instalada

Primeiro, verifique se o Python já está instalado e qual versão está disponível no seu sistema:

```bash
python --version
# ou para Python 3
python3 --version
```

### 2. Instalar Python

Se o Python não estiver instalado ou você precisar de uma versão diferente, você pode instalar usando o gerenciador de pacotes da sua distribuição. Por exemplo, para distribuições baseadas em Debian (como Ubuntu), você pode usar:

```bash
sudo apt update
sudo apt install python3
```

Para distribuições baseadas em Fedora:

```bash
sudo dnf install python3
```

### 3. Instalar o pip (gerenciador de pacotes Python)

O `pip` é o gerenciador de pacotes Python e é essencial para instalar e gerenciar bibliotecas e pacotes Python que não estão incluídos na biblioteca padrão. Para instalá-lo:

```bash
sudo apt install python3-pip  # Para Debian/Ubuntu
# ou
sudo dnf install python3-pip  # Para Fedora

```

### 4. Configurar um ambiente virtual

É uma boa prática usar ambientes virtuais para gerenciar dependências para diferentes projetos. Para instalar o pacote que permite criar ambientes virtuais:

```bash
python3 -m pip install --user virtualenv
```

Para criar um ambiente virtual:

```bash
python3 -m virtualenv nome_do_ambiente

```

Para ativar o ambiente virtual:

```bash
source nome_do_ambiente/bin/activate

```

### 5. Instalar bibliotecas adicionais

Com o ambiente virtual ativado, você pode instalar as bibliotecas necessárias usando o `pip`. Por exemplo, para instalar a biblioteca `requests`:

```bash
pip install requests

```

### 6. Manter o Python atualizado

Para atualizar o Python e o pip para as últimas versões disponíveis:

```bash
sudo apt upgrade python3  # Para Debian/Ubuntu
# ou
sudo dnf upgrade python3  # Para Fedora

# Atualizar pip
pip install --upgrade pip

```

Esses são os passos básicos para configurar um ambiente Python funcional em um sistema Linux. Adaptá-los de acordo com a distribuição específica e as necessidades do seu projeto pode ser necessário.

## Ambiente Windows

Entre no site do Python e instale na sua máquina o arquivo global do Python:

[Python Releases for Windows](https://www.python.org/downloads/windows/)

Link Dowload Python

Entre no site do Pycharm e baixe a IDE do Python

[Download PyCharm: Python IDE for Professional Developers by JetBrains](https://www.jetbrains.com/pycharm/download/#section=windows)

Link Pycharm

[[Python Básico]]