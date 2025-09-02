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

# The LIKE keyword


The LIKE keyword is used to check the similarities of strings. For example, if we want to fetch all of the records that the name starts with the letter a then we will use the LIKE keyword.

Two main wildcards are used:

- % - means any number of characters
-  _ - means exactly one character
For example:

- %a - means any string that ends with a
- a% - means any string that starts with a
- %a% - means any string that contains a
- _a% - means that the letter a is the second character in the string
- %a__ - means that the string contains a in the 3rd from last place
 To use it we will write:
```sql
SELECT col1, col2, ...
FROM table1
WHERE col1 LIKE '%a__'
```
