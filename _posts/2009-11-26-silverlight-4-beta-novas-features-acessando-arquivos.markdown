---
layout: post
title: Silverlight 4 beta - Novas Features - Acessando Arquivos
wordpress_id: 222
wordpress_url: http://viniciusquaiato.com/blog/?p=222
categories:
- title: .NET
  slug: dotnet
  autoslug: .net
- title: Visual Studio 2010
  slug: visual-studio-2010
  autoslug: visual-studio-2010
- title: Silverlight
  slug: silverlight
  autoslug: silverlight
tags:
- title: Silverlight
  slug: silverlight
  autoslug: silverlight
---


Fala galera, beleza?Silverlight 4 - Capturando WebCam - [http://viniciusquaiato.com/blog/silverlight-4-capturando-webcam/](http://viniciusquaiato.com/blog/silverlight-4-capturando-webcam/)Vamos falar mais um pouco do silverlight 4 beta, desta vez vamos acessar arquivose pastas da máquina utilizando uma aplicação Silverlight rodando fora do browser (Out of Browser).Vamos abrir o Visual Studio 2010 beta 2 e criar uma nova aplicação Silverlight:[![Criando projeto Silverlight](http://viniciusquaiato.com/images_posts/Criando-projeto-Silverlight.jpg "Criando projeto Silverlight")](http://viniciusquaiato.com/images_posts/Criando-projeto-Silverlight.jpg)



A interface utilizada será bem simples como mostra a imagem e o código XAML abaixo:[![Interface Silverlight](http://viniciusquaiato.com/images_posts/Interface-Silverlight.jpg "Interface Silverlight")](http://viniciusquaiato.com/images_posts/Interface-Silverlight.jpg)

Código XAML:
{% highlight csharp %}
            <textbox height="80" horizontalalignment="Left" margin="12,175,0,0" name="txtConteudoArquivo" verticalalignment="Top" width="263" acceptsreturn="True" />            </button>
{% endhighlight %}
Feito isso vamos implementar agora a listagem dos arquivos da pasta "Documents", como mostra a listagem do click do primeiro botão abaixo:
{% highlight csharp %}

private void btnListar_Click(object sender, RoutedEventArgs e){
var files = Directory.EnumerateFiles(                    Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments)                );
foreach(var item in files)        this.listBox1.Items.Add(item);
    }

{% endhighlight %}
As linhas 3, 4 e 5 são as principais nesta listagem. Nelas estamos obtendo os nomes dos arquivos do diretório "Meus Documentos". Notem a utilização das classes Environment e Directory.Já nas linhas 7 e 8 estamos apenas adicionando os nomes dos arquivos à nossa ListBox.A listagem a seguir mostra como fazer a gravação de um arquivo texto também na pasta "Meus Documentos":
{% highlight csharp %}

private void btnGravar_Click(object sender, RoutedEventArgs e){
var streamWriter = File.CreateText(            System.IO.Path.Combine(                Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), "Silverlight.txt")            );
    streamWriter.WriteLine("Arquivo gerado pela app Silverlight...");
    streamWriter.WriteLine("=======================================");
    streamWriter.WriteLine(this.txtConteudoArquivo.Text);
    streamWriter.Close();
    }



{% endhighlight %}
Este também é um código bem simples. Na linha 3 estamos criando uma stream para a gravação de um arquivo, novamente utilizando a classe Environment (linha 4).Nas linhas 7, 8 e 9 gravamos o conteúdo do arquivo, e na linha 10 finalizamos nossas operações.Para que nossa aplicação rode fora do browser, vamos realizar esta configuração no projeto silverlight, como mostram as imagens abaixo:[![Configurando Silverlight Fora do Browser](http://viniciusquaiato.com/images_posts/Configurando-Silverlight-Fora-do-Browser.jpg "Configurando Silverlight Fora do Browser")](http://viniciusquaiato.com/images_posts/Configurando-Silverlight-Fora-do-Browser.jpg)



[![Configurando Silverlight Fora do Browser 2](http://viniciusquaiato.com/images_posts/Configurando-Silverlight-Fora-do-Browser-2.jpg "Configurando Silverlight Fora do Browser 2")](http://viniciusquaiato.com/images_posts/Configurando-Silverlight-Fora-do-Browser-2.jpg)



Agora é preciso instalar nossa aplicação. Para isso basta iniciar a mesma, com F5 no Visual Studio. Quando a página abrir, basta clicar com o botão direito na página, como mostra a imagem abaixo:[![Instalando Aplicacao Silverlight Fora do Browser](http://viniciusquaiato.com/images_posts/Instalando-Aplicacao-Silverlight-Fora-do-Browser.jpg "Instalando Aplicação Silverlight Fora do Browser")](http://viniciusquaiato.com/images_posts/Instalando-Aplicacao-Silverlight-Fora-do-Browser.jpg)



[![Instalando Aplicacao Silverlight Fora do Browser 2](http://viniciusquaiato.com/images_posts/Instalando-Aplicacao-Silverlight-Fora-do-Browser-2.jpg "Instalando Aplicação Silverlight Fora do Browser 2")](http://viniciusquaiato.com/images_posts/Instalando-Aplicacao-Silverlight-Fora-do-Browser-2.jpg)



E como resultado temos:[![Aplicacao Silverlight rodando fora do browser](http://viniciusquaiato.com/images_posts/Aplicacao-Silverlight-rodando-fora-do-browser.jpg "Aplicacao Silverlight rodando fora do browser")](http://viniciusquaiato.com/images_posts/Aplicacao-Silverlight-rodando-fora-do-browser.jpg)



E aqui podemos ver o arquivo gerado:[![Arquivo gerado pelo silverlight](http://viniciusquaiato.com/images_posts/Arquivo-gerado-pelo-silverlight.jpg "Arquivo gerado pelo silverlight")](http://viniciusquaiato.com/images_posts/Arquivo-gerado-pelo-silverlight.jpg)

Bom é isso aê pessoal. [Quem quiser a solução Silverlight + C# pode ser baixada aqui.](http://www.viniciusquaiato.com/files/codesamples/silverlight4/acessandoArquivos.rar)Qualquer dúvida, é só entrar em contato.

Abraços,
Vinicius Quaiato.
