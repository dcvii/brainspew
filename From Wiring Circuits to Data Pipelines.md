---
title: "From Wiring Circuits to Data Pipelines"
source: "https://dataengineeringcentral.substack.com/p/from-wiring-circuits-to-data-pipelines?publication_id=1224799&post_id=184378371&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Daniel Beach]]"
published: 2026-01-20
created: 2026-01-20
description: "A Career in Data with Andy Leonard"
tags:
  - "clippings"
---
<iframe xmlns="http://www.w3.org/1999/xhtml" src="https://substack.com/visited-surface-frame" width="0" height="0" class="visitedSurfacesIFrame-yy8AJL"></iframe><iframe xmlns="http://www.w3.org/1999/xhtml" src="https://substack.com/session-attribution-frame" width="0" height="0" class="visitedSurfacesIFrame-yy8AJL"></iframe>

[

![Data Engineering Central](https://substackcdn.com/image/fetch/$s_!pIVQ!,w_80,h_80,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F880c179a-d4f4-4f41-a70c-48e557c48f38_256x256.png)

](https://dataengineeringcentral.substack.com/)

# [![Data Engineering Central](https://substackcdn.com/image/fetch/$s_!8m0m!,e_trim:10:white/e_trim:10:transparent/h_72,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff7a54c15-7911-486e-bab7-e14f14c848a5_1344x256.jpeg)](https://dataengineeringcentral.substack.com/)

[![Data Engineering Central](https://substackcdn.com/image/fetch/$s_!9izE!,w_152,h_152,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd6a29bf1-b54f-4014-b5d7-6d7274f707df_2184x978.png)](https://dataengineeringcentral.substack.com/)

Data Engineering Central Podcast

From Wiring Circuits to Data Pipelines

1×

0:00

Current time: 0:00 / Total time: -2:10:01

\-2:10:01

<audio src="https://api.substack.com/api/v1/audio/upload/579b0ca8-f6b0-4694-b1a5-58773cd8479f/src?token=843b7f30-2061-4d28-a6b6-9a76b1bc1442" preload="auto">Audio playback is not supported on your browser. Please upgrade.</audio>

0:10

So welcome to the Data Engineering Central podcast. I'm Dan Beach, your host. Today we have Andy with us. How's it going, Andy?

0:16

It's going well, Dan. How are you?

0:19

uh great so in iowa even though it's january it's like supposed to hit like 55 today which is strange for us we don't have a bunch of snow it's like weird i don't know what's the weather like out in virginia in the winter

0:33

We're in an unseasonably warm period here as well. The high today is going to be in the low 70s. Yeah, which is summertime, springtime weather here for Virginia. That's going to change, I understand. I'm a bit of a weather weenie.

0:51

We can talk about that if you'd like to get into it, but I'm not a professional by any stretch.

0:57

Yeah, it's like deer season here right now, so I have, like, my late muzzleloader tags. I have two to fill, and it's just it makes it hard because there's no snow. Probably, you know, I can't. I'm trying to track a deer. Yeah, this is different, right? It's like hunting in the summer. I want to see tracks.

1:12

If it's white with snow, I can see a deer in the woods. Right now, everything looks gray and like a deer, which means I can't shoot one, basically. That's what that means.

1:22

I hunted when I was a kid, a much younger man, and... It never stuck with me. I'm not against hunting by any stretch, and I love deer meat. I think we're coming up on doe season if we haven't hit that yet here. So the last couple of weeks of deer season, they allow you to hunt doe here.

1:47

What else do you have? Do you have black bears out there? I don't know. What's in Virginia?

1:53

Virginia is a weird state. I mean, I've been to Iowa a few times. I don't know everything about Iowa, and I'm lousy about geography. But it's certainly not the largest state. But it is almost as long as Texas. So we're 400 miles east to west. And I think Texas is like 450 or something.

2:16

So we're you know, it's a it is a sizable state in that dimension. We have mountains. We have the Appalachian Mountains, the Blue Ridge part of the Appalachian Mountains out here. We have the Cumberland Gap is in the farthest west part of the state. Yeah. So Kentucky and Tennessee and Virginia joined.

2:36

My dad lived out there for a while before he passed. And I used to go visit him and enjoy and appreciate that. We have a Piedmont area. That's where I live, kind of southern central Virginia. Red clay is our soil here. Sure. And then, of course, we have the beach,

2:56

that area and the swamp down south in Northern Virginia is a, you know, very densely populated part of the state, which kind of, it's kind of the tail that wags the dog because it's an outgrowth of D.C., highly metropolitan area.

3:13

I love the Appalachian Trail. I've read a couple of books like it's my dream because I've read a bunch of like through hikes of the Appalachian Trail. So like that's it's like every software engineer's dream, right? I want to retire and go hike the Appalachian Trail basically.

3:25

So a good friend is doing that. Joe Webb is a is a legend in the SQL Server data community. He's a database administrator extraordinaire and lives in. He used to live in Tennessee, moved to Alabama. He's the past eight 10, 12 years, he's been hiking a portion of the Appalachian Trail.

3:47

Sure, doing the section hike, yeah.

3:49

Yeah, and he blogs about it and writes about it and uses it as examples for business topics and data topics. That's awesome. He's worth a follow on LinkedIn or elsewhere.

4:02

Yeah, I'll check him out. Yeah, because it's, I think, the first Appalachian Trail book I read. It was, like, in my life I was reading. It was, like, I haven't been in life's crisis. I opened this Appalachian Trail book on my Kindle, and it's, like,

4:13

Some dude is like in his 40s and he's a software engineer and he's like, I have, you know, at least this job. And I'm like, oh, this is a sign from God. I need to leave my job and go like that. Right.

4:25

Right. Yeah, it's it's a it's a good and noble thing. And I think any of those. uncomfortable, frankly unsafe endeavors that we let ourselves go on to, those are experiences where the growth happens. And, you know, you just you don't get that in a safe career or a safe life.

4:50

You know, I'm not saying, you know, go be a daredevil. I'm certainly not saying go live, you know, some, you know, go fight in a war or something like that. That's also unsafe. But do the things that stretch you and exercise courage, which requires fear. Yeah, for sure. You have to face fear. To be courageous.

5:15

Yeah, I've noticed. So feel the fear. Step up. Do the things that are uncomfortable.

5:21

Yeah, I'm a big backpacker. I like backpacking a lot, like climbing mountains, stuff like that. And I've, it's funny that you said that because it does relate to your job to tech because tech and data, especially data, you know, it's very, I would say it's, you know, it's stressful. It's, you know, dealing with things, with people,

5:40

with technology, things break, dealing with hard situations. And yeah, I totally agree that doing things outside doing hard things they translate back to the tech right you're able to overcome obstacles and you're like oh if i can climb a mountain i guess i can solve this deadlock issue or something right like i'll survive kind of thing

5:59

totally agree yeah so you said some stuff earlier and i want to catch up on, you said you mentioned DBA and stuff, and that's how I know you, because I followed you forever. Because when I cut my teeth, I cut it basically on SQL Server. That's where I got in.

6:18

I'd just be curious to hear your story from way back in the beginning, how you even got in. Was it you got into databases? Did you get into programming? Like, how did you make your way into tech when you were a young then?

6:29

Gosh, well, it's a long story.

6:33

That's fine. So

6:38

Years ago, back when the years began with the one, I was an electronics technician and I became an electrician. I was in the Virginia Army National Guard. I worked on TOE, which stands for Tube Launched Optically Sighted Wire Guided TOW Missiles Guided Systems. They were tank killers. And, um, that was what I was trained in.

7:06

We've got a six week, great six week course on electronics. Um, and I was in, in the early eighties. So we were still trained on vacuum tubes, uh, and then transistors. So it was a neat kind of bridge spot to be in to learn electronics. Um, I, Didn't go to college right away. I started attending community college.

7:31

I believe I was 26 or so when I did. It took me six years to get a two-year degree. I was working at the same time. And in that, I transitioned from being more of an electronics technician into an electrician because I got hired to work at a manufacturing plant in Richmond. And That was a fantastic experience.

7:59

My very first experience with computers was over 50 years ago. In 2025, in May of 2025, I celebrated 50 years. That means I started in May of 1975. I was 11. My neighbor retired. We lived out in the sticks. And my neighbor retired from the Air Force, 20 years in the Air Force. He was an engineer.

8:22

He worked on the Air Force counterpart to NASA. Sure. Whenever NASA and the military did joint missions, and they did, they launched by satellites and the like. And he was on the Air Force side of that. He built a computer at home. in 1975 and I was interested in, you know, going over there, bugging him.

8:49

I was severely ADHD and OCD. We didn't have those terms back then. My mom used to describe me as particular, which fit, which fit.

9:00

This sounds like a, this sounds like a movie, you know, back in the sticks in Virginia.

9:04

Shouldn't it? Yeah. Build a computer. A couple, a couple of jokes. I used to say that, um, That we were so far out in the sticks that we had to pipe in sunshine. But the moonshine came in mason jars. There you go. True story.

9:21

And now I say I suffer from CDO, which is OCD with the letters in alphabetical order. But John Barker was that man's name. And he... Approached my parents and said, look, Andy's interested in this stuff and he's got a bit of an aptitude, I think. I'd love to share with him if you don't mind and all four.

9:45

So, you know, it was kind of, I think it was a little bit of self-defense on their part because anything to keep me out of the house. I was a handful. And so I learned Motorola 6800 machine code before I turned 12th. And that's hex, hexadecimal.

10:05

I still remember some of those mnemonics and the hex codes for them. But that started me. And then later I learned basic. And that kind of started me off. And then I found that come back around when I got to working at the, I worked at a Stanley hardware plant that's no longer in Richmond.

10:25

And we had this kind of, interesting moment inflection point in my life where the day shift, I wasn't day shift, the day shift electricians and engineers were trying to code this rotary assembly table that actually assembled barrel bolts, if you know what they are. And they were upgrading from old relay ladder logic to a programmable logic controller,

10:51

an Allen Bradley. they ran Motorola 68,000 controllers. It turns out those were like the great, great, great grandkids of these machines I worked on 20 years, that I learned on 20 years earlier. Largely the same instruction set expanded a little, obviously. 20 years will do that. But they were trying to solve a particular problem in You know,

11:17

without diving too much into the control systems philosophy, relay ladder logic was the way that we did things. And it was just a set of booleans basically drawn the old way we used to physically wire relays back in the old days. And that was what the interface looked like on a laptop when you would interface

11:38

with the programmable logic controller or PLC. But you had the ability to go in and do code blocks of the machine code, the hexadecimal. If you couldn't quite figure out how to design the relay ladder logic, some of it wasn't representable. Some of the things that the controller was capable of, you couldn't represent in RLL.

12:03

And they were trying to solve a problem, and I jumped in and did a little bit of tinkering with it. We were all working as a team. I didn't, you know, solve the thing, but I did probably add the last couple of three Legos to the wall, if you will, to it.

12:19

Because I had this approach that I knew that they didn't, and they couldn't be represented in this, you know, old electrician's kind of playbook. This is in the 80s, roughly. 90s. 90s. 94, 95. And it kind of came together for me. My old hobby showed up at work. And then...

12:43

I ended up becoming a journeyman electrician and then a master electrician in the Commonwealth of Virginia, then an electrical contractor. I formed my own business. It started off with me traveling around with a laptop and using AutoCAD software to create electrical drawings. for shops that could build electrical control panels, mostly for manufacturing,

13:11

but for some commercial buildings and stuff. But they didn't have the skill of producing the drawings. And I did. So I would do that. I think I made 20, 25 bucks an hour is what I charged for doing that. And they kept asking me questions. Like, you know, we need some help programming this Alan Bradley PLC.

13:32

Do you know anybody? And I was like, well, yeah, me. And so I kind of got back into that part of it. And I was, again, shocked at how much the stuff I learned when I was a kid applied to that thinking and, you know, program logic flow. linear program logic flow especially.

13:54

And it was very helpful and I knew more than I thought I knew. Then my old basic programming grew into visual basic programming and I got into at the factory, I ended up working at two factories before I stopped. I ended up doing human machine interface. which is software platforms that are called Wonderware and RS View.

14:23

And what they are is kind of like drag and drop interfaces. And you connect them to programmable logic controllers. and they interact, they collect data on how the machine is working. And some of that data is used for deciding how to respond. The simplest example would probably be a temperature sensor that works a lot like a thermostat,

14:44

except it's a digitized version of a thermostat. So maybe you've got a tank and you've got some liquid in there that you're using maybe for electroplating. That was an example that we had at the hardware plant. And that has to maintain a certain temperature. And it's, you know, there's literal burners underneath that are, you know,

15:04

you can see the flames in a plant, you know, that's turning on the gas flames that are keeping it at a temperature. And they switch on and off. They'll come on, you know, ignite and run to the temperature rises to the right level. And then they'll stop. And you end up with this very, um, You know,

15:22

hysteresis-driven square, if you're looking at the graph, and the temperature stays within a certain range. And it's driven by automation. The temperature sensor senses it. It goes back to a very digital, a computer-driven programmable logic controller. And when it sees that temperature drop on a scan below the threshold, it turns on the gas.

15:43

When it sees it hit the upper threshold, it turns off the gas. Very Boolean output there. So working with these HMIs, these human machine interfaces, I ended up starting a, they called it an integrator. It's a manufacturing term, the systems integrator. And it meant I could redesign often, sometimes design from scratch, the control system.

16:09

And then I could build the panels. I knew how to do that part, my electrical background. And that's what I would do. I'd build them, wire the electrical control panels, and then put them in the back of my pickup and drive them to the plant, mostly working here in Virginia and North Carolina. That's crazy.

16:26

It's like full, that's like the full loop.

16:29

It was, yeah. And it was really cool, though. And then programmed the PLCs. That was kind of a second piece of the job, a second skill, if you will. And then programming the human-machine interfaces, again, another one. And being able to do that full stack was very... It was personally satisfying.

16:48

I enjoyed that, being able to be a turnkey person to deliver all that. And there was this one time... This is getting to SQL Server now. This one time in 99... seven or so. I'm redesigning all of this stuff. And it's this holiday weekend coming up. I want to say it was a Labor Day weekend.

17:08

And because of the way that it worked out, they were going to shut down the plant on a Friday and do a little mini shutdown exercise. It was a Burlington plant. And they Part of the plant I was working in was the wool came into this particular machine.

17:25

It was washed and pulled and stretched and processed and eventually turned into thread coming out the other end of it. So it was that automation product. By the way, if you've never hung around manufacturing. I actually have. So you get it, right? Seeing raw material come in and all of this stuff happened to it and then the

17:48

output, this product. and all of the quality that goes into it. the math and the engineering, mechanical and electrical engineering that goes, it's, for me, it's just fascinating. I was like a kid in a candy store, you know, just being around the machines.

18:04

Yeah, that was my first job, surprisingly. And it's funny to hear you talk about this stuff because I guess my experience is more like 2007 timeframe. Like one of my first jobs was at basically a tractor plant. Everybody knows who John Deere is, but I worked for the competitor, the red ones, the red tractors, red combines,

18:22

that's Case IH. I went there as a manufacturing engineer, so I saw a lot of the guys like you're talking about, the contractors. I saw a lot of those. It's crazy. It's like a world people don't know about. Just all the test suites that get set up. Every different station has their own, you know, they might be,

18:44

who knows, they're testing some, you know, on a tractor. It might be testing different circuits, electronics, all the cab stuff, right? If you think about it, similar to a car, all electronics in there. And just the amount of custom, you're right, just the testing huge circuits. You know, I'd see these guys with these huge Pro-E and SolidWorks,

19:02

just massive electrical diagrams. And somebody had to, like, take that and translate it into some test box. We had to wire something up and then write some code and test it. It's a whole world of stuff that people don't know about for sure.

19:18

Yeah, you're absolutely right about it. And Dan, as a sad commentary, a lot of manufacturing has left the United States. And I forget which book it was that I read. I don't read very fast, but I make up for it by reading as much as I can.

19:33

And they talked about kind of mourning the dearth of manufacturing in the U.S., that we lost more than just the economic piece of it, which is what most people talk about. We lost a part of our soul as a nation.

19:50

All the machinists. I mean, it's a whole set of people, like quality control machinists, people that specialize in injection molding or tool and dye guys. That's just like scratches the surface of... All the stuff that goes in there, right?

20:05

Yeah, and it was a huge cultural hit we took. And this particular person was lamenting that and comparing it to some of the other shifts that have occurred in culture that, you know, some of them haven't worked out. They haven't produced positive consequences. And probably the biggest overarching point they made, and I agree,

20:29

based on the argument presented, that... We became more isolated culturally. We became more depressed. Our community suffered. We became less connected on a community level. And I think a lot of that, his point was a lot of it stems from, especially in your area of the country, you're in the Midwest. A ton of manufacturing here.

20:56

The rust belt, you know, yeah. And y'all lost the most.

21:00

Yeah, you drive through all the small towns here, even the town like I grew up in. I grew up in, my claim to fame is I grew up in the only county in Iowa without a working stoplight. So, like... You know, I had to drive like over an hour to get to the nearest Walmart,

21:14

but like all these little towns. Like if I go back and see my parents, there's like a, there's an empty machine, like a large machine shop, like custom fabrication, CNC, tool and dye thing. That's like every one of those little small towns in Iowa had one of those places

21:29

that was building stuff or something on the other side of the country and all that's, most of that's gone, right? There's some of it still there, but yeah.

21:37

You see the old shells, the old shells of factories. And I go, that Burlington plant that I'm talking about now, that's been, you know, leveled. There's a lot there now and, you know, just an empty lot. And I go by there every now and then because I, gosh, I worked in there for three or four years.

21:55

They were my number one customer. And this particular machine, kind of picking the story back up, We were going to be offline for five days. They're going to leave power one and stuff like that. But they were turning it. You get it. A mini shutdown over that Labor Day weekend.

22:11

They had some emergency stuff they needed to do and they just took advantage of it. So I turned on the data points in the human machine interface software software. were collected and identified by the term tag. Tag means something different in other stuff that we use mostly today, like tagging blog posts and stuff like that.

22:35

But that was a data point. And it could be analog, it could be Boolean, there could be any number of data types associated with that tag. But to stress test it, It wasn't really in production. We were a little ahead of schedule, actually, at that point.

22:51

So I decided to stress it by turning on all of the data points and configuring the collection of data from those data points to the fastest frequency, which was every second. And there were over a thousand of them. And I said, I'm going to turn it on, store it to, I believe it was an Access 95.

23:11

I was about to ask that, like, what was the data storage at that time behind there? And that's probably a big deal back then, that much, a thousand data points every second.

23:21

Oh, gosh, that was big data.

23:23

There was a Kafka back then, right? It was a big deal.

23:27

Yeah. So it really was. Yeah. So I turned that on and I came back after the four or five days off. And I remember logging into the workstation there and it was running NT. I remember that. And it had a huge monitor. It was like 17 inch CRT. It was huge back then.

23:49

And I believe it was an MDB file type for access. It's been so long. And it was four gigs in size, which was huge. It had grown to that, running all of those data points, collecting all that data. And I double clicked on it to open it, and it wouldn't open.

24:11

So I went back to my office later that day. I went on and did some other work. I actually started another database and I went into the HMI, turned it down to, you know, collecting data points every 10 minutes or so, tags, values, which was a little more manageable.

24:28

And I ran a test for that day and saw that, yeah, my data was showing up. My thousand tags were being recorded. And I was like, I really want to solve this problem. What if I run into a scenario where I need to collect that much data? So this is telling. I went to Netscape Navigator.

24:46

I want to say I had a, it was either, I think it was a Pentium at that time, Pentium or Pentium 2. Opened Netscape Navigator, connected to CompuServe. And in Netscape Navigator, through my CompuServe there, I was able to browse to altavista.digital.com. And in those days, that was our Google. And I put in Microsoft database.

25:16

And it came back, of course, with stuff about access. And it mentioned this thing called SQL Server. I'd never heard of it before. And so... Back in those days, we had computer shows where you could go to a... There was a place in Mechanicsville just outside of Richmond, Virginia called The Showplace.

25:37

And the building's still there, but it's kind of a mall now, and there's a lot of little shops. I actually went there a couple of months ago, walked through there with my wife, and there's all sorts of shops and stuff in there. We actually had lunch there. But The Showplace... And they had a computer show.

25:56

People would sell hardware and software and anything related to computers. And there was a not-for-resale copy of SQL Server 6.5 for sale for $20. So I bought it. And I ran down to the Burlington plant the next week. And I had my little server there. And I installed it. Didn't ask anybody for permission. Just installed it.

26:25

and ran a similar test. It wasn't a long weekend. This was the middle to the end of September by this point. But I collected about two and a half gigs of data over that weekend, same test, all the tags every second. Back then, I want to say we had query analyzer.

26:48

I was going to say it was an SMS at that.

26:52

No, not then. Not then. Yeah, so it was query analyzer. I was able to open it, connect to the database, read the table, and it was a one big table design back before we called it OBD. And, um, yeah, it was bringing by, I mean, it was taking minutes to run a query, uh, to go for,

27:11

especially for a specific, like, you know, period of time, that specific hours when I was isolating it to, but yeah, it worked. And so, right. I went to the plant manager and I said, this is what we need. I think to, to go forward. Um, they bought a licensed copy of it and, um, which was the right,

27:31

right and proper thing to do. Um, And then SQL Server 7.0 came out, and we upgraded to that, and gosh, it was so much better than 6.5. And that's how I got into SQL Server. We were still doing... I went on through SQL Server 2000 and did some work there,

27:53

and I kind of stopped being a software developer. By that time, I had... I've been doing doing a lot of software development in Visual Basic, working through the different versions all the way up to 6.0. I had kind of pivoted when I want to say it was version four.

28:12

It may have been three that first came out with the idea of doing object oriented programming in Visual Basic, but definitely in four. And I pivoted into that, you know, designing classes and learning how they work. And, you know, on and off, just dabbling with data as a kind of on the periphery.

28:34

And then I got a job in Florida. So it's in 2000 when the NAFTA stuff hit, which was kind of the thing that changed the dynamic there in manufacturing for y'all. For us too, Burlington began going out of business at that point. And I describe it in an attempted humor by saying in 2000, you know,

29:03

I lost 250 pounds on a house. My marriage ended. And the... You know, just the business folded. I lost my customers. I went to work for my very first consulting job. And it was wild because I think I was making like $30,000 a year. You know, when I 30, 35,000,

29:32

when I left kind of working for other people and went full time for myself. And it wasn't that many years. I want to say it was four or five, six years when I took my next job, my first consulting job. And it was 70,000 with the offering. I was like, wow. You know, I probably could have.

29:49

gotten more money looking back, but I didn't know.

29:52

Was that first consulting job like specific to SQL server or what, what was the,

29:58

it was software development, but it was, you know, there was data work going on in there. There was a guy there who was very good at SQL server. I learned a lot more than I knew from, from him. When, when I got that job, I developed on an application for a, a compact. If you remember compact company,

30:19

They had an early handheld called an, I believe it was called an IPAC. And there was a Windows CE, I think was the operating system on that. I wrote a visual basic app that would look up, do lookups against a prescription drug database and populate dropdowns, you know, go from like the high category down through,

30:46

Lower, you know, filtering, basically filtering. And the idea was to create electronic prescriptions, an electronic prescription application because of poor handwriting and the like. I forget the number. It was in the thousands of deaths were attributed to the wrong medication being prescribed or something being wrong about the prescription because of handwriting.

31:14

So we, we pitched that, we didn't sell that, but I wrote the prototype for it. And, um, what year is this like roughly 2001, 2001.

31:24

Okay.

31:25

Yeah. 2000, 2001 in that, that neck of the woods. And then I met my, uh, my wife whom I'm married to now we're, we're cut this year. It'll be, uh, 24 years, June 1st, we will have been married. She's hung in there. Um, she, She likes to joke and say she won.

31:42

I was married 20 years for the first wife, my first wife. And my first wife and I had two wonderful daughters, and they're the mothers of my grandchildren. I have five grandchildren now. And me and my wife have three children. And so five kids, five grandkids.

32:01

Are any of them going to tech? Do you tell them to be a programmer with AI? Like, you want any of them to go into tech or no?

32:08

Yeah, so they... They all have dabbled, some more or less. My younger daughter from my first marriage, she is managing a team of data engineers now. Nice. And she has a master's in data science. They're all smart.

32:27

They're all really cool people. So you rubbed off, basically.

32:30

I guess. Yeah, they got stuck with half this DNA, you know. But another joke I make is they all suffer from ADHD as well. Saying suffer from ADHD is definitely a dual-edged sword. So once you learn to manage it, you can kind of turn it on and off when you need to. And it can help.

32:50

Believe it or not, in some ways, definitely has its downsides.

32:54

But it sounds like you kind of came like when I got into tech, I got more into like I came of age and like the Lampstack, Pearl, MySQL, all that kind of stuff. But sure. When I. Got my first job on like a data warehousing team.

33:12

That was like the age of where like SQL server was like the OLAP system, but it was OLTP system. It was like, which is different than today, the world we live in. It was like, it was like, it was basically SQL server, Oracle, pick it. Kimball data warehouse and, you know, the same SQL server.

33:30

That's both the Ola, the OLTPs, a lot of all the transactions are coming in. That is your analytics. Like that's your analytics store too. You just change the data model, you know, SSIS, SSRS like that. It's a, it was a strange time because it's so different than what we have today. Right. It's totally different now.

33:49

Yeah, you're absolutely right. And you know, it was, it's, it's very interesting. Um, you know, seeing my children learn what they're learning about. So my youngest daughter now, she's 20 and going to Virginia Tech, and she's in the CS track there and entertaining the idea of maybe taking kind of a a speedy,

34:15

I'm trying to think of the right terminology, but she wouldn't have, I think in about a year, she could get a master's. It's an accelerated, that's the word I was looking for, accelerated track for that. She's considering it. She's also considering getting married. So there's, you know,

34:31

this,

34:32

this balance kind of going on there and she probably could do both, but we'll see. We'll see how it all works out. But, you know, kind of watching all of them go through this and, and, And, you know, and coping with the, again, coping with the ADHD, enjoying the benefits of it as well.

34:50

But, you know, all of them have it, Dan. And so I have a joke where I say, what are the odds that I would marry two women that would pass on ADHD to all of my children? And I know the answer to that because I'm all right at stats.

35:06

It's one in four, but that's not where they got it. That's what makes the joke funny, right? I'm the ADHD guy, so that's where they get it.

35:21

How did you become an expert in SQL Server and data? Did you say it's just purely experience back then? Did you try to do any certifications, learn? Did you start watching Brent Ozar, SQL Server Radio? I remember those guys. Did you dive into it? dive in deep into the whole of data and SQL.

35:45

Yeah. So I'll, I'll start with a disclaimer. I don't, I shun the term expert. I say experienced a lot. You use that. You use the experience. I don't consider myself an expert at anything. The, I, I thrive off and this is, I keep bringing up ADHD, but it's part of it is you need to change.

36:08

You need that stimulus. That's part of what kind of attracted me to this field in the first place. John saw it, you know, when I was 11. So how did that translate into it? So I, I wasn't, I was actually a Microsoft certified solutions developer at, at, Right at the turning point of the cusp of .NET.

36:31

I was tinkering with .NET. We didn't have a GUI at the time. We would write. I would write in Notepad. Sure. And save the files, you know, with a .VB extension and then call, you know, the .NET build tools. That's how we did it back then. Turn of the century. And I made it into coding...

36:55

In another manufacturing plant, I was working on the intranet, and I was doing basically what we call now manufacturing execution systems. I had built one, didn't know what to call it. And it was completely web-based. I learned HTML back then in the 90s. And then active server pages later.

37:21

But I built this, that first version, I called it a plant wide web. And it was a combination of, you know, taking my CAD skills. You could turn the AutoCAD drawing into, I don't know if it's Jeff or GIF, but that file. And then on early browsers, you could use those as kind of like maps.

37:42

You could create areas of a GIF that would be subject to some things. You could do things like change the color in a portion of that image. And that was kind of the graphical interface I did for it. So I took the whole plant, AutoCAD drawings, they had them, the plant engineers had those,

38:01

and I converted it into that GIF file. And the whole plant would be on the first page and it would be either red, green or red, red, green or yellow, you know, using the stoplight analogy. All configurable and a collection of different scoped attributes that would basically determine is this machine in green,

38:23

in the yellow or in the red. And the SQL server behind it in the background. It was. Yeah. And it's like that machine I was telling you about that actually contributed to it. I was, As a, just on a lark, I was learning all of this stuff.

38:38

I already knew how to, you know, do GIF stuff in HTML files. This was before active server pages or anything like that. So effectively what I wrote was a Visual Basic 3 or 4, maybe a 5 app that was a hidden icon that would live in the taskbar. And it wasn't hidden, sorry.

39:00

It was minimized to the system tray. And you could open it up and it would kind of be your configurations screen. What it did was every 10 minutes, it was on a timer running in Visual Basic. It would overwrite the HTM file. We didn't even have dynamic HTML files when I first wrote this.

39:22

Well, maybe we did and I didn't know about them. But that's how it would. put the data in behind, it would visualize what you were seeing on the screen. It's a very static HTM file, but it was overwritten every 10 minutes. So everybody was running Netscape at the plant in the 90s there,

39:38

and they would just hit refresh every 10 minutes or so. And the page would show an update on the plant wide web. And the whole plant would be green. But it was broken into sections. You would click on a section and you may see, well, you know,

39:52

four out of five sections were green and one was in the yellow. Well, based on the math and configurations, that would equate to at the zoomed out level, a green status. And so on and so forth. You could zoom into each of those and eventually you could zoom down to the actual machines and see which status,

40:13

you know, these 80 machines that died material produced in the plant. You know, each the status of each one of those, they would be, you know, green, red or yellow as well. That led into me working on an intranet at another plant. It turned out that that plant wide web was an early manufacturing execution system.

40:37

And I worked at a plant in Jacksonville, accidentally got a job in Jacksonville, Florida.

40:44

This is your little Florida stint.

40:46

Yeah, that was it. Stayed down there for three and a half years. The first two of my and Christy's three children were born there and left that manufacturing job. To go do web intelligence for business objects at my very first data warehouse gig.

41:06

Did you just say business objects? I did say business objects. Oh, man, SAP.

41:11

Yeah. That's the first. Well, it was. It became SAP.

41:15

I thought it was my first data warehouse. I, my first tech job was a data analyst on a SQL server team that was business objects. Yeah.

41:23

So, okay. So web intelligence was this thing in 2002, 2003. Um, and, They had just ported that. It was kind of a neat setup. It was, you know, Business Objects ran in its own GUI. This was a port to the web. They called it web intelligence. And, you know, the universe, the semantic layer called the universe.

41:48

That was all in there. And nothing's changed.

41:51

It's just like the same, just different regurgitation.

41:56

It is. It really is. I wrote about this. My youngest daughter interviewed me for my 50th anniversary in computing back in May. We did a show. One of the benefits, 50 years of experience in computing is pretty much useless. But one of the places where it has some purposes is what you just said.

42:19

And you've got it too, right? You've been in this 20 years, 20, 30 years. You see that, those patterns repeating. Mm-hmm. kind of on that macro level that's one of the things you can almost predict what's coming based on where we are in the cycle you know you know it's you may may not

42:35

have the details right but you know it's going to be this in its latest incarnation so did did that and i got that they they were running they ported that using something called java server pages i didn't even know that existed at the time in

42:50

the web and i'd done like i said i'd done that plant wide webs i'd had that um I had that web page I had built for that. So I kind of knew my way around.

43:00

Was SSIS in the scene at this point or not?

43:03

No, no, it wasn't. And I didn't know about DTS had come along because it was an add-on to data transformation services, became an add-on to SQL Server 2000. I didn't know anything about that. But I was fortunate that I was in Jacksonville. because that's where Brian Knight lived and lives in that area.

43:24

And he's one of the original authors of the data transformation services books. And I ended up working for him, but not before I found myself. So the way I got my MCSD, Microsoft Certified Solutions Developer, was you had to test on a couple of products and Visual Basic was a gimme.

43:44

But I started working with something called Visual Interdev. And it was an active server pages client. And it was the very first time I opened Visual Studio. That was a brand new thing that I encountered there to start with. VB had its own GUI at that time. Well, it turned out that

44:07

The reason I got hired is they were struggling with these reports in the Java server pages. And I had SQL Server on my resume at that point. I had, you know, development of intranet reporting from the previous gig. And there was a converter where you could load up. active server pages, you know, right into visual interdev.

44:35

I knew this. And they had ported the Java server pages app to active server pages. And so that's what we were running because we were running a Microsoft stack. I forget the, it wasn't IIS, I don't think at the time, but it may have been, or it may have been something else they were running over.

44:55

They had a web server running there. I believe it was IIS, an early version of Internet Integration Services, I think is what that was. I forget. But it was web serving. When they ported it over, and at that time, Business Objects, I believe, was in Paris. And when they ported it from Java server pages,

45:15

they made a couple of changes to some of the methods. But their refactor job missed some spots. This may be, I don't know, it's probably 90 or 100 files, active server pages files. And they created like new methods that would work better in ASP than JSP. And they had like a number two at the end of it.

45:39

But they forgot to put the number two in some of the calls for it. So the page would blow up. Some of these pages, you'd be navigating along and it would give you, yeah, I can't find that. Like, well, I know how to troubleshoot this. It's an active service page. It's certified in this.

45:54

I installed interdev on my machine. Totally no permission. Again, ported the project, you know, created a project, imported all of the files. I mean, it was easy. There were tools in there, you know, for refactoring and finding stuff that was broken links effectively in the code. Fixed it. deployed it, again, not asking anybody.

46:16

We weren't technically in production at the time. There were power users running on what was going to be promoted to our production server and fixed all the bugs, zipped up the code, sent it to the Business Objects team over in Paris and said, hey, this works. You missed a few things. It wasn't much.

46:33

I mean, really, it was tens of thousands of lines of code. We were talking about a couple of dozen that had the wrong function called. They sent me a thank you note back and I was done. We were building reports at that point. We had people specializing in that sort of work. I'm not a good report builder.

46:54

It turns out I write reports like an engineer, which the first time I heard that I thought was a compliment. It's not. But we had analysts doing the reports and my job was done. In the meantime, We had a five-person team. The SQL Server data warehouse person they had hired was struggling.

47:17

He was very smart, but he was from India, and he didn't communicate well with other people. And you don't have to be from India to not communicate well with other people. I think it was mostly because he was so intelligent. And I've seen this in a number of really smart people. They don't do social interaction well.

47:37

And he was struggling with that more than most. He may have been the worst case I ever experienced in my career. I like the guy. We got along. He's a great guy. And I learned from him quite a bit, even as the job went on. My boss called me in and said, this, this guy is struggling.

47:58

Um, we're going to move him. We're not firing him. We're going to move him into doing something that's probably a little bit better suited for. And we're going to have him crafting like these one-off applications that we need to support our data project here, our data warehouse project.

48:12

And he's going to be building like apps and C sharp and stuff like that. We need somebody to fill that. You've done your job. Your part's working. You're kind of done. Um, And you're the only other person on the team with SQL Server on their resume. Can you do what we're calling an application database administrator?

48:34

And I was like, sure. How hard can it be to tell the developers no? Because that had been my experience with database administrators.

48:44

Go find the long-running query. Kill that spit. That's it.

48:48

Yeah. That was it. So I got in, and Dan, I was so far in over my head, I had no idea what a special thing was.

48:57

It's the best place to be, though.

49:01

You nailed it, right? Because there's no way to go but up from there. And I developed a saying. I have a number of little andyisms that I share, especially with my kids who are in tech. And the one that came out of that experience was, you have to make the problem give up before you do.

49:23

And that turns out to be a function of stubbornness. We can call it persistence if you want to. But, Dan, my hair's been longer, but it's never covered my redneck. Just straight up. If you call me a redneck, I am not insulted. I'm like, yeah, okay. And the sky is blue. What's new?

49:44

Most people mean something in 2026 that's different from how I define redneck. And it's not flattering at all. But you know what? I grew up this way and I own, you know, I own me. For sure. I'm just going to put it that way. I'm a Christian, actually, so I believe God owns me.

50:04

But that's all I'm going to say about that. We're talking about tech. And, you know, I've always been stubborn. It helped me in this case to kind of dig out of being so far down and over my head. I didn't know, you know, my way out.

50:20

I know one of your Christian friends, by the way. He lives... He's a good friend of mine. Roger Vassie. I can call out. Do you know Roger? He's one of my best friends. I spend a lot of time with him. I'm going to be in a cabin with him in the woods... And probably like two weeks.

50:35

I will. Maybe I'll send him this after. Shout out to Roger. I go to Bible study with him. Go to the same church.

50:41

Okay. Awesome. Awesome stuff. Well, okay. Then I can talk a little bit freely, a little more freely. Maybe I would. But it's so much a part of my life. And it really pushed me into, you know, technical evangelism. in addition to, you know, Christian evangelism.

51:03

And it turns out there's a lot of overlap in community and church thinking and the way we express ourselves and definitely a motive for helping others and sharing the knowledge, you know, any knowledge that I happened upon. And that's, I think when, you know, when people say typically when they use the word expert,

51:23

that's what they're referring to. The blog is 20 years old this year. And, you know, it's just they've it's a false impression. I'll say that to start with, because about ninety nine percent about what I write about is not something I figured out. That's about one percent. The ninety nine percent is stuff I learned from the community.

51:45

So I'm not self-taught. I'm community taught. And I had this. Motivation, this this drive. And it became a mission to share as much of that knowledge as I could to help others as much as I could. I reap tremendous benefits out of it as a result.

52:09

In that data warehouse project, I was working for a student loan company there in Jacksonville. We got that project launched. I learned about star schemas. I learned about clustered indexing there. I am not a DBA, not to this day. I'm just not. I don't think like that. I'm still in the developer mindset.

52:33

I'll say I'm a developer, but I usually don't say software developer. I say data engineering developer or data engineer, which is software development, but it's a little narrow niche in there. And I'm good at that. I'm not here to, you know, I'm not playing being falsely humble or anything like that. I am a good data engineer.

52:55

I don't know why. It's a neck. It's just like a fish in water for me. You know, it just it's just that way. I was doing it before I knew what it was called. I was doing business intelligence in the Burlington plant in the 90s. I was having to build my own. Reporting platform.

53:13

Effectively, that's what Plant Wide Web was. I built my own data acquisitions, what I called it back then, which is now what we call data engineering, because it didn't exist. Nobody knew, you know, nobody knew this stuff. There was... pieces and parts of it built into the human machine interface, collecting the data tags and being able.

53:35

But you could collect those tags, Dan, back then. And about half the time, what I saw was people would have built that and not stored it. And I'm like, why would you not analyze this data, you know, later to see how you're doing today compared to how you were doing, you know, last week or month or whatever?

53:52

It just that was just obvious to me. But it wasn't obvious at the time. It is now. You know, why would you collect data and not store it? That's interesting. At the time, they weren't. It was just everything was live in real time. You think about it on the line, you know, when.

54:11

So when statistical process control started getting started taking on and it was 80s, 90s here in the United States, it became a big deal. Six Sigma. And now all of those terms are applied to software and people, you know, I'll talk to software engineers and they'll go, they used that in manufacturing?

54:29

And I'm like, that's where it came from. You know, W. Edwards Deming and, you know, the legends in these fields, it all came from manufacturing. And anyway, now it's all made its way into software. And it's good, not a complaint or anything like, but, you know, I cut my teeth on, you know, in the Stanley hardware plant,

54:52

collecting metrics and stuff like that. And sometimes we were just writing it down on, you know, on a piece of paper and then going and entering it into like an Excel 2.0 or something spreadsheet back then and doing analysis on it then. But, You know, all of these, again,

55:10

more of this 50 years of experience where it kind of comes into play, collecting the data. And, you know, that wasn't just a given back then. It was just it was all real time. It's right in front of the place. But like you were talking about quality control stuff, running the tests, that data was stored.

55:26

Even if it was stored manually at the time, it was stored. And eventually it found its way onto a computer somewhere at the case plan, I'm sure.

55:35

There's a lot of SQL Server Expresses running on desktops underneath somebody's desk, more or less.

55:42

Exactly. And that's, I mean, you know, we laugh now, but that's how we did it. And that was our IoT, if you think about it.

55:50

Yeah. It's been interesting to see the, like he's talked about data engineer now, like what it was called before. Like it was just, I remember there was no such thing as a data engineer. It was like, I just remember the popularity of like titles, like a data developer. I remember when that came on, you're a data developer.

56:09

I remember when business intelligence like that was a thing, especially around the SAP time period. Because I eventually ended up with that title business intelligence engineer, you know, and then. Nice. Eventually data engineer came along. It's just funny, but it's all the same stuff, right? Like.

56:25

It is. It's exactly the same. Yeah. Tools change. Exactly the same job. The names change, but we're picking up data from wherever it originates. And, you know, and that's the role of IoT and phones now. You know, you see a lot of that in wearables or, you know, the AI driven wearables or, you know,

56:47

this is where all that evolved from. These are now the originators of data in digital form. And once it gets into digital form, then we can store it. We've got a bajillion formats now we can store that data in and then another bajillion platforms we can use to move it around and format it and shape it and

57:08

analyze it. And it's wonderful. And I think AI is kind of our next, you know, AI is starting to be used more and more in the analysis process. And that's kind of where things are going. Yeah, picking all of this up.

57:21

The one thing I miss though, like when I think way back to those days, there's two things I want to say. Like I'm not a DBA either because I've sat next to DBAs and it is like a different, it's a different world, right? Like they sort of dabble in data analytics, but at the same time, like...

57:38

just a different mindset of like these i've sat next to guys who can run sql server failover clusters and can mirror stuff you know they just know every little nuance of everything which it's almost like they understand a machine more than anything right they're like a machine like you could think about it like i could maybe it's

57:55

a car or something they just know every little button and knob and turn and that the other thing i feel like people miss is and what i miss sometimes i remember like being a business objects administrator and like setting up i feel like that's what's missing nowadays it's like people haven't had that experience of

58:16

like what is it like to set up a server what is it like to open up ports what is it like to open up start this thing on the server and open up the ports and make sure the firewall is open between these two machines that they can talk Just all that stuff.

58:31

It's like, it's invisible now, more or less, right? It's totally, I feel like it's a lost art, not to everyone, but people now can just open a notebook in Databricks and they click run and magically there's compute there and it runs. You know what I'm saying? It's like, it's a different world now than it was.

58:48

It really is. And I, I like the velocity that we're able to achieve in producing reports, you know, getting data from wherever it originates to a report. We're in a, you know, in a whole new world and AI is changing it yet again. You know, this is the next iteration of that.

59:05

But yeah, I remember the, you know, when, when you were going to provision, uh, you know, a new server, that that meant getting into pickup and driving to town, going to the computer store and buying a box of parts, right? And coming back and assembling all of those, you know, installing the motherboard, installing the CPU,

59:29

installing the RAM, installing the network cards and the video card and all of that. And setting it up and hooking it to a monitor and then loading all the software, starting with the OS, you know, it just you're right. It is a different world. it really was. And it, you know, I'm not throwing off. I'm not,

59:50

you know, calling everybody whippersnappers and telling them to get off my lawn by any stretch. Although I am 62, I'm getting up there. Um, but it's, it, you know, I think understanding the bit of the history where we came from can help. And not just, not just for, you know,

1:00:10

it can certainly give you a little bit of perspective and a little bit of a glance at the long tail, but, Knowing, having our experiences, seeing these things go through a few iterations of the big cycle that lasts, I don't know, eight to 12 years, it's coming back around.

1:00:27

And having gone through this before, I've got a feel for, you know, where the bodies are buried. what's going to work here, what may not. And every single time through the cycle, I don't know if you've noticed this or not. It seems like they fixed something that you couldn't quite do well. It's like, yeah, there's the, the,

1:00:47

um, the, it's almost like the cycle is born pregnant with the next cycle. Um, And it's also carrying, not only is it carrying the seed of the next cycle in it, it's also carrying the poison pill of itself, right? It's going to die. It's going to kill itself because it can't address these needs that the businesses

1:01:12

require or the technology really needs. And so you see this on a miniature or smaller level. You see it on architectural level. You see it on things like as big as client server. And then you see the edge move farther out to where it is now. IoT phones and wearables is going to be the next big thing.

1:01:35

It's big now. You see that part happening. But then on a kind of a micro scale, not micro, but a medium scale, you see platforms.

1:01:44

Mm-hmm.

1:01:45

So you'll see in data engineering, you'll see, you know, a data transformation services come out. I worked on something called Data Mirror to start with. That was my first exposure to a platform that read the logs on an AS400 and wrote to SQL Server tables. And it was two agents, two services is what we call night agents.

1:02:08

I'm mixing my terms. Same function when you think about it. Two services running, one on the, you know, on the big ironed, And reading that log file and then transmitting across the network to another service that was then materializing that data in the SQL server. And that was my first one. That was data mirror.

1:02:27

And then I learned data transformation services from Brian Knight. And then SSIS, I learned we were all kind of learning it together as it came out. And I got to co-author one of the first books on SSIS. There were like 10 of us authors on that. Brian was the lead on that.

1:02:47

And there were a couple of other. Brian was a Microsoft valuable professional. And there were two other MVPs on that, Darren Green and Alan Mitchell. And then there were the rest of us people. And I had written an article for Visual Basic Magazine back then on XML, kind of converting XML over.

1:03:14

I don't even remember what it was about. And I'd written an article on reporting services for SQL Server Central, which Brian Knight and...

1:03:25

I spent a lot of time on that website.

1:03:27

Yeah. And Brian and Andy and Steve, they founded that. And then it was bought by Redgate. And Steve Jones is still with them, and he still does this. Part of his job is managing the SQL Server central website. And I'd written a reporting services article there. And Brian came to me.

1:03:51

I was working for him at that time at an insurance company in Jacksonville. And he said, do you want to join this writing team? He had, I think, three or four other authors that were working with him on the book. And they all got very busy with whatever they were doing and had to drop off the project,

1:04:10

which is horrible as an author. I know how that feels. That's a bad feeling when you've got to make that call. But they did. And it opened the door for a bunch of others to join in. A number of us worked there at that insurance company together. And so it was kind of interesting that, you know,

1:04:30

after work, we'd stick around after work and kind of powwow and Talk about, you know, what we were going to write on. We tried to coordinate the chapters in the book. Everybody was writing a chapter or three. I ended up writing two. What were your chapters on? Do you remember? One of them was on source control.

1:04:50

And I may have actually written the first published chapter on Visual Studio Team System. When it came out, you know, it was released in March of 2006. And I wrote my chapter in January of 2006. So if you remember the Visual Studio release cycle, the 2005 release cycle, they released in November.

1:05:17

It was November 7th, actually, just over 20 years ago. They released the Visual Studio 2005 release cycle. and SQL Server 2005 together. They tied them together intentionally. And after that, they all said, never again. We're not ever doing that again. They had originally included Visual Studio Team System in that.

1:05:38

They were going to release all three of them together. They got a little behind on deliverables with Team System, and they postponed it, and it was like March 16th or something, 2006, when they released it. But one of my chapters was on that. The other one was on just some demos on design patterns in SSIS. And I...

1:06:00

I think I wrote one of the three demos I documented. I remember one Kamal Hathi had written and demoed, did a video on it out at Microsoft, wrote him and said, can I publish your demo and kind of walk through, put it in my own words, you know,

1:06:14

what I see here kind of coming from my perspective as a software developer and all. And he absolutely, I credited him, of course, And I forget the other demo. It wasn't one that I wrote. It was something in the same sort of situation. The Microsoft developer community and DEA and SQL Server communities are the envy

1:06:39

of tech communities on the planet. They really are. It's very open, always been that way, very sharing, still is for the most part. And, yeah, it's just huge, huge things there. But, yeah, those were what those chapters were about. Got to do that. I remember Brian, when he was standing at my cube, asking me about it.

1:07:02

And he says, you know, do you want to do this? And I said, yes. And he said, Andy, this isn't like writing an article. This is a lot, you know, it's a lot more involved. And... I need to help, but if you say no, you know, we'll still be friends.

1:07:18

And I was like, no, I'll jump into chance. I didn't know what I was getting into, but who does? And, you know, I learned an awful lot. I was very blessed to have someone as experienced as an author as Brian Knight to work with their lead team and lots of questions and misunderstandings. I submitted that first chapter.

1:07:39

And the editor wrote me back and he said, this is too superficial and shallow for me to send to the technical editor. And I was like, all right. Like I wrote back and I said, are you firing me? And he says, no. And we ended up getting on the phone. And he says, tell me about yourself.

1:08:02

And I did. And I told him I was an engineer, had an associate's degree in electronics engineering technology and kind of been my thing. And he went, oh, and I'd never heard that reaction before, Dan. Oh. And he said, he said, what works for you as far as feedback goes? And I said, well. Just, you know,

1:08:23

explain to me what you want me to do, and I'll do my best to, you know, to write that way. And at that time, I wasn't lying. I said, I'm not a good writer. It's brand new to me. I've written a couple of articles, and it's the first time I've tried a book.

1:08:38

He said, okay, here's what I need you to do. every sentence that you wrote me is really the topic sentence of a paragraph. So I need you to expand on every one of those sentences pretty much, about 80% of them, really. And he said, just to let you know,

1:08:56

the reason I wrote back to you what I did was I'm more of a basketball coach, and I was trying to punch you and have you fight me back. That's what I wanted, and you didn't fight me back. You said, are you firing me? He says, so I was trying to motivate you.

1:09:15

I didn't realize you were an engineer. You're not the only engineer that reacted the way you did. That's why I wanted to call you and talk you through this. And it worked out. The chapter came out and, you know, that book sold crazy. I mean, I don't know.

1:09:28

It was tens of thousands of copies that that book sold. And it was like, you know, the equivalent of a John Grisham novel in tech books. And it's totally ruined me, right? That was my first book experience. So I've written over a dozen more. And it's been like, I think that book,

1:09:47

I made more money off that book than all the rest combined.

1:09:50

Speaking of content and writing and code, AI, what's your opinion on do you use AI for writing now? Do you use it for code? How is AI working into your workflow now?

1:10:04

yeah so the short answer is yes uh all of the above um it didn't start that way uh three years and what two months ago is when chat gpt officially launched uh november 2022 and um i played with it i tried to get it to do some code and it

1:10:25

didn't do very well back then and about every six or so months i would try again I think I didn't subscribe until it had been out for about a year. I started paying for a chat GPT, but I was still trying to get it to do stuff that it just wouldn't do well.

1:10:45

And I thought, yeah, okay, whatever. It'll probably get there one day. It'll definitely get better because I could see improvements and they were rapid. You know, it's definitely getting better and better. Hallucination was a huge problem. And, you know, it lied convincingly when it hallucinated. Mm-hmm.

1:11:05

It was useful every now and then for stuff, taking the edges off of an engineer-ridden email. That was one of the first uses I found for it. In March of last year, 10 months ago, I finally got ChatGPT to do something that I'd never seen it do before.

1:11:25

And actually, I say that, I got it to write some code and the code worked. But a friend of mine, a guy named Lev Selector, and Lev does a show every Friday at 2 p.m. on YouTube. He actually does it as a stream on Zoom. And if you go look Lev Selector up,

1:11:46

I think the credentials and stuff you need to connect to the live Zoom call are there. But he's got a YouTube channel, and it's the same stuff. He just hits record and does his show. He had been talking. Lev and I had worked together. I met him through a contract. um, in 2021. And, um, we became friends.

1:12:06

He's still friends. And, uh, he had been bragging about this thing called Claude code or not, not code at the time, Claude. And, um, I tried Claude and it actually wrote functional code for me in about 45 minutes. It wrote a rest API driven, um,

1:12:28

loader it loaded a tree view with fabric data factory pipelines and so could i learn that and code it yes but it would have taken me time and it would have been way more than the 45 minutes it took me to actually get the rest apis working because i i hadn't I dabbled with REST APIs,

1:12:55

but it was calling methods that are standard REST methods that I didn't even know existed. That's a fact. That's 10 months ago. And it did it in 45 minutes. That was my aha moment. And I realize that, and by the way, that app is out there. It's matured some.

1:13:16

It's called Fabric Navigator now, and it's available at my DELMSuite.com website. If you go search for Fabric Navigator, you'll probably find it. It's been out, I don't know, almost a year. And it's free. You can download it and I've got links in the help to blog posts where I tell you

1:13:35

how to set up the security so you can get everything going and use it. And I pat myself on the back a little bit. It was kind of cool. The interface to Fabric at that time was a little clunky online. It was a web-based interface. And they've made vast improvements to it here last year since then.

1:13:56

But at the time, they didn't have that kind of information density that they presented. And if you're a data engineer, you know this, Dan. You're not an enterprise data engineer. you're rarely working on one artifact at a time, one notebook or pipeline or script. It's usually you're creating a suite of these sorts of things,

1:14:17

often in the early and later phases of the kind of the flow. you can copy and paste and edit because those are the, some of the complexity lies in the middle. You can always, it's almost a bell curve. Uh, that's, you know, so transformation, that's where it's very case by case.

1:14:35

When you're looking at a source and transforming it so that it's.

1:14:38

Capturing business logic.

1:14:41

That's it. Yeah. That's all the complexity, but staging, that's not hard. You read the, whatever you write it to whatever. Um, once you've got the data kind of shaped and how you want it, and you may be in that operational data store kind of format, maybe even like something like a pre-star schema.

1:15:01

I don't know the right terms to describe all this, but then it's just a blow it out into a star. And it's almost like read it from the source, write it to stage. It's kind of that you're reading from this, whatever, and writing it into the star itself or,

1:15:15

you know, whatever the data vault, whatever you're using as your end goal shape there. But you know, kind of getting the information density is important because often you're working with a couple of dozen artifacts and they're going to be interrelated, especially when you're in that transformation phase and you're trying to figure things out. And some of these,

1:15:38

you know, you start looking at, at snowflake dimensions in a star schema, there may be five or six layers to that and determining how you're going to run that. I would, Today, if I'm building that, I'd build what I call a controller pipeline or even a script or whatever. And basically,

1:15:58

if it's a hierarchy that I'm loading in a snowflake, and it almost always is, then I load the top one first because I need that surrogate key from anything new added to that that may be added on the next layer down. And, you know, in a star, that's the way you get it.

1:16:13

If you get it, if you know, you know. And if you don't, it's not hard to learn. I learned it. And I think Dan learned it. So, you know, it's data engineering is just this kind of collection of skills where you learn these sorts of patterns and tips and tricks. And it becomes second nature pretty quickly. Honest.

1:16:29

It's not hard. It's just it's just involved to learn. And like everything else, every other job experience counts and matters.

1:16:38

data engineering data modeling especially what you're talking about it's like half art half science to me like totally almost more art than science a lot of times the

1:16:50

tuning is definitely that there's definitely skewed to art it really is and the science part comes in when you understand how to you know how to instrument What is effectively your code, your pipeline, your notebook, whatever? Again, you're doing what we do. You're capturing data from these points, and it's kind of self-similar. You're building a pipeline, say,

1:17:15

that's going to reach out to these IoT devices and states that into Parquet files. But you're instrumenting the process, and that becomes your initiating points of data. Like, when did this pipeline start? How many rows did we load? So you can calculate throughput and stuff like that. And you can try different approaches and see what works better.

1:17:40

How to initiate it. Do you scale the Spark cluster? Do you move this lever, move that lever?

1:17:50

It's interesting because I think about these things, especially in this data context, everything you just talked about and people can, the young guys can use AI. They cannot understand necessarily what they're working on, but all that, all those pieces play a part, understanding the background of like understanding indexes, why they need to exist, how,

1:18:10

why they exist a certain way, the difference, you know, whether it's clustering or partitioning. Now, when you talk about a lot of lake house architectures, It's kind of, you know, it's instead of clustering or partitioning and just understanding those. I feel like what I've noticed is like someone like you or I, when we use AI,

1:18:32

it's like we have built that over a long period of time, that knowledge of what's actually going on behind the scenes. And it assists us in making sure the AI is going down the right direction. It's doing what we want. The mistakes aren't being made like architecturally at architectural level, whether it's

1:18:48

Absolutely.

1:18:49

Modeling or otherwise. But that can be hidden from a lot of people now, right? Because if they don't know what a partition, why you would even need to partition data or why an index is important in this database. You know what I mean?

1:19:02

Yeah. And, you know, the AIs are getting so much smarter. As I said, they've gone through like five order of magnitude performance boosts, I think, in 2025 alone. And I've got this part of a unique perspective that many people don't that are trying to use AI. Of course, I've got 50 years experience doing that.

1:19:28

Only about 25 of those years is in data engineering. But I'm working with my son. He's 22 years old. And he started working with me last year just after I got into Coding with Cloud Code and producing that Fabric Navigator application. And he glommed right onto it, Dan.

1:19:50

And he picked it up and just ran with it in so many ways. I won't tell all the stories, but I've blogged about it. It's in my newsletter on Substack. And he's just... He's just knocked it, just knocked it out of the park. And we've been having, we've been comparing notes as we do this because, you know,

1:20:09

he's stuck with half my DNA, which his mother's DNA struggles to overcome, but doesn't quite, doesn't quite win most of the time. But I love working with him. Steven is his name. And he's enterprise data and analytics, AI engineer. And he wrote his own MCP server. He released it in August.

1:20:33

I think the official release was in September. It's called Durandal Memory. And it's out there on the NPM website and GitHub and all of that. And the idea was solving a problem that needed to be solved. It was these AIs suffer what we call context fatigue.

1:20:52

They kind of lose the thread and they started making suggestions that they already answered. You know, they asked questions they answered themselves 20 questions ago. But you're right about it. But I'll tell you what helped. totally unexpected working with him is he is not a software engineer.

1:21:10

He, he did support like network and computer support for three years. And that was his bailiwick. He's very good at it, but he says, you know, he tells me this about probably about halfway through since, you know, about five months ago or so. He says,

1:21:25

I'm beginning to think that not being a software developer and especially not being a data engineer, he was working with me on, you know, automating data engineering with AI. He said, I think not knowing what you know helps me more than it hurts me.

1:21:45

Sure. Isn't that preconceived of how they should do this, right? Exactly, right. Carrying that baggage along.

1:21:52

I mean, some of it is not helpful. I mean, the majority, for me, the vast majority of it isn't. Coming from, I was a software developer, then I became a data engineer, And now I'm I'm vibe coding and I'm pretty much doing that all the time. nowadays.

1:22:11

And while we're recording this, even, Cloud Code is running on a VM right behind the screen. If I minimize the window I'm talking to you on, there's a Cloud Code session going. It's probably going to run for four or five more hours. And it is working on some of my data engineering, sorry, data integration lifecycle management suite.

1:22:32

So I've got DILM suite and I've got DELM suite for data engineering. lifecycle management, Fabric Navigator is part of that. I've got a lot of support and a handful of customers out there, more than a handful, that are still running SSIS. And if you worked with SSIS,

1:22:51

especially if you tried to do it in an enterprise or as part of a team or both, you realize that when they built it, some of the stuff that's very important to us now, lifecycle management-wise, like the flow from dev to test to pride That wasn't as formalized as it is today.

1:23:12

I mean, 20 years ago, it just wasn't. It was the best we could do. I think SSIS is probably the most bang for the buck data engineering platform that I saw. First, certainly it was when it came out. And a number of people invested heavily in it. Some enterprises have thousands of packages, rather, not pipelines.

1:23:35

They're still running. They're running it locally. They're doing it because it just, with a capital J, works with a capital W. And there's a number of reasons why the friction from migrating off that into any of the other options that they have The motive to draw them into that next step just won't overcome that friction.

1:24:04

It's the same reason why all the COBOL mainframes are still running, right?

1:24:08

It's the same. 1959 is when COBOL came out, before I was born, okay?

1:24:14

Yeah, they're about like 10 miles from me. It's like a bunch of insurance companies running COBOL mainframes on server farms underneath their buildings like 10 miles from me.

1:24:25

Exactly. It's amazing to think about. Okay. Capital J just, capital W works. Why would they change? And will AI change COBOL? It might. It might be able to migrate some of those applications. But the truth is, the reason that these platforms are still in use is because they just work.

1:24:44

They just work. But it is interesting to think about the AI, the barriers. Like you talk about your son being a software developer and having these preconceived notions. Therefore, it makes him able to innovate in a way that maybe we couldn't.

1:24:57

It really does.

1:24:57

Because he doesn't have these ideas or whatever in his head, right? He just, oh, I want to do this thing, so I'm just going to do it because nobody told me it's not possible.

1:25:07

You're nailing it, Dan. Yeah, I read once that people of Inuit backgrounds, you know, in the Arctic, that they would sometimes take off on foot in the middle of just a horrific blizzard. You know, nowadays we expect... people to just freeze to death, not survive.

1:25:27

And they would just wrap way up and travel as far as they could that day and then sit down with their back to the wind and the snow blowing over them would basically build a shelter. And they would just keep hollowing it out until it was enough.

1:25:44

They just catch a night's sleep there, get up the next day and take hundreds of miles this way. And it was the mindset that you just described. They didn't have it in their mind that it was supposed to kill them. Their culture was, grandpa did this. Everybody, you know, grandma made this trip and still does.

1:26:05

You know, and you're right. It becomes a hindrance if you think it's supposed to kill you or you think we have to do it this way. And just watching him has been a fascinating experience for me. First off, we have a phenomenal relationship. I mean,

1:26:22

it just I and it means so much to me because I didn't have a relationship like this with my dad. So this is a whole different experience. In fact, it weirded me out when all of my kids wanted to spend time with me and be around me. I'm like, yeah, no, that's that's that's wrong.

1:26:42

You know, you're not supposed to feel that way about your dad. And it took me a while in some therapy to kind of work through all of that and get to the spot where, you know, I still have this very small, very deep inward kind of knee-jerk reaction whenever they say something nice. I'm just like, what?

1:26:59

I feel like we've had the same kind of dad, you know, conservative, small town, middle of the backwoods, you know. It's different.

1:27:07

Well, did the best, so to be fair, did the best he could. No doubt.

1:27:12

They just did things to you when you did something wrong. That probably doesn't happen today, you know.

1:27:17

No, no, not at all. I understand. It was a different time. We could say that, check that box and talk about the fun stuff. But now, gosh, this relationship is just incredible. So he shares things with me, way more open with me than I was about my dad.

1:27:36

And I share things with him that I wouldn't share with others either. But kind of having that meeting of the minds and him being You know, willing, even just willing to say what he said about that. That's that's huge. And some of the ideas we're working on right now,

1:27:56

and we're kind of bringing it cross pollinating from our various experiences, you know, him with this network management and tech support, IT support at a small startup. He's kind of bringing some experiences of that into what he's building with IT. He's also running a marketing company. He and his best friend from his teenage years,

1:28:18

they started a marketing company a couple of years ago, and they've just kind of got to that spot where they're beginning to make money. Nice. What is it called?

1:28:25

Make them go look it up.

1:28:27

It's called Shrike Media. So Shrike Media.

1:28:32

People will Google it if they want to check them out.

1:28:35

That's it. They've got a channel. They do a lot on social media, their Instagram and, and the like tick tock. Um, you may not see their work under their label, although they do have, I don't, I don't even, I'm sure, I'm not sure if they've got a tick tock, uh, channel or whatever you call it.

1:28:52

I don't do TikTok.

1:28:53

Yeah, do I?

1:28:54

So, but I do, you know, I'm definitely on Instagram and YouTube and stuff like that. But they've got some work posted, I know, on Instagram. And they are, you can just kind of go back and look at the early stuff they've left up, which I think is awesome, and just see how they've grown in their stuff.

1:29:12

And the latest things they did They were working for a client, a restaurant here in Farmville for the New Year's Eve party. And just the quality of the video and the editing and all of the stuff they did. He was actually whining to me because he was disappointed that it took like a day to get to,

1:29:35

I don't know, five or six thousand hits. And I'm like... I'd like to get 5,000 or 6,000 hits.

1:29:42

That's a good YouTube video for me, you know.

1:29:46

Yeah. And he's like, yeah, it took a day. Really? Yeah,

1:29:52

this brings up an interesting topic, if you have the time, of, like, this idea of, like, you have someone like your son, new... cloud code you would i mean in the old days you would call them like a junior developer or something maybe right like if you think about that i'm curious like it

1:30:10

seems like the barrier between and to some people this is probably controversial i don't know yeah this barrier between like what a senior engineer used to be able to do and what a developer, like a junior quote unquote, like that has shrunk just on a basis of like code production, et cetera. But it really makes us,

1:30:32

I feel like the, what I would call like the staff or principal or architect like that has become like that role is very, I think maybe it'll become more important in the future, right? Because these other barriers are down. Like the code barrier clearly has come down.

1:30:48

Whether people like it or not, it's just the world we live in now. So get on board. It's gone down. But this staff level of like, I don't know, like you said, working with people, talking to people, talking to the business, understanding requirements, like that's where the staff you know, like that upper level becomes that other stuff,

1:31:09

like the non-coding stuff becomes very important all of a sudden, which is what those people were doing mostly before anyways. I don't know if you agree with that or have seen that or where you think that'll go.

1:31:18

I completely agree with everything that you said about that. The importance of expertise, I think, is going to increase. And it is increasing. And it's because of Less and less because the AIs hallucinate. There was a tweet that came out, I don't know, two years ago, where somebody said, people are talking about AIs hallucinating.

1:31:47

That's all they do is hallucinate. LLMs, that's all they do. You should be shocked when they get it right. that the nearest neighbor algorithms in vector math and matrix math produce the right next word. That should be shocking to you. That's the miracle, not that they hallucinate. But all of that's evolved,

1:32:08

and it's evolving again at a rate we've never seen before in technology, just hands down. So I agree with everything you said. I would extend it to the... Two groups that come up in a book called Vibe Coding. I've just started listening to the audio book. It came out over the summer. It's by Gene Kim,

1:32:31

the DevOps guy, and a guy named Steve Yege, who's got like 20 years experience in Silicon Valley working for, I think... Amazon and Google and two other companies that they were a senior developer. But a slow adopter. Interesting mix, if you think about it. Just got into Git in 2021. Started Vibe Coding in March, like me.

1:32:58

And now he's got a book out about Vibe Coding. The two groups... that are also going to benefit from it are the older dogs, like myself, who, when I coded, you know, I still do data engineering, and I consider data engineering software development. Don't get me wrong,

1:33:20

but writing software as a software developer is something I haven't done in decades. And so I've been doing a little bit of it kind of on the side. I built those DILM suite tools over the past 10 years in C-sharp. I made the jump from VB to C-sharp in 2015.

1:33:41

And the only way I was able to do it was by making myself start a project in C-sharp. Some of that old code is in there and it's horrendous. That's what, in fact, I mentioned Cloud Code is working behind the scenes today. It's fixing that code. That's its job.

1:33:58

It's doing the first of five passes on that code. And I expect it to run all night because it's tens of thousands of hundreds of thousands of lines of code that it's looking at and making suggestions to change. It's in planning mode right now, which is super cool. That's group number one.

1:34:17

Group number two is the people kind of on the other side of Stephen that Stephen has exposure to technology. He kind of gets it. And so if you talk to him, you know, about what you're trying to do, you can explain it to him.

1:34:29

And, you know, I explained data engineering to him in about an hour and a half back in May. I kind of walked him through what we do. And he got it and ran with it. But the people beyond that, and some of these are people who fall into that category of analysts and more business people.

1:34:49

and especially people who are good at communications. Here's what I found. If you're using AI, and I mostly use Cloud Code, but I rely on Grok. Grok helps me a lot with infrastructure stuff. Grok wrote the eight-page script. I printed it to help me take my laptop.

1:35:08

I got a new laptop in November to make it dual boot into Ubuntu. So it wrote the script that I followed, and it nailed it. After I got into Ubuntu, it turns out that Ubuntu is highly flexible, Linux in general, a lot more flexibility than you get kind of in a more canned Windows 11 Pro install,

1:35:30

which is another way of saying it's also way more complicated to get some stuff that are very simple to get going in Windows Go. So I had to battle that back and forth. I was on my phone a lot while I had the Ubuntu image running on here. And I was typing scripts, reading them off my phone,

1:35:46

and I was usually clawed a lot to do the troubleshooting. But Grok got the image up and running. This has a neural processing unit in it, an NPU, this laptop. It has two GPUs. One of them is an NVIDIA 5080, and the other one is a... Shoot. I forget the model of it, but it's an Intel.

1:36:08

It's an Intel GPU, one of the old cells. You know, all of those types of things that it got going. And, you know, I can spell Linux, okay? I'm not anywhere near a Linux noob. I'm working my way up to that, okay? I can spell Python.

1:36:31

Again, and I'm having it design solutions for me because I can communicate with it. I'm having it design these solutions. I just leave it up to cloud code. I started doing this right after I saw the, I tried it after the bump I saw in the beginning of September, the quantum shift, the order of magnitude improvement.

1:36:54

And then I was hit and miss all through October. But in November, since November, I've been able to give it a good requirements doc kind of thing. And it always delivers what I want. That's number one. That changed since November. Number two change was about half the time it gets it right in one shot.

1:37:20

Sure.

1:37:21

I spend 30 or 45 minutes writing, mind you. And I give use cases. And I've learned to do that. I've had to change how I interact with the AIs. And this is very important. And I don't know if you do clips or stuff like that.

1:37:36

But if you do like little clips you post on shorts on YouTube or TikToks or whatever, then put this in there. There is no way to start working in AI at this point in 2026 even without putting your hands on the keyboard, opening up a GUI or CLI and starting to type.

1:38:01

There is something that happens in that interaction, in that exchange with it and what the individual learns. Me, even with 50 years of experience developing software, I had to learn the nuance and the flow. I had to learn how to size the bytes of the task. I was asking it to bite off and chew at one time.

1:38:27

And say, don't do this and tell it specifically, hey, don't do this.

1:38:31

Exactly.

1:38:32

Don't write this code.

1:38:34

The size of the bytes... Has jumped every time we hit one of those order of magnitude things. I am not making that up. It is, you know, five orders of magnitude over what it was when I started in March right now. That's why it's running in the background. That's why it's chewing on this stuff.

1:38:51

And it's probably going to run all night because I was able to give it. Essentially, the accumulation of about four or five days worth of work, bits and pieces here. And I know to store these in a markdown document. And I know to label them by some part of the topic.

1:39:10

And I'm giving it different pieces of the architecture. And I slowly pull the curtain back on honestly all the code I've been working on. for data integration lifecycle management suite since 2015. Since I started coding in C-sharp today, I was finally able to say, okay, you now have permission to go into this directory.

1:39:33

You know what I'm trying to do. You know the problems I was trying to solve. You know my approaches to solving them. I was trying to enable DevOps for SSIS in a number of these applications that I built out there. And I believe there's still a market out there. I know from my existing customers there is.

1:39:53

But I believe there's a market that I haven't reached yet. And part of that is because the user interfaces that I created for some of these, the big one is my SSIS framework. And it didn't have a user interface, Dan. I tried since 2014 to write that user interface various and sundry ways,

1:40:14

and I wasn't able to do it. But I've been able to produce this just in 2025. I've been able to use Cloud Code in my Data Engineering Friday show to build a framework interface using Cloud Code. live in front of the audience. I've been getting the hallucinations and the code blowing up and having to do the

1:40:37

reboots right there in front of God and everybody every Friday since January 17th. And I built that interface using Cloud Code through this. It's an Azure Data Factory framework, not an SSIS one, but it did that and it worked. And what was totally unexpected

1:41:00

is I feel about this like I felt 50 years ago when I was 12 years old and able to, and what it is, is it's not the code I've learned because it isn't the code. I'm not writing the code. What I'm doing is I'm producing. I'm producing results.

1:41:18

And it took time for me to sink my mind and learn these new patterns of thought and what's going to work for that AI and what's not. And just since March, 10 short months is all it's taken me to get to the point where I feel confident and comfortable handing over the code. I'm not alone. Andre Karpathy,

1:41:42

a world-famous software developer, wrote a lot of the tools that we use today in coding. Boris Czerny, who started Claude Code at Anthropic in September of 2024 as a little internal side project. Both of them posted in the last 10 days. Andre started by saying, I feel so behind.

1:42:05

Read that one.

1:42:06

You saw that one? Yeah. And Boris's reply, me too. And if you read that.

1:42:12

That catches you, doesn't it? Really?

1:42:15

It's like, wait a minute.

1:42:16

It made me reevaluate myself a little bit. If they're saying that.

1:42:20

I don't know how it made you feel. I don't know how it made you feel, but I'll tell you what. It made me feel like, okay, I'm not alone, right? I'm right there struggling with you.

1:42:30

It's a new frontier and everybody's on the same frontier, right?

1:42:34

Yeah. And everybody is, you're absolutely right. Frontier is a great way to describe it. And it's, I can, but I can sense the joy in the post, right? They're feeling what I'm feeling, and you're probably feeling it too. And it's not, all of a sudden,

1:42:52

what it clarified for me is it wasn't writing the code that made me feel good. It was seeing the code succeed. Solving a problem. Solving a problem.

1:43:01

Seeing the end result, like the feedback loop mentally.

1:43:04

And it's a hundred times faster now. Cloud Code writes code a thousand times faster than I can. And it used to take... The numbers I was using when I made this similar statement six months ago was it writes it 100 times faster than I do, and it gets it wrong about 90 percent of the time.

1:43:26

The end result is 10 times faster. That's OK. That's good. And now it's jumped in order of magnitude. Now it's a thousand and a hundred. That's where it is right now. And it's just that curve is not going anywhere. What does it mean? For our jobs? What does it mean for the, there are hundreds of thousands,

1:43:49

millions of software developers around the planet.

1:43:52

It does keep me up at night just a little bit.

1:43:55

I think it should. I think it's a fair thing, but.

1:43:58

Like figuring out how do I fit myself into this? Like, am I, should I just like focus on being a creator, you know?

1:44:08

It's a fair question. And I think the answer is yes. Not focus on being a creator, but keep creating. I think that's a noble and good thing that you're doing, Dan. And your newsletter is phenomenal. If you don't subscribe to Dan's newsletter, go do that. It's a great, great resource. I want to say it's Data Engineering Central.

1:44:28

And if you do that, you go to Substack.com and check that out. You can subscribe to Substack for free. Dan writes a lot of free stuff. I don't think I'm a paid subscriber yet. Probably going to happen here soon.

1:44:39

I'll give you a free one.

1:44:41

Don't do it. I want to pay. But it's, again, Substack right now feels a lot like Twitter did before 2012.

1:44:50

That's what I feel like.

1:44:52

Yeah, it's got a great, the algorithm is amazing. And I find every time it suggests somebody new for me, and my go-to used to be X. I'm still on X. I'm pretty active in there. I'm semi-active on Blue Sky, still active on LinkedIn.

1:45:08

My go-to switch late last year from when I scrolled, scrolling X, I started scrolling Substack. I got the phone app and I just – because the feed is amazing. And they're called notes on Substack. And you can post a note without posting a newsletter. You know, it's a cool platform. You owe it to yourself.

1:45:30

If you're thinking about becoming a creator, a writer – Or video. You can do video podcasts even. Yeah, anything. So I highly recommend you take a look at Substack. So just, you know, kind of, again, getting back to the AI pieces of that and how that all goes. I had this anecdote. I lived through this.

1:45:54

When I first got in to messing around with databases, again, the SQL Server specifically in the late 90s, Automation was in its infancy, especially database administration automation. And at that time, you would pay a DBA, $50,000 a year, and you had 10 databases maybe that they would manage in a large enterprise.

1:46:22

So if you did the math on that, you were paying about $5,000 a year. We're going to leave out the other expenses here. Go with me. It's contrived. $5,000 per year per database. Keep the database running, right? Well, then automation got a little bit better and monitoring got a little bit better. And the same DBA...

1:46:44

in just a few years, a couple of three years actually after that, could then monitor 20 databases and administer 20. And that cut the number in half. So now it costs you $2,500 per year for that same database. Well, that automation went, it did the same sort of quantum leaps that I'm seeing.

1:47:11

Not as fast, mind you, as what AI is doing. But it happened every couple of years. It would go an order of magnitude. And in some instances, and there's a lot of caveats, and you can just imagine asterisks across the screen here that go with this. But in some enterprises,

1:47:30

the DBAs that 15 years earlier were managing 10 databases started managing 10,000. That happened. That's real numbers. And so if you do the math on that, it was costing you $5,000 per database. Now it's costing you five bucks. That is a game changer. The economics of that is a game changer.

1:47:56

There's a lot of economics kind of rolling into similar economics rolling into ROI. Here's what I saw. I saw as the number of databases a DBA could be expected to administer increased. I saw the number of DBAs being hired fall off first. And then I saw DBAs being let go.

1:48:18

And that kind of was a chaotic period there that lasted, I don't know, a couple of three years over the early 2000s. Then the crazy thing happened. When the cost of managing the database dropped to, you know, five bucks, they couldn't find enough DBAs all of a sudden.

1:48:38

So the hiring ramped right back up and eventually exceeded where in my, you know, back of the napkin.

1:48:45

Most guys now probably make really good money because they're far between, you know what I'm saying?

1:48:51

Right. And so what happened was the market compensated in this way. This was the dynamic I observed. The number of DBAs needed dropped. And so they went and did other jobs. But, um, But as it pivoted, as the cost of the database itself dropped so dramatically, orders of magnitude, then the number of databases exploded.

1:49:18

And now all of a sudden, you needed more database administrators, again, to combat. Because despite Microsoft marketing, and I dinged them about this in about every third talk I deliver, back in SQL Server 2000 when they released it, it was so good, it would tune itself and you wouldn't need a DBA.

1:49:36

I was like, come on, guys, come on. And they made similar statements, you know, in the years since then. It's just like, yeah, really? And they're doing it again. And what it is, is automation. does that. It improves our ability as an individual to do more work, to get more done faster, of higher quality.

1:49:58

All of the metrics, if you're measuring them, we're going up and to the right. And that's as it should be. AI is no different. It's doing that. And that's going to continue regardless of what the market impact of that is. But I think in a couple of years,

1:50:15

because this is going to happen a lot faster than it took for DBAs and database automation. I think in a couple of years, here's some things that are going to be true. We're going to be able to, we're going to be speaking to probably our phone and giving it the documentation that we need,

1:50:31

which you can do that today, by the way. We're going to be telling it what we want it to do. We want to talk to the phone for somewhere between two and 20 minutes. And then we're going to say build it. And what it's going to return to us, if it gives us anything,

1:50:46

it's probably going to send us the equivalent of a URL, if not a URL. And the application is going to be up and running somewhere.

1:50:55

Mm-hmm.

1:50:56

We're probably not even going to know where. It's going to become invisible. You use that word. That's going to happen. A lot of things are going to fade into the background with this happens. And the equivalent of an executable or a website in 2026 is going to be surfaced at that point. And I predict...

1:51:16

that somewhere in a couple of three years timeframe that there's going to be this other thing that kind of emerges out of that. That's almost like a combination of both. We have it today, but it exists as an executable and as a website working together. We have API calls going back and forth and that sort of stuff,

1:51:34

but it is still more discreet than it's going to be. It is going to do exactly what Dan mentioned earlier. It's going to become invisible. It's going to fade into the infrastructure. And What we're going to see is chunks of functionality that emerge and they're going to

1:51:53

emerge so quickly that it's going to be the ability to create some problem solving chunk of functionality. is going to, the time to do that is going to be reduced to minutes, and the cost of it is going to be reduced to fractions of a cent. That's what's coming. What does that look like?

1:52:17

My friend Kevin Hazard wrote, he rarely writes on his sub stack, but he asked a question in 2014. We were working together, sitting in Boston Logan, and he said, what happens when When the cost of creating an application drops to zero, when the cost of the labor is reduced to zero, what does that world look like?

1:52:43

And that was such a prescient question because we're on that glide right now, that glide path. And he wrote about it. He mentioned it in that. He mentioned me because we were having the conversation. We've had many conversations over the past. I mentioned in a note in Substack that I pointed to his blog post about 2025 in

1:53:04

review. I said, I have mixed emotions about recommending people read Kevin's work because I've kind of had him all to myself, me and a handful of close friends. And it's almost like a competitive advantage.

1:53:17

Mm-hmm.

1:53:18

I almost don't want you reading it because I know you'll read it and be inspired by these ideas that he has. And he's just, he's that guy who has time and time and time and time again nailed it. He's called it. And I don't doubt that he's calling it now again in his latest post.

1:53:37

So do go read Kevin Hazard's Substack as well. H-A-Z-Z-A-R-D. Yeah, I call him the Duke. Yeah, the Duke's a hazard. Oh, yeah. That's my nickname for him. And he's just, in addition to being crazy smart, he's just a great guy. But we're seeing that with AI. We're going to see this happen.

1:53:56

And there's a group of people that either haven't had the experience that I've had. Maybe they've tried and it didn't work out for them and their personality is to, you know, it got to their threshold of frustration. Like, I'm just going to give up on it. I was there from November of 2022 to March of 25.

1:54:15

I was there.

1:54:16

I was there, too. Co-pilot day.

1:54:20

Until it worked. And when it worked, man did it. And part of it, and I'm sure this happened to you, too, Dan, is we were evolving very slowly. We were learning the tips and the tricks. Yeah, it was a new thing for us, right?

1:54:34

Yeah.

1:54:35

Right. And it was also becoming less the barrier was dropping on the technology side as well. So we merged. For me, it was March 25. And then we took off with it. I expect that merge to accelerate. I don't expect an order of magnitude. I expect it to jump in three orders of magnitude. Right.

1:54:54

I expect it to go metric.

1:54:56

Right.

1:54:56

You know, like from Killa to Meg, right? It's going to be that kind of jump this year is what my heart tells me. So many people are going to get into it and they're going to solve so many problems so fast. Yeah,

1:55:10

I'm looking forward to like the infrastructure, like not only code, like clearly the code is there, but like that integration of like not only can Claude, you know, just make whatever widget I could possibly dream of, but like the... Actually, the infrastructure too, right? This whole other, right? So it can just be done. So I don't,

1:55:31

that person doesn't have to set up an AC2 instance and install a web server, you know, like, because that's a big part of it too, right?

1:55:39

Absolutely. And imagine when it breaks out of software and it's already doing this, right? Imagine being able to either print yourself circuitry, maybe even a CPU or design the CPU, have Cloud Code work with you or some AI work with you to design a CPU and send it off.

1:56:06

One of the projects me and Stephen did is we restored an old Jeep Comanche that I had parked like for 16 years. And he's found a service called, I think it's called Send, Cut, Send. And there were parts on that Jeep that had, like floorboard pieces that had rusted out and were gone.

1:56:26

And this is a 1990 Comanche. You're not going to find those parts. You need to send me a picture of those.

1:56:33

I have a Jeep Gladiator, so I like Jeeps.

1:56:37

Oh, nice. We rebuilt that Comanche. He did most of the work. I was moral support and a great tool handler and light holder. That was my role. But he did it. It's long and a great story that we documented. It took him 16 months to get it running. But it was running, and there's stuff that keeps going.

1:56:57

He's kind of in the beta phase right now. He's putting a transmission in it, and he's realizing he's going to have to rebuild the motor so he can use the transmission to its fullest extent. Send, cut, send. He would draw in one of the free CAD programs that are available now. He would draw the part...

1:57:16

Send him the specs. They charge him like 18 bucks to send him back a big custom made complex part with all sorts of things in it. I mean, most of the things he bought were 10 bucks or so. And so he was he was doing his back.

1:57:31

He was working as an electrician back then before he went into the to the gig with the with the startup. Imagine being able to do that with a CPU and a GPU or being able to send off a spec that is the equivalent of the successor.

1:57:49

I can't remember the thing NVIDIA just put out, but it's the successor to the Blackwell Show. Just you design it your way. You interact with the AI, converse on your phone with the AI, do that. And then after the design is shipped off and you're going to pay 20 bucks and get that chip back.

1:58:12

And it's going to plug right into a socket and run all of the programs on all of the platforms, all of the OSs that are available at the same time. It'll do all of those. And it'll have a quantum processing unit built right into it, not just a neural, but quantum.

1:58:29

And as soon as you tell it to go ahead and send that email, make that order and take the 20 bucks out of your account, then you start talking to whatever AI it is, about the operating system and how you want it to work on that chip. And it remembers the chip design.

1:58:44

So it's going to start thinking about, all right, how do I leverage the quantum processing and the neural processing and the GPU and all of the CPUs, the logical processors that are built on here? Maybe even by then, a collection, an array, if you will, of GPUs and NPUs and maybe even QPUs, right, the quantum processors.

1:59:03

All of that is on a chip you talked to the AI about and it arrives in the mail a week later. You plug it in and you begin interacting with it. Maybe it needs a new motherboard, another 20 bucks that you do that. These costs plummeting are part of the equation.

1:59:23

And if I have a hard time in my mind seeing how we go from where we are in January of 2026 to that world, where the economics are such that it enables human flourishing at that scale. I hear people smarter than me saying that they believe that's possible, that we can get to there.

1:59:50

I don't know if they see the path in between. I don't. I'm beginning to believe that they're right, that Elon and others who are talking about this future where Kevin, where the cost of software development goes to zero.

2:00:08

It's almost like it's a cultural shift too, right? Because there's so many people who... They don't even realize what's possible or, you know, it's somewhat of a cultural shift.

2:00:20

We're going to live through this. I mean, being 62, I watched Neil Armstrong step foot on the moon on a black and white TV in Green Bay, Virginia, which has like population 90 or something. My mom still lives there. We're going to go from like Star Trek.

2:00:38

land, you know, where the first Star Trek series, we're living beyond some of that now. You know what I mean? And having lived through that and participated in it as a consumer, you know, and a little bit as a contributor of it, it's very, very small fraction of a fraction. But Being into what's next.

2:01:03

I can't tell you, the joy I get out of watching this code run and watching it fix my 10 years of code, it would be very easy, I think, to look at that and get angry about all the work that I put into this and stuff like that. Not the way my brain works.

2:01:21

It's very much a sunk cost engine, my brain. Everything that I already know is worthless to me. Everything that I don't know It's worth a million bucks. I'm a little like Rain Man in that scene where he gets asked about the cost of a candy bar and the cost of a new car.

2:01:39

And his answer to both questions is about a hundred bucks. Right. I'm kind of there with that. And Dave Plummer wrote a book about the millionaire autistic, which is worth a read. Dave wrote task manager. If you don't know who Dave Plummer is. So you've used his work. Yeah. I used his work earlier today.

2:02:01

He's got a YouTube channel. He's an interesting character. It's a good read. And he talks about, you know, those sorts of things, too, in his book about effectively, I don't want to say weaponizing autism, but he talks about ADHD being on the part of the autism spectrum as well and a number of things.

2:02:24

We just know today that we didn't know. All of that's going to kind of flow into this culture shift, as you said, Dan. I think you're spot on with that. And if I have concerns, and I do, my concerns today are not about Not so much about what it looks like when we get there.

2:02:43

I do have some concerns about that, too. But I'm more concerned, much more concerned about the transition from here to there. I think about that chaos I saw when the DBAs were getting laid off. I worry about, is that what we're seeing the beginnings of?

2:03:01

Hundreds of thousands of jobs were lost in 2025, and most of it started in the summer. And, you know, and it accelerated through the end of that. I don't think that's going to stop. And a lot of software developers and people in support of software development lost their jobs. It was blamed on AI. There's more there.

2:03:21

Yeah, for sure. Honest. I've been around long enough and I've worked. I've been a worker and I've. I was a manager for Unisys for two and a half years, managed a large team there. If you can't cut 10% of your people, you're just not trying. And it's not because they're bad people. It's because...

2:03:43

if you do you kind of look at what's going on with the work that's being produced and where there's duplication of effort and stuff like that it's not bad it's just that it's it's more like musical chairs right there's two chairs and three people

2:03:59

somebody's not gonna get a seat when it's when the tune stops and you can do that at about that level at about 10 and i think a lot of what happened was that some of it I heard rumors that there were internal corporate surveys at big companies.

2:04:14

And one of the questions was, are you going to use AI? And some of it was people saying, I'm never going to use AI. And they got fired for that. That was a rumor. I don't know how true that is. I'm not getting into AI because I'm afraid. I'm doing AI because I see it helping me.

2:04:35

And again, it's still a lot of people in January, 2026 talking about hallucinations and talking about how you can't trust this stuff. They're not wrong about either one of those things, but the perception to reality ratio is skewing and it's getting less and less.

2:04:54

That shift's not turning around like the AI shift's not. I see this a lot from some people, even some of my friends. It's about a Rust developer. I know it lives a couple miles away. It's like, dude, man, this ship has sailed. You cannot turn this ship around.

2:05:09

It really has.

2:05:10

You can watch it sail off in front of the sunset without you, but I would suggest you get on because it ain't coming back.

2:05:19

The last milestone for me happened around the first of November, that first week of November. I saw it then. When I started seeing one-shots happening about half the time, when I saw all of the things I asked AI to do, it was doing. And with that, honest, it was a paradigm shift for me.

2:05:36

I had to start thinking bigger. I was like, wait a minute. That's where I came up with that analogy I just shared with you, right? Imagine AI. Designing the chip, designing the motherboard, designing the device, and then designing the system that, you know, the OS that runs it, the software that runs it.

2:05:52

And then populating it with a suite of functional, whatever they're called at that time. I'm hesitant to use the word applications, but that's where that analogy comes from. My thinking had to jump. And I think we're going to see something like that. I'm not any good at predicting the future. Who knows?

2:06:12

My knack is seeing something and going, that's a good idea. That's a gift. That and data engineering.

2:06:20

Yeah, we'll go on the AI ride just like we went on the SQL Server ride back in the day. Just the same server. That's it, Dan. Just a different ride, I guess.

2:06:29

Right.

2:06:29

I appreciate you joining me today for this podcast. If people want to find out more about you and... I'll leave some links in to everywhere this ends up. I'll leave links to your website, Substack, whatever. Do you have any particular place you want people to reach out to you on LinkedIn, website, sub stack,

2:06:48

whatever you can, you can definitely start at engineer of data, all one word, all lowercase, engineer of data.substack.com.

2:06:58

Okay.

2:06:59

That's where my energy is being focused these days. Getting a lot of response, a lot of community building happening there for me. Don't know why it's, but it's just working. I've got over 5,000 free subscribers, a handful of paid. I'm seeing in the neck of the, under 1% are paid right now,

2:07:23

but I didn't really start the push to add value to paying for the subscription. I really didn't start that until last month. And no surprise, I think it was ChatGPT that helped me most with the ideas that are producing. I doubled my paid subscribers, which it went from single digits to the teens.

2:07:43

OK, so you got to put that in perspective. But, you know, an hour, hour and a half with ChatGPT, what should I do? And then it took me a couple of weeks to build a playbook out there. And that's a paid subscriber benefit now. It's how I build Hyper-V VM.

2:08:02

I have a hard time. I don't know. It's this pull between I just create stuff and put it out there because I enjoy it. I enjoy talking to people like you, learning myself, just sharing it versus like I'm not a good salesman. I'm an engineer.

2:08:17

I'm not a good salesman either. But you're right in that if you don't enjoy it, that kind of taxes anything you're going to put your hand to. And it's a horrible text. And I'm seeing that. One of the reasons I'm enjoying vibe coding as much as I am and I've gotten into it

2:08:37

as much as I am is because it's just so much fun. So, but Dan, this has been a big honor for me. If you go to the engineer of Substack and you sign up for a free subscription, there's links that I put out. I write more free stuff, way more free stuff than I do anything that you,

2:08:53

you know, is behind the paywall. But there's links to all of the other sites that just come up in the natural flow. I've got a few teams. Enterprise Data and Analytics is my consulting company. I've got a few teams and venues going there. Three teams right now that are out there actively doing consulting work.

2:09:12

And as of June, I was able to stop billing consulting hours myself. First time ever. I've had both time and money. And that's when I really started, you know, cranking the gauge over on AI because I had I didn't have to worry about billing hours to to pay the bills. And I hope to continue and expand that.

2:09:37

It's kind of cool because all day long I play right now. That's awesome.

2:09:41

I'll put links to all that in the description of whatever you're listening or watching.

2:09:46

Appreciate that, Dan, so much. This was an awesome conversation.

2:09:50

I feel like I talked too much.

2:09:52

Let's do it again. Let's do it again in a few months. I'll have learned some more about AI.

2:09:57

We'll see if we were right or wrong about things, right? That would be awesome. Let's do it.

[![Data Engineering Central](https://substackcdn.com/image/fetch/$s_!9izE!,w_96,h_96,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd6a29bf1-b54f-4014-b5d7-6d7274f707df_2184x978.png)](https://dataengineeringcentral.substack.com/)

Data Engineering Central Podcast

Long Live the Data Engineer. No holds barred. Talking about Data Engineering news, topics, and general mayhem.

Long Live the Data Engineer. No holds barred. Talking about Data Engineering news, topics, and general mayhem.

Listen on

Substack App

Apple Podcasts

Spotify

RSS Feed

Email mobile setup link

Appears in episode

[

![Daniel Beach's avatar](https://substackcdn.com/image/fetch/$s_!UXdB!,w_32,h_32,c_fill,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F81caaeec-9053-487c-a59c-ba5f8e4644ad_256x256.jpeg)

](https://substack.com/@dataengineeringcentral?utm_source=author-byline-face-podcast)

Daniel Beach

Recent Episodes

![](https://substackcdn.com/image/fetch/$s_!heH7!,w_150,h_150,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_center/https%3A%2F%2Fsubstack-video.s3.amazonaws.com%2Fvideo_upload%2Fpost%2F184371353%2F9d463190-e8ee-43ad-8ece-ddd132eab712%2Ftranscoded-1768256701.png)

[From DBA to Data Everything](https://dataengineeringcentral.substack.com/p/from-dba-to-data-everything)

Jan 14 • [Daniel Beach](https://substack.com/@dataengineeringcentral)

![](https://substackcdn.com/image/fetch/$s_!joSf!,w_150,h_150,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_center/https%3A%2F%2Fsubstack-video.s3.amazonaws.com%2Fvideo_upload%2Fpost%2F182889224%2Fcaf957f6-aba5-4464-898e-66aa706a6e88%2Ftranscoded-1767034885.png)

[Data Engineering Central Podcast - 10](https://dataengineeringcentral.substack.com/p/data-engineering-central-podcast-f35)

Jan 2 • [Daniel Beach](https://substack.com/@dataengineeringcentral)

![](https://substackcdn.com/image/fetch/$s_!HwRO!,w_150,h_150,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_center/https%3A%2F%2Fsubstack-video.s3.amazonaws.com%2Fvideo_upload%2Fpost%2F181261013%2F12963e79-49f7-462e-a1ce-cf275097b8d7%2Ftranscoded-00001.png)

[Scott Haines on the Future of Data Engineering](https://dataengineeringcentral.substack.com/p/scott-haines-on-the-future-of-data)

Dec 17, 2025 • [Daniel Beach](https://substack.com/@dataengineeringcentral)

![](https://substackcdn.com/image/fetch/$s_!795b!,w_150,h_150,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_center/https%3A%2F%2Fsubstack-video.s3.amazonaws.com%2Fvideo_upload%2Fpost%2F178818802%2F7a71cf72-e132-437b-8a50-10d8f4a4228c%2Ftranscoded-1763060191.png)

[Data Engineering Central Podcast - 09](https://dataengineeringcentral.substack.com/p/data-engineering-central-podcast-db1)

Nov 13, 2025 • [Daniel Beach](https://substack.com/@dataengineeringcentral)

![](https://substackcdn.com/image/fetch/$s_!bjXa!,w_150,h_150,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_center/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe18333e1-c1b1-4dc0-936a-e1b0c0088177_1024x1024.png)

[Data Engineering Central Podcast - Episode 8](https://dataengineeringcentral.substack.com/p/data-engineering-central-podcast-410)

Jul 10, 2025 • [Daniel Beach](https://substack.com/@dataengineeringcentral)

![](https://substackcdn.com/image/fetch/$s_!DE3i!,w_150,h_150,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_center/https%3A%2F%2Fsubstack-video.s3.amazonaws.com%2Fvideo_upload%2Fpost%2F164251337%2F7e99db8e-d37d-4d74-9023-d25e475073f0%2Ftranscoded-00001.png)

[Apache Iceberg Rant.](https://dataengineeringcentral.substack.com/p/apache-iceberg-rant)

May 26, 2025 • [Daniel Beach](https://substack.com/@dataengineeringcentral)

![](https://substackcdn.com/image/fetch/$s_!t2-r!,w_150,h_150,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_center/https%3A%2F%2Fsubstack-video.s3.amazonaws.com%2Fvideo_upload%2Fpost%2F160452902%2Fe4030c91-2c6a-4bd0-80c6-3df54046dcaa%2Ftranscoded-1743628061.png)

[Data Engineering Central Podcast - 07](https://dataengineeringcentral.substack.com/p/data-engineering-central-podcast-150)

Apr 2, 2025 • [Daniel Beach](https://substack.com/@dataengineeringcentral)

© 2026 dataengineeringdude · [Privacy](https://substack.com/privacy) ∙ [Terms](https://substack.com/tos) ∙ [Collection notice](https://substack.com/ccpa#personal-data-collected)

[Start your Substack](https://your.substack.com/publish)[Get the app](https://substack.com/app/app-store-redirect?utm_campaign=app-marketing&utm_content=web-footer-button)

[Substack](https://substack.com/) is the home for great culture