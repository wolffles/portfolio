---
layout: post
title: Introduction to Jekyll
---

## What is Jekyll?
Jekyll is a parsing engine bundled as a ruby gem used to build static websites from dynamic components such as templates, partials, liquid code, markdown, etc. Jekyll is known as "a simple, blog aware, static site generator.

## What does Jekyll do?
Jekyll is installed as a ruby gem local computer. Once installed you can call jekyll serve in the terminal in a directory and provided that directory is setup in a way jekyll expects, it will do magic stuff like parse markdown/textile files, compute categories, tags, permalinks, and construct your pages from layout templates and partials.

Once parsed, Jekyll stores the result in a self-contained static `_site` folder. The intention here is that you can serve all contents in this folder statically from a plain static web-server.

You can think of Jekyll as a normalish dynamic blog but rather than parsing content, templates, and tags on each request, Jekyll does this once beforehand and caches the entire website in a folder for serving statically.

## Why Should I Care?
Jekyll is very minimalistic and very efficient. The most important thing to realize about Jekyll is that it creates a static representation of your website requiring only a static web-server. Traditional dynamic blogs like Wordpress require a database and server-side code. Heavily trafficked dynamic blogs must employ a caching layer that ultimately performs the same job Jekyll sets out to do; serve static content.

Therefore if you like to keep things simple and you prefer the command-line over an admin panel UI then give Jekyll a try.

Developers like Jekyll because we can write content like we write code:

- Ability to write content in markdown or textile in your favorite text-editor.
- Ability to write and preview your content via localhost.
- No internet connection required.
- Ability to publish via git.
- Ability to host your blog on a static web-server.
- Ability to host freely on GitHub Pages.
- No database required.

*if you liked this information, you might find this site interesting and very useful [informative Jekyll site](http://jekyllbootstrap.com/lessons/jekyll-introduction.html) scroll down pass all you've already read to "How Jekyll Works"* 
