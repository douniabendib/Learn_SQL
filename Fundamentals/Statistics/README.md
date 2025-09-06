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

# Grouping Part 1


We have calculated data for the entire field thus far, and now we will introduce the ability to calculate data for specific groups.

workers
| id | area | age |
|----|------|-----|
|  1 |  A   | 35  |
|  2 |  A   | 37  |
|  3 |  B   | 29  |
|  4 |  B   | 39  |
If we write 
```sql
SELECT AVG(age) as avg_age FROM workers
```
We will receive only the average age of all the workers together. 

What if we want to calculate the average age for each area?

For that, we can use the GROUP BY keywords
```sql
SELECT area, AVG(age) as avg_age FROM workers
GROUP BY area
```
The result:
| area | avg_age |
|------|---------|
|  A   |   36    |
|  B   |   34    |
Now we know that the average age in Area A is 36 and the average age in Area B is 34.

# Grouping Part 2


The WHERE keyword runs a condition on each record separately. For example:
```sql
SELECT * FROM table1
WHERE col1 > col2
```
The col1 > col2 will run on every record and check if it is met.

But what if we want to filter aggregate results? For example:
```sql
SELECT category, AVG(price) FROM table1
WHERE AVG(price) > 40
GROUP BY category
```
This will not work because WHERE cannot check any aggregations. For that, we have the HAVING keyword. It filters data by the aggregate condition.
```sql
SELECT category, AVG(price) FROM table1
GROUP BY category
HAVING AVG(price) > 40
```
This will filter all the categories for which the average price is greater than 40.

If we want to combine HAVING and WHERE clause we will write:
```sql
SELECT category, AVG(price) FROM table1
WHERE price > 25
GROUP BY category
HAVING AVG(price) > 40
```
This will first go record by record and filter all the records for which the price is greater than 25, and only after that will it run the GROUP BY clause and filter every category for which the average price is greater than 40.
