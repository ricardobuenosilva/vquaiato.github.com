def aggregate_keywords(category,posts)
  keywords = SortedSet.new()
  keywords << category
  posts.each do |post|
    post_data = post.to_liquid
    if post_data.has_key? 'keywords'
      post_data['keywords'].each do |word|
        keywords << word
      end
    end
  end

  return keywords.to_a.join(',')
end

def clean(to_clean)
      mapping = {
        'E' => [200,201,202,203],
        'e' => [232,233,234,235],
        'A' => [192,193,194,195,196,197],
        'a' => [224,225,226,227,228,229,230],
        'C' => [199],
        'c' => [231],
        'O' => [210,211,212,213,214,216],
        'o' => [242,243,244,245,246,248],
        'I' => [204,205,206,207],
        'i' => [236,237,238,239],
        'U' => [217,218,219,220],
        'u' => [249,250,251,252],
        'N' => [209],
        'n' => [241],
        'Y' => [221],
        'y' => [253,255],
        'AE' => [306],
        'ae' => [346],
        'OE' => [188],
        'oe' => [189]
      }
  str = String.new(to_clean.gsub /\s+/,'-')
  str.gsub! /--+/,'-'
  str.downcase!
  mapping.each {|letter,accents|
    packed = accents.pack('U*')
    rxp = Regexp.new("[#{packed}]", nil)
    str.gsub!(rxp, letter)
  }
  str
end

namespace :tags do
  desc "remove todas as paginas de tags existentes"
  task :clean do
    puts "removendo tags.."
    rm_rf "tags"
    mkdir "tags"
  end

  desc "gera as paginas de tags"
  task :generate => [:clean] do
    puts 'gerando tags...'
    require 'rubygems'
    require 'jekyll'
    include Jekyll::Filters

    options = Jekyll.configuration({})
    site = Jekyll::Site.new(options)
    site.read_posts('')
    site.tags.each do |kategory, posts|
      category = kategory["slug"]
      ordered_posts = posts.sort_by{|p| p.to_liquid["date"]}.reverse
      keywords = aggregate_keywords(category, ordered_posts)

      html= <<-HTML
---
layout: default
title: Posts tagged #{category}
keywords: [#{keywords}]
---
<h2 class="category">#{kategory["title"]}</h2>
<ul class="posts">
HTML
ordered_posts.each do |post|
post_data = post.to_liquid
html << <<-HTML
<li>
<p>
<span class="date">#{post_data["date"].strftime("%d/%m/%Y")}</span> &raquo;
<a href="#{post_data["url"]}">#{post_data["title"]}</a>
</p>
</li>
HTML
end
html << <<-HTML
</ul>
HTML
      dir_name = "tags/#{clean(category)}"
      Dir::mkdir dir_name unless FileTest::directory?(dir_name)
      File.open("#{dir_name}/index.md", 'w+') do |file|
        file.puts html
      end
    end
  end
end

desc "publica o site, gerando as categorias, commitando e dando push no github"
task :publish, [:arg1] => ["tags:generate"] do |t, args|
  puts "publicando"
  message = args[:arg1]

  %x{git add -A}
  %x{git commit -am "#{message}"}
  %x{git pp}

  puts "publicado"
end

