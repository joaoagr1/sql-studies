# Operadores

Os operadores SQL são utilizados para realizar operações como comparações e cálculos aritméticos. Eles são essenciais na formação de consultas. Os operadores SQL são divididos nos seguintes tipos:

## Operadores Aritméticos

Estes são utilizados para realizar operações matemáticas. Aqui está uma lista desses operadores:

- `+` : Adição
- `-` : Subtração
- `*` : Multiplicação
- `/` : Divisão
- `%` : Módulo

**Exemplo:**

```sql
SELECT produto, preço, (preço * 0.18) AS imposto
FROM produtos;
```

## Operadores de Comparação

Estes são usados na cláusula `WHERE` para comparar uma expressão com outra. Alguns desses operadores são:

- `=` : Igual
- `!=` ou `<>` : Diferente
- `>` : Maior que
- `<` : Menor que
- `>=`: Maior ou igual
- `<=`: Menor ou igual

**Exemplo:**

```sql
SELECT nome, idade
FROM estudantes
WHERE idade > 18;
```

## Operadores Lógicos

Eles são usados para combinar o conjunto de resultados de duas condições diferentes. Estes incluem:

- `AND`: Retorna verdadeiro se ambas as condições forem verdadeiras.
- `OR` : Retorna verdadeiro se qualquer uma das condições for verdadeira.
- `NOT`: Retorna o valor booleano oposto da condição.

**Exemplo:**

```sql
SELECT * 
FROM funcionários
WHERE salário > 50000 AND idade < 30;
```

## Operadores Bit a Bit

Estes realizam operações a nível de bit nas entradas. Aqui está uma lista desses operadores:

- `&` : Bitwise AND
- `|` : Bitwise OR
- `^` : Bitwise XOR

Os operadores bitwise são muito menos comumente usados em SQL do que os outros tipos de operadores.