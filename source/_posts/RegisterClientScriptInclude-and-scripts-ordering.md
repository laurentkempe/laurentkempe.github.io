title: RegisterClientScriptInclude and scripts ordering
date: 5/25/2007 8:04:38 AM
updated: 5/25/2007 8:04:38 AM
tags: ["ASP.NET AJAX"]
---
I spend a part of this evening fighting with *ScriptManager.RegisterClientScriptInclude *and had no chance to use it in a way that my javascripts would appear after MicrosoftAjax.js and in an order that I defined.

I finally found a solution, using ScriptManagerProxy and declaratively listing the javascripts in the order I wanted.<scripts>
