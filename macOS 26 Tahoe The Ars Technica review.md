---
title: "macOS 26 Tahoe: The Ars Technica review"
source: "https://arstechnica.com/gadgets/2025/09/macos-26-tahoe-the-ars-technica-review/?utm_brand=ars&utm_mailing=Ars_Orbital_091725&bxid=5bdce29e24c17c3610eca679&cndid=47035322&hasha=52cbe55757d1771cd90780b4b16ca07e&hashb=a42d701e3281b0a14218f41eb8b7ba50ebd8a194&hashc=51312edeef233a5dda516e6876a0a1b94a92e34faef426067d81108e45e0678f&esrc="
author:
  - "[[Andrew Cunningham]]"
published: 2025-09-15
created: 2025-09-24
description: "Liquid Glass brings translucent sheen to the typical batch of iterative changes."
tags:
  - "clippings"
---
The last time Apple gave macOS a fresh design was in 2020's [macOS 11 Big Sur](https://arstechnica.com/gadgets/2020/11/macos-11-0-big-sur-the-ars-technica-review/).

That release was relatively light on new features and heavy on symbolism. Big Sur is also when Apple finally jettisoned the "10" in Mac OS X after two decades. More importantly, it was the first release installed on then-new Apple Silicon Macs, the culmination of a decade-plus of in-house chip design that began with [single-core, low-power iPhone and iPad chips](https://en.wikipedia.org/wiki/Apple_A4) and culminated in something [powerful enough for the Mac Pro](https://arstechnica.com/gadgets/2023/06/this-is-the-new-apple-silicon-mac-pro/).

Today's macOS 26 Tahoe release holds up a translucent, glassy mirror to the Big Sur update. It comes with an all-new look, one that further unifies Apple's design language across all its operating systems. And it even throws out the old version numbering system and introduces a new one.

But if Big Sur was the beginning of an era, Tahoe is the end of one. This will be the final release to support any Intel Macs at all—and it runs on just a bare handful of them, ending support for all Intel MacBook Airs and most other Intel Macs besides. Starting with next year's release, Apple will be able to start jettisoning all Intel code from macOS, including (eventually) the Rosetta translation technology that allows Apple Silicon Macs to run Intel code.

As we do every year, we'll look at, and underneath, the shiny surface of the new release. If you have an older Intel Mac that isn't supported, is there anything here that might make you want to upgrade? Is Liquid Glass disruptive or revelatory or just another layer of cosmetic polish on top of the Mac's familiar time-tested Macintosh interface? Let's dive in.

## System requirements and compatibility

Tahoe drops many 2018, 2019, and even 2020-vintage Intel Macs that could run last year's Sequoia, plus the late 2017 iMac Pro.

Here are the supported systems:

- All Apple Silicon MacBook Airs, MacBook Pros, iMacs, Mac minis, Mac Studios, and Mac Pros with an M1, M2, M3, or M4-series chip.
- 2019 16-inch MacBook Pro
- 2020 13-inch MacBook Pro with four Thunderbolt 3 ports (but *not* the version with two Thunderbolt ports)
- 2020 iMac
- 2019 Mac Pro

That support list is rough news for owners of a couple of early-2020 laptops or anybody who bought 2018's Mac mini toward the end of its life (Apple sold some configurations all the way through January 2023).

It's especially difficult this year to divine why Apple is dumping some Intel Macs and keeping others around; *in general,* Apple drops Macs that rely on older Intel-integrated GPUs like the UHD Graphics 630 or Iris Plus Graphics 615 or 645; the 16-inch MacBook Pro uses one, but it's at least backed up by a dedicated AMD Radeon chip. The 10th-generation Intel chip in the 13-inch MacBook Pro makes the cut, but the marginally slower iteration of the same hardware in the 2020 Intel MacBook Air does not.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/Apple_new-macbook-air-wallpaper-screen_03182020.jpg)

The early 2020 Intel MacBook Air is barely 5 years old, and its updates have already dried up. Credit: Apple

But whatever side of the line your Intel Mac falls on, at least we all have closure now—a publicly announced, predictable timeline for the end of Intel support. Macs running 2023's macOS 14 Sonoma get one more year of Safari and security updates; 2024's macOS 15 Sequoia gets two more years; and Tahoe's security updates will dry up in mid to late 2028. The full version of Rosetta 2, the Intel-to-Arm app translation layer that keeps most Intel apps running on Apple Silicon Macs, will go away in macOS 28 in late 2027, though Apple says some traces of it will remain after that to support older games.

Next year's macOS release will be the first to require Apple Silicon—but at that point, we'll hopefully get at least a handful of years where *no* Macs get dropped from the support list, something that hasn't happened (!).

### Other system requirements

Though the Apple Silicon-only era won't officially start until next year, there's a long list of new and old features that already only function on Apple Silicon Macs.

Anything that touches Apple Intelligence at all—from summarizing notifications to Image Playgrounds—wants an M1 chip or better. The nice thing is that these features will run on *any* Apple Silicon Macs, from an M1 with 8GB of RAM up through an M4 Max or M3 Ultra. But the list of things Intel Macs can't do is getting pretty long:

- Metal 4 and features that require it, including frame generation.
- Features under the Apple Intelligence umbrella:
	- Genmoji
	- Image Playgrounds
	- Notification summaries
	- Writing tools
	- Live translation in the Phone, FaceTime, and Messages apps
- Other features, including those from older macOS versions, that require Apple Silicon:
	- Running iOS/iPadOS apps
	- Spatial Audio in FaceTime when using AirPods
	- The 3D globe and more detailed renderings of cities in Apple Maps
	- On-device voice dictation, with no Internet connection required and no time limit
	- Portrait Mode in FaceTime
	- Live Captions transcriptions in FaceTime or any other app
	- "Reference mode," which lets you use a 12.9-inch M1 or M2 iPad Pro or any M4 iPad Pro "as a secondary reference display" in Sidecar mode
	- Inserting emoji using voice dictation
	- Game mode, which limits background tasks and reduces Bluetooth latency when enabled
	- High-performance mode in the Screen Sharing app
	- Getting rid of the "Hey" in "Hey Siri"
	- Running games built with the Game Porting Toolkit

## What isn’t ready for launch yet?

It has become common practice for Apple to announce features at WWDC that it doesn't plan to ship in the x.0 release of the software; those features usually hit somewhere in the x.1 to x.4 updates, at which point the current OS shifts into a lower-key, mostly maintenance mode as Apple's development efforts shift toward next year's version.

The big missing piece for Tahoe and Apple's other fall releases is the new "more personal Siri," a version of the voice assistant that Apple plans to make more capable by backing it up with a large language model that can work with content on your device or in your iCloud account. This feature was somewhat infamously promised as part of last year's release but got bumped back after development difficulties. Apple executives claim that underlying improvements to Apple Intelligence in macOS 26 and the other operating systems will make it possible to ship the new Siri this year.

Otherwise, it doesn't look like there's much in the "later this fall/coming next year" category for this year's releases. If Apple has decided to keep its focus on the ecosystem-wide aesthetic redesign and a long-awaited high-stakes Siri update for this particular update cycle, I can hardly blame them.

## Options (or lack thereof) for owners of unsupported Macs

Usually, we talk about what options Intel Mac owners have if their hardware is still in decent shape and they'd like to continue using it with different software, but we're getting to the point where Intel Mac owners are just running out of options.

In past years, Windows 10 has been a workable alternative to tossing functional hardware, and it's the only other operating system that Apple officially supported on the hardware, thanks to Apple's Boot Camp software and drivers. But Windows 10's security updates dry up in October of this year (or October 2026, if you [jump through the hoops to sign up for a year of extra patches](https://arstechnica.com/gadgets/2025/07/how-to-get-another-free-year-of-updates-for-your-windows-10-pc/)), which actually makes Windows 10 *worse* on many Intel Macs than just staying on macOS.

