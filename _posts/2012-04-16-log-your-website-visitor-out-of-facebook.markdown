---
layout: post
title: "Log Your Website Visitor Out of Facebook"
date: 2012-04-16 -0800
comments: true
disqus_identifier: 7
tags: [Programming]
---
One of my webs lets the user authenticate using the Facebook OAuth 2.0
Graph protocol. When the user clicks the Logout button, a call is made
(Http redirect) to Facebook to have it log the user off Facebook and my
site and then it returns to my site to display my page with the button
now showing *Login*instead of *Logout*. The user never sees any Facebook
page during the logout.

The way this works is to pass a parameter to Facebook that indicates the
url to return to when it is done. A few weeks ago, this stopped working.
Instead of returning to the specified url, Facebook logged out the user
but displayed its own page. It ignored the return url parameter.

The return parameter is specified as **next=**.

I posted a [Facebook
bug](http://bugs.developers.facebook.net/show_bug.cgi?id=17217) and
someone did reply with a solution. It did not immediately work for me
but with some experimentation, I found out the needed syntax.

This does work if you do it right. I tried some variations and some work
and some don't. By "work", I mean the redirect will log you out and it
will return to your url in the "next" parameter.

[](https://www.facebook.com/logout.php?next=[http://www.yoursite.com]&access_token=[current)[**https://www.facebook.com/logout.php?next=[http://www.yoursite.com]&access\_token=[current**](https://www.facebook.com/logout.php?next=[http://www.yoursite.com]&access_token=[current)**\_token****]**

1.  Use **https**, not **http** - it won't return if you use http (for
    facebook.com)
2.  Supply the **access\_token** parameter - it won't return if omitted
3.  Both **www**.facebook.com and **m**.facebook.com appear to work
4.  Supply or omit the **&confirm=1** parameter (some folks mentioned
    it). It worked either way
5.  UrlEncode the **next** parameter if necessary (contains question
    marks, ampersands, equal signs, etc.)
6.  I passed **&next=****http://localhost:5000/** - final slash is not
    required but recommended.


