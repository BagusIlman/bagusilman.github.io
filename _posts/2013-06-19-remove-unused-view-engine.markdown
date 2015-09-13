---
layout: post
title:  "Remove Unused View Engine"
date:   2013-06-19 00:55:37
categories: Article
---
Kalau anda adalah Asp.Net MVC developer, mungkin anda belum tahu kalau secara default Asp.Net akan me-load view engine dari razor dan webform. Hal ini dapat menjadi performance issue karena MVC akan mencoba untuk mencari view dari webform terlebih dahulu sebelum mencoba untuk mencari view dari razor.

Anda dapat secara mudah mengatasi hal tersebut dengan menambahkan code di Global.asax pada method Application_Start()

{% highlight csharp %}
ViewEngines.Engines.Clear();
ViewEngines.Engines.Add(new RazorViewEngine());
{% endhighlight %}

