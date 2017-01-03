---
layout: post
title: "Fatal Error C0000034 installing Windows 7 SP1"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 10
tags: [Personal]
---
I attempted installation of SP1 for Windows 7 on an Acer (Aspire Revo
3610) PC running 64-bit Windows 7. The PC runs as a home server and I
started the install while remotely connected. Once it completed the
install (with about 5 other Windows updates), I allowed it to reboot.
![](/images/blogs_webguild_com/gary/Acer.png)

I eventually noticed that it never came back up (I was unable to ping
it) so I went to the console (my TV monitor) and it displayed no signal.
The power light was on so I left it alone incase it was just a really
long install. I actually installed the SP1 on my desktop, also running
64-bit and though it took a long time (maybe an hour), it did complete
and start up OK.

I then powered the Acer off and on and it started a reboot which
displayed on the console. It indicated it had a problem and offered a
recovery or continue the boot normally. I opted to continue the normal
boot. It displayed the bootup graphic and started a count-up of the dlls
it was updating similar to my successful install. However, it stopped
early and displayed a fatal error:

> Fatal Error C0000034 applying update operation (Update 282 of 103814)

I searched the web and did not get many hits on this error and none very
helpful other than to recover from a backup or checkpoint.

So, I rebooted again, this time choosing to recover from the last good
boot. This also took a while - maybe 1/2 an hour but was successful.

I will reattempt the SP1 install when I can get more information on this
error and its resolution.

**UPDATE** (from
[this](http://social.technet.microsoft.com/Forums/en-US/w7itprogeneral/thread/608ecca8-b815-4ff6-8f3c-a828518434a7))
- Once you are recovered, provide your logs to Microsoft

*Go to the folder **C:\\Windows\\Logs\\CBS\\** and copy all files to
your document folder, also copy the setupapi logs from the folder
**C:\\Windows\\Inf** and the file **C:\\Windows\\winsxs\\poqexec.log**
to your document folder. Zip all files into 1 Zip file and upload the
Zip file to your SkyDrive and post a link**here:
[http://social.technet.microsoft.com/Forums/en-US/w7itproui/thread/4fc10639-02db-4665-993a-08d865088d65](http://social.technet.microsoft.com/Forums/en-US/w7itproui/thread/4fc10639-02db-4665-993a-08d865088d65)*

**UPDATE 2** (A reported solution from **thiswoot**:
[here](http://social.technet.microsoft.com/Forums/en-US/w7itproinstall/thread/1c9a7151-b48c-4a98-aae7-a4b82682ea8e/#bcabda57-7338-499f-aee2-d708e76df315))
- Basically, select Launch Startup Repair; follow the steps to get to
the command line; run **notepad.exe c:\\windows\\winsxs\\pending.xml**;
reboot and wait about 15 minutes and the SP1 will complete its install.

