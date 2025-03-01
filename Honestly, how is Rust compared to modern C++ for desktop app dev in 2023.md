---
title: "Honestly, how is Rust compared to modern C++ for desktop app dev in 2023"
source: "https://www.reddit.com/r/rust/comments/15fqzp5/honestly_how_is_rust_compared_to_modern_c_for/?post_fullname=t3_15fqzp5&post_index=1"
author:
  - "[[[deleted]]]"
published: 2023-08-01
created: 2025-02-17
description: "Note: I get it if this post gets removed for off-topic, I just really like the input and knowledge of the Rust sub users. I'm a big fan of t"
tags:
  - "clippings"
---
*Note: I get it if this post gets removed for off-topic, I just really like the input and knowledge of the Rust sub users. I'm a big fan of the Rust language, but I'm seeking practical advice here.*

I'm thinking of creating a cross platform desktop app, and the largest libraries available are for C++. That includes the foundational libraries, like Qt, and also for the app-specific functionality which requires low-level networking like packet manipulation. Rust has Tauri, but I'm mainly looking for a system-tray-only type of app, and I'm not a fan of relying on a web tech to render my app. I'm striving for quality.

Rust is clearly weaker when it comes to the ecosystem in my case, but at the same time I love the cargo build system, the easy plug-and-play crates and the raliability of written code, and last but not least no stupid, time wasting header files.

But now I'll ask a question that I know is impossible to answer, but I'm looking for different opinions, experiences and reasoning:

which, in your opinion, is better for my green field cross platform desktop app with low level ?

Edit: After reading comments and remembering my conclusion the last time I looked into this problem space, I think I'll be programming the "core" of my application in Rust, as there are some low level networking libraries available, and then I can plug-and-play whatever presentation layer framework I want such as Tauri or egui. Most importantly the app is to mainly live in the systray, and Tauri supposedly has that functionality. Result: max performance for the end user, with safety as an added bonus as always with Rust. In addition, I can re-use my Rust code in the backend as I plan on doing a websocket real-time server communicating with this desktop app and a web app of the same user. I'm sure that would be a pain to implement in C++, but rather pleasant in Rust given frameworks like Axum.

---

## Comments

