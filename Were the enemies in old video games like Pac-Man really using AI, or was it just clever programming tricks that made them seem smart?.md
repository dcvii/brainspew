---
title: Were the enemies in old video games like Pac-Man really using AI, or was it just clever programming tricks that made them seem smart?
source: https://www.quora.com/Were-the-enemies-in-old-video-games-like-Pac-Man-really-using-AI-or-was-it-just-clever-programming-tricks-that-made-them-seem-smart/answer/OpenBlueprint?ch=10&oid=1477743910806776&share=2d21676e&srid=tIPY&target_type=answer
author:
published:
created: 2026-07-08
description: "OpenBlueprint's answer: Pac-Man’s ghosts never communicate, adapt, or learn. Their brilliantly coordinated ambushes are an illusion created by four simple rules of blind geometry.To a computer scientist in 1980, this illusion was an incredibly elegant form of AI called a finite state machine, re..."
tags:
  - brain_spew
  - games
---

](https://www.quora.com/notifications)[Were the enemies in old video games like Pac-Man really using AI, or was it just clever programming tricks that made them seem smart?](https://www.quora.com/Were-the-enemies-in-old-video-games-like-Pac-Man-really-using-AI-or-was-it-just-clever-programming-tricks-that-made-them-seem-smart)

![](https://qph.cf2.quoracdn.net/main-qimg-cd116f96183e681cc7d79534206eda3b)

Pac-Man’s ghosts never communicate, adapt, or learn. Their brilliantly coordinated ambushes are an illusion created by four simple rules of blind geometry. To a computer scientist in 1980, this illusion was an incredibly elegant form of AI called a finite state machine, relying on a mathematically rigid targeting system. The genius of creator Toru Iwatani's design was not computing power; it was giving four distinct "personalities" to the ghosts using just a few lines of code. The ghosts never actually look at the whole maze to plan a route. Instead, at any given intersection, each ghost simply calculates the straight-line distance to a specific target tile on the grid and turns in whichever direction gets it closer to that target. The illusion of a coordinated enemy team comes entirely from how each ghost defines its target tile: Blinky (Red): The Chaser. His target tile is exactly the tile Pac-Man is currently occupying. He relentlessly hunts the player down. Pinky (Pink): The Ambusher. Her target tile is four spaces ahead of the direction Pac-Man is currently facing. She does not chase; she tries to cut off the escape route. Inky (Cyan): The Fickle. His targeting is the most complex. The game draws a vector from Blinky's location to two tiles ahead of Pac-Man, and then doubles that vector's distance to set Inky's target. His movements seem erratic because they depend entirely on where Blinky and Pac-Man happen to be relative to each other. Clyde (Orange): The Coward. When he is far away (more than eight tiles), he targets Pac-Man directly, just like Blinky. But as soon as he crosses that eight-tile radius, his target abruptly switches to his home corner at the bottom left of the screen. He appears to charge in for the kill and then chicken out at the last second. When these four hardcoded mathematical rules play out simultaneously, the result is beautiful emergent behavior. A player being chased by Blinky is naturally forced to run forward, which is exactly where Pinky is already heading to intercept them. Meanwhile, Inky and Clyde act as unpredictable wildcards that seal the trap. A few lines of rigid math created one of the most convincing illusions of intelligence in arcade history. A screenshot of Pac-Man recreating the original arcade display. Photo by Bandai Namco Entertainment America (Wikimedia Commons) is licensed under CC BY 3.0.

21K views ·

View 1,029 upvotes

·

View 10 shares

·[

1 of 8 answers

](https://www.quora.com/Were-the-enemies-in-old-video-games-like-Pac-Man-really-using-AI-or-was-it-just-clever-programming-tricks-that-made-them-seem-smart)

[![Profile photo for Michael David Cobb Bowen](https://qph.cf2.quoracdn.net/main-thumb-17296487-100-nuswfmmvsmekbujhoikudktinmtidakz.jpeg)](https://www.quora.com/profile/Michael-David-Cobb-Bowen)

Link

Text