---
title: "ArvanCloud_2026-01-08_IranInternetShutdown/README.md at main · narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown"
source: "https://github.com/narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown/blob/main/README.md"
author:
  - "[[narimangharib]]"
published:
created: 2026-01-14
description:
tags:
  - "clippings"
---
[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown/tree/main?resume=1)

[Iran Internet Shutdown - ArvanCloud Infrastructure Analysis](https://github.com/narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown/commit/7a5a790b2c509e8c03daba2e4019151fbf323140)

[7a5a790](https://github.com/narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown/commit/7a5a790b2c509e8c03daba2e4019151fbf323140) ·

On January 8, 2026, Iran cut internet access for 90 million citizens. Government websites remained on operational infrastructure while everything else went dark. This research documents how.

---

## The Evidence

Every Iranian government website that remains on operational infrastructure during the shutdown runs on **ArvanCloud** - a company sanctioned by the US Treasury for "facilitating the Iranian regime's censorship of the Internet."

| Site | IP | Server Header |
| --- | --- | --- |
| president.ir | 185.143.234.235 | `server: ArvanCloud` |
| dolat.ir | 185.143.232.201 | `server: ArvanCloud` |
| mfa.ir | 185.143.232.201 | `server: ArvanCloud` |
| majlis.ir | 185.143.233.235 | `server: ArvanCloud` |
| irna.ir | 185.143.234.235 | `server: ArvanCloud` |
| isna.ir | 185.143.234.21 | `server: ArvanCloud` |

All IPs trace back to **AS205585** - ArvanCloud's Iranian CDN network (`185.143.232.0/22`).

---

**104 domains tested. Results:**

| Status | Count | What it means |
| --- | --- | --- |
| On ArvanCloud | 28 | Government sites, state news - infrastructure operational, DNS resolving |
| On TIC/DCC | 3 | Government-approved messengers (Eitaa, Bale) |
| Other CDNs | 27 | Some commercial services on domestic infrastructure |
| Not resolving | 46 | Banking, independent news, many services - no DNS response |

The pattern: **government infrastructure stays operational, everything else goes dark.**

---

ArvanCloud uses a JavaScript challenge on all hosted sites:

```
Cookie: __arcsjsc = arcookie-[timestamp]-[hash]
```

- Timezone detection identifies Iranian users
- XOR-obfuscated tokens (key: 0x6)
- Real-time timestamps in cookies
- Identical code across all government domains

The filtering happens at the network level. ArvanCloud's BGP routes stay announced while international traffic gets blocked.

---

## Network Infrastructure

```
INTERNATIONAL INTERNET
         ❌ BLOCKED (BGP routes withdrawn)
         │
   ┌─────┴─────┐
   │    NIN    │  National Information Network
   │           │
   │ ArvanCloud│──→ Government sites, state media
   │ TIC/DCC   │──→ Approved messengers
   │           │
   └───────────┘
         │
    Citizens stuck here - no global access
```

**ArvanCloud ASNs:**

- AS202468 - 35,584 IPs, 6,435+ domains
- AS205585 - Government site hosting (185.143.232.0/22)
- AS208006 - UAE entity for international routing

---

## Reports

| Document | Description |
| --- | --- |
| [Main Evidence](https://github.com/narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown/blob/main/IRAN_SHUTDOWN_EVIDENCE_2026-01-08.md) | Full domain scan, IP mappings, infrastructure breakdown |
| [Filtering Analysis](https://github.com/narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown/blob/main/ARVANCLOUD_FILTERING_ANALYSIS.md) | JavaScript reverse engineering, cookie mechanism, XOR cipher |
| [BGP Analysis](https://github.com/narimangharib/ArvanCloud_2026-01-08_IranInternetShutdown/blob/main/BGP_ROUTING_ANALYSIS.md) | Network routing, ASN relationships, shutdown implementation |

---

```
# Check DNS
dig president.ir +short
# 185.143.234.235

# Check server
curl -sI https://president.ir | grep server
# server: ArvanCloud

# Check ownership
whois 185.143.234.235 | grep netname
# netname: ANYCAST_185-143-234-0_24
# descr: AbrArvan BGP Anycast
```

---

ArvanCloud isn't just hosting websites. It's the infrastructure backbone that keeps government services operational while citizens lose all connectivity.

The US Treasury sanctioned them for exactly this. The evidence is in the DNS records, the HTTP headers, and the network routing.

---

*Data collected January 8, 2026 via direct DNS/HTTP verification*