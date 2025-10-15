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