Windows 11 isn't officially supported on any Intel Mac, since Apple doesn't enable the built-in TPM 2.0 module in Intel's CPUs. But as of this writing, it's still possible to [install Windows 11 on unsupported hardware](https://arstechnica.com/gadgets/2024/10/how-to-upgrade-to-windows-11-whether-your-pc-is-supported-or-not/). Your experience with this should *mostly* be pretty good, as I've found on [the motley collection of 12- and 13-year-old PC hardware](https://arstechnica.com/gadgets/2024/10/what-i-learned-from-3-years-of-running-windows-11-on-unsupported-pcs/) that I've run it on.

But installing Microsoft's big yearly update patches is a pain, and it's one you'll have to endure if you want to keep getting those security updates. You'll deal with any instability caused by using Apple's aging Windows 10 drivers on a new OS, and the possibility that Microsoft could decide to change Windows' underlying hardware requirements in a way that makes it impossible to install. (This has already happened once—2024's big update quietly made it impossible to run Windows 11 on some late-'00s-into-early-2010s hardware that had been able to use the first few versions.)

You could find some refuge in one of the many flavors of Linux (Ubuntu, Fedora, ChromeOS Flex, and innumerable others), but you'll run into problems on newer Macs with Apple T2 chips. The T2 is used by macOS to handle all kinds of things that are handled by other chips in PCs—video encoding and decoding, disk encryption, storing TouchID fingerprints, enabling the webcam and trackpad, and as an SSD controller, to name a few.

For Linux distributions to be able to do all of these things with the T2, Apple would need to either open up access to it, or someone in the Linux community would need to reverse-engineer support for it. Neither of those things has happened. And given the age and relative obscurity of the T2 hardware, it doesn't seem enormously likely at this point.

Your best option may be the [OpenCore Legacy Patcher](https://dortania.github.io/OpenCore-Legacy-Patcher/) (OCLP) project, which uses a lot of community-driven "Hackintosh" tools to do for old Intel Macs what they do for generic Intel and AMD hardware: get the latest macOS running on hardware Apple doesn't support.

Each year, that task gets harder, as Apple strips more of the underlying Intel support files out of new macOS versions. A lot of what OCLP does is patch in files from older macOS versions to restore that missing hardware support, and the more stuff that goes missing, the higher the degree of difficulty. On [this year's list](https://github.com/dortania/OpenCore-Legacy-Patcher/issues/1167) of "challenges": Fusion Drive support, legacy graphics drivers, FileVault disk encryption support, drivers for older Wi-Fi, Bluetooth, and USB hardware, and support for both the Apple T1 and Apple T2 chips.

For the Apple T2, the challenge for OCLP is similar to the challenges for Linux: a lot of hardware features require it to work, and Apple hasn't documented it or opened it up so that anyone else can use it. The 2018 MacBook Air, the first T2-equipped model to be dropped, still doesn't work with last year's macOS Sequoia. The additional T2 models that Tahoe dumps will be similarly difficult to support.

The OCLP team claims to have made "some progress" on T2 support, but these Macs still won't boot Tahoe, and it may or may not ever become possible.

Many Intel Macs still have between one and three years of security update support left; for unsupported Macs, your best bet is probably to keep using your older but officially supported macOS version for as long as it's patched. You'll miss out on newer iCloud and iMessage features, but things will *mostly* continue to function as they currently do, and it can buy you time to put together money for a new machine (while buying the OCLP project time to try to add support for your Mac, if it's not already supported). Just know that you're getting to the point where staying up to date and patched is going to require newer hardware.

## Branding: What’s in a number?

The first thing to note about the branding of macOS 26 is the number itself. The jump from 15 to 26 isn't as jarring as five years ago, when we finally lost the "10" that had given Mac OS X part of its name for so many years. But it's still potentially confusing in the short term, even if in the long term I do think it makes more sense for an ecosystem as tightly integrated as Apple's to unify around consistent version numbers up and down the entire product stack.

As with new cars, the "26" here is year-based but forward-looking—it's numbered for the year where it will spend nine or so months as the actively developed, currently supported version of the operating system, and not for the year of its release.

On the technical side, just like with the jump from version 10.15 to 11.0, macOS 26 can identify itself as macOS 16 to apps and scripts that might otherwise be broken by the jump. [As detailed](https://eclecticlight.co/2025/06/13/is-tahoe-really-macos-26-or-16/) by the Eclectic Light Company's Howard Oakley, apps developed targeting macOS versions 15 or below will see "16," while apps developed targeting macOS 26 or newer will see "26." Different kinds of scripts have slightly different compatibility behaviors.

### What’s in a name?

Tahoe is Apple's 13th California-themed macOS codename, and while the company has stuck a couple of pins in the southern part of the state, the majority of the releases stick within a couple of hundred miles of Apple's Bay Area stomping grounds. Tahoe is one of those.

I am not a California native, but I usually take a little time to read about whatever landmark Apple has named its newest release after. I don't actually think that the codenames signal anything in particular about Apple's goals or intents for a given release, but it is usually fun to work backwards from the name to an explanation.

Nestled in [the Sierra Nevada mountain range](https://arstechnica.com/gadgets/2016/09/macos-10-12-sierra-the-ars-technica-review), Lake Tahoe narrowly misses out on a range of superlatives, in terms of US-based freshwater lakes: It's smaller in volume than the Great Lakes, and it isn't as deep as Oregon's Crater Lake. But it's large and deep enough to have inspired tales of its own Loch Ness Monster-style cryptid ("Tahoe Tessie"), among multiple other urban legends about the frozen bodies of mafia victims or volcanic tunnels that connect it to other lakes.

Tahoe is also one of a few macOS releases (including Sierra and Mojave) where the California landmark in question is shared with the neighboring state of Nevada. Partly because it's a body of water and partly because the distinctive angle in California's eastern border actually starts *in* Lake Tahoe, the exact location of the border has apparently been the matter of some dispute going as far back as the founding of California.

Both Nevada and California defined their state boundaries in terms of geographical coordinates, and there's apparently some variance as to where those coordinates are depending on the precise shape you use [to model the surface of the Earth](https://en.wikipedia.org/wiki/Figure_of_the_Earth) —one boundary marker on the US National Register of Historic Places [notes](https://npgallery.nps.gov/NRHP/GetAsset/NRHP/81000387_text) that six different geographical surveys of California's border were conducted between 1855 and 1900, and *none* of them agreed on where the border was. The dispute was at its liveliest when the states and the people in them were trying to lay claim to mineral deposits on the border, but it wasn't formally settled until it [went up to the Supreme Court in 1980](https://supreme.justia.com/cases/federal/us/447/125/).

So by choosing Tahoe as the name for this year's macOS release, Apple doubtlessly (probably) thought that the clear waters of Lake Tahoe would be a good match for the added motion and translucency of Liquid Glass. The company probably *didn't* mean to draw attention to the fact that Liquid Glass occasionally renders the boundaries between different parts of a window indistinct, fomenting border disputes. But it ended up being weirdly appropriate anyway. It's fun to learn things!

## Installer and installation

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/Installer-icons.jpg)

A near-decade's worth of macOS installer icons—and finally, one is different! Credit: Andrew Cunningham

This year's installer icon is one of the ones that finally justifies years' worth of effort spent tracking and talking about the changes in macOS installer icons. Apple's system-wide quest to replace all app icons with rounded squares has extended to the macOS install icon, which has shed its "circle with an arrow pointing down at it" appearance for the first time in modern macOS' 25-year history. It used to be a circle pointing to a CD or DVD; after that it was just a circle because it was a circle. No longer!

The new icon still uses the "abstract" version of the Tahoe default wallpaper—a wavy, predominantly blue bunch of colorful swirls with a faintly glassy texture that recalls the look of Liquid Glass and the motion of water. This image is made into a rounded square, with a Liquid Glass-style downward-pointing arrow hovering on top of it (there's still a circular icon buried in the installer app, without the arrow—you could use it to make a version of the old icon if you're feeling nostalgic.)

The default Tahoe desktop wallpaper is a photorealistic image, a Dynamic Wallpaper (meaning it's both wallpaper and screensaver, with seamless switches between the two) of Lake Tahoe in Day, Morning, Evening, and Night varieties that can change according to the time of day, whether your Mac is in Light or Dark Mode, or user preference (my favorite is Evening).

The installer itself is roughly 16.9GB in size. If you're creating USB install media for use on multiple Macs, you'll definitely need a 32GB or larger stick, rather than 16GB.

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-setup-left-align-1024x747.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-setup-left-align.jpeg) Tahoe's system dialog and other messages switch to a left-aligned style this year, after years of a predominantly center-aligned style.

Andrew Cunningham

Tahoe's system dialog and other messages switch to a left-aligned style this year, after years of a predominantly center-aligned style. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sequoia-setup-center-align-1024x747.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sequoia-setup-center-align.jpeg) The same screen in macOS Sequoia, with center-aligned text.

Andrew Cunningham

The same screen in macOS Sequoia, with center-aligned text. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-dialog-left-1024x640.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-dialog-left.jpeg) A left-aligned system dialog in Tahoe.

Andrew Cunningham

A left-aligned system dialog in Tahoe. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sequoia-dialog-center-1024x640.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sequoia-dialog-center.jpeg) The same dialog in Sequoia, center-aligned.

Andrew Cunningham

The same dialog in Sequoia, center-aligned. Andrew Cunningham

The install process itself isn't dramatically different from the last few macOS releases, except that it will be your first exposure to the left-justified text that's now used throughout system dialogs. That text has been center-aligned for so long that it's still disorienting to me even after months of using Tahoe daily, like viewing a website on a bad Internet connection where the CSS doesn't load. The part of my brain that insists on building perfectly symmetrical buildings in *Minecraft* doesn't like the asymmetrical whitespace that left-aligned text creates.

If you're upgrading to Tahoe from an older macOS version, you'll be shown a brief reel of demo videos highlighting some of the release's most user-noticeable features: the Liquid Glass UI, the new color customization options, some of the changes to Spotlight search, and the presence of the Phone app. Apple's other updates this year come with similar new-feature sizzle reels. You won't see these videos if you're setting up a brand-new Mac, or one where you've totally reinstalled macOS from scratch.

### Free space: Hope you have GB to spare

The amount of free space needed for a baseline macOS install generally climbs from year to year, with some exceptions for years when a particularly large tranche of Intel-specific code gets stripped out (next year, maybe?).

These numbers will vary slightly for different Macs. We have numbers for a base macOS 15.6.1 install and a base macOS 26.0 GM install inside a virtual machine made using Apple's built-in VM framework on an M1 MacBook Air, and we have the same numbers from bare-metal installations on a 15-inch M4 MacBook Air. For the M4 Air, we looked at the numbers with and without Apple Intelligence enabled, since turning those features on requires a multi-gigabyte download of the various models Apple is using to make its AI features work.

|  | System | Preboot | Data | Recovery | All volumes |
| --- | --- | --- | --- | --- | --- |
| **macOS Sequoia 15.6.1, virtual machine** | 11.3GB | 6.1GB | 3.2GB | 1.0GB | 21.6GB |
| **macOS Tahoe 26.0 RC, virtual machine** | 12.0GB | 6.7GB | 7.5GB | 1.2GB | 27.4GB |
| **macOS Sequoia 15.6.1, M4 MacBook Air** | 11.3GB | 7.1GB | 4.9GB | 1.1GB | 24.4GB |
| **macOS Tahoe 26.0 RC, M4 MacBook Air** | 12.0GB | 7.7GB | 10.7GB | 1.2GB | 31.6GB |
| **Sequoia, M4, Apple Intelligence** | 11.3GB | 7.1GB | 11.7GB | 1.1GB | 31.2GB |
| **Tahoe, M4, Apple Intelligence** | 12.0GB | 7.7GB | 18.3GB | 1.2GB | 39.2GB |

The bad news is that Tahoe needs a lot more storage space than Sequoia—a whole lot. In a virtual machine, a fresh Sequoia install used 21.6GB and a Tahoe install used 27.4GB, a nearly 6GB increase. On the M4 MacBook Air, it's a 7.2GB increase.

The gap widens even further with Apple Intelligence enabled—a round 8GB increase on the M4 Air. A fresh install of Sequoia with Apple Intelligence installed takes around the same amount of disk space as an install of Tahoe *without* Apple Intelligence. Tahoe with Apple Intelligence enabled needs twice as much space as a fresh Big Sur install did .

### FileVault, on by default

One other tweak to the install process is the default behavior for Apple's FileVault disk encryption. If you sign in to an Apple account as part of setting up macOS, FileVault now turns on automatically, and also automatically uses your Apple Account for recovery in the event something goes wrong.

This is a departure from previous macOS versions, which made FileVault optional and gave you other, non-cloud options for backing up your recovery key (including printing it out or just writing it down).

But if you decline to sign in with an Apple Account during setup, just creating a local account, the macOS installer *offers* FileVault encryption, generating a recovery key that you can write down and store elsewhere, but it's possible to skip FileVault entirely. Automating disk encryption and using an online account to sign in mirrors how Microsoft handles disk encryption in modern versions of Windows. But Microsoft tries to require you to use a Microsoft Account and steadily [makes that restriction harder and harder to get around](https://arstechnica.com/gadgets/2025/03/new-windows-11-build-makes-mandatory-microsoft-account-sign-in-even-more-mandatory/). Apple, at least, still has a big "no thanks" button as part of the setup flow.

## Liquid Glass

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-light.jpeg)

The macOS 26 Tahoe release and its new Liquid Glass user interface theme. Credit: Andrew Cunningham

"Liquid Glass" is Apple's branding for the ecosystem-wide reskinning that all of its operating systems are getting this year, its most substantive and comprehensive visual redesign since introducing the "flat" aesthetic of iOS 7 back in 2013.

Liquid Glass isn't a return to the days of "skeuomorphism," when the company's apps tried to mimic the look of real-world materials like brushed metal, paper, and glass in occasionally nonsensical ways. It's more like: If the default background in the iOS 7 era was a totally flat, featureless field of white or black or gray, the default background in the iOS 26 era is now a frosted sheet of glass. These glass sheets allow more of whatever is "underneath" them to shine through, and they have more visible edges that mimic the way that glass catches and reflects light.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-audio.webp)

The audio slider turns glassy when being dragged. Credit: Andrew Cunningham

That's the "glass" part. The "liquid" part is a greater sense of motion and bounciness throughout the operating systems when pulling up notifications or summoning the Control Center or interacting with sliders or checkboxes. I do not find myself with lots of opinions one way or the other about the "liquid" part; a little playfulness never hurt anyone, and the animations here don't commit the same sin as some of the new animations in iOS 7 did: Waiting for them to happen *does not actually increase the amount of time you'll spend waiting for things to happen*. Good enough for me!

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-toggle.webp)

Bouncy Liquid Glass toggles in the Settings app. Credit: Andrew Cunningham

Once you filter out YouTube engagement-bait ("liquid ass! liquid ass!" they gleefully chirp in unison, each one confident that they've been the first to arrive at the World's Most Obvious Joke), the general response to the Liquid Glass is " [eh, you get used to it](https://www.theverge.com/mobile/710980/apple-ios-26-preview-liquid-glass-ux)."

This is how I've felt myself responding to it—in macOS especially, it mostly just fades into the background, and you can keep using your computer the way you could before. Hardly a ringing endorsement. But when you watch a fairly prominent and storied company like Sonos [eat itself alive over a bad app redesign](https://arstechnica.com/gadgets/2025/01/sonos-ceo-behind-disastrous-app-exits-with-1-9-million-severance/)  or when you remember [the growing pains of iOS 7](https://arstechnica.com/gadgets/2013/09/ios-7-thoroughly-reviewed/), it's easier to appreciate a visual overhaul that's different without being disruptive.

With that being said, the increased translucency of all these glassy layers does sometimes create legibility problems—problems that are more frustrating because of Apple's visible efforts to fix or work around them.

### Consistently inconsistent

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/photos-liquid-glass.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/photos-liquid-glass.jpeg) The Photos app uses the glassier style for the top of its window, with both the color and the shape of content under the UI staying pretty visible as it hits the top of the window.

Andrew Cunningham

The Photos app uses the glassier style for the top of its window, with both the color and the shape of content under the UI staying pretty visible as it hits the top of the window. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-finder-2-1024x512.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-finder-2.jpeg) A normal Finder window also keeps icons visible underneath the title bar, but with slightly more aggressive fading and blurring.

Andrew Cunningham

A normal Finder window also keeps icons visible underneath the title bar, but with slightly more aggressive fading and blurring. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-finder-1024x512.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-finder.jpeg) Windows can elect to have a "hard-style" divider, where small text labels are involved. Here, you can catch just the tiniest hint of the content underneath the title bar.

Andrew Cunningham

Windows can elect to have a "hard-style" divider, where small text labels are involved. Here, you can catch just the tiniest hint of the content underneath the title bar. Andrew Cunningham

Apple has defined two looks for the top part of a Liquid Glass window. One, as visible in the Photos app, is to let more of the underlying content shine through the top of the window, dimming it and diffusing it less aggressively. The other, visible in some views of the Finder or in the Files app for the iPad, uses what Apple calls a "hard-style" effect, fading and diffusing underlying objects more aggressively right where the window content meets the title bar or category labels. The stuff underneath is still visible, but readability is prioritized above translucency.

Those two approaches also extend to other UI elements. Compare the look of the Notification Center in iOS 26 and macOS 26—the iOS 26 bubbles really do have the appearance of thin sheets of lightly frosted glass, where the macOS bubbles just give you the vaguest impression of what's lying underneath them.

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/ios-26-notification-1024x261.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/ios-26-notification.jpeg) The notification style in iOS 26. The glass here is distinctly glassy.

Andrew Cunningham

The notification style in iOS 26. The glass here is distinctly glassy. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-notification-1024x341.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/liquid-glass-notification.jpeg) Notifications and many other pop-ups in Tahoe use a less translucent glass style. You can still see things through it, but it's more similar to the way things looked before.

