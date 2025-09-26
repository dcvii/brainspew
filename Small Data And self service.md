---
title: "Small Data And self service"
source: "https://datamonkeysite.com/"
author:
  - "[[Small Data And self service]]"
published: 2025-03-19
created: 2025-04-07
description: "PowerBI & Fabric and Data in General"
tags:
  - "clippings"
---
[![LLMs Are Getting Better at SQL](https://datamonkeysite.com/wp-content/uploads/2025/03/image.png?w=1200)](https://datamonkeysite.com/2025/03/07/llms-are-getting-better-at-sql/)

For no particular reason, I recently opened a Power BI report with two fact tables, exported the model definition to TMDL, saved it as a file, and loaded it into several state-of-the-art LLMs, including ChatGPT, Grok, Anthropic, and Qwen QWQ. I wasn’t particularly interested in comparing specific models—I just wanted to get a general sense of how they performed. To keep things simple, I used only the free tiers.

To my surprise, these models are getting really smart. They all recognized that the file represented a Power BI semantic model. They understood the concept of tables, columns, relationships, and measures, which was quite impressive.

You can [download the Model here](https://github.com/djouallah/Fabric_Notebooks_Demo/tree/main/SemanticModel), i added a semantic Model as a text file in case you don’t have PowerBI

## The Power of Semantic Models

Power BI, and before that PowerPivot, has supported multiple fact tables from day one. I remember the first time I used PowerPivot— a colleague showed me how to handle multiple fact tables: just don’t join fact to fact. Instead, use a common dimension, and everything will work fine. Back then, I had no idea about Kimball, multi-stage SQL queries, chasm trap etc. As a business user, I only cared that I got the correct results. It took me years to appreciate the ingenuity and engineering that went into making this work seamlessly. To me, this is an example of great product design: solve a very hard problem, and people will use it.

But this blog isn’t about Power BI and DAX—that’s a solved problem. Instead, I wanted to explore whether LLMs, by reading only metadata, could generate correct SQL queries for relatively complex questions.

Note: for people not familiar with TMDL, it is a human readable format of PowerBI semantic Model ( if human can read it, then LLMs will understand it too)

## Testing LLMs with SQL Generation

I started with simple queries involving only one fact table, and the results were straightforward. The models correctly referenced measure definitions, avoiding column name hallucinations. Good news so far.

Things got more interesting when I asked for a query using a more complex measure, such as **Net Sales**:

```js
Net Sales = [Total Sales] - [Total Returns]
```

This measure involves two tables: `store_sales` and `store_returns`.

### Expected SQL Approach: Drilling Across

My expectation was that the models would use the [**Drilling Across** technique](https://www.kimballgroup.com/2003/04/the-soul-of-the-data-warehouse-part-two-drilling-across/). For example, when asked for net sales and cumulative sales by year and brand, a well-structured query would look like this:

1. Compute total sales by year and brand.
2. Compute total returns by year and brand.
3. Join these results on year and brand.
4. Calculate net sales as `[Total Sales] - [Total Returns]`.
5. Calculate cumulative Sales

Most LLMs generated a similar approach. Some required a hint (“don’t ever join fact to fact”), but the biggest issue was the final join. Many models defaulted to a **LEFT JOIN**, which is problematic—some returns for a brand might not occur in the same period as the sales, leading to incomplete results.

That said, some models got it right on the first attempt, which was very impressive. something like this:

```js
WITH sales AS (
    SELECT
        d.d_year,
        i.i_brand,
        SUM(s.ss_sales_price * s.ss_quantity) AS total_sales
    FROM store_sales s
    JOIN item i ON s.ss_item_sk = i.i_item_sk
    JOIN date_dim d ON s.ss_sold_date_sk = d.d_date_sk
    GROUP BY d.d_year, i.i_brand
),
returns AS (
    SELECT
        d.d_year,
        i.i_brand,
        SUM(r.sr_return_amt) AS total_returns
    FROM store_returns r
    JOIN item i ON r.sr_item_sk = i.i_item_sk
    JOIN date_dim d ON r.sr_returned_date_sk = d.d_date_sk
    GROUP BY d.d_year, i.i_brand
)
SELECT
    COALESCE(s.d_year, r.d_year) AS year,
    COALESCE(s.i_brand, r.i_brand) AS brand,
    COALESCE(s.total_sales, 0) AS total_sales,
    COALESCE(r.total_returns, 0) AS total_returns,
    (COALESCE(s.total_sales, 0) - COALESCE(r.total_returns, 0)) AS net_sales,
    SUM(COALESCE(s.total_sales, 0) - COALESCE(r.total_returns, 0))
        OVER (PARTITION BY COALESCE(s.i_brand, r.i_brand) ORDER BY COALESCE(s.d_year, r.d_year)
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cumulative_net_sales
FROM sales s
FULL OUTER JOIN returns r
ON s.d_year = r.d_year AND s.i_brand = r.i_brand
ORDER BY COALESCE(s.i_brand, r.i_brand), COALESCE(s.d_year, r.d_year);
```

### An Alternative Approach: UNION ALL

One LLM got creative and proposed a different solution using **UNION ALL**:

```js
WITH combined AS (
    SELECT d.d_year, i.i_brand, 'sales' AS type, s.ss_sales_price * s.ss_quantity AS amount
    FROM store_sales s
    JOIN date_dim d ON s.ss_sold_date_sk = d.d_date_sk
    JOIN item i ON s.ss_item_sk = i.i_item_sk
    UNION ALL
    SELECT d.d_year, i.i_brand, 'returns' AS type, r.sr_return_amt AS amount
    FROM store_returns r
    JOIN date_dim d ON r.sr_returned_date_sk = d.d_date_sk
    JOIN item i ON r.sr_item_sk = i.i_item_sk
)
SELECT
    d_year AS year,
    i_brand AS brand,
    SUM(CASE WHEN type = 'sales' THEN amount ELSE 0 END) AS total_sales,
    SUM(CASE WHEN type = 'returns' THEN amount ELSE 0 END) AS total_returns,
    (SUM(CASE WHEN type = 'sales' THEN amount ELSE 0 END) - SUM(CASE WHEN type = 'returns' THEN amount ELSE 0 END)) AS net_sales,
    SUM(SUM(CASE WHEN type = 'sales' THEN amount ELSE 0 END) - SUM(CASE WHEN type = 'returns' THEN amount ELSE 0 END))
        OVER (PARTITION BY i_brand ORDER BY d_year ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cumulative_net_sales
FROM combined
GROUP BY d_year, i_brand
ORDER BY i_brand, d_year;
```

***Edit: people who know what they are doing, did not like the union all solution for performance reason***

## So, Is SQL a Solved Problem?

No, of course not. There’s still no guarantee of getting the same answer when asking the same question multiple times. Additionally, AI has no real understanding of the data. The moment you introduce filters, you can get all sorts of unexpected results,***Although Providing sample values from columns into a semantic model helps a lot***, still real-world models are far more complex and often contain ambiguities.

While LLMs generate correct SQL, they don’t always generate the most **efficient** queries, But you can argue, it is the Database problem to solve 🙂

## Compute Considerations

I don’t know enough to make a strong statement about the current cost of running LLMs, but I ran a simple experiment: I tested **QWQ-32** on my laptop (which has an **NVIDIA RTX A2000 GPU with 4GB of dedicated memory** ). The good news? It worked. Running an open-source “thinking model” on a personal laptop is already impressive. The bad news? It was painfully slow—so much so that I’m not eager to repeat the test.

From a practical perspective, generating SQL queries this way seems extremely expensive. A decent BI tool can generate similar queries in milliseconds, using orders of magnitude less compute power, but as LLMs continue to improve in efficiency, maybe in a couple of years, the compute requirement to generate SQL Queries will become trivial?

## Final Thoughts

Having experimented with LLMs since 2023, I can say with confidence that they have improved significantly ( LLMs in 2023 were not very good to be honest). They are getting better and, more importantly, cheaper, opening the door for new applications.

The initial promise was that you could just throw data at an AI system, and it would figure out everything. I suspect that’s not true. In reality, to get useful results, you need **more structure**, and well-defined **semantic models** will play a crucial role in making asking your Data a reality.