---
layout: post
title: Code Snippet para TestMethods no VisualStudio
wordpress_id: 681
wordpress_url: http://viniciusquaiato.com/blog/?p=681
categories:
- title: TDD
  slug: tdd
  autoslug: tdd
- title: .NET
  slug: dotnet
  autoslug: .net
- title: Visual Studio 2010
  slug: visual-studio-2010
  autoslug: visual-studio-2010
- title: "Boas Pr\xC3\xA1ticas"
  slug: boas-praticas
  autoslug: "boas-pr\xC3\xA1ticas"
tags:
- title: "Quick Tip"
  slug: quick-tip
  autoslug: quick-tip
---
Sempre achei um "pé" ter que ficar copiando métodos de teste, tudo pela preguiça de colocar o attribute [TestMethod]
public void etc, etc.

Criei um CodeSnippet pra ser usado com C# que resolve alguns desses problemas. Abaixo segue o código do Snippet, à noite eu mostro como inserir o mesmo no VisualStudio, e coloco um link para download também:

{% highlight csharp %}
<?xml version="1.0" encoding="utf-8" ?>
<codesnippets>
  <codesnippet>
    <header>
      <title>Test Method</title>
      <shortcut>test</shortcut>
      <description>Code snippet to create a test method</description>
      <author>Vinicius Quaiato</author>
      <snippettypes>
        <snippettype>Expansion</snippettype>
      </snippettypes>
    </header>
    <snippet>
      <declarations>
        <literal>
          <id>Test_Method_Name</id>
          <tooltip>The name of the method. Try using a name that indicates the purpose of the test</tooltip>
          <default>Test_Method_Name</default>
        </literal>
      </declarations>
      <code language="csharp">
        <![CDATA[[TestMethod]
        public void $Test_Method_Name$(){    }
        ]]>
      </code>
    </snippet>
  </codesnippet>
</codesnippets>
{% endhighlight %}

Espero que ajude um pouco. É mais rápido digitar "test + tab + tab" do que copiar, colar e alterar o nome do método anterior.

Abraços,
Vinicius Quaiato.
