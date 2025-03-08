---
title: "SQL Basics Cheat Sheet"
source: "https://learnsql.com/blog/sql-basics-cheat-sheet/#left-join"
author:
  - "[[LearnSQL.com Team]]"
published: 2020-09-25
created: 2025-02-24
description: "This 2-page SQL Basics Cheat Sheet will be a great value for beginners as well as for professionals. Download it in PDF or PNG format."
tags:
  - "clippings"
---
*Download this 2-page SQL Basics Cheat Sheet in PDF or PNG format, print it out, and stick to your desk.*

The *SQL Basics Cheat Sheet* provides you with the syntax of all basics clauses, shows you how to write different conditions, and has examples. You can download this cheat sheet as follows:

**SQL**, or *Structured Query Language*, is a language to talk to databases. It allows you to select specific data and to build complex reports. Today, SQL is a universal language of data. It is used in practically all technologies that process data.

## Sample data

![Sample data tables](https://learnsql.com/blog/sql-basics-cheat-sheet/01-sample-data.png)

## Querying single table

Fetch all columns from the `country` table:

```
SELECT *
FROM country;
```

Fetch `id` and `name` columns from the `city` table:

```
SELECT id, name
FROM city;
```

Fetch city names sorted by the `rating` column in the default ASCending order:

```
SELECT name
FROM city
ORDER BY rating [ASC];
```

Fetch city names sorted by the `rating` column in the DESCending order:

```
SELECT name
FROM city
ORDER BY rating DESC;
```

## Aliases

### Columns

```
SELECT name AS city_name
FROM city;
```

### Tables

```
SELECT co.name, ci.name
FROM city AS ci
JOIN country AS co
  ON ci.country_id = co.id;
```

## Filtering the output

### Comparison operators

Fetch names of cities that have a rating above 3:

```
SELECT name
FROM city
WHERE rating > 3;
```

Fetch names of cities that are neither Berlin nor Madrid:

```
SELECT name
FROM city
WHERE name != 'Berlin'
  AND name != 'Madrid';
```

### Text operators

Fetch names of cities that start with a 'P' or end with an 's':

```
SELECT name
FROM city
WHERE name LIKE 'P%'
  OR name LIKE '%s';
```

Fetch names of cities that start with any letter followed by 'ublin' (like Dublin in Ireland or Lublin in Poland):

```
SELECT name
FROM city
WHERE name LIKE '_ublin';
```

### Other operators

Fetch names of cities that have a population between 500K and 5M:

```
SELECT name
FROM city
WHERE population BETWEEN 500000 AND 5000000;
```

Fetch names of cities that don't miss a rating value:

```
SELECT name
FROM city
WHERE rating IS NOT NULL;
```

Fetch names of cities that are in countries with IDs 1, 4, 7, or 8:

```
SELECT name
FROM city
WHERE country_id IN (1, 4, 7, 8);
```

## Querying multiple tables

### INNER JOIN

**`JOIN`** (or explicitly **`INNER JOIN`**) returns rows that have matching values in both tables.

```
SELECT city.name, country.name
FROM city
[INNER] JOIN country
  ON city.country_id = country.id;
```
![Tables joined using INNER JOIN](https://learnsql.com/blog/sql-basics-cheat-sheet/02-inner-join.png)

### LEFT JOIN

**`LEFT JOIN`** returns all rows from the left table with corresponding rows from the right table. If there's no matching row, **`NULL`**s are returned as values from the second table.

```
SELECT city.name, country.name
FROM city
LEFT JOIN country
  ON city.country_id = country.id;
```
![Tables joined using LEFT JOIN](https://learnsql.com/blog/sql-basics-cheat-sheet/03-left-join.png)

### RIGHT JOIN

**`[RIGHT JOIN](https://learnsql.com/blog/right-join/)`** returns all rows from the right table with corresponding rows from the left table. If there's no matching row, **`NULL`**s are returned as values from the left table.

```
SELECT city.name, country.name
FROM city
RIGHT JOIN country
  ON city.country_id = country.id;
```
![Tables joined using RIGHT JOIN](https://learnsql.com/blog/sql-basics-cheat-sheet/04-right-join.png)

### FULL JOIN

**`FULL JOIN`** (or explicitly **`FULL OUTER JOIN`**) returns all rows from both tables – if there's no matching row in the second table, **`NULL`**s are returned.

```
SELECT city.name, country.name
FROM city
FULL [OUTER] JOIN country
  ON city.country_id = country.id;
```
![Tables joined using FULL JOIN](https://learnsql.com/blog/sql-basics-cheat-sheet/05-full-join.png)

### CROSS JOIN

**`CROSS JOIN`** returns all possible combinations of rows from both tables. There are two syntaxes available.

```
SELECT city.name, country.name
FROM city
CROSS JOIN country;

SELECT city.name, country.name
FROM city, country;
```
![Tables joined using CROSS JOIN](https://learnsql.com/blog/sql-basics-cheat-sheet/06-cross-join.png)

### NATURAL JOIN

**`NATURAL JOIN`** will join tables by all columns with the same name.

```
SELECT city.name, country.name
FROM city
NATURAL JOIN country;
```
![Tables joined using NATURAL JOIN](https://learnsql.com/blog/sql-basics-cheat-sheet/07-natural-join.png)

**`NATURAL JOIN`** used these columns to match rows:  
**`city.id`**, **`city.name`**, **`country.id`**, **`country.name`**.  
**`NATURAL JOIN`** is very rarely used in practice.

## Aggregation and grouping

`GROUP BY` **groups** together rows that have the same values in specified columns. It computes summaries (aggregates) for each unique combination of values.

![Table before and after aggregation](https://learnsql.com/blog/sql-basics-cheat-sheet/08-aggregation.png)

### Aggregate functions

- `avg(expr)` − average value for rows within the group
- `count(expr)` − count of values for rows within the group
- `max(expr)` − maximum value within the group
- `min(expr)` − minimum value within the group
- `sum(expr)` − sum of values within the group

### Example queries

Find out the number of cities:

```
SELECT COUNT(*)
FROM city;
```

Find out the number of cities with non-null ratings:

```
SELECT COUNT(rating)
FROM city;
```

Find out the number of distinctive country values:

```
SELECT COUNT(DISTINCT country_id)
FROM city;
```

Find out the smallest and the greatest country populations:

```
SELECT MIN(population), MAX(population)
FROM country;
```

Find out the total population of cities in respective countries:

```
SELECT country_id, SUM(population)
FROM city
GROUP BY country_id;
```

Find out the average rating for cities in respective countries if the average is above 3.0:

```
SELECT country_id, AVG(rating)
FROM city
GROUP BY country_id
HAVING AVG(rating) > 3.0;
```

## Subqueries

A subquery is a query that is nested inside another query, or inside another subquery. There are different types of subqueries.

### Single value

The simplest subquery returns exactly one column and exactly one row. It can be used with comparison operators `=`, `<`, `<=`, `>`, or `>=`.

This query finds cities with the same rating as Paris:

```
SELECT name
FROM city
WHERE rating = (
  SELECT rating
  FROM city
  WHERE name = 'Paris'
);
```

### Multiple values

A subquery can also return multiple columns or multiple rows. Such subqueries can be used with operators `IN`, `EXISTS`, `ALL`, or `ANY`.

This query finds cities in countries that have a population above 20M:

```
SELECT name
FROM city
WHERE country_id IN (
  SELECT country_id
  FROM country
  WHERE population > 20000000
);
```

### Correlated

A correlated subquery refers to the tables introduced in the outer query. A correlated subquery depends on the outer query. It cannot be run independently from the outer query.

This query finds cities with a population greater than the average population in the country:

```
SELECT *
FROM city main_city
WHERE population > (
  SELECT AVG(population)
  FROM city average_city
  WHERE average_city.country_id = main_city.country_id
);
```

This query finds countries that have at least one city:

```
SELECT name
FROM country
WHERE EXISTS (
  SELECT *
  FROM city
  WHERE country_id = country.id
);
```

## Set operations

Set operations are used to combine the results of two or more queries into a single result. The combined queries must return the same number of columns and compatible data types. The names of the corresponding columns can be different

![Sample data for set operations](https://learnsql.com/blog/sql-basics-cheat-sheet/09-sets-data.png)

### UNION

**`UNION`** combines the results of two result sets and removes duplicates. **`UNION ALL`** doesn't remove duplicate rows.

This query displays German cyclists together with German skaters:

```
SELECT name
FROM cycling
WHERE country = 'DE'
UNION / UNION ALL
SELECT name
FROM skating
WHERE country = 'DE';
```
![UNION circles](https://learnsql.com/blog/sql-basics-cheat-sheet/10-union.png)

### INTERSECT

**`INTERSECT`** returns only rows that appear in both result sets.

This query displays German cyclists who are also German skaters at the same time:

```
SELECT name
FROM cycling
WHERE country = 'DE'
INTERSECT
SELECT name
FROM skating
WHERE country = 'DE';
```
![INTERSECT circles](https://learnsql.com/blog/sql-basics-cheat-sheet/11-intersect.png)

### EXCEPT

**`EXCEPT`** returns only the rows that appear in the first result set but do not appear in the second result set.

This query displays German cyclists unless they are also German skaters at the same time:

```
SELECT name
FROM cycling
WHERE country = 'DE'
EXCEPT / MINUS
SELECT name
FROM skating
WHERE country = 'DE';
```
![EXCEPT circles](https://learnsql.com/blog/sql-basics-cheat-sheet/12-except.png)