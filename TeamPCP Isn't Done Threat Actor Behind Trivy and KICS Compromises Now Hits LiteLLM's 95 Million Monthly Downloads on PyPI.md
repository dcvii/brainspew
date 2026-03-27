---
title: "TeamPCP Isn't Done: Threat Actor Behind Trivy and KICS Compromises Now Hits LiteLLM's 95 Million Monthly Downloads on PyPI"
source: "https://www.endorlabs.com/learn/teampcp-isnt-done"
author:
  - "[[By Endor Labs]]"
published:
created: 2026-03-25
description:
tags:
  - "brain_spew"
---
On March 24, 2026, Endor Labs identified that `litellm` versions 1.82.7 and 1.82.8 on PyPI contain malicious code not present in the upstream GitHub repository. `litellm` is a widely used open source library with over 95 million month downloads. It lets developers route requests across LLM providers through a single API.

Both compromised versions include a backdoored file that decodes and executes a hidden payload the moment the file is imported. Version 1.82.8 goes further: it installs a `.pth` file that runs the payload on *any* Python invocation, even if litellm is never imported. Version 1.82.6 is the last known-clean release.

Once triggered, the payload runs a three-stage attack: it harvests credentials (SSH keys, cloud tokens, Kubernetes secrets, crypto wallets, and.env files), attempts lateral movement across Kubernetes clusters by deploying privileged pods to every node, and installs a persistent systemd backdoor that polls for additional binaries. Exfiltrated data is encrypted and sent to an attacker-controlled domain.

