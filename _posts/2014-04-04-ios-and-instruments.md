---
layout: post
title: Looking at iOS's background processes
---
Visibility into iOS's background activity
Looking at iOS's background processes

One part of Android that I've always thought is missing from iOS is good battery monitoring. Yeah, partly I just like knowing what's going on, but it also helps give you some visibility into battery problems. Phones have small batteries, so they get away with an all-day battery life because most of the time they're idle and almost everything is off. The bad side is unlike a laptop, a wedged process running in the background means serious battery drain problems.

<div class="img_wrap">
  <img class="img_wide" style="height: 400px;" src="/images/20140404-ios_battery.png">
  <img class="img_wide" style="height: 400px;" src="/images/20140404-android_battery.png">
  <div class="img_text">To say Android is better equipped here would be an understatement</div>
</div>

This problem is dodged by the system being agressive about what can run in the background, and when. But, it can still surprise you. It used to be that if you installed the Skype app, it sat in the background and chewed on your battery[^skype-drain]. With each release, app have more licence to do things in the background.

It's not very well known that, without jailbreaking, you can get a better look at what's running on your phone, and help diagnose battery issues, or splat offending apps and services. This works with Instruments. Prerequisites are Xcode (and a Mac), and your device being connected with a cable. You also need to set up your phone to work with Instruments, which you do just by opening Xcode with your phone connected[^instruments-warning].

In Instruments select iOS in the left panel, and the Energy Diagnostics template. Hit record to see what's happening on your device. In addition to the standard tools - CPU usage, Network activity - you can see when apps enter and exit running states. For example, Weather wakes up for a few seconds every time you unlock the phone. App actity is shown via the flags at the top of the timeline.

<div class="img_wrap">
  <img class="img_wide" style="height: 600px" src="/images/20140404-instruments_record.png">
</div>

Perhaps more usefully that just showing data when you're connected to your laptop, you can collect diagnostics while using a phone, and review them in Instruments. Once you've set your phone up to work with Instruments, you gain a Developer menu item in Settings. Head over there in Logging, then start recording. To view the data, plug your phone in then from Instruments go to File > Import Logged Data from Device. 

[^skype-drain]: This was due to Skype's decentralised architecture. See [this email written by Skype's Princial Architect](http://markmail.org/message/exc3srjkx3uu66bz?q=android) and search for "hand warmer".

[^instruments-warning]: If you're seeing this warning in Instruments, this is probably the issue. The Developer-ness persists until you restart your phone. <img style="margin-left: 10px;" src="/images/20140404-instruments_warning.png">