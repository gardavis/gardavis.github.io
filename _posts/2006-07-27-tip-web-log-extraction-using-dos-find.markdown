---
layout: post
title: "Tip: Web log extraction using DOS FIND"
date: 2006-08-27 -0800
comments: true
disqus_identifier: 19
tags: [Personal]
---
Here’s a useful trick for working with the huge web log files.  

Use the DOS "find" command to extract the records of interest, usually
an IP works but a timestamp could also. Then you wind up with a smaller
subset file that is easier to work with. Find is like the Unix grep.

  D:\\usage\\W3SVC242754246\>find "203.217.13.46" ex051201.log \> x.txt

  ---------- EX051201.LOG

2005-12-01 06:43:39 W3SVC242754246 ALLXLWS1 12.8.2.161 GET /WXLogin.htm
- 80 - 203.217.13.46 HTTP/1.1
Mozilla/4.0+(compatible;+MSIE+6.0;+Windows+NT+5.0;+.NET+CLR+1.0.3705;+.NET+CLR+1.1.4322)
si=webxmi - webxmi.xent.com 200 0 0 1852 427 328

2005-12-01 06:43:47 W3SVC242754246 ALLXLWS1 12.8.2.161 POST
/WebXM/Login.aspx url=/Default.aspx 80 - 203.217.13.46 HTTP/1.1
Mozilla/4.0+(compatible;+MSIE+6.0;+Windows+NT+5.0;+.NET+CLR+1.0.3705;+.NET+CLR+1.1.4322)
si=webami;+sdc\_standard\_pool=2701264908.20480.0000
http://webxmi.xent.com/WXLogin.htm webxmi.xent.com 302 0 0 814 722 390
