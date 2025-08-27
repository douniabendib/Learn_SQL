# Conditions Basics


Sometimes we would like to fetch records that meet a certain condition.

For example

- fetch all of the records that have the family name "Aothly" 
- fetch all of the records that the amount is bigger than 5
- fetch all of the records with the country "Mexico"
To add conditions we can use the WHERE keyword

For example here is a sales table:

| Coin | Amount |
|------|--------|
| AGK  | 13     |
| GOL  | 21     |
| KLA  | 15     |
| AGK  | 18     |

To fetch all of the records with the coin "AGK" we will write:
```sql
SELECT * FROM sales
WHERE coin = 'AGK'
```
To fetch all of the records with amount smaller or equal to 20 we will write:
```sql
SELECT * FROM sales
WHERE amount <= 20
```
# The AND Keyword

The **AND** keyword means that both conditions must be true; if either one of them is not, then the condition will not be met.

## Example People Table

| Name   | Age | Gender |
|--------|-----|--------|
| Joas   | 13  | Male   |
| Holwa  | 17  | Male   |
| Nohlas | 24  | Female |
| Polar  | 23  | Male   |
| Loopa  | 18  | Female |

## SQL Query

The following query:

```sql
SELECT * 
FROM people
WHERE gender = "female" AND age < 20
```
means that we are looking for all records where the gender is "female" and the age is less than 20.

## Result

| Name  | Age | Gender |
|-------|-----|--------|
| Loopa | 18  | Female |

# The OR Keyword

The **OR** keyword means that we want one of the conditions to be true.

## Example People Table

| Name   | Age | Gender |
|--------|-----|--------|
| Joas   | 13  | Male   |
| Holwa  | 17  | Male   |
| Nohlas | 24  | Female |
| Polar  | 23  | Male   |
| Loopa  | 18  | Female |

## SQL Query

```sql
SELECT * 
FROM people
WHERE gender = 'female' OR age < 20
```
This query means that we are looking for all records where either the gender is female or the age is less than 20.

This will be the result:

## Result

| Name   | Age | Gender |
|--------|-----|--------|
| Joas   | 13  | Male   |
| Holwa  | 17  | Male   |
| Nohlas | 24  | Female |
| Loopa  | 18  | Female |

# The NOT Keyword

The **NOT** keyword means that we don't want the condition to be met.

## Example People Table

| Name   | Age | Gender |
|--------|-----|--------|
| Joas   | 13  | Male   |
| Holwa  | 17  | Male   |
| Nohlas | 24  | Female |
| Polar  | 23  | Male   |
| Loopa  | 18  | Female |

## SQL Query

```sql
SELECT * 
FROM people
WHERE NOT gender = 'male'
```
## Result

| Name   | Age | Gender |
|--------|-----|--------|
| Nohlas | 24  | Female |
| Loopa  | 18  | Female |

The NOT keyword basically flips the condition. For example the following queries are the same:
```sql
WHERE age > 20
```
```sql
WHERE NOT age <= 20
```

# Multiple Conditions Combined


Creating a query with only one condition is not sufficient. Sometimes we would like to check something more complicated. For that SQL (and many other programming languages) have the AND, OR, and NOT keywords to increase our ability to fetch the right result we need.

The AND and OR keywords are used like this:
```sql
SELECT col1, col2 
FROM table1
WHERE condition1 AND condition2 OR condition3 ...
```
We can stack as many conditions as we want together.
