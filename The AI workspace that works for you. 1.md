---
title: "The AI workspace that works for you."
source: "https://www.notion.so/product-templates/The-Delegation-Toolkit-2d55a2ccb5268058be19d76fd9758824"
author:
  - "[[Notion]]"
published:
created: 2026-01-01
description: "A tool that connects everyday work into one space. It gives you and your teams AI tools—search, writing, note-taking—inside an all-in-one, flexible workspace."
tags:
  - "clippings"
---
## The Delegation Toolkit

#### Paste-ready prompts for reliable AI delegation (with built-in verification)

These prompts are designed for the real world: AI can attempt multi-hour work, but reliability is uneven. The goal isn’t “fire-and-forget.” The goal is structured delegation where the output is checkable, auditable, and safe to use.

You will get the best results when you treat specification as part of the work—not overhead.

### How to Use This Toolkit

#### Choose the right prompt

Under 1 hour: Use the Quick Delegation Prompt (below) or the Core Delegation Framework with fewer fields.

1–4 hours: Use the Core Delegation Framework or a specialized prompt (Research / Writing / Code / Process).

Over 4 hours: Break the work into chunks. Long runs fail quietly. Design checkpoints.

#### The default workflow

Run Prompt 7 (Spec-Writing Assistant) if you’re not sure what to specify.

Delegate using Prompt 1 or a specialized prompt (2–5).

Run Prompt 6 (Verification & QA Pass) on the output before using it.

#### The key rule (for novices)

If you don’t know what to fill in, leave it blank. Every prompt below instructs the assistant to:

Ask for missing info one question at a time

Offer reasonable options if you’re unsure

Proceed once the critical gaps are closed

### The Meta-Principle

The time you spend on the spec is the work.

A vague prompt that produces something you can’t trust is not efficiency—it’s waste. A clear spec that takes 10–20 minutes to write but produces output you can verify is leverage.

If you can’t fill in a section, that’s information: you’re not ready to delegate that part yet. Use the Spec-Writing Assistant to discover what you’re missing.

## Quick Delegation Prompt (for most people, most of the time)

Use this when you want something fast but still structured.

You are going to do a real task for me. If anything important is missing, ask me ONE question at a time (most important first). If I don’t know, give me 2–3 options and ask me to choose. Once you have enough to proceed, start immediately. TASK: - What I want: \[ \] DELIVERABLE: - What you will produce: \[ \] - Format/length/tone: \[ \] MUST-HAVES: - \[ \] - \[ \] MUST-NOTS: - \[ \] - \[ \] DONE MEANS: - \[ \] - \[ \] Now ask the single most important question you need to begin. If nothing is missing, begin.

## PROMPT 1: Core Delegation Framework

Use this for any task you expect to take 30+ minutes.

You are executing a real task for me. Execution rules: - If required info is missing, ask me ONE question at a time (most important first). - After I answer, briefly restate your updated understanding and ask the next one question. - If I don’t know, propose 2–3 reasonable options and ask me to pick. - Do not invent facts, sources, links, or citations. If you can’t verify, label it clearly. - If you are uncertain about a key decision, FLAG it and ask before proceeding. - Once you have enough to proceed, start immediately (do not wait for extra confirmation). === OUTCOME === Deliverable: \[what you’re producing\] Format: \[structure, length, file type, required sections\] Audience: \[who it’s for / what matters to them\] Quality bar: - Excellent: \[ \] - Acceptable: \[ \] - Fail: \[ \] Example of “done well” (optional): \[ \] === INPUTS & ACCESS === Materials provided (if any): \[links / pasted text / files\] Tool access: - Web browsing available? \[unknown/yes/no\] - Code execution available? \[unknown/yes/no\] - Access to my repo/files? \[unknown/yes/no\] If any are unknown, ask me. === CONSTRAINTS === Do NOT: - \[prohibited actions, assumptions, scope boundaries\] You MUST: - \[non-negotiables, standards, compliance rules\] === EDGE CASES — FLAG, DON’T GUESS === If you encounter any of these, stop and ask: - \[ambiguity type\] - \[policy/safety/security uncertainty\] - \[decision that depends on my preference\] === SUCCESS CRITERIA === I will verify completion by: - \[check 1\] - \[check 2\] “Done” means: - \[concrete condition\] - \[concrete condition\] === STOP CONDITIONS === Pause and ask if: - You detect you might be solving the wrong problem - A key dependency is missing - You need to make an irreversible decision === START === 1) Restate your understanding (brief). 2) List any missing critical info. 3) Ask me the single most important question to proceed. If nothing critical is missing, proceed to execution immediately.

## PROMPT 2: Research & Analysis Delegation

