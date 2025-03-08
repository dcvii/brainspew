---
title: "SQL Recap for Interviews"
source: "https://medium.com/towards-data-science/sql-cheat-sheet-for-interviews-6e5981fa797b"
author:
  - "[[Vijini Mallawaarachchi]]"
published: 2017-09-15
created: 2025-02-25
description: "SQL or Structured Query Language is a language designed to manage data in a Relational Database Management System (RDBMS). In this article, I will be walking you through the commonly used SQL…"
tags:
  - "clippings"
---
## Querying Related Commands

## 13\. SELECT

The **SELECT** statement is used to select data from a particular table.

```
SELECT <col_name1>, <col_name2>, …
     FROM <table_name>;
```

You can select all the contents of a table as follows. Refer Figure 4 as well.

```
SELECT * FROM <table_name>;
```
![](https://miro.medium.com/v2/resize:fit:700/1*KE0JHUoXlYP7qZhv167R7A.png)

Figure 4: Select all from ***department*** and **course** tables

## 14\. SELECT DISTINCT

A column of a table can often contain duplicate values. **SELECT DISTINCT** allows you to retrieve the distinct values.

```
SELECT DISTINCT <col_name1>, <col_name2>, …
     FROM <table_name>;
```
![](https://miro.medium.com/v2/resize:fit:700/1*6slQLk4XK_DOyiTx5uPQUQ.png)

Figure 5: **SELECT DISTINCT** example

## 15\. WHERE

You can use **WHERE** keyword in a **SELECT** statement in order to include conditions for your data.

```
SELECT <col_name1>, <col_name2>, …
     FROM <table_name>
     WHERE <condition>;
```

You can include conditions consisting of,

- Comparison of **text**
- Comparison of **numbers**
- Logical operations including **AND**, **OR** and **NOT**.

## **Example**

Go through the following example statements. Note how conditions have been included with the **WHERE** clause.

```
SELECT * FROM course WHERE dept_name=’Comp. Sci.’;
SELECT * FROM course WHERE credits>3;
SELECT * FROM course WHERE dept_name='Comp. Sci.' AND credits>3;
```
![](https://miro.medium.com/v2/resize:fit:700/1*WG9bGaM_jfCXHnKf8lnWUQ.png)

Figure 6: Usage of **WHERE** in **SELECT**

## 16\. GROUP BY

The **GROUP BY** statement is often used with **aggregate functions** such as **COUNT**, **MAX**, **MIN**, **SUM** and **AVG** to group the result-set.

```
SELECT <col_name1>, <col_name2>, …
     FROM <table_name>
     GROUP BY <col_namex>;
```

## **Example**

List the number of courses for each department.

```
SELECT COUNT(course_id), dept_name 
     FROM course 
     GROUP BY dept_name;
```
![](https://miro.medium.com/v2/resize:fit:700/1*fKp_hj9KtqCbSSZzDlM9Hg.png)

Figure 7: **Number of courses** for each **department**

## 17\. HAVING

==The== ==**HAVING**== ==clause was introduced to SQL because the== ==**WHERE**== ==keyword could not be used to compare values of== ==**aggregate functions**====.==

```
SELECT <col_name1>, <col_name2>, ...
    FROM <table_name>
    GROUP BY <column_namex>
    HAVING <condition>
```

## **Example**

List the number of courses for each department which offers more than one course.

```
SELECT COUNT(course_id), dept_name 
    FROM course 
    GROUP BY dept_name 
    HAVING COUNT(course_id)>1;
```
![](https://miro.medium.com/v2/resize:fit:700/1*cqNFuoVCDDgJQB3t0Fmq5w.png)

Figure 8: **Departments** offering more than one **course**

## **18\. ORDER BY**

**ORDER BY** is used to **sort a result set in ascending or descending order**. ORDER BY will sort in ascending order if you do not specify ASC or DESC.

```
SELECT <col_name1>, <col_name2>, …
FROM <table_name>
ORDER BY <col_name1>, <col_name2>, … ASC|DESC;
```

## **Example**

List the courses in ascending and descending order of number of credits.

```
SELECT * FROM course ORDER BY credits;
SELECT * FROM course ORDER BY credits DESC;
```
![](https://miro.medium.com/v2/resize:fit:700/1*sW0wA_Uchc2-v2VUOCwmdA.png)

Figure 9: **Courses** sorted according to **credits**

## 19\. BETWEEN

**BETWEEN** clause is used to **select data within a given range**. The values can be numbers, text or even dates.

```
SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <col_namex> BETWEEN <value1> AND <value2>;
```

## **Example**

List the instructors who get a salary in between 50 000 and 100 000.

```
SELECT * FROM instructor 
    WHERE salary BETWEEN 50000 AND 100000;
```
![](https://miro.medium.com/v2/resize:fit:700/1*Exndq_gYcFTdDDnIZ7jjTA.png)

Figure 10: **Instructors** who get a salary in between 50 000 and 100 000

## 20\. LIKE

The **LIKE** operator is used in a **WHERE** clause to search for a **specified pattern in text**.

There are two wildcard operators used with LIKE.

- **%** (Zero, one, or multiple characters)
- **\_** (A single character)

```
SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <col_namex> LIKE <pattern>;
```

## Example

List the courses where the course name contains “to” and the courses where the course\_id starts with “CS-”.

```
SELECT * FROM course WHERE title LIKE ‘%to%’;
SELECT * FROM course WHERE course_id LIKE 'CS-___';
```
![](https://miro.medium.com/v2/resize:fit:700/1*bZ9pg4m8LL2MuRcNrlamoA.png)

Figure 11: Use of **wildcard operators** with **LIKE**

## 21\. IN

Using **IN** clause, you can allow **multiple values within a WHERE clause**.

```
SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <col_namen> IN (<value1>, <value2>, …);
```

## Example

List the students in the departments of Comp. Sci., Physics, and Elec. Eng.

```
SELECT * FROM student 
    WHERE dept_name IN (‘Comp. Sci.’, ‘Physics’, ‘Elec. Eng.’);
```
![](https://miro.medium.com/v2/resize:fit:700/1*i6uuZfV3jdri4DmfdvJkkQ.png)

Figure 12: **Students** in the **departments** of Comp. Sci., Physics, and Elec. Eng

## 22\. JOIN

**JOIN** is used to combine values of two or more tables based on common attributes within them. Figure 13 given below depicts the different types of SQL joins. Note the difference between **LEFT OUTER JOIN** and **RIGHT OUTER JOIN**.

```
SELECT <col_name1>, <col_name2>, …
    FROM <table_name1>
    JOIN <table_name2> 
    ON <table_name1.col_namex> = <table2.col_namex>;
```

## Example 1

Select all the courses with relevant department details.

```
SELECT * FROM course 
    JOIN department 
    ON course.dept_name=department.dept_name;
```
![](https://miro.medium.com/v2/resize:fit:700/1*unyp1mwbjq7kx75e3cV4sg.png)

Figure 14: All the **courses** with **department** details

## Example 2

Select all the prerequisite courses with their course details.

```
SELECT prereq.course_id, title, dept_name, credits, prereq_id 
    FROM prereq 
    LEFT OUTER JOIN course 
    ON prereq.course_id=course.course_id;
```
![](https://miro.medium.com/v2/resize:fit:700/1*acF6tqM0-PSelx5zTz_TXg.png)

Figure 15: All the **prerequisite** courses with their **course** details

## Example 3

Select all the courses with their course details, regardless of whether or not they have prerequisites.

```
SELECT course.course_id, title, dept_name, credits, prereq_id 
    FROM prereq 
    RIGHT OUTER JOIN course 
    ON prereq.course_id=course.course_id;
```
![](https://miro.medium.com/v2/resize:fit:700/1*JDVJnbkrjYB7YjDO_JT66g.png)

Figure 16: All the **courses** with their course details, regardless of whether or not they have **prerequisites**

## 23\. Views

Views are virtual SQL tables created using a result set of a statement. It contains rows and columns and is very similar to a general SQL table. A view always shows up-to-date data within the database.

## CREATE VIEW

```
CREATE VIEW <view_name> AS
    SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <condition>;
```

## DROP VIEW

```
DROP VIEW <view_name>;
```

## Example

Create a view consisting of courses with 3 credits.

![](https://miro.medium.com/v2/resize:fit:700/1*OuOCqwtXZgpKsa_7x3kESA.png)

Figure 17: A **view** consisting of **courses** with **3 credits**

## 24\. Aggregate Functions

These functions are used to obtain a cumulative result relevant to the data being considered. Following are the commonly used aggregate functions.

- **COUNT(col\_name)** — Returns the number of rows
- **SUM(col\_name)** — Returns the sum of the values in a given column
- **AVG (col\_name)**— Returns the average of the values of a given column
- **MIN(col\_name)** — Returns the smallest value of a given column
- **MAX(col\_name)** — Returns the largest value of a given column

## 25\. Nested Subqueries

Nested subqueries are SQL queries which include a **SELECT-FROM-WHERE** expression that is nested within another query.

## Example

Find courses offered in Fall 2009 and in Spring 2010.

```
SELECT DISTINCT course_id 
    FROM section 
    WHERE semester = ‘Fall’ AND year= 2009 AND course_id IN (
        SELECT course_id 
            FROM section 
            WHERE semester = ‘Spring’ AND year= 2010
    );
```
![](https://miro.medium.com/v2/resize:fit:700/1*zQ4mCPqbS50Nj7LgFgPE4A.png)

Figure 18: **Courses** offered in **Fall 2009** and in **Spring 2010**