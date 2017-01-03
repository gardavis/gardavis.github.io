---
layout: post
title: "How to Enable jQuery Intellisense in Your MVC 3 Razor Code"
date: 2012-04-16 -0800
comments: true
disqus_identifier: 6
tags: [Programming]
---
You probably include your \<script\> to pull in the jQuery JavaScript in
your layout.cshtml (master page in Razor), perhaps something like this:

```html
<script src="http://ajax.aspnetcdn.com/ajax/jquery/jquery-1.6.2.min.js" type="text/javascript"></script>
```

```csharp
 
```

But your code pages that use jQuery do not show Intellisense. To enable
Intellisense, add this to the top of the pages so Visual Studio has a
reference to the vsdoc which is hosted by the Microsoft CDN:

```csharp
@if (false) {<script src="http://ajax.aspnetcdn.com/ajax/jquery/jquery-1.6.2.min.js" type="text/javascript" />}
```

```csharp
 
```

The if statement will prevent the script tag from being emitted to the
browser since it is only needed for Visual Studio
development.[![jquery](/images/blogs_webguild_com/gary/Windows-Live-Writer/How-to-enable-Intellisense_EE4A/jquery_thumb.png "jquery")](/images/blogs_webguild_com/gary/Windows-Live-Writer/How-to-enable-Intellisense_EE4A/jquery_2.png)

It is not necessary to specify the path to the vsdoc file since Visual
Studio knows to look for the vsdoc in the same location and use it if it
finds it.

The Intellisense is shown based on deleting then typing the open paren
at the point indicated.

BTW, the **\$(function()** at the top of the example is a common
shorthand for **\$(document).ready(function()**.

The CDN used is the [Microsoft Ajax Content Delivery
Network](http://www.asp.net/ajaxlibrary/cdn.ashx) and they changed the
domain from ajax.microsoft.com to ajax.aspnetcdn.com to improve
performance and prevent microsoft.com cookie transmission.

The CDN also has the files for the jQueryUI .js and .css for the themes.

```csharp
<link type="text/css" rel="Stylesheet" 
```

```csharp
    href="http://ajax.aspnetcdn.com/ajax/jquery.ui/1.8.14/themes/redmond/jquery-ui.css" />
```

```html
<script type="text/javascript" 
```

```csharp
    src="http://ajax.aspnetcdn.com/ajax/jquery.ui/1.8.14/jquery-ui.min.js"></script>
```

```csharp
 
```

Note that the current versions of these files at this time is 1.6.2 for
jQuery and 1.8.14 for jQueryUI.

