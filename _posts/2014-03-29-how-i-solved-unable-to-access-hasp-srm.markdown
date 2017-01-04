---
layout: post
title: "How I solved “Unable to access HASP SRM Run-time Environment? (H0033)”"
date: 2014-03-29 -0800
comments: true
disqus_identifier: 3045
tags: []
---
### Background

My wife asked me to install her Viking embroidery “5D” software on her
Surface Pro PC so she could use the touch tablet and pen to do graphics
drawing and editing in the Design Creator.

The software is protected by requiring the user to have a USB dongle
plugged in when running the program.

Installation went through normal software install and then it also had 3
updates to install. Two of the updates seemed to end with an error,
perhaps because I did not reboot the PC after each (it was not clear
whether or not to do this). At any point, running the program with the
dongle installed resulted in the H0033 error.[![HASP
Dongle](/images/blogs_webguild_com/Windows-Live-Writer/How-do-I-resolve-the-message-Unable-to-a_EDD5/HASPDongle_thumb.png "HASP Dongle")](/images/blogs_webguild_com/Windows-Live-Writer/How-do-I-resolve-the-message-Unable-to-a_EDD5/HASPDongle_2.png)

I tried doing a repair install and also install of drivers (from the
main install menu) – neither helped.

Searching on this error showed several hits saying to go to the windows
Services and enabling the HASP License Manager (or Sentinel HASP License
Manager) but in my case, I did not have the HASP entry in Services.

I looked in the Device Manager and saw an error for the HASP device and
its properties said the device driver was not installed. Doing an
Uninstall followed by a Scan for New Hardware did not help.

Some posts said to try to go to this url in your browser:
<http://localhost:1947> but that just displayed an error. Normally, this
would display the HASP SRM Admin Control Center. 

### Solution

I eventually found a post to download the HASP SRM Runtime drivers at
[http://sentinelcustomer.safenet-inc.com/sentineldownloads/](http://sentinelcustomer.safenet-inc.com/sentineldownloads/).
Installing this did solve the H0033 error. Also, once installed, the
dongle light was lit and the <http://localhost:1947> worked.

From the download page, I chose to install the **Sentinel HASP/LDK
Windows GUI Run-time Installer**.

Ref:
[http://sentineldiscussion.safenet-inc.com/topic/unable-to-access-sentinel-hasp-run-time-environment-h0033](http://sentineldiscussion.safenet-inc.com/topic/unable-to-access-sentinel-hasp-run-time-environment-h0033)

Copy of HASP SRM Runtime download zip file:

-   V7.32 as of Apr. 2015: [Click
    here](http://www.webguild.com/data/Sentinel_LDK_Run-time_setup-V7.32.zip)
    – This is the previous version I know works.
-   V7.52 as of Dec. 2016: [Click
    here](http://www.webguild.com/data/Sentinel_LDK_Run-time_setup-V7.52.zip)
    – This is the latest version. Does it work?


Please post feedback on your results.
