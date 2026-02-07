---
title: "LLMs on Urbit • Blog"
source: "https://urbit.org/blog/llms-on-urbit"
author:
published:
created: 2026-02-05
description: "A walkthrough of how to use current Urbit LLM tooling by ~niblyx-malnus"
tags:
  - "clippings"
---
Blog

## LLMs on Urbit

### A walkthrough of how to use current Urbit LLM tooling by ~niblyx-malnus

### 2026-1-27

~niblyx-malnus

![llms on urbit image](https://s3.us-east-1.amazonaws.com/urbit.orgcontent/Blog/Blog_LLMs+on+Urbit_Social+16x9.png)

The following constitutes an overview of the progress we have made atGroundwire towards the integration of LLMs into the process of softwaredevelopment on Urbit and the development of general purpose LLM personalassistants on Urbit. The aim of this article is to elucidate themotivations and guiding principles behind this work, shed light on itsunderlying structure, and to make these repos accessible for direct use andfurther independent development.

The work centers on two repos: **clurd**, a Python script that givesClaude Code direct access to a running Urbit ship's Dojo, and **urbit-master**, an experimental desk for building an LLM-powered"everything app" on Urbit. `clurd` is stable and has been tremendouslyuseful for development. `urbit-master` is in active flux - it containsmost of the interesting ideas but changes frequently. This articledocuments `urbit-master` as it exists at [commit `1ce76a3`](https://github.com/gwbtc/urbit-master/commit/1ce76a376b7b174ca003e3c86b1927ab1875210e).

In this article we will cover:

- A summary of 'Clurd'
- An overview of Urbit-master
- How to get setup
- Guiding Principles
- A detailed exploration of Urbit-master
	- Internal Structure
	- `sailbox`
	- `tarball`

## Clurd - a summary

This article will focus mostly on `urbit-master`, but first I'll give abrief summary of `clurd`.

`clurd` is a Python script enabling agentic, terminal-based LLMs likeClaude Code to interact directly with a running Urbit ship. Using thistool, Claude Code has access to generators and threads and can runarbitrary Hoon code directly in the Dojo. The project emerged out ofexplorations into the highest-leverage way to use Claude Code to buildon Urbit.

Early experiments involved simply giving Claude Code local access to thecore repos - `urbit/urbit`, `urbit/vere`, `docs.urbit.org` - to teach itHoon. It quickly became apparent that Claude was already conversant inHoon. It even was capable of giving a pretty thorough and accurateexplanation of %spider. The problem wasn't knowledge but feedback: itscode frequently failed to compile. It did, however, adjust fairly wellwhen error output was manually copied back into the conversation.

In addition to the obviously exciting idea of giving an LLM generalaccess to an urbit ship, the idea of giving Claude access to tightfeedback loops for writing and compiling code motivated the constructionof a simple tool for writing to and reading from the Dojo.

It occurred to me that `webterm` already exposes the Dojo over HTTP. Aftersome tinkering, I pointed Claude at the `webterm` repo and told it to dowhat `webterm` does: submit characters one at a time to the main Dojosession, listen to the same endpoints `webterm` listens to, reconstructthe terminal output the same way `webterm` reconstructs it, and return theresult after a timer expires.

That's basically all `clurd` is - a Python script that pretends to be `webterm`, giving Claude Code a direct line to the Dojo; a simple hackthat opened up new horizons and allowed a shift in focus from allowingLLMs to interact with Urbit *at all* to allowing LLMs to interact withUrbit *effectively*.

## Urbit-master - an overview

Before exploring `urbit-master` in greater detail I will provide someinstructions for setup. But before that I'd like to give an overview ofwhat `urbit-master` actually is and why it exists.

The purpose of `urbit-master` is to be a place for me to develop smalltools to facilitate daily life; tools that help me organize my thoughtsand aims and to coordinate them across time, and eventually tocoordinate them with other people. It posits that today LLMs are anindispensable tool to this end.

At commit `1ce76a3` it provides: a web-based Claude chat interface withconversation branching, an MCP server exposing Urbit-native tools toexternal LLM clients, a task management system (open-loops), scheduledautomation (alarms), Telegram notifications, S3 integration for backup,and a file browser for viewing and managing state as ordinary files.

The underlying architecture is built on two key libraries: `sailbox`,an agent wrapper based on thread-like "fibers" enablingasync/await-style programming in Hoon, and `tarball`, afilesystem-as-state abstraction that makes state legible and portable.

## Setup

### Prerequisites

- A running Urbit ship
- API keys for desired integrations (Claude, Telegram, Brave, S3)

### Installation

```bash
# Clone the repo
git clone https://github.com/gwbtc/urbit-master
cd urbit-master
```

### Configuration

```bash
# Copy example config
cp config.example.json config.json
```

Edit `config.json` with your credentials:

```json
{
  "ship_url": "http://localhost:8080",
  "access_code": "your-access-code",
  "telegram": {
    "bot_token": "...",
    "chat_id": "..."
  },
  "s3": {
    "access_key": "...",
    "secret_key": "...",
    "region": "...",
    "bucket": "...",
    "endpoint": "..."
  },
  "claude": { "api_key": "..." },
  "brave": { "api_key": "..." }
}
```

*Note: `claude` and `brave` keys are not in `config.example.json` butare expected by the scripts.*

### Push credentials to ship

```bash
./urbit-master update all
```

### Sync desk to ship

In Dojo, create and mount the desk:

```
|new-desk %master
|install our %master
|mount %master
```

Then run `sync.sh` in a separate tmux pane or window (it watches for changes):

```bash
./sync.sh
```

Or simply replace the contents of `[your ship]/master` with the contents of `[urbit-master repo]/desk`

Finally, commit in Dojo:

```
|commit %master
```

### Verify

```bash
./urbit-master status                      # Check connectivity
./urbit-master test mcp tools/list         # List available MCP tools
```

Once running, visit `/master` in your browser (e.g.,`http://localhost:8080/master`) to see the main interface.

### Two Ways to Use Claude

**1\. Chat Interface (Claude API)**

The web-based chat at `/master/claude` uses the Claude API directly.This requires a Claude API key configured in `config.json` and pushed tothe ship.

To get an API key: create an account at [platform.claude.com](https://platform.claude.com/), then generate an APIkey at [platform.claude.com/settings/keys](https://platform.claude.com/settings/keys).

**2\. Claude Code via MCP**

Claude Code can connect to the ship's MCP endpoint to access tools (openloops, alarms, telegram, etc.) while working locally.

In your terminal, add the MCP server:

```bash
claude mcp add --transport http urbit-master http://localhost:8080/master/mcp \
  --header "Cookie: urbauth-~your-ship=your-cookie-value"
```

(Replace `localhost:8080` with your ship's URL and set the `urbauth` cookie for your ship.)

These are independent - you can use one or both.

### Setting Up Telegram Notifications

To use the Telegram integration, you need a bot token and chat ID.

**Create a bot:**

1. Open Telegram and search for `@BotFather`
2. Send `/newbot` and follow the prompts (name your bot, give it ausername ending in `bot`)
3. BotFather will give you an API token - save this for `config.json`

**Get your chat ID:**

1. Start a chat with your new bot (send it any message)
2. Visit `https://api.telegram.org/bot<YourBotToken>/getUpdates`
3. Look for the `chat.id` field in the JSON response

**Test it:**

```
https://api.telegram.org/bot<YourBotToken>/sendMessage?chat_id=<ChatID>&text=test
```

### Setting Up clurd (Optional)

`clurd` lets Claude Code interact directly with a running Urbit ship -running generators, threads, and arbitrary Hoon in the Dojo.

1. Clone the repo:
	```bash
	git clone https://github.com/niblyx-malnus/clurd
	cd clurd
	```
2. Copy and edit the config:
	```bash
	cp config.example.json config.json
	```
	Set your `ship_url` and `access_code`.
3. Point Claude Code at the README:
	```bash
	Read the README.md in this project to learn how to use the available tools.
	```

Once configured, Claude Code can run Hoon directly on your ship duringdevelopment sessions.

---

## Guiding Principles

The emergence of `urbit-master` has been and continues to be guided by a handfulof underlying principles which I will elaborate here.

**For development:**

- Tight feedback loops are most desirable - new code can be tested earlyand often, adjustments made quickly.
- Most important errors should be caught at compile time.
- Tight feedback loops require *low-stress* iteration - if every changefeels risky, you slow down.
- This is enabled by: graceful state migration across upgrades, and easybackup to Earth.
- Robustness and speed are mutually reinforcing: the safety net enablesthe speed.

**Tools and interfaces:**

- Tools are used through interfaces.
- The interface must be as simple and legible as possible, balancingease of use with transparency to the underlying structure.
- Tool and interface constrain and shape one another.
- Therefore: put a tool under development in direct contact with themedium of its final interface as early as possible, so tool andinterface can be developed iteratively as a single system.

**Structure and process:**

- New structure emerges to support new processes, which are invited bynew desires, demands and opportunities.
- These only emerge in the context of actively inhabited structure -structure which persists by virtue of facilitating an ongoing activeprocess.
- New processes must elaborate, amplify or replace old processes asgracefully as possible.
- In particular: memory and data which current processes rely on mustnot be unduly disturbed and must be adapted seamlessly to new structure.
- More plainly: we need a system which can be actively relied on forimportant daily tasks while simultaneously being actively developed toimprove and extend function through rapid iteration - unburdened byextreme caution to avoid state destruction or meticulous attention tocomplicated state migration.

**What to build - Start simple and concrete:**

- Build simple tools that can be directly useful to you in your dailylife for the things you actually do.
- Choose things that could benefit from being networked but don't require it
- Examples: an alarm clock, an egg timer, a notepad, a todo list, thecalendar *on your fridge*, a recipe collection with useful metadata, aplace to tally weekly mileage, a simple tool to track your lifts.
- It is easier to generalize and abstract a concrete, well-understoodtool than to build a general tool from scratch that serves many purposes.
- It is easier to network a concrete and well-understood tool that manypeople use than to build a networked tool from scratch before anyoneuses it.

**Synchronization and coordinated action across time:**

- For you and for your computer, synchronization, rhythms,coordinated action across time and deferred plans triggering action at afuture moment are critical.
- The first `urbit-master` MCP tool built was the Telegram notificationstool; a dead-simple, no-frills but workable notification system. Yourship can tell you when something has happened, remind you to dosomething, or nudge you at a scheduled time.
- This has also begun to be generalized as a general purpose tool-schedulingsystem akin to cron jobs.
- Synchronization and coordination across the network is the desired end goal.

**Asynchronous "imperative" programs (Urbit thread-like things)**

- We want to give LLMs access to tools.
- Tool use implies action, action implies command, command impliesspecifying what to do under various conditions informed in part by an orderedhistory of previous actions - in other words, imperative programming.
- Many tools interact with real networks or things locally conceived of asnetworks before completion - they have an asynchronous character.
- When you want to *do* things, think in terms of Urbit "threads".

**Networks of autarkies:**

- There is something in the spirit of Bitcoin which I have absorbedthrough recent exposure that suggests that the healthiest networksamount, paradoxically, to networks of little autarkies.
- A healthy network must be robust to failures of communication at everyscale, including at the level of the "application".
- Most applications should be locally useful first.
- Networking an existing application amounts to specifying a lightweightand minimal protocol - as in all likelihood it will resist being changed.
- In principle, even different, independently developed tools thatperform similar functions might be networked by the same protocol.
- Applications that must be networks first are typically nothing morethan such protocols.

**Legible state and practical backup:**

- State should be legible and portable as conventional files anddirectories - easy to move in and out of Urbit as they are understood ona conventional Unix filesystem.
- It should be easy and trivial to back up your state to "Earth" - theworld of normal conventional computing as it exists today - whether toyour local machine or to a server.
- This informs the `tarball` filesystem-as-state design, the S3integration (which provides the practical bridge for backing up stateto conventional cloud storage), and the web-based file browser at `/master/ball` which lets you view, upload, download, and manage stateas ordinary files.

**Recoverable processes (not yet implemented):**

- All active processes should be recoverable directly from state, evenstate imported from Earth in a normal directory structure.
- If you restore a backup, your alarms, scheduled tasks, and ongoingprocesses should resume - not just your data.

**Sandboxing via namespace (not yet implemented):**

- Terminal-based agentic LLMs think of themselves as living somewhere ina namespace and running commands somewhere in a namespace.
- Anything on Urbit can be conceived of as a "poke" emitted by one locationin a namespace and sent to another.
- A poke might simply climb to the nearest ancestor and then descend toits destination.
- Security becomes: for each node in the namespace, specify whatdestinations can be emitted up through that node.

---

## urbit-master

### App Features (outside MCP)

**Claude Chat Interface**

- Multiple persistent conversations
- Conversation branching (explore alternative discussion paths from any message)
- Real-time streaming responses via SSE
- Context management with character/token caps
- Interrupt button for in-flight requests
- Tool approval UI (approve/deny/always-allow)
- Rate limiting retry/backoff

**Credential Management**

- Stores API keys/secrets for Claude, Telegram, S3, Brave
- Configurable via HTTP endpoints

**State Browser (`/master/ball`)**

- Web-based file browser for viewing state as directories and files
- Upload files, create folders, create symlinks
- Download any directory as a `tarball`
- Delete files and folders

**MCP Server**

- Exposes an MCP (Model Context Protocol) endpoint at `/master/mcp`
- Allows Claude to call Urbit-native tools during conversation

### MCP Tools

**External Integrations**

- Telegram notifications
- Web search via Brave API *(not working at this commit)*

**Scheduled Automation (Alarms)**

- Schedule any MCP tool to execute at specific times
- Recurring executions with configurable intervals
- ISO-8601 duration support

**Task Management (Open Loops)**

- Create, close, reopen, delete tasks
- Labels/tags system
- Due dates (best-by)
- Search/filter by text regex, labels, state

**Desk Management**

- Commit desks and get version info

**Miscellaneous**

- Generate random values (integers, floats, booleans, UUIDs) *(buggy)*

### System Information

With each API request, the system prompt includes live context:

- Ship name (e.g., `~zod`)
- Current time in user's timezone (e.g., "Wednesday 2025-01-15 3:42pm EST")
- Chat ID
- Context window stats: messages in context / total, chars / max chars,truncation status
- Message ranges with ISO-8601 timestamps
- Open loops system guidance (how to use the task tracking tools)

---

## Internal Structure

### Core Infrastructure

**`lib/sailbox.hoon`** - Fiber-based agent wrapper

- Wraps standard gall agent
- Provides async/await pattern via fibers
- Handles SSE connections
- *Why it matters:* enables imperative async programming

**`lib/sailboxio.hoon`** - IO primitives for fibers

- State read/write operations
- HTTP request/response helpers
- Card emission
- *Why it matters:* the verbs available inside a fiber

**`lib/tarball.hoon`** - Filesystem-as-state

- Hierarchical file storage using `axal`
- Typed read/write with marks
- Path operations (mkdir, list, get, put)
- *Why it matters:* enables flexible state without complex migrations

### The Agent

**`app/master.hoon`** - The main agent

- Surprisingly small because logic lives in libraries
- Defines: initial state, migration, process handler, SSE hooks
- Routes HTTP to appropriate handlers
- *Why it matters:* the entry point, shows how pieces connect

### Routing & HTTP

**`lib/routes/master.hoon`** - Top-level router

- Dispatches GET/POST to sub-routers
- Authentication checks
- *Why it matters:* how requests find their handlers

**`lib/routes/claude.hoon`** - Chat interface routes

- Chat CRUD, message handling, streaming
- *Why it matters:* the main user-facing feature

### What is MCP?

The [Model Context Protocol](https://modelcontextprotocol.io/) (MCP) isan open standard introduced by Anthropic in November 2024 for connectingLLMs to external tools and data sources. It has since been widelyadopted (OpenAI, Google, Microsoft, etc.).

**The core idea:** Before MCP, LLMs could call tools, but everyintegration was bespoke. MCP standardizes the interface so one toolimplementation works with any MCP-compatible client (Claude Code,ChatGPT, custom agents, etc.).

**How it works:**

- JSON-RPC 2.0 over HTTP (or stdio)
- `initialize` - handshake, capability negotiation
- `tools/list` - client asks "what tools do you have?"
- `tools/call` - client invokes a tool with arguments, gets result

**In `urbit-master`:**

The MCP implementation is split into two files:

1. **`lib/mcp.hoon`** - Protocol adapter
	- Converts tool definitions to MCP JSON format
	- Handles JSON-RPC routing (`initialize`, `tools/list`, `tools/call`)
	- Delegates actual execution to `lib/tools.hoon`
2. **`lib/routes/mcp.hoon`** - HTTP endpoint
	- Parses incoming JSON
	- Calls `handle-request:mcp`
	- Returns JSON response

The key insight: `lib/mcp.hoon` knows nothing about *what* tools exist.It just translates between MCP protocol and the generic tool interfacein `lib/tools.hoon`. Add a tool there, and MCP picks it upautomatically.

### Tools

**`lib/tools.hoon`** - Tool definitions

- Protocol-agnostic tool registry
- Each tool: name, description, params, handler
- *Why it matters:* single source of truth for what LLMs can do

### Data Types

**`sur/claude.hoon`** - Chat structures

- Message, chat (versioned), tool request/result
- Branching strategy documented in comments
- *Why it matters:* the shape of persistent data

### Feature Libraries

**`lib/claude.hoon`** - Claude API client

**`lib/alarms.hoon`** - Scheduled execution

**`lib/open-loops.hoon`** - Task management

### Adding New Tools (for developers)

To add a new tool, you only need to edit `lib/tools.hoon`. No routing orMCP changes required.

**Step 1: Add to `all-tools` list**

```hoon
:*  'my_tool_name'
    'Description of what the tool does'
    %-  ~(gas by *(map @t parameter-def))
    :~  :-  'param1'
        ^-  parameter-def
        [%string 'Description of param1']
        :-  'param2'
        ^-  parameter-def
        [%number 'Description of param2']
    ==
    ~['param1']  ::  required parameters
    tool-my-tool-name
==
```

**Step 2: Write the handler arm**

The handler signature is:

```hoon
++  tool-my-tool-name
  ^-  tool-handler
  |=  arguments=(map @t json)
  =/  m  (fiber:io ,tool-result)
  ^-  form:m
  ::  ... implementation ...
  (pure:m [%text 'result'])  ::  or [%error 'message']
```

**Minimal example: `tool-get-ship`**

```hoon
++  tool-get-ship
  ^-  tool-handler
  |=  arguments=(map @t json)
  =/  m  (fiber:io ,tool-result)
  ^-  form:m
  ;<  =bowl:gall  bind:m  get-bowl:io
  (pure:m [%text (scot %p our.bowl)])
```

---

### sailbox

`sailbox` is an agent wrapper library that enables async/await-styleprogramming in Hoon. The name reflects its heritage: it began as asandbox for developers to quickly learn Sail (Hoon's HTML templating).It was then adapted as a means of teaching Claude Sail, and soonincorporated ideas from "Grubbery" - an Urbit-thread-inspiredasynchronous-process-based application model - to allow for rapiditeration on Sail-based reactive web applications, eventually becominga general-purpose async agent wrapper. The name is likely to changein the future to more accurately reflect its current function.

The fundamental premise of `sailbox` - and Grubbery before it - is that"actions" want to be associated with some agent-like locus of controland yet also often want to be defined as segregated and interleavedasynchronous processes. Threads are Urbit-native asynchronousprocesses, but they are not associated with a locus of control and donot manage any persistent state directly.

#### The Problem sailbox Solves

A standard Gall agent handles events one at a time. When you poke anagent, it can emit cards (effects) and update its state, but it cannotwait for a response before continuing. If you need to make an HTTPrequest and then do something with the result, you must split yourlogic across multiple event handlers - `++on-poke`, `++on-arvo`,`++on-agent`, `++on-watch`, `++on-leave` - manually tracking what youwere doing when each response arrives.

This becomes unwieldy quickly. A simple workflow like "fetch JSON froman API, parse it, update state, send a notification" might span threeor four event handlers with intermediate state to track progress.

#### The Fiber Pattern

`sailbox` introduces "fibers" - lightweight processes that can wait forinput and continue where they left off. A fiber is essentially astrand (from Urbit threads) adapted to manipulate agent statedirectly. It is a computation that may need to wait for external input(an HTTP response, a timer, a poke-ack) before continuing.

The key is a continuation monad that lets you write what looks likesequential code:

```
fetch data from API
parse response
update state
send notification
```

Each step that requires waiting returns a continuation. When theawaited input arrives, the fiber continues exactly where it left off,with all local bindings intact.

#### What You Implement

To write a `sailbox` agent, you implement a handful of arms:

- **`++process`**: The main fiber that handles incoming pokes. This iswhere your agent's logic lives, written in the fiber style.
- **`++initial`**: The starting state for a fresh agent.
- **`++migrate`**: Transform old state to new state on agent upgrade.
- **`++make-sse-event`** and **`++first-sse-event`**: Generate SSEevents for connected clients.
- **`++on-peek`**: Handle scry requests.

The `++agent` function in `sailbox` wraps your implementation into astandard Gall agent, handling all the event routing and fiberscheduling internally.

#### The I/O Vocabulary

`sailboxio` provides the operations available inside a fiber:

**State access**: Read and replace the agent's state (a `tarball`).

**Agent communication**: Poke other agents, subscribe to paths, handleresponses.

**Arvo operations**: Set timers, read from Clay, make HTTP requests.

**HTTP responses**: Send simple payloads, emit SSE events.

**Tarball operations**: Create directories, add files, delete entries.

When a fiber needs to wait for input, it returns a continuation - thenext function to call when input arrives. The `sailbox` wrapper agentstores this continuation and invokes it when new input comes in.

#### Process Scheduling

Multiple fibers can be active simultaneously. `sailbox` maintains a"pipe" of running processes, each identified by a unique ID. When onefiber is waiting, another can make progress.

A mutex ("boar") prevents race conditions when fibers need exclusiveaccess to shared state. A fiber can claim the mutex while performinga critical section, blocking other fibers from running until itreleases.

#### HTTP and SSE

`sailbox` handles HTTP requests by spawning a fiber for each request.The fiber runs until it produces a response or fails. SSE connectionsare tracked separately, with a keep-alive timer and automatic cleanup.

`sailbox` extends the standard gall card type with two additions:`%simple-payload` for responding to HTTP requests and `%sse` foremitting events to connected SSE clients. `%simple-payload` is thefundamental mechanism by which fibers respond to web requests - itpowers the Claude chat interface, the MCP API, the file browser, andall other HTTP endpoints. `%sse` enables real-time streaming updatesfor chat responses, progress indicators, and live state changes.

---

### tarball

`tarball` is a filesystem-as-state abstraction. Instead of definingrigid structures for agent state, `tarball` represents state as atree of directories and files - exactly like a conventional filesystem.

Here, too, the name reflects its origins: it was originally just a wayto upload files and directories over the web and download directoriesas tarballs. That functionality is still there - the file browser at `/master/ball` lets you do exactly this. The library evolved as Ibegan experimenting with making the entire state of an agent resemblea traditional Unix directory structure. Like `sailbox`, the name islikely to change in the future to more accurately reflect its currentfunction.

#### The Core Idea

Agent state is an `(axal lump)` - a recursive tree structure whereeach node can contain files and subdirectories. Each file is a `cage` (a mark and a vase), wrapped with metadata like modificationtime. This means state can hold any typed Hoon data, organizedhierarchically.

#### Why Filesystem Semantics?

**Legibility**: State is visible as paths and files. You can browse `/chats/abc123/messages` rather than inspecting opaque nounstructures.

**Portability**: Export state as a tarball, back it up, move it toanother ship, or restore from a backup. The file browser at `/master/ball` makes this tangible.

**Graceful migration**: Adding new features often means adding newpaths. Existing paths remain valid. Individual data types can bemigrated at the mark level - type migration happens per-mark ratherthan as a monolithic state migration. No need for complex versionnumbers and migration functions.

**Mark integration**: Files are cages, so the mark system handlesserialization. A `.json` file is a `%json` cage; an image is `%mime`.The conversion machinery already exists.

#### The ++ba Interface

`tarball` provides a door (`++ba`) for manipulating the state:

**Basic operations**: `get`, `put`, `del`, `has` - read, write,delete, and check existence of files at paths.

**Directory operations**: `mkd` (make directory), `lop` (deletesubtree), `dip` (descend into subdirectory).

**Listing**: `lis` (list files in directory), `lss` (listsubdirectories).

**Bulk operations**: `tap` (flatten to list), `gas` (insert list),`run` (apply function to all files).

**Typed access**: `got-cage`, `got-file`, `got-cage-as` - retrievefiles with expected types, crash if wrong.

#### Symlinks

`tarball` supports symlinks (`road` type) - either absolute paths orrelative paths (with parent-directory traversal). This is primarilyabout completeness with respect to Unix-native tarballs: if you wantto import and export real tarballs, you need to handle symlinks.

#### Validation

When you `put` a cage, `tarball` validates it using the mark system.If the mark has a `dais`, the value is normalized. This catchesmalformed data at write time rather than read time.

#### Integration with sailbox

`sailboxio` provides fiber-aware wrappers for `tarball` operations:`put-cage`, `put-file`, `mkd`, `del`, `lop`. These access thecurrent state via `get-state` and update it via `replace`.

The combination means: your agent's state is a filesystem, youragent's logic is written as sequential async code, and the twoconnect through a consistent interface.

---

This concludes our summary of the fundamentals - not everything wascovered in detail, but enough to orient further exploration. We areencouraged by the progress so far and believe there is more latent inthese ideas than we have yet extracted. Personal AI on Urbit - AI thatserves you, runs on your machine, and answers to no one else - remainsa compelling vision, and this work is our attempt to move toward it.

`clurd` is stable and ready for use. `urbit-master` remainsexperimental and under active development, but functional for daily useand experimentation at the documented commit. Both repos are availablefor direct use and further independent development.

- clurd: [github.com/niblyx-malnus/clurd](https://github.com/niblyx-malnus/clurd)
- urbit-master: [github.com/gwbtc/urbit-master](https://github.com/gwbtc/urbit-master)

Questions, feedback, and contributions are welcome.