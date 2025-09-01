# Null values


In the real world, we might have fields with no values. A field with no value is called null.

We can manipulate our query using IS NULL or IS NOT NULL to fetch relevant data

For example the following query will return all of the records where col1 has no value:
```sql
SELECT *
FROM table1
WHERE col1 IS NULL
```
# Sort Results Part 1


When querying a database, organizing your results in a meaningful order can make data analysis much more efficient. To sort the result we use the ORDER BY keyword and after that, we should specify by which field we are ordering by. By default, it sorts by ascending order. For example consider the following competition table:

| runner_id | age | avg_speed |
|-----------|-----|-----------|
| 1         | 47  | 3.65      |
| 2         | 62  | 3.07      |
| 3         | 57  | 6.82      |
| 4         | 56  | 4.34      |
| 5         | 25  | 4.93      |
| 6         | 40  | 3.94      |
| 7         | 23  | 6.58      |
| 8         | 40  | 3.43      |
```sql
SELECT *
FROM competition
WHERE age > 50
ORDER BY avg_speed
```
This is the result

| runner_id | age | avg_speed |
|-----------|-----|-----------|
| 2         | 62  | 3.07      |
| 4         | 56  | 4.34      |
| 3         | 57  | 6.82      |

To specify how to sort that data we can add DESC or ASC keywords after the name of the column.
```sql
ORDER BY avg_speed ASC
```
# Sort Results Part 2


When using ORDER BY in SQL, you can sort data by multiple columns.

For example consider the following competition table:

| runner_id | age | avg_speed |
|-----------|-----|-----------|
| 1         | 47  | 3.65      |
| 2         | 62  | 3.07      |
| 3         | 57  | 6.82      |
| 4         | 56  | 4.34      |
| 5         | 25  | 4.93      |
| 6         | 40  | 3.94      |
| 7         | 23  | 6.58      |
| 8         | 40  | 3.43      |

```sql
SELECT *
FROM competition
WHERE age < 50
ORDER BY age DESC, avg_speed DESC
```
This query will:
1. First sort all records by age in descending order (highest to lowest)
2. If two or more records have the same age, it will then sort those specific records by avg_speed in descending order

The result:

| runner_id | age | avg_speed |
|-----------|-----|-----------|
| 1         | 47  | 3.65      |
| 8         | 40  | 3.43      |
| 6         | 40  | 3.94      |
| 5         | 25  | 4.93      |
| 7         | 23  | 6.58      |


