---
title: "Intelligence Dissolves Privacy"
source: "https://www.lesswrong.com/posts/rNpGFodLTFvhqLmK6/intelligence-dissolves-privacy"
author:
  - "[[Vaniver]]"
published: 2026-04-01
created: 2026-05-05
description: "The future is going to be different from the present. Let's think about how. …"
tags:
  - "brain_spew"
---
The future is going to be different from the present. Let's think about how.

Specifically, our expectations about what's reasonable are downstream of our past experiences, and those experiences were downstream of our options (and the options other people in our society had). As those options change, so too our experiences, and so too our expectations of what's reasonable. I once thought it was reasonable to pick up the phone and call someone when I wanted to talk to them, and to pick up my phone when it rang; things have changed, and someone thinking about what's possible could have seen the dilution of that signal into noise coming. So let's try to see more things coming, and maybe that will give us the ability to choose what it will actually look like.

I think lots of people's intuitions and expectations about "privacy" will be violated, as technology develops, and we should try to figure out a good spot to land. This line of thinking was prompted by one of Anthropic's 'red lines' that they declined to cross, which got the Department of War mad at them; the idea of "no domestic bulk surveillance." I want to investigate that in a roundabout way, first stepping back and asking what is even possible to expect, here.

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/v1775097940/lexical_client_uploads/jokumifetyksx8pwkcfl.png)

"any legal use"

Widespread access to intelligence will change privacy expectations dramatically, by allowing for 1) much more recording of information, 2) much more processing of recorded information, and 3) much more sophisticated interpretation of that information.

In American contexts, law enforcement officers have access to a wide range of information about people, but require permission to look at it (a ‘warrant’). If you’re a person of interest in a crime, they can look at your cell phone records to get evidence about whether or not you were involved in the crime, but otherwise you’re protected by the 4th Amendment from unreasonable searches and seizures. But what determines what is *reasonable*?

Some considerations:[^1]

1. What protects the privacy of innocent individuals. People with access to LEO systems might have their own personal reasons to look up information–like seeing what their ex-girlfriends are up to–which society doesn’t want them to be able to act on.
2. What is informative. If you have to review the cell phone records of everyone in the LA area whenever a murder happens in LA, you’re probably going to be wasting many hours of investigative effort, because most of those people are irrelevant to the case.
3. What is cheap. If you need to put a public servant with health care and a pension on reviewing information, it is harming the public (who is paying for this!) to make them review irrelevant information.

This has already been changed by technology becoming cheaper. It would be prohibitively expensive to have police doing stakeouts on every corner; it is not prohibitively expensive for every shopkeeper to have a CCTV system recording the street outside of their shop, and those costs continue to decline. Put together a network of those, and now a city can be under near-complete surveillance.[^2]

AI continues these trends. If LLMs can review cell phone records for pennies on the dollar, it might make sense to look at a hundred times as many records. And now rather than having to have a person go camera-to-camera and track the movements of an individual thru the city, you can have a software system using facial recognition and gait analysis and spatial modeling to track whole crowds at a feasible cost.

So as a technical matter, it is already possible or it's not very far from interested parties being able to track your location at any time, if you have your phone on you or you're in a car or you're inside a city, in a 'bulk' rather than targeted way. As a social matter, this might seem pretty impolite--or it might be part of a trade most people are willing to make.

In particular, one other way that technology changes the dynamics is by making it easier for attackers to do significant amounts of damage, which raises the value of surveillance, and of predicting and catching crimes before they happen rather than investigating and punishing them after the fact.

Let's return to the interpretation of information, and look at some subtler ways that increased intelligence will change the dynamics. Many things can be inferred from 'public records' in nonobvious ways. For example, if your camera is fast enough and sensitive enough, you can measure someone's heartbeat just by watching the subtle blush-and-pale cycle of the blood in their face; standard cameras are good enough for this, and changes in heartbeat are informative about thoughts, along with other subtle changes in facial appearance.

But I'm going to talk about gaydar, because it ties back into the broader social questions of where we want society to end up. Sometimes, people can guess the sexual orientation of another person just by observing them, using both deliberate and accidental features. Gay men sometimes benefit from looking gay ("the earring in his right ear suggests--" or "his haircut implies--"), and also they have various developmental differences that can manifest in appearance. In 2018, [Wang and Kosinki trained a neural network](https://psycnet.apa.org/fulltext/2018-03783-002.html) to do it off of dating photos and it substantially outperformed humans (80% success rate rather than 60% success rate.) [^3]

So as we we get more widespread intelligence–as software gains capabilities that were formerly available only to human experts and use of that software becomes potentially widespread–we stop being able to hide some things. What do we want to do about that?

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/v1775099877/lexical_client_uploads/qom7jlbyij1wnrt7igks.png)

This doesn't include a line for when an expert observer could have guessed that I'd be gay, which is probably a decade earlier.

The world has changed a lot here, over the course of my lifetime! When I was a child, being gay was mostly hidden and navigating being gay required subtlety and discernment. Part of the response to the AIDS crisis, at the insistence of gay rights groups, was to prioritize patient confidentiality over stopping the spread.[^4] But now, as an adult, being gay is not mostly hidden; you don’t have to use a profiling algorithm on my face, up until Facebook removed it in 2022 you could just go to my profile and see that I’ve checked the box for “interested in men”. (Or you could search my LessWrong comments, or–)

