# Built-In Aggregate Part 1


There are many built-in functions in SQL but we will cover the aggregate functions in this lesson.

An aggregate function receives a field as input and calculates something over this field. The most common aggregate functions are:

- MAX - Returns the max value of a field
- MIN - Returns the min value of a field
- AVG - Returns the average value of a field
- COUNT - Returns the total number of records
- SUM - Return the sum of all non-null values in a field
You can use these functions in your SELECT statement like this:
```sql
SELECT MAX(col1), MIN(col2), AVG(col3), …
```
For example, to find the highest salary in an employees table:
```sql
SELECT MAX(salary) FROM employees
```
Or to get multiple aggregates at once:
```sql
SELECT MAX(salary), MIN(salary), AVG(salary) FROM employees
```

# Built-In Aggregate Part 2


Sometimes we need to use aggregate functions in more complex ways, such as comparing each row with an aggregate value. This is where nested queries come in handy.
When you want to perform calculations that combine individual rows with aggregate values, you need to use a nested query. Here's why:
This won't work:
```sql
SELECT value + MIN(value)
FROM table1
```
The reason is that aggregate functions work on the entire column, while the 'value' reference is trying to work row by row. To solve this, we use a nested query:
```sql
SELECT value + (SELECT MIN(value) FROM table1)
FROM table1
```
This works because the nested query (SELECT MIN(value) FROM table1) is executed first and returns a single value, which can then be used in the main query for each row.
Common use cases for nested aggregates:
1. Comparing each value to the average
2. Calculating percentage of total
3. Finding differences from maximum or minimum values
