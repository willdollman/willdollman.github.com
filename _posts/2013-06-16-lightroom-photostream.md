---
layout: post
title: Using Lightroom with Apple's Photo Stream
---

Photo Stream is a neat iOS feature. Every photo you take with your phone just appears on your computer.

You can also use it to get photos from an actual camera onto your devices - it's handy for flicking through pictures on an iPhone, and photos look really awesome on an iPad with a retina display. If you use iPhoto to manage your photos, this all happens automatically - but what about if you use Lightroom? Here's how I do it.

Windows
-------

You'll need to install the [iCloud Control Panel][icloud-windows]. Once you do, you'll have a 'Photo Stream' folder in My Photos, and anything that gets dropped in there is uploaded.
[icloud-windows]: http://www.apple.com/uk/icloud/setup/pc.html

All you need to do in Lightroom is create an export preset that exports your photos as JPGs to this folder, and they'll show up on your other devices. Simple!

OS X
----

Not quite so simple.

As with Windows, we want an export preset in Lightroom that exports JPGs to a folder - this time though, we don't care where it puts then.
<a href="/images/2013-06-16-lightroom_export_presets.png"><img alt="Lightroom Export Presets" src="/images/2013-06-16-lightroom_export_presets.png" style="display:block; margin-left: auto; margin-right:auto; margin-top: 10px; margin-bottom: 10px;" width="600"></a>

Lightroom lets you run a program after the export, in the "Post-Processing" step. To get our pictures into Photo Stream, I use an Automator script. Open Automator, and enter the following steps:
<a href="/images/2013-06-16-folder_to_photostream.png"><img alt="Folder to Photo Stream Automator script" src="/images/2013-06-16-folder_to_photostream.png" style="display:block; margin-left: auto; margin-right:auto; margin-top: 20px; margin-bottom: 10px;" width="500"></a>
This script will import your photos into iPhoto, where they'll be uploaded to your Photo Stream and appear on your devices. The Photo Stream agent uploads even while iPhoto is closed, so there's no need to keep it open.

You can also find the source for the Automator script [on my github page][github-applescripts].
[github-applescripts]: https://github.com/willdollman/applescripts
