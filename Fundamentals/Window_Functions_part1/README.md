# ROW_NUMBER function


Window functions perform calculations across a set of table rows related to the current row. Unlike regular aggregate functions, window functions don't collapse the results into a single row. They're particularly useful when you need to:

Calculate running totals
Rank items within groups
Compare current rows with previous/following rows
Analyze trends over time periods
For example here are some real world examples for window functions use-case:

- Sales Analysis:
1. Calculate cumulative sales up to each year (1995, 1997, 1999)
2. Find top-selling products for each quarter
- Sports Statistics:
1. Track Olympic medal counts across different years
2. Identify leading athletes in each competition period (2000, 2004, 2008)

ROW_NUMBER() is one of the simplest window functions. It assigns a unique sequential number to each row in the result set. Here how to use it:
```sql
SELECT column1, column2,
       ROW_NUMBER() OVER ([PARTITION BY column] [ORDER BY column]) as row_num
FROM table_name;
```
It is mandatory to use the OVER clause with ROW_NUMBER() : ROW_NUMBER() OVER ()

For example:
```sql
SELECT product_name, sale_date,
       ROW_NUMBER() OVER () as row_num
FROM sales;
```
This adds a row_num column that counts from 1 to the total number of rows.

Note: The OVER clause can contain ordering and partitioning instructions to control how the numbering works.

# ORDER BY criterion


Use ROW_NUMBER() OVER (ORDER BY column) to generate row numbers based on a specific ordering:
```sql
ROW_NUMBER() OVER (ORDER BY year DESC) as row_num
```
This creates a numbered column following the descending year order. You can use ASC for ascending or DESC for descending order, and can also order by calculated expressions.
