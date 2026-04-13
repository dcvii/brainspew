---
title: "Why Distributed Systems Fail and How to Limit the Damage"
source: "https://newsletter.francofernando.com/p/why-distributed-systems-fail-and?publication_id=1172544&post_id=191037904&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Franco Fernando]]"
published: 2026-04-03
created: 2026-04-07
description: "A look at the most common failure modes and the techniques to reduce their impact."
tags:
  - "brain_spew"
---
### A look at the most common failure modes and the techniques to reduce their impact.

Hi Friends,

Welcome to the 167th issue of the Polymathic Engineer.

A rule of thumb when working on a distributed system is to assume that anything can go wrong. The way engineers usually deal with this is by using scalability patterns like data partitioning, functional decomposition, and replication.

The problem with these patterns is that they all add more moving parts and make our systems more complicated. Since each part has a chance of failing, the more there are, the higher the chance that at least one of them will fail at any given moment. Software crashes, power outages, hardware faults, and memory leaks can happen all the time.

This isn't only a worry in theory. As we discussed in [another article](https://francofernando.substack.com/p/availability), a system can only be down for approximately 15 minutes a day to guarantee it is available 99.99% of the time. For three nines, that drops to 43 minutes per month. In general, the more nines you want, the faster your system needs to detect failures and recover from them when they occur. There is no time for a person to notice anything went wrong and fix it.

In this article, we will discuss the most common root causes of failures in distributed systems and see how to address them. The outline is as follows:

- Common root causes of failures
- Managing risk
- Redundancy
- Correlation
- Fault isolation
- Shuffle Sharding and Cellular Architecture

---

Project-based learning is the best way to develop technical skills. [CodeCrafters](https://app.codecrafters.io/join?via=FrancoFernando) is an excellent platform for tackling exciting projects, such as building your own Redis, Kafka, a [DNS server](https://app.codecrafters.io/join/dns-server?via=francofernando), SQLite, or Git from scratch. [Sign up, and become a better software engineer](https://app.codecrafters.io/join?via=FrancoFernando).

---

## Common root causes of failures

To build fault-tolerant distributed systems, you first need to fully understand what can go wrong. Let's start looking at the most common failure modes you can encounter.

#### Infrastructure Faults

Hardware doesn’t last forever. Hard drives fail, memory modules go bad, and network cards stop working. Power outages happen, and fiber cuts or electrical storms can take down whole data centers. The good news is that redundancy makes it straightforward to remedy these infrastructural problems. The underlying idea is simple: if one of your servers goes down, the others may take over.

#### Incorrect Error Handling

A [study of user-reported failures](https://scispace.com/pdf/an-analysis-of-production-failures-in-distributed-data-igrujmovmy.pdf) from well-known distributed data storage showed an unexpected result. Most major failures were not caused by infrastructure issues. They were caused by mistakes made when dealing with non-fatal faults. The bugs were very easy to fix. In some cases, error handlers didn’t even look at errors; in others, handlers were only partially set up, or caught too generic exceptions. The main point was that most bugs could have been found with simple unit tests.

#### Configuration Changes

Changes to configurations cause failures more often than most engineers think, and it is not always a simple mistake like a typo in a database connection string that makes them risky. One example is a valid configuration change turning on a feature flag that hasn’t been used in years. Even if there is a code path, and the value looks correct, the behavior is no longer what was meant.

Configuration changes are challenging because they may not take effect right away. A change that is not valid might not be seen for hours or days if an application only gets a configuration value when a certain code path runs. This is why configuration should be managed like code: version-controlled, reviewed, and released incrementally.

#### Single points of failure

A single point of failure is any component that, brings the entire system down when it fails. The tricky part is that they are not always obvious.

People are a surprisingly common one. If someone has to manually execute a sequence of operational steps in the right order without making a mistake, it is only a matter of time before something goes wrong. Computers, on the other hand, are much better at executing instructions. This is why you should automate whenever possible.

But systems have non-human SPOFs as well. DNS is a good example: if clients can’t resolve your domain, it doesn’t matter how healthy your servers are. TLS certificates are another one: if yours expires, every client connection will be refused.

When designing a system, a useful exercise is to go through each component and ask what happens if it disappears. Some SPOFs can be removed with redundancy. Others can’t, but you can at least work to reduce how much damage they cause when they do fail.

#### Network faults

When two processes talk to each other over the network, a lot can go wrong. Messages might get lost, arrive late, or be sent more than once. The sender rarely knows which of these things happened because they only see a timeout.

But timeouts are the easy case. A more difficult situation is when the network doesn’t completely fail; it just gets slow. A process sends a request and gets a response, but it takes 10 times longer than usual. There is no error to catch and no timeout to trigger. The caller just waits, hanging on to resources while they do. These partial failures are sometimes called *gray failures* and are considerably harder to find than a clean crash. A slow dependency can silently bring the entire system to a halt before anybody knows something is wrong.

#### Resource leaks

Every process has a limited number of resources it can use, such as memory, threads, file handles, and database connections. When a bug causes one of these resources not to be released properly, you get a leak. The hard part is that leaks don’t show up right away. A slow memory leak might take days to fill up the heap. A connection pool that loses one connection per hour won’t cause problems until there are none left.

This is what makes resource leaks so dangerous: they pass all the tests in staging but don't show up in production until the app has been running long enough. And when they do ultimately fix the problem, it often doesn't seem like the original defect at all. A leaky connection doesn't make a sound, but it just shows up as a strange timeout in another part of the system.

#### Load pressure

A system can perform perfectly fine under normal conditions, but it can break down when the load gets too high. The hard aspect is that the extra load doesn't necessarily come from the users. Sometimes the spike comes from places you don’t expect: a web scraper hitting your API thousands of times per second, or a denial-of-service attack flooding your servers with traffic.

What makes load-related failures difficult is that they can turn a healthy system into an unhealthy one very quickly. When the thread pool is full, a service that responds in 50 milliseconds under normal load can take 5 seconds. And that slowdown does not stay in one place, but extends to all the other services that are waiting for a response.

#### Cascading failures

Cascading failures happen when a fault in a component causes faults in some others, which then trigger more faults, and so on. A common example is when a server gets too many requests, starts to answer slowly, and callers start to time out. Those callers retry, adding even more load to the already struggling server. The situation gets worse and worse until the whole system grinds to a halt.

*Metastable failures* are the most dangerous kind of cascade failures. This happens when the system gets stuck in a bad state that doesn't go away even after the original cause has gone away. For example, a short spike in traffic creates a lot of retries. The retries themselves create enough load to produce more retries, and the system persists in this self-sustaining failure mode long after the original spike is over. When this happens, it is not possible to just wait for the problem to pass. The system needs an intervention to break the cycle.

## Managing Risk

By now, the list of things that can go wrong may seem a bit too long. But just because a mistake could happen doesn't imply we have to fix it immediately.

Hi **mbowen@mdcbowen.org**

## This post is for paid subscribers

[Already a paid subscriber? **Switch accounts**](https://substack.com/sign-in?redirect=%2Fp%2Fwhy-distributed-systems-fail-and%3Fpublication_id%3D1172544%26post_id%3D191037904%26isFreemail%3Dtrue%26r%3D7br8e%26triedRedirect%3Dtrue&for_pub=francofernando&change_user=true)