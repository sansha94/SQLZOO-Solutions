## Questions Index

* [Ques 1](#ques-1-show-the-the-percentage-who-strongly-agree)

* [Ques 2](#ques-2-show-the-institution-and-subject-where-the-score-is-at-least-100-for-question-15)

* [Ques 3](#ques-3-show-the-institution-and-score-where-the-score-for-8-computer-science-is-less-than-50-for-question-q15)

* [Ques 4](#ques-4-show-the-subject-and-total-number-of-students-who-responded-to-question-22-for-each-of-the-subjects-8-computer-science-and-h-creative-arts-and-design)

* [Ques 5](#ques-5-show-the-subject-and-total-number-of-students-who-a_strongly_agree-to-question-22-for-each-of-the-subjects-8-computer-science-and-h-creative-arts-and-design)


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

### Ques 3. Show the institution and score where the score for '(8) Computer Science' is less than 50 for question 'Q15'.

```sql
SELECT institution, score
FROM nss
WHERE subject='(8) Computer Science'
  AND question='Q15'
  AND score < 50
```

### Ques 4. Show the subject and total number of students who responded to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'.

```sql
SELECT subject, SUM(response) AS total_students
FROM nss
WHERE subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
  AND question='Q22'
GROUP BY subject
```

### Ques 5. Show the subject and total number of students who A_STRONGLY_AGREE to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'.

```sql
SELECT subject, SUM(response*A_STRONGLY_AGREE/100) AS total_students
FROM nss
WHERE subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
  AND question='Q22'
GROUP BY subject
```
