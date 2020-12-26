## Questions Index

* [Ques 1](#ques-1-change-the-query-shown-so-that-it-displays-nobel-prizes-for-1950)

* [Ques 2](#ques-2-show-who-won-the-1962-prize-for-literature)

* [Ques 3](#ques-3-show-the-year-and-subject-that-won-albert-einstein-his-prize)

* [Ques 4](#ques-4-give-the-name-of-the-peace-winners-since-the-year-2000-including-2000)

* [Ques 5](#ques-5-show-all-details-yr-subject-winner-of-the-literature-prize-winners-for-1980-to-1989-inclusive)

* [Ques 6](#ques-6-show-all-details-of-the-presidential-winners)

* [Ques 7](#ques-7-show-the-winners-with-first-name-john)

* [Ques 8](#ques-8-show-the-year-subject-and-name-of-physics-winners-for-1980-together-with-the-chemistry-winners-for-1984)

* [Ques 9](#ques-9-show-the-year-subject-and-name-of-winners-for-1980-excluding-chemistry-and-medicine)

* [Ques 10](#ques-10-show-year-subject-and-name-of-people-who-won-a-medicine-prize-in-an-early-year-before-1910-not-including-1910-together-with-winners-of-a-literature-prize-in-a-later-year-after-2004-including-2004)

* [Ques 11](#ques-11-find-all-details-of-the-prize-won-by-peter-grünberg)

* [Ques 12](#ques-12-find-all-details-of-the-prize-won-by-eugene-oneill)

* [Ques 13](#ques-13-list-the-winners-year-and-subject-where-the-winner-starts-with-sir-show-the-the-most-recent-first-then-by-name-order)

* [Ques 14](#ques-14-show-the-1984-winners-and-subject-ordered-by-subject-and-winner-name-but-list-chemistry-and-physics-last)

### Ques 1. Change the query shown so that it displays Nobel prizes for 1950

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950
```

### Ques 2. Show who won the 1962 prize for Literature

```sql
SELECT winner
FROM nobel
WHERE yr = 1962 AND subject = 'Literature'
```

### Ques 3. Show the year and subject that won 'Albert Einstein' his prize

```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```

### Ques 4. Give the name of the 'Peace' winners since the year 2000, including 2000

```sql
SELECT winner
FROM nobel
WHERE yr >= 2000 and subject = 'Peace'
```

### Ques 5. Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'Literature') AND (yr BETWEEN 1980 AND 1989)
```

### Ques 6. Show all details of the presidential winners

* Theodore Roosevelt
* Woodrow Wilson
* Jimmy Carter
* Barack Obama

```sql
SELECT * FROM nobel
WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter', 'Barack Obama')
```

### Ques 7. Show the winners with first name John

```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%'
```

### Ques 8. Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (yr = 1980 AND subject = 'Physics') OR
(yr = 1984 AND subject = 'Chemistry')
```

### Ques 9. Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980 AND subject NOT IN ('Chemistry', 'Medicine')
```

### Ques 10. Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (yr < 1910 AND subject = 'Medicine') OR
(yr >= 2004 AND subject = 'Literature')
```

### Ques 11. Find all details of the prize won by PETER GRÜNBERG

```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG'
```

### Ques 12. Find all details of the prize won by EUGENE O'NEILL

```sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O''NEILL'
```

### Ques 13. List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner
```

### Ques 14. Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last

```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('Physics','Chemistry'), subject, winner
```
