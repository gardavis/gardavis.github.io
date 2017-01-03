---
layout: post
title: "How I fixed my son's new laptop 160GB drive"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 37
tags: [Personal]
---
My son bought a new 160GB SATA drive for his Dell laptop to replace the
original 40GB drive. I used a USB adapter to connect the drive to the
laptop and used Acronis V11 Home to clone the Dell drive to the new
drive.

After it completed the clone, I pulled out the old and installed the new
and powered up. The drive started the boot and the Windows XP screen
displayed and I thought we were home free! However, it blue-screened
shortly after the Windows screen displayed.

I booted to the setup bios and it showed the new drive as 40GB, same as
the old. Every tool I tried showed 40GB instead of 160GB and I have a
lot of them. Reformatting, zeroing, etc would not bring the drive back
to its original state.

After some hours of searching, I finally found a
[thread](http://forum.hddguru.com/hard-disk-drives-repair-and-data-recovery-f1/disk-resized-from-120gb-to-60gb-after-cloning-with-acronis-t6774.html?sid=d9dae0aa8cbf7d2d6aa9b79f8071b3eb)
which led to the solution. The tool is called
[HDAT2](http://www.hdat2.com/hdat2_faq.html%20). The problem seems to be
the combination of the Dell laptop (with MediaDirect which uses a Host
Protected Area (HPA) of the disk) and Acronis which had apparently
problems with this HPA configuration corrupting the drive.

I burned the HDAT2 ISO to a bootable CD and booted it up to a laptop
with the new drive connected via the USB adapter. HDAT2 did see the USB
drive when the USB ASPI driver was selected during bootup but the option
I was looking for (Set Max (HPA)) was not on the main menu like it was
for the internal drive. So, I pulled out the old and popped in the new
(again) and booted up the HDAT2 CD and this time the Set Max (HPA) menu
item displayed for the drive.

I selected this option and it immediatly showed the discrepancy and had
the Max Address field already populated with the correct value so all I
had to do was type S to Save and that fixed the problem. The new drive
now reported its correct size.

I will not use Acronis with this Dell for a disk clone. BTW, Acronis had
worked fine for my old Dell when I upgraded its drive.

Note that the thread referenced above discussed a Seagate drive that had
issues and a special procedure for dealing with 28 vs 48 bit LBA. My
son's drive is a Western Digital and did not have those problems. A
simple press of the S key was all that was needed in my case.

