---
title: Ubiquiti network restart guide
source: https://chatgpt.com/share/694571c3-d7ec-8004-b025-ccdbc14aa1fa
author:
  - "[[BrainSpew/DIDs]]"
published:
created: 2025-12-19
description: ChatGPT is your AI chatbot for everyday use. Chat with the most advanced AI to explore ideas, solve problems, and learn faster.
tags:
  - clippings
---
Uploaded a file

I am trying to restart my network. I'm having problems with the Ubiquiti Site Manager. It doesn't recognize my hardware communicating on the new ISP

---

Got it — this is a *very* common pain point when changing ISPs on a UniFi/Ubiquiti network. Let’s walk through this methodically and avoid factory-resetting anything unless we have to.

I’ll assume you’re using **UniFi Site Manager / UniFi OS** with some combination of **Cloud Gateway / Dream Machine / USG / CloudKey**, switches, and APs.

---

## The core issue (most likely)

When you change ISPs, **one or more of these usually breaks**:

1. **WAN interface expectations**
	- Old ISP = DHCP
	- New ISP = PPPoE / VLAN / static IP / different MTU
2. **Controller reachability**
	- Devices *are online* but cannot “phone home” to the controller
3. **Layer-2 vs Layer-3 mismatch**
	- The gateway got an IP, but internal devices are on the wrong subnet
4. **Site Manager visibility**
	- Hardware is running, but adopted to a *different* site or controller instance

---

## First: establish ground truth (don’t trust Site Manager yet)

### 1️⃣ Can you reach the gateway locally?

From a machine plugged into the LAN:

- Try:
	or

If **local access works but Site Manager doesn’t show devices**, this is a *controller registration* issue, not a hardware failure.

👉 Tell me:

- Can you log into the gateway locally?
- What model is it? (UDM, UDM Pro, Cloud Gateway Ultra, USG, etc.)

---

## Second: verify WAN is actually up

Log into the gateway locally and check:

### WAN status

Look for:

- IP address assigned?
- Gateway?
- DNS?
- Link speed?

If WAN shows **Connected but no internet**, the usual culprits are:

| New ISP Requirement | Symptom |
| --- | --- |
| VLAN tagging (e.g. VLAN 35, 201) | WAN gets link but no traffic |
| PPPoE | WAN shows disconnected |
| Static IP | WAN connected, no routing |
| MTU mismatch | Some sites work, others fail |

👉 Tell me:

- Who is the new ISP?
- Did they give you **PPPoE creds**, **VLAN ID**, or a **static IP sheet**?

---

## Third: Site Manager specifically not seeing hardware

If WAN is up **but Site Manager doesn’t recognize devices**:

### Common causes

#### A. Devices are adopted to a different site

Especially common if you:

- Reset only *some* devices
- Had multiple UniFi accounts
- Migrated from CloudKey → UniFi OS

Check:

- **Settings → System → Advanced**
- Look at **Controller Hostname / Inform URL**

#### B. Inform URL broken

Devices must reach:

If DNS is wrong after ISP change, adoption breaks.

**Quick fix (from gateway SSH):**

If DNS fails → fix DNS on WAN.

---

## Fourth: do NOT factory reset yet — try this first

### Restart order (important)

1. **Power down modem / ONT**
2. Power down **UniFi Gateway**
3. Wait 2 minutes
4. Power up modem / ONT
5. Wait until ISP link is stable
6. Power up UniFi Gateway
7. Wait 5–10 minutes
8. Power up switches
9. Power up APs

This forces correct WAN negotiation and device re-informing.

---

## Fifth: when Site Manager still shows nothing

At this point, one of these is true:

- Gateway cannot reach UniFi cloud
- Gateway is logged into a different UniFi account
- Devices are adopted but invisible due to site mismatch

### Quick diagnostic questions (please answer these):

1. **Gateway model**
2. **New ISP + connection type**
3. Can you access the gateway locally?
4. Does WAN show an IP?
5. Are switches/APs showing “Connected” locally but not in Site Manager?

---

## If you want: safe recovery path (no full reset)

If needed, I can walk you through:

- SSH into gateway
- Manually re-set inform URL
- Force re-adoption without nuking configs
- Verify VLAN/PPPoE config for your ISP
- Determine whether this is a UniFi OS bug vs ISP issue

Just reply with:

- Gateway model
- ISP name
- What you see on WAN status

We’ll get Southwall back online without burning it down 🔧

---

I haven't rebooted my USG but I did rebook the Cloud Key. Should I do the former?

---

Short answer: **yes — but do it in the right order.**  
What you did (rebooting the Cloud Key but not the USG) is *very likely* why Site Manager looks confused.

Let me explain *why*, then give you a **safe, low-risk reboot sequence**.

---

