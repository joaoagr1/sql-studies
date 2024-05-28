# Stored Procedures em SQL

## O que são Stored Procedures?

Stored procedures (procedimentos armazenados) são conjuntos de comandos SQL que são armazenados no banco de dados. Elas permitem agrupar uma série de operações ou consultas em um único procedimento que pode ser executado de uma só vez, melhorando a eficiência e a reutilização do código.

## Por que usar Stored Procedures?

- **Performance:** Stored procedures são compiladas e armazenadas no banco de dados, o que pode melhorar a performance, especialmente em operações complexas.
- **Reutilização:** Código SQL pode ser reutilizado em diferentes partes de um aplicativo, facilitando a manutenção.
- **Segurança:** Permite controlar o acesso a dados e operações através de permissões específicas para os procedimentos armazenados.
- **Manutenção:** Simplifica a manutenção do código SQL, centralizando a lógica do banco de dados.
- **Transações:** Facilitam o gerenciamento de transações complexas.

## Como Criar Stored Procedures

A sintaxe para criar stored procedures pode variar entre diferentes sistemas de gerenciamento de banco de dados (SGBDs), como MySQL, SQL Server, PostgreSQL, Oracle, etc. Vamos ver exemplos em alguns dos SGBDs mais populares.

### MySQL

```sql
DELIMITER //

CREATE PROCEDURE GetCustomerOrders (IN customerID INT)
BEGIN
    SELECT * FROM Orders WHERE CustomerID = customerID;
END //

DELIMITER ;
```

### SQL Server

```sql
CREATE PROCEDURE GetCustomerOrders
    @CustomerID INT
AS
BEGIN
    SELECT * FROM Orders WHERE CustomerID = @CustomerID;
END
```

### PostgreSQL

```sql
CREATE OR REPLACE FUNCTION GetCustomerOrders(customerID INT)
RETURNS TABLE(OrderID INT, OrderDate DATE, Amount DECIMAL) AS $$
BEGIN
    RETURN QUERY
    SELECT OrderID, OrderDate, Amount
    FROM Orders
    WHERE CustomerID = customerID;
END;
$$ LANGUAGE plpgsql;
```

## Parâmetros de Entrada e Saída

Stored procedures podem ter parâmetros de entrada (IN), saída (OUT), ou ambos (INOUT).

### MySQL

#### Parâmetros de Entrada

```sql
DELIMITER //

CREATE PROCEDURE AddNewCustomer (IN customerName VARCHAR(100), IN contactName VARCHAR(100))
BEGIN
    INSERT INTO Customers (CustomerName, ContactName) VALUES (customerName, contactName);
END //

DELIMITER ;
```

#### Parâmetros de Saída

```sql
DELIMITER //

CREATE PROCEDURE GetTotalOrders (IN customerID INT, OUT totalOrders INT)
BEGIN
    SELECT COUNT(*) INTO totalOrders FROM Orders WHERE CustomerID = customerID;
END //

DELIMITER ;
```

### SQL Server

#### Parâmetros de Entrada

```sql
CREATE PROCEDURE AddNewCustomer
    @CustomerName NVARCHAR(100),
    @ContactName NVARCHAR(100)
AS
BEGIN
    INSERT INTO Customers (CustomerName, ContactName) VALUES (@CustomerName, @ContactName);
END
```

#### Parâmetros de Saída

```sql
CREATE PROCEDURE GetTotalOrders
    @CustomerID INT,
    @TotalOrders INT OUTPUT
AS
BEGIN
    SELECT @TotalOrders = COUNT(*) FROM Orders WHERE CustomerID = @CustomerID;
END
```

### PostgreSQL

#### Parâmetros de Entrada e Saída

```sql
CREATE OR REPLACE FUNCTION GetTotalOrders(customerID INT, OUT totalOrders INT) AS $$
BEGIN
    SELECT COUNT(*) INTO totalOrders FROM Orders WHERE CustomerID = customerID;
END;
$$ LANGUAGE plpgsql;
```

## Exemplos de Uso

### MySQL

#### Executando uma Stored Procedure com Parâmetro de Entrada

```sql
CALL GetCustomerOrders(1);
```

#### Executando uma Stored Procedure com Parâmetro de Saída

```sql
CALL GetTotalOrders(1, @totalOrders);
SELECT @totalOrders;
```

### SQL Server

#### Executando uma Stored Procedure com Parâmetro de Entrada

```sql
EXEC GetCustomerOrders @CustomerID = 1;
```

#### Executando uma Stored Procedure com Parâmetro de Saída

```sql
DECLARE @TotalOrders INT;
EXEC GetTotalOrders @CustomerID = 1, @TotalOrders = @TotalOrders OUTPUT;
SELECT @TotalOrders;
```

### PostgreSQL

#### Executando uma Stored Procedure

```sql
SELECT * FROM GetCustomerOrders(1);
```

#### Executando uma Function com Parâmetro de Saída

```sql
SELECT * FROM GetTotalOrders(1);
```

## Considerações Finais

Stored procedures são uma poderosa ferramenta para gerenciar operações complexas de banco de dados. Elas oferecem benefícios significativos em termos de desempenho, reutilização de código, segurança e manutenção. Cada SGBD tem suas próprias particularidades na definição e execução de stored procedures, portanto, é importante consultar a documentação específica do sistema que você está utilizando.