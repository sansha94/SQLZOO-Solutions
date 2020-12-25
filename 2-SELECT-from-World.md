## Questions Index

* [Ques 1](#ques-1-show-the-name-continent-and-population-of-all-countries)

* [Ques 2](#ques-2-show-the-name-for-the-countries-that-have-a-population-of-at-least-200-million)

* [Ques 3](#ques-3-give-the-name-and-the-per-capita-gdp-for-those-countries-with-a-population-of-at-least-200-million)

* [Ques 4](#ques-4-show-the-name-and-population-in-millions-for-the-countries-of-the-continent-south-america-divide-the-population-by-1000000-to-get-population-in-millions)

* [Ques 5](#ques-5-show-the-name-and-population-for-france-germany-italy)

* [Ques 6](#ques-6-show-the-countries-which-have-a-name-that-includes-the-word-united)

* [Ques 7](#ques-7-show-the-countries-that-are-big-by-area-or-big-by-population-show-name-population-and-area)

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

### Ques 4. Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions

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
