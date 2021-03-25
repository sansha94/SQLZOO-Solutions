## Questions Index

* [Ques 1](#ques-1-show-the-total-population-of-the-world)

* [Ques 2](#ques-2-list-all-the-continents---just-once-each)

* [Ques 3](#ques-3-give-the-total-gdp-of-africa)

* [Ques 4](#ques-4-how-many-countries-have-an-area-of-at-least-1000000)

* [Ques 5](#ques-5-what-is-the-total-population-of-estonia-latvia-lithuania)

* [Ques 6](#ques-6-for-each-continent-show-the-continent-and-number-of-countries)

* [Ques 7](#ques-7-for-each-continent-show-the-continent-and-number-of-countries-with-populations-of-at-least-10-million)

* [Ques 8](#ques-8-list-the-continents-that-have-a-total-population-of-at-least-100-million)


### Ques 1. Show the total population of the world.

```sql
SELECT SUM(population)
FROM world
```

### Ques 2. List all the continents - just once each.

```sql
SELECT DISTINCT continent
FROM world
```

### Ques 3. Give the total GDP of Africa

```sql
SELECT sum(gdp)
FROM world
WHERE continent = 'Africa'
```

### Ques 4. How many countries have an area of at least 1000000

```sql
SELECT COUNT(name)
FROM world
WHERE area >= 1000000
```

### Ques 5. What is the total population of ('Estonia', 'Latvia', 'Lithuania')

```sql
SELECT sum(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```

### Ques 6. For each continent show the continent and number of countries.

```sql
SELECT continent, COUNT(name)
FROM world
GROUP BY continent
```

### Ques 7. For each continent show the continent and number of countries with populations of at least 10 million.

```sql
SELECT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent
```

### Ques 8. List the continents that have a total population of at least 100 million.

```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000
```
