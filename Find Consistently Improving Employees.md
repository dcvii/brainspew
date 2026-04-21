---
title: "Find Consistently Improving Employees"
source: "https://leetcode.com/problems/find-consistently-improving-employees/description/?envType=problem-list-v2&envId=database"
author:
published:
created: 2026-04-21
description: "Can you solve this real interview question? Find Consistently Improving Employees - Table: employees+-------------+---------+| Column Name | Type    |+-------------+---------+| employee_id | int     || name        | varchar |+-------------+---------+employee_id is the unique identifier for this table.Each row contains information about an employee.Table: performance_reviews+-------------+------+| Column Name | Type |+-------------+------+| review_id   | int  || employee_id | int  || review_date | date || rating      | int  |+-------------+------+review_id is the unique identifier for this table.Each row represents a performance review for an employee. The rating is on a scale of 1-5 where 5 is excellent and 1 is poor.Write a solution to find employees who have consistently improved their performance over their last three reviews. * An employee must have at least 3 review to be considered * The employee's last 3 reviews must show strictly increasing ratings (each review better than the previous) * Use the most recent 3 reviews based on review_date for each employee * Calculate the improvement score as the difference between the latest rating and the earliest rating among the last 3 reviewsReturn the result table ordered by improvement score in descending order, then by name in ascending order.The result format is in the following example. Example:Input:employees table:+-------------+----------------+| employee_id | name           |+-------------+----------------+| 1           | Alice Johnson  || 2           | Bob Smith      || 3           | Carol Davis    || 4           | David Wilson   || 5           | Emma Brown     |+-------------+----------------+performance_reviews table:+-----------+-------------+-------------+--------+| review_id | employee_id | review_date | rating |+-----------+-------------+-------------+--------+| 1         | 1           | 2023-01-15  | 2      || 2         | 1           | 2023-04-15  | 3      || 3         | 1           | 2023-07-15  | 4      || 4         | 1           | 2023-10-15  | 5      || 5         | 2           | 2023-02-01  | 3      || 6         | 2           | 2023-05-01  | 2      || 7         | 2           | 2023-08-01  | 4      || 8         | 2           | 2023-11-01  | 5      || 9         | 3           | 2023-03-10  | 1      || 10        | 3           | 2023-06-10  | 2      || 11        | 3           | 2023-09-10  | 3      || 12        | 3           | 2023-12-10  | 4      || 13        | 4           | 2023-01-20  | 4      || 14        | 4           | 2023-04-20  | 4      || 15        | 4           | 2023-07-20  | 4      || 16        | 5           | 2023-02-15  | 3      || 17        | 5           | 2023-05-15  | 2      |+-----------+-------------+-------------+--------+Output:+-------------+----------------+-------------------+| employee_id | name           | improvement_score |+-------------+----------------+-------------------+| 2           | Bob Smith      | 3                 || 1           | Alice Johnson  | 2                 || 3           | Carol Davis    | 2                 |+-------------+----------------+-------------------+Explanation: * Alice Johnson (employee_id = 1):   * Has 4 reviews with ratings: 2, 3, 4, 5   * Last 3 reviews (by date): 2023-04-15 (3), 2023-07-15 (4), 2023-10-15 (5)   * Ratings are strictly increasing: 3 → 4 → 5   * Improvement score: 5 - 3 = 2 * Carol Davis (employee_id = 3):   * Has 4 reviews with ratings: 1, 2, 3, 4   * Last 3 reviews (by date): 2023-06-10 (2), 2023-09-10 (3), 2023-12-10 (4)   * Ratings are strictly increasing: 2 → 3 → 4   * Improvement score: 4 - 2 = 2 * Bob Smith (employee_id = 2):   * Has 4 reviews with ratings: 3, 2, 4, 5   * Last 3 reviews (by date): 2023-05-01 (2), 2023-08-01 (4), 2023-11-01 (5)   * Ratings are strictly increasing: 2 → 4 → 5   * Improvement score: 5 - 2 = 3 * Employees not included:   * David Wilson (employee_id = 4): Last 3 reviews are all 4 (no improvement)   * Emma Brown (employee_id = 5): Only has 2 reviews (needs at least 3)The output table is ordered by improvement_score in descending order, then by name in ascending order."
tags:
  - "brain_spew"
