Vamos criar um estudo completo sobre funções avançadas em SQL, separando-as em categorias: funções numéricas, funções de string, funções condicionais e funções de data e tempo. Cada seção incluirá explicações e exemplos.

## Funções Avançadas em SQL

### Funções Numéricas

As funções numéricas em SQL são usadas para realizar operações matemáticas em dados numéricos.

#### Exemplos de Funções Numéricas

1. **ABS()**
   - **Descrição**: Retorna o valor absoluto de um número.
   - **Sintaxe**: `ABS(number)`
   - **Exemplo**:

     ```sql
     SELECT ABS(-15) AS AbsoluteValue;
     ```

2. **CEIL() / CEILING()**
   - **Descrição**: Retorna o menor número inteiro maior ou igual ao número especificado.
   - **Sintaxe**: `CEIL(number)` ou `CEILING(number)`
   - **Exemplo**:

     ```sql
     SELECT CEIL(4.2) AS CeilValue;
     ```

3. **FLOOR()**
   - **Descrição**: Retorna o maior número inteiro menor ou igual ao número especificado.
   - **Sintaxe**: `FLOOR(number)`
   - **Exemplo**:

     ```sql
     SELECT FLOOR(4.8) AS FloorValue;
     ```

4. **ROUND()**
   - **Descrição**: Arredonda um número para um número especificado de casas decimais.
   - **Sintaxe**: `ROUND(number, decimal_places)`
   - **Exemplo**:

     ```sql
     SELECT ROUND(3.14159, 2) AS RoundedValue;
     ```

5. **POWER()**
   - **Descrição**: Retorna o valor de um número elevado a uma potência especificada.
   - **Sintaxe**: `POWER(base, exponent)`
   - **Exemplo**:

     ```sql
     SELECT POWER(2, 3) AS PowerValue;
     ```