The infrastructure and tradecraft match TeamPCP, the actor behind a month-long supply chain campaign that has now crossed five ecosystems: GitHub Actions, Docker Hub, npm ([CanisterWorm](https://www.endorlabs.com/learn/canisterworm)), OpenVSX, and PyPI. The pattern is deliberate. TeamPCP has recently targed security-adjacent tools, including Aqua Security's Trivy, a vulnerability scanner, and Checkmarx's KICS, an IaC analyzer, and now an LLM proxy. These tools run in environments that are likely to contain valuable credentials and other secrets, so compromising them gives the attacker broad access.

## Affected Packages

| Package Name | Version(s) | Publication Date | Injection Vectors | Status |
| --- | --- | --- | --- | --- |
| `litellm` | `1.82.7` | 2026-03-24 | `proxy_server.py` (import-time) | Removed from PyPI |
| `litellm` | `1.82.8` | 2026-03-24 | `proxy_server.py` (import-time) + `litellm_init.pth` (interpreter startup) | Removed from PyPI |

**Last known-clean version:** litellm@1.82.6 (published 2026-03-22, verified clean by Endor Labs).

## Technical Analysis

### Infection Chain

The malicious code resides in a single file within the litellm wheel distributed on PyPI: litellm/proxy/proxy\_server.py. The attacker inserted 12 lines at line 128, between two unrelated legitimate code blocks (the REALTIME\_REQUEST\_SCOPE\_TEMPLATE dictionary and the showwarning function). The GitHub source at the corresponding commit does not contain these lines — the injection was performed during or after the wheel build process.

The injected code executes at module import time, meaning any process that imports litellm.proxy.proxy\_server triggers the payload without any additional user interaction:

![Image](https://cdn.prod.website-files.com/6574c9e538a34feac8cec013/69c295e6b9f0a826e70a56f3_2d8fc2f4.png)

Figure 1: The 12-line injection in proxy\_server.py (lines 128–139). The malicious code sits between the legitimate REALTIME\_REQUEST\_SCOPE\_TEMPLATE dictionary (line 122) and the showwarning function (line 141). Line 130 contains the active base64 payload (34,460 characters); lines 131–132 contain commented-out earlier iterations.

The technique of writing a decoded script to a temporary file and executing it via subprocess.run(\[sys.executable, p\]) avoids direct use of exec() or eval(), which are commonly flagged by static analysis tools. The same file legitimately uses subprocess.Popen to launch ollama serve (line 2036), so the presence of subprocess calls does not stand out during code review.

**Version 1.82.8 adds a second, more aggressive vector.** A file named litellm\_init.pth (34,628 bytes) is included at the wheel root. Python.pth files placed in site-packages are processed automatically by site.py at interpreter startup. The file contains a single line that imports subprocess and launches a detached Python process to decode and execute the same base64 payload:

![Image](https://cdn.prod.website-files.com/6574c9e538a34feac8cec013/69c295e6b9f0a826e70a56f6_852472fc.png)

Figure 2: The \`litellm\_init.pth\` file from \`litellm@1.82.8\` (reformatted for readability — the original is a single 34,628-byte line). A single \`subprocess.Popen\` call silently launches a detached Python process that decodes and executes the same base64 payload found in \`proxy\_server.py\`. The \`DEVNULL\` redirects suppress all output.

This decodes and executes the same payload as the proxy\_server.py injection, but with two critical differences:

1. It fires on **every Python invocation** in the environment, not just when litellm is imported
2. It uses subprocess.Popen (non-blocking) instead of subprocess.run (blocking), so the payload runs silently in the background without delaying Python startup. The use of exec(base64.b64decode(...)) here — despite the attacker having removed exec() from the main proxy\_server.py payload — reflects a.pth file constraint:.pth files must execute code in a single line, making exec() unavoidable

This makes 1.82.8 significantly more dangerous: any Python script, test runner, or tool invoked in an environment where litellm is installed will silently trigger the credential harvester in the background.

### Malicious Behavior

The base64 payload decodes to an orchestrator script (Stage 1) that contains two embedded components: a credential harvester (Stage 2, encoded as B64\_SCRIPT) and a persistence dropper (Stage 3, encoded as PERSIST\_B64).

**Stage 1 — Orchestrator.** The orchestrator runs the credential harvester by piping the decoded B64\_SCRIPT into a Python subprocess via stdin. The harvester's stdout output (all collected credentials) is written to a temporary file. The orchestrator then encrypts this file using a randomly generated AES-256-CBC session key, encrypts the session key with a hardcoded RSA-4096 public key using OAEP padding, bundles both into a tarball named tpcp.tar.gz, and POSTs it to https\[://\]models\[.\]litellm\[.\]cloud/ with an X-Filename: tpcp.tar.gz header. Only the holder of the corresponding RSA private key can decrypt the exfiltrated data.

**Stage 2 — Credential Harvester.** The harvester (332 lines of Python) performs a systematic sweep of the compromised system. It collects:

- **System information**: hostname, username, kernel version, IP addresses, routing tables, all environment variables
- **SSH keys**: id\_rsa, id\_ed25519, id\_ecdsa, id\_dsa, authorized\_keys, known\_hosts, and SSH configs for all users under /home/\*/ and /root/
- **Cloud credentials**: AWS (~/.aws/credentials, IMDS role credentials via 169.254.169.254, Secrets Manager contents, SSM parameters), GCP (application\_default\_credentials.json, gcloud configs), Azure (~/.azure/ directory tree)
- **Kubernetes secrets**: service account tokens, kubeconfig files, and a full dump of all secrets across all namespaces via the K8s API
- **Environment files**:.env,.env.local,.env.production,.env.development,.env.staging — searched recursively up to 6 directories deep across /home, /root, /opt, /srv, /var/www, /app, /data, /var/lib, and /tmp
- **Database credentials**:.pgpass, my.cnf, redis.conf,.mongorc.js, and relevant environment variables
- **Cryptocurrency wallets**: Bitcoin (wallet.dat), Ethereum keystores, Solana validator keypairs, Cardano signing/verification keys, and configs for Litecoin, Dogecoin, Zcash, Dash, Ripple, and Monero
- **TLS/SSL private keys**: all.pem,.key,.p12,.pfx files, LetsEncrypt certificates
- **CI/CD secrets**: terraform.tfvars, terraform.tfstate,.gitlab-ci.yml, Jenkinsfile, WireGuard configs
- **Shell histories**: bash, zsh, MySQL, PostgreSQL, Redis CLI histories
- **System files**: /etc/passwd, /etc/shadow, authentication logs

The harvester also implements a full AWS SigV4 signing routine to authenticate API calls to Secrets Manager and SSM Parameter Store using credentials obtained from the EC2 Instance Metadata Service (IMDS).

**Kubernetes lateral movement.** If a Kubernetes service account token exists at /var/run/secrets/kubernetes.io/serviceaccount/token, the harvester enumerates all nodes in the cluster and deploys a privileged pod to each one. Each pod runs in kube-system, uses alpine:latest, requests privileged: true with hostPID and hostNetwork access, and mounts the entire host root filesystem at /host. The pod tolerates all taints (ensuring it can schedule on every node, including control-plane nodes) and uses restartPolicy: Never to avoid leaving long-running evidence.

![Image](https://cdn.prod.website-files.com/6574c9e538a34feac8cec013/69c295e6b9f0a826e70a56fc_2225f0e7.png)

Figure 3: Decoded content - the privileged pod manifest from the Stage 2 credential harvester. The pod specification requests full host access - \`hostPID\`, \`hostNetwork\`, privileged security context, and a volume mount of the entire host filesystem (\`/\`) at \`/host\`. Pods are named \`node-setup-{node\_name}\` and deployed to the \`kube-system\` namespace.

Each pod chroots into the host filesystem and installs the Stage 3 persistence dropper as a systemd user service on every node.

### Persistence

**Stage 3 — Persistent Backdoor.** The persistence dropper is installed at ~/.config/sysmon/sysmon.py with a corresponding systemd unit at ~/.config/systemd/user/sysmon.service (service name: "System Telemetry Service"). After a 5-minute initial delay (time.sleep(300)), it enters a loop that polls https://checkmarx.zone/raw every 50 minutes (time.sleep(3000)). Each cycle fetches a URL from the C2, compares it against a local state file (/tmp/.pg\_state) to avoid re-downloading, and checks for a kill switch ("youtube.com" not in l). If the URL is new and the kill switch is not engaged, the dropper downloads the binary to /tmp/pglog, makes it executable, and runs it in a detached session.

![Image](https://cdn.prod.website-files.com/6574c9e538a34feac8cec013/69c295e6b9f0a826e70a56f9_e459c2de.png)

Figure 4: Decoded content - the Stage 3 persistence dropper (44 lines). The C2 URL (\`checkmarx.zone/raw\`), binary target (\`/tmp/pglog\`), state file (\`/tmp/.pg\_state\`), 5-minute initial delay, 50-minute poll interval, and youtube.com kill switch are all visible. This script is installed as a systemd user service and survives reboots.

The binary path /tmp/pglog is deliberately chosen to masquerade as a PostgreSQL process in process listings.

### Payload Development History

Two additional base64 blobs on lines 131 and 132 of proxy\_server.py are commented-out earlier iterations of the payload, left in the published package as an OPSEC failure. Decoding all three reveals the attacker's development progression:

**Iteration 1** (line 132, 38,568 base64 chars → 28,924 bytes): The earliest version. Uses StringIO + exec() for execution and writes output to a named file (collected\_vars.txt). The inner harvester obfuscates shell commands with a custom RC4 cipher. Despite these differences, the core targets are already present: the same checkmarx.zone/raw C2, sysmon.service persistence, RSA-4096 key, and credential harvesting scope.

**Iteration 2** (line 131, 69,316 base64 chars → 51,985 bytes): A transitional version. The outer orchestrator is unchanged, but the inner harvester now carries both the old RC4 version (commented out) and a new plaintext version — byte-for-byte identical to the final active harvester. This is the largest blob because it contains both inner scripts.

**Iteration 3** (line 130, active, 34,460 base64 chars → 25,844 bytes): The production version. The outer orchestrator was rewritten to use subprocess piping and tempfile.TemporaryDirectory. The RC4 layer and exec() calls are gone. All C2 infrastructure, persistence, encryption, and credential targets are identical across all three iterations — only the delivery and evasion mechanisms changed.

### C2 and Obfuscation

The malware uses two C2 domains:

- **models.litellm.cloud** — receives the encrypted credential archive (tpcp.tar.gz) via HTTPS POST. The domain impersonates the legitimate litellm project.
- **checkmarx.zone** — serves binary payload URLs for the persistence dropper. This is the same C2 domain used in TeamPCP's Checkmarx KICS GitHub Action compromise and OpenVSX extension attacks.

Obfuscation is layered: the injection in proxy\_server.py contains only standard library imports and a base64 string — no suspicious function calls are visible at the surface level. The actual malicious logic is triple-nested (base64 in proxy\_server.py -> base64 B64\_SCRIPT in the orchestrator -> base64 PERSIST\_B64 in the harvester). All credential data is encrypted with a hybrid RSA+AES scheme before exfiltration, preventing inspection of the exfiltrated content in network traffic. The attacker rebuilt the wheel with a regenerated RECORD file — we confirmed the RECORD entry for proxy\_server.py contains the SHA-256 of the backdoored file (sha256=oNIpvo78svkTXirVW6J1t23c\_rVfpDcOClIqW97gEgs), not the original. Standard integrity checks against the wheel's own metadata pass, making source-to-artifact comparison the only reliable detection method.

### Attribution: TeamPCP

Endor Labs attributes this attack to **TeamPCP** with high confidence based on multiple matching indicators with the campaign [documented by Wiz](https://www.wiz.io/blog/teampcp-attack-kics-github-action) on March 23, 2026:

| Indicator | KICS/Trivy/OpenVSX (Wiz) | litellm (Endor Labs) |
| --- | --- | --- |
| C2 domain | `checkmarx.zone` | `checkmarx.zone/raw` |
| Persistence script | `~/.config/sysmon/sysmon.py` | `~/.config/sysmon/sysmon.py` |
| Systemd unit | `~/.config/systemd/user/sysmon.service` | `~/.config/systemd/user/sysmon.service` |
| Service display name | "System Telemetry Service" | "System Telemetry Service" |
| C2 poll interval | Every 50 minutes | `time.sleep(3000)` = 50 minutes |
| Kill switch | Response contains "youtube" | `"youtube.com" not in l` |
| Exfil archive name | `tpcp.tar.gz` | `tpcp.tar.gz` |
| K8s persistence | Kubernetes-focused persistence code | Privileged pods to all nodes |
| Encryption | RSA + AES with openssl | AES-256-CBC + RSA-4096 OAEP via openssl |

The tpcp.tar.gz filename directly references the group's name (TeamPCP → tpcp). PyPI metadata shows litellm@1.82.7 was uploaded at **2026-03-24 10:39:24 UTC** and 1.82.8 at **10:52:19 UTC** — approximately 22 hours after the KICS compromise (March 23, 12:58 UTC). The 13-minute gap between the two malicious releases, combined with the addition of the.pth injection vector in 1.82.8, indicates the attacker was actively iterating during the attack window.

### Campaign Timeline: How TeamPCP Built Access

The litellm compromise is the latest operation in a campaign spanning nearly a month and five supply chain ecosystems. Each attack yielded credentials that unlocked the next target.

| Date | Target | Attack Vector | Impact |
| --- | --- | --- | --- |
| **Feb 28** | Aqua Trivy | [`hackerbot-claw`](https://www.stepsecurity.io/blog/hackerbot-claw-github-actions-exploitation) exploited a [`pull_request_target` Pwn Request vulnerability](https://www.stepsecurity.io/blog/github-actions-pwn-request-vulnerability) in Trivy's `API Diff Check` workflow, stealing a PAT with write access from the runner. | Full repo takeover — privatized, releases v0.27.0–v0.69.1 deleted, suspicious VSCode extension artifact pushed to OpenVSX. Aqua [remediated](https://github.com/aquasecurity/trivy/discussions/10265) but **containment was incomplete**. |
| **Mar 19** | Aqua Trivy (second compromise) | TeamPCP [exploited residual access](https://www.wiz.io/blog/trivy-compromised-teampcp-supply-chain-attack) from incomplete Feb 28 containment. Imposter commits (spoofing maintainers `DmitriyLewen`, `rauchg`) + tag hijacking of `v0.69.4` → triggered release pipeline. Also compromised `aqua-bot` service account. | Backdoored binaries to GitHub Releases, Docker Hub, GHCR, ECR. 75/76 `trivy-action` + 7 `setup-trivy` tags force-pushed. Credential stealer scraped `Runner.Worker` process memory from downstream CI/CD pipelines. C2: `scan.aquasecurtiy.org`. |
| **Mar 20** | npm (45+ packages) | Stolen npm tokens from compromised CI/CD runners → [self-propagating worm](https://www.aikido.dev/blog/teampcp-deploys-worm-npm-trivy-compromise) (`deploy.js`) autonomously enumerated and published malicious patch versions across all packages each token could access. | 28 `@EmilGroup` packages, 16 `@opengov`, others — all within 60 seconds. `postinstall` hook dropped `pgmon.service` persistence with ICP Canister C2 (decentralized, censorship-resistant). |
| **Mar 22** | Docker Hub | Continued access to Aqua's stolen Docker Hub credentials. | Malicious `trivy:0.69.5` and `0.69.6` images published. Internal Aqua repos made public on GitHub. |
| **Mar 23** | Checkmarx OpenVSX + KICS | Compromised `ast-phoenix` (OpenVSX) and `cx-plugins-releases` (GitHub) service accounts — exact compromise vector [not publicly disclosed](https://checkmarx.com/blog/checkmarx-security-update/). Imposter commits + tag hijacking for KICS (same technique as Trivy). | Two IDE extensions backdoored (`ast-results@2.53.0`, `cx-dev-assist@1.7.0`), all 35 KICS GitHub Action tags hijacked, `ast-github-action@2.3.28` also compromised. New C2: `checkmarx.zone`. First appearance of K8s persistence code. |
| **Mar 24** | **litellm PyPI** (this report) | Compromised PyPI publishing credentials — exact vector not confirmed. | Backdoored `litellm` 1.82.7 and 1.82.8 published to PyPI. Full credential harvester + K8s lateral movement + persistent backdoor. C2: `models.litellm.cloud` + `checkmarx.zone/raw`. |

### Looking Ahead

This campaign is almost certainly not over. TeamPCP has demonstrated a consistent pattern: each compromised environment yields credentials that unlock the next target. Based on the campaign's trajectory, we assess the following as likely next steps:

**More package registries.** TeamPCP has already hit GitHub Actions, OpenVSX, npm, and PyPI within five days. Docker Hub was directly compromised via stolen Aqua credentials. RubyGems, crates.io, and Maven Central remain obvious targets — any CI/CD pipeline running a compromised Trivy or KICS action during the March 19–23 window would have exposed publishing tokens for whichever registries those pipelines deploy to.

**Self-propagating worms in new ecosystems.** The npm CanisterWorm demonstrated that TeamPCP has automated credential-to-compromise tooling: given a stolen token, the worm autonomously enumerates, versions, and publishes malicious packages across an entire scope in under a minute. A PyPI equivalent — using stolen PyPI tokens to push malicious patch releases to every package an account maintains — is a natural adaptation and requires only minor retooling.

**Decentralized C2 adoption.** The Trivy and npm attacks used an ICP Canister (Internet Computer Protocol) as a dead-drop C2 — a decentralized, censorship-resistant hosting layer with no single takedown point. The KICS and litellm attacks used checkmarx.zone, a traditional domain that can be seized. If defenders take down checkmarx.zone, TeamPCP has already proven they can fall back to infrastructure that is substantially harder to disrupt.

**Broader credential harvesting from production environments.** The pivot from CI/CD (GitHub Actions runners) to production (PyPI packages running in Kubernetes clusters) is a deliberate escalation. CI/CD secrets are valuable but ephemeral — they rotate, they expire, they're scoped to build-time. Production secrets (AWS IAM credentials, database passwords, Kubernetes service account tokens) are longer-lived, higher-privilege, and provide direct access to customer data and infrastructure. The litellm payload's focus on AWS Secrets Manager, SSM Parameters, and full Kubernetes lateral movement signals that TeamPCP is optimizing for production-grade access.

**The security-tool paradox will deepen.** TeamPCP has exclusively targeted security-adjacent software: a vulnerability scanner (Trivy), an IaC analyzer (KICS), and an LLM proxy that handles API keys and secrets (litellm). These tools run with elevated privileges by design — they need broad access to scan, analyze, or proxy. Compromising them is maximally efficient: the attacker inherits the trust the organization has already granted to the tool. We expect continued targeting of security, observability, and infrastructure tooling — the categories of software most likely to have access to credentials and cloud APIs.

## Mitigation

### Short-term: Detection and Response

Check whether litellm@1.82.7 or litellm@1.82.8 is installed in any environment:

`pip show litellm 2>/dev/null | grep -i version`

`pip freeze 2>/dev` **`/null | grep litellm`**

For 1.82.8 specifically, also check for the.pth file in site-packages:

`find "$(python3 -c 'import site; print(site.getsitepackages()[0])')" -name "litellm_init.pth" 2>/dev/null`

Search for persistence artifacts on affected hosts:

`ls -la ~/.config/sysmon/sysmon.py 2>/dev/null`

`ls -la ~/.config/systemd/user/sysmon.service 2>/dev/null`

`ls -la /tmp/pglog /tmp/.pg_state 2>/dev/null`

`systemctl --user status sysmon.service 2>/dev/null`

In Kubernetes clusters where litellm was deployed, check for attacker pods:

`kubectl get pods -n kube-system | grep node-setup`

Review network logs for connections to models.litellm.cloud and checkmarx.zone. If any of these indicators are present, treat the environment as fully compromised and rotate all credentials that were accessible on the host — including LLM provider API keys, AWS/GCP/Azure credentials, SSH keys, database passwords, Kubernetes secrets,.env values, npm tokens, and Vault tokens.

To remove the persistence mechanism:

`systemctl --user stop sysmon.service`

`systemctl --user disable sysmon.service`

`rm -f ~/.config/sysmon/sysmon.py`

`rm -f ~/.config/systemd/user/sysmon.service`

`rm -f /tmp/pglog /tmp/.pg_state`

`systemctl --user daemon-reload`

Since TeamPCP also compromised Checkmarx KICS and Aqua Trivy GitHub Actions, organizations should audit CI/CD pipelines for usage of these tools during their respective compromise windows.

### Long-term: Prevention Best Practices

Pin dependencies to exact versions and verify package integrity against the upstream source repository — not just the registry's own RECORD hashes, which the attacker regenerated. For packages with public GitHub repositories, compare the distributed artifact against the tagged source commit. Enable [PyPI Trusted Publishers](https://docs.pypi.org/trusted-publishers/) (OIDC-based publishing) to eliminate long-lived API tokens from CI pipelines. Monitor for unexpected dependency changes using lock files and automated diff reviews.

## Indicators of Compromise (IoCs)

| IoC                                                                | Type                                      | Status            |
| ------------------------------------------------------------------ | ----------------------------------------- | ----------------- |
| `litellm==1.82.7`                                                  | PyPI Package                              | Removed from PyPI |
| `litellm==1.82.8`                                                  | PyPI Package                              | Removed from PyPI |
| `8395c3268d5c5dbae1c7c6d4bb3c318c752ba4608cfcd90eb97ffb94a910eac2` | SHA-256 (1.82.7 wheel)                    | Active IoC        |
| `d2a0d5f564628773b6af7b9c11f6b86531a875bd2d186d7081ab62748a800ebb` | SHA-256 (1.82.8 wheel)                    | Active IoC        |
| `a0d229be8efcb2f9135e2ad55ba275b76ddcfeb55fa4370e0a522a5bdee0120b` | SHA-256 (compromised `proxy_server.py`)   | Active IoC        |
| `71e35aef03099cd1f2d6446734273025a163597de93912df321ef118bf135238` | SHA-256 (`litellm_init.pth`, 1.82.8 only) | Active IoC        |
| `models.litellm.cloud`                                             | C2 Domain (exfiltration)                  | Active            |
| `checkmarx.zone`                                                   | C2 Domain (persistence)                   | Active            |
| `checkmarx.zone/raw`                                               | C2 Endpoint (payload delivery)            | Active            |
| `~/.config/sysmon/sysmon.py`                                       | Filesystem (persistence script)           | Active IoC        |
| `~/.config/systemd/user/sysmon.service`                            | Filesystem (systemd unit)                 | Active IoC        |
| `/tmp/pglog`                                                       | Filesystem (downloaded binary)            | Active IoC        |
| `/tmp/.pg_state`                                                   | Filesystem (state tracking)               | Active IoC        |
| `node-setup-*` pods in `kube-system`                               | Kubernetes (attacker pods)                | Active IoC        |
| `tpcp.tar.gz`                                                      | Exfiltration archive name                 | Active IoC        |
| `X-Filename: tpcp.tar.gz`                                          | HTTP header (exfiltration POST)           | Active IoC        |
| `litellm_init.pth`                                                 | Filesystem (.pth payload, 1.82.8 only)    | Active IoC        |

## Conclusion

The litellm compromise is the latest escalation in a month-long campaign that began with a single incomplete incident response. On February 28, an autonomous bot exploited a workflow vulnerability in Trivy and stole a PAT. Aqua remediated the surface-level damage but left residual access. Three weeks later, TeamPCP leveraged that opening — and in five days crossed five supply chain ecosystems: GitHub Actions, Docker Hub, npm, OpenVSX, and now PyPI.

The choice of targets is deliberate. TeamPCP has exclusively compromised security-adjacent software — a vulnerability scanner (Trivy), an IaC analyzer (KICS), and an LLM proxy (litellm) — tools that run with elevated privileges by design. Compromising them is maximally efficient: the attacker inherits the broad access the organization already granted to the tool.