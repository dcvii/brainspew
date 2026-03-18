---
title: "gstack: Installing Garry Tan's Claude Code Setup in One Click"
source: "https://www.sitepoint.com/gstack-claude-code-setup/"
author:
  - "[[By SitePoint Team]]"
published:
created: 2026-03-18
description:
tags:
  - "brain_spew"
---
**Disclaimer on sources and versions:** This article describes gstack as attributed to Garry Tan based on publicly circulated references. No primary source announcement has been cited. Package names, repository URLs, and installation behavior should be verified against official communications before use. Specific paths, outputs, and Claude Code behaviors may differ across versions and operating systems. Where this article says gstack does something, treat that as "gstack is reported to do something" unless you have confirmed it yourself.

gstack packages a complete, opinionated Claude Code configuration into a single install command. Instead of spending hours assembling custom instructions from scattered GitHub repos, tweets, and blog posts, you start from a working baseline and adjust from there.

This tutorial covers what gstack installs, how to run and verify the installation, what the most impactful configuration choices inside it are, and how to customize the setup for your own needs.

## What Is gstack?

### The Problem It Solves

Claude Code supports a configuration layer through CLAUDE.md files, which are persistent instruction documents that shape how the assistant behaves during coding sessions. ("Skills" in this context refers to these CLAUDE.md instruction files and any associated slash command definitions. Claude Code's official documentation may use different terminology.) The best configurations, though, amount to undocumented tribal knowledge. No official gallery of instruction sets exists. Most developers either stick with vanilla defaults and get none of the benefits of custom instructions, or spend hours manually assembling setups from scattered sources. The result is a fragmented ecosystem where expert-level configurations exist but stay locked inside individual workflows.

gstack addresses this directly. It packages a complete, opinionated configuration into a reproducible installer. Rather than reverse-engineering what works through trial and error, you start from a proven baseline and iterate from there.

### What gstack Actually Installs

gstack bundles a full opinionated stack of Claude Code instructions: code review conventions, architecture guidance, testing patterns, commit message formatting, and project scaffolding rules. At its core, the tool installs a comprehensive CLAUDE.md file that persistently instructs Claude Code how to behave, along with any associated slash commands that shape assistant behavior during coding sessions.

The repository URL should be confirmed from Garry Tan's official communications before use. **\[LINK TO BE VERIFIED BEFORE PUBLICATION\]** Inspect the full contents of the configuration files and installation logic before running anything.

## Prerequisites

You need the following before installing gstack:

- **Claude Code** already installed and authenticated. gstack layers configuration on top of an existing Claude Code installation; it does not install Claude Code itself. Check your version with `claude --version`. Confirm gstack compatibility against the versions listed in the gstack repository's README.
- If you are on Windows, use WSL. Ensure both Claude Code and your terminal session run on the same filesystem side (WSL or Windows native) to avoid path resolution issues. On macOS and Linux, any standard terminal works.
- **Node.js v18+ (LTS)** and **npm** available on your system. Verify with `node --version`.
- Confirm write access to `~/.claude/`, the directory where Claude Code reads its configuration. Verify with `ls ~/.claude/` or create it with `mkdir -p ~/.claude/`.

This is an intermediate tutorial. It assumes familiarity with command-line tools, basic filesystem navigation, and prior experience using Claude Code for at least simple tasks.

## How to Install gstack

### The One-Command Install

**Security check first:** Before executing, run `npm info gstack` to verify that the package exists on npm and that the publisher matches the expected maintainer. Inspect the `author`, `homepage`, and `repository` fields. If the command returns `npm ERR! 404 Not Found`, the package does not exist and you should not proceed. Never run an `npx` command from an unverified package.

To inspect the package more thoroughly before running it:

```
# Verify package metadata and note the published integrity hash
npm info gstack --json | grep -E '"version"|"integrity"|"_resolved"'
# Inspect package contents without executing (supply chain check)
npm pack gstack --dry-run 2>&1 | head -40
```

**Before running:** If you have an existing `~/.claude/CLAUDE.md`, back it up first to avoid data loss:

```
# Back up existing CLAUDE.md only if it exists
BACKUP_TARGET=~/.claude/CLAUDE.md.bak.$(date +%s)
if [ -f ~/.claude/CLAUDE.md ]; then
  cp ~/.claude/CLAUDE.md "$BACKUP_TARGET" && \
    echo "Backup written to $BACKUP_TARGET" || \
    { echo "ERROR: Backup failed — aborting."; exit 1; }
else
  echo "No existing ~/.claude/CLAUDE.md found — skipping backup."
fi
```

The installation is a single command. **Important:** Using `@latest` is a floating pointer. For production use, pin to a specific verified version after confirming with `npm info gstack`:

```
# Replace X.Y.Z with the verified version from npm info output above
GSTACK_VERSION="X.Y.Z"
timeout 60 npx gstack@${GSTACK_VERSION} || {
  echo "ERROR: gstack install failed (exit $?). Check network and npm registry."
  exit 1
}
```

This downloads the gstack package, copies the configuration files into the Claude Code configuration directory, and sets up the CLAUDE.md file that Claude Code reads as its persistent instruction set. Under the hood, the command resolves the gstack package from npm, executes its installer script, identifies the appropriate Claude Code configuration directory on the local system, and writes the configuration files and CLAUDE.md into place. No manual file copying or directory creation is required.

> Instead of spending hours assembling custom instructions from scattered GitHub repos, tweets, and blog posts, you start from a working baseline and adjust from there.

### Verifying the Installation

After running the install command, the terminal should display output confirming that files were written successfully. The exact output format depends on the gstack version. Verify success by confirming the file exists, is non-empty, and contains readable text:

```
# Verify installation: existence, non-empty content, and readable text format
if [ ! -f ~/.claude/CLAUDE.md ]; then
  echo "FAIL: ~/.claude/CLAUDE.md not found."
  exit 1
fi
BYTE_COUNT=$(wc -c < ~/.claude/CLAUDE.md)
if [ "$BYTE_COUNT" -eq 0 ]; then
  echo "FAIL: ~/.claude/CLAUDE.md exists but is empty (possible partial write)."
  exit 1
fi
file ~/.claude/CLAUDE.md | grep -qiE 'text|ascii|utf' || {
  echo "WARN: File may not be valid UTF-8 text — inspect manually."
}
echo "OK: ~/.claude/CLAUDE.md present, ${BYTE_COUNT} bytes."
head -5 ~/.claude/CLAUDE.md
```

If the file exists and contains structured instructions covering code review, architecture, testing, and commit conventions, the installation succeeded.

If you cannot find the file at `~/.claude/CLAUDE.md`, locate Claude Code's actual config directory. On macOS this is typically `~/.claude/`; on Linux it may differ. Consult `claude --help` or the official Claude Code documentation for the `--config-dir` flag or equivalent.

**Common issues and troubleshooting:**

- **Permission errors:** If the command fails with an EACCES or permissions error, check that the current user has write access to the `~/.claude/` directory. Avoid using `sudo` with `npx`; instead, fix the directory ownership.
- **Wrong directory:** If Claude Code was installed with a non-default configuration path, gstack may write files to a location Claude Code does not read from. Verify the Claude Code configuration directory and move files manually if needed.
- **Claude Code not found:** gstack configures Claude Code but does not validate that Claude Code is installed. If the configuration does not appear to take effect after installation, confirm that Claude Code itself is properly installed and authenticated.

### Reverting the Installation

To revert gstack's changes, remove the installed CLAUDE.md and restore your backup. **Warning:** This sequence will permanently delete your current CLAUDE.md. Only proceed if you have a verified backup:

```
# Revert gstack installation safely
if [ ! -f ~/.claude/CLAUDE.md.bak ]; then
  # Check for timestamped backups
  LATEST_BAK=$(ls -t ~/.claude/CLAUDE.md.bak.* 2>/dev/null | head -1)
  if [ -z "$LATEST_BAK" ]; then
    echo "ERROR: No backup found at ~/.claude/CLAUDE.md.bak or ~/.claude/CLAUDE.md.bak.* — aborting revert."
    echo "Locate your previous CLAUDE.md manually before proceeding."
    exit 1
  fi
  echo "Using timestamped backup: $LATEST_BAK"
  BACKUP_SOURCE="$LATEST_BAK"
else
  BACKUP_SOURCE=~/.claude/CLAUDE.md.bak
fi
rm ~/.claude/CLAUDE.md && \
  cp "$BACKUP_SOURCE" ~/.claude/CLAUDE.md && \
  echo "Revert complete." || \
  echo "ERROR: Revert failed — check ~/.claude/ manually."
```

## What's Inside the gstack Configuration

### Key Instructions Breakdown

The CLAUDE.md file gstack installs is not a loose collection of tips. It is a structured instruction set that shapes Claude Code's behavior across the full development lifecycle. The most impactful areas:

Without custom architecture guidance, Claude Code tends to over-engineer simple tasks, reaching for abstractions when a flat function would do. gstack's architecture decision conventions tell Claude Code how to reason about system design choices, when to suggest abstractions versus keeping things concrete, and how to frame trade-offs when proposing structural changes.

The configuration also encodes code review rules: what Claude Code should flag during review, including security concerns, performance implications, naming inconsistencies, and test coverage gaps. These rules encode an opinionated but practical standard for what "good code" looks like when you are trying to ship, not pass an academic review.

> The CLAUDE.md file gstack installs is not a loose collection of tips. It is a structured instruction set that shapes Claude Code's behavior across the full development lifecycle.

Testing conventions govern how Claude Code generates and suggests tests. This covers test naming, fixture organization, and when to prefer integration tests over unit tests. Commit message formatting rules enforce a consistent style, typically following conventional commit patterns, so that Claude Code's suggested commits land merge-ready without manual editing.

The following is an **illustrative example** of the type of rules a CLAUDE.md might contain. **Do not copy this block into your configuration; it is a placeholder, not actual gstack output.** Verify actual installed content with `cat ~/.claude/CLAUDE.md` after installation:

```
<!-- ILLUSTRATIVE EXAMPLE ONLY — NOT INSTALLED BY GSTACK -->
<!-- Run: cat ~/.claude/CLAUDE.md to see actual installed content -->
## Code Review Rules
- Always check for security implications before suggesting code changes
- Flag any function longer than 50 lines as a candidate for refactoring
- Prefer composition over inheritance when suggesting architectural patterns
- When reviewing, consider backward compatibility with existing API consumers
- Never suggest disabling linting rules without explicit justification
```

This kind of concrete, rule-based instruction is what transforms Claude Code from a generic assistant into a coding partner that reflects a specific engineering philosophy.

### Customizing gstack After Installation

gstack's output is plain text files. After installation, every file is fully editable. The primary file to modify is `~/.claude/CLAUDE.md`. You can add, remove, or reweight instructions to match personal or team preferences.

Configuration files live in the `~/.claude/` directory structure. You can add new instruction categories, adjust thresholds in existing rules (like the function length threshold in the example above), or add project-type-specific instructions for frameworks you commonly use.

For long-term maintenance, fork the gstack repository on GitHub once you have confirmed the repository URL, apply your modifications to the fork, and pull upstream changes as they land. This preserves your ability to benefit from ongoing improvements while keeping custom overrides in place.

## How gstack Compares to Other Claude Code Setups

| Criteria | Vanilla Claude Code | Manual Curation | Community Packs | gstack |
| --- | --- | --- | --- | --- |
| Install Effort | None (default) | High (hours of research and assembly) | Medium (minutes to hours depending on source count) | One command |
| Pre-configured Instructions | None (CLAUDE.md support exists but no instructions ship by default) | Depends on time invested | Depends on pack scope | Full opinionated stack |
| Customizability | N/A | Full | Moderate | Full (fork and extend) |
| Maintained By | Anthropic | You | Community | Attributed to Garry Tan (verify from official sources) |
| Best For | First-time explorers | Power users with specific workflows | Experimenters | Developers wanting a ready-made baseline |
| Key Downside | No instructions out of the box | Time-intensive to build and maintain | Quality and maintenance vary widely | Opinionated defaults may conflict with existing team conventions |

Vanilla Claude Code is the right choice for someone just exploring the tool for the first time, where configuration overhead would be premature. Manual curation makes sense for power users with highly specific workflows who want total control from day one.

Community skill packs offer middle ground but vary in quality and maintenance cadence. gstack occupies a specific niche: a strong starting point for intermediate developers who want to be productive immediately with Claude Code and customize later. The attribution to a high-profile builder provides a degree of confidence, though you should independently verify the maintainer and inspect the source before relying on any third-party configuration.

## Tips for Getting the Most Out of gstack

### Pair It with Your Project-Specific CLAUDE.md

gstack sets a global baseline that applies across all Claude Code sessions. For maximum effectiveness, layer project-specific CLAUDE.md files in individual repositories. These project-level files can specify framework conventions, API naming patterns, database schemas, and other context that a global configuration cannot capture. Claude Code reads both files. The Anthropic Claude Code docs describe this merging behavior at [docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code). Verify the current precedence rules there, as behavior may change across Claude Code versions.

### Keep It Updated

Re-run the install command with a verified version number to pick up changes. To stay informed, watch the gstack GitHub repository for releases once you have confirmed the correct URL.

### Share Your Extensions

If the gstack repository accepts contributions (check for a CONTRIBUTING.md or pull request guidelines in the repo), developers who build useful extensions on top of gstack's base, such as framework-specific rules for Next.js, Rails, or Go, can contribute them back. Claude Code configuration sharing is still young, and shared, version-controlled instruction sets will likely become as standard as shared linting configs.

> As AI coding tools mature, configuring them effectively is becoming a skill in its own right. gstack makes expert-level setups more accessible, closing the gap between a newcomer's Claude Code experience and that of someone who has spent months refining their workflow.

## One Command to a Working Claude Code Setup

gstack delivers an opinionated Claude Code setup, cutting the hours you would otherwise spend researching and iterating to reach a comparable breadth of instruction coverage across code review, architecture, testing, and commit conventions. As AI coding tools mature, configuring them effectively is becoming a skill in its own right. gstack makes expert-level setups more accessible, closing the gap between a newcomer's Claude Code experience and that of someone who has spent months refining their workflow.

The next step is direct: verify the package with `npm info gstack`, install gstack with a pinned version, apply it to an active project, observe where the defaults align with your workflow and where they diverge, and customize from there. For Claude Code fundamentals, the [Anthropic Claude Code documentation](https://docs.anthropic.com/en/docs/claude-code) is the canonical reference.