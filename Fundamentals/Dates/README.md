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
