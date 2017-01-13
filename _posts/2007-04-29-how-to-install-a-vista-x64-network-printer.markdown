---
layout: post
title: "How to install a Vista x64 network printer..."
date: 2007-04-29 -0800
comments: true
disqus_identifier: 40
tags: [Personal]
---
I have an Epson printer on my Windows 2003 Server. I want to use that
printer as a network printer on my x64 Vista PC.

I attempt to add the network printer to my Vista and get this error:

**"The server for the 'EPSON Sytlus COLOR 880' printer does not have the
correct printer driver installed...."**

The solution is to install the driver locally as the first step and
connect to the remote network port as the second step.

In my case, the Epson is an *in-the-box*driver. The actual printer does
not have to be plugged into the local PC. Next, go into the new printer
driver's properties; Ports tab. Click Add Port. Select Local Port and
click New Port. Enter the UNC address of the remote printer as the Port
Name (like [\\\\server\\Epson880](file://\\server\Epson880)).

 

Refs:

[http://forums.microsoft.com/TechNet/ShowPost.aspx?PostID=1135306&SiteID=17](http://forums.microsoft.com/TechNet/ShowPost.aspx?PostID=1135306&SiteID=17)

[http://www.kevinyank.com/blog/archives/connect-to-a-network-printer-on-a-windows-xp-server-in-windows-vista](http://www.kevinyank.com/blog/archives/connect-to-a-network-printer-on-a-windows-xp-server-in-windows-vista "http://www.kevinyank.com/blog/archives/connect-to-a-network-printer-on-a-windows-xp-server-in-windows-vista")
