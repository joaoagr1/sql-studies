# Estudo Completo de Funções em SQL

## Introdução

Funções em SQL são blocos de código que realizam operações específicas e retornam um valor único. Elas são úteis para encapsular lógica de negócios e cálculos que precisam ser reutilizados em várias partes de um banco de dados. As funções podem ser usadas em consultas SQL, procedimentos armazenados e outras funções, tornando-as ferramentas poderosas para desenvolvedores de banco de dados.

## Tipos de Funções

### Funções Escalares

As funções escalares retornam um valor único, que pode ser de qualquer tipo de dado suportado pelo SQL, como INTEGER, VARCHAR, DATE, etc. Elas podem ser usadas em qualquer lugar em uma consulta SQL onde um valor único é esperado, como em cláusulas `SELECT`, `WHERE`, `HAVING`, etc.

### Funções de Agregação

As funções de agregação operam em um conjunto de valores e retornam um único valor. Exemplos comuns incluem `SUM`, `AVG`, `COUNT`, `MIN` e `MAX`. Embora geralmente sejam funções embutidas fornecidas pelo SQL, é possível criar funções de agregação personalizadas em alguns sistemas de banco de dados.

### Funções de Tabela

As funções de tabela retornam um conjunto de resultados, ou seja, uma tabela. Elas podem ser usadas em cláusulas `FROM` como se fossem uma tabela real.

## Criando Funções

### Sintaxe Básica

A sintaxe para criar uma função varia ligeiramente entre diferentes sistemas de gerenciamento de banco de dados (SGBDs), mas a estrutura básica é similar. Aqui está a sintaxe básica para criar uma função em MySQL:

```sql
CREATE FUNCTION nome_da_funcao (parametro1 tipo1, parametro2 tipo2, ...)
RETURNS tipo_retorno
BEGIN
    -- corpo da função
    RETURN valor;
END;
```

### Exemplo de Função Escalar

Vamos criar uma função simples que calcula o desconto de um preço baseado em uma taxa de desconto fornecida:

```sql
CREATE FUNCTION CalculaDesconto (preco DECIMAL(10, 2), taxa_desconto DECIMAL(5, 2))
RETURNS DECIMAL(10, 2)
BEGIN
    RETURN preco - (preco * taxa_desconto / 100);
END;
```

### Chamando a Função

Você pode chamar a função em uma consulta SQL como qualquer outra função:

```sql
SELECT CalculaDesconto(100, 10) AS preco_com_desconto;
```

## Parâmetros de Função

### Parâmetros de Entrada

Parâmetros de entrada são usados para passar valores para a função. No exemplo acima, `preco` e `taxa_desconto` são parâmetros de entrada.

### Parâmetros de Saída

Ao contrário das stored procedures, as funções em SQL geralmente não suportam parâmetros de saída diretamente. Em vez disso, elas retornam um único valor como resultado da função.

## Funções em Diferentes SGBDs

### MySQL

Em MySQL, a criação e uso de funções seguem a estrutura básica descrita anteriormente. MySQL oferece suporte para muitas funções embutidas e permite a criação de funções personalizadas.

### PostgreSQL

Em PostgreSQL, a sintaxe é ligeiramente diferente e oferece mais flexibilidade com suporte a linguagens procedurais como PL/pgSQL.

```sql
CREATE FUNCTION CalculaDesconto(preco NUMERIC, taxa_desconto NUMERIC)
RETURNS NUMERIC AS $$
BEGIN
    RETURN preco - (preco * taxa_desconto / 100);
END;
$$ LANGUAGE plpgsql;
```

### SQL Server

No SQL Server, a sintaxe é similar, mas com algumas diferenças em termos de tipos de dados e características específicas.

```sql
CREATE FUNCTION dbo.CalculaDesconto (@preco DECIMAL(10, 2), @taxa_desconto DECIMAL(5, 2))
RETURNS DECIMAL(10, 2)
AS
BEGIN
    RETURN @preco - (@preco * @taxa_desconto / 100);
END;
```

## Funções de Tabela

### Definição

Funções de tabela retornam um conjunto de resultados e podem ser usadas em consultas como se fossem tabelas reais. Existem dois tipos principais de funções de tabela:

- **Inline Table-Valued Functions:** Similares a views parametrizadas, retornam um único `SELECT`.
- **Multi-Statement Table-Valued Functions:** Permitem múltiplas instruções e manipulação de dados antes de retornar o resultado.

### Exemplo de Inline Table-Valued Function em SQL Server

```sql
CREATE FUNCTION dbo.GetOrdersByCustomer (@CustomerID INT)
RETURNS TABLE
AS
RETURN
(
    SELECT OrderID, OrderDate, TotalAmount
    FROM Orders
    WHERE CustomerID = @CustomerID
);
```

### Usando uma Inline Table-Valued Function

```sql
SELECT * FROM dbo.GetOrdersByCustomer(1);
```

### Exemplo de Multi-Statement Table-Valued Function em SQL Server

```sql
CREATE FUNCTION dbo.GetCustomerOrderSummary (@CustomerID INT)
RETURNS @OrderSummary TABLE (OrderID INT, OrderDate DATE, TotalAmount DECIMAL(10, 2))
AS
BEGIN
    INSERT INTO @OrderSummary
    SELECT OrderID, OrderDate, TotalAmount
    FROM Orders
    WHERE CustomerID = @CustomerID;

    RETURN;
END;
```

### Usando uma Multi-Statement Table-Valued Function

```sql
SELECT * FROM dbo.GetCustomerOrderSummary(1);
```

## Boas Práticas

1. **Modularização:** Divida a lógica complexa em funções menores e reutilizáveis.
2. **Documentação:** Documente suas funções com comentários para facilitar a manutenção.
3. **Performance:** Evite funções em linhas críticas de performance onde operações em lote seriam mais eficientes.
4. **Segurança:** Certifique-se de que suas funções não introduzem vulnerabilidades de segurança, como injeção de SQL.

## Conclusão

Funções em SQL são uma ferramenta poderosa para encapsular lógica de negócios e cálculos complexos dentro do banco de dados. Elas promovem a reutilização de código, melhoram a organização e a legibilidade do SQL, e podem melhorar a performance quando usadas corretamente. Entender como criar e utilizar funções em diferentes SGBDs é essencial para qualquer desenvolvedor de banco de dados.