> **anlumo** • [81 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juf1w94/) • 2023-08-02
> 
> Slint is trying to copy Qt, but Qt has a headstart of nearly three decades and also a lot more developers behind it.
> 
> I personally chose to use neither, since the ecosystem just isn't there. I'm using Flutter in combination with the flutter\_rust\_bridge to write the stability and performance critical parts in Rust and the UI in Dart.
> 
> > **stumblinbear** • [31 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juf2tfr/) • 2023-08-02
> > 
> > I'm just writing my own flutter-like UI framework in Rust, haha
> > 
> > > **anlumo** • [25 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juf52uv/) • 2023-08-02
> > > 
> > > Having grown up together with GUI frameworks (from [Turbo Vision](https://en.wikipedia.org/wiki/Turbo_Vision), [PowerPlant](https://en.wikipedia.org/wiki/PowerPlant), Cocoa, Qt, UIKit to Emberjs, React, etc), I feel like the programming world is slowly approaching the ideal architecture for GUI programming, and it's very close to what Flutter is doing (which is usually called “inspired by elm” I think).
> > > 
> > > However, Flutter itself is very reliant on class inheritance (Widget -> StatelessWidget/StatefulWidget -> your own subclass), so I have no idea how you want to do that in Rust. Also, you get the problem of ownership not being that easy to handle when you want event handlers to mutably access `self`. Yew gets around this by using a message queue (which is actually closer to elm, but further away from Flutter), but this is a bit awkward because you need three places in the code that have to be coordinated (the enum, the event handler and the place where the event is sent).
> > > 
> > > Btw, there's also [Xilem](https://github.com/linebender/xilem/), which more or less attempts to do the same.
> > > 
> > > > **stumblinbear** • [11 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jug0kv1/) • 2023-08-02
> > > > 
> > > > Yeah it's not necessarily an easy problem to solve. It requires an unfortunate amount of dynamic dispatch, but I keep it outside of that realm as much as possible. So far I've managed stateless, stateful, layout, and paint widgets, along with inherited widgets, with almost completely localized updates when things change. I stole a ton of ideas from flutter including the element tree, which means the vast majority of the tree isn't actually updated at all. In release mode some examples I've put together are updating extremely quickly (way under a ms, a few hundred micros and it doesn't increase much with the size of the tree; I need to do more stress testing), so I don't think the dynamic dispatch is a huge issue.
> > > > 
> > > > Each widget impls an ElementBuilder trait which returns a specialized element for that widget. Stateless and stateful widgets can't do layout, layout widgets cannot hold state, paint widgets only host a paint function for rendering. If you want a specialized use case, you can just make your own Element
> > > > 
> > > > The event handler case is relatively straightforward. You receive a context on build and you register your callback through that (just ctx.callback(func)) which returns a type you can use to queue the callback to be run on the next engine update where you can receive mutable access.
> > > > 
> > > > It's not perfect, but I'm happy with how it's going so far. I've been working on it for around a year and a half so far (off and on). I actually just added in multi-window support (pretty basic right now, but I'm looking to expand it) with the windows defined in the tree itself.
> > > > 
> > > > I'm personally not a huge fan of the Elm architecture, and trying to make absolutely everything in the tree statically typed is an exercise in frustration, especially for the devs that have to use it, so I just went with Rcs. They're quick enough and let me do tree diffing for free! (Especially useful when a widget isn't able to derive PartialEq)
> > > > 
> > > > Not looking for it to be the absolutely most performant thing out there, just for it to be ergonomic and familiar
> 
> **\[deleted\]** • [14 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugum6f/) • 2023-08-02
> 
> Thanks for the recommendation. However I highly dislike Flutter for a number of reasons. To simplify, Flutter != quality IMO, including on desktop. My biggest issues have been:
> 
> \- The concept of bringing your own render engine is a good idea if you are going to build something like a game or fundamentaly different experience than a "standard" GUI. But at the same time you're removing so many essential features that make a good, premium user experience like when content should move at 120Hz (ProMotion), accessibility, slight performance decreases like janks and stutters, higher resource usage. It's essentially reinventing the wheel for a lot of things that the native platform already has implemented, and generally do a better job of implementing for that specific device. That is most relevant for mobile, but also applies to desktop (especially Mac since the users generally care more for premium UX). Also, last time I tried Flutter desktop, it was hard capped at 60hz... That was seriously annoying when I was sitting on a 240hz monitor and created an instant dislike for Flutter's own "better than native" rendering system.
> 
> \- Flutter is created by Google for Google. That means the default UI is material UI, and I seriously highly despise material UI. For the love of good please keep that cheap android-y looking ass GUI away from all and any of my devices, and websites. Unless it's a Google website. It just screams "default, cheap template" whenever I see material UI that's not a Google product. I know it is possible to customize to the point that you have created your own widgets that does not look like MUI, but I really dislike having MUI as the default starting foundation for my GUIs.
> 
> \- The Dart language and Flutter design system has a lot of haters and lovers as usual, but I really dislike the idea of having yet another TypeJavaReactClassScript language. I want to get away from that as far as possible.
> 
> Taking all that into consideration, I think I'll try doing Rust and then plug-and-play whatever GUI or system tray functionality I may need from the likes of Tauri or egui.
> 
> > **anlumo** • [10 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugwnnp/) • 2023-08-02
> > 
> > > The concept of bringing your own render engine is a good idea if you are going to build something like a game or fundamentaly different experience than a "standard" GUI.
> > 
> > That's a tradeoff that has to be made if you're going cross-platform and want to ensure that the app works correctly on all with the same code.
> > 
> > > you're removing so many essential features that make a good, premium user experience like when content should move at 120Hz (ProMotion), accessibility, slight performance decreases like janks and stutters, higher resource usage.
> > 
> > Since that part of Flutter is implemented in C++, in theory the same experience should be possible. Also, the Flutter shells all implement the platform's accessibility API (I checked). The native UI of every platform doesn't do any different magic than drawing its widgets with some kind of rendering API (OpenGL, Metal, whatever).
> > 
> > > Also, last time I tried Flutter desktop, it was hard capped at 60hz
> > 
> > That was fixed a while ago. Flutter is in very active development, especially for the desktop platforms.
> > 
> > > That means the default UI is material UI, and I seriously highly despise material UI.
> > 
> > There are alternatives:
> > 
> > - [https://pub.dev/packages/macos\_ui](https://pub.dev/packages/macos_ui)
> > - [https://pub.dev/packages/fluent\_ui](https://pub.dev/packages/fluent_ui)
> > - [https://pub.dev/packages/chicago](https://pub.dev/packages/chicago)
> > - [https://pub.dev/packages/yaru\_widgets](https://pub.dev/packages/yaru_widgets)
> > 
> > So, you don't have to write your own widgets in another style, just use one of the existing third party libraries.
> > 
> > > The Dart language and Flutter design system has a lot of haters and lovers as usual, but I really dislike the idea of having yet another TypeJavaReactClassScript language.
> > 
> > Yeah, I'm also not a big fan of Dart. It has all of those issues Rust set out to fix. Interestingly, in the last Dart release they added pattern matching that looks exactly like the one in Rust (down to using the same syntax), and it also now has sound nullability like Rust. Maybe they're seeing the light there and are working on it.
> 
> **Phoxot** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugriac/) • 2023-08-02
> 
> Exactly this, I've been on many projects and used all sort of frameworks over the years. Used WinForms (VBA, C#), WPF (C#), Qt (C++) and some custom C++ solutions. But since a year or so I've been developing apps using Flutter and it has been nothing but great so far. The amount you can achieve in short periods of time is amazing yet keeping the option alive for a Rust or C++ bridge (for desktops) is what I've been looking for.
> 
> **LiterallyHitlar1** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhenvk/) • 2023-08-02
> 
> qmetaobject works very well with rust
> 
> **Im\_Justin\_Cider** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jughfmi/) • 2023-08-02
> 
> How did flutter overcome the three decade headstart? Is it just Google being google? And if so, do you think flutter was built with any passion at all? Is that even important?
> 
> > **GOD\_Official\_Reddit** • [9 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugnlp3/) • 2023-08-02
> > 
> > IMO google being google essentially. When you have access to the chrome team who have those decades of experience writing rendering engines that run on anything and the Android team who not only have the experience but also write the os it’s a bit of a cheat code.
> > 
> > I would say it was definitely written with passion, the ability to write apps that run anywhere in a performant way is such a grail for mobile devs and the alternatives for that are honestly horrible to work with, then extending that out to desktop is even more icing on the cake.
> > 
> > **anlumo** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugtpvg/) • 2023-08-02
> > 
> > First off, Qt has kinda stagnated. It doesn’t take three decades to get a usable UI framework. I think 5 to 10 years is enough, and Flutter 1.0 was released 6 years ago. They also use Skia for rendering, which gives them a big head start.
> > 
> > Google operates as a conglomerate of several small independent companies, but each with infinite budget (until it gets killed when there’s no significant output after some time). I think this leads to a certain level of passion, because the project has to defend itself against other projects within the company, for example the native Android UI framework and Kotlin in this case, but they’re still free to use other team's products, for example Dart and Skia.
> > 
> > > **pjmlp** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhnwsv/) • 2023-08-02
> > > 
> > > Any competition to Qt, also needs to take stuff like QtCreator and Qt Design Studio into account.
> > > 
> > > The C++ code might have kind of stagnated, yet there is plenty of stuff on the QML and tooling area.
> > > 
> > > > **anlumo** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juho9bg/) • 2023-08-02
> > > > 
> > > > Since Qt's free license is not compatible with my commercial projects, it's not on the table anyways, and thus no UI framework has to compete with any of its features.
> > > > 
> > > > That said, there's [FlutterFlow](https://flutterflow.io/), which looks promising based on my limited testing.

> **\[deleted\]** • [0 points](https://reddit.com/) • 2023-08-01
> 
> > Remember that you only live once.
> 
> I get enough lifetime analysis from the compiler, thank you very much 😄
> 
> > **\[deleted\]** • [20 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhv2ks/) • 2023-08-02
> > 
> > > Remember that you only live once.
> > 
> > I get enough lifetime analysis from the compiler, thank you very much 😄
> > 
> > **\[deleted\]** • [13 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juesbbg/) • 2023-08-01
> > 
> > Good advice, thanks

> **ryanmcgrath** • [34 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juepew8/) • 2023-08-01
> 
> Can you describe what you're after with "system tray only"? For something of that general level I've found it's not that bad to maintain `n` GUI codebases, since these (often) aren't as complex.
> 
> There is realistically no native GUI that cannot be done via Rust, but it does often require you understanding the native layer well enough to interface with it. Understanding the "big 3" of macOS/Windows/GTK|KDE isn't as common as one might expect but if you've got it like that then I'd personally say it's fine.

> **physics515** • [64 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufg1k5/) • 2023-08-02
> 
> Not really an answer to your question but I've been working on an app in Tauri recently and I've been blown away by both how easy it is and how performant it is compared to electron. Damn near native performance. Of course, I'm keeping as much code on the rust side as possible and just using Tauri for UI so it really is native for the most part.
> 
> Full stack if you're interested: Tauri Commands (backend) Nuxt (front-end framework) Tailwind (CSS framework)
> 
> Development is so incredibly fast!
> 
> > **\[deleted\]** • [0 points](https://reddit.com/) • 2023-08-02
> > 
> > Is it really the fault of Electron, or of poorly written apps? For example, VS Code uses Electron, but at least on my machine it is much more snappy than any other IDE (Visual Studio, IDEA) - even with plugins.
> > 
> > Electron does have some overhead, but I have often seen apps built with e.g. WPF perform much worse. Some developers completely disregard optimization, naively re-render the whole page all the time and allocate thousands of GC'd objects every second, while others apply reasonable best practices to a good framework (like React), so that any change in state only compares a few pointers in VDOM and changes styles in a small section of the screen. It's also possible to achieve good performance in vanilla JS, although it gets more difficult as your app starts displaying multiple screens and highly dynamic lists - modern frameworks make these scenarios much more maintainable without significant loss of performance.
> > 
> > I would love to see a performant React-like framework that runs purely native Rust code, but people sometimes forget that web technologies have converged on some pretty awesome things in the past few years, and V8's team managed to squeeze a lot of performance of the poor old JavaScript runtime. Chromium (and, by extension, Electron) has one of the most impressive JITs out there. I think that Electron or Tauri and the web ecosystem are still a good fit for UI-heavy apps of reasonable complexity.
> > 
> > > **smthamazing** • [9 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugmda9/) • 2023-08-02
> > > 
> > > Is it really the fault of Electron, or of poorly written apps? For example, VS Code uses Electron, but at least on my machine it is much more snappy than any other IDE (Visual Studio, IDEA) - even with plugins.
> > > 
> > > Electron does have some overhead, but I have often seen apps built with e.g. WPF perform much worse. Some developers completely disregard optimization, naively re-render the whole page all the time and allocate thousands of GC'd objects every second, while others apply reasonable best practices to a good framework (like React), so that any change in state only compares a few pointers in VDOM and changes styles in a small section of the screen. It's also possible to achieve good performance in vanilla JS, although it gets more difficult as your app starts displaying multiple screens and highly dynamic lists - modern frameworks make these scenarios much more maintainable without significant loss of performance.
> > > 
> > > I would love to see a performant React-like framework that runs purely native Rust code, but people sometimes forget that web technologies have converged on some pretty awesome things in the past few years, and V8's team managed to squeeze a lot of performance of the poor old JavaScript runtime. Chromium (and, by extension, Electron) has one of the most impressive JITs out there. I think that Electron or Tauri and the web ecosystem are still a good fit for UI-heavy apps of reasonable complexity.
> > > 
> > > > **\[deleted\]** • [0 points](https://reddit.com/) • 2023-08-03
> > 
> > **GolemancerVekk** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugee80/) • 2023-08-02
> > 
> > I've never understood why API bindings into Qt or GTK for JavaScript never took off.
> > 
> > > **althahahayes** • [7 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugftue/) • 2023-08-02
> > > 
> > > There's a project called `nodegui` which provides widgets from Qt.
> > > 
> > > But overall, making Qt bindings is pretty difficult, it's a C++ library, with a lot of C++ idioms. You can't FFI with C++ templates, you need to handle inheritance, you need to handle overloads... To add insult to injury, Qt has its own preprocessor called `moc` that generates metadata and is essential for things like signals/slots to work.  
> > > You also need to be careful about ABI, Qt compiled with MSVC won't work with a program compiled with MinGW.  
> > > And building it is also a big pain (at least on windows).
> > > 
> > > As for GTK, since it's written in C, there are plenty of bindings for it. But the last time I tried it, it looked very unative on windows, and the build process was also annoying (Need visual studio, cmake, meson, ninja, python, pkg-config, msys2...)
> > > 
> > > > **theingleneuk** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugrbl1/) • 2023-08-02
> > > > 
> > > > What does un-native look like on Windows? Good?
> > > > 
> > > > > **althahahayes** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugw9om/) • 2023-08-02
> > > > > 
> > > > > Looks like a gnome app with CSD instead of the win32 title bar that almost every other program uses.  
> > > > > Admittedly, themeing on windows is a huge mess: some default programs use the windows 7 theme while others use the windows 10 one.  
> > > > > I personally consider that whatever theme win32 uses to be the native one.
> 
> **Nzkx** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jujhin8/) • 2023-08-02
> 
> The problem I found with this approach is everything that you need to transmit between Rust or C++ had to be serialized for the browser, akin to "backend" and "frontend" separation.
> 
> Imagine someone want to write a large computation with Tauri and have a GUI at same time. Everything is calculated on Rust/C++ side in the backend.
> 
> You have to serialize the result of that computation and transmit into browser-side, and for some application it's not possible to move memory like that without noticeable jank. If you want a comparison, imagine transmitting 100 megabytes of JSON over a network for example.
> 
> Or maybe I'm wrong and I don't understand how it work and it's fast enough to do that in less than 1ms, but for me this was my concern with theses browser engine. The need to serialize everything. It's good for some use case, but not for all use case (I guess that's part of why we don't see theses browser engine shipped inside game, at least not that much).
> 
> > **physics515** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jujpofu/) • 2023-08-02
> > 
> > I'm not sure I really understand your concern. I've never heard of any circumstance where someone needed to generate a UI from 100mb of JSON. Any modern frontend framework (Vue, React, etc) will most likely force you into breaking that down into more logical chunks anyway (assuming you are following best practices).
> > 
> > If you are saying that you want to do some computation on the data then there would be no need to send it to the frontend anyhow, so just keep it all in rust.
> > 
> > Edit: I guess I'm coming at it from a component frame work mindset. Meaning if I have a 100mb of data on the rust side, each component in the JavaScript framework is going to request whatever is relevant to it.
> > 
> > So I would write Tauri commands to extract the relevant bit from the 100mb of data and only serialize that bit. So the 100mb of data gets sent as 100 x 1mb requests processed on separate threads async. Maybe it takes more than 1ms but my eyes cant perceive 1ms so it doesn't matter on a frontend as far as I'm concerned.
> 
> **\[deleted\]** • [\-7 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugezdb/) • 2023-08-02
> 
> trees fanatical unique onerous decide rich zonked squalid wakeful employ
> 
> *This post was mass deleted and anonymized with* [*Redact*](https://redact.dev/)
> 
> > **AryaDee** • [24 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugi525/) • 2023-08-02
> > 
> > I may be misunderstanding you, but if you're saying Tauri is heavy because it relies on webtech, I disagree. I have a [small app](https://github.com/aryadaroui/Favy) I'm making for organizing my photos, and it's about 7 MB storage, and about 30-40 MB of memory (increases with more photos loaded, but that doesnt count)
> > 
> > > **mrjackwills** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugjxx6/) • 2023-08-02
> > > 
> > > I was just about to start a new Tauri app for this very purpose, but yours looks great. I have some ideas about tagging etc, so I might be able to help (and also submit some PRs)
> > > 
> > > **0\_djek** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juj7dk1/) • 2023-08-02
> > > 
> > > I have answered some of the issues, could you check it and respond to them?