Andrew Cunningham

Notifications and many other pop-ups in Tahoe use a less translucent glass style. You can still see things through it, but it's more similar to the way things looked before. Andrew Cunningham

Other macOS menu bar items, when expanded, use a less translucent style that more closely matches what Apple is doing with notifications. Spotlight does, too. You can see some restraint in Safari's address bar and header area, for example, which are a hint more translucent than in Sequoia but considerably more opaque than the same aggressively light-bending glassy UI in iOS 26. In terms of the built-in system-level features, it's really only Control Center that seems to use the clearer, glassier look.

It's worth remembering that even at the height of Flatness Fever in the mid-2010s, the Mac's user interface always , even as Apple ratcheted up the contrast, vibrancy, and translucency. In the same way, the Mac's version of Liquid Glass looks slightly toned down compared to the same styling in iOS and iPadOS, with a lot less shininess and translucency (not none, but less).

Individual apps are split a bit more evenly between the less-translucent and more-translucent styles. Safari's address bar and header area are a hint more translucent than in Sequoia but considerably more opaque than the same aggressively light-bending glassy UI in iOS 26.

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/ios-26-safari.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/ios-26-safari.jpeg) The Safari address bar in iOS: more glassy, with clearly visible colors and shapes underneath, and more bending of light around the edges.

Andrew Cunningham

The Safari address bar in iOS: more glassy, with clearly visible colors and shapes underneath, and more bending of light around the edges. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-safari-1024x427.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-safari.jpeg) Safari in macOS Tahoe. You can make out a hint of the shape of the object under the address bar area, but it's a lot less translucent than in iOS.

Andrew Cunningham

Safari in macOS Tahoe. You can make out a hint of the shape of the object under the address bar area, but it's a lot less translucent than in iOS. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sequoia-safari-1024x427.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sequoia-safari.jpeg) Safari 26 in macOS Sequoia. Here, you only really see the color of the object underneath, with less of the shape. But the translucency level and readability are similar overall.

Andrew Cunningham

Safari 26 in macOS Sequoia. Here, you only really see the color of the object underneath, with less of the shape. But the translucency level and readability are similar overall. Andrew Cunningham

But apps like Photos and Messages share more underlying code with their iOS and iPadOS equivalents. The header/title bar area in the Photos app is everything that the header/title bar in Safari isn't: aggressively glassy all the way to the edge. Apple diffuses the color and shape of underlying content somewhat and dims it a little so that all of the UI that's up there at the top of the screen stays legible, which *usually* works but occasionally doesn't.

Ars Technica macOS reviews have commented on and complained about the conflict between translucency and legibility in macOS for [literally decades](https://arstechnica.com/gadgets/2007/10/mac-os-x-10-5/), but Liquid Glass really does kick things up to an entirely new level, and it's easier than it ought to be to take screenshots where things just look *bad*.

Liquid Glass is at its worst when text or images with lots of fine details slide underneath other text. It's visible in the way the text labels from the Settings app conflict with text in the Search box, or when details in photos make the top parts of the Photos app borderline illegible, or in the way some of the buttons are obliterated when you're using a background for a group chat in the Messages app.

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-settings-smear.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-settings-smear.jpeg) Text in and underneath the Search bar blurring together into a fuzzy mess.

Andrew Cunningham

Text in and underneath the Search bar blurring together into a fuzzy mess. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-photos-smear.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-photos-smear.jpeg) Faded gray text losing legibility on top of a photo with fine details.

Andrew Cunningham

Faded gray text losing legibility on top of a photo with fine details. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-text-smear.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-text-smear.jpeg) The text here tries to use a drop shadow to keep the light text readable against a light background, but the smaller the text is the less well it works.

Andrew Cunningham

The text here tries to use a drop shadow to keep the light text readable against a light background, but the smaller the text is the less well it works. Andrew Cunningham

You can tell Apple is aware of the problem because of some of the things it has implemented to try to keep things readable in the face of glassy translucency. Scrolling through the App Store or the Games App or Photos, the buttons at the top of the window subtly change their brightness and opacity. Text in the Messages app tries to cast a faint shadow in an attempt to stay readable when positioned over top of a loud background image. All of these subtle, automatic adjustments are happening by design, and some of them work better than others.

In apps that use the glassier, more translucent style, gray text, or text that has its own translucency effect, is always in danger of getting washed out, as is any text without some kind of backing layer between it and the content underneath (see how texts in the Messages app stay readable even when names and timestamps get washed out).

Tweaks Apple has made to the translucency levels throughout the beta process have improved this across all its platforms, which I'd expect to keep happening post-release. I also think Liquid Glass *mostly* looks better in motion than it does in screenshots. It's not hard to take still images of individual elements that look bad or weird, but these cherry-picked stills don't necessarily capture what it actually looks like in active daily use.

I'd like to see two things as Liquid Glass evolves: a commitment to creating and maintaining legibility and contrast for any text that could ever sit directly on top of other text or images, and more consistency in the way Apple tries to address translucency problems across apps and the various bits and pieces of the macOS user interface. What I do *not* particularly want Apple to do is to point to the Reduce Transparency toggle in the Accessibility settings and say "if you don't like it then turn it off." Sure, it's nice to have that as an option, and it does address a *lot* of the individual gripes I've just highlighted here, but it's more of a workaround than a fix.

### “Reduce transparency”: What you can control in the Accessibility settings

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/reduce-transparancy-control-center-1024x939.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/reduce-transparancy-control-center.jpeg) Control Center with reduce transparency turned on.

Andrew Cunningham

Control Center with reduce transparency turned on. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/photos-reduce-transparency-1024x295.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/photos-reduce-transparency.jpeg) For app windows, the reduce transparency setting also brings back clearly delineated title bars.

Andrew Cunningham

For app windows, the reduce transparency setting also brings back clearly delineated title bars. Andrew Cunningham

On that note, though, let's take a quick look at everything that happens to Liquid Glass when you *do* hit the Reduce Transparency toggle in the Accessibility settings.

As in older releases, windows in this mode will stop picking up a subtle color tint from whatever your desktop wallpaper is. Tahoe's disappearing menu bar background reappears naturally, with no visible trace of the translucency it used to have.

Menus, Spotlight, the Control Center, notifications, and any other UI element that could appear on top of any other UI element get rid of all translucency and transparency, just showing you text on top of a light or dark background. Sometimes, you'll still see those glassy outlines around the edges of things—the Control Center, Safari tabs, menus, and Spotlight are all places you can still see them. But sometimes those borders will disappear, too, like they do for notifications.

The most noticeable change to the new Liquid Glass-ified version of macOS is that Finder, Photos, Messages, and other apps regain a clearly delineated menu bar area. Text, buttons, and other elements become more consistently legible in this mode, and window content is no longer visible beneath them.

If you're having big problems with Liquid Glass and you don't want to wait for Apple to fix whatever problem you're having, the toggle can make the most bothersome aspects of the redesign go away. But it's a hacksaw, not a scalpel—if you mostly like Liquid Glass but have problems with it in one or two specific apps, it's an all-or-nothing proposition and not something you can turn off selectively.

Part of the Liquid Glass revamp is that the Mac's menu bar is going from translucent to fully transparent. The menu bar area still exists, and by default it still persists across the top of the screen at all times unless you're in Full Screen mode (unlike the iPad's now-you-see-me-now-you-don't menu bar). There's just no background on by default, and there's usually no effort made to diffuse or darken anything underneath the menu bar to make it more legible.

I say "usually" because the menu bar does still have some tricks up its sleeve. It will automatically shift from white text to black text based on whether you're using a dark or light-colored background, something that it could already do before. But under certain circumstances—when using some shades of gray as your background or an image that's dark in some areas but light in others—macOS will still draw an extremely subtle drop-shadow underneath the menu bar area to maintain legibility. You may never see this drop shadow, and I only noticed it showing up when I was specifically trying to make it show up. But it's still there as a kind of break-glass-in-case-of-legibility-emergency option.

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/invisible-menu-bar-drop-shadow.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/invisible-menu-bar-drop-shadow.jpeg) But for wallpapers where the color or pattern could still possibly cause readability issues, a subtle drop shadow shows up underneath it automatically.

Andrew Cunningham

But for wallpapers where the color or pattern could still possibly cause readability issues, a subtle drop shadow shows up underneath it automatically. Andrew Cunningham

If this doesn't work, and you do want a menu bar background that doesn't require you to turn off transparency and translucency everywhere in the operating system, there's a new Menu Bar item in the Settings with a toggle to re-enable the background. That background *usually* works just like it used to in older macOS versions, but it's more visible against a lighter-colored background. There's not a "light" background version of it that shows up when you're using a darker wallpaper anymore—Apple seems to be assuming that white text on a dark background provides sufficient contrast for people who want it.

The other big menu bar-wide change in Tahoe is that many menu items get their own little glyphs now to go along with the text. Common system-provided menu items like "open" or "paste" or all the things under the Window menu automatically get new icons, even for apps that haven't been updated with Tahoe in mind. These are all pulled from [Apple's SF Symbols library](https://developer.apple.com/sf-symbols/), which developers can pull from for their own custom menu bar icons.

### An expansive Control Center

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/control-center-customize.jpeg)

Customizing the Control Center and customizing the menu bar is done through the same interface. Credit: Andrew Cunningham

I mentioned the new Menu Bar area in the Settings app, but it's not just for determining menu bar translucency. It also serves as a replacement for the old Control Center settings, because there's more overlap between the menu bar and Control Center in Tahoe.

Tahoe offers toggles for the same handful of classic macOS menu bar items, including Spotlight, Siri, the battery meter, Wi-Fi, audio, Bluetooth, Time Machine, Fast User Switching, and a handful of others. But in Tahoe, the Control Center is getting dramatically more customizable—there are no longer fixed mandatory items that *must* appear in the Control Center, and there are a whole bunch of new controls besides. And each one of those controls can be added to the menu bar as its own standalone, top-level icon.

That means there's no Control Center item too minor or too niche to be added to the menu bar as a shortcut. If you're the kind of person who uses Shazam to identify ambient music half a dozen times a day, you can add it to the menu bar now. (I like a control that offers to automatically tile your windows for you, splitting the screen between your two most recent windows without all the clicking and/or dragging it usually takes.)

Most of these Control Center-derived menu bar items lack the finesse of the purpose-built menu bar items. Clicking the Wi-Fi or Sound settings or Dropbox's menu bar icon opens a little sub-menu without making you leave the app you're already in or dive into Settings, but many of the Control Center menu bar items are just buttons that open apps or turn settings on and off. The icons don't really change their state to reflect their status, like the Wi-Fi or Sound icons can.

Two stray observations about this newfound menu bar customization: First, this is one place where newer MacBooks' silly display notch is an active functional downgrade from a regular screen rather than a minor eyesore, because you can't fit as many menu bar icons. Second, Apple doesn't really limit you on the number of icons that can show up here—depending on the size of your screen, it's not too difficult to start eating into the space used for actual menus if you add too many.

If this happens, the menus will shove the menu bar icons over to the right a bit when you're actually digging into menus, so that you can see everything you need to see. Both visually and functionally, I prefer the menu bar with just a couple of extra frequently used icons in it. But it's one of a few places in Tahoe where Apple will actually *let* you make things kind of ugly before it will restrict your ability to change things. And on that note...

### Infinite color options

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-light.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-light.jpeg) Broadly speaking, Tahoe has six different visual styles, though many elements can be customized individually. Light mode with light icons adheres the most closely to the traditional look of macOS.

Andrew Cunningham

Broadly speaking, Tahoe has six different visual styles, though many elements can be customized individually. Light mode with light icons adheres the most closely to the traditional look of macOS. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-dark-1024x662.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-dark.jpeg) Dark mode, dark icons.

Andrew Cunningham

Dark mode, dark icons. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-clear-light-1024x662.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-clear-light.jpeg) Light mode, clear icons.

Andrew Cunningham

Light mode, clear icons. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-clear-dark-640x414.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-clear-dark.jpeg) Dark mode, clear icons.

Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-tint-light-640x414.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-tint-light.jpeg) Light mode, tinted icons.

Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-tint-dark-640x414.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-tint-dark.jpeg) Dark mode, tinted icons.

Andrew Cunningham

Since introducing Dark Mode in macOS 10.14 Mojave in 2018, macOS has included a handful of toggles for customizing the overall look of your Mac. Tahoe supercharges that ability, adding not just the relatively well-publicized dark and translucent icon options and colorful Finder folders but splitting up some existing options so that they can be customized independently. The result is a version of macOS that's more visually flexible than anything we've seen since [the old Mac OS Appearance Manager was still a thing](https://www.macgui.com/downloads/?mode=category&cat_id=11).

These are the appearance settings that Tahoe will let you customize independently:

- Whether windows and apps are in Light or Dark mode.
- Whether icons and widgets are in Light mode, Dark mode, transparent mode, or tinted mode.
- The color of your folders, which also controls the tint of icons and widgets in tinted mode.
- Your text highlight color.
- Your "theme" color. This dictates the color used for things like menu selections and buttons in various apps. By default, your text highlight color and default folder color track this selection, but you can change them if you want.
- Using tags, it's possible to give individual folders a different color from the rest of the folders on your system.

This isn't new to Tahoe, but if you want to add even *more* color, go into the Display settings in Accessibility and mess with your pointer outline and fill color.

The original introduction of Dark Mode also made it possible to make macOS more colorful, moving away from the Aqua and Graphite themes that defined macOS X for most of its run. But Tahoe opens things up to some truly discordant-looking color combinations.

## New icons

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/icon-compare-2.jpg)

