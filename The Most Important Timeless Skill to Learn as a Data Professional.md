---
title: "The Most Important Timeless Skill to Learn as a Data Professional"
source: "https://sqlpatterns.com/p/the-most-powerful-timeless-skill"
author:
  - "[[Ergest Xheblati]]"
published: 2025-11-29
created: 2025-11-29
description: "How to build expertise and have a long and successful career in data"
tags:
  - "clippings"
---
### How to build expertise and have a long and successful career in data

When I started out in data all I wanted was to have a long and satisfying career, to be compensated well regardless of advances in technology or the whims of the market and of course to love what I did.

**More importantly I wanted to build expertise**. So I looked everywhere. Career books, videos, articles, podcasts but only found bits and pieces.

The best book on the topic was Cal Newport’s *So Good They Can’t Ignore You.* It has a simple premise: *If you focus on learning “rare and valuable skills” you’ll have a long and successful career, full of opportunities, satisfaction and compensation.*

That’s great, but what skills fit those criteria? Cal doesn’t give you a satisfactory answer, but I believe I found it, at least for data professionals:

That skill is the ability to find points of leverage that dramatically improve an organization with relatively less effort, articulate them as clearly and intelligently as possible (for myself and others) and then connect them to your knowledge and experience.

By the way, when I say “organization” I don’t necessarily mean the entire company. It could be that, of course but it could also just be an org inside of a big company.

In this issue I’ll try to achieve three things:

1. First, I’ll show you why you should focus on finding these leverage points
2. Second, I’ll give you ideas on how to learn them
3. Finally, I’ll provide a couple of examples so you understand what I’m talking about

#### What are points of leverage?

Organizations are complex systems. The parts are interconnected, full of dependencies and feedback loops. This means that improvements to the parts don’t necessarily add up to overall improvement.

Complexity also makes it so that organizations have points of leverage (also known as constraints) that drive most of the throughput.

Efforts to improve anything other than these points will at best result in incremental improvements and at worst waste time, effort and money with nothing to show for.

Many of these leverage points are inherent to the business model.

For example a subscription business model’s key leverage point is retention. Without it, all you have is a leaky bucket where all your marketing efforts will only delay the demise of the business.

#### Why focus on finding leverage points?

**First** of all understand that everyone from the C-suite down to every manager are already looking for them. That’s why you’re getting inundated with data requests. In fact, every request can be seen as an attempt to find leverage points:

> “Can you break down conversion rates by channel for Q4?”
> 
> **Translation**: Are there any channels that are better than others where we can focus our efforts and win more deals?
> 
> “What’s our win rate for deals over $50k?”
> 
> **Translation**: Is there a segment of our customer base that spends more money, converts better and is easier or faster to close? That way we can focus our efforts and increase sales.
> 
> “How many users churned after the pricing change?”
> 
> **Translation**: Is pricing a lever? Is there a segment of our customer base who are price sensitive vs price insensitive? That way we can tailor our offerings accordingly and keep both or choose to focus on one vs the other.

The hope is that you (as a data professional) can find these leverage points in data. And as data professionals we sit in the perfect position to do so. How do I know? I’ve been there!

Being the business analyst gave me access to all the company’s data from sales, marketing, finance, operations, customer service, etc. The only problem is we waste this golden opportunity.

All you need is a little initiative. The key is asking the right questions, analyzing the business properly, coming up with hypotheses for where the leverage points lie, and tinkering with data.

I call this “tinkering without permission” and it’s one of the key attitudes you should turn into second nature. I’ll write more about that in another issue.

**Second**, this skill is highly valued. If all you did was focus on finding the next “million dollar” leverage point you’d be the most highly valued person at that company. Now tell me what CEO or president of an organization wouldn’t want to have a person like that on their team?

It also compounds over time, meaning the more you learn the more valuable you become, and can easily be transferred to other organizations. You can become an expert doing this, and expertise in data outside of technical skills is rare. That expertise is exactly what I was after.

#### How do you learn this skill?

Assuming you agree with me, we can now shift our attention to figuring out how to learn this skill. If I could write a letter to my younger self, I would tell him to do everything in his power to learn it. Yes, I’ve only just begun to think this way, but it’s already bearing fruit.

The only reliable way I’ve found to learn this skill myself is through case studies. This means reading books, listening to podcasts that discuss specific businesses, watching YouTube videos, hunting for patterns and collecting examples.

So in future issues I will pick out specific case studies I find in books, articles, podcasts, etc. to help you start to spot patterns and build your intuition as I continue to build mine. We’ll be on this journey together.

Let me illustrate with a couple of examples.

#### How PayPal boosted revenue by $100 million

In the book *Growth Levels and How to Find Them* Matt Lerner relays a story of how he found a leverage point, while launching a new product at PayPal, that ultimately resulted in $100 million of additional revenue:

> “It was 2005. PayPal had decided to expand and bet the whole company on a new product, which allowed merchants to process transactions on their own sites via card processing APIs. Even back then, it was obvious the world needed this product. I was in charge of launching it. Thousands signed up, but few used it: the activation rate was just 10%.”