## Why this happens (UniFi-specific gotcha)

In a UniFi stack:

- **USG = router + WAN state + NAT**
- **Cloud Key = controller (brains, but not traffic)**

When:

- ISP changes **WAN characteristics**, and
- Cloud Key reboots **before** the USG re-establishes WAN,

you can get into a state where:

- USG has stale WAN routing/DNS
- Cloud Key comes up and can’t reach:
- Devices *think* they’re adopted, but can’t report status
- Site Manager shows “nothing” or “offline”

This is especially common with **USG (older firmware)**.

---

## What you should do now (safe procedure)

### ✅ Yes — reboot the USG

But do it **after** stabilizing the WAN.

### Correct reboot order (important)

1️⃣ **Power off modem / ONT**

- Wait **60–120 seconds**

2️⃣ **Power off USG**

- Leave it off

3️⃣ **Wait 2 minutes**

- This clears old ARP, DHCP, PPPoE sessions

4️⃣ **Power on modem / ONT**

- Wait until ISP link is fully up
	- All “online” / “service” lights solid

5️⃣ **Power on USG**

- Wait **5 minutes**
- Do *not* touch Cloud Key yet

6️⃣ **Verify WAN on USG**  
If possible, check:

- WAN has IP
- DNS resolves
- Internet reachable

7️⃣ **Only now reboot Cloud Key**

- This allows it to come up with a clean, routable WAN

---

## What not to do (yet)

❌ Do **not** factory reset the USG  
❌ Do **not** “forget” devices  
❌ Do **not** re-adopt anything yet

Those are last-resort steps.

---

## What success looks like

After this sequence:

- USG shows **Connected** WAN
- Cloud Key can reach UniFi cloud
- Switches/APs reappear in Site Manager
- Adoption state stabilizes on its own

It can take **5–10 minutes** after Cloud Key reboot for Site Manager to populate.

---

## If it still doesn’t work after this

Then we’re likely dealing with one of these:

- ISP requires **VLAN tagging or PPPoE**
- DNS on WAN is broken
- Cloud Key is signed into a **different UniFi account**
- Inform URL mismatch

At that point I’ll have you check:

- USG WAN config
- Cloud Key → Settings → System → Advanced
- Possibly a single SSH command (non-destructive)

---

## Bottom line

👉 **Yes, reboot the USG — but only after cycling the modem and before rebooting the Cloud Key again.**

When you’re done, tell me:

- Did the USG get a WAN IP?
- Do you see *anything* reappear in Site Manager?

We’ll take the next step based on that.

---

Aha. Rebooting USG.

---

Perfect — that’s exactly the right “aha” moment 👍  
Now **hands off for a few minutes** and let it do its thing.

Here’s what to watch for while the USG is rebooting:

---

## What should happen next (timeline)

### ⏱️ 0–2 minutes

- USG boots
- WAN link negotiates with the new ISP
- DHCP / PPPoE / VLAN handshake happens

### ⏱️ 2–5 minutes

- USG establishes routing + DNS
- Internal LAN stabilizes
- Switches/APs regain upstream reachability

### ⏱️ 5–10 minutes

- Cloud Key successfully “phones home”
- Devices start reappearing in **Site Manager**
- Status may briefly flip between *Adopting / Provisioning / Connected* — this is normal

---

## What to check (only if you can)

If you have a browser handy on the LAN:

- Try loading **any external site** (even a basic one)
- If that works, the WAN is almost certainly correct

If you can reach the Cloud Key locally:

- Log in and confirm the **USG shows WAN Connected**

---

## Important: don’t intervene yet

For the next **10 minutes**:

❌ Don’t reboot again  
❌ Don’t forget/re-adopt devices  
❌ Don’t change WAN settings

UniFi is slow but *eventually consistent*.

---

## If something still looks off after 10 minutes

Just tell me **one sentence**:

- “Internet works / doesn’t work”
- “Site Manager shows devices / still empty”

Based on that, I’ll know immediately whether:

- we’re done ✅
- DNS needs fixing
- WAN VLAN/PPPoE is missing
- or the Cloud Key needs one final clean reboot

You’re on the right path — this was the correct move.

---

My WAN connects just fine if I go pure Wifi. I am connected to an extender which may not be looking directly at my ATT router - so there's probably confusion between the two, because when I plug int the ethernet cable, stuff gets confused. It's not the old network but something is screwy.

---

That description is *very* telling — and you’re thinking about it in exactly the right way. This is **not a UniFi mystery**, it’s a **Layer-2 / topology ambiguity** caused by the extender + AT&T gateway + UniFi all trying to be “the router.”

Let me reframe what’s happening, then give you a clean way out.

---

## What’s actually going wrong (plain English)

You currently have **two different network worlds** that work *independently* but break when bridged:

