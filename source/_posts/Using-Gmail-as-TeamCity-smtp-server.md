title: "Using Gmail as TeamCity smtp server"
permalink: "Using-Gmail-as-TeamCity-smtp-server"
date: 6/1/2010 6:57:29 AM
updated: 9/17/2010 9:56:49 PM
disqusIdentifier: 20100601065729
tags: ["Team City", "Jobping"]
alias:
 - /post/Using-Gmail-as-TeamCity-smtp-server.aspx/index.html
---
Some time ago when I had to reinstall our [Jobping](http://www.jobping.com) Continuous Integration server, which is [Team City](http://www.jetbrains.com/teamcity/?fromServer) I also decided not to reinstall any smtp server but to use Gmail server.

Here is the configuration that I used, which worked perfectly for me
<!-- more -->

![4656773327_09a7eed279_o[1]](/images/4656773327_09a7eed279_o%5B1%5D.png "4656773327_09a7eed279_o[1]") 

Use SMTP port 465 and TLS (SSL) !
