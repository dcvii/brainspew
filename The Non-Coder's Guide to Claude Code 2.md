---
title: "The Non-Coder's Guide to Claude Code"
source: "https://leadershipinchange.com/p/the-non-coders-guide-to-claude-code?publication_id=4640380&post_id=184484319&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Joel Salinas]]"
published: 2026-01-22
created: 2026-01-29
description: "Everything non-technical leaders need to know about building with AI"
tags:
  - "clippings"
---
### Everything non-technical leaders need to know about building with AI

![](https://substackcdn.com/image/fetch/$s_!r9Cf!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9ace0dbc-3eb8-4ef8-8569-56cdc36a82f0_1536x1024.png)

*Before we start: Ready to **implement** and **build** with AI? **Join Premium** for $1,345+ in tools and systems at $39/yr. **[Start here](https://leadershipinchange.com/p/premium-member-hub)** | Looking for 1-on-1 **coaching** or a private **knowledge hub** build? **[Book a free call](https://jsalinas.org/#services)**[.](https://jsalinas.org/#services)*

---

I almost skipped Claude Code the first time I heard about it.

The word “code” hit me like a wall. It brought back every frustrating moment of feeling locked out of the technical world, sitting in meetings while developers talked in languages I didn’t understand, waiting days for simple changes because I couldn’t build them myself, watching opportunities pass because “we’d need to code that.”

That’s the barrier most leaders face with Claude Code. **The name alone makes you want to move on to something that feels more accessible.** But here’s what I discovered after I pushed past that intimidation: **the floodgates are opening.**

Non-technical people are building real tools (me!!!) - websites, data systems, custom workflows - without writing a single line of code. **I built my entire website ([jsalinas.org)](http://jsalinas.org/) in one Saturday, then spent two days refining it.** No coding background. No technical degree. Just clear direction and AI handling the technical execution.

This shift isn’t about learning to code. **It’s about understanding how leaders who are innovative, adaptable, and know how to direct AI will have an enormous strategic advantage in the future.**

Today’s guest post comes from one of my new favorite technical AI creators, [Alejandro Aboy](https://open.substack.com/users/22949723-alejandro-aboy?utm_source=mentions), **a data engineer with serious technical capability** who’s actually using Claude Code to solve real business problems. What he’s about to show you isn’t theoretical, it’s practical, implementable, and designed specifically for leaders who can’t code but need to solve data problems fast.

**In this post, you’ll learn:**

- What Claude Code actually does (without technical jargon)
- Why “code” in the name is misleading for what leaders actually do with it
- Real business scenarios where non-technical leaders use Claude Code to get answers
- How to set it up and start using it Monday morning
- What this tool signals about the future of business building

![](https://substackcdn.com/image/fetch/$s_!MRS0!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F68e1be70-c893-415a-91ca-617f7e20c61a_394x401.png)

Grab a coffee and enjoy! Also… EXAMPLES included at the end.

---

## Making Sense of Company Data: A Claude Code Introduction for Non-Technical Leaders

#### Your dashboards show different numbers. Your data team is overwhelmed. Here’s how AI helps you get answers without coding.

![](https://substackcdn.com/image/fetch/$s_!VVG3!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F46a60c85-97e8-4124-826d-3d3675a6158b_707x387.png)

---

*Hi, I am Alejandro Aboy. I write at [The Pipe & The Line](https://thepipeandtheline.substack.com/?utm_source=substack&utm_campaign=publication_embed&utm_medium=web) about Data & AI technical topics, but also about how the data industry evolves and how we can leverage the right mindset and the right tools to achieve our goals.*

---

Over 2025 (and probably 2026), most of AI use cases are and will be around coding.

But for non technical users, there’s potential even in tools that are meant for technical people, such as Claude Code.

You have the power of Claude but supercharged, which allows you to leverage Agents, Skills and custom workflows that you like to reuse, all from your local machine and without falling into other teams as bottlenecks.

In this article we will go through different use cases I’ve seen over time at work and that can be easily replicated without technical frictions.

**Table of Contents:**

- The Stages Of Data (And Why You See Discrepancies)
- What Claude Code Actually Does
- Hands-On Real World Examples
	- What You Need to Set This Up
	- Example #1: Pipeline Discrepancies
	- Example #2: Google Sheet vs Data Warehouse
	- Example #3: Requirements Without the Back-and-Forth
	- Example #4: From Meeting Notes to Action
- Final Words

---

> *SIDENOTE: Anthropic just launched [Cowork](https://leadershipinchange.com/p/claude-cowork-what-it-is-why-it-matters) “Claude Code for the rest of your work”, which attempts to provide Claude Code capabilities for non technical users. For now it’s in preview and not available for everyone, but it might have new features as weeks goes by, so many of the learnings in this article could be transferred to the Cowork ecosystem eventually.*

## The Stages Of Data (And Why You See Discrepancies)

Think of this scenario: Two executives using 2 different dashboards to see the “same” data.

Normally, they would schedule a meeting with the data team in three days just to remain confused because the answer is not enough.

They have explained to you, but it is still not clear why 2 Dashboards reading from Salesforce or Hubspot give different numbers for the same thing.

There’s something important to break down first, which are the data layers:

- **Source** → Where data is generated and lives.
- **Transformation** → Where someone decides what metrics mean and applies business logic to them.
- **Dashboard** → Where you see the number.

Depending on your work scope, you are either closer to the source or to the dashboard, but not in the transformation layer, unless you work in the data team.

Many things can happen along the way that could cause confusion at the end of the data path, such as:

- **Timing Mismatches** \- e.g. HubSpot updates are on the spot. Database refreshes at 2 AM.
- **Definition Drift** \- e.g. One team’s “active user” ≠ another team’s “active user.”
- **Hidden Filters** \- e.g. Dashboard A excludes refunds over $10K. Dashboard B includes them.

Years ago data teams were bottlenecks and stakeholders had to wait to get the most simple explanation for what they are seeing.

Now you don’t need to code in Python or SQL to understand why numbers don’t match.

You need a tool that traces the actual path your data takes.

That tool is Claude Code, a terminal-based AI that helps you get together custom workflows, skills and more; faster and in plain English.

---

## What Claude Code Actually Does

*\> Note: Even though this explanation is for non-technical usage, there are some mandatory steps you will need to put together. The good news is, they are as simple as copy pasting. If you need, you can ask Claude or any other AI how to set this up for extra guidance.*

To get started, you need to open the Terminal App on your Mac or Shell App on your Windows.

Then you follow this guide**:**[https://code.claude.com/docs/en/overview](https://code.claude.com/docs/en/overview)

**What makes it different:**

- Connects directly to business tools (HubSpot, Google Sheets, Databases)
- Reads actual data, not hypotheticals
- Shows its work

Claude Code can become a translator between you and your data.

> When you ask: “Why don’t these pipeline numbers match?” it will connect to HubSpot, read your database tables, compare the logic and you will do something like *“HubSpot includes On Hold deals. Your warehouse excludes them after 90 days.”*

**It becomes a workflow machine that you can customize as much as you can**, without getting limited by plain Claude, where you have many shared features but requires you to guide much more of what it should be doing, and its also lacking the context power Claude Code can achieve.

### Claude Code Features To Customise Your Workflows

The best thing about Claude Code, **is that you can ask it to create anything you want just by chatting.**

![](https://substackcdn.com/image/fetch/$s_!_xsR!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa8baeabf-3493-447d-989c-1d195c69b021_1536x1024.png)

**All these features live under Markdown (.md) files, which is what all AI systems use to present documentation.**

We can break down its core features into these groups:

- [Slash Commands:](https://code.claude.com/docs/en/slash-commands)
	- User-triggered shortcuts that save you from writing repeatable workflows.
	- **Example:** /audit\_dashboard - triggers dashboard comparison workflow.
		![](https://substackcdn.com/image/fetch/$s_!45Rk!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc3a3b09b-c009-498b-a086-2916d85fa234_2640x4300.png)
- [Sub Agents](https://code.claude.com/docs/en/sub-agents)
	- Parallel Claude Agents with specialized focus and isolated context.
	- You can type /agents and follow along to create an Agent with Claude.
	- **Example:** @data-reconciliation - compares HubSpot vs Warehouse in parallel
		![](https://substackcdn.com/image/fetch/$s_!wUF-!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Faf4fd30e-34d7-4105-b3a0-6ed99766d37d_3680x3220.png)
- [Skills](https://code.claude.com/docs/en/skills)
	- Auto-invoked knowledge packages Claude loads when relevant. Claude Code won’t tell you that it is using the skill per se, but it will follow it if it thinks it needs to.
	- **Example:** data-discrepancy-analyzer - auto-loads when comparing two data sources
		![](https://substackcdn.com/image/fetch/$s_!umex!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F52cbb4c9-eb6c-4ce1-8155-29e2a50b6a20_3224x4660.png)
- [MCP](https://code.claude.com/docs/en/mcp)
	- Tools we provide Claude Code to connect with context. Each MCP is different and the way to connect them is required in the use case and authentication setup so it can recognize you. Normally you get linked into a screen so you can confirm your identity just by clicking, no technical knowledge required.
	- **Example:** Read Hubspot deals and prepare a quick summary report to write a document on Confluence. Uses 2 tools to read from one and write to the other without getting out of Claude Code nor exporting or copy pasting data into it.

*There are no rules here, you can use some of them or even all of them and let Claude Code figure out the rest as it goes. You will find your best use cases while using its tools.*

With slash commands you **trigger**, with sub agents **you ask a dedicated role to achieve something**, skills are **packed instructions to be considered when relevant** and MCPs provide **powerful integrations for the AI to better achieve its tasks**, so you pick your best weapons according to your workflows.

This is how a folder using Claude Code looks after creating some agents, skills and commands.

![](https://substackcdn.com/image/fetch/$s_!rZ7P!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5e2b8981-05a4-4f4a-9024-a2b9788bd7bf_286x155.png)

Remember: Ask Claude Code to help you build these capabilities

Claude Code has **plugin marketplaces**: repositories of pre-built skills, agents, and commands you can install in seconds. You can take a look at the most known one: [aitmpl](https://www.aitmpl.com/agents?source=post_page-----4e53d6688b34---------------------------------------).

---

## Hands-On Real World Examples

### What You Need to Set This Up

**Prerequisites**:

- Claude Code via subscription or API Usage Billing
- Access to your Mac’s Terminal or Windows Shell

> *\> Note: Regarding GDPR-Security concerns, if you work with extremely confidential information, contact your InfoSec team to confirm if Anthropic is approved as a third party tool or find a way to Claude Code through its API on your company’s internal servers instead.*
> 
> *I grouped together some use cases with simulated scenarios of things you can do from a data perspective. Depending on the tools you use everyday you need to do your research to explore how to connect MCPs and configure your Claude Code to run the tools you need.*

### Example #1: Pipeline Discrepancies

**Your Situation:  
**HubSpot shows $1M. CFO’s dashboard using the database shows $810K.

**What You Do:**

*“Compare the HubSpot pipeline with our warehouse deals table. Why is there a difference?”*

![](https://substackcdn.com/image/fetch/$s_!M6vG!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc5d354af-6f69-437e-9c53-93401c3dad5b_3680x4932.png)

*\> Note that Claude Code might ask for permissions to run tools, you can accept each time or just accept definitely so it doesn’t ask you next time.*

![](https://substackcdn.com/image/fetch/$s_!n01T!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4cee3f31-ea5f-40b8-9b79-e40057500119_902x425.png)

**Insight**: Now you can say: “Let’s align on whether On Hold counts as an active pipeline.”

---

### Example #2: Google Sheet vs Data Warehouse

**Your Situation:  
**Marketing Director’s Google Sheet doesn’t match the data team’s dashboard.

**What You Do:**

*“Read Google Sheet ‘Q1 Campaign Performance’ Compare with warehouse table marketing.campaigns. Why are CPL numbers different?”*

![](https://substackcdn.com/image/fetch/$s_!KmZE!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5df2d5f5-8333-4a46-a79e-e41c05565076_3680x5920.png)

**Insight:** Your sheet is fresher. The warehouse is cleaner. They serve different purposes.

---

### Example #3: Requirements Without the Back-and-Forth

**Your Situation:  
**You asked for a “customer churn dashboard.” The data team built something. Wrong. They rebuilt. Still wrong.

**What You Do:**

*“I need a customer churn dashboard. Help me write requirements based on our warehouse tables so the data team gets it right the first time.”*

![](https://substackcdn.com/image/fetch/$s_!Fatl!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fca67de51-9960-4d11-b3c1-2c1edd9eb6ba_3680x5652.png)

**Insight**: You used AI to break down what you wanted and reduced lots of meetings.

---

### Example #4: From Meeting Notes to Action

**Your Situation:  
**You discussed a churn dashboard in a meeting. Took notes in Confluence. Need to create proper requirements and a ticket for your data team.

**What You Do:**

*“Read my Confluence page ‘Q1 Data Requests - Churn Discussion’”*

To launch a slash-command, you just type / and start writing the name of the command like this:

![](https://substackcdn.com/image/fetch/$s_!Mazx!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6c0925e8-173c-426e-97a9-27668cc0802b_733x139.png)

Then you will get the output:

![](https://substackcdn.com/image/fetch/$s_!BO2a!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7ce6ec6a-d749-47f5-9c45-652ec17e884e_3680x2412.png)

\> Note: Claude might ask you questions sometimes to validate requests and have better context to follow up.

![](https://substackcdn.com/image/fetch/$s_!F7lH!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7ac56768-7be0-47c5-acd4-94ed27bca9d7_1149x504.png)

**Insight:** Transforms loose meeting notes into actionable work without manually rewriting everything or switching between three different tools.

---

## Final Words

You’re not trying to become a data analyst engineer.

You’re trying to stop making decisions based on numbers you don’t understand.

Your data team isn’t incompetent. They’re drowning in vague requests like “the numbers don’t match.”

Claude Code translates:

- ❌ “These numbers are wrong”
- ✅ “HubSpot includes On Hold deals, warehouse excludes them after 90 days—which should we standardize on?”

That’s a 5-minute conversation instead of 5 days.

And this is just using it for a data-driven mindset, you can leverage it for almost any use case you can think of.

These features are just a tiny part of a lot of things you can do, since you can customize it to your liking as much as you can.

When you really get the power it can provide, you really start using AI to enable yourself.

Let Claude Code trace where things diverge so you can unlock yourself and focus on bringing real insights to make the right decisions.

Gracias, [Alejandro Aboy](https://open.substack.com/users/22949723-alejandro-aboy?utm_source=mentions)!  
  
The leaders who win in the next five years won’t be the ones who learn to code. They’ll be the ones who understand how to direct AI to solve real business problems. Claude Code is one tool in that ecosystem, but the principle applies everywhere:

**Innovation, adaptability, and knowing how to use AI strategically create an enormous competitive advantage.**

Six months ago, I fully moved from ChatGPT to Claude as my main workhorse for everything I do. Claude Code takes that foundation and opens doors for building things I never thought possible as a non-coder. If you’re curious about Alejandro’s work, he writes at **The Pipe & The Line** about data and AI - practical, technical, but always grounded in real-world application.

---

*Want help building your AI strategy? I help mission-driven leaders implement AI without the tool chaos.**[Let’s connect!](http://jsalinas.org/)***

---

**If You Only Remember This:**

- The word “code” in Claude Code is misleading - you’re directing, not coding
- **The floodgates are opening for non-technical people to build things in the future**
- This isn’t about becoming technical - it’s about understanding what’s now possible

What’s one thing you’ve been waiting on your technical team to build that you could potentially direct yourself with tools like Claude Code?

Let us know…

---

#### Join 3,500+ Leaders Implementing AI today…

**Which Sounds Like You?**

**“I need systems, not just ideas”** → Join Premium (Starting at $39/yr, $1,345+ value): Tested prompts, frameworks, direct coaching access. [Start here](https://leadershipinchange.com/subscribe)

**“I need this built for my context”** → AI coaching, custom Second Brain setup, strategy audits. [Message me or book a free call](https://jsalinas.org/#services)

**“I want to reach these leaders”** → Sponsor one post (short supply). 3,500+ executives. [Check availability](https://jsalinas.org/#contactme)

> *PS: Many subscribers get their Premium membership reimbursed through their company’s professional development $. [Use this template to request yours.](https://docs.google.com/document/d/1o_7xKPLF5GqUQ9U6OKuJYCCUAOSlKgLdDQ042Kw6jCU/edit?usp=sharing)*
> 
> [LinkedIn](http://www.linkedin.com/in/jsalinasf) / [Community Chat](https://open.substack.com/pub/leadershipinchange10/chat?utm_source=chat_embed) / [Medium](https://leadershipinchange10.medium.com/)