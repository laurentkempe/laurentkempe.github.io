title: "ASP.NET MVC 2, MSpec and Watin"
permalink: "ASPNET-MVC-2-MSpec-and-Watin"
date: 5/19/2010 5:07:53 PM
updated: 10/15/2010 11:20:48 AM
disqusIdentifier: 20100519050753
tags: ["Watin", "MSpec", "Jobping"]
alias:
 - /post/ASPNET-MVC-2-MSpec-and-Watin.aspx/index.html
---
The other day I posted about “[Automated functional tests using Watin and MSpec](http://www.laurentkempe.com/post/Automated-functional-tests-using-Watin-and-MSpec.aspx)” which we do at [Jobping](http://www.jobping.com) as a spike to automate our functional tests on our ASP.NET MVC 2 site.

Yesterday evening I was facing an issue in my base class **WebBaseSpec** which led to really strange side effects. Basically when I was running one unit test alone it was Green, running all or more than one unit test will fail miserably with the well known STA issue of [Watin](http://watin.sourceforge.net/).
<!-- more -->

So I thought that I had an issue with the ReSharper MSpec plugin but after some discussion with [Alexander Groß](http://therightstuff.de/)I realized that the second failing test was showing another issue than the STA issue.

Going further I realized that when I was checking the following
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:9ce6104f-a9aa-4a17-a79f-3a39532ebf7c:14430a2e-0f58-4214-af6d-145c4a32c3fc" class="wlWriterEditableSmartContent"> <div style="border: #000080 1px solid; color: #000; font-family: 'Courier New', Courier, Monospace; font-size: 10pt"> <div style="background-color: #ffffff; overflow: auto; padding: 2px 5px; white-space: nowrap"><span style="color:#2b91af">It</span> should_direct_user_to_aboutus_page = () =>   
     Browser.Uri.Route().ShouldMapTo<<span style="color:#2b91af">HomeController</span>>(x => x.About());</div> </div> </div>  

First I needed to call the ASP.NET MVC RegisterRoutes
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:9ce6104f-a9aa-4a17-a79f-3a39532ebf7c:63124e7b-4b0d-44a3-9dd6-20be9d9ff0c8" class="wlWriterEditableSmartContent"> <div style="border: #000080 1px solid; color: #000; font-family: 'Courier New', Courier, Monospace; font-size: 10pt"> <div style="background-color: #ffffff; overflow: auto; padding: 2px 5px; white-space: nowrap"><span style="color:#2b91af">MvcApplication</span>.RegisterRoutes(<span style="color:#2b91af">RouteTable</span>.Routes);</div> </div> </div>  

which was done in the constructor of my **WebBaseSpec** class.
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:9ce6104f-a9aa-4a17-a79f-3a39532ebf7c:80e0035c-f154-4262-8d7b-af068a5a4e60" class="wlWriterEditableSmartContent"> <div style="border: #000080 1px solid; color: #000; font-family: 'Courier New', Courier, Monospace; font-size: 10pt"> <div style="background-color: #ffffff; overflow: auto; padding: 2px 5px; white-space: nowrap"><span style="color:#0000ff">protected</span> WebBaseSpec()  
 {  
     <span style="color:#2b91af">MvcApplication</span>.RegisterRoutes(<span style="color:#2b91af">RouteTable</span>.Routes);  
     InitBrowser();  
 }</div> </div> </div>  

That’s was the problem, I was registering the routes several time, one time per test. So first one was ok, second one was failing…

So I modified it to the following, ensuring that the routes were registered only one time!
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:9ce6104f-a9aa-4a17-a79f-3a39532ebf7c:126789d7-ff2e-4236-85fa-f3a3e257f937" class="wlWriterEditableSmartContent"> <div style="border: #000080 1px solid; color: #000; font-family: 'Courier New', Courier, Monospace; font-size: 10pt"> <div style="background-color: #ffffff; overflow: auto; padding: 2px 5px; white-space: nowrap"><span style="color:#0000ff">private</span> <span style="color:#0000ff">static</span> <span style="color:#0000ff">bool</span> registered;  

 <span style="color:#808080">///</span><span style="color:#008000"> </span><span style="color:#808080"><summary></span>  
 <span style="color:#808080">///</span><span style="color:#008000"> Initializes a new instance of the </span><span style="color:#808080"><see cref="WebBaseSpec"/></span><span style="color:#008000"> class.</span>  
 <span style="color:#808080">///</span><span style="color:#008000"> </span><span style="color:#808080"></summary></span>  
 <span style="color:#0000ff">protected</span> WebBaseSpec()  
 {  
     <span style="color:#0000ff">if</span> (!registered)  
     {  
         <span style="color:#2b91af">MvcApplication</span>.RegisterRoutes(<span style="color:#2b91af">RouteTable</span>.Routes);  
         registered = <span style="color:#0000ff">true</span>;  
     }  
     InitBrowser();  
 }</div> </div> </div>  

Now I can run all my functional tests again

![4621024158_d2c99039a0_o[1]](/images/4621024158_d2c99039a0_o%5B1%5D.png "4621024158_d2c99039a0_o[1]")
