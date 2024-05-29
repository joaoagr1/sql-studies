## Subconsultas (Subqueries) em SQL

### O que é uma Subconsulta?

Em SQL, uma subconsulta é uma consulta embutida dentro de outra consulta SQL. Também pode ser chamada de consulta aninhada (nested query) ou consulta interna (inner query). A consulta que contém a subconsulta é frequentemente chamada de consulta externa (outer query). Subconsultas são utilizadas para recuperar dados que serão usados na consulta principal como uma condição para restringir ainda mais os dados a serem recuperados.

### Onde Usar Subconsultas?

Subconsultas podem ser usadas em várias partes de uma consulta SQL, incluindo:

- Declaração `SELECT`
- Cláusula `FROM`
- Cláusula `WHERE`
- Cláusula `GROUP BY`
- Cláusula `HAVING`

### Sintaxe Geral

Em geral, a sintaxe de uma subconsulta pode ser escrita como:

```sql
SELECT column_name [, column_name]
FROM table1 [, table2]
WHERE column_name OPERATOR
   (SELECT column_name [, column_name]
   FROM table1 [, table2]
   [WHERE]);
```

### Tipos de Subconsultas

#### Subconsulta Escalar (Scalar Subquery)

- **Descrição**: Retorna um único valor.
- **Exemplo**:

```sql
SELECT name 
FROM student 
WHERE roll_id = (SELECT roll_id FROM student WHERE name = 'John');
```

Neste exemplo, a subconsulta retorna o `roll_id` do estudante chamado 'John'. A consulta externa utiliza este valor para encontrar o nome do estudante com o mesmo `roll_id`.

#### Subconsulta de Linha (Row Subquery)

- **Descrição**: Retorna uma única linha ou múltiplas linhas com dois ou mais valores.
- **Exemplo**:

```sql
SELECT * FROM student 
WHERE (roll_id, age) = (SELECT MIN(roll_id), MIN(age) FROM student);
```

Aqui, a subconsulta retorna o menor `roll_id` e a menor `age` da tabela `student`. A consulta externa usa estes valores para encontrar o estudante correspondente.

#### Subconsulta de Coluna (Column Subquery)

- **Descrição**: Retorna valores de uma única coluna com múltiplas linhas.
- **Exemplo**:

```sql
SELECT name, age 
FROM student 
WHERE name IN (SELECT name FROM student);
```

A subconsulta retorna todos os nomes da tabela `student`. A consulta externa usa esses nomes para filtrar os registros.

#### Subconsulta de Tabela (Table Subquery)

- **Descrição**: Retorna mais de uma linha e mais de uma coluna.
- **Exemplo**:

```sql
SELECT name, age 
FROM student 
WHERE (name, age) IN (SELECT name, age FROM student);
```

A subconsulta retorna pares de `name` e `age` da tabela `student`. A consulta externa usa esses pares para filtrar os registros.

### Subconsultas Correlacionadas e Não Correlacionadas

- **Subconsulta Não Correlacionada (Uncorrelated Subquery)**: É uma subconsulta que pode ser executada de forma independente da consulta externa. Não depende de valores da consulta externa.
  - **Exemplo**:

  ```sql
  SELECT name 
  FROM student 
  WHERE roll_id = (SELECT MAX(roll_id) FROM student);
  ```

- **Subconsulta Correlacionada (Correlated Subquery)**: É uma subconsulta que usa valores da consulta externa. Não pode ser executada independentemente.
  - **Exemplo**:

  ```sql
  SELECT name 
  FROM student s1 
  WHERE age > (SELECT AVG(age) FROM student s2 WHERE s1.department_id = s2.department_id);
  ```

  Neste exemplo, a subconsulta utiliza `s1.department_id` da consulta externa `s1` para calcular a média das idades dos estudantes no mesmo departamento.

### Resumo dos Tipos de Subconsultas

- **Subconsulta Escalar**: Retorna um único valor.
- **Subconsulta de Coluna**: Retorna múltiplas linhas de uma única coluna.
- **Subconsulta de Linha**: Retorna uma ou mais linhas de múltiplas colunas.
- **Subconsulta de Tabela**: Retorna múltiplas linhas e colunas.
- **Subconsulta Aninhada (Nested Subquery)**: Qualquer subconsulta dentro de outra subconsulta.
- **Subconsulta Correlacionada**: Usa valores da consulta externa.

