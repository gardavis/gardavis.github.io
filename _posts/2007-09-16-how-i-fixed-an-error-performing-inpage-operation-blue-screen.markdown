---
layout: post
title: "How I fixed an &quot;Error Performing Inpage Operation&quot; Blue Screen reboot loop"
date: 2007-09-16 -0800
comments: true
disqus_identifier: 16
tags: [Personal]
---
On a laptop, attempting to boot up resulted in a brief error and return
to the reboot sequence. Selecting safe boot, did not help nor did
attempting to go back to a previously good boot.

At some point, I saw the inpage error message.

The problem was that somehow, the C: drive got corrupted. The D: drive
(partition on the same physical drive) is used as a GateWay recovery
partition and it was OK, so I know the drive itself was OK; just the C:
partiton was messed up.

I did not want to re-install using the D: drive (by hitting F11 at
boot). I used a bootable CD that boots into windows from that device
that I had in my stack of recovery tools (see
[www.nu2.nu/](http://www.nu2.nu/)). Perhaps a Dos boot floppy might do
the trick.

Attempting to view C: showed just an error.

I then ran **chkdsk /r** from a dos window and it took about a 1/2 hour
to complete, found several issues and after complete, I was able to view
the C:\\ drive. Reboot then succeeded as normal!