> **\_xiphiaz** • [11 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufhj69/) • 2023-08-02
> 
> Not quite what you’re after but I just built a small cross platform desktop app using Kotlin KMM and it was crazy how quickly I got something decent looking up and running. And Kotlin is a joy to work with, like Rust.
> 
> > **Barafu** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juh35do/) • 2023-08-02
> > 
> > Never looked that way. Can you build a reasonable GUi desktop app for Win&Lin with it?
> > 
> > > **yektadev** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/julpaan/) • 2023-08-03
> > > 
> > > That's what I've been doing for the last two years. It's a fast and pleasant experience. Jetpack Compose learnt a lot from Flutter and is overall built on the same set of ideas. And then we have JetBrains, coming to transform all that effort put into Android's Jetpack Compose and turn it into a multiplatform technology (thanks to Kotlin Multiplatform). I chose Compose because Kotlin appeared to be a more "lovable" language than Dart for me.

> **Meloentjee** • [9 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugd78q/) • 2023-08-02
> 
> Not an awnser to your question but ive been working on a directx11 game engine for the last couple of months but i discontinued the project. I used the win32 crate. It has been an terrible experience compared to C++.
> 
> There is no documentation at all and you're very dependent on C++ sources. You will have to translate the C++ code to rust code.
> 
> Because win32 is an unsafe crate and rust manages your memory, you'll encounter a lot of memory issues.
> 
> Wont recommend the win32 crate to anyone.
> 
> > **sweating\_teflon** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugzbqw/) • 2023-08-02
> > 
> > Sounds like fun. Maybe it's time someone creates a Rust version of MFC?
> > 
> > > **Pangocciolo** • [5 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jul9nwx/) • 2023-08-03
> > > 
> > > > MFC
> > > 
> > > Jesus
> > > 
> > > > **sweating\_teflon** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jum6ikt/) • 2023-08-03
> > > > 
> > > > Oh, if you go biblical, it'd be JFC but that would be for Java. Rust version would be called RFC which brings in another bunch of problems...

