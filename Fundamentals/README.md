# RANK & DENSE_RANK Functions


ROW_NUMBER() is one type of ranking function, and there are two more: RANK() and DENSE_RANK().

The RANK() function numbers rows like ROW_NUMBER(), but it gives identical numbers for the same rows and skips numbers. DENSE_RANK() is similar to RANK(), but it does not skip numbers.

For example:

| id | level |
|----|-------|
| 1  | 5     |
| 2  | 6     |
| 3  | 6     |
| 4  | 7     |
| 5  | 7     |
| 6  | 5     |

```sql
SELECT id, 
    ROW_NUMBER() OVER (ORDER BY level) as row_num,
    RANK() OVER (ORDER BY level) as row_rank,
    DENSE_RANK() OVER (ORDER BY level) as row_dense_rank
FROM table1
```

This will return:

| id | level | row_num | row_rank | row_dense_rank |
|----|-------|---------|----------|----------------|
| 1  | 5     | 1       | 1        | 1              |
| 2  | 6     | 2       | 2        | 2              |
| 3  | 6     | 3       | 2        | 2              |
| 4  | 7     | 4       | 4        | 3              |
| 5  | 7     | 5       | 4        | 3              |
| 6  | 5     | 6       | 6        | 4              |

The ROW_NUMBER() goes from 1 to 6 with unique values, the RANK() provides the same values for the same levels, but it skipped 3 and 5, and the DENSE_RANK() also provides the same values for the same levels but it doesn't skip any values.

# NTILE Function


NTILE(n) numbers the rows by splitting them into n approximately equal pieces. It is often used for performance enhancements - sending large amounts of data at once might be not a good idea, so this function allows to send smaller pieces at a time.

For example:

| id | level |
|----|-------|
| 1  | 4     |
| 2  | 4     |
| 3  | 5     |
| 4  | 6     |
| 5  | 7     |
| 6  | 7     |

```sql
SELECT id, level, NTILE(3) OVER (ORDER BY level) as pieces
from table1
```
This will return:

| id | level | pieces |
|----|-------|--------|
| 1  | 4     | 1      |
| 2  | 4     | 1      |
| 3  | 5     | 2      |
| 4  | 6     | 2      |
| 5  | 7     | 3      |
| 6  | 7     | 3      |

We got 3 pieces: level 4 in piece 1, level 5 and level 6 in piece 2, and level 7 in piece 3.
When the number of rows isn't evenly divisible by n, NTILE distributes the rows as evenly as possible, with larger groups appearing first. For example, if you have 9 rows and NTILE(4), the distribution would be:

- Group 1: 3 rows
- Group 2: 2 rows
- Group 3: 2 rows
- Group 4: 2 rows
This ensures that no group differs by more than one row from any other group, and any extra rows are distributed to the lower-numbered groups first.

# Aggregation Functions


Aggregation functions are used to calculate the AVG() or MAX() or any other aggregation function up until the current row.
For example, we could calculate the maximum revenue we got until each ending period:

| month | revenue | region |
|-------|---------|--------|
| 4     | 40      | East   |
| 5     | 20      | East   |
| 6     | 60      | West   |
| 7     | 55      | West   |
| 8     | 61      | East   |

```sql
SELECT month, revenue, MAX(revenue) OVER (ORDER BY month ASC) as max_revenue
from table1
```
This will return:

| month | revenue | max_revenue |
|-------|---------|-------------|
| 4     | 40      | 40          |
| 5     | 20      | 40          |
| 6     | 60      | 60          |
| 7     | 55      | 60          |
| 8     | 61      | 61          |

For months 4 and 5 the maximum revenue is 40, for months 5 and 6 the revenue is 60 and for months 8, it is 61. This is because when it finds a new bigger revenue, it drops the old one and uses the biggest so far.

For AVG() function it will look like this:
```sql
SELECT month, revenue, AVG(revenue) OVER (ORDER BY month ASC) as avg_revenue
from table1
```
| month | revenue | avg_revenue |
|-------|---------|-------------|
| 4     | 40      | 40          |
| 5     | 20      | 30          |
| 6     | 60      | 40          |
| 7     | 55      | 43.75       |
| 8     | 61      | 47.2        |

We can also group our calculations by specific categories using PARTITION BY. For example:
```sql
SELECT month, revenue, region,
MAX(revenue) OVER (PARTITION BY region ORDER BY month ASC) as max_revenue
FROM table1
```
Would give us:

| month | revenue | region | max_revenue |
|-------|---------|--------|-------------|
| 4     | 40      | East   | 40          |
| 5     | 20      | East   | 40          |
| 6     | 60      | West   | 60          |
| 7     | 55      | West   | 60          |
| 8     | 61      | East   | 61          |
Now the maximum is calculated separately for each region. The East region and West region maintain their own running maximums independently.

# ROWS & RANGE Criterion

As of now, we can't be flexible regarding choosing how many rows before or after to take into account. Now it is possible with ROWS & RANGE criteria. To use them we write:

* OVER (ROWS BETWEEN --START-- AND --END--)

* OVER (RANGE BETWEEN --START-- AND --END--)

And we can specify the following options:

* CURRENT ROW - the current row
* n PRECEDING - rows before the current row
* n FOLLOWING - rows after the current row 
The difference between ROWS & RANGE is that ROWS criterion doesn't care about the values, just the positions, whereas RANGE defines the window in terms of value ranges rather than row positions.

For RANGE we must specify ORDER BY --column_name-- because if not it would not know how to choose the window.

For example:
```sql
ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
```
Here it creates a window that includes the current row, the row before it, and the row after it.
```sql
RANGE BETWEEN 1 PRECEDING AND 1 FOLLOWING ORDER BY levels
```
Here it creates a window that includes for each level (sorted in ascending order) the current level, one level before it, and one level after it. If the current level is 5 then it will include levels 4, 5, and 6.

Note: The use of RANGE BETWEEN might result in more rows being included in your window, because it includes all rows that share the same values as those in the range, while ROWS BETWEEN will always include the same number of rows (as long as they are available in the data set). 

Also RANGE does not support date columns.

Here's a simple example to illustrate ROWS vs RANGE:

- Using ROWS:
```sql
SELECT employee_name, salary,
    AVG(salary) OVER (
        ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
    ) as avg_salary_rows
```
- Using RANGE:
```sql
SELECT employee_name, salary,
    AVG(salary) OVER (
        ORDER BY salary
        RANGE BETWEEN 1000 PRECEDING AND 1000 FOLLOWING
    ) as avg_salary_range
```
