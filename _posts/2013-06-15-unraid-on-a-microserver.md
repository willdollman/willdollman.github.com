---
layout: post
title: unRAID on a Microserver
---

I have an HP N40L MicroServer, and for a while I've been looking at ways of turning it into a network storage device with some disk redundancy. There are a couple of solutions for this which are usually suggested:

- **RAID 5** isn't a good fit for home use. As well as requiring additional hardware, if something goes wrong the chance of *losing everything* is too high for my liking.
- **ZFS** is promising, but its lack of Linux support means the best way to get it is FreeNAS - it's good, but I couldn't get Wake on LAN working, ZFS's RAM requirements are high, and I'd prefer to stick with something Linux-flavoured.

A third is [unRAID][unRAID]. You have a bunch of disks, and use the largest as a parity disk. Lose one drive and you can rebuild; lose two and you lose the data on both of them, but **not** everything else as well. There are some disadvantages to its high level approach (rather than at the hardware or filesystem level), but the tradeoffs suit what I want. However, it does cost money to use with more than three disks, and part of it isn't open source which might put some off. 

[unRAID]: http://lime-technology.com/


I don't want to regurgitate the [unRAID wiki] [unraid-wiki] in this post - the documentation is good when you know what you're looking for, but I found it to be lacking in a *sensible defaults and useful things to install* section. That's what I hope this is, because once you start using unRAID you'll notice a couple immediate of problems.
- The stock web UI is ugly
- Shutting down requires you to run a full parity-sync if you don't stop the array first
- Adding disk to the array takes hours
- Installing packages is a pain
- And if you're using a MicroServer... wake on LAN doesn't work

[unraid-wiki]: http://lime-technology.com/wiki/index.php/UnRAID_Wiki "unRAID wiki"

The web UI problem is pretty easy to solve with a plugin called [SimpleFeatures] [simplefeatures-gcode]. 
It changes the stock interface into this, as well as adding a handful of other features which integrate well into the web interface. 

<div class="img_wrap">
  <img class="img_standard" src="/images/2013-06-15-unraid_simplefeatures.png"/>
</div>

[simplefeatures-gcode]: https://code.google.com/p/unraid-simplefeatures/

Requiring a parity check after an abrupt power off is one of the high-level implementation disadvantages I mentioned. The data disks are formatted as ReiserFS which is a [journaled file system] [journal-wiki], but the parity drive is literally just an XOR of all the bits of the other drives. No filesystem, just bits. So if you just turn the power off, the parity disk may be inconsistent with the other disks and the only real solution is to scrub over all the disks and check that it's not. 
Instead, you should stop the array before shutting down - luckily, there's a nice [powerdown script][powerdown-script] that does this for you.

[journal-wiki]: http://en.wikipedia.org/wiki/Journaling_file_system
[powerdown-script]: https://code.google.com/p/unraid-powercontrol/

Wake on LAN with the N40L is a pain and doesn't work properly. The way to get it working with Linux is to take the network interface down before you switch it off, which keeps the interface listening for magic packets when the server is off. I couldn't get it working in the 4.x releases, but the latest 5.0-rc12a release work great. Add the line */sbin/ifconfig eth0 down* to the powerdown script, just before the */sbin/shutdown* line.

When you add a disk to the array, it first writes zeroes to it and then formats it. If you're adding a 2TB drive, that's over 5 hours during which the array is inaccessible. Unacceptable! What we need is a script that does that in the background. Again, someone's been there already and created a [preclear script][preclear-script]. It takes longer to run than the standard preparation as it does a full read, write and then reads again - I found it took around 5 hours per terabyte. It also does SMART checking before and after, so it's a decent way to burn in new drives.

[preclear-script]: http://lime-technology.com/forum/index.php?topic=2817.0

Packages. unRAID is a stripped down Slackware distro that fits into 128MB, so understandably it's a bit light on packages. You can do it yourself, but [unRAID unMenu][unraid-unmenu] provides a quick and dirty web interface to install common packages with unRAID customisations. Customisations? This is a live OS remember, so everything apart from **/boot** gets thrown away when the power goes down. For example, if you install sshd through unMenu, it also sets up a script to copy /etc/ssh/ back into place on each boot. Personally I can't get by without SSH and Vim. 

[unraid-unmenu]: https://code.google.com/p/unraid-unmenu/

While it took a bit of tweaking to get it set up to a state I like, unRAID feels pretty solid. If you're looking for a network storage solution that just uses a computer rather than a dedicated device, it's worth a look.
