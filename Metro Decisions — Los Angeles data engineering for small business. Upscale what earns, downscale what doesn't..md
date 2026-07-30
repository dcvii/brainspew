---
title: "Metro Decisions — Los Angeles data engineering for small business. Upscale what earns, downscale what doesn't."
source: "https://www.metrodecisions.com/"
author:
published:
created: 2026-07-30
description: "Los Angeles data engineering for small business. Upscale what earns, downscale what doesn't."
tags:
  - "brain_spew"
---
## Right-size your data.

Grow when you need to. Cut when you don't.

I'm Michael Bowen. I help small and mid-sized businesses in LA and OC build the data platform they actually need — and rip out the one they don't.

Forty years in data engineering. Xerox, Pilot Software, Hyperion, Boeing, Qantas, Guess, Teva, OpenText. Now local, focused, and lazy on your behalf: the smallest working system, running where you can afford it, owned by you.

Upscale

You've outgrown spreadsheets.

You need a real pipeline, a real warehouse, and reporting that doesn't take a week to change.

- **Data platforms that fit the business.** DuckDB, Postgres, S3, dbt — modern, columnar, cheap to run.
- **Pipelines you can trust.** Producer/consumer with control tables so you know where every number came from.
- **AI where it earns its keep.** Agentic workflows for specialist, repetitive work — not chatbots for their own sake.
- **Ontology-driven models** (Kermadec) so your vocabulary lives in one place and drives everything downstream.

Downscale

You're paying for software you don't use.

Legacy Essbase, an over-scoped Snowflake bill, a BI tool with three active users, a SaaS stack that's out-of-hand.

- **Migration audits.** What you have, what it costs, what it actually does.
- **Modern replacements.** DuckDB + Polars + Postgres often turns a $50K/yr line item into a $500/yr one.
- **Local-first, code-first.** Your data on your infrastructure, in files you can read, in SQL you can grep.
- **Retire dead vocabulary.** If nobody's using the report, we archive it. If nobody opens the dashboard, we delete it.

Products & practice

## The tools behind the work.

kermadec Framework

### Ontology-driven data engineering.

Describe the domain once in a shared ontology; Kermadec emits the dbt project, the schema tests, the Arrow flight schemas, and the lineage database.

- mdu emit --target dbt-project — model your business, get a running warehouse.
- SHACL → dbt schema tests — validation rules that travel with the data.
- Merged lineage in.kermadec.db — every column has a story.

The "left of go" work: get the definitions right, and the code writes itself.

metro-method Pattern

### Producer/consumer pipelines.

The pattern I've been building since 2016. S3 as the permanent record, DuckDB as the query-in-place engine, control tables for provenance.

Every ETL step named, tracked, replayable: Capture, Ingest, Cleanse, Stage, Merge, Calc, Report, Distribute.

Modern stack, timeless pattern. Works for a five-person team; scales when you grow.

### The modern SMB data stack

Storage:

S3 or local disk. Cheap, versioned, encrypted.

Warehouse:

DuckDB for analytics, Postgres for operations.

Transform:

SQL first, Polars where it earns it, dbt for orchestration.

Pipelines:

Go for producers, Python for consumers, dlt for connectors.

AI:

MCP servers, agentic workflows, LLM where domain reasoning pays.

Cost:

Usually 5–10× less than the enterprise alternative.

Whitepapers

## Read before you buy.

Short, opinionated papers on the SMB data stack. Drop your email; I'll send the PDF and one follow-up. That's it.

wp-istd

### ISTD vs Medallion.

Idempotent, Set-Transformational, Denormalized design — six named layers with unambiguous roles, versus Bronze/Silver/Gold's three-layer shorthand. Which one you want depends on where business logic lives and who is on-call at 3am.

wp-dfa

### Design for Analysis.

A lightweight, formal methodology for analytic projects — six phases, a six-point assessment, and three first principles that keep every design choice anchored to the business question instead of the tool.

Who I work with

## Small and mid-sized businesses in LA and OC.

Retail, media & entertainment, real estate, hospitality, professional services, healthcare — that:

- — Have outgrown spreadsheets but can't justify a full data team.
- — Are paying enterprise SaaS prices for tools built for the Fortune 500.
- — Want AI in their workflows without hiring a research lab.
- — Need one experienced practitioner, not a five-consultant slide deck.

If you're a two-person startup or a fifty-person shop and your data situation is "somebody knows how it works," we should talk.

About

## Forty years. One laptop.

I've been doing this for forty years — from Xerox in El Segundo and Pilot Software in Cambridge, to Hyperion, Rolta, Hackett, Solver, Full 360, OpenText, and now back to Metro Decisions, which I founded in 2001.

I've architected 42-node Vertica clusters at Guess, benchmarked AWS Vertica + Tableau at Teva, run near-real-time ETL across five time zones at Nissan, built the global engineering financial model for 17,000 Boeing projects, and integrated regulatory pilot-fatigue rules at Qantas.

That work taught me two things:

1. **Most companies own more software than they use.** Complexity is the default; simplicity takes work.
2. **The best code is the code never written.** The best system is the smallest one that solves the problem.

I'm currently converting decades of Ruby, Perl, and enterprise-stack work to Go, Python, DuckDB, Iceberg, Ducklake, Temporal, and MCP. Not because it's fashionable — because it's cheaper, faster, and fits on one laptop.

Based in Los Angeles. Available across LA and Orange County; remote for the rest.

1\. Fit call

30 minutes, free. You describe what you have and what hurts. I tell you honestly whether I'm the right fit.

2\. Assessment

1–2 weeks, fixed fee. Inventory your stack, cost it out, one-page recommendation: keep, cut, add.

3\. Delivery

Fixed-scope projects or monthly retainer. No long contracts, no minimums beyond the assessment.

Book a fit call

## Tell me what hurts.

Drop your email and the thing you're trying to fix. 30 minutes, no slides, no pitch. I'll tell you honestly whether I can help.

No newsletter. No share. One reply, from me, to schedule the call.