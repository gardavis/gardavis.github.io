---
layout: post
title: "How I Blocked Spam Coming Into my Home Email Server"
date: 2012-04-17 -0800
comments: true
disqus_identifier: 35
tags: [Personal]
---
Some time ago, I blogged about setting up my home email server to
support incoming email using the Rollernet.us service ([How I Solved
Comcast's Block of my SMTP (Email) Port
25](http://webguild.dyndns.org/Blog/archive/2008/05/21/how-i-solved-comcasts-block-of-my-smtp-port-25.aspx "How I Solved Comcast's Block of my SMTP (Email) Port 25")).
Most of my incoming email is through the webguild.com site but in this
case, it is business-related email for my wife’s site,
[www.debsrealty.com](http://www.debsrealty.com) which is hosted by the
same home server.

The Webguild email was spam-filtered fairly effectively but the email
coming in to Debsrealty via Rollernet was leaking lots of Canadian
pharmacy and other spam. Lots of this spam is originating from some
network of infected computers like the [Waledac
botnet](http://www.crn.com/security/223100744)). These spam emails are
very difficult to block using the Outlook rules so I logged on to the
Rollernet account to see what they offered for spam filtering support.
It turns out there is pretty good support.

There five filtering options available. 
[![RollernetFiltering](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIBlockedSomeSpamComingIntomyHomeEmail_AA6E/RollernetFiltering_thumb.png "RollernetFiltering")](/images/blogs_webguild_com/gary/WindowsLiveWriter/HowIBlockedSomeSpamComingIntomyHomeEmail_AA6E/RollernetFiltering_2.png)I
had not configured any of them but two of the five were already enabled
([DNSBL](https://acc.rollernet.us/help/mail/dnsbl.php) and
[SPF](https://acc.rollernet.us/help/mail/spf.php)). I then turned on two
of the remaining three options
([Greylisting](https://acc.rollernet.us/help/index.php#grey) and
[Anti-Virus](https://acc.rollernet.us/help/index.php#antivirus)) to see
if that solved the primary problems. Greylisting keeps track of incoming
emails looking at three things (sender’s IP, From and To). If it is new,
it replies to the sender to retry later. Normal senders will retry but
spambots don’t bother. Retries are passed on by the filter and it
remembers so future email with the same “triplet” are pass without
delay. This technique is very effective and did successfully block all
of the *pharmacy* spam that Deborah was receiving. There are logs of all
incoming email kept by Rollernet to see whether or not an email was
filtered and why.

The final option is the
[SpamAssassin](https://acc.rollernet.us/help/mail/spamassassin.php)
filter which looks at the content to see if it can recognize spam and
add **\*\*SPAM**at the start of the Subject of suspicious emails (easily
checked by Outlook rules). SpamAssassin assigns a score to each email on
how certain (on not) it is that the email is spam. Then you specify the
score that you want to use and if an email has a higher score than your
threshold, it will be flagged as mentioned (or you can block it). I may
enable this if Deborah gets more spam not blocked by the other methods.

