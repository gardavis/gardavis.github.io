---
layout: post
title: "How I Use my Blackberry as a Laptop Modem"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 32
tags: [Personal]
---
Yesterday, there was a major computer room power outage at my company.
All Internet connectivity was down. Even the phones were not working.
Fortunately, our websites failed over to our business continuity site
without a hiccup.

However, everybody at their desks had nothing to do since even internal
network connectivity was affected. My desktop computer is actually a
laptop which I had configured to use my Blackberry as a tethered modem
to allow Internet access when traveling. I plugged in my BB, started up
the Desktop Manager, clicked the Start-\>Connect To-\>Blackberry Bold
9700 and was quickly connected to the outside world. People walking by
my office looked in and saw me typing away and raised an eyebrow. Power
was restored 5 hours later and the servers all back to normal in another
5 hours.

This is the way I configured my system. My laptop is running Windows
Server 2008 R2 (64bit) which is similar to Windows 7. A similar
procedure may work to tether other cell phones that have a data plan
though the parts about Desktop Manager will not apply.

Install the Desktop Manager (DM) software ([click
here](http://na.blackberry.com/eng/services/desktop/desktop_pc.jsp) or
search Google to locate the download). This will install a modem named
*Standard Modem* assigned to a com port.

There is a setting needed for the Standard Modem. Go to Control
Panel-\>Phone and Modem. Modem tab. Select Standard Modem and click
Properties.

[![1](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/1_thumb.png "1")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/1_2.png)

Click the Advanced Tab and enter this string into the Extra
initialization commands field:

> **+cgdcont=1,"IP","wap.cingular"**

I have also seen **isp.cingular** used in some postings I have read, so
if you have problems, you can try changing the above command. Click OK
to close out the dialog boxes.

I don’t remember if you have to add a Dial Up connection or if it is
already done as part of the DM install. I named my connection
“BlackBerry Bold 9700” (see image below). If necessary, you may have to
run the Setup a New Connection procedure in your network center.

To connect, plug in your BB (or use Bluetooth if your laptop has it and
you can get that working). Run the DM program; it should say it is
connected and you can minimize it.

I connect using the Connect To link below or the connections icon in the
tray. There are a few ways.

[![2](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/2_thumb.png "2")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/2_2.png)

Click the Connect button and the DialUp displays:

[![3](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/3_thumb_1.png "3")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/3_4.png)

The fields are already filled in. There is no need to change the
defaults – even the user id and password can be left blank or whatever
they are. The phone number to dial is \*99\# and should already be
displayed.

You can click on Properties and change some settings so when you click
to connect, it will dial automatically and not bother displaying the
above step.

[![4](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/4_thumb.png "4")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/4_2.png)

Click Dial. It will progress through a few steps (dialing, registering)
and you will then be connected.

[![5](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/5_thumb.png "5")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/5_2.png)

If an error code displays, various things could be wrong. Maybe you need
the tether plan added to the Blackberry account; maybe the DM is not
running or your BB is not connected, etc.

I just tried to close down DM with the connection still active and it
looks like this is supported – you don’t need to keep it minimized:

[![6](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/6_thumb.png "6")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/6_2.png)

If I try to connect without having DM running, I get this Error 692:

[![7](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/7_thumb.png "7")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIUsemyBlackberryasaLaptopModem_8B04/7_2.png)

I get the same error code if DM is up but my BB is not plugged in to the
USB cable.

I mentioned Bluetooth earlier. If you can get this working, it is really
nice. My wife’s laptop has it and to connect, DM is not needed. I just
click to connect for the connection and my BB may be on the desk or in
the holster – it just connects and off you go. When connected (Bluetooth
or USB), you still can make and receive calls without interrupting your
connection.

Good luck!

