### 1\. O Contexto: Escopos em Python (A Regra LEGB)

Antes de tudo, precisamos entender como o Python procura por uma variável. Quando você usa um nome (como `minha_variavel`), o Python tenta encontrá-lo seguindo uma ordem específica, conhecida como a **Regra LEGB**:

1.  **L (Local):** O escopo mais interno. Se você está dentro de uma função, o Python primeiro procura se a variável foi definida ali.
2.  **E (Enclosing):** O escopo de funções "envolventes" ou "externas". Se uma função está definida dentro de outra função, o Python procura no escopo da função externa.
3.  **G (Global):** O escopo do módulo. Variáveis definidas no nível superior do seu arquivo `.py`.
4.  **B (Built-in):** O escopo final. Nomes pré-definidos no Python, como `print()`, `len()`, `str()`, etc.

Se o Python não encontra o nome em nenhuma dessas camadas, ele levanta um `NameError`.

Agora, vamos dissecar cada componente da sua pergunta.

-----

### 2\. As Funções `globals()` e `locals()`

Essas são funções *built-in* que nos dão um "instantâneo" dos nomes (variáveis, funções, classes) visíveis em um determinado escopo. Elas retornam dicionários.

#### `globals()`

A função `globals()` sempre retorna um dicionário representando o **escopo global** do módulo atual.

  * **O que é o escopo global?** É o "nível principal" do seu arquivo. Qualquer variável ou função que você define fora de qualquer classe ou função está no escopo global.
  * **Comportamento:** Este dicionário é "vivo". Se você modificar este dicionário (adicionando ou alterando uma chave), você está *realmente* modificando a variável global correspondente.

**Exemplo Prático com `globals()`:**

```python
# coding: utf-8

# 1. Definindo uma variável global
NIVEL_DO_JOGO = 1

def mostrar_nivel():
    # 2. Acessando a variável global (leitura)
    # Python não a encontra localmente (L), nem em escopos envolventes (E),
    # então a encontra no escopo Global (G).
    print(f"Nível atual (lido de dentro da função): {NIVEL_DO_JOGO}")

print("--- Antes da chamada ---")
mostrar_nivel()

# 3. Acessando o dicionário global
dicionario_global = globals()

print("\n--- Dicionário Global (parcial) ---")
# Vamos ver algumas chaves interessantes
print(f"Nossa variável: 'NIVEL_DO_JOGO': {dicionario_global['NIVEL_DO_JOGO']}")
print(f"Nossa função: 'mostrar_nivel': {dicionario_global['mostrar_nivel']}")
print(f"Nome do módulo: '__name__': {dicionario_global['__name__']}")

# 4. Modificando uma variável global USANDO a função globals()
# Esta é uma prática incomum, mas demonstra o conceito.
dicionario_global['NIVEL_DO_JOGO'] = 5

print("\n--- Após modificar via globals() ---")
mostrar_nivel()

# 5. A forma padrão de modificar uma variável global
# (Apenas para ilustração, evite isso dentro de funções sem a keyword 'global')
NIVEL_DO_JOGO = 10
print("\n--- Após modificar diretamente ---")
mostrar_nivel()
```

**Raciocínio Lógico:**
`globals()` nos dá um dicionário de todos os nomes que "pertencem" ao módulo. Isso é útil para *introspecção* (ver o que está definido) e, em casos raros (como metaprogramação), para modificar esse escopo dinamicamente.

-----

#### `locals()`

A função `locals()` retorna um dicionário representando o **escopo local** atual.

  * **Comportamento (Nível do Módulo):** Se você chamar `locals()` no nível global (fora de uma função), ela se comportará exatamente como `globals()`, retornando o dicionário do módulo.
  * **Comportamento (Dentro de uma Função):** É aqui que ela se torna interessante. Quando chamada dentro de uma função, `locals()` retorna um dicionário de todas as variáveis definidas *dentro* daquela função (argumentos e variáveis locais).
  * **Uma Pegadinha Crucial:** O Python faz otimizações. Ao contrário de `globals()`, o dicionário retornado por `locals()` dentro de uma função é, na prática, uma **cópia** para leitura. Tentar *modificar* variáveis locais alterando este dicionário **não funciona de forma confiável** (e não deve ser feito). Ele deve ser usado apenas para *inspeção*.

**Exemplo Prático com `locals()`:**