> **rusty-apple** • [8 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufs4ej/) • 2023-08-02
> 
> A different kind of answer but you can actually use Flutter & it has system tray plugins like sys\_tray and tray\_manager I don't think anything more is needed than that

> **LetrixZ** • [8 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufzrvi/) • 2023-08-02
> 
> Tauri can do native system tray stuff I think. And you don't have to use any JS framework to render a window.
> 
> > **reactiveme** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juh13pq/) • 2023-08-02
> > 
> > Yap, you can, and you can use any framework or no framework. It's really just html and js. The cool part is that you can do most things in rust.

> **Barafu** • [8 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juh25uo/) • 2023-08-02
> 
> I am using C++ and Rust interchangeably at work. C++ can be almost as convenient as Rust, but only if multiple conditions are met:
> 
> - Modern C++, at least C++17 is used.
> - Everyone knows how to use it, and don't write "C with classes"
> - Safety coding rules are developed, written out and *enforced for everyone*.
> - Everyone uses the same OS as a target hardware, and the same compiler.
> 
> It is a big chore, actually. A lot of manual control of what Rust controls itself. If people have 2-3 years of random C++ experience, teaching them Rust is *faster* than teaching them a good form of C++.
> 
> > **oleid** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jukvz79/) • 2023-08-03
> > 
> > And even C++17 is a pita, as certain quality of life things are not possible. The little things like `emplace_back` for structs without any manually defined conductors or views let alone algorithms on views, which are only available in C++23.
> > 
> > If one starts C++ projects today I wouldn't bother starting below C++20.

> **teerre** • [15 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufmxt1/) • 2023-08-02
> 
> For work I write quite a bit of Qt. I would never choose Qt if I could. I would choose imgui. Which maps relatively well to egui in Rust.
> 
> But this highly depend on what you're doing. When you say "system tray app", it seems you don't need a gui library at all.
> 
> Similarly, if you GUI is a button and some fields, nothing matters. Anything you do will be ok. But if your app is a complex set of multiple sub apps rendering different completely complex widgets, then it's totally different. Same goes for look and feel, do you need a native look? Do you need a custom look (decoration, windowing etc)? If yes, then choosing something like egui will have you writing shaders, is that a problem?
> 
> In summary, without more details, it's hard to say if the language choice makes a difference.

