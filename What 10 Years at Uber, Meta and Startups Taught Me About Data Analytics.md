---
title: "What 10 Years at Uber, Meta and Startups Taught Me About Data Analytics"
source: "https://medium.com/data-science/what-10-years-at-uber-meta-and-startups-taught-me-about-data-analytics-fd948b912556"
author:
  - "[[Torsten Walbaum]]"
published: 2024-06-18
created: 2025-04-25
description: "Over the last 10 years, I have worked in analytical roles in a number of companies, from a small Fintech startup in Germany to high-growth pre-IPO scale-ups (Rippling) and big tech companies (Uber…"
tags:
  - "clippings"
---
## [TDS Archive](https://medium.com/data-science?source=post_page---publication_nav-7f60cf5620c9-fd948b912556---------------------------------------)

[![TDS Archive](https://miro.medium.com/v2/resize:fill:76:76/1*JEuS4KBdakUcjg9sC7Wo4A.png)](https://medium.com/data-science?source=post_page---post_publication_sidebar-7f60cf5620c9-fd948b912556---------------------------------------)

An archive of data science, data analytics, data engineering, machine learning, and artificial intelligence writing from the former Towards Data Science Medium publication.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*QYzTQ-IC4HWm7x2JzQbblw.png)

Image by Author (generated via Midjourney)

==Over the last 10 years, I have worked in analytical roles in a number of companies, from a small Fintech startup in Germany to high-growth pre-IPO scale-ups (Rippling) and big tech companies (Uber, Meta).==

Each company had a unique data culture and each role came with its own challenges and a set of hard-earned lessons. Below, you’ll find ten of my key learnings over the last decade, many of which I’ve found to hold true regardless of company stage, product or business model.

## 1\. You need to tell a story with data.

Think about who your audience is.

If you work in a research-focused organization or you are mostly presenting to technical stakeholders (e.g. Engineering), an academic “white paper”-style analysis might be the way to go.

But if your audience are non-technical business teams or executives, you’ll want to make sure you are focusing on the key insights rather than getting into the technical details, and are connecting your work to the business decisions it is supposed to influence. If you focus too much on the technical details of the analysis, you’ll lose your audience; ==communication in the workplace is not about what you find interesting to share, but what the audience needs to hear.==

The most well-known approach for this type of insights-led, top-down communication is the Pyramid Principle developed by McKinsey consultant Barbara Minto. Check out [this recent TDS article](https://towardsdatascience.com/how-to-better-communicate-as-a-data-scientist-6fc5428d3143) on how to leverage it to communicate better as a DS.

## 2\. Strong business acumen is the biggest differentiator between good and great data scientists.

If you are a Senior DS at a company with a high bar, you can expect all of your peers to have strong technical skills.

You won’t stand out by incrementally improving your technical skillset, but rather by ensuring your work is driving maximum impact for your stakeholders (e.g. Product, Engineering, Biz teams).

==This is where Business Acumen comes into play: In order to maximize your impact, you need to== ==**1)**== ==deeply understand the priorities of the business and the problems your stakeholders are facing,== ==**2)**== ==scope analytics solutions that directly help those priorities or address those problems, and== ==**3)**== ==communicate your insights and recommendations in a way that your audience understands them (see #1 above).==

With strong Business Acumen, you’ll also be able to sanity check your work since you’ll have the business context and judgment to understand whether the result of your analysis, or your proposal, makes sense or not.

**Business Acumen is not something that is taught in school or DS bootcamps; so how do you develop it?** Here are a few concrete things you can do:

1. Pay attention in the Company All Hands and other cross-team meetings when strategic priorities are discussed
2. Practice connecting these priorities to your team’s work; during planning cycles or when new projects come up, ask yourself: “How does this relate to the high-level business priorities?” If you can’t make the connection, discuss this with your manager
3. When you are doing an analysis, always ask yourself “So what?”. A data point or insight only becomes relevant and impactful once you can answer this question and articulate why anyone should care about it. What should they be doing differently based on this data?

The ultimate goal here is to ==transition from taking requests and working on inbound JIRA tickets to being a== ==***thought partner***== ==of your stakeholders== that shapes the analytics roadmap in partnership with them.

## 3\. Be an objective truth seeker

Many people cherry pick data to fit their narrative. This makes sense: Most organizations reward people for hitting their goals, not for being the most objective.

==As a Data Scientist, you have the luxury to push back against this.== Data Science teams typically don’t directly own business metrics and are therefore under less pressure to hit short-term goals compared to teams like Sales.

Stakeholders will sometimes pressure you to find data that supports a narrative they have already created in advance. While playing along with this might score you some points in the near term, ==what will help you in the long term is being a truth seeker and promoting the narrative that the data truly supports.==

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*YSsQ1AmuF5eKyb0YEw5qsA.png)