```python
# coding: utf-8

VARIAVEL_GLOBAL = "Eu sou global"

def calcular_bonus(salario_base, multiplicador):
    # 1. 'salario_base' e 'multiplicador' são argumentos, portanto, locais.
    imposto = 0.275  # 2. 'imposto' é uma variável local.
    
    # 3. Vamos inspecionar o escopo local
    nomes_locais = locals()
    
    print("\n--- Dicionário Local (dentro de calcular_bonus) ---")
    print(f"'salario_base': {nomes_locais['salario_base']}")
    print(f"'multiplicador': {nomes_locais['multiplicador']}")
    print(f"'imposto': {nomes_locais['imposto']}")
    
    # 4. 'nomes_locais' também está em si mesmo!
    print(f"A própria 'nomes_locais' existe localmente: {'nomes_locais' in nomes_locais}")
    
    # 5. 'VARIAVEL_GLOBAL' NÃO está no dicionário local
    print(f"'VARIAVEL_GLOBAL' está em locals()? {'VARIAVEL_GLOBAL' in nomes_locais}")

    # 6. TENTATIVA DE MODIFICAÇÃO (Não faça isso!)
    nomes_locais['imposto'] = 0.5  # Modificando o dicionário
    print(f"\nValor de 'imposto' após modificar locals(): {imposto}") # <--- Verá 0.275!
    
    bonus_bruto = salario_base * multiplicador
    bonus_liquido = bonus_bruto - (bonus_bruto * imposto)
    return bonus_liquido

print("--- Chamando a função ---")
bonus_final = calcular_bonus(5000, 1.5)

print(f"\nBonus Final Calculado: {bonus_final}")

print("\n--- Locals no Nível Global ---")
# No nível global, locals() é o mesmo que globals()
print(f"locals() is globals()? {locals() is globals()}") 
```

**Raciocínio Lógico:**
`locals()` nos dá um dicionário dos nomes no escopo mais imediato (a função atual). É primariamente uma ferramenta de *debug* e *introspecção* para ver o estado de uma função em um ponto específico.

-----

### 3\. Variáveis Livres (Free Variables) e Closures

Este é o cerne da questão e onde a regra **E (Enclosing)** entra em jogo.

Uma **Variável Livre** é uma variável que é *usada* em um escopo (como uma função interna), mas *não é definida* nesse escopo local, nem no escopo global. Ela é "livre" porque seu valor é "capturado" do escopo que a envolve (a função externa).

Isso nos leva ao conceito de **Closure** (Fechamento).

Um **Closure** é um objeto de função (a função interna) que "se lembra" do ambiente em que foi criada. Ela carrega consigo as referências às variáveis livres do escopo envolvente (a função externa), *mesmo depois que a função externa já terminou sua execução*.

**Exemplo Prático de Closure e Variável Livre:**

```python
# coding: utf-8

def criar_saudacao(saudacao_base):
    # 1. 'saudacao_base' é local para 'criar_saudacao'
    
    def saudar(nome):
        # 2. 'nome' é local para 'saudar'.
        # 3. 'saudacao_base' NÃO é local para 'saudar' e NÃO é global.
        #    Ela é uma VARIÁVEL LIVRE, capturada do escopo 'Enclosing'.
        print(f"{saudacao_base}, {nome}!")
    
    # 4. A função externa retorna a função interna (o closure)
    return saudar

# 5. Criamos duas instâncias do closure
bom_dia = criar_saudacao("Bom dia")
boa_noite = criar_saudacao("Boa noite")

# 6. A função 'criar_saudacao' JÁ TERMINOU SUA EXECUÇÃO.
#    Suas variáveis locais (como 'saudacao_base') deveriam ter desaparecido.

# 7. Mas os closures 'bom_dia' e 'boa_noite' "se lembram"
#    do valor que 'saudacao_base' tinha quando eles foram criados.

print("--- Executando os Closures ---")
bom_dia("Ana")
boa_noite("Carlos")

# 8. Podemos inspecionar o closure (apenas para fins educacionais)
#    '__closure__' armazena as variáveis livres capturadas.
print("\n--- Inspeção do Closure 'bom_dia' ---")
# É uma tupla de "células" que guardam as variáveis livres
print(f"Objeto de closure: {bom_dia.__closure__}")
print(f"Valor da variável livre: {bom_dia.__closure__[0].cell_contents}")
```

