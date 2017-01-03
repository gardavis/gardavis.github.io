---
layout: post
title: "How to enable the Microsoft Installer logging"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 23
tags: [Personal]
---
Sometimes, when installing software that uses the Microsoft Windows
Installer, it fails with some sort of cryptic error message. Enabling
generation of the log file may give you insights to the reason for the
failure and hope to resolve the issue.

To enable logging:

1.  Run regedt32
2.  Navigate to HKLM\\SOFTWARE\\Policies\\Microsoft\\Windows\\Installer
3.  Create REG\_SZ with name "Logging" and value of "**iwearucmpvox**"
    (turns all logging on)
4.  Create REG\_DWORD with name "Debug" and value of **2**
5.  Download and run DebugView from Microsoft Sysinternals site
6.  Rerun the install

The debug view window will capture all MSI debugging information as it
happens. 
 The log file itself will be created in the temp directory (ie,
C:\\Users\\\<account\>\\AppData\\Local\\Temp) 
 and will have a name like "MSIe9359.LOG".

Note that you can also change installer logging using the group policy
editor (gpedit.msc). 
 The installer settings can be found at Computer Configuration -
Administrative Templates - Windows 
 Components - Windows Installer.

Ref: Originally found on the TivoCommunity.com forum.


