---
layout: post
title: "How I Fixed the Windows Sidebar Netflix Gadget"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 28
tags: [Personal]
---
The [**Netflix Now Showing**
gadget](http://gallery.live.com/liveItemDetail.aspx?li=83d48ed3-1307-46cf-8d6d-60190f5caeae&bt=1&pl=1)
for the Windows Vista Sidebar is a useful little thing to display the
DVDs you currently have checked out as well as a few of the upcoming
DVDs you are to receive from the top of your Netflix queue.

Sometimes, when my Windows Vista 64 Ultimate starts up and I log on, an
error message pops up three times indicating Line 91: Error: 'xmlathome'
is undefined:

![NetflixGadgetError](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIFixedtheWindowsSidebarNetflixGadget_99C7/NetflixGadgetError_3.jpg)

A search of Google showed several people had this error (which was an
annoyance but did not prevent the gadget from working). I went to the
[author's site](http://www.scottsloane.com/) but there was no mention of
the gadget there.

So, I decided to click Yes to debug using Visual Studio. The line in
error was highlighted:

     var athomestate = xmlathome.readyState;

The debugger showed that xmlathome was truly undefined (null) so the
attempt to reference readyState caused the error.

Looking at the code showed that a *race condition* existed where the
CheckState function could be called before the xmlathome variable was
initialized. The fix is to make sure the variable is initialized before
the function could ever be called. The line to initialize the xmlathome
variable just needs to be moved up in the code a few lines (from line 77
to line 71 as shown):

![NetflixGadgetFix](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIFixedtheWindowsSidebarNetflixGadget_99C7/NetflixGadgetFix_3.jpg)

The file that needs to be fixed is netflix.js in this folder (copy/paste
this into Windows Explorer):

     %UserProfile%\\AppData\\Local\\Microsoft\\Windows
Sidebar\\Gadgets\\Netflix[1].gadget\