Icons in macOS Tahoe aren't allowed to overhang the borders of the rounded square anymore. Sometimes the differences aren't too noticeable, though overall they have a little less personality now. Credit: Andrew Cunningham

All of Apple's first-party system icons have gotten a Liquid Glass-themed overhaul for Tahoe. Apple wants all icons, including its own, to be more consistent across its platforms. This means the last handful of icons that used the classic Mac "object sitting on top of some kind of image" style design have been removed from this version, replaced with the iOS-style rounded square. Those icons are also updated with Liquid Glass theming.

This icon shape has served the iPhone and iPad reasonably well for their entire existence, and Apple had already embraced the rounded square for most of its icons back in the Big Sur update. But the *mandatory* use of the shape, enforced at the operating-system level, is new, and it *is* too bad that first- and third-party apps that added small accents or overhanging elements to their own rounded squares are being discouraged from that behavior now.

For Apple's own icons, the new Liquid Glass icon updates are so subtle that it's hard to notice the difference, especially if the icon you're looking at is just a tiny patch of screen sitting in the Finder or on your Dock. Icons for Safari, the App Store, Messages, Reminders, and Music (among others) look almost the same as they did before.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/icon-compare-1.jpg)

Many icons get subtle Liquid Glass updates that look a lot like their previous versions. Credit: Andrew Cunningham

Icons with overhanging bits (the tabs in Contacts, the bookmark in Dictionary) or with external objects superimposed on them (the little magnifying glass for Preview, the disk with a stethoscope for Disk Utility, the caliper thing for System Information) have been changed more extensively. Sometimes the thing that was overhanging the edges of the icon just gets tucked within its borders somehow, and sometimes Apple has settled on much more abstract iconography instead. I am not sure, for example, what the wrench in the new Disk Utility icon is meant to be turning, but "not really knowing how to physically represent what solid-state storage looks like" turns out to be a recurring theme. At least the iPhone Mirroring icon now looks like something that was designed intentionally rather than a placeholder.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/icon-compare-3.jpg)

Even icons for system apps have been changed to conform to the new look. Credit: Andrew Cunningham

Apple has updated many of its system icons, including the old hard-drive-shaped icon for [your Mac's internal disk](https://arstechnica.com/gadgets/2025/08/rip-to-the-macintosh-hd-hard-drive-icon-2000-2025/). As with Disk Utility, the new icon looks basically nothing like any internal SSD that has ever existed; it could kind of look like an *external* SSD, but external disks get their own special icons.

Those system icon changes extend to folders in the Finder, which can change colors to match the highlight color you select in the Settings. Apps like Dropbox that use their own custom icons for some folders will need to be updated to support this feature, though—you may still run into icons with the old blue styling here and there.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-folder-color-change.webp)

Changing folder colors in Tahoe. Folders can also change colors individually using tags. Credit: Andrew Cunningham

But in most other cases, Apple seems happy to take older icons and automatically modify them to match Tahoe's theming rather than letting old, non-updated icons stick out as all the other icons on your system change their colors and tints.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/squircle-jail.jpg)

Apps that don't conform to the rounded square shape are put into icon jail. Credit: Andrew Cunningham

If you have an app icon that *isn't* a rounded square, macOS takes it and stuffs it inside a rounded gray square (I've seen this referred to colloquially as "icon jail" or "squircle jail," and it feels apt). If your app was already using a rounded square without any overhang, Tahoe will add a glassy border around the edge of it. And if your icon uses flat colors on top of a flat background, Tahoe will even add a bit of a glassy look to the *interior* elements, too (Slack's icon is one good example of this).

How and why is this happening? It turns out that Tahoe treats icons differently than every other version of macOS going all the way back to the dawn of Mac OS X.

### But when is an icon not an icon?

Undergirding macOS's more flexible theming and color-shifting icons is an entirely different approach to icons.

In past macOS versions, the icon you saw in the Finder or on the Dock was the.icns file contained in the app package (usually in the Resources folder in any given app bundle). The OS didn't usually do anything to this icon; it was just displayed as it was, even though in the Big Sur era Apple [strongly encouraged](https://web.archive.org/web/20201117064439/https://developer.apple.com/design/human-interface-guidelines/macos/icons-and-images/app-icon/) the usage of either rounded squares or lightly modified versions of rounded squares, in an "it would be nice if you all would start doing this" kind of way.

Tahoe is obviously getting more aggressive with icon-shape enforcement, up to and including automatically manipulating them and sentencing them to icon jail. Part of the point of this is to nudge developers toward using a single icon for every one of Apple's platforms that the app runs on—including iOS/iPadOS, macOS, and even watchOS. And to do *that* without requiring developers to manually create infinite color and tint combinations, we've got a new Apple Icon format (.icon) and [the Icon Composer app](https://developer.apple.com/icon-composer/).

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/icon-composer.jpeg)

Playing with the Ars logo in Apple's Icon Composer app for developers. Credit: Andrew Cunningham

Icon Composer is a layer-based image-editing app devoted entirely to the task of building icons for Apple's operating systems. It can import layers in.svg or transparent.png formats and offers basic controls for adjusting the opacity and shadows and arrangement of different layers (like macOS, the app applies the glassy effect to elements on its own). Developers can test icons in light, dark, or clear modes against any background color or gradient or background image that they want. If you do want your Mac and iOS apps to be a little different, there's a toggle in the app you can create to treat them separately, though it will still need to conform to the new rounded-square convention.

Icon Composer is meant as a last stop for an icon you've already designed in another app. Apple has created icon templates compatible with Adobe Photoshop and Illustrator, Figma, and Sketch. Those files contain 1024×1024 pixel rounded square shapes plus all of the gridlines that Apple encourages developers to use when designing and spacing different icon elements; Apple provides instructions for exporting layers from those apps individually as.svg or.png files.

You can love or hate Liquid Glass, and you can mourn or celebrate or be indifferent to this final death of Mac app icons with anything resembling their own unique shapes. But the idea behind Icon Composer and the new icon system is laudable, at least. Rather than manually generating icons in all kinds of different sizes for different platforms, you just create your icon once, double-check that it looks good in various modes against various backgrounds, and you send it to Xcode.

For backward compatibility, Xcode will generate a legacy.icns file based on your new.icon file; shipping different icons to fit the different looks of Tahoe and older macOS versions is [apparently not possible by design](https://mastodon.social/@siracusa/115180108905478797).

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-app-pop-in.webp)

Credit: Andrew Cunningham

One downside to all of this icon trickery is that I can now semi-regularly open a Finder window and see a hint of a delay in between when the window pops up and when the icons all pop in. This effect is especially pronounced right after you change your icons' color scheme or tint—I'd guess that the icon images are cached somewhere once they're generated, and only generated again if you change them. I would assume that the effect will be worse on a slower disk, like an external hard drive or a networked file share.

## Spotlight

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-spotlight.jpeg)

Spotlight in macOS 26 Tahoe. Credit: Andrew Cunningham

This is completely anecdotal and unscientific, but when I hear some Mac power-user types talk about extra apps they *need* on a Mac to feel at home and productive, the apps that come up the most often are ones that replace or augment the built-in Spotlight search.

Spotlight, in its previous form, was focused mostly around searches, with a few extra capabilities (like basic arithmetic or unit conversions) thrown in for good measure. It could search for local files or apps, for some kinds of online information like movies and sports scores, for contacts, and a few other things—being able to search for and launch apps makes it a decent de facto app launcher for items that aren't on your Dock.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/spotlight-primer.jpeg)

A broad overview of Spotlight's new capabilities. Credit: Andrew Cunningham

Some of the Spotlight improvements in Tahoe refine the search features that were already there, and some are new additions targeted toward the kinds of power users who might otherwise turn to apps like [Alfred](https://www.alfredapp.com/), [LaunchBar](https://www.obdev.at/products/launchbar/index.html), or [Raycast](https://www.raycast.com/) for similar functionality. I don't know that Spotlight will replace those apps for their existing users, but as with the Passwords app, it might make Spotlight good enough to keep some people from hankering for a third-party solution in the first place.

Spotlight still mainly takes the form of a big search bar in the middle of your screen, invoked by clicking the magnifying glass on the top-right of the menu bar or with the Command + space keyboard shortcut. Apple seems to know that many people using Spotlight *are* using it exclusively with the keyboard, so everything here is meant to be doable with a handful of keyboard shortcuts and button presses.

Apple has added several generalized improvements to Spotlight in this release. These include the ability to search certain websites directly (type a URL and then tab to search that domain exclusively); to filter searches by typing a forward slash and then the name of an app, a file type, a folder, or a cloud storage provider; to search through currently open Safari tabs; and to page through your Spotlight search history by pressing the up and down arrows, the same way you look through your history in a command-line window.

But Spotlight's biggest change is the addition of four sub-categories that spring up to the right of the search bar after you let it sit without input for a couple of seconds: an Applications view, a Files view, an Actions view (with the same icon as the Shortcuts app), and a Clipboard view.

The Applications view is as close as Apple gets to offering the old Launchpad's functionality, listing five of your most frequently used apps at the top, an alphabetized list of your other apps below, and a few subcategory labels that mostly correspond to . If you're paired to an iPhone via iPhone Mirroring, your iPhone apps also show up here, which can make for a big, messy alphabetized list of apps you'd never want to use on your Mac; conveniently, it's possible to hide iPhone apps from this view and just see the apps on your Mac. Apps in your Utilities folder are hidden away in their own section at the bottom of the list.

Aside from deciding whether you want to view iPhone apps and whether to view apps in a grid or list format, this view feels like it wants to be more customizable—a Windows Start menu-esque ability to manually pin or unpin apps from the top of the list would be nice.

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/spotlight-apps.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/spotlight-apps.jpeg) The default Apps view in Spotlight, a replacement for the old Launchpad screen. If you've got iPhone Mirroring on, your phone apps all appear in this list too.

Andrew Cunningham

The default Apps view in Spotlight, a replacement for the old Launchpad screen. If you've got iPhone Mirroring on, your phone apps all appear in this list too. Andrew Cunningham

Use the arrow keys to highlight an app and press tab, and you'll be able to search within that app directly from Spotlight, useful for apps with searchable repositories of information, like Mail and Notes.

To an even greater extent than the Applications view, the Files view seems like it's meant to give Spotlight a tighter focus, rather than add all-new functionality. Finding files has been a core feature of Spotlight since it was originally added [two decades (!) ago](https://arstechnica.com/gadgets/2005/04/macosx-10-4/), but updates since then have buried them a little underneath a pile of website suggestions, App Store suggestions, and IMDB results, none of which are useful when you're just trying to find that dang spreadsheet you saved somewhere.

The Files view is visually similar to the Applications view (including the ability to use a list view instead of a grid), but the purpose of each section has changed. The text labels across the top of the window are commonly used apps that are associated with documents, images, and other file types, allowing you to restrict your search *only* to files openable by those apps.

The next section down includes "suggestions," generated at least in part by how recently you've opened a file. And after the suggestions is a scrollable "recents" view showing files on your Mac or your iCloud Drive or external media, sorted by how recently the files were created or modified. Third-party cloud storage providers that have shifted to using Apple's File Provider API, as [most](https://help.dropbox.com/installs/dropbox-for-macos-support) of them [have](https://support.google.com/drive/answer/12178485?hl=en), can display results here and in the general Spotlight search view.

### Shortcuts and clipboard history

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/spotlight-action-2.jpeg)

Shortcuts actions and custom Quick Keys shortcuts in Spotlight. Credit: Andrew Cunningham

The new Actions tab is where you start to get into the stuff that makes Spotlight more powerful, in addition to more focused. By default, what you'll see here is a long list of possible actions—recent ones that are more specific to you, like sending an email or text to a specific contact, as well as a long list of all the generalized shortcuts that first-party apps and compatible third-party apps can do.

All of these tasks map to actions that apps provide to the Shortcuts app using its App Intents framework—if the app you're using has created automations that can be used by Shortcuts, then those automations can be accessed here.

What makes these actions more Spotlight-y is the ability to take any specific action that you want to use and assign a Quick Keys shortcut to invoke it. For example, you could use "tmr" as a Quick Keys trigger for the "Start a Timer" action, and then type in "tmr 2" and hit enter to quickly set a two-minute timer right from Spotlight. That's a simple example, but the flexibility of Shortcuts should give you some idea of how versatile it could be once you spend some time setting it up.

