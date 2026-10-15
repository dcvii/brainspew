---
title: "Handwired: turn your regular JavaScript code into a neural net"
source: "https://chenglou.me/handwired/"
author:
published:
created: 2026-10-15
description: "Turn your regular JavaScript code into a neural net. No training, exact yet also fully differentiable, runnable in a browser without GPU."
tags:
  - "brainspew"
---
## Turn your regular JavaScript code into a neural net.

No training, exact yet also fully differentiable, runnable in a browser without GPU.

`// your code` `const result = a > 4 ? 10 : 12`

`// turns into`

`const above4 = relu(a - 4) - relu(a - 5)` `// relu(x) is Math.max(0, x)`

`const result = above4 * 10 + (1 - above4) * 12`

<svg viewBox="0 0 408 72" role="img" aria-label="The two lines of arithmetic drawn as a circuit. The input a feeds two ReLU gates, relu(a − 4) and relu(a − 5). The second gate's value is subtracted from the first's, which gives above4, and above4 feeds result."><path d="M5 36.25H28.25" fill="none" stroke="currentColor"></path><path d="M28.25 36.25V22.25a8 8 0 0 1 8-8H53" fill="none" stroke="currentColor"></path><path d="M28.25 36.25V50.25a8 8 0 0 0 8 8H53" fill="none" stroke="currentColor"></path><path d="M140 14.25H152a7.5 7.5 0 0 1 7.5 7.5a7.5 7.5 0 0 0 7.5 7.5H195" fill="none" stroke="currentColor"></path><path d="M140 58.25H152a7.5 7.5 0 0 0 7.5-7.5a7.5 7.5 0 0 1 7.5-7.5H195" fill="none" stroke="currentColor"></path><path d="M270 36.25H307" fill="none" stroke="currentColor"></path><rect x="52.5" y="0.5" width="88" height="27" rx="6" fill="none" stroke="currentColor"></rect><rect x="52.5" y="44.5" width="88" height="27" rx="6" fill="none" stroke="currentColor"></rect><rect x="194.5" y="22.5" width="76" height="27" rx="6" fill="none" stroke="currentColor"></rect><rect x="306.5" y="22.5" width="56" height="27" rx="6" fill="none" stroke="currentColor"></rect><circle cx="28.25" cy="36.25" r="3" fill="none" stroke="currentColor"></circle><circle cx="5" cy="36.25" r="4.25" fill="none" stroke="currentColor"></circle><text x="5" y="24">a</text> <text x="96.5" y="18.5">relu(a − 4)</text> <text x="96.5" y="62.5">relu(a − 5)</text> <text x="232.5" y="40.5" fill="currentColor">above4</text> <text x="334.5" y="40.5">result</text> <text x="188" y="24" fill="currentColor">+</text> <text x="188" y="56" fill="currentColor">−</text></svg>

## Demos

[![A screenshot of HandwiredOS: three windows on a desk, with a grid of photos in front.](https://chenglou.me/handwired/demos-handwiredos-zsvtedeh.webp)](https://chenglou.me/handwired/os/)

### Mini OS

A small desktop written in JS, transformed with Handwired. Giant lists, animation, stacking, scrolling, drag, input, pictures, all rendering to regular DOM.

weights

9,909

layers

130

training

0

Open

[View original](https://chenglou.me/handwired/os/)### [Learned gallery](https://chenglou.me/handwired/learned-gallery/)

Unfreeze a compiled program’s weights & train them in *real time*.

### [Search 100,000 JSON documents](https://chenglou.me/handwired/json-search/)

The regex matching, JSON parsing & highlighting are all written in JS, then turned into WebGPU kernels for massive parallelism.