--- 
layout: post
title: "QuickTip: Usando classes css em ActionLink no ASP.NET MVC"
wordpress_id: 3099
wordpress_url: http://viniciusquaiato.com/blog/?p=3099
categories: 
- title: ASP.NET MVC
  slug: asp-net-mvc
  autoslug: asp.net-mvc
tags: 
- title: ASP.NET MVC
  slug: asp-net-mvc
  autoslug: asp.net-mvc
- title: quick tip
  slug: quick-tip
  autoslug: quick-tip
---


Quando utilizamos o Html helper no ASP.NET MVC temos a opção de passar um dicionário com valores para os atributos HTML, por exemplo id, alt, title, etc.Porém quando queremos passar uma class temos problemas:[![Compilation Error html helper css class](http://viniciusquaiato.com/images_posts/Compilation-Error-html-helper-css-class-300x142.png "Compilation Error html helper css class")](http://viniciusquaiato.com/images_posts/Compilation-Error-html-helper-css-class.png)

Para utilizarmos o atributo class preciso usar um "@" como mostra o código abaixo:
{% highlight csharp %}
@Html.ActionLink("Outra Action", "Outra", null, new { @class = "customizada" }


)
{% endhighlight %}
E teremos o resultado:[![html helper css class](http://viniciusquaiato.com/images_posts/html-helper-css-class-300x162.png "html helper css class")](http://viniciusquaiato.com/images_posts/html-helper-css-class.png)

É issaê.

Abraços,
Vinicius Quaiato.