**Raciocínio Lógico:**
Quando `criar_saudacao` é executada, ela cria uma *nova* função `saudar` e um *novo* ambiente. A variável `saudacao_base` (do escopo `Enclosing`) é "capturada" por esta nova função `saudar`. O `return saudar` retorna essa função "empacotada" com seu ambiente. Isso é um closure.

-----

### 4\. A Palavra-Chave `nonlocal`

Aqui, juntamos tudo. Vimos que um closure pode *ler* uma variável livre. Mas o que acontece se tentarmos *modificar* (atribuir um novo valor) a essa variável?

**O Problema (Sem `nonlocal`):**

```python
# coding: utf-8

def contador_externo():
    contador = 0  # Esta é a variável do escopo 'Enclosing'
    
    def incrementar():
        # PROBLEMA: Ao fazer uma atribuição (contador = ...),
        # Python assume que 'contador' é uma NOVA variável LOCAL.
        # contador = contador + 1  # <--- Isso daria um UnboundLocalError
        
        # Versão mais sutil do problema:
        # Se 'contador' fosse uma lista (mutável), poderíamos fazer:
        # contador.append(1) # Isso funcionaria!
        
        # Mas para reatribuir o nome (inteiros, strings, etc.), falhamos.
        try:
            # Esta linha CRIA um 'contador' local e tenta ler
            # o 'contador' local antes de ser definido.
            contador = contador + 1
        except UnboundLocalError as e:
            print(f"Erro: {e}")
            
    incrementar()
    print(f"Valor final (externo): {contador}")

print("--- Tentativa de modificar (vai falhar) ---")
contador_externo()
```

Por padrão, se você atribui um valor a um nome dentro de uma função (`x = 5`), o Python *sempre* cria uma variável local, a menos que você diga o contrário. Isso "esconde" a variável do escopo envolvente.

**A Solução: `nonlocal`**

A palavra-chave `nonlocal` diz explicitamente ao Python: "O nome que estou usando aqui não é novo. Ele se refere à variável com este nome no **escopo envolvente (Enclosing) mais próximo**."

  * `nonlocal` se refere ao escopo **E (Enclosing)**.
  * `global` se refere ao escopo **G (Global)**.

**Exemplo Prático com `nonlocal` (A Forma Correta):**

```python
# coding: utf-8

def contador_externo_correto():
    contador = 0  # 1. Variável do escopo 'Enclosing'
    
    def incrementar():
        # 2. AVISO: Estamos nos referindo ao 'contador'
        #    do escopo 'Enclosing', não criando um novo.
        nonlocal contador 
        
        # 3. Agora esta modificação afeta a variável externa
        contador = contador + 1
        print(f"Valor interno (incrementado): {contador}")
        
    def decrementar():
        nonlocal contador
        contador = contador - 1
        print(f"Valor interno (decrementado): {contador}")

    # 4. Retornamos as funções que "fecham" (closure)
    #    sobre a variável 'contador'.
    return incrementar, decrementar

print("--- Usando o contador com 'nonlocal' ---")

# 1. 'contador' (valendo 0) é criado e capturado.
inc, dec = contador_externo_correto()

# 2. Cada chamada a 'inc' modifica o 'contador' capturado.
inc()
inc()
inc()

# 3. Cada chamada a 'dec' modifica o MESMO 'contador' capturado.
dec()
```

**Raciocínio Lógico:**
`nonlocal` é a ponte que permite a um closure não apenas *ler*, mas também *escrever* (reatribuir) em suas variáveis livres. Isso é fundamental para criar funções com "estado" (que lembram coisas entre chamadas), como vemos em decoradores que contam chamadas ou em fábricas de funções mais complexas.

### Resumo e Boas Práticas

1.  **`globals()`:** Retorna o dicionário do escopo do módulo. Útil para introspecção. Evite modificar diretamente.
2.  **`locals()`:** Retorna o dicionário do escopo local (da função). Útil *apenas* para *debug* e *leitura*. Não confie em modificá-lo.
3.  **Variável Livre:** Uma variável usada por uma função interna, mas definida em uma função externa (escopo *Enclosing*).
4.  **Closure:** Uma função interna que "carrega" as referências às suas variáveis livres, permitindo que ela acesse esses valores mesmo após a função externa ter retornado.
5.  **`nonlocal`:** A palavra-chave "mágica" que permite a um closure *modificar* (reatribuir) uma variável livre em seu escopo envolvente. Se você precisa que sua função interna mude o valor de `x = 10` para `x = 11` (e `x` está na função externa), você precisa de `nonlocal x`.