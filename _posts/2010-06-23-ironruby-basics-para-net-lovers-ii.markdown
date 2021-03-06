--- 
layout: post
title: ":IronRuby Basics para .Net Lovers => II"
wordpress_id: 1083
wordpress_url: http://viniciusquaiato.com/blog/?p=1083
categories: 
- title: IronRuby
  slug: ironruby
  autoslug: ironruby
tags: 
- title: IronRuby
  slug: ironruby
  autoslug: ironruby
- title: ruby
  slug: ruby
  autoslug: ruby
---


[![Ruby Ring](http://viniciusquaiato.com/images_posts/ruby-ring-150x150.jpg "Ruby => simplicidade e elegância")](http://viniciusquaiato.com/images_posts/ruby-ring.jpg)

Continuando a falar sobre Ruby/IronRuby para apaixonados por .net c# ou vb.net.Quando comecei a estudar Ruby eu senti uma grande resistência pois estava tentando, a todo momento, compará-la com C#. Esta é uma postura complicada, pois as duas linguagens seguem abordagens bem distintas. Então deixo a dica de estarem abertos ao estudo desta linguagem. Não é pecado estudar uma enquanto se trabalha com a outra.Uma das coisas que mais me chamou a atenção em Ruby é sua simplicidade. Um programa em Ruby pode ser feito com apenas uma linha, incrível.E desta forma, simples e clean, segue todo o trabalho com Ruby.

### :Array
No nosso dia-a-dia com .Net trabalhamos muito com coleções. 
{% highlight csharp %}
array = Array.new
{% endhighlight %}
Com isto criamos um array vazio. Poderíamos utilizar a seguinte sintaxe também:
{% highlight csharp %}
array = []
{% endhighlight %}
Isso também significa que estamos criando um array. Clever!Novamente percebemos que não existe a definição de tipos, desta forma nosso array já é um array genérico.Podemos adicionar alguns itens:
{% highlight csharp %}
array = []array[0] = "Vinicius"array[1] = "Quaiato"array[2] = 2010
{% endhighlight %}
Agora a coisa começa a ficar interessante. Temos métodos muito bons para utilizarmos com as coleções:
{% highlight csharp %}
array = ["Vinicius", "Quaiato", "Janynne", "Gomes", ".Net", "Ruby"]#obtendo o primeiro e o último elementos do arrayputs array.firstputs array.last#obtendo um range de elementosputs array[0..3]#obtendo o índice através de um valorputs array.index(".Net")
{% endhighlight %}
Na **_linha 1_** criamos um objeto utilizando a inicialização "automagica" de arrays.Nas _**linhas 4 e 5**_ invocamos os métodos _first_ e _last_. Não precisamos explicar estes métodos né? =DNa **_linha 8_** temos algo interessante. Ao invés de acessarmos um único índice do array, nós acessamos um range de valores. Neste caso estamos dizendo "me dê os elementos que vão dos índices 0 até 3", sendo que tanto o índice 0 quanto o índice 3 estão inclusos.Na **_linha 11_** o método index retorna o índice no qual o elemento ".Net" está. Caso não exista o elemento informado, retorna _**nil**_.

### :Hash => Dictionary
Nem sempre um array resolve todos os problemas. Podemos precisar de uma coleção indexada por chaves. Em .net chamamos isso de dicionários, em Ruby chamaremos isso de Hash.
{% highlight csharp %}
hash = {

hash["nome"] = "Vinicius"hash["sobrenome"] = "Quaiato"
{% endhighlight %}
Assim como criamos um array com [] (colchetes) podemos criar um hash com {

 (chaves).Definimos então duas chaves (que podem ser objetos de qualquer tipo), e seus valores. Simples!Poderíamos ter feito isso também:
{% highlight csharp %}
hash = {
nome" => "Vinicius", "sobrenome" => "Quaiato"}

{% endhighlight %}
O código é bem simples. Do lado esquerdo da "flexa" está a chave, e do lado direito o valor.Podemos ainda trabalhar com uma espécie de "enum":
{% highlight csharp %}
hash = { :nome => "Vinicius", :sobrenome => "Quaiato"}

{% endhighlight %}
Na verdade isso é chamado de Symbol. é criado utilizando a sintaxe :alguma_coisa ou :"alguma coisa".E para tornar a brincadeira interessante, vamos ver alguns métodos de um hash:
{% highlight csharp %}
#obtendo todas as chavesputs hash.keys#obtendo todos os valoresputs hash.values#obtendo o maior valorputs hash.values.max#obtendo o menor valorputs hash.values.min
{% endhighlight %}
Os métodos tem nomes bem explicativos, nem preciso dizer mais nada. =DTemos ainda algumas operações interessantes que podem ser realizadas como a comparação de dois hashes:
{% highlight csharp %}
hash1 = { :a=>"maçã", :cor=>"verde", :preco=>10}
hash2 = { :preco=>10, :a=>"maçã", :cor=>"verde"}
#retornará trueputs hash1 == hash2hash2 = { :preco=>10, :a=>"Abacaxi", :cor=>"verde"}
#retornará falseputs hash1 == hash2
{% endhighlight %}
Quando comparamos dois hash desta maneira o resultado será verdadeiro(igualdade) quando ambos possuírem a mesma quantidade de itens, e quando todas as chaves e todos os valores forem iguais, neste caso, indepente da ordem.Podemos definir um valor default para um hash. Este valor funciona no caso de tentarmos obter algo que não existe, uma chave inexistente por exemplo.Há algumas formas de fazer isso:
{% highlight csharp %}
#definindo valor default no construtor do Hashhash = Hash.new("padrão")#irá exibir 'padrão'puts hash[:chave_invalida]#setando o valor default diretamentehash.default = 2010#irá exibir 2010puts hash.default
{% endhighlight %}
Podemos deletar um item assim:
{% highlight csharp %}
hash = { :a=>"a", :b=>10, :c=>Object.new}
#exibe 3puts hash.sizehash.delete(:a)#exibe 2puts hash.size
{% endhighlight %}
Para saber se um hash está vazio ou para limpá-lo:
{% highlight csharp %}
hash = {

#exibirá trueputs hash.empty?hash = { :a=>"a", :b=>10, :c=>Object.new}
#exibirá falseputs hash.empty?#limpamos todos elementoshash.clear#exibirá trueputs hash.empty?
{% endhighlight %}
Notem que interessante o método _empty_. ele possui um ponto de interrogação. Fica muito mais claro e inteligente sabermos que se trata de uma "pergunta" que estamos fazendo ao objeto. Simplesmente incrível.Ainda temos alguns outros métodos bem interessantes, porém mostrarei em uma próxima parte, onde começaremos a falar de blocos de código, algo equivalente a nossas lambda expressions.Ainda voltaremos a falar de classes, propriedades, herança, parâmetros, etc. Há muito post a ser feito =DAbraços, e lembrem-se: feedback é bem vindo!Vinicius Quaiato.
