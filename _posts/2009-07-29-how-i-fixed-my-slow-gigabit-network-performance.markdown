---
layout: post
title: "How I fixed my slow Gigabit network performance"
date: 2009-07-29 -0800
comments: true
disqus_identifier: 15
tags: [Personal]
---
My connection used to be fast when I first installed my TRENDnet TEW
672GR Wireless “N” Gigabit router. I have three computers that are
connected using a wired GB connection. Things just seemed real slow when
sending or receiving large files between the home server and my (or my
wife’s) PC. For example, shutting down MS Money writes a backup to the
server and this took several minutes. Copying a gigabyte .avi movie file
would take a long time and copying a DVD would take hours.

So I needed some metrics to get a baseline. I decided on
[Jperf](http://code.google.com/p/xjperf/ "Jperf project at code.google.com")
([tutorial](http://openmaniak.com/ "OpenManiak Tutorial")) which is a
graphical front-end to Iperf. With this tool, you run the client at one
computer and the server on the other. The program easily connects
between them and sends messages back and forth for several seconds and
displays a graph of the performance.

[![image](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_thumb_6.png "image")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_14.png){: .left}
The graph shown on the left is the performance I was seeing which was about 376KB/sec.

Another tool I used to get some more data is
[WireShark](http://www.wireshark.org/). This is a complex tool to
capture low-level packet data on the network. I viewed some tutorials on
YouTube and captured a few seconds worth of data (that’s actually a lot
of capture). It did confirm that gigabit throughput was happening by
looking at the time between frames, but there were areas of
re-transmissions due to failed acknowledgements, collisions or
something. It takes a lot more networking experience to analyze these
captures than I have or want to learn at this point.

So the first thing I tried was to replace the cat5 homemade cables with
cat6 manufactured cables from [Monoprice](http://www.monoprice.com/), a
great place to get ~~cheap~~ inexpensive cables. This did not improve
things at all.

[![image](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_thumb_2.png "image")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_6.png){: .right}

I next tried a 7.25 GB DVD transfer and it would have completed in about
4 hours if I let it finish (see screen shot on right). The transfer rate
is 556 KB/sec, a bit faster than the above graph. It also shows the
network utilization at a fraction of a percent. The little graph at the
bottom is a nice little utility called
[DUMeter](http://www.dumeter.com/), nice to keep at the bottom of your
desktop.

My next test was to connect my PC and the Server with a 25’ cat6 cable
port to port, bypassing the router altogether. This requires a crossover
connection so the cable wire pairs are correctly flipped (normally done
when connecting via a hub, router or switch. There’s no DHCP to assign
IPs when connected this way so I had to assign static IPs to each site
(192.168.1.1 and .2).

The throughput jumped to what it should be when using Jperf. Now,
instead of 4 hours, the file transfer would take about 7 minutes.

[![image](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_thumb_3.png "image")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_8.png){: .left}

The transfer rate is about 23MB/sec and net utilization is 25%. That’s
about 50 times faster.

So with the TRENDnet in the middle, the transfer is slow and without it,
the transfer is fast. That tells me the router is the problem and that
something is seriously wrong with the Gigabit part of it (the wireless
part is fine).

I looked at the TRENDnet router configuration settings but there are
very few related to the wired LAN and nothing performance-related. Most
settings are for wireless. I checked the TRENDnet knowledgebase and
forums and found nothing obvious. I started a trouble-ticket with
TRENDnet and sent them a screen capture of the performance issue.

I continued thinking about the difference between the two tests and
decided to try removing all the attached cables from the router to make
sure none of
the
[![image](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_thumb_7.png "image")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIfixedmyslowGigabitconnectionthroughp_125A5/image_16.png){: .right}
other devices was causing the problem. There are four ports on the
router: 1) Server, 2) my PC, 3) wife’s PC and 4) connection to a 8-port
cheapie switch (Zonet). Disconnecting one at a time quickly showed that
the Zonet switch was the culprit. With it out of the mix, I had the fast
network with the TRENDnet. Even if no connections were in any of the
Zonet ports (the Tivos, etc.), it caused the slowness. So I told
TRENDnet support that they could close the ticket, it was not their
device’s fault.

This is the final Jperf graph for the fast network at 36372KB/sec. If
the above graph was included in this graph, it would just be a straight
line at hugging the bottom around 0.

***Update**: I tried a different switch (a TRENDnet 10/100 Wireless
4-port router, actually) and it had the same effect as the Zonet switch
so the problem is not fixed as I thought. I will get a new Gigabit
switch which should work, else I am back to blaming the TRENDnet Gig
router.*
