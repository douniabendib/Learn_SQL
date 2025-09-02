# Mathematical Operators


In SQL, you can perform calculations directly with column values in your queries. This is useful when you need to compute new values based on existing data. For example:

| Operator | Operation     |
|----------|---------------|
| +        | Addition      |
| -        | Subtraction   |
| *        | Multiplication|
| /        | Division      |
```sql
SELECT price + 10 as increased_price,
       price - 10 as reduced_price,
       price * 10 as multiple_price,
       price / 2 as half_price
FROM products;
```
