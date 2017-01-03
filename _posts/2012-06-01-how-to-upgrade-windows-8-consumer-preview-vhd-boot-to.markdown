---
layout: post
title: "How to Upgrade Windows 8 Consumer Preview VHD Boot to Release Preview"
date: 2012-06-01 -0800
comments: true
disqus_identifier: 1041
tags: []
---
I already went through the procedure to create a Virtual Hard Drive
(VHD) with Win8 Consumer Preview as described in the [HowToGeek.com
article](http://www.howtogeek.com/75286/how-to-dual-boot-windows-7-and-8-without-re-partitioning-using-vhd/)
and wanted to replace the VHD contents with the new Release Preview that
came out yesterday. If you have the same situation, this will save you
several steps.

If you try to upgrade your Consumer Preview, it will tell you that it is
not possible since it is on a VHD. Maybe someone will figure out a
workaround so your installed programs are not lost. So I figured for
now, I'd just blow away the Consumer Preview and use the same VHD to
hold the Release Preview.

The steps you save are creating the VHD and adding it to the boot menu.
What you want to do are these steps:

1.  Download the ISO for the RP (from
    [here](http://windows.microsoft.com/en-US/windows-8/iso))
2.  Mount the ISO as a drive (I used
    [this](http://www.slysoft.com/en/virtual-clonedrive.html))
3.  Attach the old VHD as a drive letter (Computer Mgt-\>Disk
    Mgt-\>Action-\>Attach VHD)
4.  Format the VHD drive to blow away the old Win8 CP
5.  Start PowerShell in Administrator mode to run
    the Install-WindowsImage.ps1 script (from
    [here](http://archive.msdn.microsoft.com/InstallWindowsImage/Release/ProjectReleases.aspx?ReleaseId=2662))
6.  Run Install-WindowsImage as shown below
7.  Assuming your boot menu Win8 entry is still in place, reboot into
    your new Win8 RP.

To run Install-WindowsImage enter this at the PowerShell prompt. This
assumes you have CD'd into the folder with the script:

> PS\> .\\Install-WindowsImage.ps1 –WIM J:\\Sources\\Install.wim –Apply
> –Index 1 –Destination I:\

 Also, it assumes J: is the mounted ISO and I: is the attached VHD. The
script will make the VHD bootable and copy the necessary folders and
files from the ISO to the VHD. If you need to add a new boot menu item
type **bcdboot.exe I:\\Windows** where I: is your VHD. 

![PowerShell running
Install-WindowsImage](/images/blogs_webguild_com/PSInstWin8.png)

The Install-WindowsImage took about 4 minutes where the ISO and VHD
where on an SSD and 32 minutes when both were on the same hard drive
partition.

To reuse the same boot menu, the VHD file name and location need to be
the same (use command line bcdedit with no parameters to display the
boot menu details).
  
 At this point, the VHD has an installed version of Windows 8 Release
Preview that can be booted. The initial boot will go through some
configuration and setup and you're done. The product key is:
DNJXJ-7XBW8-2378T-X22TX-BKG7J or TK8TP-9JN6P-7X7WW-RFFTV-B7QPF .

The howtogeek.com article above has all the details, screenshots and
more if you need additional information about this procedure.

Once running, you can install Windows Media Center using the info at
[this
blog](http://www.techspot.com/news/48847-media-center-yanked-from-windows-8-release-preview-heres-how-to-re-enable-it.html).
