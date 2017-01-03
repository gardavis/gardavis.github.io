---
layout: post
title: "How to Suppress Google AdSense (Syndication) for SSL Https Pages"
date: 2012-04-16 -0800
comments: true
disqus_identifier: 8
tags: [Programming]
---
Google AdSense is not supported for https ([see
here](https://www.google.com/adsense/support/bin/answer.py?hl=en&answer=10528)).
If you attempt to use it on an SSL page, you will see this warning in
IE8.[![Image1](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowtoSuppressGoogleAdsenseSyndicationfor_B0ED/Image1_thumb.png "Image1")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowtoSuppressGoogleAdsenseSyndicationfor_B0ED/Image1_2.png)
The user would have to click No to allow the request (for a .js file in
this case) to complete. Answering Yes will block it (the wording seems
backwards from what you’d expect).

Some postings I saw said to change the .js url in the script to use
https://pagead2.googleadservices.com/pagead/show\_ads.js but while this
will work for this one .js file, the script then attempts to pull in
other .js files using http so you still get the warning popup.

The best solution is to not let the warning pop up on your secure pages.

This is the standard AdSense code:

> \<script type="text/javascript"\> 
>      if ("http:" == document.location.protocol) { 
>       google\_ad\_client = "pub-1234567890123456"; 
>       google\_ad\_slot = "1234567890"; 
>       google\_ad\_width = 728; 
>       google\_ad\_height = 90; 
>       google\_ad\_format = "728x90\_as"; 
>      } 
>  \</script\>
>
> \<script type="text/javascript"
> src="[http://pagead2.googlesyndication.com/pagead/show\_ads.js](http://pagead2.googlesyndication.com/pagead/show_ads.js)"\>\</script\>
> 
This is the new version that will suppress the AdSense code and prevent
the popup on your SSL pages. Simply insert the
**document.write**statement and remove the second script.

> \<script type="text/javascript"\> 
>      if ("http:" == document.location.protocol) { 
>       google\_ad\_client = "pub-1234567890123456"; 
>       google\_ad\_slot = "1234567890"; 
>       google\_ad\_width = 728; 
>       google\_ad\_height = 90; 
>       google\_ad\_format = "728x90\_as"; 
>       document.write(unescape( 
>          "%3Cscript
> src='http://pagead2.googlesyndication.com/pagead/show\_ads.js'
> type='text/javascript' %3E%3C/script%3E")); 
>      } 
>  \</script\>

This fix uses the existing conditional block for non-SSL pages that
initializes some google\_ad variables to also emit a \<script\> element
to pull in the necessary show\_ads.js file. For SSL pages, the variables
will not be initialized and the script will not be emitted for the page.

