Closures em Python são uma técnica útil para armazenar funções com um ambiente associado que contém as variáveis locais que foram no escopo quando a função foi criada. São utilizados principalmente para evitar o uso de variáveis globais e para criar objetos que mantêm um estado oculto.

### Como Funcionam as Closures em Python

Uma closure ocorre quando uma função aninhada (função definida dentro de outra função) referencia uma variável do escopo da função pai. Isso permite que a função interna acesse essas variáveis mesmo após a execução da função externa ter sido concluída.

### Exemplo de Closure em Python

Aqui está um exemplo simples que demonstra o uso de uma closure em Python:

```python
def make_multiplier_of(n):
    def multiplier(x):
        return x * n
    return multiplier

# Cria uma closure que multiplica um número por 3
times_three = make_multiplier_of(3)

# Cria outra closure que multiplica um número por 5
times_five = make_multiplier_of(5)

# Testando as closures
print(times_three(9))  # Deve retornar 27
print(times_five(3))   # Deve retornar 15

```

### Análise do Exemplo

1. **Definição da Função Pai**: `make_multiplier_of(n)` é a função externa que recebe um parâmetro `n`.
2. **Definição da Função Aninhada**: `multiplier(x)` é a função interna que usa o valor `n` definido na função pai. Esta função é o que chamamos de closure, pois captura o valor de `n` do escopo pai.
3. **Retorno da Função Aninhada**: A função `make_multiplier_of` retorna `multiplier`, a função aninhada.
4. **Uso da Closure**: Ao chamar `make_multiplier_of(3)`, o valor `3` é fixado na closure `times_three`. Similarmente, `times_five` fixa o valor `5`. Cada closure mantém seu próprio estado independente.

### Por Que Usar Closures?

Closures podem ser particularmente úteis em situações onde você quer:

- Reduzir o uso de variáveis globais, mantendo o estado necessário dentro de um escopo limitado.
- Implementar um comportamento que dependa de algum estado privado que não deve ser acessado diretamente fora da função.
- Proporcionar uma forma de implementação de "callbacks" ou funções de retorno que mantenham informações de estado entre chamadas.

Essencialmente, closures fornecem uma maneira poderosa de vincular dados a uma função que opera sobre esses dados, mantendo a integridade e a privacidade do escopo de dados.