So from the perspective of the 2020s in America, it feels actually pretty benign. (But that's not universal; the situation is both worse in other countries, and the prospect of 'transvestigating models' feels much less benign.)

More broadly, it seems to me like there are three options for how we can react to widespread knowledge of things that were previously hidden:

1. **Acceptance.** Knowing who's gay and who's straight is fine, because both options are fine, and not being confused or ignorant is useful. (I wasted a lot of hope pining after straight guys, and a few straight women wasted hope pining after me, which all could have been avoided.)
2. **Purging.** Knowing who's gay and who's straight allows you to remove all of the gay boys from your all-boys high school, because you actually wanted an *all-straight-boys* high school.
3. **Pretend ignorance.** Even tho you *could* know who's gay and who's straight, you have a policy like Don't Ask, Don't Tell where everyone tries to act like they don't know it. (After all, only a stalker would know something like that.)

I think there's situations where each of the three is the most appropriate option. In particular, I think the situation for acceptance of sexual minorities has been on this positive trendline in part because of increased knowledge and decreased privacy. The understanding that lots of gay people were 'normal' did a lot of normalize being gay!

I also think it's easy to find situations where purging or filtering are quite sympathetic. I in fact would strongly support my local subway system tracking who the most anti-social riders are and banning them, so that the system is cleaner and safer, and if it is cheaper and better to do so with facial recognition technology or similar 'totalitarian surveillance measures', that seems probably worthwhile. (Similarly, it's very nice to not be murdered in a terrorist attack.) But it's also easy to see how such technologies can be deployed for undesirable ends; if border agents look thru someone's phone to try and determine if they're a member of a terrorist network, they can also determine whether they've made social media comments that are critical of Trump. A current controversy is how much local cities should sign on to surveillance networks like [Flock](https://www.flocksafety.com/); when many jurisdictions have committed to not cooperate with federal law enforcement on immigration enforcement, signing on with a contractor which *does* cooperate with federal law enforcement runs counter to those commitments.

As a fan of the truth and a believer in its efficacy, I am most biased against the third option. Yet many widely and strongly cherished parts of our society rest on it! Anti-discrimination laws that bar decision-making based on race are an example that it seems unwise to recklessly drop, and yet race is often quite easy for people or systems to infer.[^5] European regulations about privacy seem to me to mostly be insisting that technology develop in this direction.

Yet my overall sense is that we cannot stick our heads in the sand for long. The highest priority uses will drive adoption of the mass surveillance technology, and I strongly suspect that concerns about terrorism, great power conflict, and small-scale bad actors will be serious enough that these highest priority uses will not be foregone. Then once the camel's nose is in the tent the rest of the camel will follow. The best way out is to fix our goals and preferences:

Rather than hoping that local entities can prevent the enforcement of immigration rules that are clearly not in their interest, develop new immigration rules that cities across America *would* be comfortable cooperating with, and then use the advanced technology to do so cheaply.[^6]

Develop watchmen that watch the watchmen, such that people with access to bulk surveillance systems and are using them in corrupt ways are themselves found and punished.

Most controversially, become comfortable with benign deviancy (of the sort which will turn out to be much more prevalent than it seems) and align criminal standards with actual behavior (a world where the true speed limit is 20mph higher than the posted one will not be well-served by ubiquitous vehicle tracking).

Perhaps most importantly, it might help you to start behaving as if you're being watched and things about you are more obvious than they once were.

[^1]: I should note that I'm thinking like an economist or systems designer, not a lawyer. There must be extensive case law on what people currently think is reasonable or unreasonable, but that's only relevant for reasons of continuity. We’re imagining the future, of what things will look like *after* people have adapted to their new situation, which plausibly involves major changes to the underlying laws.

[^2]: Consider also the situation with cashless toll systems like EZ Pass, which have [long worried privacy advocates](https://insidesources.com/your-ez-pass-and-the-state-dot-is-probably-watching-you/), as they can (and sometimes are!) used to track where people travel. There's nothing *fundamentally* rights-violating here, tho; this could be replicated by anyone with enough eyes in enough places. (We already consent to each car having a unique identifier to make tracking easier!)

[^3]: “Wait,” you might say, “60% success rate for a trait with a baseline prevalence of less than 40%? How did the human guessers do worse than always guessing ‘straight’?” In their dataset, they equalized the number of homosexual and heterosexual faces, so pure-chance guessing would have scored 50%. This is still an artificial situation (they're dating site photos, not street photos) which doesn’t take into account base rates.

[^4]: As someone interested in public health, this horrifies me, but I acknowledge the ways I am a sweet summer child who grew up with the internet and the dramatic upswing in acceptance and downswing in intolerance, and decision-makers in the 80s had very different life experiences and expectations.

[^5]: When I was a data scientist, I ended up looking into the contours of compliance here. Many things that aren't race are nevertheless informative about race, and so you can construct a composite out of information which individually *is* legal or ethical to use, which is just a proxy for race, and thus the composite is illegal or unethical to use, and so people developed statistical techniques to try to make sure this isn't happening, and that the composite is composed just of 'legitimate' influence. This involves being deliberately and willfully blind to facts about the world to achieve some social end, but that's what polite ignorance is!

[^6]: There are too many horror stories of ICE misbehavior, detaining American citizens and racially profiling people on the street. Would the situation be improved or made worse by a national facial recognition database? On the one hand, Flock and similar systems would allow ICE to notice whenever someone without legal residency went out in public; on the other hand, there would be no excuse for not immediately checking the database and releasing legal residents. I think immigration reform means we can get the benefit of the latter without having to pay the costs of the former; of course, immigration reform is its own problem that deserves its own post.