### Funções de Data e Tempo
As funções de data e tempo em SQL são usadas para manipular e formatar valores de data e hora.

#### Exemplos de Funções de Data e Tempo

1. **NOW()**
   - **Descrição**: Retorna a data e hora atuais.
   - **Sintaxe**: `NOW()`
   - **Exemplo**:

     ```sql
     SELECT NOW() AS CurrentDateTime;
     ```

2. **CURDATE()**
   - **Descrição**: Retorna a data atual.
   - **Sintaxe**: `CURDATE()`
   - **Exemplo**:

     ```sql
     SELECT CURDATE() AS CurrentDate;
     ```

3. **DATE_ADD()**
   - **Descrição**: Adiciona um intervalo de tempo a uma data.
   - **Sintaxe**: `DATE_ADD(date, INTERVAL value unit)`
   - **Exemplo**:

     ```sql
     SELECT DATE_ADD('2024-01-01', INTERVAL 10 DAY) AS NewDate;
     ```

4. **DATEDIFF()**
   - **Descrição**: Calcula a diferença em dias entre duas datas.
   - **Sintaxe**: `DATEDIFF(date1, date2)`
   - **Exemplo**:

     ```sql
     SELECT DATEDIFF('2024-12-31', '2024-01-01') AS DateDifference;
     ```

5. **EXTRACT()**
   - **Descrição**: Extrai uma parte específica de uma data.
   - **Sintaxe**: `EXTRACT(unit FROM date)`
   - **Exemplo**:

     ```sql
     SELECT EXTRACT(YEAR FROM '2024-05-27') AS Year;
     ```

6. **FORMAT()**
   - **Descrição**: Formata uma data de acordo com um formato especificado.
   - **Sintaxe**: `FORMAT(date, format)`
   - **Exemplo**:

     ```sql
     SELECT DATE_FORMAT('2024-05-27', '%W, %M %d, %Y') AS FormattedDate;
     ```

Espero que este estudo completo sobre funções avançadas em SQL ajude a entender como utilizá-las de forma eficaz em suas consultas. Se precisar de mais informações ou exemplos, estou aqui para ajudar!