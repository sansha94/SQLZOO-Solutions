## Questions Index

* [Ques 1](#ques-1-show-the-name-continent-and-population-of-all-countries)

* [Ques 2](#ques-2-show-the-name-for-the-countries-that-have-a-population-of-at-least-200-million)

* [Ques 3](#ques-3-give-the-name-and-the-per-capita-gdp-for-those-countries-with-a-population-of-at-least-200-million)

* [Ques 4](#ques-4-show-the-name-and-population-in-millions-for-the-countries-of-the-continent-south-america)

* [Ques 5](#ques-5-show-the-name-and-population-for-france-germany-italy)

* [Ques 6](#ques-6-show-the-countries-which-have-a-name-that-includes-the-word-united)

* [Ques 7](#ques-7-show-the-countries-that-are-big-by-area-or-big-by-population-show-name-population-and-area)

* [Ques 8](#ques-8-show-the-countries-that-are-big-by-area-more-than-3-million-or-big-by-population-more-than-250-million-but-not-both-show-name-population-and-area)

  * [Using XOR Operator](#a-using-xor-operator)

  * [Without using XOR Operator](#b-without-using-xor-operator)

* [Ques 9](#ques-9-show-the-name-and-population-in-millions-and-the-gdp-in-billions-for-the-countries-of-the-continent-south-america)

* [Ques 10](#ques-10-show-the-name-and-per-capita-gdp-for-those-countries-with-a-gdp-of-at-least-one-trillion)

* [Ques 11](#ques-11-show-the-name-and-capital-where-the-name-and-the-capital-have-the-same-number-of-characters)

* [Ques 12](#ques-12-show-the-name-and-the-capital-where-the-first-letters-of-each-match-dont-include-countries-where-the-name-and-the-capital-are-the-same-word)

* [Ques 13](#ques-13-find-the-country-that-has-all-the-vowels-and-no-spaces-in-its-name)


### Ques 1. Show the name, continent and population of all countries

```sql
SELECT name, continent, population
FROM world
```

### Ques 2. Show the name for the countries that have a population of at least 200 million

```sql
SELECT name
FROM world
WHERE population >= 200000000
```

### Ques 3. Give the name and the per capita GDP for those countries with a population of at least 200 million

```sql
SELECT name, (gdp/population) AS "per capita GDP"
FROM world
WHERE population >= 200000000
```

### Ques 4. Show the name and population in millions for the countries of the continent 'South America'

```sql
SELECT name, population/1000000 AS "population(in millions)"
FROM world
WHERE continent = 'South America'
```

### Ques 5. Show the name and population for France, Germany, Italy

```sql
SELECT name, population
FROM world
WHERE name in ('France', 'Germany', 'Italy')
```

### Ques 6. Show the countries which have a name that includes the word 'United'

```sql
SELECT name
FROM world
WHERE name LIKE '%United%'
```

### Ques 7. Show the countries that are big by area or big by population. Show name, population and area

```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000) OR (population > 250000000)
```

### Ques 8. Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area

#### a. Using XOR operator

```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000) XOR (population > 250000000)
```

#### b. Without using XOR operator

```sql
SELECT name, population,area
FROM world
WHERE (area > 3000000 OR population > 250000000) AND NOT(area>3000000 AND population > 250000000)
```

### Ques 9. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'

```sql
SELECT name, ROUND(population / 1000000, 2) as 'population(in millions)', ROUND(gdp / 1000000000, 2) as 'gdp(in billions)'
FROM world
WHERE continent = 'South America'
```

### Ques 10. Show the name and per-capita GDP for those countries with a GDP of at least one trillion

```sql
SELECT name, ROUND((gdp / population), -3) AS 'per capita gdp'
FROM world
WHERE gdp >= 1000000000000
```

### Ques 11. Show the name and capital where the name and the capital have the same number of characters

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital)
```

### Ques 12. Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word

```sql
SELECT name, capital
FROM world
WHERE (name <> capital) AND (LEFT(name, 1) = LEFT(capital, 1))
```

### Ques 13. Find the country that has all the vowels and no spaces in its name

```sql
SELECT name
FROM world
WHERE name NOT LIKE '% %' AND
((name LIKE '%a%') AND (name LIKE '%e%') AND (name LIKE '%i%') AND (name LIKE '%o%') AND (name LIKE '%u%'))
```