> **dobkeratops** • [7 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhenpv/) • 2023-08-02
> 
> I think of rust as a \*systems\* language (like C,C++,Zig,JAI) rather than an \*application language\* (C#, Swift, Java)
> 
> C++ happens to have a better ecosystem than rust because it has a head start of a couple of decades; however even C++ isn't exactly 'good' at this task. I remember a co-worker commenting .. "there's no good way of doing UI in c++ .. microsofts solution was to make C#"
> 
> the analogous situation in games is engine code vs gameplay code. The solution with C++ engines has been to combine it with a second slower but higher productivity language, or no-code tools. Rust would be in the same boat IMO.
> 
> having said that i think rust should be better than C++ due to its build system, macros, and enum/match, but in practice the established C++ libraries is a bigger factor, and going through rust bindings to C++ adds friction that negates rusts advantages.
> 
> I'd guess the conclusion would be the same as for games .. only use Rust if you're willing to work on the frameworks - contribute to Rust GUI libs plugging gaps as you find them, as well as working on your app. It will take longer to do, but it will be more satsifying and you'll be bringing more to the world.
> 
> > **\[deleted\]** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhhjpc/) • 2023-08-02
> > 
> > Yeah I agree with that for sure. The thing is that my problem space is essentially a systems language problem, dealing with packet capture and packet crafting. For presentation layer, I'd love to provide bindings for a native SwiftUI app, a Windows C# app and a Linux something app (Vala idk). But that is a huge overhead, and as a spare time project, it's just not worth it. That's why my current plan is making my Rust desktop app system tray based and the UI will be elsewhere, cloud based, where the Rust desktop app will be communicating with my Rust websocket server, completely avoiding platform specific UI and also avoiding UX-degrading cross platform solutions.
> > 
> > > **pjmlp** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhpvnu/) • 2023-08-02
> > > 
> > > Not to talk you away from Rust, only to make the remark that there is plenty of systems stuff in modern .NET, regarding language and runtime features for stack allocation, allocation free code, low level unmanaged pointers, arena like resource management,...
> > > 
> > > > **\[deleted\]** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhs730/) • 2023-08-02
> > > > 
> > > > I did quickly evaluate C# actually, since I use it professionally at server-side, but I found that for a background service it's just a bit too resource heavy. The nature of the application is also to process packets as quickly as possible, and a garbage collector is not the right tool for the job here. I have not looked into arena allocators or stuff like that, and I don't see any reason to duct tape the .NET framework into a high-speed C# prototype when I see Rust as a better fit from the start. I'd like to avoid running higher level languages on personal devices as much as possible, and I personally dislike the C#/Java way of writing code, e.g. the "everything is a class" mindset. Additionally, I really dislike Microsoft products and their user experience so naturally I'd like to stay far away from what they use and the mindset behind those tools.
> 
> **pjmlp** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhpezp/) • 2023-08-02
> 
> > "there's no good way of doing UI in c++ .. microsofts solution was to make C#"
> 
> Yes there are, they are called C++ Builder and Qt.
> 
> As for C# and .NET, if you ask WinDev people, it is all about MFC, WTL, UWP and more recently C++/WinRT. All of them more clunky than C++ Builder and Qt, however when sometime comparable to them was created (C++/CX), they managed to kill it from the inside.
> 
> To make a point of how they think, lets pick the famous Hilo sample for Windows Vista/Windows 7, out of the ashes from Longhorn, where they managed to sabotage the .NET effort. The documentation asserts,
> 
> > The rich user experience of Windows 7 is best accessed through a powerful, flexible language, and that means C++: by using C++ you can access the raw power of the Windows 7 API. To build the Hilo sample applications, all you need is Visual C++ Express and the Windows 7 SDK, both of which are available as free downloads.
> 
> [https://github.com/microsoft/VCSamples/blob/master/VC2013Samples/Hilo/Developing%20Hilo.pdf](https://github.com/microsoft/VCSamples/blob/master/VC2013Samples/Hilo/Developing%20Hilo.pdf)

> **orfeo34** • [9 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jug5jlr/) • 2023-08-02
> 
> Gtk binding for Rust is fine.
> 
> > **Shnatsel** • [16 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugtrfp/) • 2023-08-02
> > 
> > GKT is difficult to build for anything but Linux, and has long-unresolved bugs on Windows.
> > 
> > They are also [about to drop CI for Mac](https://www.phoronix.com/news/GTK-macOS-Back-Seat), making it so that it's only guaranteed to work on Linux, leaving other platforms in limbo.
> > 
> > **\[deleted\]** • [\-6 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugwmym/) • 2023-08-02
> > 
> > Thanks, but I'm not looking to build a media player out of the early 2000s :). /s
> > 
> > > **Narishma** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhaw5d/) • 2023-08-02
> > > 
> > > What does that even mean?
> > > 
> > > **tauon\_** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhsbk2/) • 2023-08-02
> > > 
> > > i'd rather you say an actual bad thing about gtk (there are many) instead of whatever you meant by that

