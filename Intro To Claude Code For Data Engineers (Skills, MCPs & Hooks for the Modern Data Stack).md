---
title: "Intro To Claude Code For Data Engineers (Skills, MCPs & Hooks for the Modern Data Stack)"
source: "https://thepipeandtheline.substack.com/p/intro-claude-code-for-data-engineers?publication_id=1196229&post_id=188027352&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Alejandro Aboy]]"
published: 2026-02-26
created: 2026-02-26
description: "MCP, Skills, and Hooks turn Claude Code into a control layer for the entire data stack. Here's the map."
---
### MCP, Skills, and Hooks turn Claude Code into a control layer for the entire data stack. Here's the map.

> Hi there! Alejandro here 😊
> 
> Subscribe if you like to read about technical data & AI learnings, deep dives!
> 
> Enjoy the reading and let me know in the comments what you think about it 👨🏻💻

## 📝 TL;DR

- Claude Code connects to the entire data stack through MCP servers, Skills, and Hooks. Orchestration, modeling, databases, quality, docs.
- Data modeling has the most mature integrations: dbt Agent Skills with benchmarked accuracy gains and OpenMetadata MCP for impact analysis.
- MCP Data Toolbox gives you a single configuration layer for 30+ databases instead of managing one MCP per database.
- The real power is chaining. Multiple MCPs running in one session and you will start building custom use cases to match your workflows.
- Coming Soon: [Hands-On Claude Code for Data Engineers: Data Modeling with dbt, Miro & PostgreSQL Using Skills & MCPs](https://thepipeandtheline.substack.com/p/claude-code-for-data-engineers-data-modeling-dbt-miro-postgresql-skills-mcp)

---

## 🔧 Across the Data Stack

Data engineers already work across 5-10 tools daily. Airflow for orchestration, dbt for transformations, Snowflake or BigQuery for warehousing, pytest for quality, Git for version control.

Claude Code can help here, since it connects those tools through three mechanisms:

- **MCP servers** connect Claude Code to external tools in real time. Databases, orchestrators, metadata catalogs.
- **Skills** encode best practices that Claude follows automatically. dbt modeling patterns, testing strategies, migration guides.
- **Hooks** trigger actions before or after Claude does something. Run pytest before every commit, lint SQL on save.

I’ve been tracking these integrations we will discuss and here’s where things stand. Not every one is equally mature. Some are production-ready, others are early experiments

> **Recommended**: [The Non-Coder’s Guide to Claude Code](https://leadershipinchange.com/p/the-non-coders-guide-to-claude-code) if you need the fundamentals. This article goes deeper into data-specific integrations.

Let’s get started!

![](https://substackcdn.com/image/fetch/$s_!iyNd!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8d23c583-484c-49e9-bb80-8d7194b5218f_1024x1536.png)

image generated with ChatGPT.

---

## 🛠️ Deep Dive: Data Modeling with Skills and MCPs

Data modeling is where Claude Code has the most mature ecosystem for data engineers. Two angles here: Skills that teach Claude how to model, and MCPs that give it access to metadata.

### dbt Agent Skills

[dbt Agent Skills](https://github.com/dbt-labs/dbt-agent-skills) encode analytics engineering workflows that Claude follows as instructions. Some of them require dbt Cloud, but here are the ones working with dbt Core:

**Works with Core/OSS**:

- `using-dbt-for-analytics-engineering` \- build and modify models, debug errors, explore sources
- `adding-dbt-unit-test` \- unit tests and test-driven development
- `running-dbt-commands` \- CLI commands with correct flags and selectors
- `fetching-dbt-docs` \- look up dbt documentation efficiently

**Cloud-only**: semantic layer building, natural language queries, job troubleshooting, Fusion migration.

The bottomline is that they improve documentation by default, help you write all dbt semantics and metadata way faster, and keep your project fully compatible with dbt’s latest best practices.

> **Recommended**: [What’s the real deal about SKILLs (This is not an ‘MCP is dead’ post](https://thepipeandtheline.substack.com/p/whats-the-real-deal-about-skills)

### OpenMetadata MCP for Impact Analysis

The other side of data modeling is understanding what happens when you change something. OpenMetadata MCP connects Claude to your metadata catalog, so before modifying a dbt model, Claude can check what dashboards depend on it, who owns the downstream data, and whether there’s PII involved.

> **Recommended**: [End To End Agentic Data Modeling - Using AI and OpenMetadata MCP](https://pipeline2insights.substack.com/p/end-to-end-agentic-data-modeling-with-openmetadata-and-mcp) where we built a full end-to-end setup with PostgreSQL, dbt, Metabase, and OpenMetadata. The use cases there (impact analysis on schema changes, lineage exploration, data discovery) are exactly what this MCP enables inside Claude Code.

---

---

## ⚡ Hooks: Automating Quality Gates

Hooks are the part of Claude Code that most data engineers sleep on. They run shell commands before or after Claude does something. Think of them as CI/CD, but inside your AI workflow.

Three hooks that make a real difference:

### pytest before every commit

Claude writes a transformation function, stages it, and tries to commit. The hook runs your test suite first. If tests fail, the commit doesn’t happen. No bad code gets through.

```markup
{
  “event”: “PreCommit”,
  “command”: “python3 -m pytest tests/ -x -q”
}
```

### SQL lint on file save

Every time Claude writes or modifies a \`.sql\` file, sqlfluff checks it against your team’s style rules. Catches formatting issues, naming conventions, anti-patterns before they reach code review.

```markup
{
  “event”: “PostToolUse”,
  “matcher”: “Write|Edit”,
  “command”: “sqlfluff lint --dialect snowflake $FILE_PATH”
}
```

### dbt test after model changes

Claude creates or modifies a dbt model. The hook automatically runs \`dbt test\` on that model. If a schema test or data test fails, you know immediately instead of finding out in production.

```markup
{
  “event”: “PostToolUse”,
  “matcher”: “Write|Edit”,
  “command”: “dbt test --select $(basename $FILE_PATH .sql)”
}
```

The pattern here is simple. Don’t trust the AI to remember quality checks. Automate them so they can’t be skipped.

> **Pro Tip**: Ask Claude Code to create a “validation” skill to run before every new commit or edit so it will combine all of these actions into one.
> 
> **Docs**: [https://code.claude.com/docs/en/hooks](https://code.claude.com/docs/en/hooks)
> 
> **Recommended**: [Pytest for Data - Fixtures, Mocks, CI-CD, and Claude Code Hooks](https://thepipeandtheline.substack.com/p/i-learned-pytest-after-testing-in) for the full setup.

---

## 🗄️ Deep Dive: MCP Data Toolbox

Direct database access via MCP is the number one use case I see. But if your team uses PostgreSQL, BigQuery, and Snowflake, do you really want to manage three separate MCPs?

### The Unified Approach

[MCP Data Toolbox](https://googleapis.github.io/genai-toolbox/getting-started/introduction/) is Google’s open-source unified layer. It supports 30+ databases through a single \`tools.yaml\` configuration.

What it gives you:

- **Schema discovery** \- Claude can explore tables, columns, and relationships across databases
- **Query execution -** read and write operations with connection pooling
- **Result caching** \- avoid repeated expensive queries

It sits between Claude Code and your databases as a control plane. Instead of one MCP per database, you configure all connections in one place.

### When to Use Individual MCPs Instead

Data Toolbox covers the common ground. But some databases have features that go beyond SQL. [Snowflake MCP](https://github.com/Snowflake-Labs/mcp) for Cortex (RAG, semantic modeling, agentic orchestration), [PostgreSQL MCP Pro](https://github.com/crystaldba/postgres-mcp) for health analysis and index recommendations, [MotherDuck MCP](https://github.com/motherduckdb/mcp-server-motherduck) for local dev and prototyping.

**What I’d recommend for most teams:** Data Toolbox as the default, plus one specialized MCP for your primary warehouse.

---

---

## 🔄 Orchestration

[Airflow MCP](https://github.com/astronomer/agents/tree/main/astro-airflow-mcp) lives under Astronomer’s GitHub but works with any open-source Apache Airflow instance (2.x and 3.x). No Astronomer account needed. It connects via the standard Airflow REST API, so just set `AIRFLOW_API_URL`, `AIRFLOW_USERNAME`, and `AIRFLOW_PASSWORD` and you’re set.

The Airflow MCP tools I find most useful:

- `explore_dag` \- get DAG metadata, tasks, recent runs, and source code in one call
- `diagnose_dag_run` \- debug a failed run with task details and logs without opening the UI
- `get_system_health` \- health status, import errors, warnings, DAG stats

Beyond read-only monitoring, it also handles DAG management (trigger, pause/unpause), pool and variable management, and connection handling. Pair it with Context7 so Claude uses the right operator signatures for your Airflow version when generating DAGs.

Astronomer recently launched [Airflow Skills](https://github.com/astronomer/agents/tree/main/skills), while some of them are Astronomer exclusive, others are compatible with open source Airflow setups, so it’s worth taking a look.

---

## 🤯 Bonus: From Conceptual to Physical Models in One Session

If you design conceptual data models on Miro when drafting your dimensional and fact tables, you can wire that up to Claude Code with the [Miro MCP](https://github.com/miroapp/miro-ai). Browse existing boards, generate entity relationship diagrams from descriptions, and iterate on schemas visually.

But the real value is chaining it with everything else:

- Read business requirements from a Jira or Notion MCP.
- Explore raw database tables with MCP Data Toolbox to understand what’s available.
- Draft and iterate schemas visually on Miro MCP.
- Generate the physical dbt models using dbt Agent Skills, fully documented and following your project conventions.
- Run impact analysis with OpenMetadata MCP before merging.

> **Recommended**: [How AI Can Improve Your Data Modeling (And What’s Still Missing)](https://thepipeandtheline.substack.com/p/how-ai-can-improve-your-data-modeling) where we explored the gap between conceptual design and physical implementation.

---

## 📚 Docs-as-MCP

This is not only for Data Engineering projects but for most coding projects requiring documentation.

Claude will hallucinate API signatures when its training data doesn’t match your tool versions.

You can inject current docs into context. [Context7](https://github.com/upstash/context7), use [gitingest](http://gitingest/) to convert any repo into a queryable digest, or use tools like [docs-mcp-server](https://github.com/arabold/docs-mcp-server) to make sure Claude works with the right API signatures.

---

## Final Words

Now that we have the tools, we still need to figure out the best way to make them work together in our favor.

There’s no correct approach, the only valid one is the one that works for you!

---

If you enjoyed the content, hit the like ❤️ button, share, comment, repost, and all those nice things people do when like stuff these days. Glad to know you made it to this part!

---

![](https://substackcdn.com/image/fetch/$s_!BvlN!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0c07b7dd-718f-4687-8769-56706a030950_1024x1024.jpeg)

*Hi, I am Alejandro Aboy. I am currently working as a Data Engineer. I started in digital marketing at 19. I gained experience in website tracking, advertising, and analytics. I also founded my agency. In 2021, I found my passion for data engineering. So, I shifted my career focus, despite lacking a CS degree. I’m now pursuing this path, leveraging my diverse experience and willingness to learn.*