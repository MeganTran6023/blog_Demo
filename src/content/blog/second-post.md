---
title: 'Bow Hand Mechanics'
description: 'The Process of Programming Bowing Hand Motions'
pubDate: 'May 29 2026'
heroImage: '../../assets/blog_post2.png'
category: 'Programming'
---

I thought this would be a straightforward process. Only two simple motions:

* Bowing right means moving your hand to the right (right swipe). This triggers the orange character to attack right.

* Raising your fingers means curling up your fingers. Orange character jumps.

My computer told me otherwise.

## Version 1

Implementation: 

1) Core communication protocol

(insert about sending byte messages here)

2) Allow user to curl up fingers and swipe hand right anywhere on the camera screen

From this, I tracked the fingertips and their position in space by marking them with blue dots. If at least one of those dots moved from one starting x- position to a differenet x-position in a line under a certain duration, it is considered as a right-swipe. 

Same pattern applied for the jump. If at least one of those dots moved from one lower starting y- position to a different, higher y-position in a line under a certain duration, it is considered as a jump. 

Problem: Game Engine confused between character actions.

#### a) Lack fo Boundaries in Physical Space

The python script in charge to identifying whether a hand motion was a right swipe or if the fingers were curling up could not discern between the two. This results in a logic error.

#### b) No Cool-Down for Jumps

If a jump is triggered, the opencv server I made in the python script processess other inputs after the jump. What this means is that while the character is mid-jump, it can also trigger the character to do additional actions such as attack in mid air which is not what it should do. 


## Version 2

Feature: **The Jump Line** and **Jump Timer**

Improvement: Prevent logic errors between "jump" and "right attack" from hand motions. Now this allows each command to be distinct from each other.

#### a) Jump Line

(insert image)

"Jump" - triggered by raise fingertips starting below the line to some spot above the line.

"Right Attack" - triggered by moving fingertips to the right below the line under a certain amount of time. This timing prevents unintentional hand movements to trigger a "right attack".
 
Problem: Users were not properly positioning their hands as intended.

The game's functionality made complete sense to me since I am the one making it. But when having other people try out a demo version of my game, their interpretations of "jump" and "Right Attack" varied. The main theme was that everyone moved their hand in various (and sometimes bizarre) ways. This made me realize that I had to be strict about defining how each fingertip should be positioned during different stages of the hand movement for the respective character action.

#### b) Jump timer

(GIF video)

After triggering the finger motions for "jump", a red transparent layer shows below the jump line for some period of time before disappearing. This prevents multiple hand motions from triggering multiple actions concurrently to reuslt in a buggy output in the character's motions. No problems from adding this feature observed.

## Version 3 (Current)

Feature: **Multiple Mediapipe landmark checks**

Improvement: Safeguards pertaining to finger positioning to ensure proper bow hand mechanics
