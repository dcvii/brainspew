---
title: "Things I'm Actually Doing With AI #01"
source: https://tessellations.substack.com/p/things-im-actually-doing-with-ai
author:
  - "[[Michael David Cobb Bowen]]"
published: 2025-06-13
created: 2025-11-24
description: Baldrick, my homelab dogsbody.
tags:
  - clippings
  - southwall
---
Southwall is my homelab. It’s the name of my collection of compute, network and storage machines. I used to call it The Terabyte back when having a terabyte was a big deal. I have about 30x that now, and I know folks with 200TB. Anyway, I am backing off the AWS cloud for certain things because now I can host it at home. AIs are helping me do so.

So, as usual, I’m trying to do eleventeen things at the same time. One of these things is building a **next-gen analytic data platform** based around Iceberg, Postgres, DuckDB, Temporal and OpenMetadata among many other bits and pieces. Those would be bits and pieces like Github Actions, Ansible, NetBox, Prometheus and other stuff I’m forgetting. I’m piecing it all together like a Mexican Brick House. Whenever I have time to spare, I add something and/or subtract something else. At the core of this periodic construction, deconstruction and reconstruction is Warp, Zed, brew, OpenAI and Claude.

**Warp** is the command line interface built on Rust that gives me zsh on my 2024 M4 Mac Mini Pro. When I conceptualize a small piece of a project, hit Command-I and it readily accepts prompts to execute on whichever server and directory I’m located. I can call any of the following LLMs to execute my plan {Claude 4 Sonnet, 3.7 Sonnet, 3.5 Sonnet, 3.5 Haiku, Gpt-4o, GPT-4.1, o4-mini, o3, o3-mini, gemini 2.0 flash, gemini 2.5 pro}. Mostly it stays on 4 Sonnet. But I can also put it on ‘auto’ and let it choose the executor for my plan.

But first I have an **extensive dialog with GPT 4o** in that standalone app to look at alternatives, pick the technologies according to tradeoffs presented and then ask GPT to **generate a prompt for Claude**. I spent a considerable amount of time doing this before settling on **Temporal** as opposed to Airflow, Airbyte and Prefect, primarily because expect to be putting a lot of complex conditional logic and long running pipelines and I’ll want to use Python first and Golang later.

So for all of my scaffolding I’m adding a **prompt subdirectory** to keep track of these plans before they get instantiated as well as the test results that show success. So I am now my own tape ape, whereas I was very lazy in this regard before. I’m saving a bunch of money by not paying for cloud SAAS and watching over Claude’s shoulder as it reconfigures existing configurations. I’m actually learning more *with* AI because it makes me more ambitious than I would be on my own.

Just yesterday I updated one of my Ubuntu servers from 22 to 24 and then upgraded my Postgres server from 14 to 17.5. These were executed without a hitch. Since I expected to use this practice from now on especially as regards using multiple LLMs with multiple tools for upkeep, I have given this agentic entity a name, that would be Baldrick whose job it is to execute cunning plans.

![The Lean Startup - I Have a Cunning Plan + FREE CHEAT SHEET - YouTube](https://substackcdn.com/image/fetch/$s_!51TN!,w_424,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc7057191-a3e9-4f3a-a564-263186b18bdd_1280x720.jpeg)

Here is the first of them that I have recorded.

```
You are an expert DevOps assistant. I want you to configure my Mac workstation as the control node for managing my homelab called Southwall, which consists of:
- 4 Ubuntu bare-metal servers
- 2 macOS (Apple Silicon) servers

## Objectives:
1. Install and configure the following tools:
   - [ ] Ansible (for provisioning and config management)
   - [ ] NetBox CLI tools or API client (to manage inventory)
   - [ ] Prometheus-compatible tooling (node_exporter for Linux, alternatives for macOS)
   - [ ] Python + uv for scripting utilities
   - [ ] Optional: tool to pull \`lshw\`, \`dmidecode\`, \`lsblk\` from Linux machines and relevant hardware info from macOS

## Assumptions:
- My Mac runs macOS (Apple Silicon or Intel)
- I use Homebrew as my package manager
- I use Warp terminal and have Claude available as an assistant
- I have sudo access and basic Git/Python installed
- Target machines are reachable via SSH

## Tasks:
1. Use Homebrew to install Ansible, Python 3.12+, and \`uv\`
2. Create a directory structure under \`~/southwall_control\` like:

   ~/southwall_control/
   ├── ansible/
   │   ├── inventory/
   │   └── playbooks/
   ├── netbox/
   │   └── scripts/
   ├── metrics/
   │   ├── prometheus.yml
   │   └── exporters/
   ├── scripts/
   │   └── collect_hw_info.py
   └── ssh/
       └── deploy_keys/

3. For each Southwall server:
   - Check if any of my existing public SSH keys (from \`~/.ssh/*.pub\`) are authorized in \`~/.ssh/authorized_keys\`
   - If not, prompt me to confirm which key to use and replicate it to that server
   - If no key should be reused, generate a new SSH keypair and install it
   - Store metadata on key usage per server in \`ssh/key_registry.yaml\`

4. Initialize a Python environment (using \`uv\`) with \`requests\` and \`pyyaml\`
5. Set up NetBox API access for automation (token-based)
6. Create a cross-platform \`collect_hw_info.py\` script that:
   - Uses \`lshw\`, \`lsblk\`, and \`dmidecode\` on Ubuntu
   - Uses \`system_profiler\`, \`sysctl\`, and \`diskutil\` on macOS
   - Saves YAML snapshots to \`~/southwall_control/inventory_snapshots/\`

Please output one terminal command at a time and confirm after each successful step. Ask me to validate any server-specific info like IPs or credentials before proceeding.
```

Thanks for reading Tessellations! Subscribe for free to receive new posts and support my work.