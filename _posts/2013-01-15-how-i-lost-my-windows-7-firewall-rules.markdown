---
layout: post
title: "How I Lost My Windows 7 Firewall Rules"
date: 2013-01-15 -0800
comments: true
disqus_identifier: 1044
tags: []
---
I run a Windows 7 Web Server on a Media PC (see
[here](/archive/2011/02/23/fatal-error-c0000034-installing-windows-7-sp1.aspx))
as my home server and from work, I connected to it using Remote Desktop.
I ran Windows Update and part way through the 19 updates, the Remote
Desktop connection froze. I figured the updates needed a reboot and but
the server never came back up. I’d have to wait till I got home to
figure out what happened.
[![Updates1](/images/blogs_webguild_com/Windows-Live-Writer/How-I-Lost-My-Windows-7-Firewall-Rules_11E6E/Updates1_thumb.png "Updates1")](/images/blogs_webguild_com/Windows-Live-Writer/How-I-Lost-My-Windows-7-Firewall-Rules_11E6E/Updates1_2.png){: .right}

When I got home, the server was pretty much how I left it from work. It
had completed the updates and was just ready to reboot. The problem was
that I could not connect to the server remotely. Outgoing connections
were working fine (web pages, etc.). It turned out that the Firewall was
blocking everything. I disabled the firewall and was then able to
connect to the server (web pages, Remote Desktop, SQL Server).

I went into the Windows Firewall advanced settings and all inbound and
outbound rules were missing!

First I ran [MalwareBytes](http://malwarebytes.org) Anti-Malware and it
showed no viruses or threats. Next I went to restore back to before the
updates but my System Restore was not turned on! I do run Windows Backup
and the last backup of the system image was a few days earlier. I could
get my firewall rules from the SYSTEM registry on that backup.

[![FirewallReg](/images/blogs_webguild_com/Windows-Live-Writer/How-I-Lost-My-Windows-7-Firewall-Rules_11E6E/FirewallReg_thumb.png "FirewallReg")](/images/blogs_webguild_com/Windows-Live-Writer/How-I-Lost-My-Windows-7-Firewall-Rules_11E6E/FirewallReg_2.png){: .left}
The backup creates a VHD virtual drive for the system and the program files.
I mounted the system VHD as a drive and located the registry
(\\windows\\system32\\config\\SYSTEM). I ran regedit and attached the
SYSTEM registry file hive to get to the registry settings for the
firewall. I located the firewall settings at this location
HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\SharedAccess.
I attached the backup hive to HKEY\_LOCAL\_MACHINE\\SYSTEMBackup (focus
on HKEY\_LOCAL\_MACHINE then File-\>Load Hive). I drilled down to
SharedAccess on the SYSTEMBackup (see image).

Comparing this structure on SYSTEMBackup to SYSTEM, I noticed that on
SYSTEM the entire Defaults key was missing and the
Parameters\\FirewallPolicy\\FirewallRules key was there but there were
no rules within it. The Default is probably not required but is the
firewall reset info if needed.

I exported the SYSTEMBackup keys to a .reg file. I edited the file to
change the location of the keys from SYSTEMBackup to SYSTEM. I then
saved the file back (save as ANSI, not unicode). I then right-clicked
the file and selected Merge to restore my firewall rules. **NOTE:**This
is potentially very dangerous since you are modifying the registry!

Going back into the Windows Firewall advanced settings showed my inbound
and outbound rules in place.

The rules seem to need a bit more tweaking since my HTTP ports are still
blocked.

A good place to test out your firewall is at
[www.grc.com](http://www.grc.com) – navigate to the Shields Up page to
verify your ports are blocked as expected. Note that your router may be
doing most of the port blocking for you.
