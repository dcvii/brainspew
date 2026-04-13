---
title: "How To Create Technical Debt With Empathy ❤️"
source: "https://careerquerylessons.substack.com/p/how-to-create-technical-debt-with?publication_id=5998391&post_id=176940096&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[By Alejandro Aboy]]"
published:
created: 2026-02-02
description:
tags:
  - "clippings"
---
---

---

> Hey person! 🙌 Thanks for checking in. Alejandro here 😊
> 
> Suscribe if you like to read about learnings, reflections and other thoughts that can be helpful for your career in tech & data!
> 
> Enjoy the reading and let me know in the comments what you think about it 👨🏻💻

Let me tell you something that took me years to understand: **everything you create is debt**.

Whether it’s that PR you just merged, that custom dashboard logic you published, or that “quick fix” you promised to revisit later—it’s all debt.

You could make mistakes, improve stuff, or make decisions based on complex scenarios.

But “debt” should be taken with responsibility because **it’s your legacy**.

> Not just for the next person, but for your future self too.

I’ll describe some experience-based scenarios and give you frameworks to handle them the best we can. Let’s go into framework mode!

## 🔠 There are 2 sides of technical debt

You can approach the problem from two perspectives, and trust me, I’ve been on both sides:

**New in the job:**

You start reading docs, the codebase, checking dashboards, and getting to know stakeholders.

Probably not everything will “click” in the first months.

There are many things that are not intuitive, and you’re sitting there wondering “why did they build it this way?”

**Old in the job:**

You’ve been working for some time or maybe leaving in the short term.

You’ve introduced many changes: improvements, “bandages,” or those infamous “I will fix this later” logics.

You’ve worked in a context that pushed you to make risky or cautious decisions.

Here’s the truth: **you can check things you’ve done 6 months ago and have no idea what you were thinking at that time**.

Maybe it’s because you’ve learned new things and improved your skills. That’s usually the reason.

But it also means you need to be empathetic—both to the person who came before you AND to your future self.

## 👀 When analyzing debt, what are the relevant angles?

Before you judge anyone’s code (including your own), you need to understand **The Context**. I see four variables that affect decisions:

**🤑 Resources**

Having too many resources to spend (e.g., all your services are in the Cloud, nothing open-source or self-managed) versus trying to cut as much as possible (e.g., fighting maintenance issues to avoid Cloud solutions).

**🫂 Headcount**

Having 200 more employees (e.g., the BI tool has 100 reports, but only 3 are being used) versus having 50 employees after rounds of layoffs (e.g., abandoned documentation or too many assets to maintain).

**🚀 Growth expectations**

Thinking growth will scale 10x the actual growth they ended up having (e.g., building custom logic to handle more customers that never came).

**🥳 Culture**

Different management with different mindsets—more conservative, more aggressive, more risky, you name it.

A culture that encourages knowledge base camps and recurrent documentation can make a huge difference.

Also, different technical profiles matter:

## 💶 Technical debt analysis: it’s time to pay the interest

Some frameworks can help you classify debt by analyzing logic. Let’s get practical:

**The Technical Debt Quadrant:**

You group decisions based on **Reckless-Prudent** and **Deliberate-Inadvertent**.

You could be making decisions and accepting the consequences, or you might lack the experience to make good choices.

You could be taking precautions to cover for bad outcomes, or just going ahead without much thought.

(Inspired by Martin Fowler’s Technical Debt Quadrant)

**Interest Probability Framework (from Managing Technical Debt book):**

It tries to predict if the debt will cause future problems, and seeks to know how painful and soon those effects will be. You have 3 main concepts:

1. **Interest accrual**: how the “interest” increases over time—same as a bank loan where the longer you wait to pay it off, the more you owe
2. **Interest amount**: effort required to address the issue if it causes problems (time, resources, lost opportunities)
3. **Time sensitivity**: how quickly the interest amount increases if the debt is not addressed

> *Based on the research, I created this template you can review every couple of months to reflect on new debt introduce and maybe come up with a backlog to tackle it.*

## 🤷🏻♂️ Ask yourself: “How can I help you(r future you)?”

When adding new debt, think wisely. This is not only for your replacement—it’s for **you**.