Image by Author (created via Midjourney)

Even if it is uncomfortable in the moment (as you might be pushing a narrative people don’t want to hear), it will help you stand out and position you as someone that executives will approach when they need an unfiltered and unbiased view on what’s really going on.

## 4\. Data + Primary Research = ❤️

Data people often frown at “anecdotal evidence”, but it’s a necessary complement to rigorous quantitative analysis.

Running experiments and analyzing large datasets can give you statistically significant insights, but you often miss out on signals that either haven’t reached a large enough scale yet to show up in your data or that are not picked up well by structured data.

==Diving into closed-lost deal notes, talking to customers, reading support tickets etc. is sometimes the only way to uncover certain issues (or truly understand root causes).==

**For example,** let’s say you work in a B2B SaaS business. You might see in the data that win rates for your Enterprise deals are declining, and maybe you can even narrow it down to a certain type of customer.

But to truly understand what’s going on, you’ll have to talk to Sales representatives, dig into their deal notes, talk to prospects etc.. In the beginning, this will seem like random anecdotes and noise, but after a while a pattern will start to emerge; and odds are, that pattern did not show in any of the standardized metrics you are tracking.

## 5\. If the data looks too good to be true, it usually is

When people see a steep uptick in a metric, they tend to get excited and attribute this movement to something they did, e.g. a recent feature launch.

Unfortunately, when a metric change seems suspiciously positive, it is often because of data issues or one-off effects. For example:

- Data is incomplete for recent periods, and the metric will level out once all data points are in
- There is a one-time tailwind that won’t sustain (e.g. you see a boost in Sales in early January; instead of a sustained improvement to Sales performance, it’s just the backlog from the holiday period that is clearing up)

Don’t get carried away by the excitement about an uptick in metrics. You need a healthy dose of skepticism, curiosity and experience to avoid pitfalls and generate robust insights.

## 6\. Be open to changing your mind

If you work with data, it’s natural to change your opinion on a regular basis. For example:

- You recommended a course of action to an executive, but have lost faith that it’s the right path forward since you got more data
- You interpreted a metric movement a certain way, but you ran an additional analysis and now you think something else is going on

However, most analytical people are hesitant to walk back on statements they made in the past out of fear of looking incompetent or angering stakeholders.

That’s understandable; changing your recommendation typically means additional work for stakeholders to adjust to the new reality, and there is a risk they’ll be annoyed as a result.

Still, you shouldn’t stick to a prior recommendation simply out of fear of losing face. You won’t be able to do a good job defending an opinion once you’ve lost faith in it. Leaders like Jeff Bezos recognize the importance of changing your mind when confronted with new information, or simply when you’ve looked at an issue from a different angle. As long as you can clearly articulate why your recommendation changed, it is a sign of strength and intellectual rigor, not weakness.

> Changing your mind a lot is so important. You should never let anyone trap you with anything you’ve said in the past. — Jeff Bezos

## 7\. You need to be pragmatic

When working in the Analytics realm, it’s easy to develop perfectionism. You’ve been trained on scientific methods, and pride yourself in knowing the ideal way to approach an analysis or experiment.

Unfortunately, the reality of running a business often puts severe constraints in our way. We need an answer faster than the experiment can provide statistically significant results, we don’t have enough users for a proper unbiased split, or our dataset doesn’t go back far enough to establish the time series pattern we’d like to look at.

It’s your job to help the teams running the business (those shipping the products, closing the deals etc.) get things done. If you insist on the perfect approach, it’s likely the business just moves on without you and your insights.

As with many things, done is better than perfect.

## 8\. Don’t burn out your Data Scientists with ad-hoc requests

Hiring full-stack data scientists to mostly build dashboards or do ad-hoc data pulls & investigations all day is a surefire way to burn them out and have churn on the team.

Many companies, esp. high-growth startups, are hesitant to hire Data Analysts or BI folks specifically dedicated to metric investigations and dashboard building. Headcount is limited, and managers want flexibility in what their teams can tackle, so they hire well-rounded Data Scientists and plan to give them the occasional dashboarding task or metrics investigation request.

