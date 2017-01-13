---
layout: post
title: "How I Enabled HTTP Compression on my IIS6 Windows Server 2003"
date: 2007-11-25 -0800
comments: true
disqus_identifier: 17
tags: [Personal]
---
IIS6 supports HTTP compression of the responses sent back to user's
browsers but it needs to be enabled for this to be effective. Completely
enabling compression is not obvious and if you think you are enabling
compression by simply checking the  "Enable" checkboxes on the Internet
Service Manager (ISM) you probably are in for a surprise.

These are the steps I used to get compression working and verify that
what I did actually worked. I used the steps described in this
[DotNetJunkies
link](http://www.dotnetjunkies.com/howto/16267d49-4c6e-4063-ab12-853761d31e66.dcik)
as my starting point. To verify that compression is working as expected
on your server, use [PipeBoost.com](http://www.pipeboost.com/) to
request the page or the file and review its response (compressed or
not). Another way is to use [Fiddler](http://www.fiddlertool.com) to
look at the HTTP headers sent to and returned from the web server.

You will have to edit the IIS metabase to add the file types to the
existing list for compression. To allow you to edit the metabase while
IIS is running, you have to enable editing of the Metabase in the ISM.
Right-click the Server-\>Properties-\>Enable Direct Metabase Edit. Check
the box and click OK.

![Server Properties](/images/blogs_webguild_com/gary/Ism1.png)

Now right-click Web Sites-\>Properties-\>Services tab.

![Service tab in web site
properties](/images/blogs_webguild_com/gary/Ism2.png)

This shows I have chosen to compress both dynamic (application) and
static files. I left the temp directory (used for caching compressed
versions of the static files) as the default. I also limited my cache
size. Change these if desired. There is some overhead in checking to
compress dynamic files since each web page request will require some
processing time to save in bandwidth.

By default, the important file types are not compressed (.aspx, .css,
.js, etc) so we will add these types with the metabase edit shortly.

Next, select the Web Service Extensions and add a new extension to
identify the gzip.dll. By convention, I called this Http Compression and
the location of the dll is in your Windows folder
\\System32\\inetsrv\\gzip.dll as shown below. Set the checkbox to allow
and click OK.

![Web Services Property to add Http
Compression](/images/blogs_webguild_com/gary/ISM3.png%20)

 Now we can edit the Metabase. Navigate to the same inetsrv folder from
above. For safety, make a copy of the MetaBase.xml file. Edit with your
favorite editor. Find the section for **gzip** (not the one for
**deflate**) and add the lines highlighted: 

![Edit Metabase to add
types](/images/blogs_webguild_com/gary/MetaBaseEdit.png)

The lines added have tabs followed by the types on separate lines. Save
the file.

The final step is to do an IISRESET. This forces IIS to re-load the
edited Metabase.xml and enable the compression.

You can now go to the PipeBoost.com site and enter your URL to verify
that it displays that the page Document Status is **Compressed**. You
can individually try an aspx page and a css or js page to make sure both
dynamic and static pages are compressed. You can also start up Fiddler
and browse to your page and verify the components are compressed. The
browser must tell the server that it can handle compression (most
current popular browsers) with a header 

![Fiddler displays request and response headers showing gzip
used](/images/blogs_webguild_com/gary/FiddlerHeaders.png)

If you don't see the Content-Encoding: gzip response header for the
file, compression is not correctly enabled.

You can also use Fiddler to see what the size of the request would be
both compressed or not by changing the radion button: 

![Fiddler Transformer
tab](/images/blogs_webguild_com/gary/FiddlerTransformer.png)
