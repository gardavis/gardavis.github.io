---
layout: post
title: "How I Ported a Windows Phone 7 App to WP8"
date: 2013-01-10 -0800
comments: true
disqus_identifier: 1043
tags: [WP7,Programming,WP8]
---
I completed the porting of my
[Tivo Net Remote](http://www.windowsphone.com/en-us/store/app/tivo-net-remote/6a96de72-0338-4b60-ad1d-1c18cb365f27 "Link to TiVoNetRemote WP App")
app last week from WP7 to WP8 using some ideas from the Nokia Porting
Guide. It was published yesterday.

I opened the source code solution using the new SDK and verified it
compiled. There were minor changes I wanted to get in. One was to remove
the Performance Progress Bar from the toolkit and use the native
Progress Bar which was fixed to be like the toolkit version.

I then created a new project in the solution for the WP8 version. I used
the copy-as-link on all the source files, though I did compare the
differences in the App.xaml to manually migrate some of the lines of
code in the .cs. There were a few files, I think tile images, that did
not work with the link technique so I copied the files to the new
project. The problem seemed to be in the packaging of the xap – the
files just were not copied when they were links or something.

The App communicates with the TiVo using sockets and the WP8 has a
really nice StreamSocket class I was able to use cutting down the comm
code quite a bit for the WP8 version.

To submit the update, both xap files (WP7 and WP8) were uploaded to the
Microsoft store. The re-certification process took four or five days.

I uninstalled my test version from my WP8 and searched the store for the
new one and found it. The entry showed the Try and Buy buttons though I
had purchased the WP7 version long ago. I clicked the Try to install it
and it ran in trial mode. This did not make sense that I would have to
buy it again.
[![PortArticleImg1](/images/blogs_webguild_com/Windows-Live-Writer/98620fb2515e_E3F0/PortArticleImg1_thumb_1.png "PortArticleImg1")](/images/blogs_webguild_com/Windows-Live-Writer/98620fb2515e_E3F0/PortArticleImg1_4.png){: .right}

I went to [www.WindowsPhone.com](http://www.WindowsPhone.com) to see my
purchase history and saw two entries for TivoNetRemote – one to
Purchase/Reinstall and the other to simply Reinstall.

I uninstalled the app from the phone and clicked the web page link to
reinstall (both entries have the same link/appid). The reinstall did
wind up installing the full version so I did not have to re-purchase it.
The appid is unchanged from the original.

[![PortArticleLog](/images/blogs_webguild_com/Windows-Live-Writer/98620fb2515e_E3F0/PortArticleLog_thumb_1.png "PortArticleLog")](/images/blogs_webguild_com/Windows-Live-Writer/98620fb2515e_E3F0/PortArticleLog_4.png){: .left}
When someone runs the app, it sends a message to a web service to log some
info (max of once per day) and get the app settings.             
