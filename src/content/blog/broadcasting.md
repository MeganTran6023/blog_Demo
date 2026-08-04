---
title: 'Screen Mirroring Issues'
description: 'Why My Game Did Not Process Hand Motions when Broadcasted to TV Screens'
pubDate: 'Aug 3 2026'
heroImage: ''
category: 'Programming'
---

## The Issue
One of the researchers I collaborated with on a project was demoing out my game when he wanted to broadcast my computer screen to his TV. I found that to be a great idea as the larger display would enhance the playing experience, like when one watches a movie on the grand size screen in a theater. It was astonishing seeing my demo on the TV screen, but not when the camera could not pick up my colleague's hand-motions.

## Why I Think This Happened 
First, let me explain this using every day scenarios. 

### Non - Technical Explanation
Imagine a professor who has a mountain of tasks to finish, such as research projects, teaching, and writing grants. Suddenly, they get a brand-new interruption, like needing to answer an urgent student email. However, they are already on a strict deadline to complete a major grant due very soon. Because they are completely overworked, they can only handle so much at once and something has to give.

### Technical Explanation
The program running my game operates on a single execution thread. On that exact same thread, the computer is simultaneously trying to support the screen mirroring component being implemented. This heavy lifting steals vital CPU cycles away from my application. As a result, the screen mirroring to the TV works, but the initialization of the camera used to process hand motions fails.