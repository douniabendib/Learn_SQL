# The IN keyword


When we need to find rows where a column matches any one of several possible values, we can write it using multiple OR conditions. For example the following query is very long:
```sql
SELECT *
FROM table1
WHERE col1 = 'a' OR col1 = 'b' OR col1 = 'c' OR col1 = 'd' OR ...
```
We can simplify it by using the IN keyword like this:
```sql
SELECT *
FROM table1
WHERE col1 IN ('a', 'b', 'c', 'd', 'e', 'f')
```
This shorter version does exactly the same thing: it returns rows where col1 equals any of the values listed in the parentheses.

# The BETWEEN keyword


As of now, we learned to use bigger > and smaller < to demand a range for a field. But there is another way.

Instead of writing:
```sql
WHERE col1 >= 5 AND col1 <= 10
```
We can write:
```sql
WHERE col1 BETWEEN 5 AND 10
```
The BETWEEN operator is inclusive, meaning it includes the boundary values (in this case, 5 and 10) in the results. This makes your SQL queries cleaner and more readable, especially when dealing with date ranges or numerical intervals.