Use this for research, synthesis, recommendations—where stale data and fake citations ruin you.

You are conducting research and analysis for me. Execution rules: - If required info is missing, ask me ONE question at a time. - Do not invent sources, links, quotes, or citations. If you can’t verify, say so plainly. - If web browsing is unavailable, ask me to paste sources OR give me search queries to run. - Once you have enough to proceed, start immediately. === RESEARCH OBJECTIVE === Question to answer: \[specific question\] Scope boundaries: - Geography: \[ \] - Time window: \[e.g., last 24 months / since 2020 / etc.\] - Industry/product scope: \[ \] Depth: \[executive brief / detailed memo / comprehensive\] Output format: \[memo / report / slide outline / etc.\] === SOURCE REQUIREMENTS === Preferred source types (priority order): 1) Primary sources (official docs, filings, datasets, standards) 2) Named research orgs (if relevant): \[ \] 3) High-quality journalism (if relevant): \[ \] Avoid: - Low-trust aggregators, unsourced claims, forums (unless explicitly requested) - Anything outside the time window unless clearly labeled “historical context” For factual claims that matter (numbers, rankings, timelines, attributions, policy/legal/security claims): - Provide source name + publication date - Label primary vs secondary - If you cannot verify directly, mark \[UNVERIFIED\] and explain what would verify it === ANALYSIS FRAMEWORK === Organize around: - \[dimension 1\] - \[dimension 2\] - \[comparisons you want\] === FLAG FOR HUMAN REVIEW === Stop and surface explicitly if you find: - Credible sources contradict each other - A key claim relies on a single source - The best available info is outdated - You hit a gap that changes the recommendation === DELIVERABLE STRUCTURE === 1) Executive summary (5–10 sentences) 2) Key findings (by framework) 3) Evidence (claim → source → date → primary/secondary) 4) Limitations & gaps 5) Spot-check list (3–10 items a human should verify) 6) If browsing wasn’t available: “What I would search next” (queries) === START === Restate the research question and ask me the single most important question you need to begin. If nothing is missing, begin.

## PROMPT 3: Document / Report Creation

Use this for polished writing where the failure mode is smooth prose with hidden errors.

You are drafting a document for me. Execution rules: - If required info is missing, ask me ONE question at a time. - Do not present speculation as fact. - If you’re unsure, label uncertainty clearly and add a \[VERIFY\] tag. - Once you have enough to proceed, start immediately. === DOCUMENT SPEC === Document type: \[memo / blog post / email / brief / etc.\] Purpose: \[what this must accomplish\] Audience: \[who, what they care about, sophistication level\] Length: \[target word count or pages\] Tone: \[direct / formal / conversational / etc.\] Structure (required sections, in order): \[ \] === CONTENT REQUIREMENTS === Must include: - \[required elements\] Must NOT include: - Claims without evidence - Speculation framed as fact - Off-limits topics or frames: \[ \] === SOURCE HANDLING === If the claim comes from: - My provided materials: cite where (page/section/quote) - Your general knowledge: mark \[VERIFY\] unless it’s truly generic - Uncertain/unknown: state uncertainty + mark \[UNKNOWN\] === TAGGING (INLINE) === Use these tags in the draft: - \[VERIFY\] = I should fact-check this - \[ASSUMPTION\] = you made a judgment call - \[PLACEHOLDER\] = you need me to supply something - \[TONE CHECK\] = tone choice needs my input === OUTPUT FORMAT === 1) Outline (sections + 1–2 bullets each) 2) Draft 3) Checklist: requirements covered + where 4) \[VERIFY\]/\[ASSUMPTION\]/\[PLACEHOLDER\] roundup list === START === Ask me the single most important question you need to begin. If nothing is missing, produce the outline and start drafting.

## PROMPT 4: Code / Technical Implementation

Use this for building features/fixes where the failure mode is “runs, but wrong.”

You are implementing a technical change for me. Execution rules: - If required info is missing, ask me ONE question at a time. - Do not assume tool access. If you can’t run code or access a repo, say so and provide runnable instructions + tests anyway. - Flag security-sensitive areas as \[REVIEW\]. - Once you have enough to proceed, start immediately. === TECHNICAL SPEC === Objective: \[what it must do\] Context: \[system / repo / constraints\] Language/Framework: \[ \] Inputs: \[ \] Outputs: \[ \] Environment: \[local / server / cloud / versions\] === REQUIREMENTS === Functional: - \[ \] Non-functional: - Performance constraints: \[ \] - Security constraints: \[ \] - Error handling expectations: \[ \] === CONSTRAINTS === Do NOT: - Modify: \[files/systems\] - Use: \[libraries/patterns\] Must maintain: - Compatibility/interfaces: \[ \] === EDGE CASES === Must handle: - \[edge case → expected behavior\] If unclear, FLAG and ask. === TESTING === Include: - Unit tests for: \[ \] - Coverage for: happy path + error cases + edge cases - Manual verification steps === DELIVERABLE FORMAT === 1) Code (with comments on non-obvious decisions) 2) Tests 3) “How to run” instructions 4) Assumptions + unknowns 5) \[REVIEW\] list (what a human should inspect) === START === Ask me the single most important question you need to begin. If nothing is missing, outline the approach briefly and then write the implementation.

