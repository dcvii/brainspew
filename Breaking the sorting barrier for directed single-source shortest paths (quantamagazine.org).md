---
title: "Breaking the sorting barrier for directed single-source shortest paths (quantamagazine.org)"
source: "https://news.ycombinator.com/item?id=44812695"
author:
  - "[[baruchel]]"
published: 2025-08-06
created: 2025-08-11
description:
tags:
  - "clippings"
---
[https://www.quantamagazine.org/new-method-is-the-fastest-way-to-find-the-best-routes-20250806/](https://www.quantamagazine.org/new-method-is-the-fastest-way-to-find-the-best-routes-20250806/)

[https://arxiv.org/abs/2504.17033](https://arxiv.org/abs/2504.17033)

---

## Comments

> **o11c** • [2025-08-06](https://news.ycombinator.com/item?id=44815509)
> 
> First, note that this complexity is actually *worse* for highly dense graphs, where \`m\` (number of edges) dominates rather than \`n\` (number of nodes) \[note that a useful graph always has \`m > n\`, and often \`m <= 2*d* n\`, where \`d\` is the number of dimensions and the 2 is because we're using directed edges. Ugh, how do we compare log powers?\].
> 
> Additionally, the \`n\` in the complexity only matters if for the Dijkstra approach you *actually* need a frontier of size proportional to \`n\` \[remember that for open-grid-like graphs, the frontier is limited is limited to \`sqrt(n)\` for a plane, and for linear-ish graphs, the frontier is even more limited\].
> 
> Also note that the "sorting barrier" only applies to comparison-based sorts, not e.g. various kinds of bucket sorts (which are easy to use when your weights are small integers). Which seems to be part of what this algorithm does, though I haven't understood it fully.
> 
> > **lqet** • [2025-08-06](https://news.ycombinator.com/item?id=44816176)
> > 
> > Very good points. I wonder what this means for real-world street network graphs. In my experience, *m* can be considered proportional to *n* in road network graphs (I would estimate *m ≈ 2C n*, with *C* being between 2 and 3). This would mean that the asymptotic running time of this new algorithm on a classic road transportation network would be more like *O(Cn log^2/3 n) = O(n log^2/3 n)*, so definitely better than classic Dijkstra (*O(n log n)* in this scenario). On the other hand, the frontier in road network graphs is usually not very big, and (as you also said for grid graphs) you normally *never* "max out" the priority queue with *n* nodes, not even close. I would be surprised if the *^2/3* beats the additional constant overhead of the new approach in this case.
> > 
> > > **valenterry** • [2025-08-07](https://news.ycombinator.com/item?id=44819839)
> > > 
> > > In real world you are not using either, you have way more way to optimize for a specific problem. For street networks you'd probably start with "A\*" or something like that.
> > > 
> > > > **clausecker** • [2025-08-07](https://news.ycombinator.com/item?id=44822431)
> > > > 
> > > > The current meta game is the use of contraction hierarchies. Basically, you sinplify the network into hubs connected by trunk lines and then refine the routing close to start and destination.
> > 
> > **adgjlsfhk1** • [2025-08-06](https://news.ycombinator.com/item?id=44817642)
> > 
> > in the real world djikstra will definitely be faster.
> > 
> > > **mananaysiempre** • [2025-08-06](https://news.ycombinator.com/item?id=44818772)
> > > 
> > > It’s not often that you see O(E + V log V) Dijkstra with Fibonacci heaps, either, the O((E + V) log V) version with plain binary heaps is much more popular. I don’t know if that’s because the constants for a Fibonacci heap are worse or just because the data structure is so specialized.
> > > 
> > > > **lqet** • [2025-08-07](https://news.ycombinator.com/item?id=44821499)
> > > > 
> > > > Yes, a standard binary heap is *very* fast and incredibly simple to implement, mostly because you can store the entire heap in a single continuous array, and because you can access individual elements by simple pointer arithmetic. It's quite hard to beat this in practice.
> 
> **hinkley** • [2025-08-07](https://news.ycombinator.com/item?id=44819440)
> 
> So that means it doesn’t work for Traveling Salesman, where the edges are nearly n^2? That might explain why it’s not been found before.

> **karussell** • [2025-08-06](https://news.ycombinator.com/item?id=44818667)
> 
> It is somewhat funny that it took 12 submissions here on hackernews to bring it to a wider audience :) [https://hn.algolia.com/?query="2504.17033"](https://hn.algolia.com/?query=%222504.17033%22)

> **polytely** • [2025-08-06](https://news.ycombinator.com/item?id=44813223)
> 
> \> But curiously, none of the pieces use fancy mathematics.
> 
> \> “This thing might as well have been discovered 50 years ago, but it wasn’t,” Thorup said. “That makes it that much more impressive.”
> 
> this is so cool to me, it feel like a solution you could\* have stumbled upon while doing game development or something
> 
> \*probably wouldn't but still
> 
> > **RobRivera** • [2025-08-06](https://news.ycombinator.com/item?id=44815568)
> > 
> > Gamedevs -I find at least- are so obsessively deep at SOLVING their problem at hand that their headspace is indexed on shipping the game, the project, deadlines, and what to eat for the next meal (probably pizza).
> > 
> > Rather than the academia.
> > 
> > Just a hunch tho
> > 
> > > **8n4vidtmkvmk** • [2025-08-06](https://news.ycombinator.com/item?id=44815971)
> > > 
> > > Isn't that just it though? The problem very well could be that some part of the game is running too slow so they just start solving it. No time to read and write academic papers.
> > > 
> > > > **colonCapitalDee** • [2025-08-06](https://news.ycombinator.com/item?id=44817702)
> > > > 
> > > > This algorithm is asymptotically faster than the state of the art, but it isn't faster in practice. At least not yet!
> > > > 
> > > > **thfuran** • [2025-08-07](https://news.ycombinator.com/item?id=44819808)
> > > > 
> > > > Somebody somewhere might be Ramanujan, but the average person is going to be a whole lot better served by reading literature than trying to reinvent the field.
> > > > 
> > > > > **8n4vidtmkvmk** • [2025-08-08](https://news.ycombinator.com/item?id=44832230)
> > > > > 
> > > > > I'd certainly Google for some algos before writing one myself.
> > > > > 
> > > > > Years ago, however, I came across a paper for optimal convex polygon decomposition that had zero implementations and the paper was so complicated.. couldn't figure out how to implement it myself. I came up with something new and published it which was apparently enticing enough to be picked up by at least one game library. So that was neat.
> > > 
> > > **RobRivera** • [2025-08-06](https://news.ycombinator.com/item?id=44817385)
> > > 
> > > That's what I have found to be the case: time is in short supply
> 
> **hinkley** • [2025-08-06](https://news.ycombinator.com/item?id=44815506)
> 
> Maybe someone did and just didn’t see it as novel?
> 
> > **kevingadd** • [2025-08-06](https://news.ycombinator.com/item?id=44818981)
> > 
> > Depending on where you work they might not let you publish a paper about it. Certainly was the case at one game studio I worked for, very secretive.

> **ljlolel** • [2025-08-06](https://news.ycombinator.com/item?id=44813038)
> 
> Tarjan was my algorithms professor. He invented many of them
> 
> > **larodi** • [2025-08-06](https://news.ycombinator.com/item?id=44814304)
> > 
> > …invented many of them algorithms? like which?
> > 
> > > **teraflop** • [2025-08-06](https://news.ycombinator.com/item?id=44815811)
> > > 
> > > Aside from inventing a bunch of individual algorithms, Tarjan is also known for introducing various theoretical *techniques* that are now considered fundamental. Most notably, amortized analysis.
> > > 
> > > His Turing award writeup gives a pretty broad overview of his research contributions: [https://amturing.acm.org/award\_winners/tarjan\_1092048.cfm](https://amturing.acm.org/award_winners/tarjan_1092048.cfm)
> > > 
> > > **kzrdude** • [2025-08-06](https://news.ycombinator.com/item?id=44814324)
> > > 
> > > Maybe Tarjan's strongly connected components. That's one I've implemented at some point at least.
> > > 
> > > > **larodi** • [2025-08-09](https://news.ycombinator.com/item?id=44848331)
> > > > 
> > > > Thanks, this is interesting, how could I miss an important algorithm related to graphs, incredible.
> > 
> > **bob1029** • [2025-08-06](https://news.ycombinator.com/item?id=44814387)
> > 
> > This is one of my favorites:
> > 
> > [https://en.wikipedia.org/wiki/Splay\_tree](https://en.wikipedia.org/wiki/Splay_tree)

> **aDyslecticCrow** • [2025-08-06](https://news.ycombinator.com/item?id=44814703)
> 
> I'm intrigued but the article is very verbose with little detail. Mabie the paper will give a more satisfying description.
> 
> Im most curiosity how the algorithm fulfil the "global minima" that djixtra guarantees. The clumping of front-tier nodes seem prone to missing some solutions if unlucky.

> **ape4** • [2025-08-06](https://news.ycombinator.com/item?id=44813454)
> 
> Sounds a lot more complicated that Dijkstra. But I guess that's the way it goes.
> 
> > **larodi** • [2025-08-06](https://news.ycombinator.com/item?id=44814318)
> > 
> > Dijkstra is still very difficult for many and not universally taught in 7th grade even though you can arguably explain what a shortest path in a graph is to 14 y.o.
> > 
> > > **chowells** • [2025-08-07](https://news.ycombinator.com/item?id=44821304)
> > > 
> > > Dijkstra's algorithm is completely trivial. It's a greedy algorithm; there's nothing more complex involved than repeating the same simple step over and over. You pick a starting node then repeatedly add the lowest-cost edge to a node you haven't already reached. It's harder to explain what a "node" and "edge" are than to explain how Dijkstra's algorithm works.
> > > 
> > > Many textbooks make it sound harder than that because they want to examine complex data structures that make various parts of that as fast as possible. But the complexity is the implementation of the data structures, not Dijkstra's algorithm.
> > > 
> > > > **larodi** • [2025-08-08](https://news.ycombinator.com/item?id=44833911)
> > > > 
> > > > indeed. and I can confirm I learned this algorithm back in the day in 8th grade, as we were given home assignments and myself had to read through a book 'introduction to Graphs' which was designated for 2nd university year students.
> > > > 
> > > > I was able to read halfway through the book before it started getting too complex for my teen mind.
> > > > 
> > > > so, can it be taught? - yes is it trivial - I would not dare say, but is elegant in simplicity do people understand and remember it easily - no, they don't
> > > > 
> > > > should you decide to prove me right, well - try to teach it to someone, but also require that he not only understands but implements it. well those who could do this in 8th grade were those going to Olympiads in Informatics.
> > > > 
> > > > perhaps things have changed since the 90s and children are smarter today. so my bet is you can teach it to 5th graders, not sure to what effect though.
> > 
> > **GolDDranks** • [2025-08-06](https://news.ycombinator.com/item?id=44814390)
> > 
> > Dijkstra \_could\_ be universally taught in 7th grade if we had the curriculum for that. Maybe I'm biased, but it doesn't seem conceptually significantly more difficult than solving first degree equations, and we teach those in 7th grade, at least in Finland where I'm from.
> > 
> > > **larodi** • [2025-08-08](https://news.ycombinator.com/item?id=44833959)
> > > 
> > > Depends on which school, as this is not taught at all outside mathematics school. My claim is you can teach it to 5th graders, this is what I tell my university students and I mean it.
> > > 
> > > Myself and others from the math schools knew this algorithm in 8th grade for sure, as we been already using it in 9th grade for competitions. This does not mean all my classmates knew it, of course not.
> > > 
> > > So it depends who you teach this to. Theoretically - you should be able to, practically - well, perhaps not so much, as math is not the only thing 8th grader learns, in fact his head is bombarded with ... dozen disciplines at a time.
> > > 
> > > Besides, I recently met a classmate, previous IoI medalist, who works quant-something somewhere for 15th + years, and is a PHD and everything. We start talking about mathematics and I find to my total surprise he knows very little about grammars, never used them. He remembers Dijkstra or Ford-Fulkerson, but only as a title, while I'm sure he learned these at some point in Stanford, as the shortest-path and A\* was not something we had in textbooks back in the 90s for sure.
> > > 
> > > **crawfordcomeaux** • [2025-08-06](https://news.ycombinator.com/item?id=44816198)
> > > 
> > > For sure! The main thing keeping us from teaching advanced things to younger folks is the seeming addiction to teaching poorly/ineffectively. I'm here to find the physical play-with-your-hands demonstrations needed for teaching kids as young as 5 the intuitions/concepts behind higher-order category theory without all the jargon.
> > > 
> > > > **kevindamm** • [2025-08-06](https://news.ycombinator.com/item?id=44816446)
> > > > 
> > > > I think you could do it with many board games. Mouse Trap for monads? Poker for permutations? Dice for decision theory?
> > 
> > **hinkley** • [2025-08-06](https://news.ycombinator.com/item?id=44818673)
> > 
> > I think we forget how old the term algorithm is. We started this journey trying to automate human tasks by divide and conquer, not computers.
> > 
> > Merge sort is supposedly invented in 1950, it’s more likely it was invented in 1050 than 1950. Sort a room full of documents for me. You have three minions, go.
> > 
> > > **larodi** • [2025-08-08](https://news.ycombinator.com/item?id=44833884)
> > > 
> > > \> I think we forget how old the term algorithm is.
> > > 
> > > given Al Kwarizimi lived ~12 century (if memory serves right) it is a fairly old term in this regard.
> > > 
> > > when was it that modern people started using the word, I'd bet beginning of 20th century, but this is a wild guess.
> > > 
> > > when did everyone started calling algorithms "ai", well perhaps ~1960 ?
> > > 
> > > **adgjlsfhk1** • [2025-08-06](https://news.ycombinator.com/item?id=44818701)
> > > 
> > > I think humans generally use some form of bucket/radix sorting (or selection sort for small collections)
> > > 
> > > > **hinkley** • [2025-08-07](https://news.ycombinator.com/item?id=44819360)
> > > > 
> > > > A human is different than “humans” a human with a stack may sort it into four stacks and then sort amongst them, yes.
> > > > 
> > > > But a room of five clerks all taking tasks off a pile and then sorting their own piles is merge sort at the end of the day. Literally, and figuratively.
> 
> **cantor\_S\_drug** • [2025-08-06](https://news.ycombinator.com/item?id=44813584)
> 
> reminds me of TimSort.

> **flafla2** • [2025-08-06](https://news.ycombinator.com/item?id=44814193)
> 
> O(m log^2/3 n) !!! What a triumph.
> 
> > **supernetworks\_** • [2025-08-06](https://news.ycombinator.com/item?id=44814242)
> > 
> > [https://arxiv.org/abs/2504.17033](https://arxiv.org/abs/2504.17033)
> > 
> > We give a deterministic O(mlog2/3n)-time algorithm for single-source shortest paths (SSSP) on directed graphs with real non-negative edge weights in the comparison-addition model. This is the first result to break the O(m+nlogn) time bound of Dijkstra's algorithm on sparse graphs, showing that Dijkstra's algorithm is not optimal for SSSP.
> > 
> > > **hinkley** • [2025-08-06](https://news.ycombinator.com/item?id=44815549)
> > > 
> > > log^2/3 might be the weirdest component I’ve ever seen in a complexity formula.
> > > 
> > > > **jojomodding** • [2025-08-06](https://news.ycombinator.com/item?id=44816459)
> > > > 
> > > > I'm continually amazed by the asymptotic complexity of union-find, which is O(alpha(n)), where alpha(x) is the inverse of the Ackermann function (and n the number of sets you union). In other words, O(6) or so as long as your inputs fit into the observable universe.
> > > > 
> > > > > **hinkley** • [2025-08-06](https://news.ycombinator.com/item?id=44816673)
> > > > > 
> > > > > There's definitely a divide on who sees what sort of algorithms. The subject of this article is in Graph Theory space, which a lot of us get even without trying (I dabbled in TSP for a while because it's a difficult distributed programming problem and I wanted to explore the space for that reason).
> > > > > 
> > > > > But if you're not implementing AI or game engines, some of the linear algebra space may be a road less traveled.
> > > 
> > > **bawolff** • [2025-08-06](https://news.ycombinator.com/item?id=44815985)
> > > 
> > > I still think matrix multiplication's O(n^2.371339) is super weird.
> > > 
> > > > **adgjlsfhk1** • [2025-08-06](https://news.ycombinator.com/item?id=44816050)
> > > > 
> > > > Matrix multiplication definitely should be O(n^(2+o(1))).
> > > 
> > > **adgjlsfhk1** • [2025-08-06](https://news.ycombinator.com/item?id=44816036)
> > > 
> > > for about a decade, integer multiplication was at n*4^log\*(n) where log\* is the iterated logarithm.
> > > 
> > > Also the curently best factorization algorithm (GNFS) is at exp(k\*log(n)^1/3log(log(n))^2/3).
> > > 
> > > *
> > > 
> > > *Intro algorithms classes just tend to stay away from the really cursed runtimes since the normal ones are enough to traumatize the undergrads.*
> > > 
> > > > **hinkley** • [2025-08-06](https://news.ycombinator.com/item?id=44816694)
> > > > 
> > > > Are BigInteger multiplications in logn² now or do they still have weird terms in them?
> > > > 
> > > > > **adgjlsfhk1** • [2025-08-06](https://news.ycombinator.com/item?id=44817121)
> > > > > 
> > > > > down to nlogn
> > > 
> > > **Sniffnoy** • [2025-08-06](https://news.ycombinator.com/item?id=44816690)
> > > 
> > > Hey the asterisks in your reply got read as formatting so it's ended up messed-up.
> > > 
> > > > **adgjlsfhk1** • [2025-08-06](https://news.ycombinator.com/item?id=44817131)
> > > > 
> > > > oops. fixed.

> **crawfordcomeaux** • [2025-08-06](https://news.ycombinator.com/item?id=44816228)
> 
> I wonder if hybridizing this with selective use of randomness to probe beyond frontiers leads to another speedup.