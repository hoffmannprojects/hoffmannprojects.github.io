---
#layout: # should be set by default
title: "Space Bowling"
field: "PROGRAMMING (Unity, C#)"
featured-img: bowlmaster
permalink: /:collection/bowlmaster/
---
![alt text](/assets/img/portfolio/bowlmaster.jpg "Logo Title Text 1")

3D bowling in space. Personal project.

## Details:
- Implemented architecture, fully compliant with official ten-pin bowling rules, using test-driven development (TDD) with unity testing tools:
  - GameManager class holds game state. 
  - GameManager requests next appropriate action from static action system class.
  - GameManager requests current score from static scoring system class.
  - Realtime scoring system takes possible bonuses from future attempts into account.
- Animations with sub-state machines.
- Manipulation of Unity's physics engine.
- Touch control system with swipe input for launching the ball.
- Camera chases the ball until in front of the pins.

- Written in C#
- Engine: Unity
- Platform: PC/Mac, Android/iOS