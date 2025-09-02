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

# Mathematical Columns


You can combine multiple columns and numbers in complex expressions. For example:
```sql
SELECT (price * quantity) + shipping_cost as final_price
FROM orders;
```
You can also use parentheses to control the order of operations:
```sql
SELECT (base_salary + bonus) * (1 - tax_rate) as net_pay
FROM payroll;
```

# The Modulo Operation


The modulo operator % tells you what's left over after dividing one number by another.
```sql
dividend % divisor
```
dividend: The number being divided.
divisor: The number that divides the dividend.
For example
```sql
10 % 3
```
Here, 10 is divided by 3. 3 goes into 10 three times, with a remainder of 1. So, result will be 1.

Usually modulo is used for checking if a number is even or odd:

If a number is even, dividing it by 2 will leave a remainder of 0.
If a number is odd, dividing it by 2 will leave a remainder of 1.
For example find even-numbered rows:
```sql
SELECT * FROM table WHERE id % 2 = 0;
```
Or for cycling through values:

number % 12 (returns 0-11)
number % 8 (return 0-7)
For example group items into sets of 5:
```sql
SELECT item_number % 5 as group_number FROM inventory;
```
