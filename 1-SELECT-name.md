## Questions Index

* [Ques 1](#ques-1-find-the-country-that-start-with-y)

* [Ques 2](#ques-2-find-the-countries-that-end-with-y)

* [Ques 3](#ques-3-find-the-countries-that-contain-the-letter-x)

* [Ques 4](#ques-4-find-the-countries-that-end-with-land)

* [Ques 5](#ques-5-find-the-countries-that-start-with-c-and-end-with-ia)

* [Ques 6]()

* [Ques 7]()

* [Ques 8]()

* [Ques 9]()

* [Ques 10]()

* [Ques 11]()

* [Ques 12]()

* [Ques 13]()

* [Ques 14]()

* [Ques 15]()

### Ques 1. Find the country that start with Y

```sql
SELECT name FROM world
WHERE name LIKE 'Y%'
```

### Ques 2. Find the countries that end with y

```sql
SELECT name FROM world
WHERE name LIKE '%y'
```

### Ques 3. Find the countries that contain the letter x

```sql
SELECT name FROM world
WHERE name LIKE '%x%'
```

### Ques 4. Find the countries that end with land

```sql
SELECT name FROM world
WHERE name LIKE '%land'
```

### Ques 5. Find the countries that start with C and end with ia

```sql
SELECT name FROM world
WHERE name LIKE 'C%ia'
```

### Ques 6. Find the country that has oo in the name

```sql
SELECT name FROM world
WHERE name LIKE '%oo%'
```

### Ques 7. Find the countries that have three or more a in the name

```sql
SELECT name FROM world
WHERE name LIKE '%a%a%a%'
```

### Ques 8. Find the countries that have "t" as the second character

```sql
SELECT name FROM world
WHERE name LIKE '_t%'
ORDER BY name
```

### Ques 9. Find the countries that have two "o" characters separated by two others

```sql
SELECT name FROM world
WHERE name LIKE '%o__o%'
```

### Ques 10. Find the countries that have exactly four characters

```sql
SELECT name FROM world
WHERE name LIKE '____'
```

### Ques 11. Find the country where the name is the capital city

```sql
SELECT name
FROM world
WHERE name = capital
```

### Ques 12. Find the country where the capital is the country plus "City"

```sql
SELECT name
FROM world
WHERE capital LIKE '%City'
```

### Ques 13. Find the capital and the name where the capital includes the name of the country

```sql
SELECT capital, name
FROM world
WHERE capital LIKE concat(name, '%')
```

### Ques 14. Find the capital and the name where the capital is an extension of name of the country

```sql
SELECT capital, name
FROM world
WHERE capital LIKE concat(name, '_%')
```

### Ques 15. Show the name and the extension where the capital is an extension of name of the country

```sql
SELECT name, REPLACE(capital, name, '')
FROM world
WHERE capital LIKE concat(name, '_%');
```