### World A — “Pure Wi-Fi” (works)

- Your device connects via:
- AT&T router is doing:
	- DHCP
	- NAT
	- DNS
- Internet works fine

### World B — “Ethernet into UniFi” (breaks)

- Path becomes something like:
- Now **two routers see each other**
- DHCP responses collide
- Default gateway ambiguity
- ARP confusion
- UniFi controller loses upstream consistency

This is classic **double-router + extender bridge confusion**.

---

## The extender is the silent troublemaker

Most Wi-Fi extenders do one of these (often poorly documented):

1. **NAT + DHCP** (acts like a mini router)
2. **Bridge mode** (Layer-2 pass-through)
3. **Pseudo-bridge** (still rewrites MACs / ARP)

When you:

- Use Wi-Fi → you stay inside the extender’s “world”
- Plug Ethernet → you jump networks mid-stream

UniFi *hates* this.

---

## The key question (don’t skip this)

👉 **Where is your USG connected relative to the AT&T router?**

One of these is true:

### ❌ Bad (very common)

### ❌ Also bad

### ✅ Correct (what you want)

---

## Why Ethernet “confuses everything”

When you plug in Ethernet:

- Your device gets:
	- an IP from **UniFi DHCP**
- But traffic may return via:
	- **AT&T Wi-Fi path**
- Replies don’t match the MAC/IP pair
- Sessions reset
- Controller thinks devices are flapping

Wi-Fi works because it never touches UniFi.

---

## Immediate stabilizing steps (no resets)

### Step 1: Pick ONE router (for now)

For diagnosis, do this:

**Option A (temporary, fastest):**

- Unplug **USG WAN**
- Let AT&T router do everything
- UniFi becomes “dumb switches/APs”

If things stabilize → topology confirmed.

**Option B (preferred long-term):**

- Keep **USG as the only router**
- AT&T router in **IP Passthrough / Bridge mode**
- Extender disabled or put in true bridge mode

---

## AT&T-specific landmine (important)

AT&T gateways (BGW210, BGW320, etc.):

- **Do not do true bridge**
- They use **IP Passthrough**
- Only ONE downstream MAC can get the public IP

If your extender grabs that IP first:

- USG gets a private IP
- Everything breaks intermittently

👉 This matches your symptoms *exactly*.

---

## What I’d recommend you do next (in order)

1️⃣ Disconnect the **Wi-Fi extender completely**  
2️⃣ Hard-wire:

3️⃣ Verify:

- USG WAN gets a **public IP**
- Internet works over Ethernet

4️⃣ Only then:

- Either remove the extender permanently
- Or re-add it **behind UniFi**, not AT&T

---

## One clarifying question (very important)

**What model is your AT&T router?**  
(BGW210? BGW320?)

Once I know that, I can tell you:

- Exact IP Passthrough settings
- Whether the extender can be salvaged
- Or if it *must* be retired

You’re not crazy — this is textbook “extender + ISP gateway + real router” chaos. We can clean it up cleanly.

---

Here's the problem. My ATT Gateway is in the garage and cannot be hardwired to anything. Internet (AT&T Fiber) ↓ BGW620-700 (Gateway - Garage) ↓ WFEXT 4991-41 (WiFi Extender - Rack 2 Shelf 1) -> USG

---

Got it. This diagram clarifies everything — and you’ve correctly identified the *hard constraint* that drives the whole design:

> **The AT&T gateway cannot be hard-wired to the rack.**

That means you are **forced to use Wi-Fi as a WAN backhaul**, which is exactly where UniFi + AT&T extenders get… prickly.

Let me be very clear and precise here.

---

## What you have now (and why it’s unstable)

This creates **three fundamental problems**:

---

### 1️⃣ Double NAT + competing DHCP domains

- BGW620 is a router
- WFEXT is *not* a clean bridge (it rewrites MACs)
- USG is also a router

Your USG WAN is **not seeing a real Layer-2 bridge** — it’s seeing a *pseudo-client network*.

Result:

- WAN IP on USG is unstable
- Gateway ARP tables flap
- Controller loses upstream intermittently

---

### 2️⃣ AT&T extenders are not Ethernet-clean

The WFEXT 4991-41:

- Is designed to extend Wi-Fi to *end devices*
- Not to provide a transparent Ethernet WAN uplink
- Often:
	- Changes MAC addresses
	- Filters DHCP options
	- Breaks long-lived TCP sessions

UniFi assumes **clean Ethernet semantics**. This extender does not provide that.

---

### 3️⃣ UniFi + Wi-Fi WAN is a second-class citizen

USG:

- Technically supports Wi-Fi WAN **only via USB or dedicated client radios**
- Does **not** tolerate pseudo-bridged Ethernet over Wi-Fi well
- Especially when the upstream is AT&T hardware

