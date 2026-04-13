---
title: "In Math, Rigor Is Vital. But Are Digitized Proofs Taking It Too Far?"
source: "https://www.quantamagazine.org/in-math-rigor-is-vital-but-are-digitized-proofs-taking-it-too-far-20260325/"
author:
  - "[[Leila Sloman]]"
published: 2026-03-25
created: 2026-03-30
description: "The quest to make mathematics rigorous has a long and spotty history — one mathematicians can learn from as they push to formalize everything in the computer program Lean."
tags:
  - "brain_spew"
---
![](https://www.quantamagazine.org/wp-content/uploads/2026/03/FormalMess-crKristinaArmitage-Lede-scaled.webp)

In ancient Greece, Euclid showed that if you agree on a small list of preliminary principles, or axioms, you can use deductive reasoning to reveal all sorts of new mathematical truths. But although these early proofs, as mathematicians call them, were derived using the laws of logic, they sometimes also contained hidden, unstated assumptions or relied on misleading intuitions. In these cases, small gaps in a proof might go unnoticed; one couldn’t say with absolute confidence that it was correct.

Over the past few centuries, mathematicians have sought to close those gaps. By the early 1900s, they settled on the axioms they wanted to use. They also introduced different logical systems and standards in an effort to further “formalize” their arguments — to guarantee that, if you made every deduction in a proof explicit, its conclusion would have to be true no matter how long and convoluted it got.

This formalization effort engendered trust. But it did far more than that. The push to formalize has helped mathematicians uncover novel connections between different areas of math. It has taken the field in unexpected new directions. It has taught us, said [David Bressoud](https://www.davidbressoud.org/) of Macalester College in Minnesota, that “you often don’t know what you don’t know. And to be humble about that.”

But big advances in mathematics inevitably require bold ideas. These often come from experimentation and intuition — from exploring novel mathematical worlds and testing out novel theories, even if you can’t prove that every step in the journey logically follows from the last. It’s a less formal way of doing math that at first tends to contain mistakes.

It’s not easy to strike a fruitful balance between the creativity needed to paint new mathematical landscapes and the rigor necessary to ensure that the resulting pictures are true. Sometimes, formalization can upset that balance. What some mathematicians see as a move toward greater certainty, others might see as pedantry or a barrier to progress.

![Two pages of Euclid’s Elements.](https://www.quantamagazine.org/wp-content/uploads/2026/03/Euclids-Elements.webp)

Euclid’s Elements marked the first major effort to formalize mathematics in the West. It established a deductive method for proving statements that’s still used today. Above, pages from the first printed edition of the work, made in 1482. Folger Shakespeare Library/Creative Commons CC BY-SA 4.0

Today, mathematicians are attempting their most ambitious formalization project yet. They’re aiming to rewrite all of mathematics in a computer language known as Lean, which can then automatically verify their proofs. Writing a proof in Lean requires an enormous amount of time and effort, but so far, the program has been used to verify more than 260,000 theorems. It has the potential to put mathematics on the most solid foundation one can imagine.

As with past attempts to formalize math, Lean has generated mixed feelings. Some mathematicians look forward to offloading tedious verification work onto computers and see Lean as a potentially transformative new way of doing mathematics. Others think that their time and resources are better spent elsewhere — or, worse, that a Lean-centric approach will distort the true value of mathematics. It’s a discussion that’s starting to play out in the hallways of math departments around the world: How do we balance the creativity needed to discover new mathematical connections with the rigor needed to ensure that every logical step is undeniable?

## Setting Limits

A major milestone in the quest for rigor came about because of hidden problems with one of the most important mathematical achievements of all time.

In the late 17th century, Isaac Newton and Gottfried Leibniz independently developed calculus, a technique for understanding how quickly a function changes at a given point. But in an informal sense, calculus had already been around for centuries. In fact, Archimedes was doing something like calculus in the third century BCE. To calculate the area of a circle, he first studied the areas of shapes with straight sides called polygons. By using polygons with more and more sides, he was estimating a limit: the area of the circle. Newton and Leibniz took a similar approach, using limits to understand change.

![Page of a textbook written by Archimedes.](https://www.quantamagazine.org/wp-content/uploads/2026/03/Archimedes-page.webp)

In his treatise On Conoids and Spheroids, seen here in an 1897 translation, Archimedes introduced ideas that would play a key role in the development of calculus millennia later. From T.L. Heath’s edition of The Woks of Archimedes. Cambridge University Press, 1897/Public Domain

Calculus immediately became useful throughout math and physics. But it was not formal by modern standards: Leibniz’s and Newton’s papers glossed over some ambiguities. Calculus relies on the notions of infinity and infinitely small quantities (called infinitesimals), but Newton and Leibniz defined these concepts in vague geometric terms; used incorrectly, their formulas could lead to nonsensical calculations, like division by zero.

For 150 years, that didn’t cause any problems. Scientists simply learned to tell when calculus could be used effectively and when it couldn’t. But in the early 19th century, mathematicians started to encounter phenomena — infinite sums and [strange, jagged curves](https://www.quantamagazine.org/the-jagged-monstrous-function-that-broke-calculus-20250123/), for instance — that defied their intuition for what was possible.

These encounters came at a time of broader questioning across the arts and sciences. Philosophers, painters, writers, and researchers were beginning to probe the limits of what they thought they knew. “Intuition is suspect,” said [Alma Steingart](https://scienceandsociety.columbia.edu/directory/alma-steingart), a historian at Columbia University. “There is this feeling that intuition can lead you the wrong way.”

![Portrait of Gottfried Leibniz](https://www.quantamagazine.org/wp-content/uploads/2026/03/Gottfried-Leibniz-cr-Christoph-Bernhard-Francke.webp)

Gottfried Leibniz (left) and Isaac Newton independently invented calculus in the 17th century. For years, they feuded over who came up with its central ideas first. Christoph Bernhard Francke (left); Godfrey Kneller

Renowned mathematicians such as Niels Abel, Augustin-Louis Cauchy, and Karl Weierstrass realized that to make sense of the bizarre sums and curves that were cropping up in their work, they needed to return to their most fundamental definitions. What is a function? What does it mean for a function to be continuous? What really happens when you add up infinitely many objects?

They came up with formal definitions that answered these questions. (Weierstrass, for instance, introduced the precise definition of a limit that students still use today.) Their new definitions enabled mathematicians to study functions in a much deeper and more rigorous way than they ever had before — ultimately spawning the field of analysis.

Today, analysis is one of the most important areas in math. It allows mathematicians to understand everything from fluid flow and electrical currents to the chemical makeup of far-off stars. And it is deeply connected to almost every other type of math, including the far older fields of number theory and geometry.

The formalization of calculus also led to the birth of set theory, which established the rules that underlie modern mathematics. Set theory is now an active area of study in its own right.

![Portrait of Augustin Louis Cachy Charles Reutlinger](https://www.quantamagazine.org/wp-content/uploads/2026/03/Augustin_Louis_Cauchy-Charles-Reutlinger-via-The-Smithsonian-Libraries-Large.webp)

In the 19th century, Augustin-Louis Cauchy (left) and Karl Weierstrass redefined key concepts in calculus, giving rise to the modern field of analysis. The Smithsonian Libraries (left); Public Domain

Still, some researchers also faced this new wave of formalization with trepidation. “It is not easy to get up any enthusiasm after it has been artificially cooled by the wet blankets of the rigorists,” the physicist Oliver Heaviside wrote in 1899.

As the historian Jesper Lützen [has observed](https://www.ams.org/publications/authors/books/postpub/hmath-24), looking back at this time period: “Analysis gained both rigor and generality, but it lost in elegance and simplicity and was estranged from intuition. Many mathematicians regretted this tendency, but it was hard to escape.”

Crucially, rigorists and their detractors found a compromise: Mathematicians continued to use the careful definitions of Cauchy and Weierstrass, but they also developed frameworks that allowed scientists like Heaviside to compute with infinity and infinitesimals more freely.

In other words, formalization wasn’t their only aim. In fact, an important part of this story is the intent behind the formalization. Its focus was relatively narrow: Weierstrass and his colleagues had been dealing with very particular questions about the behavior of functions, and they turned to formalization in order to deal with those problems. From there, the development of analysis, set theory, and other formal systems happened organically.

“The edifice of science is not raised like a dwelling, in which the foundations are first firmly laid and only then one proceeds to construct and to enlarge the rooms,” the great mathematician David Hilbert [wrote in 1905](https://www.leocorry.com/_files/ugd/e6fef7_dbe9131a54ed48c996cd517588422cdd.pdf). Rather, scientists should first find “comfortable spaces to wander around and only subsequently, when signs appear here and there that the loose foundations are not able to sustain the expansion of the rooms, \[should they\] support and fortify them.”

“This is not a weakness,” he continued, “but rather the right and healthy path of development.”

After all, a formalization effort can have very different consequences when it aims to go beyond cementing loose foundations.

## The Austere Academy

It’s possible to take clarity and rigor too far.

Consider one of math’s most famous (or infamous, depending on whom you ask) schools of thought, a philosophy put forth by a [secret society of mathematicians](https://www.quantamagazine.org/inside-the-secret-math-society-known-as-nicolas-bourbaki-20201109/) called Bourbaki.

In the mid-1930s, mathematics in France had been suffering for decades. The country had lost a generation of promising students and researchers during World War I; its universities were teaching math in uncoordinated, fragmented ways, using materials that were woefully out of date. And so several young mathematicians banded together to form Bourbaki. They began with a modest goal: to bring the French curriculum into the modern era with a new, more cohesive textbook. Soon, though, their ambitions grew much larger. Today, Bourbaki (whose members remain a secret) has produced over 40 volumes, covering every conceivable area of mathematics.

![Black-and-white photo of a group of men posing in front of a building.](https://www.quantamagazine.org/wp-content/uploads/2026/03/Bourbaki-secret-society-cr-Nicolas-Bourbaki-cropped-scaled.webp)

The secret math society Bourbaki — founded in the 1930s — valued rigor, abstraction, and logic above all else. Among its founding members were Henri Cartan (standing, far left), André Weil (standing, second from right) and Szolem Mandelbrojt (seated, right).

The real legacy of these books, however, is not their content but their style. Bourbaki prioritized abstraction over all else, eschewing concrete examples and calculations in favor of only the most general statements. They presented each proof as a series of logical deductions, usually without reference to any underlying intuition or rationale.

“It’s a style that is very formal,” said [Leo Corry](https://www.leocorry.com/), a historian at Tel Aviv University. “Very austere.”

Bourbaki’s philosophy quickly spread, influencing mathematics almost everywhere. “It had an enormous influence,” said [Patrick Massot](https://www.imo.universite-paris-saclay.fr/~patrick.massot/en/) of Paris-Saclay University. “The most successful parts have become so much part of the common mathematical knowledge and style that it’s hard to think of what it was before.”

The subject became far more airtight, if increasingly abstract and difficult. “This was not a brilliant decision from a pedagogical point of view,” [wrote Maurice Mashaal](https://bookstore.ams.org/bourbaki/), the longtime editor of *Pour la Science* and the author of a book on Bourbaki. But the group’s emphasis on abstraction molded research mathematics in ways that are harder to assess.

Some mathematicians revere Bourbaki’s approach. Massot argues that through abstraction and elegance, “you are forced to understand what really makes things work, and what is just noise.” Formalization, in this view, has brought clarity.

But Bourbaki’s project had unforeseen consequences as well. Their vocabulary and style weren’t a natural fit for every type of mathematics. For example, the fields of combinatorics (often described as the science of counting) and graph theory (the science of networks) tend to be highly concrete and visual. Perhaps, then, it’s no surprise that for decades, they were sidelined at most prestigious institutions in the United States and parts of Europe; they were only able to thrive in places where Bourbaki’s influence was limited, like Hungary.

“Graph theory \[was\] the slum of topology,” said [Béla Bollobás](https://www.maths.cam.ac.uk/person/bb12) of the University of Cambridge. “That atmosphere changed only recently. Very recently.”

Even in fields that did flourish under the Bourbaki framework — algebra, topology, analysis — some mathematicians worry that Bourbaki was too successful. According to them, the ways in which proofs are written and theories constructed have become overly homogeneous.

“There is a sense that it decreased the cultural diversity of mathematics,” said [Aravind Asok](https://dornsife.usc.edu/aravind-asok/) of the University of Southern California. Before Bourbaki, for instance, there were many versions of algebraic geometry. In France, for example, methods were grounded in analysis, while in Italy, a geometric style reigned.

The Italian school, which lacked rigor and involved many errors, quickly faded as Bourbaki’s influence spread. Certainly, algebraic geometry became more reliable. But by cutting off other paths of possible progress, Bourbaki introduced a new problem. “I don’t want any mathematics where one mode dominates,” Asok said. “There is a cultural history to mathematics that deserves to be preserved.”

## Proofs and Promises

Despite the best efforts of Bourbaki, Cauchy, and Weierstrass, truly formal proofs have always been objects of theory, not practice. Some mathematicians now hope that computers can change that.

Since the 1960s, researchers have been developing computer programs called proof assistants. Using a proof assistant, a mathematician will write every line of a proof (including every definition) in a language that the computer can understand, and then the proof assistant will check the logic. If even a single step doesn’t follow from a preceding one — if you haven’t rigorously shown every tiny detail, like the fact that 1 + 1 equals 2 — then the program will not consider the proof correct.

Currently, mathematicians are hoping to formalize all of mathematics using a proof assistant called Lean. They’ve created a library of more than 120,000 definitions so far and have verified a quarter of a million theorems. Several mathematicians maintain this database, keeping it up to date and vetting new contributions. (A handful of them do this work full time.) They’ve received over $10 million in funding, mostly from the billionaire financier Alex Gerko.

Samuel Velasco/ *Quanta Magazine*

Lean is “revolutionary,” said [Alex Kontorovich](https://sites.math.rutgers.edu/~alexk/) of Rutgers University, in part because it breaks up a single proof into many pieces that can each be handled separately, verified independently, and reused in other proofs. “Imagine if every time you wanted to build a spaceship, every single engineer has to understand every single component — from mining the iron ore, to smelting it, designing it. Now with these formal systems, for the first time, you can do mathematics and just buy somebody’s part off the shelf.”

But it usually takes months to write and vet definitions and proofs in Lean. (In some cases, formalizing a proof takes only a few weeks; in others, more than a year.) Some mathematicians therefore worry that their time and resources would be better spent on other pursuits. They argue that while verifying proofs is important, checking them by hand has worked well enough. Even though “there are many, many errors in the literature,” Asok said, “my experience is that mathematics is remarkably robust.” There’s little danger, in other words, that the whole edifice of math could come crashing down.

That said, using Lean has also led to new math. In 2019, the mathematician [Peter Scholze](https://people.mpim-bonn.mpg.de/scholze/) wrote a proof by hand of a theorem that was poised to play a key role in a new mathematical theory he was developing. But the proof was extremely complicated, and he struggled to determine if it was correct. So in late 2020, a team of mathematicians led by [Johan Commelin](https://math.commelin.net/) and [Adam Topaz](https://adamtopaz.com/) set out to [formalize the proof in Lean](https://www.quantamagazine.org/lean-computer-program-confirms-peter-scholze-proof-20210728/). Several months later, they confirmed that it was correct, giving mathematicians greater confidence in Scholze’s new theory. And in the process, they found a cleaner proof and refined some of Scholze’s original ideas.

“It forces you to think about mathematics in the right way,” said [Kevin Buzzard](https://profiles.imperial.ac.uk/k.buzzard), a mathematician at Imperial College London and one of Lean’s biggest proponents. “It forces you to become an artist.” (Buzzard has spent the past year working to use Lean to [formalize a proof of Fermat’s Last Theorem](https://imperialcollegelondon.github.io/FLT/), an important result whose proof is famously long and complicated.)

![Man in a blue sweater smiling in front of piles of papers.](https://www.quantamagazine.org/wp-content/uploads/2026/03/Kevin-Buzzard-cr-Courtesy-of-Kevin-Buzzard.webp)

Kevin Buzzard is currently using Lean to formalize the proof of Fermat’s Last Theorem, one of the most famous results in math. “I want this argument to be a thing of beauty,” he said. “I want it to slip down the throat.” Courtesy of Kevin Buzzard

Moreover, taking the time to develop Lean now might be a good investment in a future where artificial intelligence is bound to play a bigger role in mathematics. As mathematicians try to use AI to write informal proofs, it will be more important to verify their accuracy using programs like Lean. (Plus, AI is already helping to write Lean proofs more efficiently.)

Still, the widespread adoption of Lean comes with risks. Could Lean, like Bourbaki, subtly shift the kinds of questions that mathematicians find interesting?

## A ‘Moving, Shifting Beast’

Within Lean, there is little room for conceptual, methodological, or ideological diversity.

For one thing, every new proof in Lean can only use formal definitions and theorems that have already been verified and stored in its library. This means that these definitions and proofs need to seamlessly fit together. It also means that updating or changing a definition creates a domino effect: Proofs written with the old definition may not work with the new one.

That could be a problem. Mathematics is “not a fixed and finite and formalized enterprise,” said [Stephanie Dick](https://www.sfu.ca/communication/people/faculty/stephanie-dick.html) of Simon Fraser University. “It’s a moving, shifting beast, and the terms of it are changing all the time.”

![Blond woman sitting on a staircase.](https://www.quantamagazine.org/wp-content/uploads/2026/03/Stephanie-Dick-cr-Eric-Sucar_University-of-Pennsylvania.webp)

Stephanie Dick is wary of how new technologies, such as proof assistants, might subtly influence what questions mathematicians ask in their research. Eric Sucar/University of Pennsylvania

Because of this, previous attempts to digitize mathematical results (such as a 1994 project called the [QED Manifesto](https://www.cs.ru.nl/~freek/qed/qed.html)) quickly deteriorated into arguments about which definitions and frameworks to use. “Everybody loves this idea in principle, but in practice, it’s a nightmare,” Dick said. “They disagree about what programming language to write in. … There’s fundamental disagreement about whether this kind of project could be possible at all.”

To avoid these disagreements, a dedicated group of Lean users is responsible for determining which definitions should go into Lean’s library and how those definitions should be coded — much as Wikipedia does it, according to [Simon DeDeo](https://www.cmu.edu/dietrich/sds/people/faculty/simon-dedeo.html) of Carnegie Mellon University.

“It is really a community trying to do the best thing for the community,” said [Emily Riehl](https://math.jhu.edu/~eriehl/), a mathematician at Johns Hopkins University. So far, it’s worked, and the process has been largely democratic. But, she said, “what’s bad about it is, there is one decision that will be made in the end, \[when\] in many cases, there’s not one correct decision. Some people will be happy, and other people will be unhappy.”

Just as Bourbaki’s approach was optimal for certain subjects and not others, the Lean language and the choice of definitions that go into its library are better suited to some areas of math than others. They’re a good fit for number theory and algebraic geometry, for instance. Graph theory and category theory, not so much.

This is just one way Lean could make math more homogeneous. Dick points out that past technologies — even [choices of which notation to use](https://www.quantamagazine.org/how-writing-changes-mathematical-thought-20260325/) — have subtly changed how mathematicians approach their work. Lean might encourage them to focus on developing concepts that can be formalized more easily, even if they don’t realize it. “I’ve now found so many cases where something like that is happening,” she said — where “it actually shifts the focus and the intuition and the understanding away from the mathematical problem domain toward the behavior of this system.”

There is certainly a lot to be excited about when it comes to Lean. But Riehl, for her part, thinks that mathematicians should try to use more than one kind of proof assistant, rather than relying solely on Lean. She’s not sure how practical that will be, however, given how much effort formalization requires.

## On Overcorrection

For centuries now, mathematicians have sought greater rigor by focusing on whether they can verify every line of a proof. But that wasn’t always the case. To Descartes in the 1600s, rigor meant being able to hold an idea in your head and intuitively understand why it’s true. As a result, according to [Akshay Venkatesh](https://www.ias.edu/math/people/faculty/venkatesh) of the Institute for Advanced Study, older proofs used to “have a kind of grittiness.”

“It doesn’t make for a formally elegant argument,” he said. But it’s “something a human being can easily understand.” Modern proofs are more elegant, sure. But they’re also more slippery, harder for the mind to get a grip on. (Interestingly, Buzzard used similar language while discussing his hopes for how Lean would influence proof-writing. “I want this argument to be a thing of beauty,” he said. “I want it to slip down the throat.”)

This trend reflects a notion that’s now taken for granted: that proof should lie at the heart of math. “There’s no question that the concept of proof is a fundamental part of mathematics,” Venkatesh said. But “where I think there should be a question is whether it should be the defining feature of mathematics.”

Formalization in Lean would continue this trend of prioritizing proof. But it’s not the only future that mathematicians are imagining. Researchers are encouraged to think “that the only way forward is to have papers be Lean-formalized,” Asok said. “I would argue another way is that we just take a step back and stop writing so much. But that’s antithetical to the incentives that are in place.”

It’s impossible to predict all the possible ways that formalization in Lean could impact mathematics. What’s clear from history is that math has a tendency to self-correct — and that the future of this next wave of formalization will be one we haven’t imagined yet.

*Editor’s Note: Alex Kontorovich is a member of* Quanta Magazine *’s advisory board.*

***Correction:*** *March 27, 2026  
An earlier version of this story referred to Maurice Mashaal as a mathematician. He is in fact a journalist. Also, Béla Bollobás’s affiliation has been updated to reflect that he is primarily affiliated with the University of Cambridge.*