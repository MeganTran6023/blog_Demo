---
title: 'Messing around with Docker'
description: 'My notes from experimenting with Docker for the first time.'
pubDate: 'Sep 4 2026'
category: 'Programming'
---

## Why Docker?

I wanted to find a way to containerize my application so users intending to play this at home or in musical lessons can easily do so. 


## A Delayed Demo

I didn't think my changes from when I was playing around with Docker in regards to my game would affect the demo script I prepared. Suddenly, the camera screen would not appear along with the game application screen!

## What happened

When I was trying to get my camera to work on docker, I had designated the Linux operating system to use the camera instead of my regular Windows operating system. My python script uses windows to then connect to the camera while docker uses Linux.

The command used to get my camera to work for docker was (more specifically, with X410):

```usbipd bind --busid 1-6 ```

To break it down: 

```usbipd```: Think of this as the librarian who manages which computer has access to each USB device.

```unbind```: This is the instruction telling the librarian to check the USB device to Linux so it can use it.

```--busid 1-6```: This is the device's library barcode/ID number. It tells the librarian exactly which USB device to unbind.

## The Solution

I felt bad that my demo wasn't working as planned, especially since the professor and I rescheduled a couple of times. But, its not a real demo if something doesn't mess up. Luckily, it resolves... so far.

To fix this, I used

```usbipd unbind --busid 1-6 ```

To break it down: 

```usbipd```: Think of this as the librarian who manages which computer has access to each USB device.

```unbind```: This is the instruction telling the librarian to check the USB device back out of Linux, so Windows can use it again.

```--busid 1-6```: This is the device's library barcode/ID number. It tells the librarian exactly which USB device to unbind.