---

## Why “pure Wi-Fi works” but Ethernet doesn’t

When you go pure Wi-Fi:

- You’re a normal AT&T client
- Everything behaves

When you plug into UniFi:

- You’re traversing:
- Return paths mismatch
- NAT tables desync
- DNS resolution flips

This is expected, not a misconfiguration.

---

## Hard truth (important)

> **There is no fully stable configuration where a USG sits behind an AT&T Wi-Fi extender and acts as a router.**

Anyone telling you otherwise is hand-waving.

---

## Your realistic options (ranked)

### 🟢 Option 1 — Make UniFi Layer-2 only (most stable)

- Disable DHCP on USG
- Or remove USG entirely
- Let AT&T handle routing
- UniFi handles:
	- Switching
	- Wi-Fi
	- VLANs (limited)

**Pros**

- Rock solid
- No flapping
- No adoption issues

**Cons**

- No UniFi gateway features
- Limited VLAN support

---

### 🟡 Option 2 — Replace extender with true wireless bridge (recommended)

Replace WFEXT with:

- Ubiquiti airMAX
- Ubiquiti UniFi Building Bridge
- TP-Link CPE
- MikroTik wireless bridge

Now the USG sees **real Ethernet**, not client Wi-Fi.

**Pros**

- Full UniFi routing
- Stable
- Clean L2

**Cons**

- $100–$200
- Extra hardware

---

### 🔴 Option 3 — Use AT&T IP Passthrough (won’t really help)

Because:

- Passthrough only works for **direct Ethernet**
- Your extender grabs the public IP first
- USG never gets it

This will remain flaky.

---

### 🟢 Option 4 — Put the USG in the garage (if possible)

Even temporarily:

This flips the topology correctly.

---

## What I would do in your situation

Given:

- Fiber in garage
- Rack elsewhere
- You want stability *now*

👉 **Disable routing on the USG and run UniFi as L2 only**  
Then plan a **wireless bridge upgrade** later.

This aligns with your engineering instincts: *eliminate ambiguity before optimizing*.

---

## Immediate next steps (no new hardware)

1. Power down USG
2. Connect rack via extender
3. Let BGW620 do DHCP
4. Bring UniFi back as switches/APs only
5. Confirm stability

If you want, I can:

- Walk you through disabling USG routing cleanly
- Recommend a specific wireless bridge for your distance
- Draw a final “clean” topology for Southwall

Just say which path you want to take.

---

I have taken Option 1. Everything seems to work, but my Cloud Key has gone dark. I probably wont spend money for the bridge any time soon. Why did you pick the four you did. Give me some comparisons between them.

---

Great — Option 1 working *mostly* makes sense as a stop-gap. Now let’s unpack **why your Cloud Key went dark** and then go into the **comparisons between the four options** I listed so you understand the trade-offs.

---

## ❓ Why your Cloud Key “went dark”

Under Option 1 you’ve essentially:

With the USG **no longer acting as a router**, two things likely happened to your Cloud Key:

### 🟡 1. It lost its “inform” source

Cloud Key expects to manage **adopted** UniFi devices behind a UniFi gateway (USG), but now:

- There is no *controller → device management path* in the traditional UniFi sense
- Devices aren’t being “adopted” by the controller
- They’re simply acting as **dumb switches/APs**

So the Cloud Key thinks there are *no devices to manage.* That’s why it looks dark.

### 🔵 2. Its local IP may have changed

Under the USG you had a clean LAN (e.g., 192.168.1.x).  
Under the AT&T extender, DHCP from the BGW620 might assign different ranges or reserved addresses.

If the Cloud Key got a new IP and your browser assumed the old one, you may simply be hitting a dead endpoint.

#### Quick check for Cloud Key

- Connect a laptop to the same UniFi switch/AP layer
- Find the Cloud Key’s IP (via DHCP table on **BGW620**)
- Browse to that IP directly

If it’s reachable but shows no devices — that’s entirely expected given Option 1.

---

## 📊 Why I picked those four options — explained

Here’s a comparison of the four approaches, with **pros and cons** and the *kinds of problems they solve.*

---

## 🟢 Option 1 — Let AT&T do routing; UniFi as L2 only

**Pros**

- Cheapest (no new gear)
- Simplest topology
- Works reliably as long as all logic is in AT&T router

**Cons**

- No UniFi gateway features (firewall, VLAN routing, DPI, VPN)
- Cloud Key may see no devices (because it’s not controlling them)
- Layer-2 may still be flaky through the extender

**Best for**

- Users who just want “it works” without UniFi routing

---

## 🟡 Option 2 — Wireless bridge instead of extender

**Pros**

