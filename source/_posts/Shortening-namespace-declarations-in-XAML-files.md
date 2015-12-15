title: Shortening namespace declarations in XAML files
date: 12/15/2011 2:49:43 AM
updated: 12/15/2011 7:30:59 AM
tags: ["WPF", "Silverlight"]
---
[![Vue sur la tête de la femme couchée de la terrasse de la villa cannelle](http://farm6.staticflickr.com/5190/5563773074_38938ee129_m.jpg)](http://www.flickr.com/photos/laurentkempe/5563773074/ "Vue sur la tête de la femme couchée de la terrasse de la villa cannelle by Laurent Kempé, on Flickr")This afternoon I was working on [Innoveo](http://www.innoveo.com/) [Skye Editor](http://www.innoveo.com/SoftwareSolution.aspx) which is a WPF application written in C#. 

The application is using [Telerik RadControls for WPF](http://www.telerik.com/products/wpf.aspx). 

I was facing the issue of having more and more namespace declarations like the following for **RadInput** and **Rad**:

<span style="color: blue"><</span><span style="color: #a31515">Window </span><span style="color: red">x</span><span style="color: blue">:</span><span style="color: red">Class</span><span style="color: blue">="skyeEditor.View.Dialogs.ProductSettingsDialog"
        </span><span style="color: red">xmlns</span><span style="color: blue">="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        </span><span style="color: red">xmlns</span><span style="color: blue">:</span><span style="color: red">x</span><span style="color: blue">="http://schemas.microsoft.com/winfx/2006/xaml"
        </span><span style="color: red">xmlns</span><span style="color: blue">:</span><span style="color: red">RadInput</span><span style="color: blue">="clr-namespace:Telerik.Windows.Controls;assembly=Telerik.Windows.Controls.Input"
        </span><span style="color: red">xmlns</span><span style="color: blue">:</span><span style="color: red">Rad</span><span style="color: blue">="clr-namespace:Telerik.Windows.Controls;assembly=Telerik.Windows.Controls"
</span>

Searching for a solution I thought of ASP.NET in which you can declare in the web.config things like that:

> <pages pageBaseType="System.Web.Mvc.WebViewPage">
>   <namespaces>
>     <add namespace="MyNamespace" />

My goal was to have one namespace declaration for example **telerik** and be able to use it in all my XAML files without having to declare too much. 

So I started an online discussion with [Laurent Bugnion](http://www.galasoft.ch/intro_en.html) who has always shown me the good direction, which in this case is the 

> ### [XmlnsDefinitionAttribute](http://msdn.microsoft.com/en-us/library/system.windows.markup.xmlnsdefinitionattribute.aspx) Class

Followed by an article from [Sandino Di Mattia](http://blog.sandrinodimattia.net/) about “[A Guide to Cleaner XAML with Custom Namespaces and Prefixes (WPF/Silverlight)](http://www.codeproject.com/KB/silverlight/xaml_custom_namespaces.aspx?adcid=2499&azid=85&PageFlow=FixedWidth)”.

Using the idea I was able to add the following to the **AssemblyInfo.cs** of my own project:

[<span style="color: blue">assembly</span>: <span style="color: #2b91af">XmlnsDefinition</span>(<span style="color: #a31515">"telerik"</span>,
                           <span style="color: #a31515">"Telerik.Windows.Controls"</span>,
                           AssemblyName = <span style="color: #a31515">"Telerik.Windows.Controls"</span>)]

[<span style="color: blue">assembly</span>: <span style="color: #2b91af">XmlnsDefinition</span>(<span style="color: #a31515">"telerik"</span>,
                           <span style="color: #a31515">"Telerik.Windows.Controls"</span>,
                           AssemblyName = <span style="color: #a31515">"Telerik.Windows.Controls.Input"</span>)]

[<span style="color: blue">assembly</span>: <span style="color: #2b91af">XmlnsDefinition</span>(<span style="color: #a31515">"telerik"</span>,
                           <span style="color: #a31515">"Telerik.Windows.Controls"</span>,
                           AssemblyName = <span style="color: #a31515">"Telerik.Windows.Controls.Navigation"</span>)]

[<span style="color: blue">assembly</span>: <span style="color: #2b91af">XmlnsDefinition</span>(<span style="color: #a31515">"telerik"</span>,
                           <span style="color: #a31515">"Telerik.Windows.Controls"</span>,
                           AssemblyName = <span style="color: #a31515">"Telerik.Windows.Controls.RibbonView"</span>)]

And then my XAML file declaration looks like that:

<span style="color: blue"><</span><span style="color: #a31515">Window </span><span style="color: red">x</span><span style="color: blue">:</span><span style="color: red">Class</span><span style="color: blue">="skyeEditor.View.Dialogs.ProductSettingsDialog"
        </span><span style="color: red">xmlns</span><span style="color: blue">="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        </span><span style="color: red">xmlns</span><span style="color: blue">:</span><span style="color: red">x</span><span style="color: blue">="http://schemas.microsoft.com/winfx/2006/xaml"
        </span><span style="color: red">xmlns</span><span style="color: blue">:</span><span style="color: red">telerik</span><span style="color: blue">="http://schemas.telerik.com/2008/xaml/presentation"
</span>

And I can use everywhere for all Telerik RadControls for WPF with the prefix **telerik** 

<span style="color: blue"><</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">RadComboBox </span><span style="color: red">ItemsSource</span><span style="color: blue">="{</span><span style="color: #a31515">Binding </span><span style="color: red">ProductNodeLabels</span><span style="color: blue">}"
                        </span><span style="color: red">SelectedItem</span><span style="color: blue">="{</span><span style="color: #a31515">Binding </span><span style="color: red">SelectedProductNodeLabel</span><span style="color: blue">}"
                        </span><span style="color: red">Margin</span><span style="color: blue">="0,0,0,5" />
</span>

A little step but a nice improvement!
