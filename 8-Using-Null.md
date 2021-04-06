## Questions Index

* [Ques 1](#ques-1-list-the-teachers-who-have-null-for-their-department)

* [Ques 2](#ques-2-note-the-inner-join-misses-the-teachers-with-no-department-and-the-departments-with-no-teacher)

* [Ques 3](#ques-3-use-a-different-join-so-that-all-teachers-are-listed)

* [Ques 4](#ques-4-use-a-different-join-so-that-all-departments-are-listed)

* [Ques 5](#ques-5-use-coalesce-to-print-the-mobile-number-use-the-number-07986-444-2266-if-there-is-no-number-given-show-teacher-name-and-mobile-number-or-07986-444-2266)

* [Ques 6](#ques-6-use-the-coalesce-function-and-a-left-join-to-print-the-teacher-name-and-department-name-use-the-string-none-where-there-is-no-department)

* [Ques 7](#ques-7-use-count-to-show-the-number-of-teachers-and-the-number-of-mobile-phones)

* [Ques 8](#ques-8-use-count-and-group-by-deptname-to-show-each-department-and-the-number-of-staff-use-a-right-join-to-ensure-that-the-engineering-department-is-listed)

* [Ques 9](#ques-9-use-case-to-show-the-name-of-each-teacher-followed-by-sci-if-the-teacher-is-in-dept-1-or-2-and-art-otherwise)

* [Ques 10](#ques-10-use-case-to-show-the-name-of-each-teacher-followed-by-sci-if-the-teacher-is-in-dept-1-or-2-show-art-if-the-teachers-dept-is-3-and-none-otherwise)


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

### Ques 5. Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no number given. Show teacher name and mobile number or '07986 444 2266'.

```sql
SELECT name, COALESCE(mobile, '07986 444 2266')
FROM teacher
```

### Ques 6. Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.

```sql
SELECT t.name, COALESCE(d.name, 'None')
FROM teacher t
LEFT JOIN dept d ON (t.dept = d.id)
```

### Ques 7. Use COUNT to show the number of teachers and the number of mobile phones.

```sql
SELECT COUNT(name) AS total_teachers,
       COUNT(mobile) AS total_mobiles
FROM teacher
```

### Ques 8. Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.

```sql
SELECT dept.name as department,
       COUNT(teacher.name) AS total_teachers
FROM teacher
RIGHT JOIN dept ON (teacher.dept=dept.id)
GROUP BY dept.name
```

### Ques 9. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.

```sql
SELECT t.name,
       CASE WHEN t.dept IN (1, 2)
            THEN 'Sci'
            ELSE 'Art'
       END AS department
FROM teacher t
LEFT JOIN dept d ON (t.dept=d.id)
```

### Ques 10. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.

```sql
SELECT t.name,
       CASE WHEN t.dept IN (1, 2)
            THEN 'Sci'
            WHEN t.dept = 3
            THEN 'Art'
            ELSE 'None'
        END AS department
FROM teacher t
LEFT JOIN dept d ON (t.dept=d.id)
```
