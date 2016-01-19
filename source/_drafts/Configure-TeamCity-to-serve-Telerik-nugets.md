title: "Configure TeamCity to serve Telerik UI for WPF nugets"
permalink: "Configure-TeamCity-to-serve-Telerik-nugets"
date: 11/18/2014 11:02:26 PM
updated: 11/19/2014 7:37:18 PM
disqusIdentifier: 20141118110226
tags: ["Team City", "Telerik", "WPF"]
alias:
 - /post/Configure-TeamCity-to-serve-Telerik-nugets.aspx/index.html
---
Version control system like [Git](http://git-scm.com/) should not, in my humble opinion, store large binaries! However it was for too long what we were doing with the [Telerik UI for WPF](http://www.telerik.com/products/wpf/overview.aspx) and two smaller libraries.

I knew for quite some time that [TeamCity](https://www.jetbrains.com/teamcity/) offered the possibility to have [TeamCity as a NuGet Server](https://confluence.jetbrains.com/display/TCD8/NuGet). Then Telerik offered [Telerik UI for WPF as nuget packages](http://blogs.telerik.com/chriseargle/posts/12-10-16/nuget-or-not-for-telerik.aspx), so I finally took the time to have both working together to solve one thing I didn’t liked in our environment.
<!-- more -->

As always [Evgeniy Koshkin](https://twitter.com/lodkin) and [Eugene Petrenko](http://blog.jonnyzzz.name/) were of great help.

First you need to enable the NuGet Server functionality on TeamCity, by doing so

TBD

I have enabled the guest account to get a public NuGet feed, as the server is just in the LAN it is not a problem.

Then you will need to create a build which will simply get the Telerik NuGet packages from a folder and package those as artifacts of that build:

ADD SCREENSHOT

After extracting the Telerik NuGet packages to the folder you have chosen to use in your build, just run the build

Then you can add a NuGet source to your server and check that the NuGet packages are available.

ADD SCREENSHOT

Now to **recoverTBD **the nuget at build time you need to specify the following in your build

ADD SCREENSHOT
