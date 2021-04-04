## Questions Index

* [Ques 1](#ques-1-list-the-films-where-the-yr-is-1962-show-id-title)

* [Ques 2](#ques-2-when-was-citizen-kane-released)

* [Ques 3](#ques-3-list-all-of-the-star-trek-movies-include-the-id-title-and-yr-all-of-these-movies-include-the-words-star-trek-in-the-title-order-results-by-year)

* [Ques 4](#ques-4-what-id-number-does-the-actor-glenn-close-have)

* [Ques 5](#ques-5-what-is-the-id-of-the-film-casablanca)

* [Ques 6](#ques-6-obtain-the-cast-list-for-casablanca)

* [Ques 7](#ques-7-obtain-the-cast-list-for-the-film-alien)

* [Ques 8](#ques-8-list-the-films-in-which-harrison-ford-has-appeared)


### Ques 1. List the films where the yr is 1962. Show id, title.

```sql
SELECT id, title
FROM movie
WHERE yr=1962
```

### Ques 2. When was Citizen Kane released?

```sql
SELECT yr
FROM movie
WHERE title='Citizen Kane'
```

### Ques 3. List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.

```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr
```

### Ques 4. What id number does the actor 'Glenn Close' have?

```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```

### Ques 5. What is the id of the film 'Casablanca'?

```sql
SELECT id
FROM movie
WHERE title = 'Casablanca'
```

### Ques 6. Obtain the cast list for 'Casablanca'.

```sql
SELECT name
FROM actor
WHERE id IN (
  SELECT actorid
  FROM casting
  WHERE movieid=27
)
```

### Ques 7. Obtain the cast list for the film 'Alien'.

```sql
SELECT name
FROM actor
WHERE id IN (
  SELECT actorid
  FROM casting
  JOIN movie
    ON (movieid=id)
  WHERE title = 'Alien')
```


### Ques 8. List the films in which 'Harrison Ford' has appeared.

```sql
SELECT title
FROM movie
JOIN casting
  ON (id=movieid)
WHERE actorid = (
  SELECT id
  FROM actor
  WHERE name='Harrison Ford'
)
```
