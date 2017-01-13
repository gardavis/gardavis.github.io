---
layout: post
title: "How I solved a Windows Update failure"
date: 2008-08-13 -0800
comments: true
disqus_identifier: 20
tags: [Personal]
---
I installed Windows XP SP2 on a Virtual PC drive and ran Windows Update.
It wanted to immediately update to SP3 but the update failed so I
downloaded SP3 and installed it manually.

Then Windows Update wanted to do 18 more updates but they also failed.
The error was:

> **Problem: A problem on your computer is preventing updates from being downloaded or installed**

There was no error code number. I ran across a
[posting](http://www.technipages.com/error-a-problem-on-your-computer-is-preventing-updates-from-being-downloaded.html)
with a solution. I copied these statements into the clipboard and then
pasted them into a command prompt window. A bunch of "Succeeded" popups
displayed and I OK'd them. I retried the Windows Updated and now it
worked.

    regsvr32 wuapi.dll
    regsvr32 wuaueng1.dll
    regsvr32 wuaueng.dll
    regsvr32 wucltui.dll
    regsvr32 wups2.dll
    regsvr32 wups.dll
    regsvr32 wuweb.dll

Other things to check if this does not work is the Windows Service
("Services" in Administrative Tools) named **Automatic Updates**. Make
sure its Status is *started*and its Starup Type is *automatic*.

Another thing that has been known to cause problems is the IE security
settings. Go to IE's Internet Options-\>Security tab and click the
Trusted Sites icon and Sites button. Uncheck  *Required server*checkbox
and add these sites, one at a time:

    http://\*.microsoft.com
    https://\*.microsoft.com
    http://\*.windowsupdate.com
