Vamos criar um estudo completo em Markdown abordando os conceitos de restrições (constraints) em bancos de dados, incluindo chaves primárias, chaves estrangeiras, únicas, `NOT NULL`, e `CHECK`.

## Restrições (Constraints) em Bancos de Dados

As restrições em um banco de dados garantem a integridade e a consistência dos dados armazenados. Elas são aplicadas a colunas individuais ou a combinações de colunas em uma tabela.

### Chave Primária (Primary Key)

#### Para que serve?
- Uma chave primária é uma coluna ou um conjunto de colunas que identifica de forma única cada linha em uma tabela.
- Garante que cada registro em uma tabela tenha uma identificação única.

#### Quando usar?
- Use uma chave primária quando precisar de uma identificação única para cada registro em uma tabela.

#### Exemplo:
```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT
);
```

### Chave Estrangeira (Foreign Key)

#### Para que serve?
- Uma chave estrangeira é uma coluna ou um conjunto de colunas que estabelece uma relação entre duas tabelas.
- Ela aponta para a chave primária em outra tabela.

#### Quando usar?
- Use chaves estrangeiras para estabelecer relações entre tabelas em um banco de dados relacional.

#### Exemplo:
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    product_id INT,
    customer_id INT,
    FOREIGN KEY (product_id) REFERENCES products(product_id),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

### Única (Unique)

#### Para que serve?
- A restrição `UNIQUE` garante que todos os valores em uma coluna ou conjunto de colunas sejam diferentes.
- Permite que você tenha valores únicos em uma coluna.

#### Quando usar?
- Use quando precisar garantir que os valores em uma coluna ou conjunto de colunas sejam únicos.

#### Exemplo:
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    department_id INT
);
```

### NOT NULL

#### Para que serve?
- A restrição `NOT NULL` garante que uma coluna não aceite valores nulos.
- Obriga que um valor seja inserido em uma coluna.

#### Quando usar?
- Use quando precisar garantir que uma coluna não aceite valores nulos.

#### Exemplo:
```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2)
);
```

### CHECK

#### Para que serve?
- A restrição `CHECK` permite especificar uma condição para os valores em uma coluna.
- Garante que os valores atendam a determinadas condições.

#### Quando usar?
- Use quando precisar impor uma condição específica para os valores em uma coluna.

#### Exemplo:
```sql
CREATE TABLE grades (
    student_id INT,
    course_id INT,
    grade INT CHECK (grade >= 0 AND grade <= 100),
    PRIMARY KEY (student_id, course_id)
);
```