- Clean Ethernet backhaul
- USG can be full router
- UniFi controller sees everything

**Cons**

- Requires hardware purchase
- Slightly more complex setup

**Best for**

- People who want *full* UniFi functionality but can’t run cable

---

## 🔴 Option 3 — AT&T IP Passthrough

(Only works with *direct Ethernet.*)

**Pros**

- Allows USG to get public WAN IP
- Great when wired

**Cons**

- Useless if you're wireless backhauling
- Extender will take upstream MAC, breaking passthrough
- Still leaves the Wi-Fi bridge problem

**Best for**

- Wired backhaul scenarios

---

## 🟡 Option 4 — Place USG near BGW620

**Pros**

- Strongest topology
- USG is the only router
- Cloud Key + UniFi functions fully operational

**Cons**

- Requires moving gear
- Might need POE injector or creative power

**Best for**

- People committed to UniFi ecosystem
- Homeowners who can rewire or relocate devices

---

## 🧠 Comparison Summary

| Option | Cost | UniFi Routing | Stability Behind AT&T Extender | Controller Visibility | Best Use |
| --- | --- | --- | --- | --- | --- |
| **1\. L2 Only** | 💲 | ❌ | ⚠️ | ⚠️ | Quick & cheap |
| **2\. Wireless Bridge** | 💲💲 | ✔️ | ✔️ | ✔️ | Full feature w/out cable |
| **3\. IP Passthrough** | 💲 | ✔️ | ❌ | ✔️ | Only wired backhaul |
| **4\. Move USG** | 💲 | ✔️ | ✔️ | ✔️ | Strongest long term |

---

## 📌 Why Option 1 kills the Cloud Key status view

Under Option 1:

- USG isn’t routing → no adoption topology
- UniFi devices are acting as dumb switches/APs
- Controller has *nothing to adopt*

So the Cloud Key looks “dark” — but the network *can be working fine*. The Cloud Key still exists and can serve configurations, but there’s nothing for it to *control*.

To bring it back into play, you’d need:

- A wireless bridge or wired backhaul (like Option 2/4)
- OR keep the Cloud Key running, but host devices in a way it can *see/adopt*

---

## 🧩 If you want to keep the Cloud Key meaningful

The only two viable ways *without laying cable* are:

### 🔹 A true wireless bridge

(Not a Wi-Fi extender)

Examples:

- Ubiquiti airMAX / LiteBeam
- NanoStation / UniFi Building Bridge
- TP-Link Pharos

This removes the middleman and gives your USG a *clean WAN*.

---

## I can help you with:

✔ Identifying wireless bridge models that fit your distance  
✔ Step-by-step configuration (BGW passthrough where possible)  
✔ How to preserve the Cloud Key visibility even if you stay on Option 1

---

If you tell me:

### 📍 How far is the rack from the garage?

- (Feet, walls, floors)

### 📍 Are there line-of-sight windows/glass between them?

I’ll tailor exactly the *wireless bridge* options that will work reliably.

Just give me that and I’ll size the solution — no guesswork.

---

I meant the four wireless bridges.

---

Got it — thanks for the correction 👍  
You’re asking **why *those four wireless bridge families*** (airMAX, UniFi Building Bridge, TP-Link CPE, MikroTik) and how they compare, **not** the topology options.

This is a good question, because these are *not interchangeable Wi-Fi extenders*; they sit in a very different design space.

Below is a **practical, engineering-oriented comparison**, not marketing fluff.

---

## Why these four specifically

I picked these because they are:

1. **True Layer-2 Ethernet bridges** (not “client Wi-Fi”)
2. **Designed for backhaul**, not end-devices
3. **Proven to work behind ISP gateways** like AT&T
4. **Affordable and available**
5. **Operationally predictable** (no MAC rewriting, no NAT)

Most consumer “mesh” or “extender” products fail at least one of those.

---

## The Four Wireless Bridge Families — Compared

## 1️⃣ Ubiquiti airMAX / LiteBeam / NanoBeam

*(5 GHz PtP / PtMP backhaul)*

### What it is

- Ubiquiti’s **ISP-grade wireless Ethernet**
- Designed for **kilometers**, not rooms

### Strengths

- Rock-solid Layer-2 bridging
- Extremely stable
- Cheap for what you get
- Independent of UniFi OS quirks
- Excellent noise handling

### Weaknesses

- Separate management UI (not UniFi)
- More “network engineer” than “home user”
- Outdoor units (can be overkill indoors)

### Typical throughput

- 300–450 Mbps real-world

### Cost

- **$60–$100 per side**

### Best when

- You want **maximum stability**
- You don’t care about single-pane-of-glass management
- You’re OK with “set it once and forget it”

---

## 2️⃣ UniFi Building Bridge (UBB / UBB-XG)

