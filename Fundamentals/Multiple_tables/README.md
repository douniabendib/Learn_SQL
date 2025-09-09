# Basic Join Part 1


As of now, we tackled problems of a single table. Now we will examine how to handle multiple tables.

Let's assume we have the following tables:

courses

| course_id | lecturer_id |
|-----------|-------------|
| 1         | 1           |
| 2         | 1           |
| 3         | 2           |

lecturers

| lecturer_id | name   |
|-------------|--------|
| 1           | Jhonas |
| 2           | Malidos|

The task is to present for each course with the corresponding lecturer's name.

There are two ways to achieve this. For each option, we match each row in one table to the other. we check a condition that must be met and if the condition is met we combine the two rows into one. The desired result for both options:

| course_id | lecturer_name |
|-----------|---------------|
| 1         | Jhonas        |
| 2         | Jhonas        |
| 3         | Malidos       |

- Option 1:
```sql
SELECT courses.course_id, lecturers.name AS lecturer_name
FROM courses, lecturers
WHERE courses.lecturer_id = lecturers.lecturer_id
```
Here we write two tables in the FROM keyword, and in the WHERE clause we request that the lecturer_id of both records must be the same. In the SELECT clause we now write table.column so that the database will know where to fetch the column.

- Option 2:
```sql
SELECT courses.course_id, lecturers.name AS lecturer_name
FROM courses
JOIN lecturers ON courses.lecturer_id = lecturers.lecturer_id
```
Instead of WHERE we use JOIN table ON condition

This type of join is also called an inner join.

# Basic Join Part 2


Joins can also be used on tables that we create. To combine nested tables with joins we need to add AS to identify the nested query with a name. For example:
```sql
SELECT table1.col1, table2.col2, ...
FROM table1, (SELECT * FROM table) AS table2
WHERE table1.id = table2.id
```
# Self join


Self-joins are different types of joins. As of now, we talked about multiple table joins, but self-joins are joined to the same table. A classic example would be a table of employees.

| employee_id | employee_name | manager_id |
|-------------|---------------|------------|
| 1           | Minke         | 2          |
| 2           | Temur         | 3          |
| 3           | Tatjana       | 4          |
| 4           | Marinela      |            |
Every employee has a manager except the highest manager, and every manager is also an employee.

The problem: For each employee we want to know the manager's name.
```sql
SELECT e2.employee_id, e2.employee_name, e1.employee_name as manager_name
FROM employees as e1
JOIN employees as e2 ON e1.employee_id = e2.manager_id
```
We join between the same table except one time we call it e1 and the second time it is e2. The join is between the fields employee_id and manager_id.

The result:
| employee_id | employee_name | manager_name |
|-------------|---------------|---------------|
| 1           | Minke         | Temur         |
| 2           | Temur         | Tatjana       |
| 3           | Tatjana       | Marinela      |

# Union


Unions are different from joins. Joins are using conditions to combine tables but unions just add two tables on top of the other. To use UNION we will write:
```sql
SELECT col1, col2, ... FROM table1
UNION
SELECT col1, col2, ... FROM table2
```
Both selects must obey the following rules:

- The number of fields should be equal
- Order is important
- The columns in the same place must match the data types
For example, let's assume we have the following tables:

germany_people
| id | name   |
|----|--------|
| 1  | Lena   |
| 2  | Leonie |

england_people
| id | name   |
|----|--------|
| 1  | George |
| 2  | Lena   |

Problem: We want to make one big table of all the names we have.
```sql
SELECT name from germany_people
UNION
SELECT name from england_people
```
Result:
| name   |
|--------|
| Lena   |
| Leonie |
| George |

UNION returns only distinct values while UNION ALL return all of the records as-is:
```sql
SELECT name from germany_people
UNION ALL
SELECT name from england_people
```
Result:

| name   |
|--------|
| Lena   |
| Leonie |
| George |
| Lena   |

# Simplify queries, WITH keyword


Queries can get too messy by adding many inner queries. For example here is a query that has many sub-queries:
```sql
SELECT * FROM table1
WHERE col2 IN (
    SELECT col1 FROM table2
    WHERE col3 + col2 > 3 AND col5 LIKE '%test%' AND col6 IN (
        SELECT col5 FROM table3
        WHERE col1 AND col3 OR col2
    )
)
```
To make it easier we can use the WITH query_name AS (...) keyword. It allows us to save a query with a name and use it wherever we want:
```sql
WITH query1 AS (
    SELECT col5 FROM table3
    WHERE col1 AND col3 OR col2
), query2 AS (
    SELECT col1 FROM table2
    WHERE col3 + col2 > 3 AND col5 LIKE '%test%' AND col6 IN query1
)
SELECT * FROM table1
WHERE col2 IN query2 AND col4 IN query1
```
Here we reused query1 in query2 and in the main query.
