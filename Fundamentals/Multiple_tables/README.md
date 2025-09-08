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
