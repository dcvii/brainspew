---
title: "Massive compromise hits LiteLLM and the whole AI developers community: how did it happen?"
source: "https://cybernews.com/security/critical-litellm-supply-chain-attack-sends-shockwaves/"
author:
published:
created: 2026-03-25
description:
tags:
  - "brain_spew"
---
***LiteLLM, a massively popular Python library used by AI developers, was compromised to deliver a mass credential harvesting malware, sending shockwaves across the industry. The “software horror” spread like an infection to other projects through dependencies. A clearer picture has emerged of how the unprecedented hack unfolded.***

Developers are sounding the alarm bells. If you installed LiteLLM 1.82.7 or 1.82.8, immediately rotate everything: all secrets, every environment variable, SSH key, cloud credential, and API keys present on the system, security researchers warn. You might not even know that you use these packages – they often come as dependencies with major AI projects.

AI developers across the world report that their machines suddenly started behaving strangely.

Callum McMahon, a [research scientist at FutureSeach](https://futuresearch.ai/blog/no-prompt-injection-required/), was the first to disclose the issue on GitHub.

![litellm](https://media.cybernews.com/images/1500w/2026/03/litellm.png)

“It started with my machine stuttering hard, something that really shouldn’t be happening on a 48GB Mac. Htop (CLI process viewer) taking 10s of seconds to load, CPU pegged at 100%, all signs I’ll be working on my local env for a while…. After failing to software reset my Mac, I took a final picture for evidence and hard reset,” said McMahon.

“I was just setting up a new project, and things behaved weirdly. My laptop ran out of RAM, it looked like a forkbomb was running. I've investigated and found that a base64 encoded blob has been added to proxy\_server.py,” said another developer, [who was first to report the attack on Hacker News](https://news.ycombinator.com/item?id=47501426).

“We have been pwned by this,” complains a developer on GitHub.

“This is very, very bad, thousands of people are likely getting pwned right now.”

Don't miss our latest stories on Google News. Add us as your Preferred Source on Google

The LiteLLM library is massively popular, with 97 million monthly downloads on PyPI. Developers use it as a unified interface to connect their apps to over 100 AI services from OpenAI, Anthropic, and others.

It’s like a universal adapter allowing you to control LLMs, AI agents, and MCP tools from one place.

This means attackers obtained highly valuable API keys and credentials that could cause significant losses. Moreover, it opens the door to many other repositories that depend on LiteLLM, allowing attackers to snowball the attack even further.

## How was LiteLLM breached?

It appears that the publisher behind LiteLLM was completely compromised, which is a result of a previous supply chain attack upstream.

LiteLLM’s build pipeline included Trivy security scanner, which wasn’t locked to a specific version. Hackers first poisoned the popular security tool, and this opened the door to a much bigger plunder.

![PyPI malware](https://media.cybernews.com/2023/05/pypi-pythin-malware.png)

Image by Cybernews.

Security scanner Trivy, owned by Aqua Security, was initially compromised during [an automated attack by an AI bot](https://cybernews.com/security/claude-powered-ai-bot-compromises-five-github-repositories/) scanning for misconfigured CI/CD workflows (automated scripts developers use to test, build, and publish software).

The repository had a vulnerable workflow, enabling hackers to steal a personal access token belonging to the service account, used in at least 33 other workflows in the Aqua Security GitHub organization.

The attackers used the stolen token to hijack the Trivy repository, wipe its releases, and publish a malicious extension on OpenVSX that attempted to abuse local AI coding agents. After Aqua Security disclosed and mitigated the incident, a second attack happened on March 19th, 2026.

Endor Labs suspects that “Aqua remediated the surface-level damage but left residual access.”

“The attacker returned with a more complex payload: a multi-stage credential stealer,” the Snyk researchers explain.

The attackers injected malware into the “trivy-action” – an automation script developers use to run the Trivy scanning engine to check their code for known security vulnerabilities.

On March 24th, LiteLLM’s automation ran Trivy as part of the build process and exfiltrated the PYPI publishing token to the attackers.

“With that credential, the attackers published litellm 1.82.7 at 10:39 UTC and 1.82.8 at 10:52 UTC, each containing malicious payloads,” the researchers explained.

![python-burning-a-massive-bag-of-money.jpg](https://media.cybernews.com/2025/10/python-burning-a-massive-bag-of-money.jpg)

## The attack wreaking havoc

The LiteLLM team was [quickly made aware](https://github.com/BerriAI/litellm/issues/24512) of the attack and blocked all downloads of quarantined packages. The GitHub issue opened by McMahon was flooded with bots, a deliberate tactic by the attacker to obscure the incident's severity and mislead readers into believing the problem had been handled.

The team scrambled to change all maintainer accounts, delete all keys for GitHub, Docker, CircleCI, PyPI, and others. At the same time, bots flooded the GitHub.

The malicious packages were available on PyPI for roughly three hours, and the damage was done.

Major AI frameworks, including Microsoft GraphRAG, Google ADK, DSPy, OpenHands, and CrewAI, all pulled the malicious LiteLLM version as an indirect dependency.

The affected projects include widely used machine learning frameworks DSPy and MLflow, popular AI agent frameworks CrewAI and OpenHands, and others.

![Two developers expressing uncertainty.](https://media.cybernews.com/2025/06/uncertain-developers.jpg)

Two developers expressing uncertainty.

It means that anyone installing a tool that depends on LiteLLM could also have been infected with the credential stealer in the background, even if they had no idea the library was involved.

Following the incident, many other popular repositories filed security patches pinning LiteLLM to the safe version.

“LiteLLM is a transitive dependency in a large number of AI frameworks and tools. Because most projects pin litellm>= with no upper bound, users of these projects may have pulled 1.82.7 or 1.82.8 without ever directly depending on litellm,” [StepSecurity explains in its research.](https://www.stepsecurity.io/blog/litellm-credential-stealer-hidden-in-pypi-wheel#stage-1-mass-credential-harvester)

The researchers recommend checking for the installed LiteLLM version and treating the system as compromised if 1.82.7 or 1.82.8 are detected.

“The attacker picked the one package whose entire job is holding every AI credential in the organization in one place. OpenAI keys, Anthropic keys, Google keys, Amazon keys… all routed through one proxy. All compromised at once,” Aakash Gupta, product growth writer and newsletter creator, posted on X.

## The implications are far-reaching

Andrej Karpathy, a prominent AI scientist, labeled the attack as software horror.

“Supply chain attacks like this are basically the scariest thing imaginable in modern software. Every time you install any dependency, you could be pulling in a poisoned package anywhere deep inside its entire dependency tree,” the expert said.

Karpathy warns that modern reliance on dependencies must be re-evaluated, because a single compromised package can bring down everything built on it, like a single bad brick collapsing the whole pyramid.

Karpathy would rather ask LLM to “yoink” part of the code with the required functionality rather than use the dependency.

“Simple ‘pip install litellm’ was enough to exfiltrate SSH keys, AWS/GCP/Azure creds, Kubernetes configs, git credentials, env vars (all your API keys), shell history, crypto wallets, SSL private keys, CI/CD secrets, database passwords,” Karpathy posted on X.

## The malware is capable of exfiltrating nearly everything

Many security experts noted that the malware was likely AI-generated – it contained a bug known as a fork bomb, causing the affected systems to crash.

“If the attacker didn't vibe code this attack, it could have been undetected for many days or weeks,” Karpathy noted.

That doesn’t reduce its impact on the affected systems. The malware contains a harvester that systematically reads and exfiltrates every credential it can reach. StepSecurity listed its targets:

- **SSH keys** (private keys and host authentication files)
- **Git credentials** (usernames, passwords, and repository access tokens)
- **AWS** (access keys, IAM role credentials, live calls to Secrets Manager and SSM Parameter Store)
- **Kubernetes** (cluster configs, admin credentials, service account tokens and secrets across all namespaces)
- **Google Cloud Platform** (application default credentials, service account keys)
- **Azure** (full credentials directory)
- **Docker** (registry authentication configs)
- **Environment files**
- **Package manager tokens** (npm, Vault, database passwords, including PostgreSQL, MySQL, MongoDB)
- **Shell history**
- **TLS/PKI** private keys and certificate files
- **CI/CD configs** (Terraform state, GitLab, Travis, Jenkins, and Ansible files)
- **Crypto wallets** Bitcoin, Litecoin, Dogecoin, Ethereum keystore, Solana keypairs, Cardano files
- **System files** (user account database and authentication logs)

The exfiltration was extremely thorough, and the malware didn't just grab credentials sitting on disk. It used obtained credentials to make live API calls to AWS and Kubernetes to pull any secrets from there as well.

All this was just the first stage.

In the second stage, the malware also dropped a persistent command-and-control backdoor that requires no root privileges and persists after reboots.

In the third stage, the malware uses a stolen Kubernetes service account token to spread itself to every server in the cluster, dropping a backdoor on each one.

“Even if you deleted the infected container, the backdoor was already running on the underlying machines beneath it. Cleaning up the container alone was not enough,” StepSecurity warned.

The malware was supposed to complete the job silently. However, due to an unintended bug, the process kept multiplying, causing “severe CPU exhaustion.”

According to malware researchers vx-underground, the threat actor managed to exfiltrate 300GB of data from over 500,000 infected systems in a short period of time.

## Who’s behind the attack?

The massive attack is attributed to a financially motivated threat group dubbed TeamPCP. The group first appeared in late 2025, conducting worm-driven campaigns targeting exposed Docker APIs, Kubernetes clusters, and CI/CD pipelines, [according to the Wiz Threat Center](https://threats.wiz.io/all-actors/teampcp).

Even before LiteLLM, the threat actor executed “the most consequential CI/CD supply chain attack documented to date,” [Phoenix Security said.](https://phoenix.security/teampcp-supply-chain-attack-trivy-checkmarx-github-actions-npm-canisterworm/)

They’re responsible for a month-long supply chain campaign that spans multiple ecosystems, including GitHub, npm, OpenVSX, PyPI, and Docker Hub.

TeamPCP compromised two major open-source security vendors (Aqua Security and Checkmarx), four GitHub Actions repositories, two OpenVSX extensions, container registries, and used a self-propagating worm dubbed CanisterWork, controlled over blockchain, to compromise at least 66 npm packages.

The hackers monetize harvested credentials by deploying ransomware, mining cryptocurrency, and engaging in extortion.

“This campaign is almost certainly not over. TeamPCP has demonstrated a consistent pattern: each compromised environment yields credentials that unlock the next target,” [Endor Labs said in its research.](https://www.endorlabs.com/learn/teampcp-isnt-done)

“The LiteLLM compromise is the latest escalation in a month-long campaign that began with a single incomplete incident response.”

The security firm expects more infected package registries and self-propagating malware in new ecosystems.

---

***Unlock more exclusive Cybernews content on YouTube.***