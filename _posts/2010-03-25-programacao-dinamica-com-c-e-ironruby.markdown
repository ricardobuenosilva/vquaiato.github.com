---
layout: post
title: "Programação dinâmica com C# e IronRuby"
wordpress_id: 731
wordpress_url: http://viniciusquaiato.com/blog/?p=731
keywords:
- .NET 4.0
- IronRuby
- Novidades
- script
tags:
- title: dynamic
  slug: dynamic
  autoslug: dynamic
- title: IronRuby
  slug: ironruby
  autoslug: ironruby
---
![](http://viniciusquaiato.com/images_posts/ruby-299x300.png "ruby")Que tal escrever um sistema em C#, com todas suas classes, camada de persistência, interface, etc e ainda assim permitir de uma maneira fácil escrever "plugins" e scripts que alterem alguns comportamentos do sistema?Pense que existe um ponto no seu sistema que pode sofrer constantes mudanças de regra: o cálculo de um desconto, o cálculo de um imposto, uma série de ações que podem ser feitas antes ou depois de alguma operação, etc.O esforço de alteração, build e deploy é tão grande que sentimos a necessidade de tornar nosso sistema mais maleável, e pronto para estas mudanças. Queremos que o usuário do sistema possa fazer isso sem ter de contar com mais desenvolvimento, build, deploy, etc.Neste primeiro artigo criarei uma simples calculadora em C#, só que ao invés de efetuar as contas dentro do código C# ela fará chamadas para uma classe [Ruby](http://www.ruby-lang.org/pt/) que conterá os métodos para cada uma das operações.Desta forma poderemos alterar o método no arquivo Ruby e pronto, nosso sistema está com um novo comportamento, sem deploy, sem recompilações, etc.Vamos ao código:
{% highlight csharp %}

public
static class RubyEngineCreator{

private
static ScriptEngine ironRubyEngine = null;

private
static ScriptEngine CreateEngine()    {
if(ironRubyEngine == null)            ironRubyEngine = Ruby.CreateEngine();
return ironRubyEngine;
    }

public
static dynamic GetRubyObject(string rubyFileName, string rubyClassName)    {
string binDebug = Path.GetDirectoryName(typeof(RubyEngineCreator).Assembly.Location);
var path = Path.Combine(binDebug, string.Format("{
}
.rb", rubyFileName));
    CreateEngine().ExecuteFile(path);
    dynamic variable = CreateEngine().Runtime.Globals.GetVariable(rubyClassName);
return CreateEngine().Operations.CreateInstance(variable);
    }
}

{% endhighlight %}
O que fiz acima foi encapsular a criação de uma engine [IronRuby](http://ironruby.net/), e instanciar uma classe IronRuby. Se você não entendeu nada, leia este post [aqui](http://viniciusquaiato.com/blog/ironruby-rodando-ruby-dentro-do-net/), ele explica exatamente o que foi feito.Agora criarei minha classe Calculadora:
{% highlight csharp %}

public class Calculadora{

private
static string RUBY_FILE_NAME = "Calculadora";

private
static string RUBY_CLASS_NAME = "Calculadora";

private
static dynamic rubyObject = null;

private
static dynamic RubyObject    {        get        {
if(rubyObject == null)                rubyObject = RubyEngineCreator.GetRubyObject(RUBY_FILE_NAME, RUBY_CLASS_NAME);
return rubyObject;
    }
    }

public
static double Somar(float num1, float num2)    {
return RubyObject.Somar(num1, num2);
    }

public
static double Subtrair(float num1, float num2)    {
return RubyObject.Subtrair(num1, num2);
    }

public
static double Dividir(float num1, float num2)    {
return RubyObject.Dividir(num1, num2);
    }

public
static double Multiplicar(float num1, float num2)    {
return RubyObject.Multiplicar(num1, num2);
    }

public
static double Fatorial(float num1)    {
return RubyObject.Fatorial(num1);
    }

public
static double Potencia(float num1, float num2)    {
return RubyObject.Potencia(num1, num2);
    }
}

{% endhighlight %}
Este código é ainda mais simples. Utilizando dynamic obtemos a instância da classe IronRuby e então chamamos os métodos contra este objeto dynamic. Se você não sabe o que [dynamic](http://www.hanselman.com/blog/C4AndTheDynamicKeywordWhirlwindTourAroundNET4AndVisualStudio2010Beta1.aspx) no .NET 4.0 dê uma olhada neste artigos: <a href="http://viniciusquaiato.com/blog/expandoobject-dinamismo-dotnet-4/" target+"_blank">aqui, [aqui](http://viniciusquaiato.com/blog/dynamicobject-dinamismo-no-net-4-0/) e [aqui](http://viniciusquaiato.com/blog/apresentacao-dynamic-types-no-net-4/).Aqui segue a classe Ruby/IronRuby que contém os métodos:
{% highlight csharp %}
class Calculadora    def Somar(n1, n2)        n1 + n2    end    def Subtrair(n1, n2)        n1 - n2    end    def Dividir(n1, n2)        n1 / n2    end    def Multiplicar(n1, n2)        n1 * n2    end    def Fatorial(n)
if(n > 0)            return n * Fatorial(n - 1)        end        return 1    end    def Potencia(n, p)        n**p    endend
{% endhighlight %}
Pronto! tudo que precisamos é que o arquivo Calculadora.rb esteja na pasta do nosso projeto(na pasta bin, neste caso).Abaixo segue o código que consome a calculadora, e uma imagem do resultado das operações:
{% highlight csharp %}

static void Main(string[] args){    Console.WriteLine("Somando 2 + 2 = {
}
", Calculadora.Somar(2, 2));
    Console.WriteLine("\n\nSubtraindo 4 - 2 = {
}
", Calculadora.Subtrair(4, 2));
    Console.WriteLine("\n\nDividindo 10 / 2 = {
}
", Calculadora.Dividir(10, 2));
    Console.WriteLine("\n\nFatorial 5 = {
}
", Calculadora.Fatorial(5));
    Console.WriteLine("\n\nPotencia 3^3 = {
}
", Calculadora.Potencia(3, 3));
    Console.ReadKey();
    }



{% endhighlight %}
Resultado:[![C# com Scripts IronRuby](http://viniciusquaiato.com/images_posts/resultado.jpg "C# com Scripts IronRuby")](http://viniciusquaiato.com/images_posts/resultado.jpg)

Esta é uma situação bastante simples. Experimente alteraro arquivo Calculadora.rb. Troque as operações de Soma por substração, etc. Brinque com a classe Ruby, e abra o programa .exe gerado, para ver que dinamicamente o comportamento dele foi alterado, sem recompilar ou reescrever nada.Em um próximo post, darei um exemplo de como alterar/incrementar regras de negócio de forma dinâmica utilizando script IronRuby.Você pode baixar a solution da calculadora [aqui](http://viniciusquaiato.com/files/codesamples/dynamic/CalculadoraScriptRuby.zip).Qualquer dúvida, sugestão, crítica. Mande e-mail, mensagens no [twitter](http://twitter.com/vquaiato), gtalk, etc.

Att,
Vinicius Quaiato.
