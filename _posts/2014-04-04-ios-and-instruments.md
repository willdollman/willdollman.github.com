---
layout: post
title: iOS - what happens in the background?
---

One part of Android that I've always thought is missing from iOS is good battery monitoring. Yeah, partly I just like knowing what's going on, but it also gives you some visibility into battery problems. Phones have small batteries, so they get away with an all-day battery life because most of the time they're idle and almost everything is off. The flip side is that unlike a laptop, a wedged process running in the background means serious battery drain problems.

<div class="img_wrap">
  <img class="img_high" src="/images/20140404-ios_battery.png">
  <img class="img_high" src="/images/20140404-android_battery.png">
  <div class="img_text">To say Android is better equipped here would be an understatement</div>
</div>

This problem is dodged by the system being agressive about what can run in the background, and when. But, it can still surprise you - it used to be that if you installed the Skype app, it sat in the background and chewed on your battery [^skype-drain]. Not to mention that with each iOS release, apps have more licence to run in the background.

What doesn't seem to be well known is that there's a way to do this without jailbreaking, using [Instruments][instruments-wiki]. Prerequisites are Xcode (and a Mac). You need to connect your device with a cable then set it up to work with Instruments, which you do just by opening Xcode with your phone connected [^instruments-warning].

[instruments-wiki]: http://en.wikipedia.org/wiki/Instruments_(application)

In Instruments select iOS in the left panel, and the Energy Diagnostics template. To see what's happening on your phone, hit record. In addition to the standard tools - CPU usage, Network activity - you can see when apps enter and exit running states via the flags at the top of the timeline. For example, Weather wakes up for a few seconds every time you unlock the phone.

<div class="img_wrap">
  <img class="img_wide dropshadow" style="height: 600px" src="/images/20140404-instruments_record.png">
</div>

More useful than just showing data when you're connected to your laptop is that you can record diagnostics, and later review them in Instruments. Setting your phone up to work with Instruments adds a Developer menu item in Settings. To view the data, reconnect your phone then go to File > Import Logged Data from Device in Instruments.

<div class="img_wrap">
  <img class="img_high" src="/images/20140404-ios_developer.png">
  <img class="img_high" src="/images/20140404-ios_record.png">
</div>

[^skype-drain]: This was due to Skype's decentralised architecture. See [this email written by Skype's Princial Architect](http://markmail.org/message/exc3srjkx3uu66bz?q=android) and search for "hand warmer".

[^instruments-warning]: If you're seeing this warning in Instruments, that's probably the issue. The Developer-ness persists until you restart your phone. <br><img class="img_halfsize" style="margin-left: 5px;" src="/images/20140404-instruments_warning.png">
