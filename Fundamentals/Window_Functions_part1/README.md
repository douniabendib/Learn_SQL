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

# PARTITION BY criterion


Another option for the OVER () clause is PARTITION BY

It allows us to number the rows for each group separately 

For example:

| id  | type |
|-----|------|
| 132 | t1   |
| 52  | t2   |
| 92  | t1   |
| 154 | t3   |
| 198 | t1   |
```sql
SELECT id, type, ROW_NUMBER() OVER (PARTITION BY type ORDER BY id) as row_num
FROM table1
```
This will generate a column that will number each type within itself:

| id  | type | row_num |
|-----|------|---------|
| 132 | t1   | 1       |
| 52  | t2   | 1       |
| 92  | t1   | 2       |
| 154 | t3   | 1       |
| 198 | t1   | 3       |

id 92 has row_num 2 because it is the second row of type t1 when ordered by id.

Note: ROW_NUMBER() requires an ORDER BY clause within the OVER() to determine how rows should be numbered within each partition.

We can even specify multiple columns inside the PARTITION BY:
```sql
ROW_NUMBER() OVER (PARTITION BY type, hue ORDER BY id)
```
# PARTITION & ORDER


We can also combine PARTITION BY with ORDER BY. For example consider the following table1:
| id  | type |
|-----|------|
| 132 | t1   |
| 52  | t2   |
| 92  | t1   |
| 154 | t3   |
| 198 | t1   |
```sql
SELECT id, type, ROW_NUMBER() OVER (PARTITION BY type ORDER BY id) as row_num
FROM table1
```
This will number the rows in ascending order by the id of each type:

| id  | type | row_num |
|-----|------|---------|
| 132 | t1   | 2       |
| 52  | t2   | 1       |
| 92  | t1   | 1       |
| 154 | t3   | 1       |
| 198 | t1   | 3       |

Now id 132 has row_num 2 because it is larger than 92 and smaller than 198 (of all the t1 type rows).

# LEAD & LAG Functions
 
The LAG and LEAD functions allow access to values from previous or next rows:

LAG function - gets value from previous row:
```sql
LAG(column_name, n) OVER (ORDER BY column)
```
LEAD function - gets value from next row:
```sql
LEAD(column_name, n) OVER (ORDER BY column)
```
Example using LAG to get previous month's revenue:
```sql
SELECT id, revenue, LAG(revenue, 1) OVER (ORDER BY month) as prev_month_revenue
```
FROM table1 ORDER BY id
The first row will have NULL for the LAG value, and the last row will have NULL for the LEAD value
