---
layout: post
title: "How I Solved the VS2010 Error: &quot;Unable to start debugging&hellip;&quot;"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 11
tags: [Programming]
---
I received error message "Unable to start debugging on the web server"
in Visual Studio 2010. I clicked the Help button and followed the
related suggestions without success. 
 
 This happens with a newly created local ASP.Net project when modified
to use IIS instead of Cassini (which works for debugging). It
immediately pops up the error. Nothing shows up in the Event Viewer.
This also happens with VS2008. Debugging used to work. 
 
 I am able to attach to the w3wp process to debug. It works but is not
as convenient as F5.

I posted the problem at
[Experts-Exchange](http://www.experts-exchange.com/Web_Development/Software/Q_26204688.html)
and
[StackOverflow](http://stackoverflow.com/questions/2878136/vs2010-error-unable-to-start-debugging-on-the-web-server).
The answer came from Jeroen at StackOverflow:

1.  In Regedit, navigate to
    HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Lsa
2.  Right-click Lsa and create a new DWORD value
3.  Name it DisableLoopbackCheck
4.  Set its value to 1
5.  Reboot (instead, I killed the msvsmon.exe process and restarted
    Visual Studio)

My website (and IIS7.5) is on my local PC (Windows Server 2008 R2).

After finding that solution, I searched a bit on LSA and found this
related KB article:
[http://support.microsoft.com/kb/896861](http://support.microsoft.com/kb/896861)
– it’s about IIS 5.1! It is something about a loopback security check
that helps prevent *reflection* attacks.

Also reference Min Kwan Park’s blog which has lots of possible solutions
for various debugger issues (though this is and old posting):
[http://blogs.msdn.com/b/mkpark/archive/2004/03/09/86872.aspx](http://blogs.msdn.com/b/mkpark/archive/2004/03/09/86872.aspx)

 [Update]

The debug started to fail again in the same way, immediately displaying
the *Unable to start debugging* error after the compile. Killing the
msvsmon and restarting VS2010 did not help. As soon as I click F5,
msvsmon.exe shows up on the taskmanager list and the error displays.

