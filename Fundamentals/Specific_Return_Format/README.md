# Null values


In the real world, we might have fields with no values. A field with no value is called null.

We can manipulate our query using IS NULL or IS NOT NULL to fetch relevant data

For example the following query will return all of the records where col1 has no value:
```sql
SELECT *
FROM table1
WHERE col1 IS NULL
```