> **jaskij** • [27 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juenkhb/) • 2023-08-01
> 
> Honestly? I wouldn't use either.
> 
> IMO your choices are either web-based stuff like Electron, or a cross-platform C# framework like Avalonia or MAUI.
> 
> > **biglymonies** • [33 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufp52q/) • 2023-08-02
> > 
> > I have a really popular Electron app. I would never ever recommend someone use it for anything. Tauri is a much better alternative if the features and security restrictions support your use case.
> > 
> > > **lspwd** • [9 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juftza9/) • 2023-08-02
> > > 
> > > I haven't used Tauri, but imo programming for inconsistencies between WebViews sounds like an absolute nightmare. It sucks electron is so huge but shipping with a consistent version of chromium is *really* nice for developer experience. Plus it supports so much more than a WebView does. It comes down to what the app is and who's funding it. Personal project? Go at it? Large company? Electron is nice because any front end engineer can hop in and PMs are happy that things move rapidly.
> > > 
> > > Again haven't used it, but Dioxus looks neat.
> > > 
> > > > **biglymonies** • [10 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufv2n3/) • 2023-08-02
> > > > 
> > > > The functionality between the platform webviews is pretty extensively tested with Tauri tbh, and for any frontend inconsistencies you can use a service like browserfy to perform automated tests. That with some run-of-the-mill polyfills and you're almost guaranteed a consistent experience across all targets.
> > > > 
> > > > The inconsistencies between Electron versions is a bigger nightmare than getting things to render properly in WebKit/WebView2/etc lol. Updating deps on my app oftentimes requires pretty heavy refactoring.
> > > > 
> > > > TIL about Dioxus - I'll give that a try for a disassembler I'm writing. Thanks!
> > > > 
> > > > > **lspwd** • [5 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jug27xn/) • 2023-08-02
> > > > > 
> > > > > Maybe latest webviews are mostly at parity, but is everyone on latest - I'm not down to get reports of someone on an old os version. Those bugs suck to repro (and know to test for, unless you're doing image diffing tests)
> > > > > 
> > > > > Also, web dev against safari is already garbage, I wouldn't expect a macOS WebView to be any better.
> > > > > 
> > > > > I would love to use Tauri though, I like the idea of it. I wrote something similar to electron-redux for Tauri and wish I could use it with something real
> > > > > 
> > > > > I just watched/skimmed this talk from may of this year and learned about Dioxus, there's a lot more though! [https://youtu.be/XjbVnwBtVEk](https://youtu.be/XjbVnwBtVEk)
> > > > > 
> > > > > Im following dev of blitz [https://github.com/DioxusLabs/blitz](https://github.com/DioxusLabs/blitz) to see when that gets pulled in... Or something new someday that uses servo...
> > > > > 
> > > > > > **jkelleyrtp** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jui6cxu/) • 2023-08-02
> > > > > > 
> > > > > > We will be pulling in servo soon. Stay tuned :-)
> > 
> > **jaskij** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufq1pj/) • 2023-08-02
> > 
> > I was using Electron as an example of web based tech. Tauri is still web based. It just uses the native webview of the OS (how does that even work on Linux?), instead of bundling one like Electron. This is a big step in the right direction, fair. But it doesn't change the fact that they're fundamentally the same, using an HTML frontend. Also it still uses JS, which is the big issue for me personally.
> > 
> > > **biglymonies** • [7 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufs3bc/) • 2023-08-02
> > > 
> > > That's all perfectly fair - I didn't mean to make assumptions. I'm just very passionate about steering people away from the same mistakes I made lol
> > > 
> > > > **jaskij** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufsa7d/) • 2023-08-02
> > > > 
> > > > Fair enough. And to be clear - Tauri is much better than Electron simply because it uses the native webview, which gets regularly updated. That much isn't even in question.
> 
> **CodeDead-gh** • [12 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufw048/) • 2023-08-02
> 
> Most modern OS's have a WebView. Linux generally uses one based on WebKitGTK. Tauri will generally use that in combination with wry being a small layer on top. Tao is used to create and manage windows, which uses gtk3 on Linux. Tao + wry = tauri. That's how it works on Linux and other platforms (soon including mobile platforms), by combining the system's webview (with a small layer on top) with a windowing layer that is native to the platform.
> 
> When writing Tauri apps, best practices dictate that one should write the UI logic in JS/TS/WASM and you put the intensive work in the Rust backend that runs natively on the system.
> 
> The performance impact of using JS/TS/WASM only for UI-related things is negligible when most major bottlenecks in GUI apps are IO, network, CPU bound. That way, the UI remains responsive even when intense work is being performed in the Tauri / Rust backend (UI responsiveness being something that you should strive for regardless of using Tauri, Qt, Electron, ...).
> 
> If your app isn't that intensive, one might even wonder 'why' a desktop app is really necessary, if it runs in the browser already without needing native functions or any particularly hard/blocking work, a PWA that users can 'install' without the need for system webviews or native calls, should already suffice.
> 
> Using something like Tauri, is currently one of the easiest ways for developers to create tiny, cross-platform applications, combining the features of the web, that don't need a lot of disk space or RAM and that still perform really well considering the intensive work is being done in Rust on the native platform but it is true that combining a project using HTML, CSS, JS/TS with Rust code is perhaps more difficult to manage since you can have code in multiple languages that need to be maintained, but one could opt for using something like 'yew' in the front-end which is also entirely made using Rust.
> 
> To top it all off, Tauri is entirely open-source, doesn't rely on Google/Microsoft, has very little requirements in terms of dependencies, has been supported for years, does not infringe on user-privacy and has amazing community support, I would not be so eager to write it off that easily in favor of other frameworks. Especially considering a big chunk of today's programmers write code in web-based technologies like JavaScript (that being good or bad, I leave up to you).
> 
> > **jaskij** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufw79x/) • 2023-08-02
> > 
> > Why do I have deja vu? Feels like I got the same reply twice in a row.
> 
> **Barafu** • [0 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juh3qon/) • 2023-08-02
> 
> [MAUI](https://mauikit.org/) is a C++ framework.
> 
> > **jaskij** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juh4uy0/) • 2023-08-02
> > 
> > That doesn't preclude there being a C# under the same name, right? [https://dotnet.microsoft.com/en-us/apps/maui](https://dotnet.microsoft.com/en-us/apps/maui)
> > 
> > Edit: what you linked is called MauiKit, not MAUI
> 
> **stach\_io** • [\-23 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juepmhm/) • 2023-08-01
> 
> Yeah it’s strange seeing someone say they’re not a fan of web based apps. If there are libraries out there that beat the fluidity and versatility of web rendering, I’d love to know.
> 
> > **thepotofpine** • [22 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jueq0es/) • 2023-08-01
> > 
> > Web based apps are the death of low spec computers, discord and Vs code are a memory hog like no other and they run shittily slow.
> > 
> > > **RetoonHD** • [9 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juf7tnw/) • 2023-08-02
> > > 
> > > Those are actually pretty well optimized when we're talking about electron apps. But you're right that it's a lot easier to use gigabytes of memory with electron. But you can also write extremely unoptimized c++ gui's, the one that comes to mind for me is Corsair's iCUE for controlling corsair rgb and making macros. Just checked and it's using 1180MB of ram. You can write more efficient electron apps, its just that not many people do.
> > > 
> > > > **thepotofpine** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugqlw4/) • 2023-08-02
> > > > 
> > > > Fair point. Memory is only have the equation however. For example, full Visual Studio is more responsive than VS code for me, idk how it is for others, but when it comes down to basic typing even, it feels more fluid on Vs than vscode. Of course there's the occasional "not responding" but that's usually limited to things like opening a project not using the UI in general. No doubt Vs probably takes double or triple the memory though lmao.
> > > > 
> > > > Obviously a higher spec setup probably minimises and bandages over the lackluster responsiveness and performance of those bloated web apps - but on a low spec setup, things like pressing a button feel like your rolling your computer up a hill.
> > > > 
> > > > This is all spoken from personal experience idk how it is for the rest of you all.
> 
> **jaskij** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jueq34c/) • 2023-08-01
> 
> I'm not a fan either, but you take what you can get. And because of the skillset in the team at work, we will likely be looking into the second option I mentioned - cross platform C# GUI frameworks.
> 
> > **stach\_io** • [\-3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juerh0j/) • 2023-08-01
> > 
> > That’s about it. Web is tried and established, building basic desktop interpreter was a no brainer. I’d love to see something else achieve the same results but sadly that won’t happen any time soon with the majority of programmers living in web.

