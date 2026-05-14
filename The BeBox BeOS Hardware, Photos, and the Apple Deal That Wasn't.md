---
title: "The BeBox: BeOS Hardware, Photos, and the Apple Deal That Wasn't"
source: "https://www.jdhodges.com/blog/bebox-beautifully-overbuilt-computer/"
author:
  - "[[J.D. H.]]"
published: 2026-05-08
created: 2026-05-13
description: "Original 2000 BeBox photos, Be Inc. specs, GeekPort details, BeOS R5 history, the Apple/NeXT 1996 deal, Power Computing, and final eBay sale records."
tags:
  - "brain_spew"
---
Late 2000. There is a grey and blue tower PC on my dorm-room desk like nothing anybody who walks into the room has ever seen. **The Be logo on the front, a 3.5″ floppy peeking out the bottom of the drive bays, and the vertical grille that hides two columns of green LEDs (blinkenlights) dancing with the CPU load.** I paid $400 for it in two installments of $200 to a guy named Danan, about $745 inflation-adjusted to 2026. That amount of money felt like a lot for a college kid, and a true bargain for a dual-PowerPC workstation running an operating system you didn’t see in the wild.

I booted BeOS off the Fujitsu drive and it was like a dream. Programs opened immediately. Everything just clicked. The file system, which Be called BFS, was already doing things no other desktop OS in 2000 could match: *indexing every file’s attributes into a queryable database, journaling every write, treating the file manager like a live database query*. I was just starting to really get into relational database and to see an OS that had it right from the factory was a bit mind blowing! It was a truly forward-looking OS with features WAY ahead of its time. In some ways I still prefer it to modern OSes (cough cough Windows) which are worse organized and so bloated that an 8-core CPU can still feel like not enough.

The BeBox was not a better Mac. It was Be Inc.’s argument that personal computers had become timid. By the time I owned one, Be had stopped building hardware, lost a price negotiation to Apple by tens of millions of dollars, and watched the Power Computing Mac-clone bundling path collapse after Steve Jobs returned and Apple ended clone licensing. This is the story of how Be made a workstation that overengineered every detail, an OS that was right about almost everything except apps, and a price negotiation that changed who built the Mac OS we got.

