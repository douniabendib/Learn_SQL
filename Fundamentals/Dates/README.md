# Handling Dates Part 1


Dates in SQL have a specific format and we can query them similarly to numbers. To write a date in a query we will use the format: YYYY-MM-DD (2012-09-24)

To query dates we can use all the operators we already know - bigger, smaller, or equal within the WHERE keyword:
```sql
SELECT * FROM table1
WHERE col1 > '2011-01-13'
```
We can even use the BETWEEN keyword:
```sql
SELECT * FROM table1
WHERE col1 BETWEEN '2010-01-01' AND '2010-02-25'
```

# Handling Dates Part 2


Dates cannot be added or subtracted like numbers. To perform calculations on dates, we must convert them to numbers using the JULIANDAY function. This function converts dates to the Julian day, a continuous count of days since January 1, 4713 BC, which is used by astronomers for time intervals and comparisons between different calendars.

To use it we will write:
```sql
SELECT JULIANDAY('2023-02-20 12:00:00')
```
This will return 2459983.0 days

# Handling Dates Part 3


SQL provides several useful functions to manipulate and format dates. Here are some common date functions:

- DATE() - Converts a string to a date
- STRFTIME() - Formats dates according to specified parameters
- DATE('now') - Gets current date:
For example convert string to date:
```sql
SELECT DATE('2023-05-15 13:45:00')
-- Returns: 2023-05-15

SELECT DATE('now')
-- Returns current date
```
For example extract year, month and day from date:
```sql
-- Get year
SELECT STRFTIME('%Y', '2023-05-15')
-- Returns: 2023

-- Get month
SELECT STRFTIME('%m', '2023-05-15')
-- Returns: 05

-- Get day
SELECT STRFTIME('%d', '2023-05-15')
-- Returns: 15

-- Show combination of year and day
SELECT STRFTIME('%Y:%d', '2023-05-15')
-- Returns: 2023:15
```
Common format specifiers:

- %Y: Year (4 digits)
- %m: Month (01-12)
- %d: Day of month (01-31)
- %w: Day of week (0-6, Sunday is 0)
- %H: Hour (00-23)
- %M: Minute (00-59)
- %S: Second (00-59)
You can combine these functions in queries:
```sql
-- Find all records from current year
SELECT * FROM table1
WHERE STRFTIME('%Y', date_column) = STRFTIME('%Y', 'now')
```
