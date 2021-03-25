## Questions Index

* [Ques 1](#ques-1-list-each-country-name-where-the-population-is-larger-than-that-of-russia)

* [Ques 2](#ques-2-show-the-countries-in-europe-with-a-per-capita-gdp-greater-than-united-kingdom)

* [Ques 3](#ques-3-list-the-name-and-continent-of-countries-in-the-continents-containing-either-argentina-or-australia-order-by-name-of-the-country)

* [Ques 4](#ques-4-which-country-has-a-population-that-is-more-than-canada-but-less-than-poland-show-the-name-and-the-population)

* [Ques 5](#ques-5-show-the-name-and-the-population-of-each-country-in-europe-show-the-population-as-a-percentage-of-the-population-of-germany)

* [Ques 6](#ques6-which-countries-have-a-gdp-greater-than-every-country-in-europe)

* [Ques 7](#ques-7-find-the-largest-country-by-area-in-each-continent-show-the-continent-the-name-and-the-area)

* [Ques 9](#ques-9-find-the-continents-where-all-countries-have-a-population-<=-25000000-then-find-the-names-of-the-countries-associated-with-these-continents-show-name-continent-and-population)


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

### Ques 3. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

```sql
SELECT name,continent
FROM world
WHERE continent IN (
		SELECT continent
		FROM world
		WHERE name IN ('Argentina','Australia')
	)
ORDER BY name
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


### Ques6. Which countries have a GDP greater than every country in Europe?

```sql
SELECT name
FROM world
WHERE gdp > (SELECT max(gdp) FROM world WHERE continent  = 'Europe')
```

### Ques 7. Find the largest country (by area) in each continent, show the continent, the name and the area.

```sql
SELECT continent, name, area
FROM world
WHERE area IN (SELECT max(area) FROM world GROUP BY continent)
```

### Ques 9. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

```sql
SELECT name, continent, population FROM world
WHERE continent NOT IN (
	SELECT continent
	FROM world
	WHERE population > 25000000
)
```
