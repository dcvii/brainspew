---
title: "Software for cracking software. Selecting tools for reverse engineering"
source: "https://hackmag.com/security/software-for-cracking-software"
author:
  - "[[Author: Nik Zerof]]"
  - "[[Nik Zerof]]"
published:
created: 2025-06-19
description: "Tech magazine for cybersecurity specialists"
tags:
  - "clippings"
---
![](https://hackmag.com/wp-content/uploads/2019/02/618855078-h.jpg)

Every reverse engineer, malware analyst or simply a researcher eventually collects a set of utility software that they use on a daily basis to analyze, unpack, and crack other software. This article will cover mine. It will be useful to anyone who has not yet collected their own toolset and is just starting to look into the subject. However, an experienced reverse engineer must also be curious about what other crackers are using.

  

## WARNING

This article is for information purposes only. Neither the editorial team nor the author assumes any responsibility for possible harm that may arise from the use of these materials.

## Debuggers

Debugging an application is an essential part of studying it, so every reverse engineer needs a debugger at the ready. A modern debugger must support both Intel architectures (x64 and x86), so this is the first prerequisite.

We must also be able to debug kernel-mode code. You will need this every once in a while, especially if you want to look for zero-day vulnerabilities in OS kernels or reverse engineer malware in drivers. The main candidates are x64dbg and WinDbg. The first debugger works in user mode, while the second one can debug kernel-mode code.

### x64dbg

[*x64dbg.com*](https://x64dbg.com/)

This is a modern debugger with a good user interface, a worthy successor of OllyDbg. It supports both architectures (x64 and x86), and there are tons of useful plugins.

![](https://hackmag.com/wp-content/uploads/2019/02/image2-1024x549.jpeg)

x64dbg

![](https://hackmag.com/wp-content/uploads/2019/02/image3-1024x549.jpeg)

Built-in decompiler

Granted, it has its downsides as there are a number of annoying bugs. But it is actively developed and supported. Since the debugger works in user mode, it is of course vulnerable to a wide range of anti-debugging techniques. This is, however, in part offset by the availability of many different debugger hiding plugins.

x64dbg has a built-in decompiler and imports reconstructor (both x64 and x86), supports code graph visualization and read/write/execute/access breakpoints. This debugger has enabled some hackers to break down the infamous Denuvo DRM system!

#### Why not OllyDbg

We haven’t included OllyDbg here because it is very outdated. It does not support the latest operating systems or x64. The app’s official website announced a x64 version and even reported some development progress, but the site itself has not been updated since 2014. OllyDbg is undoubtedly a milestone piece of software, but now it seems that its time has passed. There have also been fewer kernel mode debuggers since Syser Kernel Debugger, a successor to SoftICE, was abandoned.

### WinDbg

[*Official homepage*](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/)

WinDbg is one of the best kernel or driver debugging tools. This debugger is supported by Microsoft and included in the Windows Driver Kit (WDK). This is currently the most up-to-date and powerful kernel code debugger. It does not feature the user-friendly interface of x64dbg, but there are not many other options, as other debuggers don’t support kernel-mode code.

![](https://hackmag.com/wp-content/uploads/2019/02/image4-1024x490.jpeg)

WinDbg supports remote debugging and can download debug symbols directly from Microsoft servers. The VirtualKD booster exists to speed up the WinDbg setup for debugging kernel-mode code in a VM. WinDbg is definitely not for beginners, but as you gain experience in reverse engineering and start testing various interesting options, you won’t be able to avoid it.

WinDbg enables you to view various system structures and easily disassemble NTAPI functions. Of course it can also be used to debug “regular” applications, but I prefer to unleash this powerful weapon only when it is really needed!

## Disassemblers

Reverse engineering cannot exist without static code analysis tools. The current selection of disassemblers is not much better than that of debuggers, but there we still have some favorites. The IDA Pro disassembler is a de facto standard in antivirus labs. Next is the Radare2 reverse engineering framework (many reckon that Radare2 is on par with IDA).

### IDA Disassembler

[*hex-rays.com/products/ida*](https://www.hex-rays.com/products/ida/)

There are two versions of IDA, a paid Pro version and a free Starter version. The free version is limited to x86 and does not support plugins. The Pro version offers full functionality with a large number of supported processor architectures and plugin support.

![](https://hackmag.com/wp-content/uploads/2019/02/image5-1024x534.jpeg)

IDA does have a built-in debugger with rather basic functionality, but its unconventional interface takes some time to get used to. IDA can also be augmented with the Hex-Rays addon, a decompiler of application source code into C code. This is very useful as it really speeds up program analysis.

Overall, IDA is a very powerful and polished tool with a long development history. Unfortunately, the Pro version costs about $500-1000 (depending on the license type) and they do not sell it to just anybody. So we have to make do with other options.

### Radare2

[*rada.re*](https://rada.re/)

Radare2 was initially conceived as a simple hex editor but grew into a full framework able to debug and disassemble all types of code including firmware, viruses and cracks.

![](https://hackmag.com/wp-content/uploads/2019/02/image6-1024x550.jpeg)

Cutter + Radare2

Radare is a set of console tools including a debugger, disassembler, decompiler, hex editor, its own compiler, utility for comparing binary files and much more. There is also a GUI addon named Cutter that greatly improves the look and usability of Radare’s framework.

The framework supports a large number of processors and platforms, which enables it to compete with products like IDA Pro. Another big advantage of Radare is that it is an open source, free and community-driven project.

## Additional utilities

We have covered the main tools, but reverse engineering also needs packer identifiers, network monitors, hex editors and many other utilities. Let’s have a closer look to the main ones.

### Detect it Easy (DiE)

[*ntinfo.biz*](https://ntinfo.biz/)

This is a great packer identifier with a large number of useful functions. For example, it allows you to view file section entropy, which facilitates visual identification of encryption.

![](https://hackmag.com/wp-content/uploads/2019/02/image7.jpeg)

DiE

It also has a resource viewer with a dump-to-disk feature. DiE enables you to easily access the import table and add plugins and scripts, configure signature scanning methods and view file headers. It fully supports PE and PE+.

There is only one problem with this program: a slow update cycle, although it has not been abandoned. In fact, a new version was released recently!

#### INFO

You can see examples of working with DiE in my previous articles: [*“Manual unpacking. Cracking a custom packer based on GlobeImposter 2.0 ransomware”*](https://xakep.ru/2018/05/23/globeimposter-2/) and [*“The art of unpacking. Gutting the protection of the crafty GootKit banker”*](https://xakep.ru/2018/08/13/gootkit/).

### ExeInfoPE

[*exeinfo-pe.en.uptodown.com*](https://exeinfo-pe.en.uptodown.com/)

This is another packer and protector detector. It has an unconventional interface that will not be to everybody’s taste. On the other hand, the program is frequently updated, offers numerous interesting functions and user-friendly tips for unpacking.

![](https://hackmag.com/wp-content/uploads/2019/02/image9.jpeg)

ExeInfoPE

Overall, I would recommend it to beginners. ExeInfoPE has a number of automatic unpackers and will tell you which tool to use to crack a bolt-on protection system.

Of course, the program also offers the full set of standard features including a file header viewer, section viewer, hex viewer and even a number of built-in mini-utilities like TerminateProcess and more. ExeInfoPE also supports plugins.

### HxD

Sometimes you may need to access HDD, memory or applications in binary mode. This is where hex editors come in handy, as exemplified by HxD. This program is free and frequently updated, supports popular formats, is good for searching and offers a user-friendly UI. There are other well-executed features, such as the ability to remotely erase (zerofill) files. There is also a portable version for easy storage on a flash drive.

![](https://hackmag.com/wp-content/uploads/2019/02/image10-1024x549.jpeg)

HxD

### HIEW

[*hiew.ru*](http://www.hiew.ru/)

This hex editor has a long history, but it is still supported by its devs. It comes in free and paid versions (the latter is $20 without updates or $200 with lifelong updates). The Norton Commander-like interface might scare off a younger crowd, but it is easy to get used to. What is especially great about HIEW, is that you can work in “keyboard-only” mode by controlling all its functions via hotkeys.

![](https://hackmag.com/wp-content/uploads/2019/02/image11-1024x592.jpeg)

HIEW

### Pestudio

[*winitor.com*](https://www.winitor.com/)

A useful program for malware analysis. Prestudio automatically scans files samples with VirusTotal, offers an interesting view of the analyzed application’s import table functions, shows the application’s viral markers, used libraries and PE file header info. It also enables you to work with resources. In other words, this is a versatile antivirus tool for initial sample analysis.

![](https://hackmag.com/wp-content/uploads/2019/02/image12-1024x550.jpeg)

Pestudio

### PE-bear

[*The PE-bear page in the developer’s blog.*](https://hshrzd.wordpress.com/pe-bear/)

Another interesting viewer/editor of PE and PE+ files comes with a packer/protector identifier and shows info on file headers, resources and sections. If you want to, you can view sections in hex mode and disassemble them into regular assembler mnemonics.

![](https://hackmag.com/wp-content/uploads/2019/02/image13-1024x549.jpeg)

PE-bear

PE-bear has a user-friendly UI and file-comparing utility. The program’s only downside, despite its open source code, are its rare updates. So, if you find a bug, you can fix it yourself.

### Fakenet-NG

[*GitHub repository*](https://github.com/fireeye/flare-fakenet-ng)

This program emulates working with a network. When studying malware samples, you often need to see all their Internet activities: monitor DNS and HTTP queries, sniff traffic and identify IP addresses of the controlling servers (for example, if you are dealing with a ransomware bot). Your VM should of course be offline, but if the virus detects it, it won’t do all the things that it usually does.

Fakenet-NG is fully supported with frequent updates, so this utility can be used in the latest operating sytems.

![](https://hackmag.com/wp-content/uploads/2019/02/image14-1024x521.jpeg)

Fakenet-NG

### ProcessExplorer

[*Official homepage*](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)

It would be hard to perform reverse engineering without programs from Sysinternals that monitor how applications access the filesystem and processes. ProcessExplorer shows all processes in a hierarchical tree view, so you can easily see their spawning order. You can also see which dynamic libraries they use, as well as their priority, digital signatures, processor usage and much more.

![](https://hackmag.com/wp-content/uploads/2019/02/image15-1024x550.jpeg)

ProcessExplorer

### RegShot

[*SourceForge repository*](https://sourceforge.net/projects/regshot/)

A handy utility for monitoring registry changes. RegShot takes snapshots of the registry before and after you do some system or software changes.

### TCPView

[*Official homepage*](https://docs.microsoft.com/en-us/sysinternals/downloads/tcpview)

A small program for monitoring an application’s network activity. You can see which ports it accesses (both local and remote), together with protocols, process identifiers and transmitted packet counters. Overall, this is one of the most useful tools for any hacker!

![](https://hackmag.com/wp-content/uploads/2019/02/image16-1024x549.jpeg)

TCPView

### Resource Hacker

[*angusj.com/resourcehacker*](http://www.angusj.com/resourcehacker/)

A popular program for editing resources, including manifests, icons, text dialog lines, cursor info and much more. You won’t need this functionality very often, but when you do, this is a suitable tool to have.

![](https://hackmag.com/wp-content/uploads/2019/02/image17-1024x548.jpeg)

Resource Hacker

## Summing up

We have covered the main utilities used for most reverse engineering tasks. I think this should be enough for a beginner. Your own list will grow as you progress.

Many reverse engineers end up writing their own targeted programs, plugins and scripts. You won’t be able to find tools for every task that will make your life easier. If you know similar software or want to share links to other useful tools, please do so in the comments!

Related posts:

![](https://hackmag.com/wp-content/uploads/2023/03/dhcp-1600-150x150.jpg)

###### 2023.03.26 — Attacks on the DHCP protocol: DHCP starvation, DHCP spoofing, and protection against these techniques

Chances are high that you had dealt with DHCP when configuring a router. But are you aware of risks arising if this protocol is misconfigured on a…

![](https://hackmag.com/wp-content/uploads/2023/02/applepay-h-150x150.jpg)

###### 2023.02.13 — First Contact: Attacks on Google Pay, Samsung Pay, and Apple Pay

Electronic wallets, such as Google Pay, Samsung Pay, and Apple Pay, are considered the most advanced and secure payment tools. However, these systems are also…

![](https://hackmag.com/wp-content/uploads/2022/02/cc-h-150x150.jpg)

###### 2022.02.09 — First contact: An introduction to credit card security

I bet you have several cards issued by international payment systems (e.g. Visa or MasterCard) in your wallet. Do you know what algorithms are…

![](https://hackmag.com/wp-content/uploads/2022/06/fuzz-h-150x150.jpg)

###### 2022.06.01 — WinAFL in practice. Using fuzzer to identify security holes in software

WinAFL is a fork of the renowned AFL fuzzer developed to fuzz closed-source programs on Windows systems. All aspects of WinAFL operation are described in the official documentation,…

![](https://hackmag.com/wp-content/uploads/2023/06/cold-1600-150x150.jpg)

###### 2023.06.08 — Cold boot attack. Dumping RAM with a USB flash drive

Even if you take efforts to protect the safety of your data, don't attach sheets with passwords to the monitor, encrypt your hard drive, and always lock your…

![](https://hackmag.com/wp-content/uploads/2022/02/core-h-150x150.jpg)

###### 2022.02.09 — Kernel exploitation for newbies: from compilation to privilege escalation

Theory is nothing without practice. Today, I will explain the nature of Linux kernel vulnerabilities and will shown how to exploit them. Get ready for an exciting journey:…

![](https://hackmag.com/wp-content/uploads/2022/12/62cdc0dc38031b519f901a0c_end-to-end-testing-150x150.jpg)

###### 2022.12.15 — What Challenges To Overcome with the Help of Automated e2e Testing?

This is an external third-party advertising publication. Every good developer will tell you that software development is a complex task. It's a tricky process requiring…

![](https://hackmag.com/wp-content/uploads/2022/02/ccf-h-150x150.jpg)

###### 2022.02.15 — First contact: How hackers steal money from bank cards

Network fraudsters and carders continuously invent new ways to steal money from cardholders and card accounts. This article discusses techniques used by criminals to bypass security…

![](https://hackmag.com/wp-content/uploads/2022/01/lrl-h-150x150.jpg)

###### 2022.01.13 — Bug in Laravel. Disassembling an exploit that allows RCE in a popular PHP framework

Bad news: the Ignition library shipped with the Laravel PHP web framework contains a vulnerability. The bug enables unauthorized users to execute arbitrary code. This article examines…

![](https://hackmag.com/wp-content/uploads/2022/02/eve-h-150x150.jpg)

###### 2022.02.15 — EVE-NG: Building a cyberpolygon for hacking experiments

Virtualization tools are required in many situations: testing of security utilities, personnel training in attack scenarios or network infrastructure protection, etc. Some admins reinvent the wheel by…