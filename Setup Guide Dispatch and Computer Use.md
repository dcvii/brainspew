---
title: "Setup Guide: Dispatch and Computer Use"
source: "https://promptkit.natebjones.com/20260324_6hc_guide_main"
author:
published:
created: 2026-03-28
description:
tags:
  - "brain_spew"
---
*This is the companion setup guide to \[The Work That Actually Leaves Your Desk\]. Everything below gets you from zero to running. No demo tasks, no pretend assignments. Just the setup so you're ready when you know what you want to delegate.*

---

## What you need before you start

Two things are non-negotiable:

**A paid Claude plan.** Pro ($20/month) or Max ($100-200/month). Free accounts can't use Dispatch or computer use. If you're not sure which plan you're on, open the Claude app on any device, go to Settings, and check your subscription tier.

**Two devices.** A Mac (desktop or laptop) and a phone (iPhone or Android). Dispatch works by pairing your phone with your computer. Your Mac does the work. Your phone is how you talk to it when you're not at your desk.

That's it. Everything else gets set up in the next ten minutes.

---

## Part 1: Setting up Dispatch

Dispatch gives you a single, persistent conversation with Claude that you can reach from your phone or your desktop. You assign work from wherever you are. Claude runs it on your Mac. You come back to finished results.

### Step 1: Get the desktop app current

Open **Claude Desktop** on your Mac. If you don't have it installed, download it from [claude.com/download](https://claude.com/download).

If you already have it, update it. Claude Desktop auto-updates, but you can force it: click **Claude** in the menu bar, then **Check for Updates**. You need the latest version. Dispatch won't appear if your app is out of date.

### Step 2: Get the mobile app current

Open the **App Store** (iPhone) or **Google Play Store** (Android) and update the Claude app. If you don't have it installed, search for "Claude" and install it. Sign in with the same account you use on your Mac.

### Step 3: Open Dispatch on your desktop

Open Claude Desktop. At the top, you'll see tabs for **Chat** and **Cowork**. Click into **Cowork**.

In the left sidebar, click **Dispatch**. You'll see a page explaining what it does. Click **Get started**.

On the next screen, you'll see two toggles:

- **Give Claude access to your files.** Turn this on if you want Claude to work with files on your computer (you probably do).
- **Keep your computer awake.** Turn this on. If your Mac falls asleep, Claude stops working. This toggle prevents that while Dispatch is active.

Click **Finish setup**.

### Step 4: Open the Claude app on your phone

Open Claude on your phone. You should see Dispatch available in the same place. Your conversation syncs between both devices automatically. Whatever you type on your phone, Claude executes on your Mac.

That's it. Dispatch is live.

### What to know before you start using it

**Your Mac has to stay on.** This is the biggest constraint. Dispatch runs on your computer, not in the cloud. If you close the Claude Desktop app or your Mac goes to sleep (and you didn't enable the "keep awake" toggle), work stops. If you're leaving your desk and want Claude to keep working, leave your Mac plugged in with the app open.

**It's one thread.** You can't start multiple Dispatch conversations. Everything lives in a single continuous thread. Claude remembers context from previous tasks, so you don't have to re-explain yourself each time.

**You can't send files from your phone.** Not yet. If Claude needs a file, it pulls it from your Mac. If you need to get a file to your Mac from your phone, sync through iCloud, Google Drive, or Dropbox first.

**Complex tasks don't always land.** Simple stuff (file search, summaries, drafting) works well. Multi-step workflows across several apps succeed roughly half the time. This is a research preview. It's improving fast, but go in expecting rough edges and you'll get more out of it.

For the full documentation, see Anthropic's guide: [Assign tasks to Claude from anywhere in Cowork](https://support.claude.com/en/articles/13947068-assign-tasks-to-claude-from-anywhere-in-cowork)

---

## Part 2: Setting up Computer Use

Computer use lets Claude interact with apps on your Mac by controlling your screen directly. It clicks, types, scrolls, and navigates, just like you would. This is how Claude reaches tools that don't have a connector, like an internal dashboard, a desktop app, or a browser-based tool nobody ever built an API for.

You don't need computer use to use Dispatch. Dispatch works with connectors and file access on its own. Computer use just extends what Dispatch can reach.

### How Claude decides what to use

When you assign a task, Claude picks the fastest path:

1. **Connectors first.** If you've connected Slack, Gmail, Google Drive, or any other service, Claude uses those integrations. They're fast and reliable.
2. **Browser second.** If there's no connector but the tool is web-based, Claude opens Chrome and navigates to it.
3. **Screen interaction last.** If nothing else works, Claude takes over your screen. This is the slowest option, but it's the one that can reach anything.

You don't choose which method Claude uses. It picks automatically. Computer use is always the fallback, not the default.

### Step 1: Turn it on

Open **Claude Desktop** on your Mac. Go to **Settings** (click the gear icon or go to Claude > Settings in the menu bar).

Under **Desktop app**, click **General**.

Find the **Computer use** toggle and turn it on.

### Step 2: Grant macOS permissions

Your Mac will ask you to grant two system permissions:

- **Accessibility:** This lets Claude click, type, and scroll on your screen.
- **Screen Recording:** This lets Claude see what's on your screen (it takes screenshots to understand where things are).

Both are required. If either is missing, computer use won't work. You can manage these later in **System Settings > Privacy & Security**.

### Step 3: That's it

There's no step 3. Computer use activates automatically when Claude needs it. The first time Claude wants to use a specific app, you'll see a permission prompt asking you to approve access for that app. You can allow it for the current session or deny it.

### What to know before you start using it

**Claude asks before touching each app.** You'll see a prompt every time Claude wants to access a new application. Nothing happens without your approval. Some apps (investment platforms, crypto wallets) are blocked by default.

**It's slow.** Screen interaction is the most fragile and time-consuming way for Claude to work. If a connector exists for the tool you're using, connect it instead. Computer use is for the stuff that has no other option.

**It's macOS only.** Windows support is coming but isn't here yet.

**Close sensitive apps first.** When computer use is active, Claude can see anything visible on your screen. If you have banking, medical, or other sensitive apps open, close them before starting a session.

**Start simple.** Anthropic's own recommendation is to begin with research or organizing tasks rather than complex multi-step workflows. Computer use works well for known, repetitive flows where the UI is consistent. It's less reliable for exploratory navigation through apps it's never seen.

For the full documentation, see Anthropic's guide: [Let Claude use your computer in Cowork](https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork)

---

## You're set up. Now what?

Both features are live. You don't need to do anything else before using them.

The article that goes with this guide covers what's actually worth pointing these tools at, and the prompt pack gives you ready-to-paste starting points for the categories of work that matter most. The setup is the easy part. The hard part is figuring out what you're carrying that you shouldn't be.

Go read the piece. Then name your open loops. Then delegate.

\[Link to article\] | \[Link to prompt pack\]