---
Description

Description

Editorial

Editorial

Solutions



Table: `employees`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| employee_id | int     |
| name        | varchar |
+-------------+---------+
employee_id is the unique identifier for this table.
Each row contains information about an employee.
```

Table: `performance_reviews`

```
+-------------+------+
| Column Name | Type |
+-------------+------+
| review_id   | int  |
| employee_id | int  |
| review_date | date |
| rating      | int  |
+-------------+------+
review_id is the unique identifier for this table.
Each row represents a performance review for an employee. The rating is on a scale of 1-5 where 5 is excellent and 1 is poor.
```

Write a solution to find employees who have consistently improved their performance over **their last three reviews**.

- An employee must have **at least** `3` **review** to be considered
- The employee's **last** `3` **reviews** must show **strictly increasing ratings** (each review better than the previous)
- Use the most recent `3` reviews based on `review_date` for each employee
- Calculate the **improvement score** as the difference between the latest rating and the earliest rating among the last `3` reviews

Return *the result table ordered by **improvement score** in **descending** order, then by **name** in **ascending** order*.

The result format is in the following example.

**Example:**

**Input:**

employees table:

```
+-------------+----------------+
| employee_id | name           |
+-------------+----------------+
| 1           | Alice Johnson  |
| 2           | Bob Smith      |
| 3           | Carol Davis    |
| 4           | David Wilson   |
| 5           | Emma Brown     |
+-------------+----------------+
```

performance\_reviews table:

```
+-----------+-------------+-------------+--------+
| review_id | employee_id | review_date | rating |
+-----------+-------------+-------------+--------+
| 1         | 1           | 2023-01-15  | 2      |
| 2         | 1           | 2023-04-15  | 3      |
| 3         | 1           | 2023-07-15  | 4      |
| 4         | 1           | 2023-10-15  | 5      |
| 5         | 2           | 2023-02-01  | 3      |
| 6         | 2           | 2023-05-01  | 2      |
| 7         | 2           | 2023-08-01  | 4      |
| 8         | 2           | 2023-11-01  | 5      |
| 9         | 3           | 2023-03-10  | 1      |
| 10        | 3           | 2023-06-10  | 2      |
| 11        | 3           | 2023-09-10  | 3      |
| 12        | 3           | 2023-12-10  | 4      |
| 13        | 4           | 2023-01-20  | 4      |
| 14        | 4           | 2023-04-20  | 4      |
| 15        | 4           | 2023-07-20  | 4      |
| 16        | 5           | 2023-02-15  | 3      |
| 17        | 5           | 2023-05-15  | 2      |
+-----------+-------------+-------------+--------+
```

**Output:**

```
+-------------+----------------+-------------------+
| employee_id | name           | improvement_score |
+-------------+----------------+-------------------+
| 2           | Bob Smith      | 3                 |
| 1           | Alice Johnson  | 2                 |
| 3           | Carol Davis    | 2                 |
+-------------+----------------+-------------------+
```

**Explanation:**

- **Alice Johnson (employee\_id = 1):**
	- Has 4 reviews with ratings: 2, 3, 4, 5
		- Last 3 reviews (by date): 2023-04-15 (3), 2023-07-15 (4), 2023-10-15 (5)
		- Ratings are strictly increasing: 3 → 4 → 5
		- Improvement score: 5 - 3 = 2
- **Carol Davis (employee\_id = 3):**
	- Has 4 reviews with ratings: 1, 2, 3, 4
		- Last 3 reviews (by date): 2023-06-10 (2), 2023-09-10 (3), 2023-12-10 (4)
		- Ratings are strictly increasing: 2 → 3 → 4
		- Improvement score: 4 - 2 = 2
- **Bob Smith (employee\_id = 2):**
	- Has 4 reviews with ratings: 3, 2, 4, 5
		- Last 3 reviews (by date): 2023-05-01 (2), 2023-08-01 (4), 2023-11-01 (5)
		- Ratings are strictly increasing: 2 → 4 → 5
		- Improvement score: 5 - 2 = 3
- **Employees not included:**
	- David Wilson (employee\_id = 4): Last 3 reviews are all 4 (no improvement)
		- Emma Brown (employee\_id = 5): Only has 2 reviews (needs at least 3)

The output table is ordered by improvement\_score in descending order, then by name in ascending order.

---

Seen this question in a real interview before?

1/6

Yes

No

Accepted

12,309/22K

Acceptance Rate

56.0%

---

Topics

[Database](https://leetcode.com/tag/database/)

---

Discussion (24)

💡 Discussion Rules

1\. Please don't post **any solutions** in this discussion.

2\. The problem discussion is for asking questions about the problem or for sharing tips - anything except for solutions.

3\. If you'd like to share your solution for feedback and ideas, please head to the solutions tab and post it there.

[Amogha Mayya](https://leetcode.com/u/AmoghaMayya/)

Jun 11, 2025

WTF is this problem broooooo 🙄🙄

21

Reply

[Apoorva Singh](https://leetcode.com/u/apoorva06singh/)

Jul 05, 2025

what if we have two different reviews on the same day for the same employee? which review should we choose then?

4

Show 3 Replies

Reply

For the tricky part of comparing the ratings and finding out the ratings: latest rating, second latest rating and third latest rating use rating, LEAD(rating, 1), LEAD(rating, 2) respectively. Hope this helps:)

3

Reply

[Kartik Sharma](https://leetcode.com/u/kartikk_sh/)

Aug 14, 2025

pretty tough problem but eventually did it on my own

3

Reply

Some days I feel like I can solve every SQL question easily, the very next day, leetcode punches me with reality with questions like this

2

Reply

its so easy problem did it in 7 mins in 2nd go

1

Reply

[Deepanshu Chauhan](https://leetcode.com/u/deepanshu1710/)

Mar 02, 2026

HINT 1: USE `LEAD`,`RANK` to get first\_prev,second\_prev and most recent review  
HINT 2: use this condtion to filter out `where rank=1 and rating > first_prev and first_prev>second_prev`  
SOLUTION-- [https://leetcode.com/problems/find-consistently-improving-employees/solutions/7620732/easy-solution-lead-cte-by-deepanshu1710-68tw](https://leetcode.com/problems/find-consistently-improving-employees/solutions/7620732/easy-solution-lead-cte-by-deepanshu1710-68tw)

1

Reply

The question is Quiet simple if u are good with the window function:  
first join the two tables  
then  
make use of lead(ratings), lead(ratings,2) to get the previous 2 ratings  
use row\_number() to get the latest record  
use count(\*) for "atleast 3 review" condition

1

Reply

If you use Oracle, use rownumber to pickup most 3, then use Lead to collapse 3 ratings to 1 row, and filter rest with null value. Then join.

Very interesting questions.

1

Reply

WITH RankedReviews AS (  
SELECT  
employee\_id,  
review\_date,  
rating,  
ROW\_NUMBER() OVER (PARTITION BY employee\_id ORDER BY review\_date DESC) AS rn  
FROM performance\_reviews  
),  
LastThreeReviews AS (  
SELECT \*  
FROM RankedReviews  
WHERE rn <= 3  
),  
PivotedReviews AS (  
SELECT  
employee\_id,  
MAX(CASE WHEN rn = 3 THEN rating END) AS rating1,  
MAX(CASE WHEN rn = 2 THEN rating END) AS rating2,  
MAX(CASE WHEN rn = 1 THEN rating END) AS rating3  
FROM LastThreeReviews  
GROUP BY employee\_id  
),  
ImprovingEmployees AS (  
SELECT  
p.employee\_id,  
e.name,  
rating3 - rating1 AS improvement\_score  
FROM PivotedReviews p  
JOIN employees e ON p.employee\_id = e.employee\_id  
WHERE rating1 < rating2 AND rating2 < rating3  
)  
SELECT \*  
FROM ImprovingEmployees  
ORDER BY improvement\_score DESC, name ASC;

1

Reply

7 Online

Saved

Ln 1, Col 1

You must run your code first