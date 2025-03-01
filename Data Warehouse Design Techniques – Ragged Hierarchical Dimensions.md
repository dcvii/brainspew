---
title: "Data Warehouse Design Techniques – Ragged Hierarchical Dimensions"
source: "https://bigbear.ai/blog/data-warehouse-design-techniques-ragged-hierarchical-dimensions/"
author:
  - "[[BigBear.ai]]"
published: 2022-01-27
created: 2025-02-21
description: "This post will discuss how to handle those ragged hierarchies, those which can skip levels in the hierarchy."
tags:
  - "database_design"
---
In my last post, we discussed the creation of simple hierarchical dimensions. In this post, I will discuss how to handle those ragged hierarchies, those which can skip levels in the hierarchy.

**Snowflaking**

There may be instances where you wish to normalize the hierarchy into a snowflake. Below is a city, state/province, country hierarchy which can easily be converted into a snowflake model.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P5-300x169.gif)

Here we would simply take the list of all of the countries and place them into a country dimension, the state/provinces into a state/province table and finally a city into a city table. While loading these dimensions, you must remember to carry the parent and grandparent IDs along. Therefore, the city dimension will reference the state table where appropriate and the country table (always) while the state/province table will only reference the country dimension.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P2-183x300.png)

**Flatten Hierarchy**

One way to handle the ragged hierarchy is to flatten the hierarchy just as we did in the simple dimensional hierarchy and copy the grandparent level data down to the parent level. This copying of this “pseudo data” into the columns where the hierarchy is skipped is done to balance any skipped hierarchy level. The “pseudo data” can also include a flag telling the user that the connection between the child record and the parent needs to be skipped and instead moved up to the next level (grandparent).

Let’s look at a classification example.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P3-300x88.png)

As you can see from the example above not all classifications refer to sub-types but rather point directly to a type. To resolve this issue for consistent reporting at the sub-type tier we would simply copy the type record data down to the sub-type tier to “cover” the missing data in the sub-type tier. Remember it is helpful to set the flag indicating that this data is pseudo data and only used to ensure create a flattened hierarchy.

**Recursion**

Another way to work with a ragged hierarchy is to use a recursion to address the recursive hierarchy. Recursion is created when the child record has a relationship to the parent record as an attribute of the child record.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P4-300x147.png)

This is the simplest and most flexible solution to address the challenge of a ragged hierarchy. Like all solutions, there are some challenges with using a recursion as a solution. The major challenges with recursion are the query performance and the limited number of reporting tools that can execute a recursion query.

**Hierarchical Bridge Table**

Hierarchical bridge tables are incredibly powerful hierarchical tools. Below is a standard organization chart. If you wanted to see all of the people who report to Shavonne or find the list of management above Duncan, a hierarchical bridge table makes this request effortless.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P5-300x169.gif)

To create a hierarchy bridge table you will create a table consisting of each record associated with itself and its association with all of its subordinates regardless of level. You should also capture the number of levels removed from itself and flags indicating if this is the top of the hierarchy or the bottom of the hierarchy. Here is an example of the data for Quinton.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P6-300x189.png)

Once this table is created you can quickly find all of the people who work under Quinton or what is the management chain above Eugene with a simple select statement.

Combining the hierarchy bridge table with a fact table request enhances the power of the reports you can generate. Let’s take a look at how we can use the hierarchy bridge table. When looking at creating a report from the top down we would join the Employee\_Key on the fact table to the Subordinate\_ID on the hierarchy bridge table which would then join to the Employee\_ID on the Employee dimension to the Superior\_Key from the hierarchy bridge table.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P7-300x67.png)

In a similar way when wishing to create an ascending report (bottom up) we would join the Employee\_Key on the fact table to the Superior\_ID on the hierarchy bridge table which would then join to the Employee\_ID on the Employee dimension to the Subordinate\_Key from the hierarchy bridge table.

![](https://bigbear.ai/wp-content/uploads/2022/01/A2-P8-300x67.png)

As you can see the hierarchy bridge table has removed the recursive join and replaced it with better performing, simple joins. You can also use the levels to help limit the number of levels above or below the current employee you wish to traverse.

Not all reporting tools can use the power of the hierarchy bridge table, in those cases I recommend using recursive hierarchies, if possible, before settling on a flattened hierarchy with pseudo data to meet your user requirements.

About the Author

**Jim McHugh** is the Vice President of National Intelligence Service – Emerging Markets Portfolio. Jim is responsible for the delivery of Analytics and Data Management to the Intelligence Community.