---
layout: post
title: "How I Upgraded my HD Tivo from 20 to 98 hours"
date: 2007-08-18 -0800
comments: true
disqus_identifier: 26
tags: [Personal]
---
I bought a new HD Tivo (not to be confused with the older Series 3 Tivo
though they are similar). I contacted Comcast to get the cable cards
installed (it took 3 visits). The cable cards plug into the HD Tivo and
eliminate the need to have a separate cable box.

The next step is to increase the hard drive capacity to hold more
recordings. The HD Tivo comes with a 160GB drive and this project
replaced it with a new 750GB drive to increase from 20 HD hours of
recordings to 98.

My upgrade today went smoothly. I started with WinMFS 1.3 beta build 3
and used it to backup my original Tivo drive. The result was a 441MB
(truncated) backup file and it took under 5 minutes. The backup is
necessary in case the hard drive craps out and needs to be replaced. It
contains not only the shows but the Tivo Linux operating system, season
passes, etc.

My PC is running Vista Ultimate 64 and I only have one free sata power
connector (I need to get a power adapter/splitter). I want to save the
existing recordings and without the extra power connector, I could not
use WinMFS at the same time as running Vista since my Vista boot is on
my other sata drive.

So the solution was to use the MFS boot which I put onto a bootable USB
drive (see
[http://mfslive.org/forums/viewtopic.php?t=228](http://mfslive.org/forums/viewtopic.php?t=228)).

The MFS ICG helped figure out the command to execute (see
[http://mfslive.org/cgen.php](http://mfslive.org/cgen.php)).

I disconnected my Vista drive and had both the new (WD7500AAKS - \$180
from Newegg) and Tivo drives connected. Booted up the USB Linux. To
verify which drive was /sda and /sdb, use Shift/PageUp to page back
through the boot up messages. It turned out to match the ICG command
line.

Next, I ran the command line (used 256MB swap) which for me transferred
about 38GB in about 15 minutes.

![](/images/blogs_webguild_com/gary/CommandOutput.png)

Next, I disconnected the old Tivo drive and booted up the Hitachi
Feature Tool (bootable CD - see
[http://www.hitachigst.com/hdd/support/download.htm](http://www.hitachigst.com/hdd/support/download.htm))
to turn on the Acoustic Management for the new WD drive. I used the Test
command to see how much more quiet it is but I did not notice much of a
difference - it was virtually silent in both cases.

I put the new drive into the Tivo and powered it up. It took about 5
minutes, much of which displayed a black TV screen. I got my b2 software
upgrade last night and the reboot from it earlier in the morning also
took the long reboot so I was not too concerned. This was my first
reboot of the Tivo since its initial powerup (none needed for cable card
installs).

So now I have about 5x the space as before.

![](/images/blogs_webguild_com/gary/SysInfo.png)

Thanks for the MFS tools that made this so easy.

Gary Davis

[Gary's Tivo Site](http://www.webguild.com/Tivo)

*Update:*

\> Next, I disconnected the old Tivo drive and booted up the Hitachi
Feature 
 Tool 
 
 Actually, that step was unnecessary since there is a tool on the 
 MFSLive Linux that will set the acoustic mode (AMM):
 
 hdparm -M 128 -K 1 
 /dev/sda 
 
 For reference, see: 
 http://www.mfslive.org/softwareguidep6.htm\#aam

