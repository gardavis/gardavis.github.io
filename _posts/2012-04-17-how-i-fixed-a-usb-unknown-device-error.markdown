---
layout: post
title: "How I Fixed a USB &quot;Unknown Device&quot; Error"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 29
tags: [Personal]
---
My son's printer stopped working on his Gateway laptop. When plugging
into any USB port, the generic "Unknown Device" error balloon displayed
in the tray area. I tried other cables, printers and even USB Drives and
all got the same error. The printer was immediately recognized in a
desktop, even though there were no drivers installed for it.

I had tried uninstalling the Unknown Devices from the Device Manager and
even the USB Hubs and Host Controllers then forcing a "scan for hardware
devices" to get them re-installed. Plugging the printer back in still
resulted in the Unknown Device.

I eventually tried this suggestion from Experts-Exchange.com which fixed
the problem. It lets you see other hidden Unknown Devices and Other
Devices in the Device Manager. Uninstalling everything USB related and
then plugging in the printer (with no reboot) got the printer recognized
immediately.

**STEP \#1:** Create a system environment variable that will allow you
to see nonpresent devices in the device manager.
 
 START-\>SETTINGS-\>CONTROL PANEL-\>SYSTEM icon-\>ADVANCED
tab-\>ENVIRONMENT VARIABLES button
 Click NEW on the bottom of the SYSTEM VARIABLES frame.
 Enter the following:
 Variable name: **devmgr\_show\_nonpresent\_devices**
 Variable value: **1**
 Click OK and close the SYSTEM/CONTROL PANEL windows.
 (It is very important to spell this exactly as it appears.  If you
mispell it, you'll know it because you won't see a "ghosted out" Unknown
Device later on.)
 
 **STEP \#2:** Open the DEVICE MANAGER, enable VIEWING HIDDEN DEVICES,
and locate the UNKNOWN DEVICE
 
 START-\>SETTINGS-\>CONTROL PANEL-\>ADMINISTRATIVE TOOLS icon-\>COMPUTER
MANAGEMENT icon-\>DEVICE MANAGER folder
 First, we want to enable viewing hidden devices.  The environment
variable gives this a second functionality as well, to see both hidden
and disconnected devices.  From the menu, select VIEW-\>SHOW HIDDEN
DEVICES 
 After that, find the device tree called "Universal Serial Bus
Controllers" (it should be the last thing in the list).
 Expand this tree, and you should see the UNKNOWN DEVICE somewhere in
there.
 
 **STEP \#3:** Unplug the USB device
 
 Now, unplug the USB device, and the UNKNOWN DEVICE should sort of
"ghost" out a bit.  If it disappears completely, either "Show Hidden
Devices" isn't checked, or the environment variable was spelled wrong.
 Close everything, check the environment variable, and try again.
 
 **STEP \#4:** Uninstall the "ghosted" UNKNOWN DEVICE
 
 Right click on the "ghosted" UNKNOWN DEVICE and select Uninstall.  Do
not accidentily uninstall anything else in the tree!  The UNKNOWN DEVICE
should now disappear.  If there are any other UNKNOWN DEVICES that are
also ghosted out, uninstall those as well.
 
 **STEP \#5:** Plug the USB device back in
 
 When you plug it back it, the USB device should now be detected
properly.  If not, .....  then well... I tried :)
 
 Good Luck!

