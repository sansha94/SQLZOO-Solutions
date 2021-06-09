## Questions Index

* [Ques 1](#ques-1-show-the-lastname-party-and-votes-for-the-constituency-s14000024-in-2017)

* [Ques 2](#ques-2-show-the-party-and-rank-for-constituency-s14000024-in-2017-list-the-output-by-party)

* [Ques 3](#ques-3-the-2015-election-is-a-different-partition-to-the-2017-election-we-only-care-about-the-order-of-votes-for-each-year)

* [Ques 4](#ques-4-use-partition-by-constituency-to-show-the-ranking-of-each-party-in-edinburgh-in-2017-order-your-results-so-the-winners-are-shown-first-then-ordered-by-constituency)

* [Ques 5](#ques-5-show-the-parties-that-won-for-each-edinburgh-constituency-in-2017)


### Ques 1. Show the lastName, party and votes for the constituency 'S14000024' in 2017.

```sql
SELECT lastName, party, votes
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY votes DESC
```

### Ques 2. Show the party and RANK for constituency S14000024 in 2017. List the output by party.

```sql
SELECT party, votes,
      RANK() OVER (ORDER BY votes DESC) as posn
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party
```

### Ques 3. The 2015 election is a different PARTITION to the 2017 election. We only care about the order of votes for each year.

```sql
SELECT yr, party, votes,
       RANK() OVER (PARTITION BY yr ORDER BY votes DESC) as posn
FROM ge
WHERE constituency = 'S14000021'
ORDER BY party, yr
```

### Ques 4. Use PARTITION BY constituency to show the ranking of each party in Edinburgh in 2017. Order your results so the winners are shown first, then ordered by constituency.

```sql
SELECT constituency, party, votes,
       RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) as posn
FROM ge
WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
  AND yr  = 2017
ORDER BY posn, constituency
```

### Ques 5. Show the parties that won for each Edinburgh constituency in 2017.

```sql
SELECT constituency, party
FROM (SELECT constituency,party, votes,
             RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) as posn
      FROM ge
      WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
            AND yr  = 2017
     ) ranked_parties
WHERE ranked_parties.posn = 1
```