*(60 GHz millimeter-wave bridge)*

### What it is

- UniFi’s **cleanest, most elegant** wireless bridge
- Appears as a “virtual cable” in UniFi

### Strengths

- Managed entirely inside UniFi
- Zero MAC/NAT weirdness
- Near-wired latency
- Automatic pairing
- Very clean topology

### Weaknesses

- **Expensive**
- Requires near line-of-sight
- 60 GHz hates walls, foliage, rain

### Typical throughput

- 1+ Gbps (when conditions are right)

### Cost

- **$450–$500 per pair**

### Best when

- You want **“as if it were wired”**
- You value elegance and manageability
- Budget is not a concern

---

## 3️⃣ TP-Link CPE / Pharos (CPE210 / CPE510 / CPE710)

### What it is

- Budget-friendly outdoor PtP bridge
- Often used by WISPs and SMBs

### Strengths

- Cheap
- Simple web UI
- Stable Layer-2
- Decent performance for the price

### Weaknesses

- Firmware less polished
- Management UX is basic
- Less resilient under RF congestion

### Typical throughput

- 200–350 Mbps

### Cost

- **$40–$80 per side**

### Best when

- You want **cheap and functional**
- You’re OK with “good enough”
- This is a temporary or secondary link

---

## 4️⃣ MikroTik Wireless Wire / SXTsq / LHG

*(RouterOS-based bridges)*

### What it is

- Extremely powerful, extremely configurable wireless gear
- Used heavily by ISPs and serious hobbyists

### Strengths

- Absolute control
- Very strong RF performance
- True L2 transparency
- Works in weird edge cases

### Weaknesses

- **Steep learning curve**
- RouterOS is not friendly
- Easy to misconfigure if you’re rusty

### Typical throughput

- 300 Mbps → multi-Gbps (model dependent)

### Cost

- **$90–$200 per side**

### Best when

- You like **total control**
- You’re comfortable with RouterOS
- You want flexibility more than simplicity

---

## Side-by-Side Summary

| Feature | airMAX | UniFi Bridge | TP-Link CPE | MikroTik |
| --- | --- | --- | --- | --- |
| True L2 bridge | ✔️ | ✔️ | ✔️ | ✔️ |
| UniFi-managed | ❌ | ✔️ | ❌ | ❌ |
| Price | 💲 | 💲💲💲 | 💲 | 💲💲 |
| Stability | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Ease of setup | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |
| RF tolerance | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Indoor friendly | ⚠️ | ⚠️ | ⚠️ | ⚠️ |

---

## Why none of these behave like your AT&T extender

Your **WFEXT**:

- Acts as a *client*
- Rewrites MACs
- Is not Ethernet-transparent
- Breaks routing expectations

All four of these:

- Present **real Ethernet**
- Preserve MACs
- Don’t do NAT
- Don’t compete for DHCP
- Make the USG *actually behave like a router*

That’s the difference.

---

## If you’re not buying soon — what to remember

When/if you do revisit this later:

- **Best value**: Ubiquiti airMAX / LiteBeam
- **Best UniFi experience**: UniFi Building Bridge
- **Cheapest acceptable**: TP-Link CPE
- **Power-user favorite**: MikroTik

Given your background and tolerance for complexity, **airMAX** is honestly the sweet spot for you.

---

If you want, next time we can:

- Pick a *specific* model based on distance & walls
- Decide indoor vs outdoor mounting
- Design it so you can “drop it in” later with minimal downtime

And for now:  
**Option 1 + Cloud Key dark = expected behavior, not failure.**

---

AirMax looks to kill my bandwidth. the WFEXT is giving me 800 up and down. So I'm going to need a really good reason to want that one. I'll probably get the MikroTik. In the meantime I have another problem which is that UpnP is not enabled on my BGW620. How can I fix that? I need it for Roon Arc

---

You’re thinking about this exactly the right way.

Two parts to answer cleanly:

1. **Why airMAX looks like a bandwidth regression (you’re right)**
2. **Why UPnP on the BGW620 is the *real* blocker for Roon ARC — and how to fix it (or work around it)**

I’ll focus most on **UPnP + Roon ARC**, because that’s actionable *now*.

---

## Part 1 — Quick confirmation on airMAX vs MikroTik

You’re not wrong:

- Your **WFEXT doing ~800/800** means it’s almost certainly using:
	- Wi-Fi 6
	- Wide channels
	- Client-mode optimizations
- Classic airMAX (5 GHz, TDMA) **will cap out well below that** in real-world TCP

Your instinct to lean **MikroTik (Wi-Fi 6 / 802.11ax PtP)** is solid *if* you later buy something like:

- MikroTik **Wireless Wire AX**
- MikroTik **Cube 60Pro ac / ax**
- Or AX-capable SXTs