Quick Keys triggers have a bunch of requirements:

- Quick Keys can't use any special characters, like % or / or # or anything else like them
- You can't use any spaces
- You can't use capital letters (removing any possibility that Quick Keys might be case-sensitive)
- Quick Keys triggers can be between one and 12 characters long.

Within those limitations, you can use any combination of letters and numbers that you like. That includes actual words, though personally I've tried to stay away from using words to avoid muddying up my general Spotlight search results. Setting multiple actions to the same Quick Keys combo is possible—it just brings up the entire list of actions with that Quick Key, rather than just triggering one specific action.

In my testing, it doesn't seem as though Quick Keys settings sync between Macs via iCloud, as text replacements and some other settings do. The downside is you'll need to set up Quick Keys on every Mac you want to use it on, if you're still splitting time between a work laptop and one at home, or a laptop and a desktop. But it does at least maximize flexibility for two Macs that are used for totally different things.

In addition to using the provided App Intents-derived actions, Quick Keys combinations can be assigned to any custom shortcut you've created in the Shortcuts app, making it possible to invoke fairly complex actions through Spotlight with just a few keypresses—converting all files in a given folder to another type, or clearing all items from your desktop that are older than a certain date. I assigned "nas" as a Quick Keys trigger for the shortcut I use to automate connecting to my home file server. (This sort of thing dovetails nicely with other improvements to Shortcuts in Tahoe, which we'll get to shortly.)

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/spotlight-clipboard.jpeg)

Clipboard history in Spotlight. It retains its history for eight hours and only supports basic re-copying, rather than editing or anything more advanced. Credit: Andrew Cunningham

The new clipboard history feature in Spotlight is probably the most broadly useful new feature, the closest you get to "low-hanging fruit" in an operating system that Apple has been continuously building on top of for 25 years.

It is turned off by default—anything that can store this kind of history is something that a snooper or domestic abuser could access. I noticed that passwords copied from Bitwarden, a third-party password manager, would show up in the clipboard history, though passwords copied from the first-party Passwords app wouldn't. It's best for privacy and security's sake, then, to make users explicitly choose to use it. But once you turn it on, it'll store your last eight hours of copy-and-pastes, whether they're text, images, or files. A user-configurable setting or a toggle for this deletion clock would be nice, but alas, it does not exist in this version.

The full list of recent copy-pastes is always accessible via the clipboard history section of Spotlight, but because they're part of Spotlight, they're searchable from within the main Spotlight bar and will show up alongside other results.

I do find myself wishing there was one keyboard shortcut, or a dock or menu bar icon, that opened the clipboard history directly. It's possible to devise a hack for this kind of thing, via scripting or Shortcuts, but there's a button assigned to opening the Apps view and an optional keyboard shortcut you can configure to open the same part of Spotlight. I've sort of gotten used to the motion of hitting Command + space to open Spotlight, and then hitting 4 while keeping my finger on the Command button. It just feels like the clipboard history is buried half an inch further down than I'd like it to be.

Spotlight's settings have evolved a little to match the feature's added complexity. The first toggle at the top controls whether you see those results in your Spotlight search from "Apple partners"—this is how it funnels in external info about movies and sports. One new button totally wipes out all your Quick Keys settings, if you want to start fresh, and another clears your Spotlight search history.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/spotlight-settings.jpeg)

Newly redesigned settings for Spotlight. Credit: Andrew Cunningham

The menu of apps and system folders to exclude from searches is basically the same as it was before, but Apple is using sliders for those toggles instead of checkboxes now, and each app's icon appears next to it to make it easier to tell at a glance which is which. The last toggle, all the way at the bottom, turns the clipboard history all the way off, stopping it from storing history and removing the section from the Spotlight interface entirely.

I find basically everything about the Spotlight upgrade to be neutral to positive, for anyone other than hardcore Launchpad fans—Apple hasn't broken the way it used to work for people who don't touch it much, while adding some extra power-user flexibility that can be customized and extended near-infinitely by Shortcuts workflows. Keeping the clipboard history off until the user opts in is a nice touch.

## Automated Shortcuts

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/shortcuts-automation-2.jpeg)

Here, I've set my Mac to connect to my home NAS whenever it's plugged in, and to read out its current battery level. Credit: Andrew Cunningham

Of all the macOS features that have been added in the last five years or so, the one I use the *most* is probably the window snapping that they added to macOS 15 Sequoia, and the one I used second-most is Shortcuts, the modern and somewhat more user-friendly replacement for the old Automator app (Automator is still here, its interface just barely modernized enough to continue blending in). I don't have a ton of shortcuts set up, but the ones I do have I use several times a day.

Tahoe doesn't add much by way of new Shortcuts, but in addition to giving you another way to access them via Quick Keys in Spotlight, it adds Automations, a list of "if, then" statements that will run certain Shortcuts automatically when certain things happen (these are, again, not to be confused with Automator, a separate app that still exists).

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/shortcuts-automate.jpeg)

Configuring a new automated Shortcut. Credit: Andrew Cunningham

Here are all of the things that can automatically run a Shortcut when they happen:

- When it's a certain time of day, or sunrise, or sunset. These shortcuts can be set to repeat daily, weekly, or monthly.
- When an alarm goes off, is snoozed, or is stopped.
- When an email arrives. Users can specify a sender, a subject, or a recipient and can assign alerts to any one of the email accounts you've configured on the system.
- When a text arrives in Messages, based on either sender or message content.
- When items are added, modified, or removed in a given folder (this could be good for selective backups, when Time Machine is too heavy-duty.)
- When a given file is modified.
- When an external drive is connected or disconnected. This can be applied to one specific external drive, or *any* external drive.
- When you connect to or disconnect from a specific Wi-Fi network, or when you're briefly disconnected from that network.
- When you connect to or disconnect from a Bluetooth device.
- When you connect to or disconnect from an external display. This one can't be tied to a specific external display—it fires when *any* external display is plugged in, which could make it a good candidate for the "run after confirmation" setting.
- When the Stage Manager multitasking UI is turned on or off.
- When a specific app is opened or closed.
- When your battery level equals, rises above, or falls below a set percentage.
- When you plug your Mac into a charger.
- When you turn on or off the Do Not Disturb, Sleep, or Reduce Interruptions modes in the Do Not Disturb settings.

Automated Shortcuts can either be run automatically and invisibly or can prompt you for confirmation before running, making it usable for things you want to happen usually or sometimes but not always. Many automations offer an option to notify the user every time they run, even if they're set to run without confirmation.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/automation-confirmation.jpeg)

You can tell automated Shortcuts to confirm with you first, which happens via notification. Credit: Andrew Cunningham

The shortcuts I use the most frequently are for converting images and slide decks into sizes and formats suitable for our CMS. Often, the images that companies send out with press releases have super-high resolutions so that they're usable anywhere on the web (as well as in print, though that use case is ever-dwindling). I often convert them to be 1920 or 2560 pixels wide, or convert them from PNG or.webp to a good-old.jpg.

Currently, I use Quick Actions to do those conversions by right-clicking the files I want to convert and then selecting which Shortcut I want to use. But with Automations, I could just as easily have every image I send to a given folder automatically convert itself into a format and size suitable for the site. I could have my laptop connect to my home NAS every time or have large video files offload themselves to an external disk every time I plug it in.

Shortcuts is already an app that only really gives you back as much effort as you put into it, and automated Shortcuts will be the same way. I often find setting up a new one to be an occasionally frustrating exercise in trial and error. But they offer yet another way to automate repetitive tasks you find yourself doing all the time, and I'm eager to see how I can work more of them into my own setup.

## Apps: Safari 26

Tahoe includes a new major version of Safari, and like macOS, iOS, and Apple's other operating systems, it's switching to a year-based version numbering system. That means we're jumping from Safari 18 to Safari 26.

Per usual, Safari 26 will also be released to macOS 14 Sonoma and macOS 15 Sequoia, the other versions of macOS that Apple is still maintaining. On those platforms, it retains a user interface similar to Safari 18's, without the rounded Liquid Glass-ified touches you get in Tahoe.

