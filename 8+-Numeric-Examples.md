## Questions Index

* [Ques 1](#ques-1-show-the-the-percentage-who-strongly-agree)

* [Ques 2](#ques-2-show-the-institution-and-subject-where-the-score-is-at-least-100-for-question-15)


### Ques 1. Show the the percentage who STRONGLY AGREE.

```sql
SELECT A_STRONGLY_AGREE
FROM nss
WHERE question='Q01'
AND institution='Edinburgh Napier University'
AND subject='(8) Computer Science'
```

### Ques 2. Show the institution and subject where the score is at least 100 for question 15.

```sql
SELECT institution, subject
FROM nss
WHERE question='Q15' AND score >= 100
```
