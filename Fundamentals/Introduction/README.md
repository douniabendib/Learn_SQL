# Introduction

SQL (Structured Query Language) is a standard language for managing and manipulating relational databases. It allows users to store, retrieve, and analyze data efficiently, making it essential for businesses and organizations worldwide.

## What is a database


Databases are like large buckets that store data in an organized manner. Here are two examples of when we would like to create a database:

A database for a university to save data about students, courses, and lecturers.
A database for a car agency to track sales, car storage, and employees.
And many more
Inside a database there are tables, and each table has a name, column names, and rows. For example, this is a workers table:

| firstname | lastname | age | exp_years | gender |
|-----------|----------|-----|------------|--------|
| Ghully    | Thuas    | 29  | 2.3        | Female |
| Bostal    | Shkolky  | 32  | 0.2        | Male   |
| Qaostu    | Malop    | 21  | 4          | Female |

The workers table has 5 columns and 3 rows. We don't need any special tool to know that we have 3 workers, and it's easy to calculate the average age of all of them (29 + 32 + 21) / 3. But what happens when we have a thousand or even a million rows?

That's where databases and SQL (Structured Query Language) come in. SQL is a standard language designed specifically for managing and manipulating data in databases. Databases store all of the tables, and SQL helps us extract and analyze the data we need.

To extract the whole table from the database, we need to specify which columns to SELECT and FROM which table to extract.

To do this we'll write:
```sql
SELECT column1, column2, column3 FROM table_name;
```

## Database concepts


In databases, rows are called records, and columns are called fields.

Tables have a fixed number of fields (columns) but can contain many records (rows). Each field has a unique name, usually in lowercase and singular form. Tables typically include an id field, which serves as a unique identifier for each record, helping to distinguish between similar entries.

In SQL, we can use the asterisk * symbol as a shortcut to select all columns from a table. Instead of listing each column name, simply write:
```sql
SELECT * FROM table_name
```
This query fetches every column in the specified table.

## Unique values
Let's assume we have the following table:

sales
|   #  | Country | City      | Amount |
|------|---------|-----------|--------|
|  1   | Poland  | Warsaw    |  13    |
|  2   | Germany | Berlin    |  24    |
|  3   | Poland  | Katowice  |  51    |
And we would like to know all of the countries where the product was sold.

If we use the normal query we know: SELECT country from sales it will return Poland, Germany, Poland. This is not what we are looking for because Poland is repeated twice.

To solve it we can use the DISTINCT keyword:
```sql
SELECT DISTINCT country FROM sales
```