There's plenty going on in Safari 26, as outlined in [the WebKit blog](https://webkit.org/blog/16993/news-from-wwdc25-web-technology-coming-this-fall-in-safari-26-beta/) and [Apple's WWDC session videos](https://webkit.org/blog/16987/web-technology-videos-at-wwdc25/). But once you filter out the incremental improvements to CSS and JavaScript that will mostly be of interest to web developers, changes that primarily affect platforms other than macOS (tweaks to how iOS and iPadOS handle webpages saved as apps, plus a bunch of stuff specific to visionOS), and password and passkey-related improvements that we'll cover in the section about the Passwords app, you don't end up with a huge list of features that Mac users will notice day to day.

Having dug through the changes, here's the list of Mac-related things that merited a half-interested "huh!" or better. When possible/applicable, we've done some surface-level checking to make sure all of this is supported in Sonoma and Sequoia, since Apple sometimes ships new Safari features that only work when the browser is installed on its newest OS.

### WebGPU support

Safari 26 adds support for the WebGPU graphics API for the first time. Like the older WebGL standard—which WebGPU is meant to replace—WebGPU mainly allows for the rendering of 3D graphics within a browser window. WebGPU is a low-level graphics API that works with your platform's native low-level graphics language—DirectX 12 on Windows, Metal in macOS, and Vulkan in Linux—to give browsers more direct access to the GPU hardware. This can improve performance, but it also allows the WebGPU language to use your graphics hardware for things other than 3D, including machine learning-related or AI-related tasks that GPUs are better at than CPUs.

"Whereas WebGL is mostly for drawing images but can be repurposed (with great effort) to do other kinds of computations, WebGPU has first-class support for performing general computations on the GPU," explains [the W3C's draft report](https://gpuweb.github.io/gpuweb/explainer/) outlining the WebGPU spec.

Apple is late to the party on implementing WebGL, but not egregiously so. Google first introduced support into Chrome (and Chromium, and products downstream of Chromium like Microsoft Edge) [back in 2023 with version 113](https://arstechnica.com/gadgets/2023/04/chrome-113-will-enable-webgpu-a-modern-low-overhead-graphics-api-for-the-web/), but only in Windows, macOS, and Android; as of this writing, Linux support is still labeled "experimental" and is disabled by default. Firefox introduced it in [version 141](https://mozillagfx.wordpress.com/2025/07/15/shipping-webgpu-on-windows-in-firefox-141/) just this past summer, but only on Windows at first, with macOS and other platforms arriving "in the coming months." So if you don't like Chrome or Chromium for some reason, this will be your first chance to use WebGPU in the stable version of any browser.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/webgl-sonoma-safari.jpeg)

WebGPU support in Safari 26 requires macOS 26 Tahoe. In our testing, it didn't work in Safari 26 running on macOS 14 Sonoma or macOS 15 Sequoia. Credit: Andrew Cunningham

As of Beta 5, [WebGPU samples that we tested](https://webgpu.github.io/webgpu-samples/?sample=rotatingCube) did *not* work in Safari 26 on macOS 14 Sonoma or macOS 15 Sequoia. To get support, you'll need to be running Safari 26 or newer on macOS 26 or newer. (WebGPU does work in Chrome and other Chromium browsers on these operating systems.)

### HDR image support

Safari has supported HDR video for several years now, but Safari 26 adds support for [embedded HDR images,](https://www.wide-gamut.com/test/image-hdr) for displays that can actually handle them.

Developers will be able to use `no-limit` and `standard` CSS tags to determine what happens when a mix of HDR and SDR content is being displayed at the same time. The `no-limit` tag will display HDR content in HDR; the `standard` tag will convert the images to SDR, which Apple says "prevents HDR images and video from appearing overly bright or out of place next to SDR content."

HDR image support also requires Safari 26 to be running on top of macOS 26. It won't be supported in Safari 26 on either macOS 14 Sonoma or macOS 15 Sequoia.

### SVG favicons

Apple and Safari have gone on quite a journey when it comes to favicons, those little icons that websites put in your browser tabs.

For many years, Safari simply didn't support favicons in tabs *at all*, using only hard-to-distinguish text labels to differentiate tabs from one another. Starting with , Apple gave users the off-by-default option to use favicons in tabs, matching the way that every other browser in existence treated them. 2020's Safari 14 . Having finally reconciled itself to the icons' utility, Apple is now working on improving them.

Those icons can actually be used in a lot of places throughout macOS (and iOS), including on Safari's new tab page, on the dock or Home screen (for web apps), and in Safari's tabs. Safari 26 adds the ability to recognize favicons in the.svg vector graphics format, which allows the images to be scaled up or down infinitely without losing quality, so they look nice and sharp no matter where they're displayed.

As Apple points out, the file size of an.svg file can often be smaller than a.png that's large enough to look good everywhere it's displayed. This saves web developers from needing to create multiple sizes of.png or.ico files and can even be used to create [an adaptive favicon](https://blog.tomayac.com/2019/09/21/prefers-color-scheme-in-svg-favicons-for-dark-mode-icons/) that can be tweaked to look different in dark and light modes.

Apple is more tardy with.svg favicon support than it is with WebGPU support—maybe not surprising, given how resistant the company was to using the icons as intended. Support has existed in Firefox and the Chromium family for many years (since 2019 or 2020 for Chromium, and as far back as 2015 for Firefox). Better late than never!

### “Pretty text”

This one is technically a web developer feature, and if the pages you're viewing don't use it, you won't see any benefit. But the way Safari uses the CSS `text-wrap: pretty` property is kind of cool, and Apple is taking it a bit further than other browsers that support the property (including, yes, Chrome).

"Pretty text" is meant to automatically fix a few different things that can make text on the Internet worse-looking and/or more difficult to read. Without adjusting the kerning or anything about the actual typography, the "pretty" property scoots words around to avoid hyphenation, avoid short last lines at the ends of paragraphs, clean up ragged right edges of paragraphs, and help fix "typographic rivers" or distracting lines of vertical blank space that can be created when too many of the spaces between words line up across too many lines of text.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/bad-typography-SM-dark.png)

Examples of the things that the "pretty" CSS property is trying to clean up. Credit: WebKit blog

Chrome's implementation is [primarily focused on fixing short last lines](https://developer.chrome.com/blog/css-text-wrap-pretty/) (also called "orphans," though the CSS Working Group recently [decided to stop using the terminology](https://github.com/w3c/csswg-drafts/issues/11283)). Apple developer evangelist Jen Simmons [writes](https://webkit.org/blog/16547/better-typography-with-text-wrap-pretty/) on the WebKit blog that the Chromium implementation of the tag just examines the last few lines of any given paragraph, while the WebKit/Safari implementation evaluates entire paragraphs at once when deciding how to lay out text.

The only thing the CSS specification says about the "pretty" tag is that browsers "should bias for better \[text\] layout over speed" when they encounter it but leaves the exact implementation up to individual browsers, which leaves room for Apple to go its own way a bit while still being standards-compliant.

Simmons and other developers have noted that the tag can come with a performance penalty but that the expected behavior is that "your text element would need to be many hundreds or thousands of lines long to see a performance hit."

The `text-wrap: pretty` property appears to work the same way in macOS 14 Sonoma and macOS 15 Sequoia as it does in Tahoe, once Safari 26 is installed.

### Additional anonymizing

Apple says that Safari 26 takes steps to hide other personally identifiable information from "known fingerprinting scripts" that gather information about the device you're using to browse. Properties that Apple is trying to mask include "screen dimensions, hardware concurrency \[that is, the number of logical processors available on your system\], the list of voices available through the SpeechSynthesis API, Apple Pay payment capabilities, web audio readback, 2D canvas, and more."

Apple just says that the browser prevents these scripts from "reliably accessing web APIs" that may reveal this kind of information, suggesting that some loopholes may still exist.

## The Phone app

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-phone-dialer.jpeg)

The dialer in the new Phone app. Credit: Andrew Cunningham

While Apple has allowed macOS users to take incoming phone calls from their Macs for years now, *placing* a call from a Mac has been less straightforward. You could start a phone call by clicking a phone number in Contacts or some other app, and Messages gives you buttons to kick off a FaceTime call. You could use Siri to dial numbers. But macOS wouldn't offer you an actual phone dialer until you had already made a phone call (in Sequoia, it's accessible via a little 3x3 grid of circles in the little notification that pops up).

The Phone app in macOS is a version of the updated app that the iPhone is getting this year, rearranged a bit to account for the increase in screen space. The default view shows your favorite contacts and recent calls, plus buttons for editing your favorites and viewing only missed calls or calls with voicemails. A pane on the right shows different information based on what you've clicked—usually a contact card, for a recent or missed call, but also playback controls and a transcript for voicemails.

Things you can do in the Phone app in iOS, like adding a number to a contact or reporting a call as spam, can be handled here. It's possible in the Settings to enable, disable, and configure call screening and call filtering from unknown callers, settings that will sync to your phone as you change them.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/phone-app-notfication.jpg)

Tahoe's tweaked version of the phone notification. Credit: Andrew Cunningham

Most importantly, hitting the 3x3 grid button next to the search bar brings up the standard iPhone dialer, one that can place calls directly to any number you like, rather than using Siri or your Contacts or Recents lists. Clicking each button individually with your pointer is an option, but the dialer also takes keyboard input (it still plays touch tones as you type numbers in) and will offer to paste things from the clipboard.

When you're on a call, devices with Apple Intelligence turned on can access the new Call Recording, Live Translation, and Hold Assist features, which are available from the ellipsis menu (you'll find more on those features elsewhere in the review), where you can bring up the contact card for whoever you're currently speaking to.

## The Journal app

The Mac picks up a version of the Journal app this year, though it doesn't explain why the app wasn't on the Mac in the first place. The iOS version of the Journal app prompts you to write based on recent locations you've visited, and your Mac might not go on as many day trips or long walks with you. But you'd think it would make sense for Apple's keyboard-driven platform to get the minimalist app that does nothing other than record your written thoughts.

Regardless, it's here now! The main addition to the app this year (on all the platforms that now include it) is an option to create multiple different journals for different kinds of entries. You could have one for home and one for work, or separate journals just for vacations or other Major Life Events that you might want to have cordoned off in their own special area.

The other major addition is a "Places" view. If you let the Journal app record your location whenever you're writing an entry, you can open a map view and see pins for all the locations you've been. Clicking a pin brings up all the entries associated with that location.

As on the iPhone, Journal on the Mac lets you add photos to entries, and journals can be locked with TouchID to add an additional layer of authentication.

## The Games app

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-games-app.jpeg)

The Games app in macOS 26 Tahoe. Credit: Andrew Cunningham

One could quibble about Apple's strategy, or about how successful the company has been in making the Mac a gaming destination. But Apple is visibly putting in the effort, adding new features and new tools in an attempt to make playing and developing games on the Mac a better experience. In the last few releases, Apple has added and continuously improved support for external game controllers, added a low-latency Game Mode, and introduced the Game Porting Toolkit, a collection of translation layers that helps developers test native Windows games on the Mac without modification.

We'll talk some more about the developer side when we talk about Metal 4, the upgraded version of Apple's graphics API, and improvements to Apple's Game Porting Toolkit. But for users, this year's big addition is a new Games app that serves as an alternate app storefront, a hub for online interactions and multiplayer, a reminder that the Apple Arcade service exists, and a library that gathers and displays all games installed on your Mac, including those you've installed from alternative game storefronts like Steam.

The Games app rises from the ashes of Game Center, an attempt during iOS' early days to give game developers a consistent Apple-controlled platform to use for leaderboards, achievements, and online multiplayer. Game Center was also a dedicated app, for a long while; the app was removed, but the underlying service was still there. Games is built directly on top of the remnants of the old Game Center, and any friends or achievements or multiplayer games you already had going through Game Center now appear in the Games app with no effort or action required.

New games can be bought directly through the Games app, or there's an "open in App Store" link next to the purchase buttons that will open the game's page in the App Store proper. Both apps are pulling ratings, descriptions, and other metadata from the same sources, and users can continue to buy games through the App Store without using the Games app at all. Purchased games show up both in the Library tab of the Games app, and in your list of past purchases in the App Store.

If you've spent any time with the Discover tab of the Mac App Store, the general layout of the Home tab in the Games app should look pretty familiar. It starts with a list of things you've recently bought or played, plus a feed of friend activity, some top charts for both Apple Arcade and various game categories, and then some curated highlights from Apple's internal App Store team.

When you're not a subscriber, the Arcade tab is just one big billboard for the Apple Arcade service, which costs $7 a month (or $20 a month as part of an Apple One subscription) for unrestricted access to a smallish but consistently updated batch of games. Subscribers can just use this tab to explore and download what's available.

The Friends tab is a repository of recent friend activity, and allows you to invite your friends into multiplayer games, or to participate in asynchronous "challenges" like trying to hit the highest score in a certain game within a certain amount of time. For people with longer and more active Game Center friend lists than I have, I can definitely see the appeal of this—something that allows for light competitive play that can be done whenever you can find the time, whether you're on a train, winding down before bed, or... well, what you're doing when you decide to play phone games is your business and not mine.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-games-library.jpeg)

The Library tab sees App Store games plus locally installed games from other sources. Credit: Andrew Cunningham

The Library tab will be the most interesting for Apple Arcade subscribers who have a lot of games installed from Steam, GOG, or some other source. App Store-purchased games show up in your library whether they're installed or not, while games bought from elsewhere will only show up if they've been installed, but it's nice to be able to gather everything from the built-in Chess app to a Steam-installed copy of *Cyberpunk 2077* all in one interface.

There are different view filters for installed games, games with controller support, and games from Apple Arcade, though unfortunately for the Mac app there's no filter that shows only games made specifically for the Mac—you'll see some clutter in here from every iOS and iPadOS game you own that can technically be installed on a Mac, even if it's not optimized for the Mac.

## Messages

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/messages-app.jpeg)

The new Messages app design, complete with background. Credit: Andrew Cunningham

My favorite feature about this year's Messages upgrade is the ability to add backgrounds to conversations, even though (as with all the new OS-wide appearance settings) it's possible to use color gradients or photos that make your backgrounds look profoundly ugly. But the backgrounds are set for each individual contact or group text, so you have lots of leeway to experiment without simultaneously uglifying every one of your chats.

These do appear to sync between devices connected to the same iCloud account, but I noticed that they only really synced from my iPhone to my Macs rather than syncing from my Macs back to my iPhone. Like the names and icons used for group chats, they sync between everyone in a text thread, at least if all the devices involved are running iOS/iPadOS/macOS 26.

Those backgrounds are set up through a redesigned Details panel, which slides over from the right when you click the name of your group chat or the contact you're texting with. It replaces the pop-up style Details panel from older OS versions, and that you can leave the window and return to it without closing the details page does make it more pleasant to interact with.

An entirely separate Backgrounds tab gives you some preset color and image options, along with letting you generate a background in Image Playgrounds (for Apple Intelligence-enabled devices) or pull from your Photos library. The pre-programmed backgrounds, for better or worse, are all subtly animated when the window is active, which can make some text on them harder to read.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/messages-background-2.jpeg)

The new Details pane slides over from the right, rather than popping up. Credit: Andrew Cunningham

The backgrounds do go static when the Messages window is out of focus, but for a persistently static background, you'll want to use a photo from your library; I finally got Image Playgrounds to cooperate when I asked for a "solid purple background with no other objects;" just asking for a solid color usually encouraged it to try to improvise.

When you've enabled a background, your own bubbles stay blue, but the gray bubbles from the other people you're talking to become translucent panes of Liquid Glass. The only things I really ever had trouble reading consistently were the timestamps, names, and other status messages that just show up as unadorned text without any kind of drop shadow or backing material.

Rather than one endlessly scrolling Details page, it's now broken up into other tabs for photos, links, and documents, to make it a little easier to dig through all the different kinds of things that you've exchanged with the person or people you're talking to. It's also possible to add and edit contact cards directly from the main Info tab.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/messages-background.jpeg)

Choosing from among built-in backgrounds and color options. Credit: Andrew Cunningham

The Messages update in iOS 26 and macOS Tahoe adds spam protection and screening of messages from unknown senders, which has prompted [concern and veiled legal threats](https://www.thefp.com/p/the-iphone-update-that-could-wreck-political-fundraising-tech-politics-business) from some political fundraisers (I do generally think it is a good sign when the people and organizations who abuse the status quo the most get upset about something Apple has added, as Meta did a few years ago when Apple [cracked down on some kinds of app tracking](https://www.nytimes.com/2020/12/16/technology/facebook-takes-the-gloves-off-in-feud-with-apple.html)). As much as we all love getting texts from candidates running for US House districts thousands of miles from where we live, from people claiming we have outstanding tolls due in states we've never been to, or from shady organizations [spreading political misinformation](https://www.cnn.com/2024/10/29/politics/misleading-text-messages-voting-allvote-swing-states), I think a lot of people are going to enjoy these features.

Other additions to the Messages app, at least for people safely ensconced in a group of blue-bubble friends, are live-updating polls, and typing indicators that tell you which person in a group chat is typing.

## Notes

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/notes-markdown.jpeg)

The Notes app can import and export Markdown files now. Credit: Andrew Cunningham

These days I tend to draft longer reviews and other feature work in [Typora](https://typora.io/), a simple cross-platform [Markdown](https://en.wikipedia.org/wiki/Markdown) text editor that supports exporting files to HTML that are easy to paste into our WordPress-based CMS. But I regularly jot down outlines, drafts of certain sections or paragraphs, and other bits and pieces in the Notes app, which is also my main repository for [podcast research notes](https://overduepodcast.com/), to-do lists, and anything else I need to jot down quickly.

Apple has made my life somewhat easier this year by adding basic Markdown support to the Notes app—not the ability to write Notes in the Markdown language, but to import Markdown files into Notes and export Markdown files from Notes.

Markdown is a language with a lot of subvariants, and Apple notes that your Markdown files may look different in Notes than they do in the editor that made them. But for my Typora-made files that just use simple text formatting, ordered and unordered lists, and links, I had no problems getting files into and out of Notes with their formatting intact.

## Terminal

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-terminal.jpeg)

