## Questions Index

* [Ques 1](#ques-1-show-the-lastname-party-and-votes-for-the-constituency-s14000024-in-2017)

* [Ques 2](#ques-2-show-the-party-and-rank-for-constituency-s14000024-in-2017-list-the-output-by-party)


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
