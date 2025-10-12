---
title: "Cubegeek"
source: "https://web.archive.org/web/20240526124958/https://www.cubegeek.com/2020/04/index.html"
author:
  - "[[Cubegeek]]"
published:
created: 2025-10-12
description: "Big Data Analytics, perspectives from a 25 year practitioner."
tags:
  - "cubegeek"
---
The Wayback Machine - https://web.archive.org/web/20240526124958/https://www.cubegeek.com/2020/04/index.html

[« August 2019](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/2019/08/index.html) | [Main](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/) | [May 2020 »](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/2020/05/index.html)

### Closures in Go + Some Memories

***Blah Abstract***  
So displaying my ignorance to the world, I am taking the chance that some of this will be useful as notes in the future. Being wordy, explaining things to myself is how it works. So, sorry to bore you if you already understand closures. Having a good teacher makes all the difference and right now my teacher is [Mark McGranaghan.](https://web.archive.org/web/20240526124958/https://markmcgranaghan.com/) I learned about Go about 7 years ago when I first left enterprise computing and started with open source. I was hanging out in East Culver City behind See's with dudes whom I should find again. Anyway. One of those dudes was excitedly talking about what golang was good for, and primarily it was about Google finding a way to stop declaring headers etc as they had been doing with C and C++. It made execution of everything 20% faster (at least). Since I always loved Pascal and static typing, I was inspired by that feature of Go. It wasn't baked at the time. In the meantime, even though all of the utilities of Vertica were written in Python, my fearless leader chose Ruby for our cloud-native development. I liked Ruby (then) over Python, PHP, JavaScript and all the other minor languages. I never liked Java, and I never had enough use for C or C++. So while it took a while to learn enough Ruby gems to be dangerous, I loved the elegance of the language, even though it was desperately difficult for me to distinguigh its regular syntax to the DSL that my boss was inserting into the code. As I started writing Ruby, I fell under the spell of building classes into an elegant (so I thought) higher level syntax. Others on my team made it very top down like scripting with no frills. While I was happy about using **pry** for interactive debugging, I eventually consigned myself to needing JRuby to speed the bastard up. And of course by the time Spark came around and more 'data scientists' (one day I'll be more gracious) started sprouting wings, I had to defend Ruby against Python more often.

While I heard this and that over the years about Haskell and Clojure, I tried to stay disinterested. But I definitely liked the idea of functional programming. I haven't really thought much about polymorphism or inheritance since the 80s. Funny, people still respect Smalltalk. While our engineering team was mastering Scala en masse, I was happy doing more stuff with JRuby and andvanced SQL in Vertica, not to mention the cool orchestration stuff I could do with Docker (now that we were done with Chef and Veewee and VirtualBox) and Terraform. Not that I needed to get into those weeds. We had dedicated heads for that. I remained focused on replication of complex business rules and workflows in the data governance domain.

Now I'm rather sick of everything. So I'm doing Go for my own whatever purposes. I'm going to Go into the ground, like it was Java and C++ and C all put together. Which it is, as far as I'm concerned. Which means for the 3rd time, I'm going to recast all of my stuff into a better language. Hopefully for the last time. I will expect that everything will eventually have a Go translation, even Apache Beam which I care about.

***Lede***  
Closures were easy to understand because I have had several situations where I was unable to articulate my need for exactly what they do and I wanted to do it. I can't remember precisely, but it was definitely a situation in which I didn't want to use globals but I felt stuck. Maybe when I see the old Ruby code I'll remember. I never got into passing blocks and yielding and whatnot, although I might have if it weren't for expedience and the convenient transom of my boss. But I understand closures now. Thanks Mark.

***Code***  
// p.15 closures

// a closure is a first class function that allows the use of free variables. You  
// use a closure to keep track of a set of variables that are declared within an  
// outer function. such that subsequent calls to the function can operate on that  
// set of retained variables as if they were globals. They are not, however. They  
// are local to the closure even after it has finished executing. The variable  
// space is retained in the definition space of the closure.

package main

import "fmt"

func say\_hello(msg string) {  
fmt.Println(msg)

}

func return\_anon\_func() func(string) {  
// return anonymous function  
return func(msg string) {  
fmt.Println(msg)  
}  
}

func int\_seq() func() int {  
i:= 0  
return func() int {  
i++  
return i  
}  
}

func main() {

say\_hello("Hello")

func(msg string){  
fmt.Println(msg)  
}("Hello Anonymous")

print\_func:= return\_anon\_func()  
print\_func("Hellow returned from Anon")

next\_int:= int\_seq()  
fmt.Println(next\_int())  
fmt.Println(next\_int())

next\_int2:= int\_seq()  
fmt.Println(next\_int2())

}

That pretty much nailed it for me. I will conform my language to the formality in due time. But I get it. Happy Happy. Joy Joy.

### A New Leaf

[![image from www.google.com](https://web.archive.org/web/20240526124958im_/https://cobb.typepad.com/.a/6a00d834515ae969e2025d9b456e0c200c-320wi "image from www.google.com")](https://web.archive.org/web/20240526124958/https://cobb.typepad.com/.a/6a00d834515ae969e2025d9b456e0c200c-popup)

So today I decided to stop playing videogames. I may or may not go cold turkey, but I basically need to liberate more time in my life to do what I want to do technically which is to build stuff for myself. The secondary consequence is that I will stop reading literature. I may or may not go cold turkey, but this is a slightly easier decision. I simply have no more great desire to learn in the dimension of wisdom. So let's get on with it shall we?

Into those slots of personal entertainment and literacy I will require **golang**. So my aim is to immerse myself in this particular language and build up a library of data wrangling and data engineering tools. So I'm most likely to go and recode everything I've coded and move on from there. I simply aim to master the language, and be wordy in doing so. I'm happy to commit to it.

That means a big deal for Cubegeek. It means I'll be switching a lot more attention to this blog and its subjects than that of Cobb. It will also mean things for my github repo.

I expect to get all Apache, from scratchy and take the short term hit with a dearth of Python. And I probably won't do anything further in Ruby. Which of course kills me because I've been doing everything with Ruby for the past 8 years. What a pain. So as Joe Rogan would say, I'm eating that punch.

It has been a while since I've been hermetic, but that's the plan. I will work for myself. I'm going to stop expecting other people to give me interesting things to do.

## Categories

- [AWS (24)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/aws/)
- [Best Practices (46)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/current_affairs/)
- [DB Tech (3)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (73)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20240526124958/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20240526124958/https://www.typepad.com/ "TypePad")

## Search

## May 2023

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 2 | 3 | [4](https://web.archive.org/web/20240526124958/https://www.cubegeek.com/2023/05/it-begins-again.html) | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 |  |  |  |