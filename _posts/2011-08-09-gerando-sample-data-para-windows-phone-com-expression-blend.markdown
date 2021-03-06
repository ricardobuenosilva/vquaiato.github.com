---
layout: post
title: Gerando Sample Data para Windows Phone com Expression Blend
wordpress_id: 3978
wordpress_url: http://viniciusquaiato.com/blog/?p=3978
keywords:
- Windows Phone 7
- Expression Blend
tags:
- title: Windows Phone 7
  slug: windows-phone-7
  autoslug: windows-phone-7
---
Fala galera, beleza? É muito comum precisar de dados fictícios quando estamos trabalhando com aplicações para o Windows Phone. Muito disso se deve ao fato de que quando criamos controles com Bindings só poderemos conferir e visualizar os estilos destes controles quando eles possuírem dados vinculados.O Expression Blend nos permite facilmente criar dados de exemplo para utilizarmos em nossas aplicações. Estes dados funcionarão tanto em design time quanto em runtime.**_(no final do post há um pequeno vídeo mostrando o que os passos abaixo explicam)_**

## Criando o projeto no Expression Blend


Vamos criar uma nova aplicação Windows Phone no Expression Blend e então adicionar um ListBox na nossa página:[![expression blend sample data 1](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-1-300x255.png "expression blend sample data 1")](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-1.png)



Depois disso vamos adicionar um ListBox em nossa aplicação:[![expression blend sample data 2](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-2-300x177.png "expression blend sample data 2")](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-2.png)



Neste ponto se fizermos o Binding de alguma propriedade no ItemTemplate não conseguiremos ver como está a formatação e o design desta propriedade sem dados. Por isso vamos criar alguma um "Sample Data Source":[![expression blend sample data 3](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-3-300x231.png "expression blend sample data 3")](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-3.png)



Precisamos dar um nome para nosso DataSource:[![expression blend sample data 4](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-4-300x145.png "expression blend sample data 4")](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-4.png)



Agora que a collection está criada vamos adicionar mais uma propriedade para que possamos representar minimamente um tweet no nosso exemplo:[![expression blend sample data 6](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-6-300x236.png "expression blend sample data 6")](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-6.png)



O próximo passo é formatar os tipos de cada uma das propriedades de nossa collection, e isso é feito de maneira bastante simples:[![expression blend sample data 7](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-7-300x178.png "expression blend sample data 7")](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-7.png)



Agora basta "arrastar" a collection para dentro do ListBox e teremos os dados exibidos com Bindings, batsando para nós configurar e formatar nosso controle :D[![expression blend sample data 8](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-8-300x227.png "expression blend sample data 8")](http://viniciusquaiato.com/images_posts/expression-blend-sample-data-8.png)



## Vídeo mostrando como usar Sample Data no Expression Blend
<object width="601" height="353"><param name="allowfullscreen" value="true" /><param name="allowscriptaccess" value="always" /><param name="movie" value="http://vimeo.com/moogaloop.swf?clip_id=27471960&amp;
    server=vimeo.com&amp;
    show_title=0&amp;
    show_byline=0&amp;
    show_portrait=0&amp;
    color=00adef&amp;
    fullscreen=1&amp;
    autoplay=0&amp;
    loop=0" /><embed src="http://vimeo.com/moogaloop.swf?clip_id=27471960&amp;
    server=vimeo.com&amp;
    show_title=0&amp;
    show_byline=0&amp;
    show_portrait=0&amp;
    color=00adef&amp;
    fullscreen=1&amp;
    autoplay=0&amp;
    loop=0" type="application/x-shockwave-flash" allowfullscreen="true" allowscriptaccess="always" width="601" height="353"></embed></object>
[SampleData para Windows Phone com Expression Blend](http://vimeo.com/27471960) from [vinicius quaiato](http://vimeo.com/user2557055) on [Vimeo](http://vimeo.com).

Neste vídeo mostro como criar Sample Data Sources para trabalhar com Windows Phone 7 utilizando o Expression Blend. Mais informações e o post completo em: http://viniciusquaiato.com/blog/gerando-sample-data-para-windows-phone-com-expression-blend
Espero que tenha sido útil. Abraços,Vinicius Quaiato.