In practice, however, this often balloons out of proportion and DS spend a disproportionate amount of time on these tasks. They get drowned in Slack pings that pull them out of their focused work, and “quick asks” (that are never as quick as they initially seem) add up to fill entire days, making it difficult to make progress on larger strategic projects in parallel.

Luckily, there are solutions to this:

1. ==Implement an AI chatbot that can field straightforward data questions==
2. Train relevant teams on basic SQL (at least 1–2 analysts per team) to make them more independent. With the [Snowflake SQL AI Assistant](https://www.snowflake.com/blog/copilot-ai-powered-sql-assistant/) or [Gemini assistance in BigQuery](https://cloud.google.com/bigquery/docs/write-sql-gemini), extensive SQL syntax knowledge is not strictly required anymore to pull data and generate insights
3. Use self-serve BI tools that give users autonomy and flexibility in getting the insights they need. There has been a ton of progress in recent years, and tools like Omni are getting us closer to a world where self-serve analytics are a reality

## 9\. Not everything needs a fancy Tableau dashboard

==Companies tend to see it as a sign of a mature, strong data culture when data is pulled out of spreadsheets into BI solutions.==

While dashboards that are heavily used by many stakeholders across the organization and are used as the basis for critical, hard-to-reverse decisions should live in a governed BI tool like Tableau, ==there are many cases where Google Sheets gets you what you need and gets you there much faster, without the need to scope and build a robust dashboard over the course of days or weeks==.

The truth is, teams will always leverage analytics capabilities of the software they use day-to-day (e.g. Salesforce) as well as spreadsheets because they need to move fast. ==Encouraging this type of nimble, decentralized analytics rather than forcing everything through the bottleneck of a BI tool allows you to preserve the resources of Data Science teams== (see #8 above) and equip the teams with what they need to succeed (basic SQL training, data modeling and visualization best practices etc.).

## 10\. Having perfectly standardized metrics across the entire company is a pipe dream

As discussed under #9 above, teams across the company will always unblock themselves by doing hacky analytics outside of BI tools, making it hard to enforce a shared data model. Esp. in fast-growing startups, it’s impossible to enforce perfect governance if you want to ensure teams can still move fast and get things done.

While it gives many Data Scientists nightmares when metric definitions don’t match, in practice it’s not the end of the world. More often than not, differences between numbers are small enough that they don’t change the overall narrative or the resulting recommendation.

==As long as critical reports (anything that goes into production, to Wall Street etc.) are handled in a rigorous fashion and adhere to standardized definitions==, it’s okay that data is slightly messy across the company (even if it feels uncomfortable).

## Final Thoughts

Some of the points above will feel uncomfortable at first (e.g. pushing back on cherry-picked narratives, taking a pragmatic approach rather than pursuing perfection etc.). But in the long run, you’ll find that it will help you stand out and establish yourself as a true thought partner.

For more hands-on analytics advice, consider following me here on Medium, on [LinkedIn](http://www.linkedin.com/comm/mynetwork/discovery-see-all?usecase=PEOPLE_FOLLOWS&followMember=torsten-walbaum) or on [Substack](https://www.operatorshandbook.com/).



[Last published Feb 3, 2025](https://medium.com/data-science/diy-ai-how-to-build-a-linear-regression-model-from-scratch-7b4cc0efd235?source=post_page---post_publication_info--fd948b912556---------------------------------------)

An archive of data science, data analytics, data engineering, machine learning, and artificial intelligence writing from the former Towards Data Science Medium publication.

Led Strategy & Analytics teams at Uber, Meta and Rippling. Follow on LinkedIn ([bit.ly/twli](http://bit.ly/twli)) and Substack ([OperatorsHandbook.com](http://operatorshandbook.com/)) for analytics & career advice

## Responses (106)

Michael David Cobb Bowen

What are your thoughts?  

==Diving into closed-lost deal notes, talking to customers, reading support tickets etc. is sometimes the only way to uncover certain issues (or truly understand root causes).==

```c
This is a key point - always look at the context of the data, not just the data itself. Often overlooked
```

154

```c
As a data scientist, I used to want the company to have a source of truth for metrics, so it’s easier to manage. 
Then I realized it’s not possible, especially as the company grows.
```

197

```c
That hit home! Thanks for writing this.
```

134

## More from Torsten Walbaum and TDS Archive

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--fd948b912556---------------------------------------)