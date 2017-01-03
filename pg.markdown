---
layout: default
title: "How I got Pinnacle to burn a DVD with audio"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 38
tags: [Personal]
---
Using Pinnacle Studio 11 (actually 11.1.1.5224) to create a DVD and then
burn (burn with Pinnacle or Nero), the resulting DVD had no sound.
Google search on the problem did not turn up much on this problem that
others have had. Some said the latest patch solved the problem but it
did not for me.

Pinnacle has a support article on this problem with no good solution.
However, one of the posts I read pointed to IFOEdit as a fix. I did have
good results with this technique.

First, create the DVD as an image on the hard drive but don't burn it.
Edit the IFO file. In the file I created, there were two IFO files:
VIDEO\_TS.IFO and VTS\_01\_0.IFO. The one to edit is VTS\_01\_0.IFO.
This only takes a minute.

Get the free current version
of [IFOEdit](http://www.videohelp.com/tools/IfoEdit) . Run it and click
the OPEN button on the bottom. Browse to your VTS\_01\_0.IFO file int he
VIDEO\_TS folder.

![](/images/blogs_webguild_com/gary/IfoEdit1.png)

What we want to do is change the audio from Mpeg-1 to Dolby AC-3. Locate
the line as shown (Movie attributes for the Mpeg-1 audio). Double click
the line to display the edit box and change Coding Mode from Mpeg to
Dolby AC-3 and click OK.

The change will not show - it still says Mpeg-1 but click to save it
anyhow (replace old version). A box will pop-up asking if you also want
to save as a .BUP. Say yes. If you reopen the file in IFOEdit, it will
now display the audio as Dolby.

The DVD can now be burned and will play the audio correctly.

