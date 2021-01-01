## Questions Index

* [Ques 1](#ques-1-list-each-country-name-where-the-population-is-larger-than-that-of-russia)

* [Ques 2](#ques-2-show-the-countries-in-europe-with-a-per-capita-gdp-greater-than-united-kingdom)

* [Ques 4](#ques-4-which-country-has-a-population-that-is-more-than-canada-but-less-than-poland-show-the-name-and-the-population)

* [Ques 5](#ques-5-show-the-name-and-the-population-of-each-country-in-europe-show-the-population-as-a-percentage-of-the-population-of-germany)

### Ques 1. List each country name where the population is larger than that of 'Russia'

```sql
SELECT name
FROM world
WHERE population > (
		SELECT population
		FROM world
		WHERE name = 'Russia'
		)
```

### Ques 2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'

```sql
SELECT name
FROM world
WHERE continent = 'Europe'
	AND (gdp / population) > (
		SELECT gdp / population
		FROM world
		WHERE name = 'United Kingdom'
		)
```

### Ques 4. Which country has a population that is more than Canada but less than Poland? Show the name and the population

```sql
SELECT name, population
FROM world
WHERE population > (
		SELECT population
		FROM world
		WHERE name IN ('Canada')
		)
	AND population < (
		SELECT population
		FROM world
		WHERE name IN ('Poland')
		)
```

### Ques 5. Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany

```sql
SELECT name
	,CONCAT (
		ROUND((
				population / (
					SELECT population
					FROM world
					WHERE name = 'Germany'
					) * 100
				))
		,'%'
		)
FROM world
WHERE continent = 'Europe'
```