## PROMPT 5: Process / Workflow Execution

Use this for audits, migrations, data processing—where missing one step silently kills you.

You are executing a multi-step process for me. Execution rules: - If required info is missing, ask me ONE question at a time. - Do not skip steps. - If anything is destructive (delete/overwrite/migrate), STOP and ask for explicit confirmation first. - Maintain an audit trail. - Once you have enough to proceed, start immediately. === PROCESS OBJECTIVE === Goal (end state): \[ \] Starting point (current state): \[ \] Success looks like (checkable): \[ \] === STEPS === Execute in order. For each step include: action → expected output → verification. 1) \[Step 1\] 2) \[Step 2\] 3) \[Step 3\] (Add more as needed) === DECISION POINTS === At step \[X\], decide \[Y\] using this logic: - If \[condition A\] → do \[approach 1\] - If \[condition B\] → do \[approach 2\] - Else → STOP and ask me === ERROR HANDLING === If you encounter: - \[error type\] → \[response\] - Anything unexpected → STOP, document state, ask me === AUDIT TRAIL (REQUIRED) === Log: - Inputs processed - Outputs generated - Decisions made - Anomalies found - What to do next === FINAL OUTPUT === 1) Confirmation of end state 2) Summary of actions 3) Audit trail 4) Follow-ups + open issues 5) Evidence of verification === START === Ask me the single most important question you need to begin. If nothing is missing, execute step 1.

## PROMPT 6: Verification & QA Pass

Use this after any output. The goal is to surface issues, not patch them.

You are performing a verification pass on the deliverable I paste next. Rules: - Do not rewrite or “fix” the deliverable. - Your job is to identify errors, gaps, contradictions, and verification steps for a human. - Be concrete: issue → where → why → how to verify. === WHAT YOU ARE CHECKING === Verification objectives: - Accuracy (no false claims) - Consistency (no contradictions) - Completeness (meets requirements) - Quality (meets the stated bar) If I provided an original spec/requirements, use it. If not, infer reasonable requirements and label them “inferred.” === CHECKS === 1) Requirements traceability - List requirements → where satisfied → missing items 2) Factual claims & evidence - Flag claims that need sources or are unsupported - Flag anything that looks like a “confident guess” 3) Logic and calculations - Verify derived numbers and reasoning steps - Flag leaps and missing premises 4) Internal consistency - Conflicting numbers/definitions/terms across sections 5) Freshness (if applicable) - Flag dates that might be outdated - Identify where newer info could matter === OUTPUT FORMAT === 1) CRITICAL ISSUES (must fix before use) - issue, location, why it matters, how to verify 2) CONCERNS (review recommended) 3) MISSING REQUIREMENTS (if any) 4) SPOT-CHECK LIST (3–10 specific checks) 5) OVERALL ASSESSMENT - Ready / Needs revision / Significant rework - Confidence: High / Medium / Low - Key caveat Now ask me to paste the deliverable (and original spec if I have it). Then proceed.

## PROMPT 7: Spec-Writing Assistant

Use this when you know what you want but can’t yet specify it cleanly.

Help me write a complete delegation spec for a task. Rules: - Ask me questions ONE category at a time. - Within a category, ask only 3–6 high-leverage questions. - After I answer, summarize what you learned and show the updated spec sections. - If I don’t know an answer, propose 2–3 reasonable defaults and ask me to choose. - When the spec is complete, output a final delegation prompt I can paste into a fresh chat. TASK (rough description): \[Paste what you want done, even if messy\] CATEGORIES: 1) OUTCOME CLARITY - What does “done” look like? - What deliverable format decisions matter? 2) CONSTRAINT DISCOVERY - What must be true? - What approaches/sources/tools should be prohibited? 3) EDGE CASE IDENTIFICATION - Where could this go wrong but look right? - Where does it require human judgment? 4) VERIFICATION DESIGN - How will I check correctness? - What should I spot-check? 5) SUCCESS CRITERIA - Minimum viable deliverable vs ideal - Concrete “done means” checklist Start with Category 1. Ask me your first question.