They had tried many different ways to fix it and the activation rate did increase to about 30% but that was still low. What Matt needed was a leverage point, so he decided to go to PayPal’s customer center and ask real customers why they had not activated.

He soon discovered that many of these merchants didn’t actually have any customers of their own, so logically they couldn’t activate. He had a hunch. What if he could find merchants who did have customers? How many of them could potentially be activated?

> “I realized the problem: many of our customers had no customers of their own. And I couldn’t “growth hack” my way around that. That night, I asked my favorite analyst, Igor (Stanford engineering grad, of course): “How much of our revenue comes from our top 10% of signups?” An hour later, he sent me a spreadsheet with the answer: almost all of it.”

Now that’s what I call a leverage point! 90% of revenue coming from 10% of signups is one of those typical Pareto distribution things that are so typical in the business world. And while you should be careful about what you do with this information—because the answer isn’t always to focus on the 10%—it made sense in this case.

And that’s what Matt and his team did.

> “We changed our entire approach. We developed a predictive model to score new signups on their propensity to become valuable customers. We’d try to increase revenue by giving high-scoring signups a white-glove onboarding experience, walking them through setup and teaching them to use the system.”

They tested this approach on a small group at first and when they saw promising results, expanded the treatment to the entire group.

> “So we expanded the white-glove treatment to all our promising signups, increasing the revenue from new cohorts by 40% would eventually deliver over $100M in annual recurring revenue.”

One more example to whet your appetite.

#### Improving retention at HubSpot

Early on in HubSpot’s journey to a CRM behemoth, they were struggling to hold on to customers. There was a concern about whether they’d ever transition from an “inbound app” and into a full-blown CRM.

Mark Znutas was an operations analyst (later VP of GTM Ops and Strategy) looking for insights in the data. The approach he describes is essentially a form of *feature engineering* and classification.

> I was an Operations Analyst at the time - one of dozens of analysts at HubSpot who struggled to stand out in the crowd…\[\]. Obviously, I knew I should spend my time thinking about improving net dollar retention, but I didn’t know where to start. How does one just fix NDR? Surely someone smarter than me would have already done it if the solution were straightforward, right?

What you can clearly see here is his quest to find and exploit leverage points. If you know anything about the SaaS business model, you’d know that retention (aka LTV) is the lifeblood of the business. NDR is just a proxy for measuring it.

Mark found his insight in a report he was already preparing that he called “The Customer File.” Anyone of you who has data science or machine learning experience will instantly recognize this format where each row represents a customer, each column is a feature and the response variable is whether they churned or not.

> The basis of nearly all of our reporting was a large table called The Customer File. It contained Stripe billing data we pulled for all our customers, aggregated by month, and calculated the beginning-of-month ARR, end-of-month ARR, net ARR change, and change category for each customer.

But the secret didn’t lie here. ARR is a lagging indicator only showing the results of actions taken in the past. It doesn’t tell you what signals to pay attention to. So Mark expanded the customer file with firmographic and behavioral data to see if he could find any patterns. Like I said about this is basically feature engineering.

> I cut retention by every dimension I could think of to see if I could find any insight into retention. Those dimensions included firmographic data, product usage data, lead source data, Sales & CS ownership data, and many others. I added new columns for every question I wanted to answer.

Eventually he found his answer in two distinct signals: business size and whether they were using the CRM platform HubSpot had just started building:

> After producing dozens of these output tables, I finally found the insight I had been searching for. There were two variables with clear and strong correlation to retention:
> 
> 1. Employee Size → Companies with 10 or fewer employees were rough
> 2. Whether the CRM customer also used HubSpot Marketing Hub → ”Platform” customers were great.

This is the kind of insight **every** executive expects to get from their data team! It fundamentally altered HubSpot’s customer acquisition strategy and starting turning their fortunes around.

> Now, it was time to put our insight into action. We went all in on focusing on our best-fit customers. We started by focusing on acquiring more “Tier 1” customers (companies with 11+ employees or HubSpot Marketing Hub) and fewer “Tier 2” customers (companies with 1-10 employees and no HubSpot Marketing Hub).

And you know what, it worked! My guess is that it also helped Mark grow in his career from an operations analyst to VP of Ops and Strategy. You can read the full article here:[Wrap Text by Equals](https://wrap-text.equals.com/p/an-analysts-quest-to-improve-retention?utm_source=substack&utm_campaign=post_embed&utm_medium=web)

[

A few weeks after launching The Ultimate Guide to ARR, I received a note from Mark Znutas, former VP of GTM Operations and Strategy at Hubspot…

](https://wrap-text.equals.com/p/an-analysts-quest-to-improve-retention?utm_source=substack&utm_campaign=post_embed&utm_medium=web)

If you really liked this article, let me know. I’m planning to focus all my efforts to teach this one single skill along with all the attitudes surrounding it, as I believe it has the highest possible ROI of any technical skill.

Until next time.