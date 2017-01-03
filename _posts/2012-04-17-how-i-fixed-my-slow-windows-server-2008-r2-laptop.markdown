---
layout: post
title: "How I fixed my slow Windows Server 2008 R2 laptop performance"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 13
tags: [Personal]
---
Yesterday, my Windows Server 2008 R2 laptop was running extremely slow.
Eventually, I figured out it was all video related – resizing windows,
Snagit, even Outlook opening email. The Aero theme was enabled.

 

A Google search helped pinpoint it to the Hyper-V role I had recently
added. The combination of Hyper-V (the virtualizaton software for Server
2008 R2) and Aero is the problem.

 

Switching off the Aero theme helped a lot but removing the Hyper-V role
is the real answer for now.

 

I wanted Hyper-V to play around with a [virtual
image](http://www.microsoft.com/downloads/details.aspx?FamilyID=27d91e63-e33b-4cef-a331-f20d343da9de&displaylang=en)
of Win Server +  Visual Studio 2010beta.

 

Links about this problem:

-   [Connect problem
    report](https://connect.microsoft.com/WindowsServerFeedback/feedback/details/356939/hyper-v-made-the-machine-unusable-super-slow?wa=wsignin1.0)
-   [Wikipedia about Hyper-V](http://en.wikipedia.org/wiki/Hyper-V)
-   [Virtual PC Guy's
    Blog](http://blogs.msdn.com/virtual_pc_guy/archive/2009/11/16/understanding-high-end-video-performance-issues-with-hyper-v.aspx)
    posting about problem details