The Terminal app gets new styles and sheds its actual 1970s terminal-based default size. Credit: Andrew Cunningham

The Terminal gets a subtle visual makeover in Tahoe, mainly via new "Clear Light" and "Clear Dark" theming options that add a touch of Liquid Glass translucency to the window.

The default typeface has been changed, from size 11 SF Mono Regular to size 12 SF Mono Terminal Regular—there's no real difference that I can see for regular letters and numbers, but Apple says the new Terminal supports Powerline glyphs, and I'd assume that's the main change between the two typefaces. Default windows open at a size of 120 columns and 30 rows, up from the previous 80 columns and 24 rows (those numbers were derived from the display resolutions of 1970s-era computer terminals, so the change is quietly momentous).

I did notice that the new theming and window sizing was only used by default on fresh installs of Tahoe; an upgrade install from macOS Sequoia still used the old default theme and 80×24 window size.

Finally, beyond the new Clear themes and all of the old ones that are still included, Apple says the new Terminal app has 24-bit color support, allowing users to choose from among 16.7 million colors when customizing the window.

## The Passwords app and passkeys

It's not a perfect comparison, but I think [passkeys](https://arstechnica.com/security/2024/12/passkey-technology-is-elegant-but-its-most-definitely-not-usable-security/) now are a bit like USB-C was in the mid to late 2010s. It's a well-intentioned idea with a lot of potential and wide industry buy-in, and clearly better in important ways than the thing they're meant to replace. But the early rollout has been piecemeal and protracted and a bit messy, and it may still be a few years before they really come into their own.

[This Apple developer video from this year's WWDC](https://developer.apple.com/videos/play/wwdc2025/279/) is a wide-ranging look at all the things Apple is doing to help streamline passkeys and their implementation in Apple's Passwords app this year, mainly focused on using passkeys instead of passwords for new accounts, keeping passkeys up to date when they change, and seamlessly helping to migrate users to passkeys as apps and services add support for them.

Tahoe and Apple's other OS updates have added an account creation API that websites and apps can use to generate a passkey instead of a password when users sign up for a new account; this passkey can then be stored in Passwords, or any third-party app capable of storing passkeys, and synced between your devices to make sign-in easier everywhere.

Apps and websites are able to signal to Passwords and other password managers when a passkey needs to be updated, like when a user changes the email address on their account or some other information after they've already signed in. The same API is also able to revoke passkeys, preventing users from trying to sign in using a passkey that no longer functions.

And when using a password to sign in to an app or website that supports passkeys, those apps will automatically be able to generate a passkey for that account and add it to the user's password manager. This won't replace the user's password—they won't suddenly be locked out on other devices that don't support passkeys or aren't synced with Passwords or another credential manager—but it does build an off-ramp that people can use to throw out their passwords and switch to a passkey-only setup at some point later on.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-passwords-export.jpeg)

The Passwords app is able to export and import passkeys and other information securely, in accordance with new FIDO Alliance standards. Credit: Andrew Cunningham

Because all of the tech industry's major players are trying to drive adoption of passkeys, Apple has made sure that these features work not just in the built-in Passwords app, but in third-party password managers and credential-storage apps that use the APIs that Apple provides for saving and autofilling credentials.

