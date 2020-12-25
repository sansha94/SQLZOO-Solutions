## Questions Index

* [Ques 1](#ques-1-modify-it-to-show-the-population-of-germany)

* [Ques 2](#ques-2-show-the-name-and-the-population-for-sweden-norway-and-denmark")

* [Ques 3](#ques-3-modify-it-to-show-the-country-and-the-area-for-countries-with-an-area-between-200000-and-250000)

### Ques 1. Modify it to show the population of Germany

```sql
SELECT population FROM world
WHERE name = 'Germany'
```

### Ques 2. Show the name and the population for 'Sweden', 'Norway' and 'Denmark'

```sql
SELECT name, population FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

### Ques 3. Modify it to show the country and the area for countries with an area between 200,000 and 250,000

```sql
SELECT name, area FROM world
WHERE area BETWEEN 200000 AND 250000
```