> **TedDallas** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufhlcw/) • 2023-08-02
> 
> If we talking C++ here then I’ll toss Lazarus into the fray. It probably is the best cross platform desktop gui designer around. It will run on shit tier hardware. And Indy components will get you what you need in terms of packet manipulation. The downside is the language Lazarus uses is object Pascal (FPC).
> 
> I do wish there was an IDE like Lazarus for Rust.
> 
> > **darthcoder** • [8 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufit5z/) • 2023-08-02
> > 
> > Don't get me started on Indy. They've been sitting on a TLS 1.3 patch for almost two years now.
> > 
> > **sweating\_teflon** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juh0aqa/) • 2023-08-02
> > 
> > An even better language to replace Pascal in Lazarus would be Nim.
> > 
> > And I agree that *nothing* comes close to Lazarus in native GUI development. Even if you have to write some Pascal, which isn't so bad. I'd work on a reliable, easy way to integrate Rust compiled modules into the Lazarus app.

> **No-Software-Allowed** • [4 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jufzrpz/) • 2023-08-02
> 
> Consider if your app really needs a full fat gui framework above the base level operating system APIs. The earliest GUI programs I created were in C against the native win32 API. There is an [official Rust crate for that](https://learn.microsoft.com/en-us/windows/dev-environment/rust/rust-for-windows). The frameworks such as MFC and WinForms made larger applications easier, but were still fairly thin wrappers around the native API.
> 
> I suspect the same to exist for the low level macOS and Linux desktop APIs.
> 
> The core logic can then be shared among the different OS specific front ends.

> **Medium\_Theat** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugof9m/) • 2023-08-02
> 
> Tauri, an equivalent of Electron, which develops App in a web frontend way

> **solidair54321** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhm8p4/) • 2023-08-02
> 
> Rust looks like fun and I'd like to use it more for hobby use. But these C++ replacement languages like D and Rust don't seem to care about cross-platform GUI. So they leave it to end users to develop, who usually build something and then abandon it. I've still not seen anything in Rust that looks OK to me which is why I always go back to C++. My favorite GUI has been JUCE, one reason is because I can easily create custom widgets in that. WxWidgets is Ok, too. I tried to duplicate one of my JUCE applications in Qt once and it was harder so I avoid that. But you can take what I say with a grain of salt because I'm more of a dinosaur that goes back to libraries like ObjectWindows and, forgive me for saying it, MFC (yuk :( ). I never heard of Tauri until I read this thread. I'm not a web programmer and so when I see words like HTML and JavaScript I run the other way, lol.
> 
> > **\[deleted\]** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhtbh7/) • 2023-08-02
> > 
> > I totally get your take! I think Rust's users are mainly in the systems development space, and less so in the application development space, so naturally there will be less focus on things like cross platform development from the language itself. However, I don't think there is anything stopping Rust from having a framework for building cross platform apps, apart from time. C++ is such a mature language and ecosystem spanning from very low level stuff to higher level tasks like application development, so naturally there will be more resources in C++. What I was wondering in my post is how this experience writing a cross platform desktop app in Rust compares to C++ ***today***, but I'm sure in the future Rust will be a nobrain winner in most areas, maybe apart from game development.
> > 
> > **A1oso** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juw3crs/) • 2023-08-05
> > 
> > > But these C++ replacement languages like D and Rust don't seem to care about cross-platform GUI. So they leave it to end users to develop
> > 
> > So, who developed JUCE, WxWidgets and Qt? I don't think it was the C++ committee.
> > 
> > GUI frameworks are almost never created by the same people who develop the programming language.

> **Doddzilla7** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juifp2s/) • 2023-08-02
> 
> Tauri with Trunk will keep you entirely in Rust + wasm land. No js. Any particular reason not to use Tauri? Seems to be the most mature Rust project in this space.