To that end, Apple has also implemented [new standards developed by the FIDO Alliance](https://fidoalliance.org/fido-alliance-publishes-new-specifications-to-promote-user-choice-and-enhanced-ux-for-passkeys/) for importing and exporting passkeys between different apps that support them. Exporting data from a password manager generally means spitting out a large plaintext.csv file and them importing that file into the new app you plan to use; the new Credential Exchange Protocol (CXP) and Credential Exchange Format (CXF) facilitates direct, secure communication between two different credential managers and standardizes the formats used to store and export passkeys, passwords, and other data.

As Apple's Passwords app becomes more useful and feature-rich, it will become more and more feasible for some users paying for a third-party password manager to switch to Apple's version instead. These new changes should help make that easier (and make the reverse easier, for people who decide to migrate from Apple's ecosystem to someplace else).

## More gaming improvements: Metal 4’s upscaling and frame-generation features

Tahoe, iOS, and iPadOS are all getting a new version of the Metal graphics and GPU compute API for the first time since 2022.

On the gaming side, [Metal 4](https://developer.apple.com/documentation/metal/understanding-the-metal-4-core-api) improves MetalFX upscaling, improves shader compilation speed, and adds the ability to generate interpolated frames, which can boost frame rates without requiring hardware upgrades.

For readers not well-versed in PC gaming, frame generation features look at two frames that your GPU has rendered and then uses machine-learning algorithms to generate a frame in between them. This is less computationally intensive than actually rendering all three of those frames; it can be combined with MetalFX's existing temporal upscaling, boosting performance even further.

Apple says that frame generation in Metal 4 uses the same depth and motion vectors that the MetalFX upscaler does, so games that have already adopted MetalFX should be able to add frame-generation support relatively easily.

But frame generation on PCs has real downsides, and we'd assume that frame generation on the Mac will have the same weaknesses. The first is that it introduces some extra input latency, because it's intentionally introducing a small delay to grab two frames so that it can create the interpolated frames between them.

But the main problem—especially for Apple's platforms, where the vast majority of users will be using the lower-end GPUs in the basic M1, M2, M3, and M4 chips rather than the beefier GPUs in the Pro, Max, or Ultra versions—is that frame-generation features need a reasonably high base frame rate to generate decent-looking results.

Think about how jerky a game looks when it's running at 15 or 20 frames per second—the onscreen image can change a lot from one frame to the next. That dramatically increases the likelihood that the interpolated frame in between the two rendered frames will look weird in some way, because the algorithm is just having to guess too much about the motion happening in between those two frames. Frame interpolation is good for making a smooth-running game look smoother; it's not a good tool for making an unplayable frame rate into a playable one.

The new upscaling features should be more broadly useful, even for the lower-end GPUs in Apple's products. For one, MetalFX now allows developers to change the input resolution dynamically. Say you're usually converting natively rendered 1080p frames into 4K frames, but your game hits a particularly complicated scene that's harder to render. MetalFX can briefly change that 1080p input resolution to something lower, which would briefly reduce image quality (since the upscaler is now turning an even lower-resolution image into a 4K image) in the interest of maintaining smoothness. Think of it as switching between the upscaler's "Quality" and "Performance" modes automatically, based on the complexity of the scene being rendered.

Metal 4 adds denoised upscaling to MetalFX, which is particularly useful when trying to provide high-quality upscaling for the ray-traced lighting effects that M3 and M4-series GPUs can render.

Those gaming improvements are helped along by some of the improvements on the GPU-compute side. These improvements include the addition of tensors, which can help with image upscaling and interpolation as well as accelerate machine-learning and AI-related workloads.

We spoke with John Poole, founder of Primate Labs and developer of Geekbench, about what some of the Metal 4 additions would improve for developers and users.

"Metal 4 tensors enable developers to combine machine learning and graphics operations within the same pipeline, improving performance and efficiency since the application no longer has to move data between separate machine learning and graphics pipelines," Poole wrote to Ars. "Applications that only run machine learning or GPU compute pipelines won't benefit much from this change, as there's no need to move data between separate pipelines. I took a look at Geekbench 6 GPU and Geekbench AI GPU benchmark scores for macOS 15.6 and macOS 26.0 and saw modest improvements at best in both."

"Developers may appreciate having tensors as a first-class storage type, though, as it will make writing machine learning GPU kernels easier," Poole continued. "I expect this change is primarily a runtime change (in that it doesn't require hardware support), which is why it's available on older Macs, iPhones, and iPads."

One throughline for most of the major additions to Metal 4: They're all attempts to keep Apple relevant in areas where its competitors, most notably Nvidia, currently have the upper hand.

Metal 4 does require a sufficiently modern Apple Silicon processor—either an Apple M1 or newer on the Mac side, or an Apple A14 Bionic or newer on iPhones and some iPads. Intel Macs and the very oldest supported iPhones and iPads with A12 and A13-series chips won't see any benefits.

### Game Porting Toolkit 3.0

The other gaming improvement for Mac this year is version 3.0 of Apple's Game Porting Toolkit. The GPTK is formally a tool meant for developers who want to start exploring a Mac port by testing their existing Windows games through translation layers, converting DirectX API calls into Metal API calls that the Mac can work with (SteamOS and the Steam Deck run Windows games on Linux the same way, also thanks to many of the exact same open source projects).

But other companies and community members have used it to run unmodified Windows games on their Macs with no effort required on the part of the game developers. The most prominent paid solution is [Crossover](https://www.codeweavers.com/crossover?id=ad&gad_source=1&gad_campaignid=20895116520&gbraid=0AAAAAqqVsgsPbgEmxoOgEB6vkRM6MHyKW&gclid=Cj0KCQjwrJTGBhCbARIsANFBfgtspJ2U2hD1fzsNhN7uzd2mFcsh4vnTA_u-k7kB74BQTDs6oX_qdAoaAnVQEALw_wcB); [Whisky](https://getwhisky.app/) was a prominent community-developed alternative, but its developer [stepped away from the project earlier this year](https://docs.getwhisky.app/maintenance-notice). Projects like [Sikarugir](https://github.com/Sikarugir-App/Sikarugir) promise similar results, though it doesn't have the same reputation for user-friendliness.

This year's GPTK update uses Metal 4's upscaling and frame-generation improvements to translate Nvidia's DLSS upscaling and frame generation in games that support it. Enable DLSS in the Windows games you're trying to run, and the GPTK will attempt to translate it to MetalFX.

YouTuber Andrew Tsai [tested](https://www.youtube.com/watch?v=amA2nufBs7s) a series of 10 Windows games using a beta version of GPTK 3.0 and CrossOver a couple of months ago. He generally came away impressed—version 3.0 of the GPTK adds enough features and fixes that some games that ran with glitches or visual artifacts now look just fine, and some games (including *Starfield*) that failed to run at all under older versions of the toolkit are now also working OK.

For all of Apple's gaming efforts, the company still tends to be announcing the same kinds of games: AAA titles from a couple of years ago that have already been available on the PC and consoles for quite a while. "Any AAA games at all" is an improvement over where the Mac was a few years ago, but we still haven't reached that tipping point where big games are being released simultaneously on both the PC and the Mac (give or take [the odd indie megahit](https://arstechnica.com/gaming/2025/08/explaining-the-internets-obsession-with-silksong-which-finally-comes-out-sept-4/)).

## Grab Bag

Observing hallowed, time-honored tradition, let's take a minute to run down a list of changes that are worth documenting, but are either too small or too niche to need extended pontification. That's right, folks, it's the Grab Bag.

### Lock screen typeface options

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-lock-screen.jpg)

Tahoe's lock screen gets a customizable clock, though it still lags behind the iOS and iPadOS lock screens in customizability features. Credit: Andrew Cunningham

The lock screen on the Mac remains a desolate place, relative to the same area in both iOS and iPadOS—this is still a no-notifications, no-widgets zone that exists only to keep your Mac locked. But Apple will at least let you customize the look of the clock now, with a list of half a dozen typefaces that mirrors those available in iOS and iPadOS (but without the same color customization options, for some reason).

The setting to change the typeface is a bit buried and separate from all the other lock screen settings. You'll find it by opening Settings, clicking Wallpaper, and then clicking the Clock Appearance button. Select the typeface you want and the weight of the typeface (if applicable), and select whether to display it over the lock screen, over both the lock screen and your screen saver, or to turn it off entirely.

### Live translation

We'll have more about Apple's live translation features in our upcoming iOS 26 review, since it's slightly more relevant on Apple's mobile handheld software platform than on the Mac. But Macs that support Apple Intelligence—every Apple Silicon model going back to the M1—can translate messages and voice calls and provide subtitles for FaceTime calls using on-device language models. I still find most of Apple's AI-related features to be either underwhelming or inessential, but this one does feel like it could be genuinely useful for travelers or anyone looking to circumvent a language barrier.

### Live Activities from iOS

![A Live Activity from an iPhone app, displayed in the macOS menu bar.](https://cdn.arstechnica.net/wp-content/uploads/2025/09/live-activities-tahoe.jpg)

A Live Activity from an iPhone app, displayed in the macOS menu bar. Credit: Andrew Cunningham

When you've got an iPhone paired with your Mac via iPhone Mirroring, you'll now automatically see pop-ups for Live Activities appear in your menu bar when they're active on the phone.

The small, black ovular widget appears on the left side of the right-hand menu bar area, with an icon and an estimated time when the activity is due to be completed. Tracking your takeout order? Trying to squeeze in five more minutes of something while you wait for your Lyft to show up? If it's on your phone, you can see it on the Mac.

### New wallpaper screensavers

We've mentioned this elsewhere already, but Tahoe comes with a small collection of new moving wallpapers themed around the codename—these are the wallpapers that can start moving to act as a screensaver, and then slow down and come to a stop when it's time to be a desktop wallpaper again.

Nothing here has the retro-cool factor of last year's classic Macintosh-themed wallpaper, but there are still some pretty ones: light and dark versions of an abstract blue glassy swirl that kind of evokes flowing water, and a shot of the shores of Lake Tahoe during four different times of day.

Several new motion wallpapers are available in the Landscapes category, too: new locations include Goa, the Himalayas, the Ganges, and tea gardens in Kerala, India, along with a couple others. The Cityscape, Underwater, Earth, and other categories appear to have all the same wallpapers available as in Sequoia.

### Two-factor autofill in any browser

When it's possible, you should move on from using SMS messages for two-factor authentication to codes generated by an app or to passkeys. But there are still plenty of times when you'll run into authentication code texts, either because you're trying to set up an account for the first time, or because the thing you're trying to log in to doesn't support anything else.

For those cases, Tahoe adds a handy feature: the ability to autofill these codes from the Messages and Mail apps into any browser, not just Safari. Just like when you use the equivalent feature in Safari or on iOS, macOS can delete these codes for you automatically after using them.

### Game Overlay

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-game-overlay.jpeg)

The Game Overlay in macOS Tahoe. Credit: Andrew Cunningham

Tahoe's new Game Overlay doesn't add features so much as it groups existing gaming-related features to make them more easily accessible.

The overlay makes itself available any time you start a game, either via a keyboard shortcut or by clicking the rocketship icon in the menu bar while a game is running. The default view includes brightness and volume settings, toggles for your Mac's energy mode (for turning on high-performance or low-power mode, when they're available), a toggle for Game Mode, and access to controller settings when you've got one connected.

The second tab in the overlay displays achievements, challenges, and leaderboards for the game you're playing—though only if they offer Apple's implementation of those features. Achievements for games installed from Steam, for example, aren't visible. And the last tab is for social features, like seeing your friends list or controlling chat settings (again, when you're using Apple's implementation).

I didn't think the [Apple Intelligence notification summaries](https://arstechnica.com/apple/2024/11/apple-intelligence-notification-summaries-are-honestly-pretty-bad/) were very useful when they launched in iOS 18 and macOS 15 Sequoia last year, and I don't think iOS 26 or Tahoe really changes the quality of those summaries in any immediately appreciable way. But following a controversy earlier this year where the summaries botched major facts in breaking news stories, Apple turned notification summaries for news apps off entirely while it worked on fixes.

Those fixes, [as we've detailed elsewhere](https://arstechnica.com/apple/2025/07/apple-intelligence-news-summaries-are-back-with-a-big-red-disclaimer/), are more about warning users of potential inaccuracies than about preventing those inaccuracies in the first place.

Apple now provides three broad categories of notification summaries: those for news and entertainment apps, those for communication and social apps, and those for all other kinds of apps. Summaries for each category can be turned on or off independently, and the news and entertainment category has a big red disclaimer warning users to "verify information" in the individual news stories before jumping to conclusions. Summaries are italicized, get a special icon, and a "summarized by Apple Intelligence" badge, just to make super-ultra-sure that people are aware they're not taking in raw data.

Personally, I think if Apple can't fix the root of the problem in a situation like this, then it's best to take the feature out of iOS and macOS entirely rather than risk giving even one person information that's worse or less accurate than the information they already get by being a person on the Internet in 2025.

As we wrote a few months ago, asking a relatively small on-device language model to accurately summarize any stack of notifications covering a wide range of topics across a wide range of contexts is setting it up to fail. It does work OK when summarizing one or two notifications, or when summarizing straightforward texts or emails from a single person. But for anything else, be prepared for hit-or-miss accuracy and usefulness.

### Relocated volume and brightness indicators

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sound-indicator-1024x256.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/sound-indicator.jpeg) Tahoe's new volume indicator, in its new location.

Andrew Cunningham

Tahoe's new volume indicator, in its new location. Andrew Cunningham

[![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/brightness-indicator-1024x256.jpeg)](https://cdn.arstechnica.net/wp-content/uploads/2025/09/brightness-indicator.jpeg) The brightness indicator has the same styling.

Andrew Cunningham

The brightness indicator has the same styling. Andrew Cunningham

The pop-ups you see when adjusting the system volume or screen brightness have been redesigned and moved. The indicators used to appear as large rounded squares, centered on the lower half of your primary display. The design had changed over the years, but this was where they've appeared throughout the 25-year existence of Mac OS X.

Now, both indicators appear in the upper-right corner of the screen, glassy rectangles that pop out from items on the menu bar. They'll usually appear next to the Control Center menu bar item, but the volume indicator will pop out of the Sound icon if it's visible.

### New low battery alert

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-low-battery.jpeg)

Tahoe picks up an iPhone-ish low-battery alert on laptops. Credit: Andrew Cunningham

Tahoe tweaks the design of macOS's low battery alert notification. A little circle-shaped meter (in the same style as battery meters in Apple's Batteries widgets) shows you in bright red just how close your battery is to being drained.

This notification still shows up separately from others and can't be dismissed, though it doesn't need to be cleared and will go away on its own. It starts firing off when your laptop's battery hits 10 percent and continues to go off when you drop another percentage point from there (it also notified me without the percentage readout changing, seemingly at random, as if to annoy me badly enough to plug my computer in more quickly).

The notification frequency and the notification thresholds can't be changed, if this isn't something you want to be reminded about *or* if it's something you want to be reminded about even earlier. But you could possibly use the battery level trigger in Shortcuts to customize your Mac's behavior a bit.

### Recovery mode changes

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-recovery.jpeg)

A new automated recovery tool in macOS Tahoe's recovery volume. Credit: Andrew Cunningham

Tahoe's version of the macOS Recovery mode gets a new look to match the rest of the OS, but there are a few other things going on, too.

If you've ever had a problem getting your Mac to boot, or if you've ever just wanted to do a totally fresh install of the operating system, you may have run into the Mac's built-in recovery environment before. On an Apple Silicon Mac, you can usually access it by pressing and holding the power button when you start up your Mac and clicking the Options button to start up using the hidden recovery volume rather than the main operating system volume.

Tahoe adds a new tool called the Device Recovery Assistant to the recovery environment, accessible from the Utilities menu. This automated tool "will look for any problems" with your system volume "and attempt to resolve them if found."

Maybe the Recovery Assistant will actually solve your boot problems, and maybe it won't—it doesn't tell you much about what it's doing, beyond needing to unlock FileVault on my system volume to check it out. An [Apple support document](https://support.apple.com/en-us/123922) about the tool is also light on descriptions of what it actually does—though Apple does not that the tool should generally run automatically in the cases where it can actually be useful, and you generally shouldn’t need to run it manually.

![](https://cdn.arstechnica.net/wp-content/uploads/2025/09/tahoe-recovery-browser.jpeg)

The web browser in the recovery environment is still WebKit, but it's not Safari-branded anymore, and it sheds a lot of Safari features you wouldn't want or need in a temporary OS. Credit: Andrew Cunningham

Apple has made a couple of other tweaks to the recovery environment, beyond adding a Liquid Glass aesthetic. The recovery environment's built-in web browser is simply called Web Browser, and while it's still based on the same WebKit engine as Safari, it doesn't have Safari's branding or its settings (or other features that are extraneous to a temporary recovery environment, like a bookmarks menu). The Terminal window picks up the new Clear theme, new SF Mono Terminal typeface, and the new default 120-row-by-30-column size.

### A new disk image format

Not all Mac users interact with disk images regularly, aside from opening them up periodically to install an app or restore an old backup. But among other things, disk images are used by Apple’s Virtualization framework, which makes it relatively simple to run macOS and Linux virtual machines on the platform for testing and other things. But the RAW disk image format used by older macOS versions can come with quite severe performance penalties, even with today’s powerful chips and fast PCI Express-connected SSDs.

Enter the Apple Sparse Image Format, or ASIF. Apple’s developer documentation says that because ASIF images’ “intrinsic structure doesn’t depend on the host file system’s capabilities,” they “transfer more efficiently between hosts or disks.” The upshot is that reading files from and writing files to these images should be a bit closer to your SSD's native performance (Howard Oakley at The Eclectic Light Company has some testing that [suggests significant performance improvements](https://eclecticlight.co/2025/06/12/macos-tahoe-brings-a-new-disk-image-format/) in many cases, though it’s hard to make one-to-one comparisons because testing of the older image formats was done on older hardware).

The upshot is that disk images should be capable of better performance in Tahoe, which will especially benefit virtual machines that rely on disk images. This could benefit the lightweight virtualization apps like [VirtualBuddy](https://github.com/insidegui/VirtualBuddy) and [Viable](https://eclecticlight.co/virtualisation-on-apple-silicon/) that mostly exist to provide a front end for the Virtualization framework, as well as virtualization apps like Parallels that offer support for Windows.

### Quantum-safe encryption support

You don’t have a quantum computer on your desk. No one does, outside of labs where this kind of technology is being tested. But when or if they become more widely used, they’ll render many industry-standard forms of encryption relatively easy to break.

Tahoe and Apple’s other OS updates this year add support for quantum-safe encryption [algorithms like ML-KEM and ML-DSA to CryptoKit](https://developer.apple.com/documentation/cryptokit/using-the-quantum-secure-apis), the framework that allows third-party apps to leverage macOS’s built-in encryption technologies. This comes a year and a half or so after Apple [began protecting iMessage conversations](https://arstechnica.com/security/2024/02/imessage-gets-a-major-makeover-that-puts-it-on-equal-footing-with-signal/) with post-quantum encryption algorithms.

Microsoft is also improving Windows 11’s support for quantum-safe encryption algorithms, as it announced [earlier this year](https://arstechnica.com/security/2025/05/heres-how-windows-11-aims-to-make-the-world-safe-in-the-post-quantum-era/). We’re unlikely to need these improved encryption algorithms soon, but by adding support to their operating systems relatively early, companies like Microsoft and Apple make it more likely that the transition will be smoother and less visible for their end users.

### More post-processing options for video and images

Apple's [VideoToolbox framework](https://developer.apple.com/documentation/videotoolbox) is what handles hardware-accelerated video encoding and decoding on Apple's platforms, and this year it's picking up a new [VTFrameProcessor API](https://developer.apple.com/documentation/videotoolbox/vtframeprocessor) that allows developers who use machine learning algorithms to enhance video playback and editing.

A frame rate conversion effect can adjust the frame rate of a video, something that can create a slow-mo effect in videos that weren't shot in slow-mo, and motion blur effect can be added to videos, too. A Super Resolution scaler can intelligently upscale low-resolution videos. For video chats, a low-latency Super Resolution filter, temporal noise filtering, and frame interpolation can improve video quality and smooth a low-frame-rate video chat.

Technically, the Mac saw the first versions of these improvements in the 15.4 update for Sequoia; the new VTFrameProcessor API is only new to iOS 26, iPadOS 26, and Catalyst apps that have been repackaged for the Mac. But additions like this can escape notice when these smaller updates come out, so it's worth calling attention to for Tahoe upgraders.

## Tahoe clears the decks

The macOS Tahoe release will probably be remembered mostly for Liquid Glass. It’s a major change to the way things look, and for better or worse, those shifts tend to suck the oxygen out of the room.

I could take or leave Liquid Glass—I mostly don't mind it, but I’m not sure I'm convinced that it's an unambiguous improvement over what Apple was using before. The standalone instances of messy overlap or overzealous translucency aren't dealbreakers, but they are small regressions in usability and accessibility that Apple will need to keep massaging over time, just as it did after iOS 7 was released. And while I see the value in visual consistency, I do think forcing apps to use a rounded square icon no matter what gives them one less way to distinguish themselves from each other in the Dock, the Finder, or Spotlight.

But even Liquid Glass-skeptical power users should find enough things to like in Tahoe to justify the installation. Maybe you’re already using a clipboard manager or Spotlight replacement that already does more than Apple’s new-and-improved version, but Quick Keys, automated Shortcuts, additional theming options, a more capable version of Metal, and the typical trail-mix-bag full of odds and ends all add up to a release that would feel pretty useful even if it looked the same as it did last year.

Getting this visual transition out of the way now also clears the decks for what could be a pretty busy macOS 27. Ending support for the last handful of Intel Macs gives Apple a cruft-clearing opportunity that it hasn’t had since [2009’s Snow Leopard release](https://arstechnica.com/gadgets/2009/08/mac-os-x-10-6/) ended support for PowerPC Macs. And who knows what other features might be possible once the Mac shifts from Apple Silicon-first to Apple Silicon-only? We’ll find out in nine months or so.