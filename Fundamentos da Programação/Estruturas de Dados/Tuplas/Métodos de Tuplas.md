As tuplas em Python são bastante simples em termos de métodos disponíveis devido à sua natureza imutável. Elas oferecem apenas alguns métodos embutidos, o que as torna previsíveis e seguras para armazenar dados que não devem ser alterados após a criação. Aqui estão todos os métodos disponíveis para objetos do tipo tupla em Python:

### Métodos de Tuplas

1. **`count()`**: Este método retorna o número de vezes que um valor especificado aparece na tupla.
    
    ```python
    tupla = (1, 2, 3, 2, 4, 2)
    print(tupla.count(2))  # Saída: 3
    
    ```
    
2. **`index()`**: Retorna o índice da primeira ocorrência de um valor especificado. Se o valor não estiver presente, o método lança um `ValueError`.
    
    ```python
    tupla = (1, 2, 3, 2, 4, 2)
    print(tupla.index(3))  # Saída: 2
    # Usando index com parâmetros adicionais: index(value, start, end)
    print(tupla.index(2, 3))  # Saída: 3 (procura por 2 começando do índice 3)
    
    ```
    

Esses são os únicos métodos específicos para tuplas, e ambos estão relacionados à consulta de informações sobre os itens armazenados. A simplicidade dos métodos disponíveis reflete a filosofia de design da tupla de ser uma coleção imutável e eficiente para acesso a dados.

### Operações Comuns com Tuplas

Além desses métodos, você pode realizar várias operações com tuplas que são comuns a outros tipos de coleções em Python, como:

- **Concatenação**: Juntar duas ou mais tuplas para formar uma nova tupla.
    
    ```python
    tupla1 = (1, 2, 3)
    tupla2 = (4, 5, 6)
    print(tupla1 + tupla2)  # Saída: (1, 2, 3, 4, 5, 6)
    
    ```
    
- **Repetição**: Repetir os elementos de uma tupla um determinado número de vezes.
    
    ```python
    tupla = (1, 2, 3)
    print(tupla * 3)  # Saída: (1, 2, 3, 1, 2, 3, 1, 2, 3)
    
    ```
    
- **Indexação e fatiamento**: Acessar elementos específicos ou obter subconjuntos de uma tupla.
    
    ```python
    tupla = (1, 2, 3, 4, 5)
    print(tupla[1])   # Saída: 2
    print(tupla[1:4]) # Saída: (2, 3, 4)
    
    ```
    

Estas são as operações e métodos básicos para trabalhar com tuplas em Python. Embora as tuplas ofereçam um conjunto limitado de métodos, elas são extremamente úteis para casos de uso onde a imutabilidade é necessária para a integridade dos dados.