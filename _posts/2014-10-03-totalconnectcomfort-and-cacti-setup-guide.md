---
layout: post
title: Setup guide - Honeywell Total Connect Comfort + Cacti
---

<div class="img_wrap">
  <img class="img_wide" src="/images/20141003-wills_room_graph.png">
</div>

<center style="margin-top: 15px;">
    <a style="font-size: 26px;" href="https://github.com/willdollman/perl-total-connect-comfort">Download all the scripts and templates you need</a>
</center>

When you're using templates, Cacti is actually quite easy to configure. If you get into trouble you may find Cacti's documentation on [setting up data input][data-input-help] helpful.

[data-input-help]: http://docs.cacti.net/manual:087:3a_advanced_topics.1_data_input_methods

If you can, install Cacti via your distribution's package manager and it'll do some of the setup for you. Follow the [Cacti docs](http://www.cacti.net/downloads/docs/html/unix_configure_cacti.html) to get it set up the rest of the way. You may also need to install `mysql-server` separately.

Then we need to set up the data grabbing script by copying it into place:

    mkdir /var/lib/cacti/scripts/TotalConnectComfort
    cp -r Device/ /var/lib/cacti/scripts/TotalConnectComfort
    cp -r cacti-scripts/temperature.pl /var/lib/cacti/scripts/TotalConnectComfort
    
    Note - the directories will be different in other OSes - on Ubuntu it'll be something along the lines of /var/lib/cacti/something/scripts

If you're copying the `Device::TotalConnectComfort` module from source (rather than installing from CPAN), you'll also need to install its dependencies. Install gcc and openssl-devel/libssl-dev using your package manager, then install cpanm and necessary modules with:

    curl -L http://cpanmin.us | perl - --sudo App::cpanminus
    cpanm JSON JSON::XS LWP::UserAgent LWP::Protocol::https

Ok, we've done all the grunt work. Now we need to make the pretty graphs. Import all four templates into Cacti via "Import Templates" (make sure you choose to "Use custom RRA settings from the template").
You'll want to customise the Data Input Method and Data Template that they match the room names in your home.

Then finally, you can go to New Graphs and start setting up graphs. For that graphs that are per-room, you should edit them by going to Graph Management so that the data sources match the rooms.

<div class="img_wrap">
  <img class="img_standard" src="/images/20141003-cacti_change_data_source.png">
</div>

After a few minutes of gather data, you should have some cool graphs!

<div class="img_wrap">
  <img class="img_standard" src="/images/20141003-cacti_all_graphs.png">
</div>

You also get a neat historical view.

<div class="img_wrap">
  <img class="img_standard" src="/images/20141003-cacti_historical.png">
  <div class="img_text">Mind the gap - we had a few network issues!</div>
 
</div>
