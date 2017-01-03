---
layout: post
title: "How to recover space from your Android-imaged SDCard"
date: 2012-05-04 -0800
comments: true
disqus_identifier: 41
tags: []
---
When using a (Micro)SDCard created in Windows for an Android boot,
partitions are written to it in a Linux format that Windows does not
completely understand.

I did this when rooting my NookColor with CyanogenMod 7. My 8GB card was
imaged using the
[Win32DiskImager](https://launchpad.net/win32-image-writer) tool that
takes an IMG file and writes it to the card, laying down various
partitions, including one standard Windows partition of about 130MB.
This basically hides the remainder of the card from Windows but boots up
my NookColor into Andriod just fine.

Well, eventually, you need to recover the card to use in Windows again.
You can't use the Windows format command since that will only empty out
the small partition. Normally, partitions can be deleted using the
Computer Management program (under Disk Management). You select the
SDCard volume and right click the partition and delete it.This did not
completely work - some partitions did not have the delete option.

To actually delete the partitions, drop down to the command line (run as
administrator, just in case). Run **diskpart**.When the prompt displays,
run these commands.

DISKPART\> **list disk     ***[lists all the disks on the system]*

DISKPART\> **select disk *n*     ***[carefully select the disk that is
the SDCard for the following command]*

DISKPART\> **list partition*     ****[lists all the partitions of the
selected disk]*

DISKPART\> **list disk     ***[lists all the disks on the system]*

DISKPART\> **select partition *n     ****[select a partition to delete]*

DISKPART\> **delete partition     ***[delete the selected partition]*

*[At this point repeat the list, select and delete commands for each
partition*

DISKPART\> **exit     ***[exits diskpart]* 

At this point, I used Disk Manager to create a new partition, assign a
drive letter and format the partition to FAT32. This can also be done
with DISKPART **create partition**and **assign** commands.

![Diskpart commands](/images/blogs_webguild_com/gary/DiskPart.png)

 References:

-   [Delete a partition or logical
    drive](http://technet.microsoft.com/en-us/library/cc738489%28WS.10%29.aspx)
-   For NookColor: [How to make a bootable CWM 3.2.0.1 (ClockWorkMod) or
    TWRP 2.1.1 bootable sd card
    ](http://androidforums.com/nookcolor-all-things-root/327798-guide-how-make-bootable-cwm-3-2-0-1-clockworkmod-twrp-2-1-1-bootable-sd-card-4-22-2012-a.html)
-   [Download and Install CM7 to Run Off SD
    Card](http://androidforums.com/nookcolor-all-things-root/367116-how-download-install-cm7-run-off-sd-card.html)


