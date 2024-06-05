### SELECT
O comando `SELECT` é usado para recuperar dados de um banco de dados. Aqui está um exemplo simples:

```sql
SELECT * FROM employees;
```

Este comando seleciona todos os dados da tabela `employees`.

### FROM
O comando `FROM` especifica as tabelas das quais você deseja selecionar dados. Por exemplo:

```sql
SELECT * FROM employees
```

Aqui, `employees` é a tabela da qual estamos selecionando dados.

### WHERE
A cláusula `WHERE` é usada para filtrar registros com base em uma condição específica. Por exemplo:

```sql
SELECT * FROM employees WHERE department = 'IT';
```

Este comando seleciona todos os funcionários que pertencem ao departamento de TI.

### ORDER BY
A cláusula `ORDER BY` é usada para classificar os resultados da consulta em uma ordem específica. Por exemplo:

```sql
SELECT * FROM employees ORDER BY salary DESC;
```

Este comando seleciona todos os funcionários e os ordena por salário em ordem decrescente.

### GROUP BY
A cláusula `GROUP BY` é usada para agrupar registros com base nos valores de uma ou mais colunas. Por exemplo:

```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

Este comando conta o número de funcionários em cada departamento.

### HAVING
A cláusula `HAVING` é usada para filtrar grupos de registros retornados pela cláusula `GROUP BY`. Por exemplo:

```sql
SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;
```

Este comando seleciona apenas os departamentos com mais de 5 funcionários.

### JOINS
Os `JOINS` são usados para combinar dados de duas ou mais tabelas em um único resultado. Por exemplo:

```sql
SELECT employees.name, departments.name 
FROM employees 
JOIN departments ON employees.department_id = departments.id;
```

Este comando combina dados das tabelas `employees` e `departments` com base na correspondência dos IDs de departamento.

### INSERT
O comando `INSERT` é usado para adicionar novos registros a uma tabela existente. Por exemplo:

```sql
INSERT INTO employees (name, department, salary) VALUES ('John Doe', 'IT', 50000);
```

Este comando insere um novo funcionário na tabela `employees` com nome, departamento e salário especificados.

### UPDATE
O comando `UPDATE` é usado para modificar registros existentes em uma tabela. Por exemplo:

```sql
UPDATE employees SET salary = 55000 WHERE name = 'John Doe';
```

Este comando atualiza o salário do funcionário chamado 'John Doe' para 55000.

### DELETE
O comando `DELETE` é usado para remover registros de uma tabela. Por exemplo:

```sql
DELETE FROM employees WHERE name = 'John Doe';
```

Este comando exclui o funcionário chamado 'John Doe' da tabela `employees`.

