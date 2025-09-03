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
