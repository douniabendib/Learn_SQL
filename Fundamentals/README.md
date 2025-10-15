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

