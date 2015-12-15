title: Limit issues with Eclipse when using VisualSVN/TortoiseSVN
date: 1/7/2010 9:56:00 PM
updated: 1/7/2010 9:56:00 PM
tags: [""]
---
In some rare case I have to use Eclipse configured to access our [Innoveo Solutions](http://www.innoveo.com/) svn server. I also for sure have Visual Studio 2008 with VisualSvn installed which install TortoiseSvn.

Today I faced the following crazy issue, from a file browse window opened through Eclipse, I saw that one file was modified so I did from that file browse window a svn revert using TortoiseSvn which ended to a crazy situation in Eclipse. It was totally messed up.

So to avoid this, I configured [TortoiseSvn Exclude Paths](http://tortoisesvn.net/docs/nightly/TortoiseSVN_en/ch05s25.html) not to show me this folder and subfolder with icon overlays:

[![4253062219_8a93a90c4d_o[1]](http://weblogs.asp.net/blogs/lkempe/4253062219_8a93a90c4d_o1_thumb_54E797AB.png "4253062219_8a93a90c4d_o[1]")](http://weblogs.asp.net/blogs/lkempe/4253062219_8a93a90c4d_o1_250CF5EA.png) 

I hope this will save me from those crazy situations!
