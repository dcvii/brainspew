---
title: "Rust vs. GO"
source: "https://itnext.io/rust-vs-go-cc38b7048181"
author:
  - "[[Javier Ramos]]"
published: 2022-04-27
created: 2025-02-17
description: "I’ve been using Go for a while now to build a wide range of applications; at the same time, I’ve been hearing many good things about Rust, so recently I decided to spend time learning Rust. Both…"
tags:
  - "clippings"
---
[

![Javier Ramos](https://miro.medium.com/v2/resize:fill:88:88/1*qo0C-KYJLOQrGrt_uDCU3w.jpeg)

](https://javier-ramos.medium.com/?source=post_page---byline--cc38b7048181---------------------------------------)

[

![ITNEXT](https://miro.medium.com/v2/resize:fill:48:48/1*yAqDFIFA5F_NXalOJKz4TA.png)

](https://itnext.io/?source=post_page---byline--cc38b7048181---------------------------------------)

![](https://miro.medium.com/v2/resize:fit:700/0*7hDOuo8jwIYbFjeW)

Photo by [Jay Heike](https://unsplash.com/@jayrheike?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

## Introduction

I’ve been using [**Go**](https://go.dev/) for a while now to build a wide range of applications; at the same time, I’ve been hearing many good things about [**Rust**](https://www.rust-lang.org/), so recently I decided to spend time **learning Rust**. Both languages, although created to achieve different goals, share many **similarities**. During the last few months I’ve been taking notes to try to wrap my ahead around the use cases where each language would be a better fit. This article is the culmination of this research. **My goal is to compare both languages from different angles and from the different points of view** so anyone regardless of their role can have a complete picture of the similarities and differences of each language.

Both [**Go**](https://go.dev/) and [**Rust**](https://www.rust-lang.org/) are relatively **new** languages (Rust is the new kid on the block) which try to overcome the [**criticisms**](https://en.wikipedia.org/wiki/Criticism_of_C%2B%2B) of **C++,** while sharing similar syntax, both were created with different design goals in mind.

In a nutshell, [**Go**](https://go.dev/) aims to **simplify** the development, making it attractive and accessible to any developer regardless of their experience. It was designed with **multi core processors** in mind simplifying parallel execution of concurrent programs while still be considered a [**general purpose programming language**](https://en.wikipedia.org/wiki/General-purpose_programming_language).

[**Rust**](https://www.rust-lang.org/), in the other hand, is a [**systems programming language**](https://en.wikipedia.org/wiki/System_programming_language) that was created to solve the memory safety issues of C++ and other problems while keeping the amazing **performance** that C++ is famous for.

![](https://miro.medium.com/v2/resize:fit:700/0*bSge7G3v_MznYqem)

Both are great languages that can achieve great **performance** for **concurrent** applications and stream processing but their design goals are quite different. In this article, I will try give you a quick overview of both languages, their **advantages and drawbacks** and review some real word use cases where we will recommend one language over the other.

## Go in a nutshell

[**Go**](https://golang.org/) was created by **Google** and it is [syntactically](https://en.wikipedia.org/wiki/Syntax_\(programming_languages\)) similar to [**C**](https://en.wikipedia.org/wiki/C_\(programming_language\))**.** Its goal was to overcome the unsafe operations present in C*++* by adding [memory safety](https://en.wikipedia.org/wiki/Memory_safety), [**garbage collection**](https://en.wikipedia.org/wiki/Garbage_collection_\(computer_science\)) and [structural typing](https://en.wikipedia.org/wiki/Structural_type_system). It is very easy to learn and simple to use. It was built for multi core machines to maximize parallelism for concurrent programs. It uses very lightweight green threads called [**Go Routines**](https://golangbot.com/goroutines/) for concurrent programming.

> Go compiles quickly to machine code yet has the convenience of garbage collection and the power of run-time reflection. It’s a fast, statically typed, compiled language that feels like a dynamically typed, interpreted language.\[2\]

Go **has a small footprint**, yet it covers many use cases such as microservices, stream processing, CLIs, and much more. Golang provides excellent support for producing binaries for different platforms without having to install Go on the target. Due to it’s small and efficient binary size, it is great for cloud native applications packaged in Containers. Your app container can be package into a [tiny container](https://github.com/GoogleContainerTools/distroless/blob/master/examples/go/Dockerfile) (~8–15MB) that can be deployed in just a couple of seconds, making it a much better option for microservices than the JVM languages. For more information check my article about deploying [**Go Microservices in Kubernetes**](https://itnext.io/grpc-go-microservices-on-kubernetes-bcb6267e9f53).

![](https://miro.medium.com/v2/resize:fit:500/0*YeJo75lO3Goja2z2)

## Go Pros

- **Super fast compiler**, it feels like an interpreted language. Great developer experience. **Fast development process and increased productivity**.
- **Simple and safe**, what I love about GO is that there is usually just one way of expressing problems, this speeds ups the development, code reviews and in general the whole development process.
- Great for both junior and senior developers. It is very **easy to learn and adopt** since it does not require a virtual environment.
- Perfect choice for **cloud native applications and Kubernetes**. Due to the small size, no warm-up times and speed.
- **Concurrency** made easy thanks to [**Go Routines**](https://golangbot.com/goroutines/).
- Great standard library which includes a web server.
- GO can be used in a **wide range of** [**use cases**](http://go-lang.cat-v.org/go-code)**:** CLIs, web applications, stream processing, etc.
- **Low resource usage**. You can run literally millions of Go Routines in a single server. It uses very little RAM and CPU compared to the JVM making it much **cheaper to run**.

## Go Cons

- It’s **not concise** and it’s hard to keep the code DRY.
- **Too simple**, basic things like Generics are not available in Go, although they will be [added soon](https://blog.tempus-ex.com/generics-in-go-how-they-work-and-how-to-play-with-them/).
- It’s a relatively **new language** with not many libraries or tutorials.
- [**Dependency management**](https://medium.com/@khorlee/dependency-management-in-go-lang-using-go-commands-7900a7b2f760) **is a bit counter intuitive** and hard to manage but it has improved since the addition of `go mod` . The good news, is that `go mod` is part of the language and not a separate project like `sbt`in Scala, although `sbt`is much more powerful.
- [**Error Handling**](https://blog.golang.org/error-handling-and-go) **is cumbersome**.
- Not as elegant, powerful and flexible compared to Rust.
- **A bit immature** compared to **C++.**

## Go Use Cases

- **CLIs and scripts**: Most of the CLIs like *kubectl* use Go.
- **Web Applications**. Since it is highly concurrent and does not require much resources, it is perfect to handle HTTP requests.
- **Stream Applications**. Go can process millions of events extremely fast using Go routines. It is a competitor of Akka streams in Scala.
- **Microservices**. Due to the small size, speed and monitoring capabilities, Go is a great choice for cloud native microservices.
- **Serverless and cloud applications**. Go is a perfect choice for [Serverless functions](https://cloud.google.com/functions/), specially in Google Cloud.

## Rust in a nutshell

[**Rust**](https://en.wikipedia.org/wiki/Rust_\(programming_language\)) is also a **new** **language** which was started back in 2006 in [**Mozilla**](https://www.mozilla.org/en-US/about/) but it did not reach the first stable release until 2015. Rust has grown in popularity since its release, specially in the last 5 years with many companies such [**AWS**](https://firecracker-microvm.github.io/), Microsoft, [Facebook](https://serokell.io/blog/rust-companies), Mozilla, [Dropbox](https://www.dropbox.com/) or [Cloudfare](https://github.com/cloudflare). Rust has been voted the *“most loved programming language”* in the [**Stack Overflow**](https://en.wikipedia.org/wiki/Stack_Overflow) Developer Survey every year since 2016, no other language has ever achieve that, hence its popularity

> **Rust** is a [multi-paradigm](https://en.wikipedia.org/wiki/Multi-paradigm_programming_language), [general-purpose programming language](https://en.wikipedia.org/wiki/General-purpose_programming_language) designed for [performance](https://en.wikipedia.org/wiki/Computer_performance) and safety, especially safe [concurrency](https://en.wikipedia.org/wiki/Concurrency_\(computer_science\)).[\[12\]](https://en.wikipedia.org/wiki/Rust_\(programming_language\)#cite_note-15)[\[13\]](https://en.wikipedia.org/wiki/Rust_\(programming_language\)#cite_note-Rust_Project_FAQ-16) Rust is [syntactically](https://en.wikipedia.org/wiki/Syntax_\(programming_languages\)) similar to [C++](https://en.wikipedia.org/wiki/C%2B%2B),[\[14\]](https://en.wikipedia.org/wiki/Rust_\(programming_language\)#cite_note-17) but can guarantee [memory safety](https://en.wikipedia.org/wiki/Memory_safety) by using a *borrow checker* to validate [references](https://en.wikipedia.org/wiki/Reference_\(computer_science\)).[\[15\]](https://en.wikipedia.org/wiki/Rust_\(programming_language\)#cite_note-unsafe-18) Rust achieves memory safety without [garbage collection](https://en.wikipedia.org/wiki/Garbage_collection_\(computer_science\)), and [reference counting](https://en.wikipedia.org/wiki/Reference_counting) is optional.[\[16\]](https://en.wikipedia.org/wiki/Rust_\(programming_language\)#cite_note-19)[\[17\]](https://en.wikipedia.org/wiki/Rust_\(programming_language\)#cite_note-20) Rust has been called a [systems programming](https://en.wikipedia.org/wiki/Systems_programming) language, and in addition to high-level features such as [functional programming](https://en.wikipedia.org/wiki/Functional_programming) it also offers mechanisms for [low-level](https://en.wikipedia.org/wiki/Low-level_programming_language) [memory management](https://en.wikipedia.org/wiki/Memory_management). — [Wikipedia](https://en.wikipedia.org/wiki/Rust_\(programming_language\))

Rust was initially developed to replace *C++* and making it more accessible to developers while maintaining the same level of **performance**. C++ has been around for almost 50 years and it is used for low level programming to develop video games, operation systems, real time systems and much more. The problem with C is that it is difficult to use and, in particular, it is not memory safe creating many of the most famous bugs and security vulnerabilities. C developers need to make sure the program is memory safe which is very difficult to achieve in a production grade application, this means that bugs are often found in production creating huge problems. These limitations gave rise to garbage collected general purpose languages such as Java at the expense on control and performance.

![](https://miro.medium.com/v2/resize:fit:700/1*7wUivtzuk20uMn5qMDbRUw.png)

So, before Rust, programmers had to make the difficult choice between an old and dangerous language (C++) or a slower general purpose language such as Java. As we continue to build bigger and and more complex applications, garbage collected languages start to fall behind in terms of performance since they do not squeeze all the power from the underlying hardware. With the introduction of multi core processors there’s a need to optimise code close to hardware to make faster and cheaper programs.

*So, if Rust is a replacement for C++ why are we comparing it with Go?* Well, in the past 10 years Rust has grown considerably and many libraries and tools were created to improve the developer experience and making it more accessible for developers and expanding the number of use cases where Rust is applicable. This means that Rust has moved from a niche to replace C++ as a systems level programming towards a high performant general purpose language able to compete with Go, Python or Java. Rust takes the performance, low resource consumption and small binaries to the next level compared to Go.

In the front-end, [**WebAssembly**](https://en.wikipedia.org/wiki/WebAssembly) put Rust in the spotlight. [WebAssembly](https://en.wikipedia.org/wiki/WebAssembly) tries to overcome the JavaScript limitations in the browser by creating a high performance applications that run on the browser, Rust is the main language in WebAssembly.

The Rust source code is compiled to native code with help of [**LLVM**](https://llvm.org/) and due to that it’s available on all LLVM supported platforms which makes it very portable but not as much as C. Rust is a truly **open source** project with a very strong and open community which is key to its success and rapid expansion.

## Rust Features

Because Rust is a new language it does not carry the historical weight of other languages such as C++ or Java, this means that it was designed following the best practices and lessons learnt from other languages.

Rust is very **feature rich**, it has a rich syntax and powerful constructs such as traits, powerful [**type system**](https://doc.rust-lang.org/book/ch19-04-advanced-types.html), [closures](https://doc.rust-lang.org/book/ch19-05-advanced-functions-and-closures.html), **generics**, collections, pattern matching, [combinators](https://learning-rust.github.io/docs/e6.combinators.html), options, etc. that you see in other powerful languages such as Scala.

Rust also compiles down to a very small binary, smaller than Go since it does not have a Garbage Collector. You can create Rust applications in a tiny container of less than 10Mb, smaller than Go.

On top of that it has excellent tooling out of the box. [**Cargo**](https://doc.rust-lang.org/cargo/) is probably the best package manager out there with great support for mono repositories. It is fast, reliable and easy to use. The compiler is awesome, the messages are very clear and most of the time it tell you exactly what you need to do.

My second favourite feature is [**Zero Cost Abstractions**](https://docs.rust-embedded.org/book/static-guarantees/zero-cost-abstractions.html) which is extremely powerful. This means that you can create abstractions to develop easy to use APIs and libraries while keeping the same performance, the compiler will parse your code and translate it to high efficient code that does not incur any overhead. This means that you can use higher-level programming concepts, like generics, collections and so on but they will not come with a run-time cost, only compiler time cost so you can keep your code clean and DRY while still getting maximum performance.

Rust **type system** is also extremely powerful and similar to other languages like **Scala**. Rust supports [**Algebraic data types**](http://blog.madhukaraphatak.com/rust-scala-part-4/) **(ADTs)** thanks to its powerful `enums` and also supports advance [**pattern matching**](https://doc.rust-lang.org/book/ch18-00-patterns.html). These features are usually only available in high level functional programming languages and Rust brings these advanced features to low level programming.

But the most **innovative** and **unique** **feature** that sets **Rust** apart from other languages is the [**Ownership Model**](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html) which is what allows Rust to be memory safe at compile time allowing you to write high efficient code which is memory safe without the need to explicitly allocate and de-allocate memory.

Before Rust, you had to choose between low level programming languages where you are responsible to manage memory and make sure it is safe or use a garbage collected language such as Java or Go which incurs performance degradation and larger binary sizes. Rust introduces a new paradigm for memory safety at compile time.

> ***Ownership*** is a set of **rules** that **governs how a Rust program manages memory.** All programs have to manage the way they use a computer’s memory while running. Some languages have garbage collection that constantly looks for no-longer used memory as the program runs; in other languages, the programmer must explicitly allocate and free the memory. **Rust** uses a **third** **approach**: memory is managed through a system of ownership with a set of rules that the compiler checks. If any of the rules are violated, the program won’t compile. None of the features of ownership will slow down your program while it’s running. — — [https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)

In a nutshell, these are the rules:

- Each value in Rust has a variable that’s called its *owner*.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

With these 3 simple rules, the Rust compiler can perform its “magic” and make sure your program is safe and that there will be no surprises in production.

While **Go** solved the memory safety issues using a garbage collector which introduces overhead, **Rust** decided to use this new model in order to create smaller and faster programs.

The main issue with this new model is that **it takes time to get use to** it, as a developer you need to spend time to understand this model very well to avoid endless hours of frustration, this is why Rust learning curve is much higher than other languages such as Go, but once you get use to this new model, you can write programs almost as fast as other languages.

## Rust Pros

- Extremely **fast** and **efficient.**
- **Feature Rich**: closures, pattern matching, collections, generics, etc.
- Concise and easy to read.
- [**WebAssembly**](https://en.wikipedia.org/wiki/WebAssembly) support.
- [**Cargo**](https://doc.rust-lang.org/cargo/) is an excellent package manager. Much better dependency management compared to Go.
- It is compatible with C and can interact with existing C programs.
- Truly **open source** with a vibrant community.
- [Low energy consumption](https://thenewstack.io/which-programming-languages-use-the-least-electricity/) and low cost.
- Excellent growth and increase in popularity.
- Great **Error handling**, specially compared to Go.
- **Very small binary size**, smaller than Go since it does not have a Garbage Collector.
- Fast Compiler, but a bit slower than Go.
- **Low resource usage** but that depends on how you build the program, but in general it will use less than Go since memory is free as the program runs and not by the Garbage Collector.

## Rust Cons

- **Immature**, still very new. There are not many production grade applications running in production, although this is growing at a fast rate.
- A bit **difficult to learn**, in particular the **ownership model** takes some time to get used to it.
- It takes longer to write Rust programs than other languages such as Go, this is because you need to follow the strict rules set by the compiler.
- **No native support for concurrency**, asynchronous programming and green threads like in Go. This is by design, Rust has basic support for operating system threads but for real world async programming you need to use libraries. The [**futures-rs**](https://github.com/rust-lang/futures-rs) library includes the foundations for zero cost async programming. It includes key trait definitions like `Stream`, as well as utilities like `join!`, `select!`, and various futures combinator methods which enable expressive asynchronous control flow. There are also many libraries and engines available for concurrent programming being [**Tokio**](https://tokio.rs/) the most famous and powerful one.

## Rust Use Cases

- **CPU** **intensive** applications such as games, operating systems, etc.
- Embedded Systems
- Application Runtimes. For example, the creator of Node.js has created [**Deno**](https://deno.land/) as the new generation of JavaScript runtime, this is written in Rust.
- **Microservices: APIs** such as **REST** end points. Rust has some of the **fastest web frameworks** such as [**Actix**](https://actix.rs/).
- [**WebAssembly**](https://en.wikipedia.org/wiki/WebAssembly) to execute efficient code in the browser. It can also be used to write high efficient [filters](https://istio.io/latest/docs/concepts/wasm/) in a service mesh such as [**Istio**](https://istio.io/latest/docs/concepts/wasm/).
- [Web Development](https://yew.rs/)
- Cryptocurrencies.

Because of its complexity I wouldn’t use Rust to create CLIs and simple scripts but this is possible.

## Rust vs GO

In short, these two new languages are great and perform better than interpreted or JVM based languages and use less resources.

However, each language was created to serve a different **purpose**.

**Go** aims for **simplicity** and easy to use. It is a [**general** **purpose**](https://en.wikipedia.org/wiki/General-purpose_programming_language) language. This is great for small projects such as microservices and for DevOps tools. It also provides a very **simple** **concurrency** model built-in in the language allowing you to write high performance code is a very simple way. This makes Go a very powerful language and it is the key of its popularity. In a manner of hours you can develop a production grade microservices. Go can be applied in a wide range of use cases from CLIs to web applications.

**Rust** in the other hand is a [**systems programming language**](https://en.wikipedia.org/wiki/System_programming_language) focused on performance, low resource usage and low level details. While Go just borrowed some of the C syntax to create a general purpose language, Rust aims to replace C++ entirely by creating a simpler and newer programming language. Furthermore, Rust [zero cost abstractions](https://docs.rust-embedded.org/book/static-guarantees/zero-cost-abstractions.html) feature and amazing [build system](https://doc.rust-lang.org/cargo/reference/workspaces.html) allowed developers to create easy to consume but still high performant libraries to use for general purpose tasks such as REST APIs, stream processing and much more allowing Rust to compete with Go.

While Go is used mainly for simple microservices, Rust can be used to build complex software with millions of lines of code. Furthermore, Rust can be used on embedded devices, on edge or in WebAssembly; environments where Go has limited support.

## Performance

Generally speaking **Rust will outperform Go**, but not by much and it will vary depending on the use case, this is because of the garbage collector. Depending on how often the **GC** runs the results may change. This is a drawback in Go: **predictability**. Although the performance differences may not be huge, Rust performance is predictable.

You can find some initial comparison [here](https://medium.com/@marek.michalik/c-vs-rust-vs-go-performance-analysis-945ab749056c). As you can see, in Go, it is easy to make mistakes that heavily affects performance. In other words, if you don’t pay close attention and understand how Go works, your code will not perform great and may have runtime defects, whereas in Rust, the compiler guides you and force you to write high performant and safe code.

In terms of **concurrency**, both languages are equally as good. Rust is still more performant but it does not have concurrency built in the languages and you need to use libraries such as [Tokio](https://tokio.rs/) whereas Go has the amazing Go Routines and channels that work very well. In my opinion, if your bottleneck is caused by blocking operations and you need concurrency and parallelism but not CPU intensive tasks, then there will be not much difference in terms of performance but Go will be much easier to use.

## Recommendations

## If you are a developer…

- Learn GO if you are a junior developer and/or you don’t have Java experience but have Python or C++ experience.
- Learn GO if you can’t afford spending years to master a new language.
- Learn GO if you embrace the DevOps culture.
- Learn GO if you are using Google Cloud.
- Learn GO if you are looking to get many job offers across many verticals.
- Use GO to write scripts and command line tools, POCs or fast APIs.
- Learn Rust if you want to get into Cryptocurrencies.
- Learn Rust if you are a senior developer and/or C developer.
- Learn Rust if you are looking after high paid jobs but not many of them.
- Learn Rust if you want to work on embedded systems or **WebAssembly** and other modern tools.
- Learn Rust if you want to impress your boss with ultra fast code that just works.
- Learn Rust if you want to build complex applications using [ADTs](http://blog.madhukaraphatak.com/rust-scala-part-4/) and advance types.
- Learn Rust or GO if you want to work in the cloud, in start-ups and cool projects.

In short, **GO** is fun and cool, **easy to learn** and simple. In 3 months you can be writing production ready applications for real world usages. **Rust** is **complex** and challenging but rewarding, it pays quite well and it has more prestige. Both languages are trending and if you learn them you will work on interesting projects in the cloud or Kubernetes. But Go is still much more popular.

## If you are a tech lead…

- Use GO to have access to many libraries and APIs or to run your programs as Serverless functions. Rust is still a bit immature.
- Use GO for custom scripts, small jobs and CLIs.
- Use GO for simple concurrency and event processing.
- Use GO if you run in the cloud, specially Google Cloud.
- Use GO for small size projects.
- Use Rust if your team already knows C and you want to write safer code.
- Use Rust for high concurrent complex distributed systems that take advantage of every bit of hardware resources and provide predictable performance.
- Use Rust to rewrite parts of your application that require high performance, you can leave the rest in another language.
- Use Rust to move away from C, they are compatible.
- Use Rust if you work in a company where bugs in production are very expensive such as healthcare, aviation, etc.
- Use Rust if your problem can be solved with the existing mature libraries such as [Tokio](https://tokio.rs/), [Rocket](https://rocket.rs/), [Actix](https://actix.rs/), etc. You will get very good performance without much effort.
- Use Rust to generate minimal binary to deploy on edge or embedded systems.
- Use Rust for big or monorepo projects
- User Rust for big codebases where modularization is key

In summary, both languages compile to a binary that consume very little resources, Rust is faster and has lower footprint but harder to learn unless your team already knows C.

## If you are a manager…

- Use GO for **Serverless** computing and FaaS.
- Use GO if you are running in Google Cloud since most of the GCP services are based on GO APIs.
- Use Rust for critical concurrent applications, monoliths or real time systems.
- Use Rust to attract highly skilled developers.
- Use Rust for large code bases and complex projects.
- Use Rust to build [**greener**](https://thenewstack.io/which-programming-languages-use-the-least-electricity/) projects.
- If you are looking to add a new language and you cannot spend much time learning it, GO is easier to adopt than Rust.
- Use any for microservices or Kubernetes.

In short, **Rust** is cheaper to run and performs better, also Rust programmers are extremely good, if you use Rust you will attract talent. The problem is that there are not many Rust developers and it could be very difficult to find them. GO in the other hand, is more popular and it is not difficult to find developers. Both languages are trending and perform very well using very little resources. C or even Python teams will find easier the migration to Rust than teams that know other languages.

## Conclusion

**Rust** is my favourite new language, **it is new, refreshing, high performant, rich and extensible**. It takes some time to get used to it, you may get frustrated with the compiler due to the ownership model but once you get used to it and understand the rules, it becomes easier.

GO in the other hand, is much **easier to use and more popular**. Many SDKs have GO clients but there are less Rust clients, so check this before embarking in a new project. For example, there are **Rust** clients for [Redis](https://redis.io/), [ElasticSearch](https://www.elastic.co/elasticsearch/), [S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html), etc but many others are missing or are too immature.

I would recommend anyone to learn both languages since their popularity is growing. Probably **GO has better return on investment**; it is easier to learn and it has more job openings. **Rust is still quite new** and it will take time before we see Rust as a requirement in most job offers. However, I would encourage everyone to learn Rust, it will make you a **better programmer**. Once you are comfortable with Rust, try to identify components of your application that will benefit from it and re implement them in Rust to improve the performance.

In general, as of 2022, **GO** is the top language and **safer option** to start a new project, specially when developing cloud native applications. However, you should consider **Rust** if you work in tech companies were **scaling and performance** are very important. Other use cases for **Rust** include embedded systems, high performant applications, WebAssembly, Cryptocurrency, concurrent applications and any complex application that require **control over the underlying hardware**.

But for me, personally, **the best thing** about **Rust** is its [**low energy consumption**](https://thenewstack.io/which-programming-languages-use-the-least-electricity/), Java almost doubles the consumption and **Go uses almost 3x more energy!**. As the population grows in our planet and **climate change** becomes an issue, we should aim to be **energy efficient and reduce our carbon footprint**. Software is literally everywhere and the amount of energy required to run it has devastating effects on the planet; reducing the energy consumption will have a huge impact on our planet (and also in your cloud bill!), and this is very important. As developers, we should be aware of this, and try to learn more **energy efficient languages** in order to contribute to create a more **sustainable** planet.

![](https://miro.medium.com/v2/resize:fit:700/0*DSsGLLU4HQPfrNUw.png)

Alongside C, Rust is the most efficient language

**UPDATE**: I’m currently in Tanzania helping a local school, I’ve created a [**GoFundMe Campaign**](https://www.gofundme.com/f/help-the-mango-school-children-in-tanzania) to help the children, to donate follow this [link](https://www.gofundme.com/f/help-the-mango-school-children-in-tanzania), every little helps!

*Remember to* ***clap*** *if you enjoyed this article and* [***follow*** ***me***](https://javier-ramos.medium.com/subscribe) *or* [***subscribe***](https://javier-ramos.medium.com/membership) *for more updates!*

[**Subscribe**](https://javier-ramos.medium.com/subscribe) to get **notified** when I publish an article and [**Join Medium.com**](https://javier-ramos.medium.com/membership) to access millions or articles!