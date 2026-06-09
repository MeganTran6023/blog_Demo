---
title: 'Object Oriented Programming - Abstract Base Classes'
description: 'My Explanation of how I applied Abstract Base Classes when programming my characters'
pubDate: 'Jun 9 2026'
heroImage: '../../assets/post_3_blog.png'
category: 'Programming'
---


## Example: Character_ABC.py

Here is my writeup of how I implemented the use of Abstract Base Classes when creating the Character classes and respective subclasses.

## Abstract Base Class (ABC)
These are the general attributes I want anything that uses this class to have.

**Purpose:** Reusability of methods in code

### Methods included-
* **Positioning:** This places a character object at some location on the pygame screen.
* **Loading single image/ multiple images (if a sprite):** All of the characters are either single images or a sprite (which is made up of multiple images).

### Methods I should include-
*Reason: All of the subclasses use these common methods that I chose not to add to the ABC for some reason.*

* **Update frames:** This iterates through each frame at some rate – for sprites
* **Idle:** Character’s resting position
* **Draw:** this outputs the frame(s) on the pygame screen

## Subclasses
These classes inherits methods in the Character ABC. Each of the specific character subclasses also have their own methods and modified values for the methods inherited from the ABC.

Lets use the subclass for the orange character as an example.

### Example: Orange Character
To show that I inherit all the methods in the ABC, I use:

```python
super().__init__()
```

But in this subclass, I also add other unique methods that other characters may not use, such as a method for the orange character to attack right (`battle_ground_attack`).