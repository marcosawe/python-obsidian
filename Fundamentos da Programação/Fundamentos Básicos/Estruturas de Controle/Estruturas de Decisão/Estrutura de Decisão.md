As estruturas de decisão em Python são blocos de código que permitem tomar decisões no programa. Isso é feito através da avaliação de uma ou mais condições que retornam `True` ou `False`. Dependendo do resultado dessa avaliação, diferentes partes do código podem ser executadas. As estruturas de decisão são fundamentais para controlar o fluxo de execução de programas, permitindo que comportamentos complexos sejam implementados de forma clara e lógica.

### Principais Estruturas de Decisão em Python

1. **`if`**:
    
    - A instrução `if` é a mais simples das estruturas de decisão. Ela avalia uma condição e, se essa condição for verdadeira (`True`), executa o bloco de código indentado que segue.
        
    - **Exemplo:**
        
        ```python
        idade = 18
        if idade >= 18:
            print("Você é maior de idade.")
        
        ```
        
2. **`else`**:
    
    - A instrução `else` é usada em conjunto com `if`. Ela especifica um bloco de código que é executado apenas se a condição testada pelo `if` for falsa (`False`).
        
    - **Exemplo:**
        
        ```python
        idade = 16
        if idade >= 18:
            print("Você é maior de idade.")
        else:
            print("Você é menor de idade.")
        
        ```
        
3. **`elif`** (else if):
    
    - A instrução `elif` permite encadear múltiplas verificações de condições, funcionando como um `if` adicional que só é considerado se todas as condições anteriores forem falsas. Pode haver vários `elif` após um `if`, e eles são avaliados na ordem em que aparecem.
        
    - **Exemplo:**
        
        ```python
        idade = 65
        if idade >= 18 and idade < 60:
            print("Você é um adulto.")
        elif idade >= 60:
            print("Você é idoso.")
        else:
            print("Você é menor de idade.")
        
        ```
        

### Estruturas de Decisão Aninhadas

- As estruturas de decisão podem ser aninhadas, ou seja, você pode ter um `if` dentro de outro `if`, `elif`, ou `else`. Isso permite a verificação de condições mais complexas e específicas.
    
- **Exemplo:**
    
    ```python
    idade = 17
    tem_permissao = True
    if idade >= 18:
        print("Você pode dirigir.")
    else:
        if tem_permissao:
            print("Você pode dirigir com permissão especial.")
        else:
            print("Você não pode dirigir.")
    
    ```
    

### Uso de Operadores Lógicos em Estruturas de Decisão

- Operadores lógicos como `and`, `or`, e `not` podem ser usados para combinar condições dentro das estruturas de decisão, aumentando a flexibilidade e poder dos testes condicionais.
    
- **Exemplo:**
    
    ```python
    idade = 25
    tem_carteira = False
    if idade >= 18 and tem_carteira:
        print("Você pode dirigir.")
    else:
        print("Você não pode dirigir.")
    
    ```
    
    ## Curto Circuito
    
    [[Curto Circuito]]
    
	 ---