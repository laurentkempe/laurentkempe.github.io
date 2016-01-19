title: "The beauty of C# and Linq"
permalink: "The-beauty-of-C-and-Linq"
date: 1/26/2010 5:57:12 AM
updated: 1/26/2010 5:57:12 AM
disqusIdentifier: 20100126055712
tags: ["C#", "Linq"]
alias:
 - /post/The-beauty-of-C-and-Linq.aspx/index.html
---
Today I faced the following challenge to solve: return all possible combinations of three source collections.

We are using C# and with Linq it was just so easy.
<!-- more -->
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:9ce6104f-a9aa-4a17-a79f-3a39532ebf7c:4d864d53-59b3-4fa4-abf7-37489ccb240f" class="wlWriterEditableSmartContent"> <div style="border: #000080 1px solid; color: #000; font-family: 'Courier New', Courier, Monospace; font-size: 10pt"> <div style="background: #fff; max-height: 300px; overflow: auto"> 

1.  <span style="color:#0000ff">public</span> <span style="color:#2b91af">List</span><<span style="color:#0000ff">string</span>> Contexts
2.  {
3.      <span style="color:#0000ff">get</span>
4.      {
5.          <span style="color:#0000ff">var</span> result = <span style="color:#0000ff">from</span> u <span style="color:#0000ff">in</span> SelectedUseCases
6.                       <span style="color:#0000ff">from</span> c <span style="color:#0000ff">in</span> SelectedChannels
7.                       <span style="color:#0000ff">from</span> up <span style="color:#0000ff">in</span> SelectedUserProfiles
8.                       <span style="color:#0000ff">select</span> <span style="color:#0000ff">string</span>.Format(<span style="color:#a31515">"{0}-{1}-{2}"</span>, u.Value, c.Value, up.Value);
9.   
10.          <span style="color:#0000ff">return</span> result.ToList();
11.      }
12.  } </div> </div> </div>  

Simple and beautiful!
