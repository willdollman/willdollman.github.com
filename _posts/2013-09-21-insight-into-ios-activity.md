---
layout: post
title: Insight into iOS activity
---

This is following the "introduce problem and background", introduce solution, show how to use solution. 

Ive be always been quite curious about what goes on in the depths of iOS. This is mostly just a desire to know how things work, I remember during early jailbreaking catching a glimpse of the folder structure and seeing how similar it was to the mac, and being able to ssh in and run common utilities like top. Realising that under the glossy touchscreen it's running unix. 
One part of android I've always been jealous of is the battery section. It shows you a graph of charge over time, and indications of which apps are response for how much battery use.  
 
I've always been quite curious about what goes on in the depths of iOS. Part of this is just a desire to know what my things are doing, and part of it is more practical. Phones have small batteries, and can get away with all-day battery lives because most of the time they're idle. The flip side is that unlike a laptop, a process running continuously in the background can mean serious battery drain problems.

As you know, Apple gets around this by not allowing stuff to run in the background. It's a pretty good solution that's served pretty well, but that does t stop the fact that people do have problems with battery drain. Yeah, sometimes it's hardware, but the software side can do a surprising number of things to... surprise you. If you install skype, and sign in, it sits in the background and chews through your battery. Forum posts of iCloud stuck syncing a corrupted contact or bookmark. IOS 7 now lets apps wake up pretty much when they want, with a lot more battery-draining potential.  With so little visibility into the device, it's easy to resort to voodoo solutions: three hard resets in a row always do it for me. Try disabling location services. Turn Siri off. Reset the network settings. 

Instruments to the rescue. You can connect your phone to your laptop (macs only I'm afraid) and run instruments, a set of profiling tools that ship with Xcode. These give you a lot of visibility into what's going on with the phone - think activity monitor and then some. Once you've connected your phone to a mac and "provisioned" it, you have insight into all the expected CPU, memory and network usage, but also currently running apps including those running in the background. 

Once a device is provisioned (footnote with instructions) you can also enable energy logging on it in the developer menu of settings (screenshot). This means the phone records things like CPU usage and open applications while not being tethered to a laptop, which you can view upon connecting back to your computer. (Photo of import menu item?) It lets you see what your phone does during general day to day usage. Weather, for example, wakes up for a few seconds also every time you unlock your phone. You can see other applications holding on to the CPU after you click the home button to do some final frantic processing before they go back to sleep. 

In a future post I'll talk about some unexpected app that wake up in the background. 
