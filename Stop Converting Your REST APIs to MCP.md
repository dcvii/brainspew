---
title: Stop Converting Your REST APIs to MCP
source: https://www.jlowin.dev/blog/stop-converting-rest-apis-to-mcp
author:
  - "[[@jlowin]]"
published:
created: 2025-07-17
description: Your auto-generated MCP is bad, and you should feel bad.
tags:
  - MCP
---
FastMCP’s [OpenAPI converter](https://gofastmcp.com/integrations/openapi) has become the most popular tool for auto-generating MCP servers from REST APIs. I’m excited about that, because I built the feature to feel like magic: a single line of code to expose your entire REST API to an LLM. It’s the ultimate shortcut, and for quick prototypes, it’s amazing.

But now I need you to stop using it so much.

I’ve come to realize that it can paper over a fundamental problem: *an API built for a human will poison your AI agent.* In practice, LLMs achieve significantly better performance with well-designed, tailored MCP servers than with auto-converted ones. The reason goes right to the core of how agents and humans interact with software, and how we design technical products for each consumer.

A good REST API is generous. It is a model of discoverability and atomicity. It offers hundreds of single-serving endpoints, flexible parameters, and endless options because programmatic iteration is cheap. Human developers are brilliant at doing discovery once and subseqeuently ignoring what’s irrelevant, and their code can chain together atomic calls — `get_user()`, then `get_orders(user_id)`, then `get_order_details(order_id)` — with quick network hops to achieve complex outcomes. For them, more choice is good. We use properties like idempotency, pagination, and caching to make our APIs more efficient in the face of relatively deterministic access patterns.

But when you hand this interface to an agent, you’re not empowering it; you’re drowning it.

Agentic iteration is brutally expensive. First, there’s the **literal cost of context**. An LLM must process the name, description, and parameters of every single tool you provide, every single time it reasons. For an agent, many programmatic choices imply a bloated context, and every extra endpoint is a tax paid in tokens and latency on every interaction. Second, **atomicity is an agent anti-pattern**. Each tool call an LLM makes is an expensive round trip involving a full reasoning cycle. Forcing an agent to chain multiple atomic calls is slow, error-prone, and burns through tokens.

Moreover, **context pollution is the silent killer of contemporary agentic workflows.** Many users do not realize that their toolkits — including MCP servers — may inject thousands more tokens than even their custom system prompts. Your agent stops being a helpful assistant and becomes an obsessive API librarian, endlessly debating the nuances of your endpoints instead of achieving its actual behavioral goal. More tool calls reinforce that behavior, and your agent gets slower, dumber, and more expensive with every interaction.

So when I see the community’s enthusiasm for auto-generating MCP servers from massive OpenAPI specs, it makes me think:

![I've got a bad feeling about this](https://www.jlowin.dev/_image?href=%2F_astro%2Fbad-feeling.TffNxw9B.webp&w=540&h=225&f=webp)

An API that is “sophisticated” for a human is one with rich, composable, atomic parts. An API that is “sophisticated” for an agent is one that is ruthlessly curated and minimalist.

We see the practical consequences of this mismatch in FastMCP’s GitHub repo almost daily. “The LLM timed out trying to decide between create\_invoice and generate\_invoice.” “My agent hallucinated a get\_all\_users\_with\_blue\_eyes endpoint because the 50 other user-related tools made it seem plausible.” “How do I prevent the LLM from trying to call the DELETE /everything endpoint I forgot was in my spec?” These are the predictable results of a flawed premise and the belief that context should be stuffed, not pruned.

The truth is, it’s far easier to build a clean, curated MCP server than it is to debug an LLM that’s lost in the labyrinth of an auto-generated REST API. As [Maxime Beauchemin recently put it](https://www.linkedin.com/feed/update/urn:li:activity:7343322701446397953/?commentUrn=urn%3Ali%3Acomment%3A%28activity%3A7343322701446397953%2C7343333026455539713%29):

> \[We must\] not only enumerate but also qualify each service, as it’s trivial for anyone to write a quick REST-API wrapper and call it done, where in reality we’re discovering that considerations around API design for LLMs are significantly different from the ones we’ve been using for REST forever.

FastMCP’s OpenAPI converter **is** a valuable tool for bootstrapping. But we have to be disciplined. We can’t let this convenient shortcut ultimately create more problems than it solves.

So, what’s the right way forward? The goal isn’t to abandon our existing APIs, but to treat them as a source of truth to be carefully translated, not a finished product to be carelessly wrapped.

1. **Bootstrap, Don’t Deploy.** Use the `FastMCP.from_openapi()` feature for what it’s truly good for: bootstrapping. Use it to quickly explore what’s possible, to see your tools through an agent’s eyes, or to run a quick internal demo. But do not ship it to production.
2. **Curate Aggressively.** The act of curation is now a core part of building for agents. Instead of exposing the raw tool, use a transformation to craft a new, LLM-friendly version. FastMCP’s `Tool.from_tool()` was built for exactly this. Take that messy `generic_search(q, lim, fq, …)` tool and transform it into a clean `find_products(keyword: str)`. Rename cryptic arguments. Hide irrelevant parameters with default values. This is where the real work lies.
3. **Start with the Agent Story.** For your most critical workflows, build a new, minimal MCP server from scratch. Don’t start with your API spec. Start with the [agent story](https://www.jlowin.dev/blog/as-an-agent-the-new-user-story): *“As an agent, given `{context}`, I use `{tools}` to achieve `{outcome}`.”* Then, build *only* the tools required to fulfill that story.

The promise of AI agents isn’t just to make our existing software “chatty.” It’s an opportunity to design cleaner, more intentional, machine-first interfaces. **Stop converting your REST APIs. Start curating them.**