So your reasoning checks out. No argument from me there.

---

## Part 2 — UPnP on the AT&T BGW620 (hard truth first)

### ⚠️ The uncomfortable reality

> **AT&T gateways do not implement full, standards-compliant UPnP.**

On most BGW-series gateways (210, 320, 620):

- UPnP is:
	- ❌ Disabled by default
	- ❌ Sometimes hidden
	- ❌ Sometimes “enabled” but non-functional
	- ❌ Often blocked for inbound WAN pinholes

Even when the UI claims UPnP is “On,” **NAT-PMP and UPnP IGD requests are frequently ignored**.

This is a *known* problem for:

- Roon ARC
- Plex remote access
- Some game consoles
- Home servers

So you’re not misconfiguring it — you’re running into AT&T policy.

---

## Step 1 — Check if UPnP is even exposed (UI)

Log into your BGW620:

Then:

1. **Firewall**
2. **NAT/Gaming**
3. Look for:
	- “UPnP”
	- “NAT-PMP”
	- “Allow unsolicited inbound traffic”

On many BGW620 firmwares:

- UPnP **is not present at all**
- Or it’s greyed out
- Or enabling it does nothing

If you don’t see it → AT&T removed it.

---

## Step 2 — Why Roon ARC fails specifically

Roon ARC needs **one inbound TCP port** mapped dynamically from WAN → Core.

Normally it uses:

- UPnP or NAT-PMP to request the port
- Falls back to manual forwarding if that fails

Your BGW620:

- Does not honor the UPnP request
- So ARC reports “Not reachable outside your network”

---

## Step 3 — The reliable fix (manual port forwarding)

This **does work** on BGW gateways.

### A. Find your Roon Core IP

On the device running Roon Core:

- Note its LAN IP (e.g. `192.168.1.87`)
- Make sure it’s **DHCP reserved** in the BGW

### B. Create a manual port mapping

On BGW620:

1. **Firewall**
2. **NAT/Gaming**
3. **Custom Services**
4. Create a new service:
	- Protocol: **TCP**
	- External Port: (Roon will tell you — often 55000+)
	- Internal Port: same
	- Map to: Roon Core IP
5. Apply
6. Save

### C. Restart Roon Core

Then:

- Settings → Roon ARC
- Re-test connectivity

This bypasses UPnP entirely.

---

## Step 4 — If AT&T blocks inbound anyway (very possible)

Some AT&T fiber configs still block unsolicited inbound even with port forwarding.

If that happens, you have **two guaranteed solutions**:

---

### ✅ Solution A — Roon ARC via Tailscale (recommended)

Roon officially supports this now.

How it works:

- No inbound ports
- Uses outbound-only encrypted tunnels
- Works perfectly behind CGNAT / AT&T gateways

Steps (high-level):

1. Install **Tailscale** on:
	- Roon Core
	- Your phone
2. Enable Tailscale subnet routing (optional)
3. Point ARC to the Tailscale IP

**Pros**

- Zero gateway changes
- Secure
- Reliable

**Cons**

- Slightly higher latency
- Another service running

For AT&T users, this is *by far* the least painful path.

---

### ✅ Solution B — Put a real router in front later (MikroTik)

When you eventually do:

You regain:

- Proper UPnP
- NAT-PMP
- Full control

But this requires:

- Wired or true wireless bridge WAN
- Which you’ve already identified as a future step

---

## Decision table (for right now)

| Option | Cost | Effort | Reliability | AT&T-friendly |
| --- | --- | --- | --- | --- |
| Enable UPnP | $0 | Low | ❌ | ❌ |
| Manual port forward | $0 | Medium | ⚠️ | ⚠️ |
| Tailscale (Roon-supported) | $0 | Low | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| New router + passthrough | $$$ | High | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |

---

## My straight recommendation (given everything you said)

- **Short term**:  
	👉 Use **Tailscale for Roon ARC**
- **Medium term**:  
	👉 MikroTik wireless bridge + router
- **Do not waste time** trying to “fix” UPnP on BGW620 — it’s not you.

If you want, next I can:

- Walk you through **Tailscale + Roon ARC step-by-step**
- Or give you a **MikroTik model shortlist** that actually preserves your 800 Mbps

Just tell me which one you want to tackle first.

---

In adding the custom service there are the following parameters: - Service Name - Global Port Range - Base Host Port - Protocol

---

Perfect — that’s the right screen. AT&T just labels things in a slightly non-standard way, which makes this confusing.

I’ll translate **each field** into what it *really* means and then give you **exact values for Roon ARC**.

---

## What each field actually means (BGW620 language → reality)

### Service Name

- Just a label
- Anything descriptive

Example:

---

### Global Port Range

