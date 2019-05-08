---
layout: post
title: How I solved “Unable to access HASP SRM Run-time Environment? (H0033)”
date: 2014-03-29 -0800
comments: true
disqus_identifier: 3045
published: true
---
First of all, don't stress! These instructions will most likely get you up and running with your 4D, 5D, 6D
or other dongle-controlled program in short order.

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
dongle installed resulted in the H0033 error.
![HASP Dongle](/images/blogs_webguild_com/Windows-Live-Writer/How-do-I-resolve-the-message-Unable-to-a_EDD5/HASPDongle_thumb.png "HASP Dongle"){: .left}

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
[https://sentinelcustomer.gemalto.com/sentineldownloads/](https://sentinelcustomer.gemalto.com/sentineldownloads/) (or use the link below).
Installing this did solve the H0033 error. Also, once installed, the
dongle light was lit and the <http://localhost:1947> worked.

From the download page, I chose to install the **Sentinel HASP/LDK
Windows GUI Run-time Installer**. The zip file contains a Readme file and a HASPUserSetup.exe file. Run the exe file to start the installation. It’s pretty quick.

Copy of HASP SRM Runtime download zip file:

-   V7.92 as of May. 2019: [Click
    here](http://www.webguild.com/data/Sentinel_LDK_Run-time_setup-V7.92.zip)
    
When I installed the driver, I did not have the dongle plugged in. After the install, I tried going to the the localhost url above and it worked (displayed a page, not an error). I then plugged in the dongle and it lit up and the localhost url displayed more mildly interesting information.

Read the feedback (over 100 posts) and you will see virtually everybody is successful with this procedure. Please post feedback on your results. 

