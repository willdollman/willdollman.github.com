---
layout: post
title: Temperature logging with Honeywell Total Connect Comfort
---

The latest foray our house has made into thing that are (unnecessarily) connected to the internet, also known as the internet of things, is the [Honeywell Total Connect Comfort][htcc]. 

[htcc]: https://infoeu.mytotalconnectcomfort.com/gb

It's controls your central heating with electronic valves on each radiator that talk wirelessly to a base unit. Each valve has a thermometer, which means that every room can be set to a different temperature, and the heating can be smart about when it turns on by learning how fast rooms warm up.

<div class="img_wrap">
  <img class="img_wide" src="/images/20141002-honeywell_base.jpg">
</div>

The intelligent per-room monitoring is the useful part of the system, and the part that will actually save you money. As it is with the internet of things though, if it can have an iPhone app... well, let's just say that you can change the bathroom temperature while you're sitting on a beach somewhere if you book isn't holding your attention.

Home automation this has an interesting future. Apple is getting big on this kind of thing with HomeKit which will be baked into every iPhone and in the future will allow you to voice control your heating through Siri. It does bring interesting questions about longevity though. How old are the standard non-Internet connected valves on your radiators, and what do you think the lifespan of the Honeywell system is? Even if it lasts a decade, will the servers that allow iPhone control be around then? Will we even have iPhones then?

<div class="img_wrap">
  <img class="img_standard" src="/images/20141002-homekit.png">
</div>

Thoughts on the future of home automation aside, one aspect I find sorely lacking is any kind of logging or historical view. The thought of all that data going to waste while I was in a position to do something about it is near unbearable. Who doesn't want to see the temperature in their house over the last year, or five?

With slightly apprehensive thoughts of taking a soldering iron to the base unit, I took a look at how the iPhone app works. Thankfully it uses a nice JSON API to talk to Honeywell's servers, which makes getting at the data a whole lot easier. There's a slight latency in the API that makes me think it's actually just proxying a connection to the hub in your house. Though I have no evidence to back me up, I think this is pretty likely. It makes the servers dirt cheap to run (and customers will expect them to run indefinitely), and partly explain why there's no historical data.

Given a nice API to talk to, I wrote a Perl wrapper to get temperatures from the API. Once in posession of the numbers, the next part is graphing them. I used Cacti for this and I've included a script that outputs in a Cacti-readable format, and several templates. [Download the code!](https://github.com/willdollman/perl-total-connect-comfort)

<div class="img_wrap">
  <img class="img_wide" src="/images/20141002-script_temperature.png">
  <div class="img_text">The output of one of the included test scripts</div>
</div>

As Cacti isn't very beginner-friendly, I've [written a setup guide](/2014/10/03/totalconnectcomfort-and-cacti-setup-guide/) that should end up getting you some awesome graphs like these:

<div class="img_wrap">
  <img class="img_standard" src="/images/20141002-cacti_all_graphs.png">
</div>

<div style="font-size: 13px; margin-top: 20px;">HomeKit logo &copy; Apple Inc.</div>