*(This trip down memory lane all came to be because of the MacBook Neo and how it reminded me in some ways of the BeBox when it comes to uniqueness and responsiveness despite minimal memory specs. For more, see [The MacBook Neo Deep Dive](https://www.jdhodges.com/blog/macbook-neo-benchmarks-analysis/). Everything is as accurate as I can remember and research, but feel free to chime comment if you see anything that can be improved!)*

## A Quick Story of How I Got Mine

![BeBox tower front view showing Be logo, three optical/floppy drives, and Blinkenlights LED vent](https://www.jdhodges.com/wp-content/uploads/2026/04/macbook-neo-bebox-front-be-logo.jpg)

My BeBox in late 2000. Beneath the iconic Be logo: a CD-ROM, a Philips OmniWriter CD-RW, a 3.5″ floppy, and the vertical-vent grille that hides the dual-CPU LED Blinkenlights on the front bezel. I LOVED THOSE LIGHTS 😍

I bought my BeBox secondhand from a guy named Danan. First $200 check on November 22, 1999. Final $200 on April 28, 2000. Two installments over five months, total $400, both transactions still living in my Quicken file from that era. I was a CS-then-CIS undergrad who had been running BeOS on commodity x86 hardware after a Best Buy run earlier that fall (the BeOS / Win98 SE bundle), with Partition Magic 4 to keep the dual-boot honest. I’d also briefly tried OS/2 Warp around the same era, never as a daily driver. The PowerPC port had been the original BeOS, though, and a real BeBox was the original BeBox, and at $400 it was the cheapest path to one I was ever going to find.

The photos in this post are from December 2000. By then I’d had it about a year. The 53C810 SCSI chain inside the case held a Fujitsu hard drive, an NEC CD-ROM, and a Philips OmniWriter CD-RW. The OmniWriter was a small luxury that BeOS handled cleanly even though the application ecosystem around it was thin. The eBay listing I would later create when I sold the BeBox confirms the model: a 133 MHz BeBox, the higher-clocked of Be’s two SKUs (Be’s own spec page calls it the Dual603e, released August 1996 at $2,995, about $6,150 inflation-adjusted to 2025). The RAM I am not 100% sure on, since the bottom-of-case sticker isn’t in any photo I still have, and I can’t remember.

What I remember is the file system. What I remember is MP3s playing while a video also played while a window I had not asked to open animated open exactly when I asked it to. The OS was elegant. The software ecosystem, even by 2000, was thin. I still think about it.

![Sealed cardboard shipping box for the BeBox on arrival day in late 1999](https://www.jdhodges.com/wp-content/uploads/2026/04/bebox-shipping-box.jpg)

The day it arrived. Cardboard box, no Be branding on the outside, just the sense that something interesting was inside.

## “One Processor Per Person Is Not Enough”

![be.com homepage from December 18, 1996, showing the One processor per person is not enough slogan and Power Computing licensing banner](https://www.jdhodges.com/wp-content/uploads/2026/04/bebox-1996-be-com-homepage.png)

Be.com homepage, December 18, 1996, captured by the Wayback Machine. The slogan is the company in seven words.

That was the slogan on Be’s homepage in December 1996, and it tells you most of what you need to know about how Be Inc. saw the world. Single-threaded operating systems were already feeling the strain by the mid-1990s. Multimedia was the consumer-facing buzzword and what it meant in practice was that PCs were being asked to play audio while drawing video while servicing user interaction while running a file manager and an email client in the background, all on top of operating systems whose ancestors had been written for one user doing one thing.

Dual-CPU was rare in 1995. I had done it with my first build, a homebuild with Tyan mobo and dual Intel Pentium II 233MHz CPUs and a SCSI HDD. That’s normally what you had to do if you wanted two processors… you needed a server-class motherboard and two physical sockets, a configuration most consumers had never seen and most workstation buyers paid through the nose for. The BeBox put two on the logic board by default, soldered down, in a midrange tower aimed at developers and content creators rather than at server racks. And it bet on PowerPC, the RISC architecture that was supposed to (eventually, maybe) end Intel’s dominance.

Be’s response to single-threaded sluggishness was to build the OS around threads from the kernel up, target a hardware platform with multiple processors out of the box, and let the dual-CPU dance be the visible promise. The Blinkenlights on the front of the BeBox, two columns of green LEDs, one per processor, behind that vertical-vent grille, were the marketing department’s gift to the engineers. Both columns blink under load, people walking past your desk ask why your computer has light-up gauges, and you get to explain that it’s a dual-PowerPC machine running an OS that is multithreaded from the kernel to the GUI. That is a long sentence to put on a marketing card. The slogan does it in seven words.

## What Be Inc. Was

Be, Inc. was founded in October 1990 by Jean-Louis Gassée and Steve Sakoman, initially in San Jose and soon at the company’s longstanding Menlo Park, California address. The seed money came from Seymour Cray, which is a sentence you don’t often write about a desktop computer company.

Gassée had been head of Apple France, then president of Apple’s product development division, before falling out with John Sculley in 1990. Sakoman had run Apple’s Newton division and grown frustrated with Apple’s RISC-vs-CISC indecision. The pair founded Be Inc. (originally Be Labs) with the explicit goal of doing the OS rewrite they thought Apple would not do.

The first prototypes used dual AT&T Hobbit CPUs alongside three AT&T DSP3210 digital signal processors for media work, an unusually parallel design that anticipated Be’s later obsession with multithreading but ran into the inevitable problem that AT&T discontinued the Hobbit. Be regrouped on PowerPC. The first BeBox shipped on October 3, 1995, two years after the public reveal of the company’s general direction at the 1993 Microprocessor Forum.

Hardware engineering was led by Joseph Palmer. The OS-side roster included Erich Ringewald on the kernel, Jon Watte on the Media Kit, Benoit Schillings on the audio mixer demos that became a Be calling card, Pierre Raynaud-Richard on the window server and the `BDirectWindow` API, and Dominic Giampaolo with Cyril Meurillon on BFS (Giampaolo later wrote the book on it). Intel eventually took a 10% stake after BeOS was ported to x86. By 1996 the company had a hardware product, an OS that early reviewers were taking seriously, a small but loud press following, and Gassée’s growing conviction that BeOS belonged on every desktop that mattered.

## The BeBox Hardware: Specs and Surprises

The BeBox shipped as a midrange tower with workstation-grade ambitions. Be’s own engineering documentation on its [archived spec page](https://web.archive.org/web/19970218175614/http://www.be.com/products/bebox/dual603spec.html) reads less like marketing collateral and more like a checklist of small choices that someone clearly cared about: scatter-gather DMA channels assigned by intended use, A/D converters wired to the joystick ports for “superior resolution,” a 37-pin connector picked specifically because *“the pin spacing is large enough for inexperienced assemblers to solder connections.”* A lot of computers from 1995 do not document themselves like that.

### Dual603 vs Dual603e

Be shipped two variants. The first BeBox, the Dual603, was announced in October 1995 with two PowerPC 603 chips clocked at 66 MHz. The second, the Dual603e, arrived in August 1996 with two 603e chips clocked at 133 MHz. Both processors were soldered directly to the logic board; there were no sockets, and there was no field upgrade path. If you wanted faster CPUs, you bought a different machine.

<table><thead><tr><th></th><th>Dual603</th><th>Dual603e</th></tr></thead><tbody><tr><td><strong>Released</strong></td><td>October 3, 1995</td><td>August 5, 1996</td></tr><tr><td><strong>CPU clock</strong></td><td>66 MHz</td><td>133 MHz</td></tr><tr><td><strong>Launch price (USD)</strong></td><td>$1,600</td><td>$2,995</td></tr><tr><td><strong>2025 inflation-adjusted</strong></td><td>≈$3,380</td><td>≈$6,150</td></tr><tr><td><strong>Units shipped</strong></td><td>≈1,000</td><td>≈800</td></tr><tr><td><strong>Processor bus</strong></td><td colspan="2">33 MHz, 64-bit data, 32-bit address, big-endian</td></tr></tbody></table>

Sources: CPU clocks and processor bus from [Be’s Dual603 spec page](https://web.archive.org/web/19970218175614/http://www.be.com/products/bebox/dual603spec.html); release dates, prices, and unit counts from [Wikipedia (BeBox)](https://en.wikipedia.org/wiki/BeBox) and Be marketing materials of the era; 2025 inflation figures from CPI conversion.

Total production landed somewhere around 1,800 units before the BeBox was discontinued in January 1997, when Be ported BeOS to the Power Macintosh and pivoted to a software-only company. Prototypes of dual-200 MHz and quad-CPU configurations existed but never shipped.

### The Memory Controller, the ISA Bridge, and the Slot Mix

Memory and PCI duties were handled by Motorola’s MPC105, a chip Be’s documentation refers to by its “Eagle” code name. The MPC105 sat between the 33 MHz processor bus and a 33 MHz PCI bus, and on the ISA side an Intel 82378 bridge handled seven scatter-gather DMA channels. Be assigned those DMA channels by purpose: floppy on Channel 2, parallel on Channel 3, IDE on Channel 5, audio capture on Channel 6, audio playback on Channel 7. That kind of explicit allocation was a Be habit; the spec page is full of small decisions that an engineer wanted to be on the record about.

Memory layout was up to 8 banks of RAM in 4 socket pairs (SIMMs in pairs to fill the 64-bit data path), parity or non-parity 72-pin, 60 nS or faster fast-page-mode. Be’s spec page lists supported sizes as 1, 2, 4, 8, 16, 32, and 128 MB SIMMs (with no mention of 64 MB), while secondary summaries give 256 MB as the practical ceiling. I don’t have a source that reconciles the mismatch, and I’m not going to invent one. A 128 KB single flash ROM held firmware, with the first sector write-protected so a corrupted update could still boot a recovery from floppy.

The slot mix was unusual. Three PCI slots, all 5V, all bus-master capable, all full-length, with 3.3V also supplied. Five ISA slots. The 3+5 split reads as transitional: PCI for new cards, ISA for legacy and lab hardware. Be was clearly expecting its early customers to bring expansion cards from previous machines and hand-rolled hardware into the box, and Be wanted to make that easy.

### The GeekPort

![BeBox back panel close-up showing the GeekPort 37-pin D-shell connector, serial ports, MIDI DIN, and RCA audio jacks](https://www.jdhodges.com/wp-content/uploads/2026/04/bebox-back-panel-geekport.jpg)

The back of my BeBox in December 2000. The wide 37-pin D-shell at center-left is the GeekPort, with a peripheral plugged in. To its left, the four 9-pin serial ports. Below, the RCA audio jacks for line in and line out. The MIDI DIN connectors live to the right of the GeekPort. This is a 1995 personal computer designed for people who wanted to wire things to it.

This is the part nobody who used a BeBox forgets. On the back of the chassis, alongside the four serial ports and the audio RCA jacks, sat a 37-pin female D-shell connector that Be’s own spec page calls “ *a new feature connector unique to the BeBox.*” Be called it the GeekPort, treated it as a trademark in every product footer of the era, and made it real:

| GeekPort feature | Detail |
| --- | --- |
| Connector | 37-pin female D-shell |
| Digital I/O | 2 × 8-bit ports, each independently configurable as input-only or output-with-readback (16 in / 8+8 / 16 out); shorted-to-power/ground protected |
| A/D conversion | 4 pins routed to a 12-bit A/D converter; analog signal ground reference; protected |
| D/A conversion | 4 pins, each on an independent 8-bit D/A converter; analog signal ground reference; protected |
| Power | 2 × +5V, 1 × +12V, 1 × −12V, 7 ground pins; shell at chassis ground |
| Protection | Three fuses on the main processor board |
| Bus | ISA, addressable from the CPU, a PCI bus-master card, or an ISA bus-master card |

The use cases were what you would imagine. Sample a temperature sensor, control a stepper driver, drive a relay board, talk to a logic analyzer you built on a breadboard. Be’s pitch was that the GeekPort would let “experimenters and small entrepreneurs… bring unique functions to the BeBox” without adding a PCI card, opening the case, or buying a digital I/O board from National Instruments. For 1995 that was an unusually generous architectural decision.

The reasoning for the 37-pin choice is worth quoting at length, because it is one of the more charming pieces of engineering documentation from the era:

> “37 Pins allows for plenty of signal pins and adequate power and grounds. The connector is listed in most electronics catalogs, and is available in most shops that cater to the experimenter. The shell of the connector is rugged, and the pin spacing is large enough for inexperienced assemblers to solder connections to the pins…
> 
> “This connector is not commonly used on PCs so the risk of plugging an incompatible device into the connector is greatly reduced…The power connections have specifically been grouped to the center of the connector to help prevent the accidental shorting between the power pins of the GeekPort to external cables and devices.”
> 
> [Be Inc., BeBox Dual603 Technical Specifications](https://web.archive.org/web/19970218175614/http://www.be.com/products/bebox/dual603spec.html)

“Inexperienced assemblers” is a tell. Be was selling a workstation, but it was openly designing for the hobbyist sitting at a kitchen table soldering wires to D-shell pins. That energy is not on the back of any modern desktop PC.

### Blinkenlights and Industrial Design

Hardware engineering at Be was led by Joseph Palmer. The case is 39.8 cm tall, 21.0 cm wide, and 46.1 cm deep, in a blue-gray two-tone with a matte plastic bezel. The PSU is rated for 100-240V AC single-phase.

The signature feature, though, is the two vertical columns of yellow-green LEDs visible through the slatted vent grille on the front. One column tracks the load on each CPU in real time, lighting more LEDs as utilization climbs and fewer as it falls; the bottommost LED on the right column doubles as a hard-disk activity indicator. People who used a BeBox call those LEDs the Blinkenlights, and owners remember them: when you ran a parallel build or kicked off a video render and watched both columns climb together, you understood viscerally what symmetric multiprocessing meant in a way that no Task Manager screenshot ever taught a Windows user. Three decades later, every PC and laptop should still have them.

### The Full I/O Panel

The back of the BeBox was unusual. Below is the abbreviated inventory; the expanded version is on Be’s own [spec page](https://web.archive.org/web/19970218175614/http://www.be.com/products/bebox/dual603spec.html).

| Port | Count | Detail |
| --- | --- | --- |
| PCI slots | 3 | 33 MHz, 32-bit, 5V (3.3V also supplied), full-length, all bus-master |
| ISA slots | 5 | via Intel 82378 bridge with 7 scatter-gather DMA channels |
| SCSI | 1 internal + 1 external | `NCR 53C810` Fast/narrow SCSI II, bus-mastering, 50-pin connectors with switchable terminators |
| IDE | 1 | standard, ISA DMA Ch. 5 |
| Floppy | 1 | 3.5″ MFM, 720 K and 1.44 M, 34-pin ribbon |
| Serial | 4 | 9-pin AT-style, 16550-compatible UARTs (16-byte FIFO). Serial 1+2 ISA/PREP-compliant; 3+4 clocked at MIDI-compatible frequency |
| Parallel | 1 | bidirectional, 25-pin AT-standard, configurable DMA + interrupt |
| MIDI DIN | 4 | 2 MIDI channels, each with its own FIFO UART, 5-pin DIN in+out per channel, opto-isolated input |
| Game ports | 2 | 15-pin D-shell, x-y data sampled by an A/D converter for higher resolution than standard PC joystick ports |
| Infrared | 3 | each programmable as a learning remote receiver or for command detection |
| GeekPort | 1 | 37-pin D-shell, see above |
| Audio | line in, mic, CD-in header, headphone, line out, internal speaker | 16-bit stereo CODEC, 44.1 / 48 kHz |
| Keyboard | 1 | 5-pin AT-DIN; PC-standard 8042 controller |
| Mouse | 1 | 6-pin mini-DIN (PS/2-style), located on I/O card |

“ *The BeBox does not come with a keyboard or mouse,*” Be’s spec page notes flatly, “ *allowing customers to purchase the industry-standard models they prefer.*” That is a sentence written by people who knew their customer.

![BeBox back panel wider view showing AC inlet, cooling fan, expansion slot bay, and the row of metal slot covers](https://www.jdhodges.com/wp-content/uploads/2026/04/bebox-back-panel-wider.jpg)

Wider view of the back panel: AC inlet at top, cooling fan in the middle, and the row of metal expansion slot covers at the bottom. Three PCI plus five ISA slots was an unusually generous mix for 1995.

## BeOS: Why It Felt So Fast

The hardware was the cool half. The OS was the radical half.

BeOS was built around the assumption that everything in the system could and should be threaded. Scot Hacker, author of [The BeOS Bible](https://birdhouse.org/beos/bible/) (with Henry Bortman and Chris Herborth; Peachpit Press, 1999), put it like this in his [BYTE column](https://birdhouse.org/beos/byte/29-10000ft/):

> “BeOS is multithreaded from the lowest levels to the highest, from the kernel to the filesystem to the GUI.”
> 
> Scot Hacker, BYTE

What that meant in practice was that the OS architecture refused to assume any one task should block any other. Every window got its own thread. The graphics engine was multithreaded. The kernel had cheap, preemptive threads, and Be’s public messaging API, the `BMessage` / `BHandler` / `BLooper` / `BMessenger` classes documented in the BeBook, gave application code a clean way to push UI work onto those threads instead of starving the main loop. On a dual-CPU machine you got the additional payoff of the second CPU being able to do something useful while the first was still waiting on disk. The Blinkenlights showed you both columns climbing in symmetric multiprocessing while the GUI stayed responsive.

### BFS: the file system that quietly was a database

The Be File System was developed by Dominic Giampaolo with Cyril Meurillon, debuted in BeOS in 1997, and later got its own book: Giampaolo’s *Practical File System Design with the Be File System* (Morgan Kaufmann, 1999). BFS was a 64-bit-capable journaled filesystem designed for the large media files Be’s customer base actually worked with, but the part that made BFS feel different from every other file system on the market was its indexed extended attributes.

Tracker, the BeOS file manager, treated the filesystem as a queryable store. An MP3 player could mirror a song’s artist/title/album metadata into BFS attributes; an email or address-book app could store each record as its own zero-byte file with indexed attributes for sender, subject, name; and a query like *“all files where artist=Aphex Twin”* returned matches in milliseconds. It was not SQL. It was an indexed attribute query against the live filesystem, run by the kernel, exposed to the GUI. For users it operated like a database that happened to also be where their files lived. When I sat down to draft the personal section of this post and tried to summarize what I remembered most about BeOS, the file system was the first thing I named. That sentiment was common in 2000, and it has not gotten any less correct since.

### The Media Kit and the audio-pro audience

The Media Kit was the API layer that mattered most for Be’s actual customer base. Audio professionals, video editors, MIDI hobbyists, anybody whose work was rate-limited by their OS rather than by their imagination. The famous BeOS trade-show demos were always media-heavy: multiple video files playing at once on multiple windows, multi-track audio mixing live without dropouts, MIDI sequencers running alongside playback. Media Kit architecture is most associated with Jon Watte, who explicitly took the lead role at Be Developer Conferences, with adjacent credits to Schillings (audio mixer demos) and Raynaud-Richard (graphics and `BDirectWindow`), and the kernel and filesystem work behind it from Ringewald, Giampaolo, and Meurillon. Together they had built a system that could carry a half-dozen real-time audio streams without coughing. Windows 98 could do this only fragilely; Mac OS 8, with cooperative app multitasking and no protected memory, was structurally bad at it.

### Boot time and the responsiveness budget

A clean BeOS boot, from POST to login, was famously short. I am not going to put a number on it because the number depended on the SCSI chain and the configuration, but it was short enough to feel comedic if you were coming from a Windows NT 4 workstation where rebooting often felt like coffee time. The more important claim was that the responsiveness budget held under load. Open a window while a video plays while a parallel build runs while you are dragging an icon, and BeOS did not stutter, because UI work was already split across loopers and threads across both available CPUs. That was an unusual claim about a 1996 desktop OS, and BeOS earned it.

## BeOS Version Timeline

BeOS shipped in stages, each one labeled with Be’s distinctive nomenclature. The early **DR** (“Developer Release”) versions were PowerPC-only on the BeBox. **R3** in March 1998 was the first commercial release that also shipped on x86. **R5** in March 2000 was the last Be-branded release, splitting into a free **Personal Edition** for x86 hosts and a paid **Pro Edition** with PowerPC support. There is no DR9. Common confusion, but the jump went from DR8 directly to R3.

| Version | Date | Platforms | Notable |
| --- | --- | --- | --- |
| DR5 | Oct 1995 | PowerPC (BeBox) | Initial release, ships with the BeBox |
| DR6 | Jan 1996 | PowerPC | First officially distributed version |
| DR7 | Apr 1996 | PowerPC | 32-bit color, virtual desktops, FTP server |
| DR8 | Sep 1996 | PowerPC | MPEG / QuickTime, OpenGL |
| R3 | Mar 1998 | PowerPC + x86 | First commercial release with x86 port |
| R4 | Nov 4, 1998 | PowerPC + x86 | Claimed 30% performance improvement |
| R4.5 (“Genki”) | 1999 | PowerPC + x86 | Broader hardware support |
| R5 (“Maui”) | Mar 28, 2000 | PowerPC + x86 | Pro / Personal split; Personal Edition is x86-only and free |
| R5.0.3 | May 26, 2000 | PowerPC + x86 | Final official release |
| R5.1 (“Dano”) | Leaked post-2001 | x86 | Internal build with the BONE networking stack; never officially released |

Source: [Wikipedia: BeOS](https://en.wikipedia.org/wiki/BeOS), version-history table.

## The Apple Deal That Didn’t Happen

This is the most-told story in BeOS lore, and getting the dates right matters because the standard internet retelling muddles them.

In 1996, Apple was hunting for a modern OS to replace the aging classic Mac OS, and CEO Gil Amelio invited back-to-back presentations from NeXT and Be on **December 10, 1996**, with NeXT presenting first. The numbers traded across the table that month do not fully agree across secondary sources. Wikipedia says Gassée wanted $300 million while Apple offered $125 million; other accounts report Apple unwilling to go above $200 million while Gassée demanded $275 million. The gap was tens of millions of dollars either way, the negotiation had a tone problem, and Amelio later wrote that he found Gassée dismissive. Apple chose NeXT.

The acquisition timeline is what gets muddled. Apple announced its intent to acquire NeXT on **December 20, 1996**, in a press release that named Jobs as returning to Apple, reporting to Amelio. The deal value was announced at approximately $400 million; Apple’s later 10-K accounted for the final price at about $427 million; the figure $429 million is the most widely repeated rounding in the secondary literature. Closing followed in early 1997. **January 7, 1997** is the date that often gets reported as the “acquisition” because that was Macworld Expo San Francisco, where Amelio and Jobs took the stage together to discuss what would become Rhapsody and, eventually, Mac OS X. The Mac OS X you used or are using right now is built on the NeXTSTEP code base; it is not built on BeOS.

**Note** Imagine the universe where the price negotiation went the other way. Apple ships a 1998 OS based on BeOS instead of NeXTSTEP. The native framework is Be’s C++ kits, with a Carbon/Blue-Box-style compatibility path for existing Mac apps. Mail.app is built on BFS attributes instead of mbox files. Spotlight is just `query()`. The iPod’s media playback inherits the Media Kit. iOS, when it arrives a decade later, is a BeOS descendant rather than a NeXT descendant. None of this happened, and we cannot know if BeOS would have scaled to ten million developers or stalled before Mac OS 9’s discontinuation. But it is impossible to read Be’s spec sheet now without imagining it.

The Be side of the negotiation has its own postmortem worth knowing about. BeOS was promising but less mature as a mass-market Mac replacement than OPENSTEP. NeXT had a working desktop OS that real customers were already shipping software on; Be had a beautiful, technically aggressive system whose first commercial Intel/x86 release would not arrive until R3 in March 1998, with broader consumer reach via R4 (November 1998) and R4.5 (1999). The price gap was the easy part of the story. The maturity gap was the hard part.

## The Power Computing Deal That Almost Was

Weeks before Apple chose NeXT, Be had been quietly assembling a different go-to-market plan. On **November 26, 1996**, Be Inc. and Power Computing Corporation announced a licensing deal that would bundle BeOS on Power Computing’s PowerPC Macintosh clones starting Q1 1997. Power Computing was the largest and most aggressive of the Mac clone vendors at the time, shipping the PowerTower Pro, PowerTower, PowerCenter, and PowerBase lines.

The press release is worth quoting because it captures the moment before the moment everything changed. From Steve Kahng, Chairman and CEO of Power Computing:

> “Power Computing has earned a strong reputation by providing leading-edge PowerPC systems to meet the needs of today’s growing digital media market. With the addition of the BeOS to our offering, Power Computing customers will now have the option of utilizing the remarkable power and performance of the BeOS along with Power Computing’s already world-class systems.”
> 
> Steve Kahng, Chairman and CEO, Power Computing Corporation

From Jean-Louis Gassée, CEO of Be, Inc.:

> “Power Computing is an ideal partner because we are after customers that are pushing the envelope in media and content creation and Power Computing is the company that is pushing the envelope in PowerPC system design. Power Computing has moved to the forefront of the PowerPC system space, and we’re excited to work with them.”
> 
> Jean-Louis Gassée, CEO, Be, Inc.
> 
> Source: [Be Inc. press release, November 26, 1996](https://web.archive.org/web/19970218183919/http://www.be.com/aboutbe/pressreleases/96-11-26_BePower.html) (Wayback Machine).

The mechanics: BeOS would ship as a bootable CD-ROM at no additional charge alongside Mac OS. The first public BeOS demo on a Power Computing system had already happened at Macworld Boston in August 1996. Existing Power Computing owners would be able to buy BeOS directly from Be. The full launch was set for Macworld Expo San Francisco in January 1997.

Then Apple announced the NeXT acquisition on December 20, 1996. January brought Macworld San Francisco, Rhapsody on stage, and the shutdown of Be’s own hardware program, with the BeBox discontinued in January 1997. Power Computing’s Mac clone business continued for several months, but Steve Jobs’s return to Apple changed the strategic calculus around clone licensing fast. On **September 2, 1997**, Apple announced it was buying Power Computing’s customer database, Mac OS distribution license, and the right to retain key Power Computing employees, in a deal initially valued at roughly $100 million in Apple stock; the agreement closed on January 28, 1998 at approximately $110 million ($80M stock, $28M receivables forgiveness, $2M support-liability assumption). The clone era effectively ended there. The BeOS bundling never reached the volume the November press release was selling. Be was, suddenly, without the mass-market hardware path it had been counting on, and without an Apple deal, all at once.

## The R5 Era and the Personal Edition Bet

By the end of 1999 Be had pivoted hard. The hardware was gone, the Apple deal was three years dead, the OEM bundling deal had survived only as a series of smaller arrangements with Hitachi (Flora Prius in Japan) and Fujitsu (Silverline in parts of Europe). The BeOS install base on x86 was passionate but small. So Be made an audacious bet: give the OS away.

On **February 28, 2000**, Be opened `free.be.com` and made **BeOS 5 Personal Edition** available as a free 48-MB download. The trick was the install model: the download decompressed to a fixed 500-MB raw disk image (called a “hardfile”) that lived inside an existing Windows or Linux partition. Boot loaders on Windows 9x and DOS could redirect to the hardfile at startup, or you could boot from a free floppy. No repartitioning. No risk to the host install. The friction of “try a new OS” had been brought as close to zero as anyone in 2000 had managed. By Be’s accounting the Personal Edition exceeded one million downloads.

Personal Edition was, importantly, **x86 only**. The BeOS that ran on a BeBox was the PowerPC build of **R5** (“Maui”), released March 28, 2000 in the same Q1 cycle as PE, sold via Gobe Software in a Pro Edition that included PowerPC support. (I bought the 5.0 Pro Edition Upgrade direct from Gobe on August 26, 2000 for $34.95 plus $5.95 shipping, total $40.90, the receipt is in my email archive from that era.)

![BeOS R5 SCSIProbe screenshot showing Be Incorporated SCSI HBA, Fujitsu disk, NEC CD-ROM, Philips OmniWriter CD-RW, and BEBOX device](https://www.jdhodges.com/wp-content/uploads/2026/04/macbook-neo-bebox-beos-trinitron-scsi.jpg)

SCSIProbe running on my BeBox under BeOS R5. The SCSI bus reports a Be Incorporated SIM on the standard NCR 53C810 controller (matching the architecture documented in Be’s original spec sheets), with a Fujitsu hard drive, an NEC CD-ROM, and a Philips OmniWriter CD-RW chained behind. The BEBOX R5 entry at ID 7 is the host adapter itself, which is the BeBox’s way of identifying itself on the bus under R5.

The Personal Edition bet had merit. It was a recognizable play: *try-before-you-buy, drive download volume, sell the Pro version to the converted, build developer momentum*. The momentum never quite arrived. The application ecosystem in 2000 was, the word I used in the personal section earlier, “thin.” NetPositive was the default BeOS web browser, with Opera shipping a BeOS port that I remember using too. MP3 players like SoundPlay and CL-Amp existed. Gobe Productive (a separate Gobe Software product from the BeOS Pro upgrade) served office-suite duty. Against the deluge of Windows software in 1999-2000 that was about as good as it got, and Be’s hardware partners had begun looking at internet appliances and set-top boxes as a more achievable path than the desktop.

## The Eventual Fall and the Microsoft Settlement

The pivot had a name: **BeIA** (“Be Internet Appliance”), a stripped-down BeOS targeted at set-top boxes, web pads, and the various other internet-appliance dreams that briefly looked credible in 1999-2001. The desktop OEM list before the pivot had included Motorola (StarMax), DayStar Digital, Hitachi (Flora Prius for the Japanese consumer market), and Fujitsu (Silverline in parts of Europe). Sony had been talked about. So had Compaq. Most of the deals shrunk or evaporated. The dot-com crash that arrived in 2000 took the internet-appliance category with it.

Be had IPO’d on Nasdaq under the ticker `BEOS` in July 1999 at the peak of the bubble. By August 2001 the company had to be sold. Palm Inc. announced the acquisition on **August 16, 2001**, with shareholders approving on **November 13, 2001**. The price was **$11 million**. Most of Palm’s interest was in BeOS engineering talent and the IP, not in continuing the BeOS desktop product. BeOS the consumer product effectively ended at the Palm sale.

The story has a coda. On **February 20, 2002**, Be Inc. (now a wind-down entity rather than an operating company) filed an antitrust complaint against Microsoft alleging Microsoft had pressured PC OEMs (specifically including Hitachi) to abandon Be products in favor of Windows-only configurations. The complaint relied heavily on the Justice Department’s then-recent antitrust findings against Microsoft. Rather than litigate, Microsoft **settled in September 2003 for $23.25 million**, with no admission of liability. The proceeds went to the Be wind-down estate and ultimately to former shareholders.

The IP traveled. Palm spun off PalmSource in 2003 to manage the OS assets; Japanese mobile-software company **ACCESS Co.** acquired PalmSource in 2005 and inherited the BeOS source tree. ACCESS’s interest was overwhelmingly in mobile platforms (Cobalt, NetFront), and BeOS as a public product was effectively retired. The codebase has not been open-sourced. What survived as a continuation of BeOS is a community recreation, not a code-line descent. That is its own story.

## BeOS vs. Windows 98 SE vs. Mac OS 8.6: Feature Matrix

Here is the comparison anybody who tried BeOS in 1999-2000 made in their head. Three desktop operating systems shipping at roughly the same time, on roughly the same kinds of hardware, aimed at roughly the same kinds of users. Two of the three are still talked about as historical artifacts and missed lessons; the third became Windows.

| Feature | BeOS R5 (2000) | Windows 98 SE (1999) | Mac OS 8.6 (1999) |
| --- | --- | --- | --- |
| Preemptive multitasking | Yes, kernel-level | For 32-bit apps; 16-bit apps cooperative | Cooperative only |
| Memory protection | Yes | Partial; 16-bit apps could crash the system | None; one bad app could halt the system |
| Symmetric multiprocessing | Yes, native | No (NT supported it; 9x did not) | No |
| Native pervasive threading | Yes, kernel to GUI | Available via Win32 API; not pervasive in shell | Limited |
| Filesystem | BFS, 64-bit, journaled, indexed attributes | FAT32 (default); NTFS available on NT only | HFS+ (extended), no journaling, no attribute indexing |
| Live filesystem queries | Yes, native | No | No (Sherlock searched, but did not query attributes) |
| Native multimedia | Media Kit; multi-stream video and audio held under multitasking load | DirectX; could stutter or drop frames when other apps were demanding | QuickTime; cooperative-multitasked, vulnerable to one badly-behaved app |
| Application ecosystem | Thin; small loyal community | Vast; the dominant desktop ecosystem | Strong in creative pro segments |
| Hardware support | Narrow at launch, broadened with R4.5 | Broad | Apple-only |

BeOS was ahead of Windows 98 SE and Mac OS 8.6 on most architectural axes (multitasking, memory protection, SMP, filesystem). It was behind on the only axis that ultimately won the desktop, which was application ecosystem. That is the story of BeOS in one row of a table.

The preemptive-multitasking row earns the most explanation, because it was the biggest day-to-day-responsiveness gap of all of them. In 2000, Microsoft had two Windows lines on different planets. **Windows 9x** (95/98/ME) preemptively scheduled 32-bit Win32 applications, but its 16-bit and legacy shared subsystems could still hang the foreground when a misbehaving program got into trouble. **Windows NT** (NT 4 Workstation) was fully preemptive with protected memory throughout, but it was sold to professionals and most home users never touched it. The consumer-side Windows move to the NT model was **Windows XP** in October 2001. Classic Mac OS did not get preemptive multitasking until **Mac OS X** arrived the same year (March 2001). BeOS had been preemptively multitasked from kernel to GUI since 1995, which is a five-to-six-year head start on consumer-desktop responsiveness over the legacy half of Win9x and over Mac OS classic. That is the technical reason a BeOS desktop felt instantly responsive and a Win98 SE or Mac OS 8 desktop could feel sticky, and it is the strongest case for the Apple counterfactual earlier in this post.

## Living Legacy in 2026: Haiku, Emulators, Hardware

BeOS the corporate product is dead. BeOS the spiritual project is in remarkably good shape.

The continuation is **Haiku**, an open-source operating system that began as **OpenBeOS** in 2001 under Michael Phipps and was renamed in 2004 to dodge a Palm trademark concern. The latest official release as of this writing is **R1/Beta 5**, dated **September 13, 2024** (build hrev57937). Haiku does what very few from-scratch reimplementations actually achieve: 32-bit Haiku targets binary compatibility with original BeOS R5 software, while 64-bit Haiku breaks the ABI but preserves the API. Supported architectures include IA-32, x86-64, RISC-V, with an ARM port in active development.

**Tip:** Want to try BeOS today without buying vintage hardware? Install [Haiku R1/Beta 5](https://www.haiku-os.org/). It’s free, open-source, and gives you the BeOS desktop, BFS, the indexed-attribute query model, the Tracker file manager, and a working Media Kit, all in active 2026 maintenance. The 32-bit x86 build of Haiku is the one with binary compatibility for original BeOS R5 software (a milestone Haiku reached in 2009), so if you find a copy of *Becasso* or *SoundPlay*, it will run on 32-bit Haiku. The 64-bit x86, RISC-V, and in-progress ARM builds break the BeOS ABI but keep the API.

[86Box](https://86box.net/) is a strong PC emulator that can boot BeOS x86 R3 and later in a virtual machine, and it is the closest reasonable approximation to “what was BeOS like in 1998 on commodity x86.” For the BeBox itself there is no good emulator in 2026. SheepShaver and PearPC emulate Power Macintosh hardware, not the BeBox’s specific firmware and chipset. If you want BeOS on a BeBox you have to find a real BeBox, and roughly 1,800 of them ever existed. Working units cost meaningful money on eBay when they appear. The [ZetaOS](https://en.wikipedia.org/wiki/ZetaOS) commercial fork from yellowTAB and later magnussoft, based on the leaked R5.1 (“Dano”) code, shipped from 2003 until ACCESS Co. disputed yellowTAB’s right to the codebase and the project ceased in 2007.

The community kept publishing. The [Be Newsletter](https://www.haiku-os.org/legacy-docs/benewsletter/Issue1-44.html) archive (Issues 1-44, 1995-1996) is on the Haiku site. The [BeOS Bible](https://birdhouse.org/beos/bible/) mirror at Scot Hacker’s birdhouse.org is still up. [BeBits](https://www.bebits.com/) historically aggregated BeOS software; the modern equivalent is [HaikuDepot](https://depot.haiku-os.org/).

## What BeOS Got Right That We’re Still Trying to Match

It is easy to write about a dead OS as a curio. The question worth asking is which of its bets aged well.

The architectural bet aged well. Pervasive multithreading from kernel to GUI, native SMP support, an indexed-attribute filesystem, a media subsystem that could survive multitasking under load. Most of those traits are now expected in any serious desktop or mobile OS. Mac OS X eventually got there via Mach + BSD + Cocoa. Linux got there via NPTL + ext4 + systemd in different combinations over years. Windows got there via the NT line, between Windows 2000 and Windows 11. BeOS got there in 1995, on hardware almost nobody bought.

The RISC bet aged well too, just slowly. PowerPC was the RISC architecture that was supposed to (eventually, maybe) end Intel’s dominance, and that argument played out for thirty years across Apple’s first PowerPC era (1994-2006), Apple’s Intel detour (2006-2020), and Apple Silicon’s return to RISC (ARM, 2020 onward). ARM is now everywhere, from data centers (AWS Graviton) to laptops (Apple Silicon, Snapdragon X Elite) to phones to embedded systems. PowerPC ceded the consumer desktop, but the architectural argument the BeBox shipped with in 1995 turned out to be correct on a thirty-year horizon.

What BeOS did not crack is the only thing that actually wins desktop OS wars: *a deep, self-sustaining application ecosystem*. Apps are the gravity well and foundation of success. Without enough of them, technical superiority is a research paper. With enough of them, technical inferiority can ride for two decades. BeOS in 1995-2001 was the cleanest possible demonstration of that asymmetry. I tried OS/2 Warp around the same era for some of the same reasons (preemptive multitasking, decent multithreading, a vocal community that knew it had a better answer than Windows 9x) and never made it to daily-driver status, for the same fundamental reason BeOS showed me. It is also why Haiku in 2026 still matters, in the same way OS/2 fans still matter, and Amiga fans still matter: *the people who used a thing that was technically right keep telling the story until somebody listens or notices*.

## And a Quick Story of How I Sold Mine

By late 2001 I was about to graduate, money was tight, and I needed cash. I listed the BeBox on eBay on November 26, 2001 (item #1302540562, “Classic 2x133Mhz BeBox FREEBonus + NO RESERVE”). Inquiries came in fast…

The selling rationale, in a reply to one prospective bidder:

> “I do like to run it because of the amazing scripting and multimedia capabilites BeOS has (still unmatched today IMHO.) \[…\] I’m graduating from school before too awful long though and am trying to save up some money. Hence I’m selling her.”
> 
> JD Hodges, email to a prospective buyer, November 28, 2001

The pitch, to another bidder asking what the BeBox was actually like to use in 2001 (a question worth taking seriously, since 1GHz consumer PCs were already shipping). The reply, in full:

> “I’ll be honest, compared to a 1GHz PC these machines are not speed demons, but they are very nice for music (MP3s etc.), web browsing, programming, and just being darn cool machines! (it’s the only computer I’ve owned that even girls “ooh and aww” at)”
> 
> JD Hodges, email to Tom Barnes, November 27, 2001

The winning bid came from Michael at Philips Research in Briarcliff Manor, New York. The math: $1,076 final price plus $43 shipping equals $1,119 total. I had bought the BeBox from Danan in installments for $400 in November 1999 / April 2000. I sold it for $1,076 two years later. Roughly 2.7x return on a vintage workstation, which is not why anybody buys a vintage workstation, but it was much appreciated at that point in my life.

She shipped via USPS Priority Mail around December 21-22, 2001. The package contained the BeBox, BeOS 4.5 and 5 Pro CDs, the BeOS Bible book (Hacker / Bortman / Herborth, Peachpit Press), an external Philips SCSI CD-R drive (with cable, no terminator), an internal NEC SCSI CD-ROM (installed in the chassis but not connected, with a note that the new owner would likely need to change SCSI IDs), and an internal Apple SCSI hard drive in the same state. The Apple hard drive replaced the Fujitsu I had been running in 2000, the one visible in the SCSIProbe screenshot earlier in this post; somewhere in the intervening year I had swapped drives. An MS serial mouse and two power cables completed the package. Day after Christmas was the expected delivery. I never heard from Michael again, which usually means it got there fine.

Even the buyer’s emails to me came signed with a quote from the BeGroovy discussion thread that captured the BeOS community of late 2001 in three lines:

> “Ihate PC’s!  
> – Yeah, Me too…they should all be thrown out of high windows.  
> – Maybe the Windows should be thrown out of all PC’s.”
> 
> Excerpt from BeGroovy Discussion Thread, used as an email signature by Michael Paine, late 2001

Do I regret selling my BeBox? Maybe just a bit, but overall I’m glad it went to someone that hopefully got some good use out of it. It was never a system that I did extensive school work on, or used for work-work, it was just something that I admired and appreciated even if it couldn’t be my daily driver.

My biggest attachment is to hardware that I’ve USED for tons of work or play, day after day. Sometimes I hold onto those. The BeBox wasn’t one of those but I am very happy I have these photos and the memories of the fun BeBox and BeOS… and that’s enough for me. 😊

## Resources

Primary sources I’d start with for going deeper:

- **Be Inc.’s archived materials** via the Wayback Machine: the [be.com homepage from December 1996](https://web.archive.org/web/19961218232510/http://www.be.com/), the [BeBox Dual603 Technical Specifications](https://web.archive.org/web/19970218175614/http://www.be.com/products/bebox/dual603spec.html) page, and the [November 26, 1996 Power Computing licensing press release](https://web.archive.org/web/19970218183919/http://www.be.com/aboutbe/pressreleases/96-11-26_BePower.html).
- **Wikipedia**: [BeBox](https://en.wikipedia.org/wiki/BeBox), [BeOS](https://en.wikipedia.org/wiki/BeOS), [Be Inc.](https://en.wikipedia.org/wiki/Be_Inc.), [Haiku](https://en.wikipedia.org/wiki/Haiku_\(operating_system\)).
- **Scot Hacker’s [BeOS Bible](https://birdhouse.org/beos/bible/)** mirror, plus the [BYTE column archive](https://birdhouse.org/beos/byte/29-10000ft/) at the same domain.
- **Hackaday**: [BeOS: The Alternate Universe’s Mac OS X](https://hackaday.com/2020/01/09/beos-the-alternate-universes-mac-os-x/) (January 2020), the best single retrospective I have read.
- **Haiku project**: [haiku-os.org](https://www.haiku-os.org/), plus the legacy [Be Newsletter archive](https://www.haiku-os.org/legacy-docs/benewsletter/Issue1-44.html).
- **Dominic Giampaolo**, *Practical File System Design with the Be File System* (Morgan Kaufmann, 1999).