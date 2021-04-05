## Questions Index

* [Ques 1](#ques-1-list-the-teachers-who-have-null-for-their-department)

* [Ques 2](#ques-2-note-the-inner-join-misses-the-teachers-with-no-department-and-the-departments-with-no-teacher)

* [Ques 3](#ques-3-use-a-different-join-so-that-all-teachers-are-listed)

* [Ques 4](#ques-4-use-a-different-join-so-that-all-departments-are-listed)


### Ques 1. List the teachers who have NULL for their department.

```sql
SELECT name
FROM teacher
WHERE dept IS NULL
```

### Ques 2. Note the INNER JOIN misses the teachers with no department and the departments with no teacher.

```sql
SELECT teacher.name, dept.name
FROM teacher
INNER JOIN dept ON (teacher.dept=dept.id)
```

### Ques 3. Use a different JOIN so that all teachers are listed.

```sql
SELECT teacher.name, dept.name
FROM teacher
LEFT JOIN dept ON (teacher.dept=dept.id)
```

### Ques 4. Use a different JOIN so that all departments are listed.

```sql
SELECT teacher.name, dept.name
FROM teacher
RIGHT JOIN dept ON (teacher.dept=dept.id)
```
