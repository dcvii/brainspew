---
title: "Mac IIfx | Low End Mac"
source: "https://lowendmac.com/1990/macintosh-iifx/"
author:
published:
created: 2025-03-26
description:
tags:
  - "clippings"
---
Six months after moving from 16 MHz to 25 MHz with the [IIci](http://lowendmac.com/1989/mac-iici/ "Mac IIci"), Apple introduced the “wicked fast” 40 MHz IIfx. This was the Mac of choice for graphic designers, offering nearly three times the performance of the [IIx](http://lowendmac.com/1988/mac-iix/ "Mac IIx") – thanks to a lightning fast CPU, a new type of RAM, and special SCSI DMA and I/O chips which relieved the CPU of much of its burden. A built-in 32 KB static RAM cache also helps boost performance.

![Macintosh IIfx with RGB display](https://lowendmac.com/ii/art/mac-ii-with-rgb-256.jpg)The IIfx was built on a 40 MHz motherboard and had the fastest clocked CPU that Apple used until the [Quadra 840av](http://lowendmac.com/1993/quadra-840av/) of 1993. NuBus cards still ran on a 10 MHz bus, which is one reason Apple announced its first accelerated video card, the [8•24GC](http://lowendmac.com/2000/apple-8-24gc-video-card/), along with the IIfx. Regular video cards were simply overshadowed by the rest of the system.

With a nod to it’s Apple II ancestors, the IIfx had two 6502 CPUs to manage the floppy drive(s), ADB port, and serial ports (see [Technote HW 09](http://developer.apple.com/technotes/hw/hw_09.html) for more details). Unlike the 1 MHz Apple II computers, these CPUs ran at 10 MHz.

The IIfx introduced latched read/write RAM to the Apple lexicon. Using a 64-pin SIMM different from that in any other Macintosh, the IIfx could overlap read and write operations. (*Byte,* 4/90, p. 112)

The IIfx requires a special “black” SCSI terminator to accommodate its unusual architecture (see [Termination Explained](http://lowendmac.com/1998/termination-explained/) for more details).

- Got a Mac II or other vintage Mac? Join our [Vintage Macs Group](http://lowendmac.com/1998/low-end-macs-vintage-macs-group/) or Vintage Macs Forum.
- Our [System 6 List](http://lowendmac.com/lists/system6.html) is for those using Mac System 6.

There is a ROM SIMM slot on the Mac IIfx that must be filled with a IIfx ROM. Without this ROM, the computer will not function.

Although appearing identical to the Mac II and IIx, the IIfx power supply has a variable speed fan to better control noise and cooling.

### Dash 30fx, a IIfx on Steroids

A company known as [68000](http://lowendmac.com/2016/the-68000-dash-30fx-an-accelerate-mac-iifx/) repackaged the Mac IIfx logic board in a huge, heavy metal case, overclocked the board to 50 or 55 MHz, replaced the 40 MHz CPU and FPU with the 50 MHz version, installed even faster RAM, and turned the “wicked fast” IIfx into something 25-35% faster!

### Upgrade Advice

Accelerators are almost unknown for the IIfx, so many years after it was discontinued.

- IIfx RAM is relatively costly, but you should have at least 8 MB. When upgrading, consider putting as much in one bank as possible, leaving the other bank for future expansion.
- An accelerated video card can make a world of difference, particularly if you use 16-bit or 24-bit modes or a monitor larger than 640 x 480 pixels. See our [NuBus Video Card Guide](http://lowendmac.com/video/index.html) for lots of information.
- A newer hard drive will be larger and faster than the one Apple shipped with the computer, but you won’t be able to take full advantage of that speed on the IIfx without a SCSI accelerator.
- More RAM plus Speed Doubler equals improved hard drive performance through intelligent caching.

Because it uses oddball memory and has some unusual circuitry, we label the IIfx a [Limited Mac](http://lowendmac.com/roadapples/iifx.shtml).

### Details

- introduced 1990.03.19 at $9,900; discontinued 1992.04.15
- code names: F-16, F-19, Stealth, Blackbird, Zone 5, Four Square, IIxi, Weed Whacker
- model no.: M5525
- Gestalt ID: 13

#### Mac OS

- requires System 6.0.5 to 7.6.1
- addressing: 24-bit or 32-bit

#### Core System

- CPU: 40 MHz 68030
- FPU: 40 MHz 68882 FPU
- Bus: 40 MHz – fastest until [Quadra 840av](http://lowendmac.com/1993/quadra-840av/)
- ROM: 512 KB
- RAM: 4 MB, expandable to 128 MB using both 4-SIMM banks of 80ns 64-pin memory; can use 1 MB, 4 MB, 8 MB, and 16 MB SIMMs (the IIfx was the only Mac to use 64-pin SIMMs)
- L2 cache: 32 KB

#### Performance

- 6.8, relative to SE
- 4.60, MacBench 2.0 CPU
- 11.45, Speedometer 3.06
- 0.71, Speedometer 4
- 10.0 MIPS
- see [Benchmarks: IIfx](http://lowendmac.com/benchmarks/iifx.shtml) for more details

#### Graphics

- video: requires video card – see our [NuBus Video Card Guide](http://lowendmac.com/video/index.html) for more information.

#### Drives

- Hard drive: 40, 80, or 160 MB SCSI
- floppy drive: 1.4 MB double-sided
- internal bay for second floppy drive

#### Expansion

- ADB ports: 2
- serial ports: 2 DIN-8 RS-422 ports on back of computer
- SCSI ports: DB-25 connector on back of computer
- sound: 8-bit stereo
- NuBus slots: 6
- one PDS slot (inline with a NuBus slot)

#### Physical

- size (HxWxD): 5.5″ x 18.7″ x 14.5″
- Weight: 24 lb.
- PRAM battery: 3.6V half-AA
- power supply: 230W

### Upgrades

- [Chipping the Mac II Series](http://lowendmac.com/2014/overclocking-the-mac-ii-series/)
- [Output Enablers](http://outputenablers.com/) 46.5-50 MHz clock accelerator
- MicroMac [Speedy](http://www.micromac.com/products/speedy.html) variable speed oscillator (to 50 MHz)

Discontinued accelerators (all are 68040) include the Applied Engineering TransWarp (25, 33 MHz 68040), Fusion Data TokaMac FX (33 MHz 68040), and [Radius Rocket](http://lowendmac.com/1991/radius-rocket-and-stage-ii-rocket/) (25 MHz 68LC040 to 40 MHz 68040).

### Online Resources

- [Guide to the Macintosh II Series](https://lowendmac.com/1992/overview-of-the-mac-ii-series/ "Guide to the Macintosh II Series"), an overview of the Mac II family.
- [Clock Chipping the Mac IIfx](http://www.applefool.com/clockchipping/iifx.html), Marc Schrier. If you upgrade to the 50 MHz 68030 CPU, you may be able to reach 60 MHz, and you can usually overclock to stock 40 MHz chip to 50 MHz.
- [Know Your Mac’s Upgrade Options](http://lowendmac.com/ed/herlihy/08ph/upgrade-options.html), Phil Herlihy, The Usefulness Equation, 2008.08.26. Any Mac can be upgraded, but it’s a question of what can be upgraded – RAM, hard drive, video, CPU – and how far it can be upgraded.
- [Creating Classic Mac Boot Floppies in OS X](http://lowendmac.com/2008/creating-classic-mac-boot-floppies-in-os-x/), Paul Brierley, The ‘Book Beat, 2008.08.07. Yes, it is possible to create a boot floppy for the Classic Mac OS using an OS X Mac that doesn’t have Classic. Here’s how.
- [The Compressed Air Keyboard Repair](http://lowendmac.com/misc/08mr/air-keyboard-cleaning.html), Charles W Moore, Miscellaneous Ramblings, 2008.07.24. If your keyboard isn’t working as well as it once did, blasting under the keys with compressed air may be the cure.
- [Why You Should Partition Your Mac’s Hard Drive](http://lowendmac.com/2008/why-you-should-partition-your-macs-hard-drive/), Dan Knight, Mac Musings, 2008.12.11. “At the very least, it makes sense to have a second partition with a bootable version of the Mac OS, so if you have problems with your work partition, you can boot from the ’emergency’ partition to run Disk Utility and other diagnostics.”
- [10 cult Macs adored by collectors](http://lowendmac.com/2008/cult-macs-adored-collectors/), Tamara Keel, Digital Fossils, 2008.05.13. Macs are not only noted for their longevity, but also by the passion which collectors have for some of the most interesting models ever made.
- [A Vintage Mac Network Can Be as Useful as a Modern One](http://lowendmac.com/myturn/0803my/nygren-vintage-network.html), Carl Nygren, My Turn, 2008.04.08. Old Macs can exchange data and share an Internet connection very nicely using Apple’s old LocalTalk networking.
- [Too few USB ports in too many Macs, developer Leopard ran on Yikes, Mac IIfx RAM heaven, and more](http://lowendmac.com/mail/0801mb/0116.html), Dan Knight, Low End Mac Mailbag, 2008.01.16. Also Macworld Expo disappoints, Pismo a great field computer, using flash memory in vintage Macs, and Word vs. Pages for academic writing.
- [512 MB in tray-loading iMacs, partitioning iBook (FireWire) hard drive, value of Kanga, and more](http://lowendmac.com/mail/0801mb/0103.html), Dan Knight, Low End Mac Mailbag, 2008.01.03. Also a source for Mac IIfx SCSI terminators, ongoing problems with a Rev. B iMac, and need to match screen size to printed output.
- [Vintage Mac Networking and File Exchange](http://lowendmac.com/2007/vintage-mac-networking-and-file-exchange/), Adam Rosen, Adam’s Apple, 2007.12.19. How to network vintage Macs with modern Macs and tips on exchanging files using floppies, Zip disks, and other media.
- [Vintage Mac Video and Monitor Mania](http://lowendmac.com/2007/vintage-mac-video-and-monitor-mania/), Adam Rosen, Adam’s Apple, 2007.12.17. Vintage Macs and monitors didn’t use VGA connectors. Tips on making modern monitors work with old Macs.
- [Getting Inside Vintage Macs and Swapping Out Bad Parts](http://lowendmac.com/2007/getting-inside-vintage-macs-and-swapping-out-bad-parts/), Adam Rosen, Adam’s Apple, 2007.12.14. When an old Mac dies, the best source of parts is usually another dead Mac with different failed parts.
- [Solving Mac Startup Problems](http://lowendmac.com/2007/solving-mac-startup-problems/), Adam Rosen, Adam’s Apple, 2007.12.12. When your old Mac won’t boot, the most likely culprits are a dead PRAM battery or a failed (or failing) hard drive.
- [Better and Safer Surfing with Internet Explorer and the Classic Mac OS](http://lowendmac.com/2007/better-safer-surfing-with-internet-explorer-and-the-classic-mac-os/), Max Wallgren, Mac Daniel, 2007.11.06. Tips on which browsers work best with different Mac OS versions plus extra software to clean cookies and caches, detect viruses, handle downloads, etc.
- [Simple Macs for Simple Tasks](http://lowendmac.com/thomas/tt07/1019.html), Tommy Thomas, Welcome to Macintosh, 2007.10.19. Long live 680×0 Macs and the classic Mac OS. For simple tasks such as writing, they can provide a great, low distraction environment.
- [Interchangeabilty and Compatibility of Apple 1.4 MB Floppy SuperDrives](http://lowendmac.com/2007/interchangeabilty-and-compatibility-of-apple-1-4-mb-floppy-superdrives/), Sonic Purity, Mac Daniel, 2007.09.26. Apple used two kinds of high-density floppy drives on Macs, auto-inject and manual inject. Can they be swapped?
- [The 25 most important Macs (part 2)](http://lowendmac.com/2009/the-25-most-important-macs/), Dan Knight, Mac Musings, 2009.02.17. The 25 most significant Macs in the first 25 years of the platform, continued.
- [Golden Apples: The 25 best Macs to date](http://lowendmac.com/ed/ms-geek/09msgk/golden-apples.html), Michelle Klein-Häss, Geek Speak, 2009.01.27. The best Macs from 1984 through 2009, including a couple that aren’t technically Macs.
- [Macintosh IIx: Apple’s flagship gains a better CPU, FPU, and floppy drive](http://lowendmac.com/musings/mm07/0919.html), Dan Knight, Mac Musings, 2007.09.19. 20 years ago Apple improved the Mac II by using a Motorola 68030 CPU with the new 68882 FPU. And to top it off, the IIx was the first Mac that could read DOS disks with its internal drive.
- [Vintage Macs provide a less distracting writing environment](http://lowendmac.com/richards/adv07/0918.html), Brian Richards, Advantage Mac, 2007.09.18. A Mac OS X user finds an old Macintosh IIsi and discovers the joy of writing undisturbed by music, messaging, and streaming content.
- [Mac System 7.5.5 Can Do Anything Mac OS 7.6.1 Can](http://lowendmac.com/2007/system-7-5-5-can-do-anything-mac-os-7-6-1-can/), Tyler Sable, Classic Restorations, 2007.06.04. Yes, it is possible to run Internet Explorer 5.1.7 and SoundJam with System 7.5.5. You just need to have all the updates – and make one modification for SoundJam.
- [Appearance Manager Allows Internet Explorer 5.1.7 to Work with Mac OS 7.6.1](http://lowendmac.com/2007/appearance-manager-lets-internet-explorer-5-1-7-work-with-mac-os-7-6-1/), Max Wallgren, Mac Daniel, 2007.05.23. Want a fairly modern browser with an old, fast operating system? Mac OS 7.6.1 plus the Appearance Manager and Internet Explorer may be just what you want.
- [Format Any Drive for Older Macs with Patched Apple Tools](http://lowendmac.com/2007/format-any-hard-drive-for-older-macs-with-patched-apple-tools/), Tyler Sable, Classic Restorations, 2007.04.25. Apple HD SC Setup and Drive Setup only work with Apple branded hard drives – until you apply the patches linked to this article.
- [Making floppies and CDs for older Macs using modern Macs, Windows, and Linux PCs](http://lowendmac.com/2007/making-floppies-and-cds-for-older-macs-using-modern-macs-windows-and-linux-pcs/), Tyler Sable, Classic Restorations, 2007.03.15. Older Macs use HFS floppies and CDs. Here are the free resources you’ll need to write floppies or CDs for vintage Macs using your modern computer.
- [System 7 Today, advocates of Apple’s ‘orphan’ Mac OS 7.6.1](http://lowendmac.com/thomas/06/1026.html), Tommy Thomas, Welcome to Macintosh, 2006.10.26. Why Mac OS 7.6.1 is far better for 68040 and PowerPC Macs than System 7.5.x.
- [30 days of old school computing: No real hardships](http://lowendmac.com/hodges/06/1011.html), Ted Hodges, Vintage Mac Living, 2006.10.11. These old black-and-white Macs are just fine for messaging, word processing, spreadsheets, scheduling, contact management, and browsing the Web.
- [Jag’s House, where older Macs still rock](http://lowendmac.com/thomas/06/0925.html), Tommy Thomas, Welcome to Macintosh, 2006.09.25. Over a decade old, Jag’s House is the oldest Mac website supporting classic Macs and remains a great resource for vintage Mac users.
- [Mac OS 8 and 8.1: Maximum Size, Maximum Convenience](http://lowendmac.com/2014/mac-os-8-and-8-1-maximum-size-maximum-convenience/), Tyler Sable, Classic Restorations, 2006.09.11. Mac OS 8 and 8.1 add some useful new features and tools, and it can even be practical on 68030-based Macs.
- [Vintage Macs with System 6 run circles around 3 GHz Windows 2000 PC](http://lowendmac.com/2006/vintage-macs-with-system-6-run-circles-around-3-ghz-windows-pc/), Tyler Sable, Classic Restorations, 2006.07.06. Which grows faster, hardware speed or software bloat? These benchmarks show vintage Macs let you be productive much more quickly than modern Windows PCs.
- [Floppy drive observations: A compleat guide to Mac floppy drives and disk formats](http://lowendmac.com/2006/floppy-drive-observations-a-compleat-guide-to-mac-floppy-drives-and-disk-formats/), Scott Baret, Online Tech Journal, 2006.06.29. A history of the Mac floppy from the 400K drive in the Mac 128K through the manual-inject 1.4M SuperDrives used in the late 1990s.
- [Moving files from your new Mac to your vintage Mac](http://lowendmac.com/brierley/06/0613.html), Paul Brierley, The ‘Book Beat, 2006.06.13. Old Macs use floppies; new ones don’t. Old Macs use AppleTalk; Tiger doesn’t support it. New Macs can burn CDs, but old CD drives can’t always read CD-R. So how do you move the files?
- [System 7.6.1 is perfect for many older Macs](http://lowendmac.com/martorana/06/0324.html), John Martorana, That Old Mac Magic, 2006.03.24. Want the best speed from your old Mac? System 7.6.1 can give you that with a fairly small memory footprint – also helpful on older Macs.
- [MpegDec: Play MP3s and streaming audio on 680×0 and old PowerPC Macs](http://lowendmac.com/thompson/06/0314.html), Nathan Thompson, Embracing Obsolescence, 2006.03.14. 680×0 Macs can play anything short of 128kbps stereo MP3s, and even the oldest PowerPC Macs have no trouble at all with those recordings.
- [System 7.5 and Mac OS 7.6: The beginning and end of an era](http://lowendmac.com/2014/system-7-5-and-mac-os-7-6-the-beginning-and-end-of-an-era/), Tyler Sable, Classic Restorations, 2006.02.15. System 7.5 and Mac OS 7.6 introduced many new features and greater modernity while staying within reach of most early Macintosh models.
- [System 7: Bigger, better, more expandable, and a bit slower than System 6](http://lowendmac.com/2014/system-7-bigger-better-more-expandable-and-a-bit-slower-than-system-6/), Tyler Sable, Classic Restorations, 2006.01.04. The early versions of System 7 provide broader capability for modern tasks than System 6 while still being practical for even the lowliest Macs.
- [Web browser tips for the classic Mac OS](http://lowendmac.com/thompson/06/0103.html), Nathan Thompson, Embracing Obsolescence, 2006.01.03. Tips on getting the most out of WaMCom, Mozilla, Internet Explorer, iCab, Opera, and WannaBe using the classic Mac OS.
- [The Joy of Six: Apple’s fast, svelte, reliable, and still usable System 6](http://lowendmac.com/2014/the-joy-of-six-apples-fast-svelte-reliable-and-still-useful-system-6/), Tyler Sable, Classic Restorations, 2005.12.06. System 6 was small enough to run quickly from an 800K floppy yet powerful enough to support 2 GB partitions, 24-bit video, and the Internet.
- [Which system software is best for my vintage Mac?](http://lowendmac.com/2007/system-7-5-5-can-do-anything-mac-os-7-6-1-can/), Tyler Sable, Classic Restorations, 2005.11.22. Which system software works best depends to a great extent on just which Mac you have and how much RAM is installed.
- [Apple Macintosh IIfx](http://www.mayrandcomputer.com/ "Apple Macintosh IIfx"), Justin Mayrand
- [Macintosh II Family Technical Overview](http://www.angelfire.com/ca2/tech68k/macii.html), darknerd, Angelfire. Some excellent, rarely discussed technical details on the whole Mac II lineup.
- [Macintosh IIfx](http://www.angelfire.com/ca2/dev68k/iifxmain.html), Dev68k. All sorts of technical details on the “wicked fast” Mac IIfx.
- Benchmark: [Mac OS 8.1 on the “wicked fast” Mac IIfx](http://lowendmac.com/benchmarks/iifx.shtml#81), 2000.08.31. Not only does it work, but performance is excellent.
- Run Mac OS 8.1 on your ‘030 Mac, Charles W Moore, Applelinks, 2000.08.08. “Born Again enables certain 68030 Macs to support Mac OS 8.1.”
- [Holy grail: The Mac IIfx](http://chrislawson.net/writing/macdaniel/2k0606cl.shtml), Chris Lawson, 2000.06.06
- [Games for ‘030s](http://lowendmac.com/gaming/2k0526.html), Brian Rumsey, Low End Mac Gaming, 2000.05.26. A look at games that run nicely on the old 68030-based Macs.
- [Troubleshooting My Mac IIfx](http://lowendmac.com/macinschool/2k0410.html), Steve Wood, View From the Classroom, 2000.04.10. The trials and joys of bringing a Mac IIfx back to life.
- Apple Macintosh IIfx, Justin Mayrand
- [Mac IIfx](http://www.mathdittos2.com/columns/bh/bh990511.html), Steve Wood, Busman’s Holiday, 1999.05.11
- [Macintosh IIfx: The Inside Story](http://developer.apple.com/technotes/hw/hw_09.html), Apple Developer Technotes, 1990.04
- [Why Should I Choose System 6 for the Mac II Family?](http://lowendmac.com/1999/why-should-i-choose-system-6-for-the-mac-ii-family/), Manuel Mejia, Mac Daniel, 1999.12.13. If they can use System 7, why use System 6?
- [System 6 for the Macintosh](http://web.archive.org/web/20000524123352/http://home.wanadoo.nl/ruud.dingemans/html/system6.html), Ruud Dingemans. If you have an older, slower, memory-limited Mac, System 6 is fast, stable, and still very usable.
- [Easter Eggs](http://www.mackido.com/EasterEggs/HW-IIfx.html), MacKiDo
- Information on [32-bit addressing](http://lowendmac.com/2015/32-bit-addressing-on-older-macs/)
- Email lists: [Classic Macs Digest](http://lowendmac.com/lists/classicmacs.shtml), [Vintage Macs](http://lowendmac.com/1998/low-end-macs-vintage-macs-group/)
- [System6](http://lowendmac.com/lists/system6.html), the email list for those who choose to use System 6.0.x.
- [Memory upgrade guide](http://lowendmac.com/2016/memory-upgrades-mac-iifx/)
- [Links to System 6.0.8 and 7.0.1](http://lowendmac.com/2013/classic-mac-os-downloads-and-updates/)
- [Macintosh IIfx Technical Specifications](http://docs.info.apple.com/article.html?artnum=112175), Apple Knowledge Base Archive

### Cautions

- Serial port normally restricted to 57.6 kbps; throughput with a 56k modem may be limited. See [56k modem page](http://lowendmac.com/2015/the-hype-about-56k-modems/#serial). For more information on Mac serial ports, read [Macintosh Serial Throughput](http://lowendmac.com/1998/macintosh-serial-throughput/) on the [Online Tech Journal](http://lowendmac.com/tech/index.shtml).
- Apple discontinued support and parts orders for the IIfx on 1998.08.31. You may be able to find dealers with parts inventory either locally or on our [parts and service list](http://lowendmac.com/dealers/service.shtml).

Keywords: #maciifx #macintoshiifx

Short link: http://goo.gl/FyVGJV

*searchword: maciifx, macintoshiifx*