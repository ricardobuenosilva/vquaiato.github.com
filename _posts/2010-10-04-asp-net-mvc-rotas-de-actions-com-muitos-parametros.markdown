---
layout: post
title: "ASP.NET MVC: rotas de actions com muitos par\xC3\xA2metros"
wordpress_id: 1641
wordpress_url: http://viniciusquaiato.com/blog/?p=1641
categories:
- title: ASP.NET MVC
  slug: asp-net-mvc
  autoslug: asp.net-mvc
tags:
- title: ASP.NET MVC
  slug: asp-net-mvc
  autoslug: asp.net-mvc
---


[![](http://viniciusquaiato.com/images_posts/rota-150x150.jpg "Rotas ASP.NET MVC")](http://viniciusquaiato.com/images_posts/rota.jpg)

O padrão do [ASP.NET MVC](http://asp.net/mvc) para tratamento de rotas é trabalhar respondendo: _"controller/action/id"_. Isto quer dizer que por padrão nossos projetos ASP.NET MVC respondem a requisições do tipo: _"produtos/detalhes/10"_ ou _"vendas/cancelar/23"_.

## Os recursos com vários parâmetros
Se quisermos responder a requisições do tipo _"minhaempresa/setor/controller/action/param1/param2/param3"_ não conseguimos isso por default, e é então que entra a configuração de rotas. Responder a uma requisição com mais de um parâmetro desta forma não é complexo, na verdade é algo bastante simples. Para um primeiro exemplo vamos imaginar que temos uma action que "mistura cores". Queremos poder escrever uma url assim no browser: _"estudio/misturar/azul/vermelho/verde"_.

Este é nosso controller:

{% highlight csharp %}
public class EstudioController : Controller{
  [HttpGet]
  public ActionResult Misturar(string cor1, string cor2, string cor3) {
    object corMisturada = string.Format("{0} + {1} + {2}", cor1, cor2, cor3);
    return View("NovaCor", corMisturada);
  }
}
{% endhighlight %}

Se simplesmente acessarmos a url no browser, obteremos:

[![Erro de rota: recurso não encontrado](http://viniciusquaiato.com/images_posts/erro-de-rota-300x152.png "Erro de rota: recurso não encontrado")](http://viniciusquaiato.com/images_posts/erro-de-rota.png)

## Adicionando uma rota no Global.asax
Para que possamos realizar a chamada a este recurso, e receber em nossa action os valores desejados, precisamos adicionar uma rota em nossa tabela de rotas. A configuração de rotas no ASP.NET MVC é feita no arquivo Global.asax, de uma maneira bastante simples. Nosso arquivo Global.asax deve estar assim:
{% highlight csharp %}

public static void RegisterRoutes(RouteCollection routes){
  routes.IgnoreRoute("{Resource}.axd/{pathInfo}");

    routes.MapRoute(
      "Default", // Route name
      "{Controller}/{Action}/{Id}", // URL with parameters
      new { controller = "Home", action = "Index", id = UrlParameter.Optional } // Parameter Defaults
    );
}
{% endhighlight %}

Este código adiciona uma rota a nossa tabela de roteamento. Vamos ver então como rotear para conseguirmos responder a nossas requisições precisamos do código a seguir:

{% highlight csharp %}
routes.MapRoute(
  "MisturarCores",
  "{Controller}/{Action}/{cor1}/{cor2}/{cor3}
");
{% endhighlight %}

Com a adição desta rota, conseguimos responder então ao nosso recurso e chegar a nossa action com todos os parâmetros preenchidos.

## Resultado
Desta forma passamos a compreender um pouco mais como é que funciona o framework MVC no ASP.NET. Temos rotas mapeadas a serem respondidas, e isso não é assim apenas no ASP.NET, é assim também no Rails, um dos mais conhecidos frameworks MVC para web. Ter conhecimento e saber do potencial que temos ao trabalhar com as rotas com toda certeza nos ajudará a criar aplicações mais interessantes com o ASP.NET MVC. Criei uma View simples apenas para renderizar o resultado da nossa action, e aqui segue o resultado:

[![Rota funcionando](http://viniciusquaiato.com/images_posts/rota-funcionando-300x158.png "Rota funcionando")](http://viniciusquaiato.com/images_posts/rota-funcionando.png)

É isso galera, em breve veremos um pouco mais sobre como trabalhar com rotas no ASP.NET MVC.Veja aqui um overview sobre rotas no ASP.NET MVC: [http://www.asp.net/mvc/tutorials/asp-net-mvc-routing-overview-cs](http://www.asp.net/mvc/tutorials/asp-net-mvc-routing-overview-cs)

Abraços,

Vinicius Quaiato.
