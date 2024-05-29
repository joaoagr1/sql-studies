### Funções de String

As funções de string em SQL são usadas para manipular e formatar valores de texto.

#### Exemplos de Funções de String

1. **CONCAT()**
   - **Descrição**: Concatena duas ou mais strings.
   - **Sintaxe**: `CONCAT(string1, string2, ...)`
   - **Exemplo**:

     ```sql
     SELECT CONCAT('Hello', ' ', 'World') AS ConcatenatedString;
     ```

2. **LENGTH()**
   - **Descrição**: Retorna o comprimento de uma string.
   - **Sintaxe**: `LENGTH(string)`
   - **Exemplo**:

     ```sql
     SELECT LENGTH('Hello World') AS StringLength;
     ```

3. **UPPER()**
   - **Descrição**: Converte uma string para maiúsculas.
   - **Sintaxe**: `UPPER(string)`
   - **Exemplo**:

     ```sql
     SELECT UPPER('Hello World') AS UpperString;
     ```

4. **LOWER()**
   - **Descrição**: Converte uma string para minúsculas.
   - **Sintaxe**: `LOWER(string)`
   - **Exemplo**:

     ```sql
     SELECT LOWER('Hello World') AS LowerString;
     ```

5. **SUBSTRING()**
   - **Descrição**: Extrai uma parte de uma string.
   - **Sintaxe**: `SUBSTRING(string, start_position, length)`
   - **Exemplo**:

     ```sql
     SELECT SUBSTRING('Hello World', 1, 5) AS SubString;
     ```

6. **TRIM()**
   - **Descrição**: Remove espaços em branco do início e do fim de uma string.
   - **Sintaxe**: `TRIM(string)`
   - **Exemplo**:

     ```sql
     SELECT TRIM('  Hello World  ') AS TrimmedString;
     ```

### Funções Condicionais

As funções condicionais em SQL são usadas para executar lógica condicional em consultas.

#### Exemplos de Funções Condicionais

1. **CASE**
   - **Descrição**: Executa lógica condicional semelhante a uma estrutura `if-then-else`.
   - **Sintaxe**:

     ```sql
     CASE
         WHEN condition THEN result
         [WHEN condition THEN result ...]
         [ELSE result]
     END
     ```
   - **Exemplo**:

     ```sql
     SELECT
         product_name,
         CASE
             WHEN quantity > 10 THEN 'In Stock'
             WHEN quantity BETWEEN 1 AND 10 THEN 'Low Stock'
             ELSE 'Out of Stock'
         END AS StockStatus
     FROM products;
     ```

2. **COALESCE()**
   - **Descrição**: Retorna o primeiro valor não nulo em uma lista de argumentos.
   - **Sintaxe**: `COALESCE(value1, value2, ..., value_n)`
   - **Exemplo**:

     ```sql
     SELECT COALESCE(NULL, NULL, 'Hello', 'World') AS FirstNonNullValue;
     ```

3. **NULLIF()**
   - **Descrição**: Retorna `NULL` se dois valores forem iguais; caso contrário, retorna o primeiro valor.
   - **Sintaxe**: `NULLIF(value1, value2)`
   - **Exemplo**:

     ```sql
     SELECT NULLIF(5, 5) AS NullIfEqual;
     ```



