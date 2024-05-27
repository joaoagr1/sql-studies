# Linguagem de Definição de Dados (DDL)

A Linguagem de Definição de Dados (DDL) é um subconjunto do SQL. Sua função principal é criar, modificar e excluir estruturas de banco de dados, mas não dados. Os comandos em DDL são:

- **CREATE:** Este comando é usado para criar o banco de dados ou seus objetos (como tabela, índice, função, visualizações, procedimentos armazenados e gatilhos).

    ```sql
    CREATE TABLE nome_da_tabela (
    coluna1 tipo_de_dado(tamanho),
    coluna2 tipo_de_dado(tamanho),
    ...
    );
    ```

- **DROP:** Este comando é usado para excluir um banco de dados ou tabela existente.

    ```sql
    DROP TABLE nome_da_tabela;
    ```

- **ALTER:** Isso é usado para alterar a estrutura do banco de dados. É usado para adicionar, excluir ou modificar colunas em uma tabela existente.

    ```sql
    ALTER TABLE nome_da_tabela ADD nome_da_coluna tipo_de_dado;
    ALTER TABLE nome_da_tabela DROP COLUMN nome_da_coluna;
    ALTER TABLE nome_da_tabela MODIFY COLUMN nome_da_coluna tipo_de_dado(tamanho);
    ```

- **TRUNCATE:** Isso é usado para remover todos os registros de uma tabela, incluindo todos os espaços alocados para os registros que são removidos.

    ```sql
    TRUNCATE TABLE nome_da_tabela;
    ```

- **RENAME:** Isso é usado para renomear um objeto no banco de dados.

    ```sql
    -- Para renomear uma tabela
    ALTER TABLE nome_da_tabela
    RENAME TO novo_nome_da_tabela;

    -- Para renomear uma coluna
    ALTER TABLE nome_da_tabela
    RENAME COLUMN nome_antiga_coluna TO novo_nome_da_coluna;
    ```

Lembre-se: Nas operações de DDL, as instruções COMMIT e ROLLBACK não podem ser executadas porque o mecanismo MySQL automaticamente confirma as alterações.

Lembre-se de substituir nome_da_tabela, nome_da_coluna, tipo_de_dado(tamanho), nome_antiga_tabela e novo_nome_da_tabela nos exemplos acima pelos seus nomes reais de tabela, nomes de coluna, tipos e tamanhos de dados, e os nomes antigos ou novos da tabela que você deseja especificar.
