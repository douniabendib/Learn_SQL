#Conditions Basics


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