> **Specialist\_Wishbone5** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juifxbx/) • 2023-08-02
> 
> If you're looking at Tauri; there's also dioxus and iced.
> 
> dioxus is react-in-nature (but apparently many times faster than a javascript/nodejs based framework; which is what you'd experience with Tauri). Works for TUI, GL, Web and others from my understanding.
> 
> iced is open-GL like; you draw onto a canvas based on message events (seems similar to QT from my ancient memory) - but is more document oriented (I hear the word ELM a lot - but have no experience).
> 
> My issue with egui is that it's immediate mode. Unless I'm missing something, you're redrawing 60 times a second even when nothing is happening. If you're making a game; that's fine. But if I'm just showing a 1/second "htop" like app, that's overkill and counter-productive to the goal of minimizing system resources. :) For that, something like dioxus or iced (with tinyskia) seems more appropriate - no events means no CPU-wakeups. I think the remaning difference between the two is a "virtual dom" v.s. a direct canvas render - namely dioxus returns "Element" objects with children (identical to web's virtual DOM), and iced is using 'generic' pass throughs of primitive draw calls. So, more efficient PER draw event, but I suspect MORE total draw events per message/dirty. System76 is using iced in their COSMIC GTK replacement.
> 
> Zero personal experience - but am, this week evaluating those two platforms for my own personal project.
> 
> Examples I see, a rotating star in iced (where the canvas redraw per event makes perfect sense; nothing is retained from draw to draw) and a TUI htop like app in dioxus, where 90% of the screen is identical after each redraw or just moved up/down a small amount. Here a virtual-dom diff would minimize the canvas redraw sections.
> 
> There's also Bevy - which is a beloved Entity Component System; but I think that's immediate mode. I DID see a bevy\_dioxus project, which makes mind go blown. :)

> **DavidXkL** • [5 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juet07e/) • 2023-08-01
> 
> Can consider Iced though. Not sure if it fits the use case that you want lol

> **threeseed** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugsi1u/) • 2023-08-02
> 
> I'm in the middle of building an app using Tauri with way too much experience in building Electron, Qt, Flutter etc cross-platform desktop apps as well many Obj-C/Swift apps.
> 
> Tauri is amazing and the epitome of quality for me. It is fast, elegant, well-documented and incorporating features from Electron in a smart and clean way. My UI renders with the same speed as a native Objective-C Mac app but I get cross-platform for free. Only issue is the lack of native controls but these days it isn't a deal breaker.
> 
> For me it goes in order of the quality of end user experience:
> 
> 1. Native apps e.g. Swift/WinUI
> 2. Tauri
> 3. Electron/Flutter
> 4. Qt
> 
> > **\[deleted\]** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugt3fz/) • 2023-08-02
> > 
> > Yup that makes sense. However, I would strongly argue that a Qt program is generally over Electron/Flutter when it comes to end user experience, and possibly Tauri as well seeing as Tauri depends on web tech to render UI. I mean, take a look at huge programs like DaVinci Resolve which is a program I'm an avid user of these days. Good luck trying to create something like that using web-tech or Flutter, and keeping it as smooth!
> > 
> > > **threeseed** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugub2s/) • 2023-08-02
> > > 
> > > I wouldn't be so quick to knock Tauri for using Web Technologies.
> > > 
> > > It is using the native web rendering library which is 3D accelerated and heavily optimised by each OS provider. WebKit on OSX for example underpins many core apps e.g. Mail. And you can take advantage of WASM on the client side.
> > > 
> > > My experience is that it's much faster than QT and Flutter.
> > > 
> > > > **\[deleted\]** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugvjnp/) • 2023-08-02
> > > > 
> > > > Yes I am aware that Tauri doesn't ship its own rendering engine and instead relies on the system's renderer. That's what made me a fan back in the early beta stage. However, native web renderer is still a web renderer. And there is a limit where web tech cannot keep up with a native rendered GUI like the Qt framework. A good example of that must be video editing software for instance, or any professional demanding desktop applications like AutoDesk apps, 3D modelling or similar. All using Qt, and it would be a real pain (and bottleneck) trying to do that in a web site.
> > > > 
> > > > However, when we're talking standard GUI that is supposed to do standard GUI things (inputs, text, pictures, buttons) then yes I agree, Tauri is fantastic and probably the best modern option today.
> > > > 
> > > > Edit: speaking of editors, I tried Microsoft's web based video editor called clip champ, and my experience can simply be summarized as: horrible, laggy, crashing product. Using web tech must seriously have bottlenecked the video editing process by at least 1/3 of my PC's actual potential.

> **Speykious** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jughks0/) • 2023-08-02
> 
> My experience is that after learning Rust I don't want to touch C++ from a mile away, so I don't want to use Qt, GTK or even SDL2/GLFW if I can get away with Winit or something else.
> 
> I also want to make desktop applications (and eventually mobile), but I've been unsatisfied by the currently available and very active Rust GUI frameworks such as Iced and Slint. Maybe try those frameworks and see if it fits your use-case, after all Slint is now a stable crate and has quite a few interesting features (such as a DSL with an LSP plugin for VSCode) and Iced was picked up by System76 for the new iteration of their Pop\_!OS Linux distribution.
> 
> As for me, I'm trying to make my own GUI framework. Well, not right now, I tried a while ago, but soon enough I'm gonna try again and see what I can do.

> **Days\_End** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugmuyz/) • 2023-08-02
> 
> > which, in your opinion, is better for my green field cross platform desktop app with low level ?
> 
> It's not impossible to answer and anyone who doesn't say C++ is doing you a disservice or doesn't understand the current state of Rust libraries. If your goal is to actually make the application go with C++ if you are actually really just tinkering / enjoying yourself then you can go Rust.

> **Viferga** • [\-2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jugtxw5/) • 2023-08-02
> 
> Use another language if you can, neither C++ nor Rust.
> 
> > **\[deleted\]** • [0 points](https://reddit.com/) • 2023-08-02
> > 
> > ASSEMBLY
> > 
> > > **nioh2\_noob** • [3 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhn3sm/) • 2023-08-02
> > > 
> > > ASSEMBLY
> > > 
> > > > **tauon\_** • [2 points](https://reddit.com/r/rust/comments/15fqzp5/comment/juhsv8k/) • 2023-08-02
> > > > 
> > > > JUST WRITE THE BYTES FOR PROCESSOR INSTRUCTIONS INTO A FILE

> **winters-brown** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jujsjgw/) • 2023-08-02
> 
> The win32 is officially ported by windows! I’ve had great success using it in my apps so far
> 
> > **International-Nose19** • [1 points](https://reddit.com/r/rust/comments/15fqzp5/comment/jukkyug/) • 2023-08-03
> > 
> > Win32 development is dead. It was a terrible API. Messages were passed instead of using objects with virtual functions. MFC helped but it was always difficult to do sophisticated things with it because widgets had inconsistencies. It hasn't been ported to any other OS afaik.