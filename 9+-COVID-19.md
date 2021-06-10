## Questions Index

* [Ques 1](#ques-1-modify-the-query-to-show-data-from-spain)


### Ques 1. Modify the query to show data from Spain.

```sql
SELECT name, DAY(whn), confirmed,
       deaths, recovered
FROM covid
WHERE name = 'Spain'
  AND MONTH(whn) = 3
ORDER BY whn
```
