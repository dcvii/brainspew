---
title: "you need to use Herdr RIGHT NOW!!"
source: "https://www.youtube.com/watch?v=9_FzA-J9S2E"
author:
  - "[[NetworkChuck]]"
published: 2026-11-06
created: 2026-11-06
description: "Could AI be your next networking assistant? Check out how HPE Networking uses AI to identify issues and optimize performance: https://ntck.co/aiopsHerdr is tmux, but built for AI. I use it every si"
tags:
  - "brainspew"
---
![](https://www.youtube.com/watch?v=9_FzA-J9S2E)

Could AI be your next networking assistant? Check out how HPE Networking uses AI to identify issues and optimize performance: https://ntck.co/aiops  
  
  
Herdr is tmux, but built for AI. I use it every single day, and it pulled me back to the terminal right when I was about to go full GUI. In this video you'll learn how to install Herdr on Mac, Linux and Windows, how panes, tabs and workspaces fit together, how to get notified when an agent finishes, gets blocked or has a question, how to connect remote Herdr sessions over SSH, and how to let your AI agents control Herdr and talk to each other. My Claude Code launched Codex, Gemini and Grok, and they all talked back.  
  
  
Join the NetworkChuck Academy!: https://ntck.co/NCAcademy  
  
  
RESOURCES / LINKS:  
🌐 Herdr: https://herdr.dev  
💻 Herdr on GitHub: https://github.com/herdrdev/herdr  
📺 you need to learn tmux RIGHT NOW!!: https://www.youtube.com/watch?v=nTqu6w2wc68  
🛠️ Claude Code: https://claude.com/claude-code  
🎙️ Wispr Flow (how I talk to my agents): https://wisprflow.ai  
🌐 Omarchy: https://omarchy.org  
📺 Set up your own AI agent (Hermes): https://www.youtube.com/watch?v=QQEgIo4Juxg  
  
  
TIMESTAMPS:  
0:00 - Herdr: tmux built for AI agents  
0:52 - How AI helps network engineers with HPE Networking (Sponsor)  
2:28 - How to install Herdr on Mac, Linux and Windows  
3:38 - Detach and come back: your sessions keep running  
4:14 - Herdr panes: split, rename, move and resize  
5:18 - Herdr tabs: keeping your panes organized  
5:52 - Herdr workspaces: organizing tabs and panes  
6:53 - The agents panel: every AI agent in one place  
7:20 - Sound and toast notifications when an agent finishes  
8:57 - Filter your agents by done, blocked, working or idle  
10:20 - Remote Herdr: add another machine over SSH  
11:53 - Your AI agents can control Herdr themselves  
12:39 - AI agents talking to each other: Claude Code, Codex, Gemini and Grok  
14:37 - Git worktrees with multiple AI agents  
15:07 - One agent on one machine talks to an agent on another  
16:09 - Stop the server and every session resumes  
16:42 - Why Herdr brought me back to the terminal  
17:23 - A prayer for you  
  
  
\*\*Sponsored by HPE Networking  
  
  
SUPPORT NETWORKCHUCK:  
☕☕ COFFEE and MERCH: https://ntck.co/coffee  
  
READY TO LEARN??  
🔥🔥Join the NetworkChuck Academy!: https://ntck.co/NCAcademy  
📚 CCNA Course: https://ntck.co/ccna  
  
  
FOLLOW ME EVERYWHERE:  
Instagram: https://www.instagram.com/networkchuck/  
X/Twitter: https://x.com/networkchuck  
Facebook: https://www.facebook.com/NetworkChuck/  
Join the Discord server: https://ntck.co/discord  
  
  
Some links in this description are affiliate links. If you buy through them, I may earn a small commission at no extra cost to you. #sponsored  
  
  
#herdr #tmux #aiagents

## Transcript

### Herdr: tmux built for AI agents

**0:00** · You need to start using Herder right now. It's like T-Max, but it's built for AI. I use this every single stinking day. Check this out. Now, just like T-Mox, we can launch it on one computer, launch some \[music\] PES, launch some AI agents, and then get the junk out of there and access it from my Omachi laptop like I never left. It's also a mouse first terminal. But where it gets crazy is how my AI agents \[music\] use her when they're done, blocked, or have a question. They let you know, notifications, icons. This sucker is AI native. Or you can quickly filter \[music\] the sessions based on their status. But this is my favorite thing right here. Your agents can drive her.

**0:31** · They can control it. Opening new panes and windows by themselves. And this one, they can talk to each other. My claw code just launched Codeex Gemini and Groth and he's talking to them and they're talking back. There is so much more it can do. \[music\] Get your copy ready. This is where you're going to be talking to your AI from now on. Let's go. Now, you will be a herder expert by the end of this video, a full convert.

### How AI helps network engineers with HPE Networking (Sponsor)

**0:52** · But before we do that, I have an urgent message for network engineers. If you're not a network engineer, move on. You can't be here. Go. Okay, network engineers, listen up. You know how I just showed you in her how an AI agent can just tap you on the shoulder and let you know something's wrong or done? That is what network engineers \[music\] need right now. This video is sponsored by HPE Networking and they asked me to do a kind of a PSA \[music\] for you, a word of encouragement. So, buckle up. Get the copy ready. This is the message. Don't be afraid of AI. You don't need to be.

**1:19** · It's not going to \[music\] replace you.

**1:21** · It's going to make you better. Answer this. How many of you right now are drowning in extra time? None of you, right? All your time right now goes to troubleshooting and putting out fires.

**1:31** · That that right there is where AI is going to help you. Instead of spending hours digging through logs, AI can dig through them for you and help you find the root cause of an outage like that.

**1:40** · Couldn't snap for a second. And I know you love those 3:00 a.m. troubleshooting calls, right? Everything's on fire. You can't even see straight. You don't have any coffee. \[music\] That's where AI really comes in handy.

**1:49** · It'll point you in the right direction while you are still making the call or while you're making coffee, either way.

**1:55** · And it's going to help you automate that boring work, too, \[music\] like documentation and diagrams, things I didn't do before anyway. Now, at least it's getting \[music\] done. And that's what HPE networking is actually doing.

**2:04** · They use AI to help identify issues and speed up root cause analysis and improve network performance so you spend less time on the stuff that stresses you out \[music\] and having more time to build and have fun, getting back to the original reason you got into networking.

**2:17** · So, think about it. AI could be that networking assistant that you need right now. To see how HPE Networking does it, I got a link in the description below.

**2:24** · Click on it, learn \[music\] more. Show them some love for sponsoring this video and making something like this possible.

### How to install Herdr on Mac, Linux and Windows

**2:28** · Now, back to Herder.

**2:32** · Let's start with getting it installed.

**2:34** · Good news, it works everywhere. So, head on over to herder.dev. And right here, you'll see the command to install for Mac OS and Linux. For Windows, I'm actually curious about this. You'll run Oh, this PowerShell command. I do want to try that cuz I'm on a Windows machine right now.

**2:47** · That totally worked. And then on Mac and Linux, I'll just paste that command. And that was quick. Now, all you really have to do is just type in herder to get started. Let's try her. Boom. Now, I love how simple the intro is. And again, this is a mouse first terminal. So, if you're not like a keyboard ccentric person, it's okay. You don't have to be scared. Look, you can even click stuff here, but you should be keyboardcentric.

**3:07** · And I'm going to show you some of the fun things like controlB will get you into prefix mode for a bunch of fun commands. So, we'll hit continue with the mouse is so weird. And the first thing it wants you to do is install some AI integrations because it's an AI first terminal. Yeah, I found Claude and I found Hermes. Let's install those. Hit enter. Done. That was quick. Notice we can use our directional arrows to kind of jump around or use our mouse to jump around. If you want some toast, you can turn on some toast. Sound indicators, themes. Ooh, theme. Let's go. Groove Box. Oh, yeah. And now we're in. And this is the best thing ever. Like, I'm not kidding. I use it every day. I already said that, but I had to say it again.

### Detach and come back: your sessions keep running

**3:38** · Now, this land, this world that we just created here, it's always running. Like, watch this. Do do this with me. We're going to in this terminal right here, type in ping 1.1.1.1 or whatever. Let that keep going. Now, we're going to do our prefix. Crl +B and then hit Q to detach. Where'd it go?

**3:52** · It's gone. Feel like I'm doing a Bluey episode. But now if we type in Herder again.

**3:58** · Hey, it's like we never left. It's still going. Herder is actually a server running in the background. And all the terminals and windows and PES and AI agents that we start launching inside of this. I'm about to show you that they just live there. They don't die. And even if the server goes down, like if you close your laptop or your computer reboots, they resurrect. I'll show you that here in a moment. But first, we got to explore. Let's get our bearings. Now, as we explore, keep in mind you can use your mouse for everything, but I'm showing you keyboard shortcuts because they're more fun. Now, first, right now, where we're at, this is a window or pane where we're pinging right now. It's a pain. Actually, let's stop our ping.

### Herdr panes: split, rename, move and resize

**4:25** · Ctrl + C, and let's launch Hermes, cuz why not? Hermes. Boom. And something fun just happened. You see that? An agent just popped up. We'll get to that here in a moment. Now, in this pane, we can do Ctrl +B, our prefix, and type in V to split it vertically. And suddenly, we have a new pane. We can also hit Ctrl +B and then the minus symbol to split horizontally. And notice it split that new paint horizontally. We can rename these panes by hitting controlB shift P.

**4:50** · Call this one Bob. Notice how it changed the name right here. Now we can move around with our mouse. Keep in mind mouse centric. Or we can use our keyboard. And I can use Vim controls like K to go up or H to go left or L to go right. We can also resize them by hitting B, R, H to go left, L to go right, J to go down, K to go up. We can also open just a ton more. And now that's way too many. It's just fun though. Try it. You can close them by hitting controlB XRB X.RLB X. Now, this was all just in one tab. A tab helps us keep our PES and stuff organized.

### Herdr tabs: keeping your panes organized

**5:21** · Let's create another tab. Crl +B C. We can name it, I don't know, clot. And we have a new tab. We can rename this tab. Crl + B shift T. We can get back to our previous tab by hitting BP to go back.

**5:34** · Crl + B N to go next orb and hit the number of the tab. One. Crl + B 2. B 1.

**5:41** · Now, again, I want to point out that all this is mousable. Is that a word? I don't know. Which is just so sick. And while I'm jumping around, I'll launch a few more agents so you can see them pop up. See, there they go. Again, we'll touch on that here in a moment. Now, let's go one more level up. We saw PES and we saw tabs. But now over here, we've got our workspaces, which organize our tabs and our panes. And right now, the name is defaulted to our home directory, the tilda home sweet home.

### Herdr workspaces: organizing tabs and panes

**6:03** · Let's rename that. ControlB shift W.

**6:07** · We'll name it MySpace. Let's create another space. Crl +B, Shiftn, new space. Control-b shift W to rename it.

**6:15** · And now we have a whole new world of tabs and panes that we can just create.

**6:19** · I'll add a few more spaces. I'm not sure why I went social media on this. It just happened. We can quickly jump between spaces by hitting BW. Notice my directional arrows let me jump around here. I can close an entire space by doing controlB shift D. Sure about that?

**6:34** · Sure. And this is by far my favorite way to navigate. Control B G for go to.

**6:39** · \[laughter\] They're all right here. Directional arrows or HjKL or just JK. And you can see what's up. And there's so much happening here. And we haven't even started talking about agents yet. Let's go.

### The agents panel: every AI agent in one place

**6:53** · Now, you may have noticed when we launched our agents and random PES, they started showing up right here in this little agents tab. Boop. Not sure why I just booped you. Notice we can click around here. Boom. Boom. Boom. And go to each agent's pane. And notice they are also labeled by workspace. So right now all our agents are in MySpace. Let's put some in Zenga. So let's go to Zenga.

**7:12** · I'll start Claude right here. And boom.

**7:14** · Notice there he is. Claude showed up in Zenga. But watch this. That's not even the fun part. We're going to enable notifications. And this is really going to show you the power of how the agents interact with Herder. And this is their house. They live here. So first, let's make sure we have it turned on. Crl +B, our prefix, and hit S for settings.

### Sound and toast notifications when an agent finishes

**7:31** · We're going to go over to sound. Make sure we have sound on. Just switch that on. Hit enter. Go to toast. Love toast.

**7:37** · We'll see. We want our notification pop-ups to h happen inside of Herder.

**7:41** · Hit enter. Boom. And that's it. Hit escape to close. Now we can try some stuff right here in Zangaland. I'll tell Claude, "Yo, dude, tell me a scary story in two paragraphs about Network Chuck."

**7:51** · And by the way, I'm using Whisper Flow right now. My favorite thing. I want to hit enter quickly. Go away so we can get notifications. And we'll wait. Ah, here it is. And I think maybe you heard it.

**8:02** · You should have heard it. Let's go over there and check it out. Control B W go go up one space. There it is. We'll try it in Hermes over here. Hey, what is the hardest math problem ever? Boom. I love how it just works. Notifications are cool, but that's not the coolest thing.

**8:15** · Watch this. I want to set up some uh chats here. I want you to ask me a series of questions. Uh math questions.

**8:21** · Prepare them right now. I'm not going to say it yet. Go over here to Claude and say, "Tell me a scary story, but you can only use three words, the same words consistently, and make it three paragraphs. produce an asky art image of um network Chuck and ask me a question for feedback to see if I if I like it.

**8:37** · I'm going to go start this one, this one, this one. Now watch this. This is going to be so cool. I'm going to let them finish. Claud needs attention. Love that. My space finished. Hermes finished. And notice how the colors are actually changing up here too. Okay, you ready for my favorite thing? So we'll do CtrlB, our prefix, and then G for go to.

**8:55** · This is the best way to view your stuff.

### Filter your agents by done, blocked, working or idle

**8:57** · We're about to unlock this right here.

**8:59** · Filters. I'm gonna hit D for done. And you can see which agents are done. Looks like Robert and Terry are done. And we can jump there real quick. Let's go check on Robert. Totally scary story.

**9:10** · Three words. That's not bad. And also kind of scary. Let's hit controlB again.

**9:14** · G. Now instead of D, we're going to hit B. B is for blocked or any agent that's waiting on you. It has some questions for you. And Zena has some questions.

**9:22** · Let's go check it out. That's a little cursed. Let's make it spooky. How sick is that though? Ooh, it made it spooky.

**9:29** · make four more versions. Now, if I hit controlB G once more and then filter off of W just hitting W, I can see which agents are working. Notice the status right here and they're done. It made a possessed one. That's scary. Don't do that. Did it incorporate that story from earlier? The behind you. Claude, you're being creepy again. B G once more. Our other filters are I for idle. So, agent's just kind of chilling. Then A for all. This is by far my favorite thing. I use it all the stinking time.

**9:58** · And I know you're sold right now. Like that was enough to make me switch, but that's not even the coolest stuff. We have two amazing things coming up. The last one I just can't even. Did I just say can't even? I need some more coffee.

**10:09** · It's a bit too early right now. You and I. Let's sip it right now together.

**10:14** · Okay, next section. Let's go.

### Remote Herdr: add another machine over SSH

**10:20** · Now, this is actually a fairly new feature. I just started using this and it's amazing. It's remote herder. So, right now we're on Terry. This is our current herder session, but my main computer is actually a Mac Studio and it's also running Herder. I can add this Herder on my Mac as a remote Herder session on Terry. And it's so stinking easy. Watch this. First, the other machine has to already have Herder and it has to be accessible via SSH. Let's do it real quick. It's so easy. Herder machine list. I've got no machines now.

**10:47** · I can do her machine add. I'll label it with D-Label. Call it Big Mac. And then just like SSH, my username plus the machine's IP address. So networkchuck at 10.77.14.204 and add my herder session on that Mac just showed up right here. Notice Terry now has a local label. And then over here we have big Mac with all his existing herder sessions. And look at that. I'm already getting notifications from that remote herder. Everything just works. BG G. It's all there. I can switch right to it.

**11:18** · Are you starting to see how powerful this tool is? It's crazy. Oh, by the way, what I'm showing you, there's a lot to remember. So, if you hit controlB, you can hit question mark and see all the prefixes and keybinds. You can press forward slash to search like close, workspace, tab, whatever. You can learn it all right there. Oh, also one thing I forgot to show you, bonus. So, of course, we have the filter options, DFW, whatever, blocked. But you can also do forward slash and search. So, I can search for baptize. And I had a session where I was talking about baptism. And I can jump right there.

**11:48** · And I think it searches like the session name and the content and everything. But now for the best feature of all time, watching the agents control herder and also talk to each other. It's so good it doesn't make any sense.

### Your AI agents can control Herdr themselves

**12:03** · Okay, so first your agent can control her. What do I mean? Watch this. Start a new session and I'll say, "Hey, Morpheus." By the way, that's my AI's name. I'm showing off Herder right now on the Herder video. Real quick, I want you to open up five pains with Herder right now. So, what's happening here is that Herder has a skill which allows it to interact with its API and I believe it has a CLI as well. There's all kinds of crazy stuff going on. Essentially, your agents can interact and boom, it just did it like right in front of us.

**12:30** · How sick is that? Okay, now close them.

**12:33** · Isn't that awesome? So, that's a skill you can just give to any one of your agents. They'll know. They'll know where they are. But it's not just that. Herder can be used for agents to talk to each other. Watch this. I love this so much.

### AI agents talking to each other: Claude Code, Codex, Gemini and Grok

**12:43** · Morpheus, I want to show off the power of Herder. So, here's what I want you to do. I want you to open up four panes right where we are. One with codeex, one with grock, one with anti-gravity, and one with with another claw session. Make them look really nice and even. And I want to do a coding session together.

**13:00** · What I want you to have them do is code together an asky art scene. Each a different scene from Harry Potter and the Prisoner of Aszaban. And I want them to play that here in the terminal. Um, make it a threeminute job. Like they have to move quickly. Go for it. You ready for this? go.

**13:18** · And notice a few of these have dialogues and they he just took care of it.

**13:25** · Morpheus was able to see their dialogue and answer it. They're all running now.

**13:28** · Look at them go. Now, what's amazing about this is that there's hooks built in. So, this main claude code session right here has hooks ready to go waiting for their answers. And as soon as any one of these suckers finishes or has a question or anything, they will talk back to him. They can talk back to each other. They're all situationally aware of what's happening. It is amazing. Now, it looks like Claude, Codex, Anti-gravity, and Gemini all finished.

**13:51** · Grock is always slow on this. Not dumb, but slow. While they're making that, I do want to show you a basic example of how they talk to each other. So, we'll just set up a new session here. Um, I want you to set up a quick codeex session to show off her um in a tab or not a tab, a pane right next to you, and um simply ask him a few questions and have him answer back to you. I want y'all to have a combo back and forth and watching them talk. Look at this.

**14:15** · Codex answered pulling its reply from the pain now. Oh, notice. Look what he did. I didn't even tell him to do this.

**14:21** · He renamed it. Okay, Grock is taking too long again. You got to hurry this guy up. There they \[laughter\] go. I love it.

**14:28** · He did the Marauders map down there.

**14:30** · That's sick. Oh, that's so fun. Expect a patron. I'm nerding out right now.

**14:34** · Sorry. \[snorts\] Not sorry. Now, her can also be aware of work trees. Check this out. Back over here, I'll say, "Hey, Morpheus, I want to show off Herder's ability to create work trees." So, I want you to create just like a dumb sample coding project with Gemini, Claude, and Codeex using work trees. Uh, make that happen right now with her, please go. And there it goes. But notice right here, work trees created. And we get a nice visual for what's happening.

### Git worktrees with multiple AI agents

**14:59** · If I hit controlB and G, I can see them doing their thing down here. All three finished. He's committing the branch.

**15:05** · And I think it was some joke thing it made. One more thing I want to show you with how herder or agents can control her. Um, if I go back up to my local machine, so on Terry, I'll launch Hermes. I'm going to teach him the Herder skill. Hey, uh, set up the Herder skill for you. Right now, you're in a Herder pane inside her. Install the Herder skill, please.

### One agent on one machine talks to an agent on another

**15:24** · Done. Now, I can't believe this is possible, but watch this. I'm going ask Terry to do this. Hey Terry, I want you to use Herder to talk to Morpheus and inside the toilet workspace, I want you to ask him about the toilet video to get a status update. Now, what this should do is Terry from his local herder situation is going to reach out to the remote herder situation over here on my Mac and talk in the toilet session to Morpheus. Ready, set, go. There it goes.

**15:50** · He's talking to him. Let's go look in there. Oh, he's answering. Hey, Terry.

**15:53** · Whatever. Whatever. Blah blah blah. And he's waiting on his answer. Oh, Morpheus just finished. He got his answer. And that's that. So what just happened there is crazy. One Herder situation talking to another one agent on one machine talking to another agent on another machine. And it was kind of seamless.

**16:08** · And finally, one last thing I want to show you is let's get out of her. So we'll do control Q to quit. Oh, I'm going to stop the server. So Herder server stop. And that should stop everything. And then I'll just type in her to get back in there. And watch what happens. It's resuming everything.

### Stop the server and every session resumes

**16:24** · Because when you're chatting with your AI agents, it's just text. So, it immediately resumed every single one of my sessions like I never left. So, laptop closes, your PC reboots or whatever. You're still there. You're still talking. You're still chatting.

**16:36** · Isn't that amazing?

**16:41** · Okay, so her time to land this plane.

### Why Herdr brought me back to the terminal

**16:44** · What do you think? I haven't even thought about T-Max until this video when I had to compare it. It's not even comparison, right? I have never looked back. Herder almost said T-Mox. Herder is amazing. What do you think? Are you going to try and use it? Comment below.

**16:57** · Again, I almost went full gooey. Herder brought me back to the terminal. And I'm happy. I legit have been using this every single day since I found it like 3 months ago. And I love love being able to jump in and just start my AI stuff or resume it from any device I have, including I found an app that does this well on my phone. There's probably another video, though. Anyways, that's all I got. I'll catch you guys next time. Hey, you made it to the end of my video. At the end of my videos, I like to pray for you, my audience. And actually, I want to address something that I saw yesterday.

### A prayer for you

**17:29** · It was this tweet or expost about hackers being very depressed about potentially their work going away.

**17:43** · All the skills they've built up over the years are now becoming, I'm just saying this is what they're thinking, are becoming useless and they're having like this crisis.

**17:52** · I think many people in it are collectively starting to feel this or at least have already felt that. I know I I went through a phase where I was waking up at 3 in the morning like \[sighs\] what's going to happen to what we do. So I know that many of you are probably feeling this way and I want to pray for you. Pray for this. Pray for your anxiety. All of it. Let's do it right now.

**18:15** · God, I thank you for the person on the other side of this camera, the screen. um wherever they are, who they are, if they're feeling the stress and anxiety of AI and how it's going to impact their jobs.

**18:28** · \[sighs\] Give them a piece, God.

**18:31** · Give them a piece. Give them optimism.

**18:34** · I've adopted the idea, the mentality of relentless optimism. And Lord, I pray that that that idea will fill them right now. Just fill their their life, their bones, everything. and just let them feel relieved and excited and not stressed about AI.

**18:52** · I pray that you would reveal to them a path forward for their family, for them.

**18:58** · Reveal to them that they're valuable and amazing and that they are so much more than what they were doing than their skills that they have been developing.

**19:08** · And those skills are still valuable, but they are more than that. and that what's coming with AI, I mean, no one really knows, but what's coming is going to be good. And just like everything we encounter in tech, we're going to adapt.

**19:21** · So, Father, I ask in your name that you just bless them right now. Fill them with that optimism and peace and a path forward. I ask this in your name, Jesus.

**19:31** · And also I ask in your name that they will know you, Jesus. That you will impress upon their hearts right now how real you are. And that you love them and you care for them. That they are wonderfully and fearfully made. And that \[sighs and gasps\] they may have found satisfaction and have been looking for something to give them value and meaning in their work. and that may be kind of fading a bit.

**20:00** · And I pray that they would find their meaning and their identity in you, Jesus, because only complete happiness and joy can be found in you. I ask this in your name. Amen. Hey, thank you for letting me do that. I know it's kind of weird. I know you may not agree with everything I'm saying. Uh that's okay. We can disagree. Uh but I want you to know that I care for you. And if you need anything, if you need to talk or anything at all, let me know.

**20:28** · That's all I got.