This is the **external (WAN) port** range.

- This is the port the *outside world* connects to
- For Roon ARC, this must match the port ARC is using

Examples:

or

(single-port ranges are written as start–end)

👉 **Use the exact port Roon ARC reports in Settings → ARC**

---

### Base Host Port

This is the **internal (LAN) port** on your Roon Core.

- Almost always the **same number** as the external port
- This is where the traffic lands *inside* your network

Example:

---

### Protocol

- Roon ARC uses **TCP only**

Set:

---

## Correct example configuration (copy this)

Assume Roon ARC says it needs port **55000**.

**Custom Service**

Then:

1. Save the service
2. Go back to **NAT/Gaming**
3. Assign this service to:
	- Your **Roon Core’s IP address**
4. Apply

---

## CRITICAL follow-ups (don’t skip)

### 1️⃣ Make sure the Roon Core IP is stable

On the BGW620:

- **Home Network → IP Allocation**
- Find your Roon Core
- Set it to **DHCP Fixed**

If the IP changes, ARC will break again.

---

### 2️⃣ Restart Roon Core

After saving the port mapping:

- Restart the Roon Core service
- Then re-test ARC

---

## If ARC still says “Not reachable”

This is **very common on AT&T**, even when port forwarding is correct.

That means AT&T is doing one of:

- Blocking unsolicited inbound
- Silent CGNAT behavior
- Ignoring the pinhole despite UI success

At that point:

- Your configuration is correct
- The gateway is the blocker

👉 **That’s when Tailscale becomes the guaranteed fix**

---

## Quick sanity check (optional)

From outside your network (cell phone on LTE/5G):

- Try connecting ARC
- If it fails immediately → inbound blocked
- If it spins → NAT is interfering

Either way, it tells us which AT&T limitation you’ve hit.

---

## Bottom line

You are configuring it **correctly** if:

- Global Port Range = external port
- Base Host Port = same internal port
- TCP only
- Fixed LAN IP

If you want, paste **the exact port number ARC shows** and I’ll sanity-check it — but you’re already on the right track.

---

OK on my Roon Client, the old external ISP address is assumed. How do I correct that?

---

This is a *very* normal Roon behavior after an ISP change — and it’s fixable without reinstalling anything.

What’s happening is:

> **Roon ARC cached the old public IP and will not automatically invalidate it**  
> until the Core re-advertises connectivity.

Let’s fix this cleanly.

---

## Why this happens (quickly)

- Roon Core discovers its **external address once**
- It caches:
	- Public IP
	- Port
- After ISP changes, ARC keeps trying the old endpoint
- Port forwarding alone does **not** force a refresh

So we need to **force the Core to re-detect its WAN identity**.

---

## Step-by-step fix (safe order)

### 1️⃣ Restart Roon Core (required)

On the machine running Roon Core:

- Fully restart the **Roon Server / Core service**
	- Not just the client UI

This alone fixes it ~50% of the time.

---

### 2️⃣ Force ARC to re-advertise

On any Roon client:

1. **Settings**
2. **Roon ARC**
3. Toggle **Enable ARC** → OFF
4. Wait 30 seconds
5. Toggle **Enable ARC** → ON
6. Click **Re-test**

This forces a new external IP discovery.

---

### 3️⃣ Clear ARC state (if still stuck)

If it *still* shows the old IP:

#### A. Disable ARC completely

- Settings → ARC → Disable

#### B. Restart Core again

#### C. Re-enable ARC

- Settings → ARC → Enable
- Wait for detection to complete

This flushes the cached WAN endpoint.

---

## If it still shows the old ISP IP

This means **Roon Core cannot reach the discovery service correctly**, usually because:

- AT&T blocks inbound verification
- UPnP is non-functional
- The gateway refuses NAT pinholes

At that point Roon **cannot verify reachability**, so it never updates the external IP.

---

## Guaranteed workaround (no port forwarding)

### ✅ Use Tailscale (Roon-supported)

Roon officially documents this because of AT&T-style gateways.

High level:

1. Install **Tailscale** on:
	- Roon Core machine
	- Phone running ARC
2. Log both into same Tailscale account
3. In ARC:
	- Let it auto-detect the Tailscale interface
	- Or manually point to the Core’s Tailscale IP (100.x.x.x)

No:

- UPnP
- Port forwarding
- Public IP detection

And it works immediately.

---

## Quick diagnostic question (one line)

After you:

- Restarted Core
- Disabled/re-enabled ARC

Does **Settings → ARC** now show:

- The **new AT&T public IP**?
- Or does it refuse to update?

If you tell me which, I can tell you instantly whether:

- You’re one step away
- Or AT&T is blocking discovery and we should switch strategies

You’re very close — this is the last annoying bit of ARC + AT&T friction.