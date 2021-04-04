## Questions Index

* [Ques 1](#ques-1-list-the-films-where-the-yr-is-1962-show-id-title)

* [Ques 2](#ques-2-when-was-citizen-kane-released)

* [Ques 3](#ques-3-list-all-of-the-star-trek-movies-include-the-id-title-and-yr-all-of-these-movies-include-the-words-star-trek-in-the-title-order-results-by-year)

* [Ques 4](#ques-4-what-id-number-does-the-actor-glenn-close-have)

* [Ques 5](#ques-5-what-is-the-id-of-the-film-casablanca)

* [Ques 6](#ques-6-obtain-the-cast-list-for-casablanca)

* [Ques 7](#ques-7-obtain-the-cast-list-for-the-film-alien)

* [Ques 8](#ques-8-list-the-films-in-which-harrison-ford-has-appeared)

* [Ques 9](#ques-9-list-the-films-where-harrison-ford-has-appeared--but-not-in-the-starring-role)

* [Ques 10](#ques-10-list-the-films-together-with-the-leading-star-for-all-1962-films)

* [Ques 11](#ques-11-which-were-the-busiest-years-for-rock-hudson-show-the-year-and-the-number-of-movies-he-made-each-year-for-any-year-in-which-he-made-more-than-2-movies)

* [Ques 12](#ques-12-list-the-film-title-and-the-leading-actor-for-all-of-the-films-julie-andrews-played-in)

* [Ques 13](#ques-13-obtain-a-list-in-alphabetical-order-of-actors-whove-had-at-least-15-starring-roles)

* [Ques 14](#ques-14-list-the-films-released-in-the-year-1978-ordered-by-the-number-of-actors-in-the-cast-then-by-title)

* [Ques 15](#ques-15-list-all-the-people-who-have-worked-with-art-garfunkel)


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
  JOIN movie ON (movieid = id)
  WHERE title = 'Alien'
)
```

### Ques 8. List the films in which 'Harrison Ford' has appeared.

```sql
SELECT title
FROM movie
JOIN casting ON (id = movieid)
WHERE actorid = (
  SELECT id
  FROM actor
  WHERE name='Harrison Ford'
)
```

### Ques 9. List the films where 'Harrison Ford' has appeared - but not in the starring role.

```sql
SELECT title
FROM movie
WHERE id IN (
  SELECT movieid
  FROM casting
  JOIN actor ON (actorid = id)
  WHERE name = 'Harrison Ford'
    AND ord != 1
)
```

### Ques 10. List the films together with the leading star for all 1962 films.

```sql
SELECT title, name
FROM movie m
JOIN casting c ON (m.id = c.movieid)
JOIN actor a ON (c.actorid = a.id)
WHERE m.yr = 1962
  AND c.ord = 1
```

### Ques 11. Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

```sql
SELECT yr, COUNT(title)
FROM movie
JOIN casting ON (movie.id = movieid)
JOIN actor   ON (actorid = actor.id)
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 1
```

### Ques 12. List the film title and the leading actor for all of the films 'Julie Andrews' played in.

```sql
SELECT title, name
FROM movie
JOIN casting ON (id = movieid)
JOIN actor ON (actor.id = actorid)
WHERE movieid IN (
  SELECT movieid FROM casting
  WHERE actorid IN (
    SELECT id FROM actor
    WHERE name='Julie Andrews')
  )
  AND ord = 1
```

### Ques 13. Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.

```sql
SELECT name
FROM actor
JOIN casting ON (id = actorid)
WHERE ord = 1
GROUP BY name
HAVING count(name) >= 15
ORDER BY name
```

### Ques 14. List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

```sql
SELECT title, COUNT(title) AS total_actors
FROM movie m
JOIN casting c ON (m.id = c.movieid)
JOIN actor a ON (c.actorid = a.id)
WHERE yr = 1978
GROUP BY title
ORDER BY total_actors DESC, title
```

### Ques 15. List all the people who have worked with 'Art Garfunkel'.

```sql
SELECT name
FROM actor a
JOIN casting c ON (id = actorid)
WHERE c.movieid IN (
  SELECT movieid
  FROM casting c
  JOIN actor a ON (c.actorid = a.id)
  WHERE a.name = 'Art Garfunkel'
)
AND a.name <> 'Art Garfunkel'
ORDER BY a.name
```
