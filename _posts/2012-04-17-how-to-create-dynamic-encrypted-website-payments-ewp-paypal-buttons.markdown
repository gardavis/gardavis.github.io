---
layout: post
title: "How to create dynamic Encrypted Website Payments (EWP) PayPal buttons"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 25
tags: [Programming]
---
If you want to sell something on your website, perhaps something like a
personalized kid's storybook, you can add a PayPal buy-button that will
send the user to PayPal to make a payment to your PayPal account. You
will get an email and then you can create and send the book to the
buyer.

The Html code that makes up the button (created manually or from the
PayPal button factory) contains things like your PayPal account email,
the item description and price and perhaps a few other parameters.
However, someone knowledgeable could view the source of your page or
save the Html from the browser, change the price and then click the
modified button and you will receive the order with a lower payment.
Maybe you will notice it but if you get lots of orders for various
items, it may go unnoticed until after you send the book.

The solution is to use PayPal's Encrypted Website Payments (EWP)
buttons. This can be done by the button factory and you can set a flag
in the profile to only allow encrypted buttons to be used on your site.
People will no longer be able to modify your buttons in any way. All the
parameters that make up the button are encrypted into one string of
characters and that string is sent as a single parameter to PayPal when
the button is clicked. When created by the factory, PayPal knows how to
decrypt what it encrypted in the first place.

However, what if you want to dynamically generate your buy-buttons in
your code? You can create the parameters as you need on the fly and use
them unencrypted but if you want to encrypt them, you can't use the
factory. For example, the personalized book's item description could be
"Billy Jones and the Magic Pancake" which will display when the buyer
enters PayPal to pay. Dynamic buttons are also useful when you have a
database with lots of items. Once you create the set of parameters for
the button, you can then run the string through an encryption routine
and use the encrypted string in your buy button. The PayPal site
explains how to do this
([link](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&content_ID=developer/e_howto_html_encryptedwebpayments#id08A3I0P017Q)).

There are several steps to do this as discussed in the link above:

1.  Obtain a private key and public certificate - You use your private
    key to decrypt something encrypted by your public cert. Public certs
    are used for encryption and authentication. 
     
2.  Upload your public cert to PayPal - You then give away your public
    certificate to anyone that needs to authenticate that you are you or
    encrypt data to send to you. In this case, you upload your public
    cert to PayPal. Actually, PayPal does not need to send you anything
    encrypted so they mainly need your public cert for authentication.
    There are other non-PayPal uses of this private key/public cert pair
    like encrypted email but I will discuss that in a future posting. 
     
3.  Downloading PayPal's public cert - PayPal has two certs, one for the
    live PayPal site and one for the PayPal sandbox (or beta sandbox).
    You use PayPal's cert to encrypt the buy-button parameters. PayPal
    provides links for you do download their certs. Certs are created
    with an expiration date. In PayPal's case, their certs will expire
    in 2035.
     
4.  Set your PayPal profile to only allow encrypted buttons. 
For testing purposes, I have created a simple
[tool](http://www.webguild.com/PayPal.aspx) to do steps 1 and 3. This
will allow you to create your private key, public cert and have both
PayPal public certs and provide them to you in a zip file. Once you have
your development working, you can then go through the steps to recreate
your key and cert and re-upload to PayPal but you will have to install
[OpenSSL](http://www.openssl.org/) on your PC. This way you know you are
the only one that has your private key. Using the private key from my
tool in production will certainly work but it did originate from my
computer.

![Form to request cert](/images/blogs_webguild_com/gary/GetCert.jpg)

Click the Buy Now and after some seconds, if you selected the Free cert,
a link will display to download the zip file and if you selected a
longer expiration date, you will first pay through PayPal and then
return to click the zip download. This is the file:

![](/images/blogs_webguild_com/gary/CertZip.jpg)

The image shows the two PayPal public certs, the Pkcs12.p12 file, your
private key (keep this secure) and your public cert (to give away). The
Readme.txt file has some hints and information on the OpenSSL commands
used to create these files. The p12 file is used by your code that
generates your encrypted buttons. This file also should be kept secure
since it contains both your private key and public cert.

The tool to create your private key and public cert is at
[http://paypal.webguild.com/](http://paypal.webguild.com/) (click the
Certs and Keys tab). This page actually uses a PayPal buy button that
uses a dynamic EWP button if you select the non-free option. The item
name and price is encrypted and you will notice the personalized item
name when you arrive on the PayPal site.

