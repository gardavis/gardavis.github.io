---
layout: post
title: "The TivoNetRemote App for the Windows Phone 7"
date: 2012-04-16 -0800
comments: true
disqus_identifier: 5
tags: [WP7]
---
I have been spending some time lately writing an app for the Windows
Phone 7 to remote
[![TivoNetRemoteMktM](/images/blogs_webguild_com/gary/Windows-Live-Writer/67b7f95c899e_117B7/TivoNetRemoteMktM_3.png "TivoNetRemoteMktM")](http://garz.me/tivonetremote)control
a TiVo using your home network (not infrared). Today, the app showed up
in the marketplace.

[![TivoNetRemotePhoneS](/images/blogs_webguild_com/gary/Windows-Live-Writer/67b7f95c899e_117B7/TivoNetRemotePhoneS_3.png "TivoNetRemotePhoneS")](http://www.tivonetremote.com/)

The app uses the Mango (7.5) version of the Windows Phone 7 which
supports TCP/IP socket communication. As you click the buttons, commands
are sent to the TiVo over the connection to tell it to do various
things. For example, **IRCODE PAUSE** is the command to pause the TiVo.
TiVo has documented most of the commands. The TiVo Premiere, S3 and TiVo
HD support network remote control.

The app uses some controls from Telerik to improve the user interface
such as page transitions, popups for Trial/Purchase notification and the
list picker.

The app has a trial and purchase mode. The trial is free but some
functionality is disabled. Purchasing the full version (\$1.99)
immediately enables the missing functions.

The app uses the Dotfuscator product from [Preemptive
Solutions](http://www.preemptive.com/) to obfuscate the code to deter
reverse engineering and decompiling the app as well as add analytics to
track the number of times the app is used by all those that downloaded
it.[![TivoRemoteWM6](/images/blogs_webguild_com/gary/Windows-Live-Writer/67b7f95c899e_117B7/TivoRemoteWM6_3.png "TivoRemoteWM6")](http://www.webguild.com/Tivo)

Much of the text and hyperlinks within the app may be updated by me
without requiring users to update their app. This is done by the app
downloading an XML file containing the text and other properties from a
website. I simply update the XML file and users will have the latest
text available to them. For example, one of the pages has a list of
resources and links to websites. I can easily add or update this list.
Also, there is a page of Headline News which I can update periodically
with new and interesting tips.

Development of the app is done using Microsoft’s Visual Studio. The code
is C\# and WP7 development is in Silverlight (xaml).

About 9 years ago, I wrote a similar app for the Windows Mobile 6 (image
on the right). This app also used network commands but it talked to the
old Series 1 TiVo using HTTP protocol to the web server that was set up
on the TiVo (TivoWeb).

For more information, click the images to get to the marketplace and the
app’s home page.

