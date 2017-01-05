---
layout: post
title: "How I Got My NookColor CM 10.2 to Mount SDCard Partition 4"
date: 2013-09-15 -0800
comments: true
disqus_identifier: 2044
tags: []
---
Years ago, I rooted my NookColor to replace its eReader functionality
with a standard Android tablet operating system. I used CyanogenMod
version 7 and periodically upgraded to new versions.

Initially, I left the stock B&N eBook code (ROM) alone in the device and
put all the modifications, upgrades, hacks, etc. on an SDCard left in
place in the slot. Eventually, around CM 10.1, I decided to replace the
B&N ROM with the CM 10.1 since I never booted into the stock ROM
anymore. I did leave the SDCard in place and using the TWRP ([TeamWin
Recovery Project](http://teamw.in/)), I could select at boot time which
ROM to boot into.

The SDCard is formatted with four partitions when set up to install or
update CM7 ROMs. The first partition (partition \#1 since numbering
starts at 1 instead of 0), has the boot files and is a small partition.
Partition \#4 has the remainder of the data of the SDCard for pictures,
videos, music, apps or whatever.

When booting to the device (emmc) ROM instead of to the SDCard ROM, the
system mounts the 1st partition of the SDCard for data (called sdcard1).
Since I have my data on partition \#4, after installing a ROM upgrade, I
would modify the boot to instead mount partition \$1 as data. The way I
did this was to modify file /system/etc/vold.fstab and change **auto**
to **4** for the sdcard entry. Auto winds up mounting partition \#1.

> dev\_mount sdcard /mnt/sdcard **auto**
> /devices/platform/mmci-omap-hs.0/mmc\_host/mmc1 

Well, when I upgraded to CM 10.2, which is Android Jellybean version
4.3, I could not find the file to edit. Some Binging around showed that
vold.fstab was no longer used in 4.3. Instead, there was a file
/init.encore.rc which was used at boot time to do various things
including the filesystem mounts. This file mount\_all to mount all
requests in /fstab.encore. Looking at this file shows the statement:

> /devices/platform/omap/omap\_hsmmc.0/mmc\_host/mmc1 /storage/sdcard1 
> auto defaults voldmanaged=sdcard:**auto** 

This is the line that has to change. Note there are two *auto*s in that
statement; the first is the filesystem type (for NookColor, it is
basically VFAT) and the second is the partition number which is the one
to change.

I switched to SuperUser mode and edited the file to change auto to 4 and
rebooted. It did not work. The edited file was back to what it was
originally.

A bit more Binging showed that the files are replaced at boot time with
versions in the boot uRamdisk file. So I had to extract the fstab.encore
file from the uRamdisk file, edit it and then replace the modified file
back into the uRamdisk.

There are several steps to do this and there are various ways to do
this. This is what I did.

The uRamdisk file is in boot partition \#1 (on the device, not the
SDCard). Once booted, this partition is not accessible so the first step
was to mount partition \#1 Using the terminal emulator in SuperUser
mode:

> cd /emmc
>
> mkdir boot
>
> mount –t vfat /dev/block/mmcblk0p1 boot

This switches to the /emmc folder which is the internal sdcard0 and is
writable. Create an empty folder to be used as a mount point named boot.
Finally mount the boot partition (device 0, partition \#1) at
/emmc/boot. Note, /emmc is the same as /storage/sdcard0. Also, /sdcard
is the same as /storage/sdcard1.

Next, plug in your Nook to your Windows PC and enable the USB file
sharing. Use explorer to locate the /emmc/boot/uRamdisk file to verify
it is where you expect it. The emmc folder will be assigned a drive
letter. If an external SDCard is in the Nook, it also will get a drive
letter. Copy the uRamdisk file to your PC as a backup.

To extract the fstab.encore file, use
[BootUtil](http://www.temblast.com/android.htm) as discussed
[here](http://forum.xda-developers.com/showthread.php?t=1777182Modifying).
Download the BootUtil to a folder. Start a command prompt and change to
that folder. Extract the fstab.encore file from the Nook version of the
uRamdisk file (or use a local version if you prefer), edit it with
notepad and replace the file back into the uRamdisk.

> bookutil /l x:\\emmc\\boot\\uRamdisk *[optional list contents]*
>
> bookutil /v /x x:\\emmc\\boot\\uRamdisk fstab.encore
>
> [edit fstab.encore to replace the second **auto** with **4**]
>
> bookutil /v /r x:\\emmc\\boot\\uRamdisk fstab.encore

Stop the USB file sharing, disconnect the cable, dismount the mounted
boot

> umount boot

Reboot and you should now have your SDCard partition \#4 mounted

There are other ways of doing parts of this procedure such as using ADB
or Samba, wifi instead of USB, dd instead of BootUtil, etc. If you have
ideas on doing this without using the terminal console or all on the
Nook instead of a Windows PC, please add some comments.
