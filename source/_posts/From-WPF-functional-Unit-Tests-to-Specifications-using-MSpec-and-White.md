title: From WPF functional Unit Tests to Specifications using MSpec and White
date: 6/11/2010 3:21:22 AM
updated: 6/13/2010 8:09:10 PM
tags: ["white", "WPF", "unit test", "MSpec"]
---
I am in the train back home and wanted to try out quickly to migrate our WPF functional tests written has Unit Tests to BDD Specifications. 

Here is the code I started from, pure Unit Test using NUnit and White
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:9ce6104f-a9aa-4a17-a79f-3a39532ebf7c:4955d68a-7a42-4fa8-bd02-2ff18f2492fe" class="wlWriterEditableSmartContent"> <div style="border: #000080 1px solid; color: #000; font-family: 'Courier New', Courier, Monospace; font-size: 10pt"> <div style="background-color: #ffffff; max-height: 500px; overflow: auto; padding: 2px 5px; white-space: nowrap">[<span style="color:#2b91af">Test</span>]  
 <span style="color:#0000ff">public</span> <span style="color:#0000ff">void</span> Opening_Valid_VersionZip()  
 {  
     OpenAndWait(<span style="color:#a31515">"Product.zip"</span>);  

     <span style="color:#2b91af">Assert</span>.That(MainWindow.Title.Equals(<span style="color:#a31515">"Product.zip - Innoveo Skye® Editor"</span>));  
     <span style="color:#2b91af">Assert</span>.That(Status.Text.Equals(<span style="color:#a31515">"product"</span>));  
     <span style="color:#2b91af">Assert</span>.That(ProductTree.Nodes.Count >= 1);  
     <span style="color:#2b91af">Assert</span>.IsFalse(SplashScreen.Visible);  
     <span style="color:#2b91af">Assert</span>.IsTrue(SaveButton.Enabled);  
     <span style="color:#2b91af">Assert</span>.IsTrue(ActivateButton.Enabled);  
 }</div> </div> </div>  

Now the same functional test written as a BDD specification using MSpec

  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:9ce6104f-a9aa-4a17-a79f-3a39532ebf7c:434f1161-ac6a-49fc-8c62-127913130898" class="wlWriterEditableSmartContent"> <div style="border: #000080 1px solid; color: #000; font-family: 'Courier New', Courier, Monospace; font-size: 10pt"> <div style="background-color: #ffffff; max-height: 500px; overflow: auto; padding: 2px 5px;">[<span style="color:#2b91af">Subject</span>(<span style="color:#a31515">"OpenVersionZip"</span>)]  
 <span style="color:#0000ff">public</span> <span style="color:#0000ff">class</span> <span style="color:#2b91af">when_user_open_valid_versionzip</span> : <span style="color:#2b91af">MainWindowViewSpecs</span>  
 {  
     <span style="color:#2b91af">Establish</span> context = () => {};  

     <span style="color:#2b91af">Because</span> of = () => OpenAndWait(<span style="color:#a31515">"Product.zip"</span>);  

     <span style="color:#2b91af">It</span> should_display_mainwindow_title_correctly = () =>   
         MainWindow.Title.ShouldEqual(<span style="color:#a31515">"Product.zip - Innoveo Skye® Editor"</span>);  

     <span style="color:#2b91af">It</span> should_display_status_correctly = () =>   
         Status.Text.ShouldEqual(<span style="color:#a31515">"product"</span>);  

     <span style="color:#2b91af">It</span> should_display_the_product_tree = () =>   
         ProductTree.Nodes.ShouldNotBeNull();  

     <span style="color:#2b91af">It</span> should_hide_the_splashscreen = () =>   
         SplashScreen.Visible.ShouldBeFalse();  

     <span style="color:#2b91af">It</span> should_enable_save_button = () =>   
         SaveButton.Enabled.ShouldBeTrue();  

     <span style="color:#2b91af">It</span> should_enable_activate_button = () =>   
         ActivateButton.Enabled.ShouldBeTrue();  
 }</div> </div> </div>  

And the output in ReSharper MSpec plugin

![4687909611_49a4e5a71a_o[1]](http://www.laurentkempe.com/image.axd?picture=4687909611_49a4e5a71a_o%5B1%5D.png "4687909611_49a4e5a71a_o[1]") 

Which one do you prefer? I personally have made my choice.
