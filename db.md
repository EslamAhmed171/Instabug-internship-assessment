# Instabug-internship-assessment
This setion contains solutions to the problems of Instabug internship assessment db section.

## Problem 1: Find top 100 students!
Given 3 tables, students(id, name) , courses(id, name) , grades(id, course_id, student_id, grade), find the top 100 students based on their average grades sorted descendingly by the average grade and in case multiple students have the same average grade, sort them lexicographically in ascending order by their names.
Your query should output a table with the following columns (name, average_grade).

### Solution:
```sql
SELECT 
    x.name AS name, 
    AVG(y.grade) AS average_grade 
FROM 
    students x
LEFT JOIN 
    grades y ON x.id = y.student_id
GROUP BY 
    x.name
ORDER BY 
    AVG(grade) DESC, x.name ASC
LIMIT 
    100
```

## Problem 2: Generate students grade report!
Given 3 tables, students(id, name) , courses(id, name) , grades(id, course_id, student_id, grade), for each student, get all the courses that he/she is enrolled in along with the grade he/she scored for each course. Order the result by the student name in ascending order and if there is a tie, break it with the course name in ascending order and if there is a tie break it with the grade in ascending order.
The final result should have 3 columns with names (name, course, grade).

### Solution:

```sql
SELECT DISTINCT 
    x.name AS name,
    z.name AS course,
    y.grade AS grade 
FROM 
    students x
JOIN 
    grades y ON x.id = y.student_id
JOIN 
    courses z ON z.id = y.course_id
ORDER BY 
    x.name ASC, 
    z.name ASC, 
    y.grade ASC
```

## Problem 3: Find the most popular course!
Given 3 tables, students(id, name) , courses(id, name) , grades(id, course_id, student_id, grade), get the name of the most popular course (the one where the most students are enrolled) and if there is a tie, get the course that's lexicographically the smallest.

### Solution:

```sql
SELECT x.name
    FROM courses x
JOIN
    grades y ON x.id = y.course_id
GROUP BY
    x.id, x.name
ORDER BY
    COUNT(*) DESC, x.name ASC
LIMIT 1
```

## Problem 4: What are the catergories of bugs we have?
Given a table called "bugs" with the following columns (id, token, title, category, device, reported_at, created_at, updated_at). Select all distinct bug categories.

### Solution:

```sql
SELECT DISTINCT category FROM bugs
```

## Problem 5: Count em bugs!
Note: Naive solution didn't pass, as the table has 10 million records. I used the available indexes i have in the database and I'm not sure if my solution is optimal.
Given a table called "bugs" with the following columns (id, token, title, category, device, reported_at, created_at, updated_at), find how many bugs were created on "2019-03-01" or later. Your query should produce a table with one column called "count".

### Solution:

```sql
SELECT
    COUNT(y.created_at) AS count 
FROM
    bugs AS x
JOIN
    bugs AS y ON x.id = y.id USE INDEX
    (PRIMARY, index_bugs_on_category_and_token_and_reported_at) 
WHERE
    y.created_at >= '2019-03-01'
```

## Problem 6: Find the title!
Note: Naive solution didn't pass, as the table has 10 million records. I used the available indexes i have in the database and I'm not sure if my solution is optimal.
Given a table called "bugs" with the following columns (id, token, title, category, device, reported_at, created_at, updated_at), find the title of the bug with token = "token660" and reported_at on "2020-08-30".

### Solution:

```sql
SELECT
    x.title
FROM
    bugs AS x
JOIN
    bugs AS y ON x.id = y.id USE INDEX
    (PRIMARY, index_bugs_on_category_and_token_and_reported_at) 
WHERE
    x.token ='token660' AND x.reported_at = '2020-08-30' 
```







