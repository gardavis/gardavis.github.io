---
layout: post
title: "How I Solved Comcast's Block of my SMTP (Email) Port 25"
date: 2008-05-21 -0800
comments: true
disqus_identifier: 18
tags: [Personal]
---
I received an email from Comcast telling me that they are blocking my
outgoing email:

> ***Dear Comcast Customer:***
>
> *ACTION REQUIRED: Comcast has determined that your computer(s) have
> been used to send unsolicited email ("spam"), which is generally an
> indicator of a virus. For your own protection and that of other
> Comcast customers, we have taken steps to prevent further transmission
> of spam from your computer(s).*

Comcast did provide information on configuring my email client to get it
to work. It's not too difficult if you are simply sending email, however
my setup is not normal. The fix is basically to modify the client to
send outgoing email using port 587 instead of the standard SMTP port 25.
Also, the port must be configured with authentication (my Comcast ID and
password).

For my situation, I run a home server to handle incoming and outgoing
email so for me the fix for outgoing email is not to my client which
talks to my email server (on port 25), but to fix the email server to
send out using port 587 authenticated.

That was the easy part. However, my wife said she had not received any
email for the last several days. I poked around and found out that
incoming port 25 was also being blocked. I was not able to connect to my
home server's port 25 from an external site (telnet debsrealty.com 25).
My wife has her own business domain for which email was directly sent to
the home server. This blockage
did not affect my email to webguild.com since the mail collects on that
hosted site and my home email server periodically picks up the mail via
POP3.

The solution is to use a different port than 25. However, there are
several steps to get this to work.

1.  My (dynamic) DNS name server is handled by sitelutions.com (free).
    They have a solution to redirect SMTP to a different port but costs
    \$29/yr. I found a free redirection from a different company
    ([www.rollernet.us](http://www.rollernet.us)). So the first step is
    to have Sitelutions redirect debsrealty.com email to
    mail.rollernet.us and mail2.rollernet.us with two "MX" records.  
     
    ![](/images/blogs_webguild_com/gary/SiteLutionsSmtp.png)
2.  Rollernet.us has this SMTP redirection free for a small amount of
    email (or \$40 for a larger amount). It will also do filtering so I
    set up to only redirect
    [deborah@debsrealty.com](mailto:deborah@debsrealty.com) email to
    debsrealty on port 2525. If you receive more email than the free
    account allows, combine step 1 and 2 and just go with the
    Sitelutions \$29/yr solution or check with your own nameserver
    company. 
     
    ![](/images/blogs_webguild_com/gary/RollernetSmtp.png)

3.  The 3rd step is to modify my router to accept incoming requests on
    port 2525 instead of 25. Also, the router configuration will route
    the requests to my home server on port 25 so I did not have to
    change the email server to listen on port 2525. I used
    [www.grc.com](http://www.grc.com) to verify port 25 was indeed
    blocked and 2525 was now open. 
     
    ![](/images/blogs_webguild_com/gary/RouterSmtp.png)

After this was all done, email started coming in for
[deborah@debsrealty.com](mailto:deborah@debsrealty.com). Messages sent
over the last few days often are retried by the various email transports
and were received. It's certainly possible that some were lost.

The rollernet site keeps a log of email transactions that is useful in
verifying functionality.
