---
layout: post
title: "How I Dealt With an ave.exe Virus Infection"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 14
tags: [Personal]
---
+--------------------------------------------------------------------------+
| Ave.exe Removal Instructions                                             |
|                                                                          |
| If you have this **ave.exe**rogue anti-virus infection and are too       |
| anxious to read this posting, these are the removal steps that worked    |
| for me on Windows XP:                                                    |
|                                                                          |
| 1.  Type *Ctrl/Shift/Escape* to bring up the task manager.               |
| 2.  Kill the **ave.exe** process. The popups will disappear. Leave the   |
|     task scheduler up.                                                   |
| 3.  Type *Windows/R* (to get the Run box) and type **regedit** and OK.   |
| 4.  Ave.exe will start again, just do step \#2 again.\                   |
|      [**Note**: Be careful with regedit. If you are not familiar with    |
|     it, use other solutions for this infection]                          |
| 5.  In Regedit, go to **HKCR\\.exe\\shell\\open\\command**. You will see |
|     something like this for (default):\                                  |
|      **"C:\\Documents and Settings\\[your account]\\Local                |
|     Settings\\Application Data\\ave.exe" /START "%1" %\***               |
| 6.  Modify the value to be:\                                             |
|      **"%1" %\***                                                        |
| 7.  Do the same with **HKCR\\secfile\\shell\\open\\command.**            |
| 8.  Delete ave.exe from the location in step 5.\                         |
|      **At this point, you have control back and no more popups.**        |
| 9.  Download the current version of Malwarebytes'                        |
|     [Anti-Malware](http://malwarebytes.org/mbam.php) and run it.         |
| 10. Choose to fix the items the scan found.                              |
| 11. Run a scan of your regular anit-virus program.                       |
| 12. Now you can read the rest of this post and add a comment about your  |
|     experience!                                                          |
+--------------------------------------------------------------------------+

 

This week I attended the Microsoft [MIX10](http://live.visitmix.com/)
Web Designer/Developer conference in Las Vegas. After the last session
of the last day, before they kicked me out of the hall with the free
WiFi, I somehow contracted a virus (I think from isohunt.com though just
from browsing the site; I did no downloads). I actually did not realize
it until the next time I started the laptop. I got a virus infection
warning popup and then another window opened automatically running a
scan and finding lots of infected files.

 
[![ave1](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIDealtWithanave.exeVirusInfection_FC19/ave1_thumb.png "ave1")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIDealtWithanave.exeVirusInfection_FC19/ave1_2.png)          
[![ave2](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIDealtWithanave.exeVirusInfection_FC19/ave2_thumb.png "ave2")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIDealtWithanave.exeVirusInfection_FC19/ave2_2.png)

Then a tray notification bubbled up with more warnings.

 
[![ave3](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIDealtWithanave.exeVirusInfection_FC19/ave3_thumb.png "ave3")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIDealtWithanave.exeVirusInfection_FC19/ave3_2.png)

The laptop was really scared out of its mind!

Well, I did not recognize the program displaying the warnings. The
laptop is an old Dell running WinXP and is up to date with patches and
runs [AVG Free](http://free.avg.com/) as its anti-virus software. The
window title of the warning and scanner was Total XP Security. I
suspected the laptop was infected with a virus that mimicked an
anti-virus program. Process status showed ave.exe, a process that I did
not recognize. Killing the process closed the popups. Until the next run
of a program (like explorer). Some programs would not start at all (like
my AVG scanner).

I searched for ave.exe but the search did not find it (it was there but
hidden). I then searched for all files modified today and it found lots
that shouldn’t have been. Exe’s that were installed long ago had a
timestamp of the time the conference ended.

So with my laptop basically disabled, I used my BlackBerry to googled
for **ave.exe virus**. There were several hits and I selected the [Virus
Removal Guru](http://www.virusremovalguru.com/?p=5911) site. Looking at
the manual removal instructions, I killed the ave.exe process and then I
located the ave.exe (C:\\Documents and Settings\\[username]\\Local
Settings\\Application Data\\ave.exe) and removed it.

Well all of a sudden, none of my programs would start. They displayed
the Windows dialog box to select a program to run the exe(?). That
indicated to me that the programs first ran the ave.exe and then it did
its work and transferred back to the originally requested program.
Without ave.exe around, the requested program could no longer start up.
The program I really wanted to run was regedit to fix up the registry.
The running explorer still worked but I could not start up a new one.

I noticed that the programs in my launch bar
([PowerBar](http://plemsoft.com/)) still ran but the same program would
not run from explorer. I dragged regedit into the launch bar and clicked
it and it did run! OK, Now I was back in business. I continued with the
manual instructions from Guru but the registry keys it mentioned did not
exist. I was hesitant to run their automatic removal tool since I am not
familiar with their site. My next step in regedit was a search for
ave.exe. There were several hits (ignore the scnsave.exe hits). The hits
showed how it intercepted the execution of programs to do its deed
first.

The first hit was:

HKCR\\.exe\\shell\\open\\command 
 (default) 
 "C:\\Documents and Settings\\Gary\\Local Settings\\Application
Data\\ave.exe" /START "%1" %\*

I changed it to match others that were not altered:

"%1" %\*

This did not work. The programs still failed to start. I went to the
next hit

HKCR\\secfile\\shell\\open\\command

This did work (phew!)

There were a few more hits related to Iexplore and FireFox.

So things are working better now. I started up a complete scan with AVG
Free and it is still running. I will research some more to make sure
everything is cleaned out before claiming success.

Here’s another link and there are several others. As this post mentions,
manual removal of viruses is generally difficult and if you make
mistakes changing the registry, you may damage your system.

Well, I am now at the Las Vegas airport, waiting for the time to board
my midnight red-eye back to Ft. Lauderdale. I was wondering what I was
going to do to fill the time between 6pm and midnight. So a successful
virus eradication plus a blog post were not on my plans but I guess you
do what you’ve gotta do:)

[Update] Some of the research shows that this virus may be removed by
recent versions of Malwarebytes'
[Anti-Malware](http://malwarebytes.org/mbam.php). Anti-Malware found
many infections which I chose to fix all. I then ran the AVG scan and it
found none.

Some references about this virus:

-   [http://www.microsoft.com/security/antivirus/rogue.aspx](http://www.microsoft.com/security/antivirus/rogue.aspx)
-   [https://www.microsoft.com/security/portal/Threat/Encyclopedia/Entry.aspx?Name=Trojan%3aWin32%2fAntivirusxp](https://www.microsoft.com/security/portal/Threat/Encyclopedia/Entry.aspx?Name=Trojan%3aWin32%2fAntivirusxp)
-   [http://www.symantec.com/connect/blogs/xp-internet-security-2010-rogue](http://www.symantec.com/connect/blogs/xp-internet-security-2010-rogue)
-   [http://www.bleepingcomputer.com/](http://www.bleepingcomputer.com/)
-   [http://www.virusremovalguru.com/?p=5911](http://www.virusremovalguru.com/?p=5911)

I think the way I got infected was at isohunt.com. I clicked a link in
the right nav Top Searches; went to the second search-results page which
partially displayed the hits and then displayed a warning about the site
containing malicious software. I clicked in the warning and exited the
site completely. I think clicking on the warning is what initiated the
download of the infection.