I can’t tell you how many times I’ve looked at my own code from 6 months ago and thought “what was I smoking?”

There are some areas we can influence to improve our legacy:

### 🔨 Implementation: your footprint in the code

Here’s what I’ve learned the hard way:

**🔬 Don’t over-optimize**

Avoid tweaking minor things unless strictly needed. It’s hard to explain that rationale later if you go too deep. I’ve spent hours optimizing code that processed 100 rows. Total waste.

**📝 Comments, comments, comments**

Try any AI Assisted IDE (e.g., Cursor). If generated comments don’t make sense, your code may not be intuitive. This helps in the validation process.

**👀 Help the eyes with patterns**

This may go against DRY (Don’t Repeat Yourself), but sometimes using code patterns or templates helps outsiders understand the code. It catches their eye and creates familiarity.

### 🔃 Maintenance: your everyday mission

**⏰ Don’t do “temporal hacks”, ask yourself:**

- Would this give more issues or fewer problems?
- Are we trading one issue for another?
- Do I intend to return and correct it as soon as possible?

I’ve seen “temporary” hacks live for 3 years. Don’t be that person.

**🚶🏻🧼 Come back and clean up:**

Don’t abandon your stuff—clear out the noise to reduce complexity. Use new learnings to improve things when opportunities are there. Don’t be afraid to remove, archive, or deprecate stuff if relevant. But always leave backups in case you need them.

**📊👨🏻💻 Monitor and decide; pay attention to details:**

> ***Save the overengineering for your side projects.** You’re the only one touching them!*
> 
> I’ve seen engineers spend weeks on custom Python packages to ingest data from a source. *Plot twist: stakeholders were fine checking insights directly on the tool. Think and assess your decisions before going through all the overengineering!*

### 📝 Documentation: your legacy within the docs

I understand topics way better when I have to explain them. Writing documentation gives you clarity and enhances your documentation skills. When you start putting things outside your head, context hits you with reality.

My favorite documentation approaches:

**💀 Post-mortem docs:**

**🔜 Decision docs:**

- Describe why you decided to use X instead of Y (e.g., using Metabase instead of Superset for BI assets)
- Cite research to support your rationale (e.g., many engineers on Reddit complain about deployment issues with Superset)
- Explain the implementation plan and the caveats about the decision

**👨🏻🏫 Workshops:**

- Run open Q&As and workshops to transfer knowledge
- Provide context on the topic, explain the outcome and what the approaches were (e.g., after collecting user feedback, we added caching to reduce Metabase loading times)
- After the workshop, grab feedback and write down a guide with a Q&A section

The base pattern of documentation is:

1. **Describe**
2. **Explain**
3. **Action taken**

**Bear in mind: the sooner you document, the better.** Then you can organize those docs in an accessible workspace.

## 📝 TL;DR

**🔠 There are 2 sides of technical debt**

**👀 When analyzing debt, check the relevant angles:**

**💶 Technical debt analysis: time to pay the interest**

- **Technical Debt Quadrant**: Categorize by human approach (Reckless/Prudent, Deliberate/Inadvertent)
- **Interest Probability Framework**: Analyze based on effect over time, effort to solve, and impact speed
- Use debt to drive business value

**🤷🏻♂️ How can I help you(r future you)?**

**🔨 Implementation: your footprint**

**🔃 Maintenance: your everyday mission**

**📝 Documentation: your legacy**

- 💀 Post-mortem docs
- 🔜 Decision docs
- 👨🏻🏫 Workshops

If you enjoyed the content, hit the like ❤️ button, share, comment, repost, and all those nice things people do when they like stuff these days. Tell me what you think about it!

[Leave a comment](https://careerquerylessons.substack.com/p/how-to-create-technical-debt-with/comments)

![](https://substackcdn.com/image/fetch/$s_!BvlN!,w_424,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0c07b7dd-718f-4687-8769-56706a030950_1024x1024.jpeg)

*Hi, I’m Alejandro Aboy. I went from marketing analyst to data engineer without a CS degree. Here, I share the lessons, mindset shifts, and stories I got from a career in Data.*

[Follow me on Linkedin](https://www.linkedin.com/in/alejandro-aboy/)