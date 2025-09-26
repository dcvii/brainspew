---
title: "Developing a dbt project with Cursor: my #profound_moment with MCP"
source: "https://alexiospanos.com/posts/2025-07-04-cursor-mcp-dbt/"
author:
  - "[[By Alex Spanos]]"
  - "[[Gergely]]"
published:
created: 2025-08-02
description:
tags:
  - "clippings"
---
---

---

**Disclaimer:** This is not a post about AI taking everyone’s jobs. Just a post about how it made my life easier.

## Hooking up Linear and Supabase MCP servers to Cursor

Everything worked on the first try. I had just watched an AI coding agent complete my data task end-to-end with minimal input from me.

I want to share this story and some reflections because it really brought home to me how software development workflows are changing in real time. My “profound moment” happened whilst working on a dbt project (pre [Fusion](https://docs.getdbt.com/docs/fusion/about-fusion)) in Cursor back in May this year.

The company I worked for used [Linear](https://linear.app/) for project management - a breath of fresh air compared to other tools I’ve used in the past.

When I saw that Linear released an official [MCP server](https://linear.app/changelog/2025-05-01-mcp), I decided to experiment with giving Cursor full autonomy to deliver a ticket from start to finish. So I created a Linear issue with a high-level description of what I wanted to achieve: add a new dbt staging model to the `analytics_raw` schema from a specified source table in the engineering OLTP database.

To deliver the issue, the agent would need information about the source table, so it required read access to our Supabase PostgreSQL database - thankfully Supabase already provided an MCP server for this (to my horror, without the ability to remove write permissions from the agent, but that’s a topic for another day).

## It worked!

After enabling Supabase and Linear MCP servers, I asked Cursor in Agent mode (Claude 3.7 Sonnet at the time) to “Complete Linear issue DAT-182”, without further instructions. I then sat back and watched it:

- query Linear and Supabase to gather the right context
- create the staging model `.sql` file
- update the properties `.yaml` file with model specs, generic tests and third party bits (for example [Elementary Data](https://docs.elementary-data.com/oss/oss-introduction) - worth a look for out-of-the-box observability on dbt projects)
- update the docs.

It then asked for permission to run the new model and the tests to confirm all was well - remembering to use [`uv`](https://docs.astral.sh/uv/) and ensuring it ran only the models and tests related to the changes.

And everything worked the first time. All I then had to do was commit the changes and let CI/CD do its thing, but the agent could have done that too (but I did ask it to write the commit message).

**Wow**.

## Reflections about what had just happened

Yes, it did have an existing codebase and plenty of [Cursor Rules](https://docs.cursor.com/context/rules) to reference, but still.. this felt like something different. Similar feeling of to when I first saw Github Copilot auto-complete a full Python function.

I saw with my own eyes proof that the technology and ecosystem have advanced to a point where they can start to deliver autonomously and accurately, and thus changing the role I used to play in the development process.

Yet, we are **not close** to a point where we can offload complex tasks to agents, and this is not a post about AI taking everyone’s jobs. During my Cursor-assisted dbt work I witnessed disappointing hallucinations, forgetfulness and general incompetence from the agent, even on simple tasks. Any non-trivial work required very close oversight, which could become overwhelming - to the point it would be much more efficient (and cost effective considering the pricing model of Cursor) to write the code myself.

Even so, the trajectory has become obvious to me. It clicked. Software development workflows have been jolted by a Dirac delta impulse, and there is no going back. And even if LLM scaling plateaus and we are stuck with Claude 4, the tooling and orchestration ecosystem that will effectively distribute the technology into more workflows is just getting started.

Consider the Model Context Protocol ([MCP](https://modelcontextprotocol.io/introduction)), Agent2Agent ([A2A](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)), [intelligent orchestration patterns](https://www.anthropic.com/engineering/building-effective-agents), Agent Communication Protocol ([ACP](https://agentcommunicationprotocol.dev/introduction/welcome))and the evolution to new interfaces beyond chat (for example [Vercel v0](https://v0.dev/)): these are gathering genuine momentum among development teams that are operating at the cutting edge - and even Product Managers. I am now seeing PMs ditch third-party tools and invent their own bespoke ones using Cursor and Lovable, which can share context with the codebase and existing company systems, and in the end work just fine.

Things are moving at a pace I can hardly believe. Already two months have passed since I had my “profound moment” and what felt like “cutting edge” at the time (getting Cursor to deliver Linear tickets) is now maybe already old news. For example, Cursor released a Slack integration a few days ago, which means you can do ["@Cursor fix this" from within a Slack conversation](https://docs.cursor.com/slack)! Still, it was satisfying to see recently cite this example as a cool new thing (check out his talk [Software engineering with LLMs in 2025: reality check](https://youtu.be/EO3_qN_Ynsk?si=F1QgfnXrE6enLecF))

## Coming up: How does all this impact Data Science and ML roles?

Like many, I am thinking a lot about the impact these new technologies will have on jobs and careers. In the short term, many will discover that they will need to reinvent themselves to adapt to the new reality. The tsunami is well on its way. Observing Software Engineers turning to AI Engineers almost overnight, made me reflect a lot on the role of the Data Scientist and ML Engineer, and even the Product Manager.

More on the emergence of AI Engineering and the impact on Data Science and ML roles in my next post!