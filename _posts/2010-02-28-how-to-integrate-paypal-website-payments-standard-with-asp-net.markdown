---
layout: post
title: "How to Integrate PayPal Website Payments Standard with ASP.Net"
date: 2010-02-28 -0800
comments: true
disqus_identifier: 9
tags: [Programming]
---
Yesterday was the [South Florida Code Camp
2010](http://www.fladotnet.com/codecamp/) in Miramar (that’s between
Miami and Ft. Lauderdale). I gave a presentation on integrating PayPal
Website Payments Standard with ASP.Net C\#. I included a [demo web
application](http://www.webguild.com/Codecamp2010/) showing four
different options to program the application though from the buyer’s
point of view, all four examples looked and acted the
same.

[![CodeCampImage1](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowtoIntegratePayPalWebsitePaymentsS.Net_AC50/CodeCampImage1_5.png "CodeCampImage1")](http://www.webguild.com/CodeCamp2010/ "Gary's Test Store"){: .left}
PayPal standard is the familiar option that displays PayPal buy-buttons
to the buyer and when clicked, control is transferred to PayPal for the
buyer to complete the payment and hopefully return to the website.

Each Buy Now button is a \<form\> with some hidden \<input\> fields and
the button \<img\>. The four examples show different ways to implement
or create the \<form\> fields. The first two examples redirect directly
to PayPal as specified by the form’s action parameter and the last two
examples post to an aspx page that controls building the post form to
cause the redirect to PayPal.

-   **Example 1** – This page builds the form and fields and may be seen
    with a View Source. This is easy and can be dynamically built by the
    code but may be hacked by a user that can copy and modify the page
    source (like the amount field) to buy your product or service at
    whatever price they want. Automated fulfillment sites may miss this
    fraudulent purchase.
-   **Example 2** – The seller used PayPal’s button factory to build a
    hosted button. This solves the security issue but at the expense of
    the dynamic nature of the form field generation and the issue of
    manually having to create a button for every product of your
    inventory. View Source shows the main field in the form is the
    identifier of the hosted button.
-   **Example 3** – In this example, clicking the button does not sent
    the buyer to PayPal immediately (though it appears that way to the
    buyer). View source will only show the product’s ID is passed in the
    form which calls PayPalRedirector.aspx. The aspx page looks up the
    product in the database to get its name, price, etc. and builds the
    html needed by PayPal (much the same as seen in Example 1. It pushes
    this html to the buyer’s browser with an automatic form submit. This
    is a bit more secure than Example 1 but a knowledgeable user can
    capture the generated html to forge a similar fraudulent order.
-   **Example 4** – This final example solve the hackability problem and
    still allows dynamic buttons to be generated. The button form is
    generated as in Example 3 but is encrypted before sending the
    redirect form to the buyer’s browser. This does require that the
    seller obtain an encryption certificate and upload the public key to
    PayPal so PayPal can decrypt your button.

The PayPalRedirector.aspx code used in Examples 3 and 4 used a class
library (PayPalStdLib) I wrote to allow easy strongly-typed access to
build and initialize the object with the payment parameters and a method
to initiate the redirect to PayPal. This is a bare-bones class you can
enhance with additional properties as needed for your own use.

The presentation was the last of the day but was well attended by a
lively group who had many questions. See my article about 
[PayPal Encrypted Website Payments](http://webguild.dyndns.org/Blog/archive/2008/08/29/how-to-create-dynamic-encrypted-website-payments-ewp-paypal-buttons.aspx)
for additional information about that part of the code in Example 4.
Source code and PowerPoint slides are available at
[http://code.msdn.microsoft.com/webguild](http://code.msdn.microsoft.com/webguild).

Plug: Webguild does PayPal development, integration and consultation
including full-blown PayPalStdLib and PayPalProLib class libraries.
