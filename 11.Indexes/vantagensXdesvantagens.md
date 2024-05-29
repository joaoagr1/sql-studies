### Índices em SQL

Os índices são ferramentas poderosas para melhorar a eficiência das consultas em SQL. Eles devem ser usados estrategicamente para maximizar o desempenho e minimizar os custos associados. Compreender como, quando e onde implementar índices é crucial para manter um banco de dados rápido e eficiente.

## Vantagens

### Melhora a Performance de Consulta em Muitos Casos
Os acessos aos dados são enormemente reduzidos. A forma como o índice é montado permite busca em uma parte dos dados. O mais comum é a utilização de árvore binária, mantendo os dados ordenados (mas existem outros tipos). Assim, uma busca binária pode ocorrer com complexidade O(log n), o que significa que você consegue achar uma informação disponível em índice em escala maior com o aumento de dados. Por exemplo:

- Com 50 linhas, você consegue chegar onde quer em até 7 passos; sem o índice, demoraria até 50 passos.
- Com mais de um bilhão de linhas, você alcança o que deseja usando índice em pouco mais de 30 passos.

A diferença é brutal.

### Pode Trazer Dados Específicos de Forma Mais Rápida
Se o que você está pedindo para trazer (fetch) está todo em índice, é possível que só uma consulta ao índice seja suficiente para obter os dados, sem precisar consultar a tabela de dados. Como os índices são menores e utilizados com mais frequência, tendem a ficar em memória. Isto pode ser uma enorme vantagem.

### Permite o Acesso de Dados Ordenados Sem o Custo de Realizar a Ordenação
Para obter a performance indicada, os dados são naturalmente ordenados, e isso é muitas vezes o que se deseja. Quando se sabe que vai utilizar muitas vezes o acesso sequencial de dados em determinada ordem, o índice vai ajudar muito. Caso contrário, uma tabela temporária deverá ser criada e todo o processo de ordenação deverá ser feito na hora, o que é bem custoso.

### Fácil Garantir que Determinadas Informações Chaves Não Estejam Duplicadas
Como a busca é rápida e simples, descobrir se uma chave já existe é uma operação muito barata, pelo menos em comparação a descobrir o mesmo sem índice.

### Resumo das Vantagens
A principal vantagem dos índices é a melhoria na performance das consultas. Os demais benefícios são colaterais, embora de grande importância também.

## Desvantagens

### Piora a Performance em Escritas de Dados no Banco de Dados
Toda vez que uma informação chave for modificada (inserida, alterada, deletada), isso obrigará a escrita no índice. O índice pode ser interpretado como uma tabela adicional escondida no banco de dados. Se a informação modificada está presente em várias chaves (vários índices), todos eles deverão ser alterados. A alteração do índice implica em acesso de leitura e escrita nele, o que adiciona um custo adicional, embora eficiente comparado ao acesso direto à tabela.

### Aumenta o Consumo de Espaço para Armazenamento do Banco de Dados (Memória e Disco)
Essa tabela adicional de chaves de índice vai ocupar um espaço extra também. Costuma ser um espaço menor que a tabela de dados original, mas existe um custo extra. Se houver muitos índices, é possível que o espaço seja até maior que a tabela original. Com muitos índices, fica difícil colocar tudo na memória.

### Aumenta a Necessidade de Manutenção Interna no Banco de Dados
Isso é um pouco dependente da implementação, mas é comum que páginas de chaves sejam abandonadas conforme elas vão sendo alteradas. Além disso, o DBA pode ter mais elementos com que se preocupar.

### Pode Diminuir a Performance de Consultas
Não há garantias de que todas as consultas serão mais rápidas com o uso de índices. Como há uma operação adicional para acesso ao índice antes do acesso aos dados principais, é possível que a soma do tempo gasto nas operações seja maior que o acesso só ao dado principal. Isso é mais comum quando o volume de dados é pequeno, mas também pode ocorrer em casos de consultas complexas ou onde uma grande porção dos dados da tabela será retornada em qualquer ordem.

### Limitações na Criação de Índices
É virtualmente impossível criar índices para qualquer chave a não ser em tabelas extremamente simples. Então, é ilusão achar que índices resolverão todos os problemas. E mesmo que fosse possível, eles causariam mais mal do que bem. Você só deve criar índices quando eles realmente são necessários e fique provado que eles estão ajudando.

## Dicas para Escolher o que Indexar

- **Evite criar muitos índices se há muita escrita nas tabelas envolvidas**: Índice ajuda muito a dar performance para leitura, mas prejudica a escrita.
- **Sempre analise o padrão de uso para escolher o melhor tipo de índice**: SGDBs modernos permitem índices que ajudam certos tipos de acesso OLTP ou OLAP.
- **Chaves menores, sem repetições e não nulas costumam ser melhores escolhas**: Para os casos onde isso não é possível, veja se o DBMS permite filtrar chaves.
- **Quando usar mais de uma coluna, escolher a ordem pode ajudar muito nos resultados de mais de uma consulta**.
- **Meça antes de criar um índice e evite-os em tabelas pequenas demais**.
- **O índice primário deve ser preferencialmente sequencial e imutável, além da obviedade de ser chave única**.

## Tipos de Índices

### Índice Simples
Um índice em uma única coluna.

```sql
CREATE INDEX idx_employee_name
ON employees (employee_name);
```

### Índice Composto
Um índice em várias colunas.

```sql
CREATE INDEX idx_employee_dept
ON employees (employee_name, department);
```

### Índice Único
Garante que os valores indexados sejam únicos.

```sql
CREATE UNIQUE INDEX idx_unique_employee_id
ON employees (employee_id);
```

### Índice de Texto Completo
Usado para buscas em colunas de texto longo.

```sql
CREATE FULLTEXT INDEX idx_fulltext_description
ON products (description);
```

### Índice Clusterizado
Reorganiza a tabela física para corresponder à ordem do índice.

```sql
CREATE CLUSTERED INDEX idx_clustered_employee_id
ON employees (employee_id);
```

### Índice Não-Clusterizado
Mantém uma estrutura separada da tabela original.

```sql
CREATE NONCLUSTERED INDEX idx_nonclustered_employee_name
ON employees (employee_name);
```

## Exemplo Prático

Suponha que temos uma tabela `orders` com milhões de registros:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_date DATE,
    customer_id INT,
    total_amount DECIMAL(10, 2)
);
```

Para acelerar buscas por data e cliente:

```sql
CREATE INDEX idx_order_date_customer
ON orders (order_date, customer_id);
```

Consulta otimizada:

```sql
SELECT order_id, total_amount
FROM orders
WHERE order_date = '2024-05-27' AND customer_id = 123;
```

## Conclusão

Os índices são ferramentas poderosas para melhorar a eficiência das consultas em SQL. Eles devem ser usados estrategicamente para maximizar o desempenho e minimizar os custos associados. Compreender como, quando e onde implementar índices é crucial para manter um banco de dados rápido e eficiente.
```