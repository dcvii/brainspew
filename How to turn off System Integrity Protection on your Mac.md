---
title: "How to turn off System Integrity Protection on your Mac"
source: "https://www.imore.com/how-turn-system-integrity-protection-macos"
author:
  - "[[Joseph Keller]]"
published: 2020-08-28
created: 2025-02-12
description: "System Integrity Protection exists to keep your Mac safe. If you absolutely need to turn it off, however, here's how you do it."
tags:
  - "clippings"
---
![macOS Catalina](https://cdn.mos.cms.futurecdn.net/a75HKbAkdD3WbSsyWZZVSY-1200-80.jpg)

macOS Catalina (Image credit: iMore)

System Integrity Protection (SIP) is a security feature of macOS designed to make it even more difficult for malware to access important system files, keeping them safe from unwanted modifications. In the early days of SIP, some developers ran into problems when the system would keep core functionality of their apps from working properly because those apps made changes to the way the operating system worked by editing the system files that SIP was now in place to protect.

Because of this, many developers (and some users) would disable SIP to let their apps work properly. Now, several years on, this is less necessary as most apps have found ways to do what they need to do without the need to disable SIP, allowing your Mac to stay more secure.

But if you absolutely need to turn off System Integrity Protection, there's a way to do it. You'll just need to use Recovery Mode and the Terminal to get it done.

## How to turn off System Integrity Protection in macOS

1. Click the **Apple symbol** in the Menu bar.
2. Click **Restart…**
3. Hold down **Command-R** to reboot into Recovery Mode.
4. Click **Utilities**.
5. Select **Terminal**.
6. Type **`csrutil disable`**.
7. Press **Return** or **Enter** on your keyboard.
8. Click the **Apple symbol** in the Menu bar.
9. Click **Restart…**

If you later want to start using SIP once again (and you really should), then follow these steps again, except this time you'll enter **`csrutil enable`** in the Terminal instead.

## How to check if System Integrity Protection is enabled or disabled

If you want to check the status of System Integrity Protection, it's just a quick pop into the Terminal and a short command. You don't even need to be in Recovery Mode this time.

1. Open **Terminal** from your Dock or Utilities folder.
2. Type **`csrutil status`** into Terminal.

![Check System Integrity Protection Status, showing how to open Terminal, then enter csrutil status](https://cdn.mos.cms.futurecdn.net/UFAA4QHs8ANvSKGm94HiQ8-320-80.jpg)

Check System Integrity Protection Status, showing how to open Terminal, then enter csrutil status (Image credit: iMore)

3. Hit **Return** or **Enter** on your keyboard.

You'll see the message **System Integrety Protection status: enabled** or **System Integrety Protection status: disabled** right after you hit Return.

## Questions

If you have any more questions about turning off System Integrity Protection, let us know in the comments.

iMore offers spot-on advice and guidance from our team of experts, with decades of Apple device experience to lean on. Learn more with iMore!

**Updated August 2020:** Updated for macOS Catalina and the macOS Big Sur beta.

<iframe data-lazy-priority="low" data-lazy-src="https://www.youtube.com/embed/eGAXfAxCIH8" allowfullscreen=""></iframe>

Joseph Keller is the former Editor in Chief of iMore. An Apple user for almost 20 years, he spends his time learning the ins and outs of iOS and macOS, always finding ways of getting the most out of his iPhone, iPad, Apple Watch, and Mac.

### Most Popular