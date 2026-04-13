---
title: Note Detail
source: https://notegpt.io/detail?id=AkqYLihWtlg
author:
published:
created: 2026-04-06
description:
tags:
  - brain_spew
  - sere
---
[

30% Off

](https://notegpt.io/pricing)

S

5 Low-Cost Tools to Get Started In Signals Intelligence

00:00

I hate to say it, but we prepared citizens aren't that prepared after all, especially when it comes to information technology. We are very reliant on the grid and internet infrastructure to get all of our news and information and to communicate with each other. If that goes away, we lose that ability.

00:22

Moreover, even if it doesn't go away, we are reliant on a system that is actively spying on us that is basically an LPOP in our pockets that we carry around with us. And who knows what kind of technocrat malign actor deep state shenanigans is using that information. So, what if we could flip the script and actively spy on those who would spy on us? Well, I'm Civil Defense Engineer, and today we are diving into the wide world of SIGINT or signals intelligence.

Read More

00:56

And to do that, we're going to be using some fairly such as this new TinySA that I've picked up. And other even cheaper devices such as an RTL-SDR, and even just your cell phone. So, we'll go over what equipment you'll need to get started, then we'll take a quick tour of the electromagnetic spectrum, and finally we'll wrap up with a demos such as tracking aircraft, tracking drones, and intercepting drone feeds, and tracking nearby Bluetooth devices, and even listening in on UHF communications and figuring out the location of a station using some directional antenna. So, I've been excited for this one. I've been preparing for it for quite a while. Hope you enjoy. SIGINT is a broad discipline of

Read More

02:00

intelligence gathering that is focused on signals, electronic signals, especially of the EMF variety that has to do with the interception, the identification, and the analysis of enemy or malign actor signals. A lot of videos on this topic just launch into what information can be gleaned from the airwaves, which is important.

02:28

It's a It's a big part of SIGINT, but it's only one part. In fact, that could be considered COMINT, which is a subset of SIGINT. And a lot Bear with me as I nerd out on definitions for a second because it'll be relevant to shaping how we think about this and what our goals are here. So, there's COMINT, then there are some other subsets such as ELINT, electronic intelligence, which is typically focused on radars and what frequencies is the enemy using for their radars and what jamming capabilities do we need to bring to the table, all that kind of stuff. We're less concerned about that as prepared citizens because our center of gravity is not our expensive Air Force and we're not quite so concerned about figuring out what anti-aircraft capabilities there are on the ground. We might be a little bit concerned about

Read More

03:27

that if especially if we're doing drone activity, but it's not the main focus for us. There is also what's called FISINT, which is foreign instrumentation signals intelligence, which is dealing with the data links of missiles, for example, the anything that is a machine-to-machine communication, so not human-to-human.

03:57

The missiles in particular, that's an even subset of that subset, which is called TELINT, telemetry intelligence. And interestingly, um a lot of that is quite open book, I learned. I didn't realize that, but some information about our strategic missiles is actually openly known by Russia and vice versa because we didn't want them to get faked out by anything and panic and bomb us back to the Stone Age.

04:31

We are interested in that in so far as the drone warfare of the 21st century has made its way down to our level. So, you can think of us looking at a waterfall chart and or even using a dedicated drone detector to look for those drone signals as a form of TELINT. So, that is something we're going to be doing as well.

05:01

We also are interested in whatever aircraft are in our area, which I regularly do every single day using the ADSB Exchange website, and I've have a web page pinned on my phone as well. Of course, for us to get the information, we need to be connected to the internet. But, we can set up our own ground tracking station for aircraft.

05:24

And that way, if we are in an area without cell service or we don't want to connect to the internet or the internet is not available for whatever reason, we can still receive ADSB transponder information for aircraft in our area. So, we're going to learn how to do that, but first let's take a look at the equipment needed and learn about the electromagnetic spectrum.

05:50

Let's take a look at what equipment we'll need for basic SIGINT. The first piece of equipment, from lowest price to highest price, is the cell phone. Now, this is probably the most expensive piece of equipment, honestly, but since everybody has one already, I'm considering it to be free. You can do a couple of things with this.

06:11

One is you can track what BLE devices are around you, Bluetooth, basically. And that will give you a sense for if there are other devices in the area and maybe even what types of devices. Sometimes, if it's an Apple device, it will be rotating through the ID and so all it tells you is that there is an Apple device nearby.

06:34

It won't tell you that it's that same specific Apple device that I've seen elsewhere. All right, I wanted to break in here and show you a quick demonstration of how this app works. So, BLE radar, unfortunately, I think you'll have to side-load it onto your phone. I didn't see it in the App Store, and I don't remember how I got it.

06:52

I've had it for a while. But, it's pretty easy to use. You just hit scan, and then it will show the devices around you. And as you can see, there are my two of my Meshtastic devices listed at the top, and it will give you a range estimate, 0.8 m, 0.3 m. Well, they're literally just sitting on the box back there.

07:12

So, that's pretty useful. And actually, I was able to accidentally spy on my coworker. I could tell when he was in his office because he had this little device that would measure radiation and it would connect via Bluetooth to his phone. And I could see exactly when he was in his office and when he left because it would show that range estimate right there.

07:34

And sorry, Mike, I'm not trying to spy on you. I know he's a subscriber, hopefully he's not watching this. You can also set radar alerts here and um some filters or even device IDs that match, it will send you a notification when it's in range. Devices following me, if you can see that something is always within range and you're not really sure why that is, it can notify you.

08:01

And there's also this journal thing. I haven't used it, I'm not sure how that works, but yeah, it's a pretty cool little app. The next piece of kit, again, from least expensive to most expensive, is the mighty Baofeng or any other handy talkie you may have cuz the point is you can scan with it. And once it picks up a signal, it will stop and then you can listen in.

08:28

Now, that's not very expedient because it takes a long time and it can only listen on one frequency at a time. So, you'll miss out on a ton of stuff. And if somebody jumps from one frequency to another or if they're doing cross-band repeating or anything like that, you are going to miss out on a lot of messages.

08:50

So, it's not very efficient. I just wanted to bring it up that that is one way you can Oh, listen. Oh, hear that? That was some digital mode. So, that's interesting. Let's talk about the SDR. Now, this is a $40 device, just a USB dongle, RTL-SDR. And this can plug I have an adapter so that I can plug into my phone. And I have the smaller rabbit ear antenna on here so that I can receive the 1090 MHz from aircraft.

09:28

And with just a couple apps that you can download on your phone, which I'll show you how to do in a second, you can track aircraft off grid and you don't have to rely on your cell connection. The other benefit of an SDR is that you can receive a broader spectrum than maybe you this that you're limited to just a few bands.

09:52

And you also can see a waterfall chart. And that is beneficial because say people are switching frequencies or there's multiple things going on at the same time, you can see visually when they're transmitting and then go listen to it. However, I haven't found a very good app for that on the phone. So, you might have to use the SDR sharp software on your computer.

10:23

If you guys know of a good app for doing SIGINT in the field on either an Android or Apple device, let me know. I'd be curious to know. The other thing about this is that it is limited to 1.3 GHz, I think. It wasn't as much as I thought. Since when I got this at first, I was using it to listen in on HF frequencies.

10:45

I wasn't even thinking about the higher frequencies like 2.4, 5.8. I just assumed that it covered that, but it doesn't. I don't know if they have versions of this device that do. I don't think so. You'd have to probably explode for a higher end SDR if that's the case. But, we have other devices that we can use to do SIGINT in those those areas of the spectrum.

11:10

For instance, this here is like a $65 device. This is for receiving the 5.8 GHz analog video such as for FPV drones. And I think it has a scanning function on here, so it can pick up when it receives those signals from an approaching FPV. That's not the best way to do that if you're if you're really trying to detect drones and you are in a life-or-death situation.

11:36

However, it is a way to do that and you can even intercept those signals and maybe figure out where the drone operator is located if you're if you're good at it. Lastly, very important piece of kit that I've recently added. TinySA, this is a spectrum analyzer. It can view the entire spectrum from like 0 to 5.4 GHz.

12:04

And it will can also display a waterfall chart. You can zoom in on certain areas of interest and then when you see transmission that you want to listen in on, you can go to that and then plug in a headphone jack and then listen to that frequency and hop around as needed. It's pretty powerful cuz spectrum analyzers until very recently in fact, they were quite large devices, pretty complicated and expensive.

12:30

Now, with the advent of SDRs, they have shrunk in size and increased in utility. Now, before we dive into the function of the gear, let us take a brief tour of the electromagnetic spectrum. Now, this is a wall chart provided by the National Telecommunications and Information Administration Office of Spectrum Management, which some of us know a thing or two about being on the spectrum.

13:00

It's nice that there's an office to help us manage it. Well, this is all of the allocations by the FCC in the US anyway. And as you can see, it's quite the eye chart. And in fact, it has so much information that you pretty much can't read it. Like, what does that say? You have to download the PDF, which I'll link below. Even then, it's kind of hard to read some stuff, but you know, it gets the general idea across.

13:26

We've got the different bands from low frequency, medium frequency, high frequency, very high frequency, ultra high frequency, super high frequency, extremely high frequency, and then tremendously high frequency. No, that stands for terahertz frequency. They broke with it. I don't know why they keep adding higher and higher intensifiers the further down you go.

13:54

Probably cuz back when Guglielmo Giovanni Maria Marconi Bravo. first developed the first radio communication system, he was using medium frequency. And as they kept discovering or developing more technology for higher and higher frequencies, they just had to keep on adding intensifiers to make it sound even higher.

14:16

For us who got our start in amateur radio, probably your first exposure to the different bands came in the form of this chart, which shows the different transmission privileges each license level has. But, if you look closely at this chart, you see just how narrow of a slice the amateur allocation is. When you get started with technician level, you're on VHF, which there's our 2-m slice, and UHF, which is right over here at 70 cm.

Read More

14:47

And then of course, we have HF. There's 40 m, there's 20 m, and so on. Now, I've really only scratched the surface of the different types of RF there is out there. But, I do want to highlight a couple of things. In a in a second, we are going to do a demonstration tracking the ADSB transponder transmissions from airplanes and aircraft, which is 1090 MHz.

15:15

So, all of this is the allocation for aeronautical radio navigation and communications. The blue areas are broadcasting, so we've got AM radio down here. We've got FM radio and you know, the TV TV broadcasting channels. And then down here, we have a ton of carrier information. You know, in the in the super high frequency and extremely high frequency range, we've got different radar systems.

15:48

We've got all kinds of allocations for for different carriers and then we get into like millimeter wave thing. So, I can't read all this, but it does say mobile satellite all kinds of stuff down here. There's a gazillion telecommunications frequencies in the world and this just gives a road map of what bands that they're in.

16:21

And as for identifying signals, there's a great website I want to introduce you to. And as you're exploring different signals on the spectrum that you encounter either with your SDR or with a spectrum analyzer, I encourage you to check out this website called SigID, which allows you to see what certain signals from around the world look like on a waterfall chart and what they sound like when you play them.

16:50

It gives you information on what frequencies they operate on and what bandwidth they use. I find it to be a fun challenge to try and find these signals out in the real world. For instance, try figuring out what signals are generated by your car either from TPMS or keyless entry, remote start kind of thing.

17:16

You can also try and pick up satellite signals. Or if you live around any military installations, you might even be able to detect radar signals. And good luck with that one though. All right. So, here are the two apps you'll need to use this guy. The first is the RTL-SDR driver. And you just need to install it.

17:43

You don't need to do anything special like run it because actually when there are Well, let me plug in the device. Okay. Okay, open RTL driver to handle blog V4? Yes. I think that opens this app. Now, you don't need to be running it when you are actually using the second one because it can only use use one app can use it at a time.

18:10

So, that's ADSB radar. Would like access to its location. While using the app, okay. Next, go up here and hit this play button up here. And it will start receiving. It's already received 23 messages. 49. Now, let's go over to the radar here. See, yep, there's a couple couple aircraft we've already detected.

18:48

And you can even go to the map, which I'm going to click off of that before it shows the detail of the map cuz I don't want to show you exactly where I live. But, um this is a very useful thing to receive what aircraft are in your area without having any cell connection. Oh, got another one. So, yeah, that's pretty fun.

19:11

Now, to calculate the length of these arms, it's that handy-dandy dipole equation. And basically for this, you just push them all the way in. I think it might be a little bit out. I'm not an SWR chaser, so I don't care exactly whether it's completely resonant or not, but I'll get close. And as you can see, it does the job of picking up the aircraft.

19:46

Let's go over the function of the TinySA. Turn it on with the switch up here. And here we have a graph of the signal strength across the spectrum. And right now we have it running from 430 MHz up to 450 MHz. So, roughly 70 cm band. Uh it looks like we have a signal receiving right now.

20:13

The marker will be at the peak here and then it will tell you what frequency it's at up here. The signal strength in the Y axis is in DBM. And it will tell you what the peak signal strength is as well. So, to change the frequency range, you go to the main menu, hit frequency, and then you can change the start and you can go all the way from 100 kHz up to by default 900 MHz.

20:54

Now, you can go a lot higher than that, but that's the full range by default. This here is the TinySA Ultra. So, the first thing you'll want to do when you get this device is enable ultra mode. To do that, go back to the main menu, hit config, \[clears throat\] hit more, and then enable ultra. Now, you have to be aware here that by default it will be disabled.

21:21

And for some reason you have to enter a code to enable it. Visit the website for the unlock code. Well, I'll just give it to you now. It is 4 3 2 1. And I don't know why they hide it behind some code here. I think it's basically to I don't know if there's like a risk of burning out the board if you're not careful.

21:45

But, as you can see with a larger range here, we're going from 0 to 3 GHz, the refresh rate is pretty slow. It's like once every 2 seconds or 3 seconds. So, if you want to narrow it down a little bit, that will really help the refresh rate. So, let's try back to the main menu, frequency, let us go from let's say 1.5 GHz up to let's do 2.

22:22

8 or so. Just something like that. That should give us kind of a a broad enough spectrum to see a lot of stuff going on. You can see a a peak signal around 2.4 something. Oh, and it jumps around. That might be my Wi-Fi over here. And then this one, 1.9 something. I'm not sure, but I think it might be a cell carrier of some sort.

22:48

And in fact, let's shorten this antenna. Now that we're in the GHz range, that might help us a little bit. Now, there's one more functionality that I want to show you here. And this isn't a full tutorial, but a very important piece of the puzzle. I'm going to go back to the uh the 70 cm that I was on before. Hopefully that signal is still out there.

23:21

All right. You can display a waterfall chart. To do that, go back to the main menu, hit display, and click waterfall. And as you can see, it'll show you the history of the signals. And it will allow you to see visually when different frequencies light up. And uh that'll allow you to more quickly ascertain what frequencies are in use.

23:55

And then you can go over to them using the scroll wheel, or you can also click on the marker and drag it, but that's pretty difficult. So, I recommend using the scroll wheel. And then once \[snorts\] you're on it, you can plug in the headphone jack and listen in. Uh I think you'll have to go and enable listen.

24:15

So, you go to level and listen. Uh unfortunately, it will keep deleting your history on the waterfall chart when you make a change like that. And it also doesn't save that to the SD card here. I think that'd be really cool feature if they could add that. The ability to save um that as an image or PDF or whatever. You know, that'd be really cool.

24:40

But, it only saves I think it's like a CSV of your signal strength over time. The other downside is that when you're playing, you don't see anything on the screen. The signal strength, the waterfall, it all just freezes as you're listening. So, that's a the basic functionality. So, this is far from a full tutorial, but uh the next thing we'll do, we'll go back outside and I will show you how to use this device to track down a signal using a directional antenna, which you can do by unscrewing the default antenna and plugging in your own antenna with a bit of coax and a SMA connector. All right. I have a beacon out here on low power on 445 MHz and this is on vox. So, it is transmitting as long as I am

Read More

25:40

talking here. Okay. So, here's my directional antenna. If you want to check out the video I did on it, I'll link it below. This is a UHF Yagi antenna and you can connect it to the TinySA. So, let's turn her on here. There is our beacon. And as you can see, it's fairly strong. But, as I'm holding my antenna away from it and moving it towards it, it climbs in strength.

26:24

And it drops out every once in a while, which makes it more challenging, but that's what you would expect in real world communications. And then keep moving it, and it drops in intensity a little bit from its peak. And this takes a lot of practice. Also, I would be greatly served by having an in in-line attenuator, which I aren't too expensive.

26:52

I should invest in something for that. Um but this gets the point across. Point it away, lower, point it towards, and it's higher. Now, I didn't bring a compass or anything, so I can't show you the full radio direction finding process, but I I'll link the video below how to do that.

27:24

Last demo here will be using the Solo Good Drone Feed monitor. And uh I don't have a drone today, but I've got one of the 5.8 GHz cameras. So, we'll just plug that into a battery here and uh it will automatically start transmitting. Okay. So, this is not a great real world test here because the the thing is sitting right here, but I just want to demonstrate the function. So, power on.

28:06

And search. Searching through all the channels and there it is. There we are. Hello, my friend. Hello. Hello. This is Civil Defense Engineer. Okay. So, as you can see, this could be used as a FPV drone detecting device. It would not be practical, but it's possible. Also, you know, it wouldn't last long before people start using other frequencies, non-standard frequencies, and uh you'd have to be a little more creative.

28:54

But, especially in Ukraine when the war just started, people were using off-the-shelf drones, off-the-shelf equipment just like this. And for a long time, and they still do, but they've got a lot more options as well, including fiber optic drones and other frequencies. For your action items for this video, conduct an RF survey of your AO.

29:17

See if there's any suspicious RF out there, any suspicious frequencies that you should record. Write them down. If if there's drone activity, if there are observation devices set up, LPOP's, and they're using RF to communicate, uh and then go out and practice with either your SDR or your spectrum analyzer, and maybe have somebody have a buddy out there pretending to be a enemy station, and see if you can track him down or glean any information from it. All of this is a perishable skill.

Read More

29:56

It's a hard skill to learn and you won't learn it just by watching a YouTube video. You got to get out and do it. I'll have more coming out on SIGINT in the future and in fact, I don't want to over promise here, but I do have a special device coming that a company called Caradag is letting me borrow.

30:18

It's a like a $2,000 piece of equipment that is used on the front lines in Ukraine to keep the soldiers safe from drones. And I I couldn't afford it, but I I asked them, "Hey, can I borrow it for the YouTube channel?" And they agreed. So, hopefully that's coming. I hope I didn't just jinx it.

30:36

But uh stay tuned for that. There are also some other devices that I wished I could have tried such as the KrakenSDR which uses a Doppler method of radio direction finding which gives you a lot more flexibility than a Yagi antenna built for a specific frequency. I do have a subscriber out there who said they have one and uh I wish I could do a collab with him, but he's in another state.

31:02

But I'll I should reach out to him and and talk about it. Anyway, that's SIGINT and stay tuned for more. This is Charlie Delta Echo out. >> \[music\]

### Chapter: Exploring Signals Intelligence (SIGINT) for Prepared Citizens

#### Introduction: Understanding SIGINT and Its Importance in Modern Preparedness

- \[ ~ \]  
	In an age where society is deeply intertwined with digital infrastructure, our heavy reliance on the **internet** and **power grids** poses a vulnerability. The sudden loss of these systems could cripple our ability to communicate and access vital information. Furthermore, the pervasive presence of smartphones—described as **LPOPs** (Little Personal Operating Platforms)—raises privacy and security concerns, as these devices constantly collect and transmit data, potentially exploited by malign actors or **technocrats**.

This chapter introduces the concept of **Signals Intelligence (SIGINT)**, a discipline involving the interception, identification, and analysis of electronic signals, particularly electromagnetic frequencies (**EMF**). SIGINT offers a way to "flip the script" by enabling citizens to monitor and spy on those who might spy on them, enhancing situational awareness and self-reliance.

Key vocabulary introduced includes:

- **SIGINT (Signals Intelligence)**: The broad practice of intercepting and analyzing electronic signals for intelligence purposes.
- **COMINT (Communications Intelligence)**: A subset of SIGINT focused on human-to-human communications.
- **ELINT (Electronic Intelligence)**: Intelligence gathered from radar and other electronic systems, primarily focused on non-communication signals.
- **FISINT (Foreign Instrumentation Signals Intelligence)**: Concerned with machine-to-machine communications, such as missile telemetry.
- **TELINT (Telemetry Intelligence)**: A specialized form of FISINT that deals with telemetry data from missiles or drones.

The significance of SIGINT for prepared citizens lies in its ability to monitor drones, aircraft, and other electronic devices in the environment, empowering people to maintain awareness even when traditional networks fail.

- Advanced Notes:
	- Preparedness today must include awareness of technological dependencies and vulnerabilities.
		- SIGINT provides a practical toolkit for information gathering beyond conventional means.
		- Understanding subsets of SIGINT (COMINT, ELINT, FISINT, TELINT) refines focus on relevant signals.
		- The chapter aims to make SIGINT accessible through affordable equipment and practical demonstrations.

---

#### Section 1: The Scope of SIGINT and Its Subsets

- \[ ~ \]  
	SIGINT encompasses a range of intelligence activities centered on electronic signals. While **COMINT** involves listening to human communications, **ELINT** focuses on radar frequencies and electronic emissions that reveal enemy capabilities such as radar jamming. For everyday citizens, ELINT is less critical unless involved in drone activity.

**FISINT** and its subset **TELINT** deal with automated machine communications, particularly telemetry from missiles or drones. Interestingly, some telemetry data about strategic missiles is openly shared between nations like the U.S. and Russia to avoid accidental escalations, highlighting the transparency that exists in certain high-stakes SIGINT contexts.

Prepared citizens can leverage TELINT concepts by monitoring drone telemetry signals, a growing concern in modern conflict and surveillance scenarios. Similarly, tracking aircraft via their ADS-B transponder signals is a practical application of SIGINT, which can be done independently of internet access using ground tracking stations.

- Advanced Notes:
	- SIGINT is broader than just intercepting conversations; it includes radar and telemetry.
		- Civilian applications focus primarily on drone and aircraft signal detection.
		- Existing public resources like ADS-B Exchange enable aircraft tracking but depend on internet connectivity.
		- Setting up independent ADS-B receivers enhances offline detection capabilities.

---

#### Section 2: Essential SIGINT Equipment for Citizens

- \[ ~ \]  
	The journey into SIGINT begins with selecting the right tools, each with different cost and capability profiles:
- **Cell Phone** (considered "free" since most have one):
	- Can scan **Bluetooth Low Energy (BLE)** devices nearby, offering awareness of active devices in the vicinity without identifying specific individuals definitively.
		- Apps like **BLE Radar** can scan, log, and alert users to devices, providing real-time proximity data.
- **Handy-Talkies (e.g., Baofeng radios):**
	- Affordable radios capable of scanning frequencies sequentially but limited by only listening to one frequency at a time.
		- Inefficient for dynamic or frequency-hopping communications but useful for basic monitoring.
- **RTL-SDR (Software Defined Radio) Dongle (~$40):**
	- A USB device capable of receiving a wide range of frequencies up to approximately 1.3 GHz.
		- Can be connected to a phone or computer and used with apps to track signals such as aircraft ADS-B transponders at 1090 MHz.
		- Provides a **waterfall chart**, visualizing signals across frequencies to detect transmissions and frequency hopping.
		- Limitation: Does not cover higher frequencies like 2.4 GHz or 5.8 GHz, common for drones and Wi-Fi.
- **5.8 GHz Analog Video Receiver (~$65):**
	- Specialized for detecting analog video signals used in FPV (First Person View) drones, useful for drone detection and signal interception.
- **TinySA Spectrum Analyzer:**
	- A compact, versatile device covering 0 to 5.4 GHz, capable of spectrum analysis including waterfall displays and audio demodulation.
		- Enables zooming in on specific frequencies and listening to transmissions via headphone jack.
		- Represents a significant advancement due to its portability and affordability compared to traditional spectrum analyzers.
- Advanced Notes:
	- Equipment choice depends on target frequencies and operational needs.
		- Spectrum analyzers and SDRs allow simultaneous multi-frequency monitoring.
		- Mobile apps complement hardware but have limitations, especially on smartphones.
		- Knowledge of antenna types and connectors (e.g., SMA, Yagi antennas) enhances signal detection and direction finding.

---

#### Section 3: A Tour of the Electromagnetic Spectrum and Frequency Allocations

- \[ ~ \]  
	Understanding the electromagnetic spectrum is foundational to effective SIGINT. The **National Telecommunications and Information Administration (NTIA)** provides detailed frequency allocation charts delineating the use of different bands by the **Federal Communications Commission (FCC)** in the U.S.

The spectrum is divided into bands characterized by increasing frequency:

- **Low Frequency (LF)**
- **Medium Frequency (MF)**
- **High Frequency (HF)**
- **Very High Frequency (VHF)**
- **Ultra High Frequency (UHF)**
- **Super High Frequency (SHF)**
- **Extremely High Frequency (EHF)**
- **Tremendously High Frequency (THF or Terahertz)**

These bands are allocated for diverse uses such as AM/FM radio, television broadcasting, aeronautical navigation, satellite communication, radar, and mobile telecommunications. For example, aircraft ADS-B transmissions operate at 1090 MHz within the UHF band.

Amateur radio operators typically have access to small slices of these bands (e.g., 2 meters in VHF and 70 cm in UHF for technician licenses), emphasizing how vast and complex the spectrum is.

- Advanced Notes:
	- Knowledge of frequency allocations helps avoid interference and identify signal sources.
		- Different applications utilize distinct bands, from commercial broadcasting to military radar.
		- Waterfall charts visually represent signal activity across frequencies, aiding identification.
		- Resources like **SigID** website help decode and recognize signals by frequency and waveform.

---

#### Section 4: Practical Demonstrations and Signal Tracking Techniques

- \[ ~ \]  
	The chapter includes hands-on demonstrations illustrating the use of SIGINT tools:
- **Tracking Aircraft with RTL-SDR:**
	- Installing the RTL-SDR driver and apps such as **ADSB Radar** enables reception of real-time aircraft transponder messages without internet access.
		- Example: Detection of 23 to 49 aircraft messages shortly after starting the receiver.
		- Antenna tuning using the **dipole length equation** improves reception quality.
- **Using TinySA Spectrum Analyzer:**
	- Powering on the device reveals signal strength over a specified frequency range (e.g., 430–450 MHz).
		- Peak signals are marked on a graph with signal strength in dBm on the Y-axis.
		- Enabling "Ultra Mode" extends frequency range to 0–3 GHz but reduces refresh rate (updates every 2–3 seconds).
		- Waterfall chart mode displays historical signal activity, facilitating frequency usage analysis.
		- Listening capability allows audio demodulation of selected signals via headphones.
		- Limitations include freezing of the display during audio playback and inability to save waterfall images directly.
- **Radio Direction Finding with a Yagi Antenna:**
	- Using a **UHF Yagi directional antenna** connected to TinySA enables signal strength comparison when pointing toward or away from a transmitter.
		- Demonstrates principles of locating a beacon transmitting at 445 MHz and the value of an **in-line attenuator** for better signal control.
		- Practical radio direction finding requires practice and additional tools like a compass.
- **Drone Signal Interception with 5.8 GHz Receiver:**
	- Demonstrates receiving analog video feeds from FPV drone cameras, simulating drone detection.
		- Notes the limitations of this approach as drone operators increasingly use non-standard frequencies, fiber optics, or encrypted links.
		- Highlights relevance to current conflicts (e.g., Ukraine), where off-the-shelf drones with standard frequencies were initially used.
- Advanced Notes:
	- Real-time demonstrations validate theoretical concepts.
		- Effective SIGINT requires iterative practice and technical adjustments.
		- Direction finding enhances the ability to locate signal sources, critical in drone detection or tracking hostile communications.
		- Adaptability is necessary given evolving technologies and frequency usage.

---

#### Section 5: Challenges, Skills Development, and Future Prospects

- \[ ~ \]  
	The speaker emphasizes that SIGINT skills are perishable and complex, requiring active practice rather than passive observation. Suggested exercises include:
- Conducting **RF surveys** of one's area of operations (AO) to identify suspicious or unknown signals.
- Recording and analyzing frequency data related to drones, LPOPs, or observation devices.
- Practicing tracking and intercepting signals with a partner simulating enemy transmissions.

Looking ahead, the speaker teases upcoming content featuring advanced SIGINT hardware loaned by a company called **Caradag** —a $2,000 device employed on the front lines in Ukraine for drone detection and soldier protection. Such equipment surpasses the consumer-grade gear demonstrated here.

Additionally, the **KrakenSDR**, a device utilizing the **Doppler radio direction finding method**, offers greater flexibility than traditional Yagi antennas by enabling multi-directional signal localization.

- Advanced Notes:
	- SIGINT is a continuously evolving field requiring ongoing learning and equipment upgrades.
		- Collaboration with experts and leveraging advanced gear enhances capability.
		- Real-world conflicts provide case studies illustrating the tactical importance of SIGINT.
		- The community-driven sharing of knowledge and resources is vital for preparedness.

---

#### Conclusion: Empowering Prepared Citizens Through SIGINT

- \[Summary\]  
	This chapter has explored the fundamentals and practical applications of **Signals Intelligence (SIGINT)** for civilian preparedness. In a world increasingly dependent on fragile digital networks, the ability to intercept and analyze electromagnetic signals offers a critical edge. Understanding the electromagnetic spectrum, acquiring affordable yet effective equipment, and developing hands-on skills enables individuals to monitor aircraft, drones, and nearby communications independently of infrastructure.

Through practical demonstrations—from smartphone BLE scanning to spectrum analysis and directional antenna tracking—readers are equipped with the knowledge to begin their SIGINT journey. While challenges remain, including equipment limitations and the need for practice, the path forward is clear: proactive engagement with SIGINT techniques can enhance situational awareness and security in uncertain times.

The integration of advanced tools and upcoming technologies promises even greater capabilities, underscoring SIGINT's evolving role in both civilian defense and modern electronic warfare. As the speaker states, "This is far from a full tutorial," but it lays a foundation for further exploration and mastery.

- Final Key Takeaways:
	- SIGINT empowers citizens to regain control over their information environment.
		- A layered approach, combining multiple tools and methods, is most effective.
		- Continuous learning and adaptation are essential in dynamic signal environments.
		- Collaboration and resource sharing multiply the benefits of SIGINT knowledge.

---

### Advanced Bullet-Point Summary

- **Introduction & Significance**
	- Modern society's reliance on grid and internet is a vulnerability.
		- Smartphones act as LPOPs, exposing users to surveillance risks.
		- SIGINT allows proactive interception and analysis of electronic signals.
		- Key SIGINT subsets: COMINT (communications), ELINT (radar), FISINT (machine signals), TELINT (telemetry).
- **SIGINT Subsets and Focus for Civilians**
	- ELINT less relevant for civilians except drone-related.
		- TELINT relevant due to drone telemetry signals.
		- ADS-B aircraft tracking possible independently from the internet.
- **Equipment Overview**
	- Cell phones scan BLE devices to detect nearby electronics.
		- Baofeng radios scan but are limited to one frequency at a time.
		- RTL-SDR dongle enables wide frequency reception up to ~1.3 GHz; visual waterfall charts aid detection.
		- 5.8 GHz receivers intercept analog FPV drone video feeds.
		- TinySA spectrum analyzer covers 0–5.4 GHz, provides audio demodulation and waterfall charts.
- **Electromagnetic Spectrum & Frequency Allocations**
	- Spectrum divided into LF, MF, HF, VHF, UHF, SHF, EHF, THF bands.
		- Frequency allocations govern usage (broadcasting, navigation, radar, telecom).
		- Amateur radio access is a narrow slice of the spectrum.
		- SigID website helps identify and decode signals.
- **Practical Demonstrations**
	- ADS-B aircraft tracking without internet using RTL-SDR and apps.
		- TinySA used for spectrum visualization and signal listening.
		- Directional antenna (Yagi) used for radio direction finding and signal localization.
		- Drone feed interception demonstrated with 5.8 GHz equipment.
		- Real-world relevance highlighted by drone warfare in Ukraine.
- **Skills and Future Directions**
	- SIGINT skills require active practice and hands-on experience.
		- Conduct RF surveys to identify and document local signals.
		- Upcoming advanced equipment (e.g., Caradag device, KrakenSDR) will enhance capabilities.
		- Collaboration and community involvement are crucial.
- **Conclusion**
	- SIGINT equips citizens to monitor and understand their electronic environment.
		- Combining knowledge, affordable gear, and practice builds resilience.
		- The field is evolving, with exciting new technologies on the horizon.
		- Preparedness includes mastering these perishable but powerful skills.

---

This chapter offers a comprehensive foundation for understanding, acquiring, and applying SIGINT techniques in civilian contexts, emphasizing practical knowledge and future potential.

AI Note

Save