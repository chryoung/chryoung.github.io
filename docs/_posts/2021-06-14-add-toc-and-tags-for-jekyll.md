---
title: Add TOC and Tags page for Jekyll on GitHub Pages
tags: jekyll blog
---

Because the limited plugins GitHub Pages [supports](https://pages.github.com/versions/). Using plugins for generating TOC and tags page is not an option. But we can leverage the [Liquid](https://shopify.github.io/liquid/) template used by Jekyll to do this.

## Add TOC

There is a well-written Jekyll plugin for generating TOC using Liquid: [allejo/jekyll-toc](https://github.com/allejo/jekyll-toc).

It doesn't require any ruby gem. So it works well with GitHub Pages.

To use it

{% raw %}
1. Download the [Liquid template](https://raw.githubusercontent.com/allejo/jekyll-toc/master/_includes/toc.html).
2. Edit `_layouts/post.html` file in your Jekyll project. If you don't have this file. See [Jekyll Theme Customization](#jekyll-theme-customization).
3. Add the following code to somewhere above `{{ content }}`.

   ```html
   <div class="toc">
       <h2>Table of Contents</h2>
       {% include toc.html html=content %}
   </div>
   ```
{% endraw %}

That's all!

## Add Tags Page

We will also use Liquid for generating tags page.

Steps:

{% raw %}
1. Create a new file `_layouts/tags.html` under your Jekyll project.
2. Add to `_layouts/tags.html`.

   ```html
   ---
   layout: default
   ---
   {% for tag in site.tags %}
   <h3 id="{{tag[0]}}">{{ tag[0] }}</h3>
   <ul>
       {% for post in tag[1] %}
       <li><a href="{{ post.url }}">{{ post.title }}</a></li>
       {% endfor %}
   </ul>
   {% endfor %}
   ```
3. Create a file `tags.md` on the folder where `index.md` is.
4. Add to `tags.md` file.

   ```
   ---
   title: Tags
   layout: tags
   ---
   ```
5. For the post you want to tag, add `tags: tag1 tag2` to the front matter.

{% endraw %}

## Jekyll Theme Customization

There is a whole [official document](https://jekyllrb.com/docs/permalinks/) talking about the Jekyll theme.

In general, the theme is installed as ruby gem. You can customize it by overriding parts of theme files.

To find the original theme files, use the command `bundle info --path your_theme`. e.g. Your theme is minima, use `bundle info --path minima` to find the path.

If you want to customize the post layout, copy `_layouts/post.html` in the folder found by the command above to your Jekyll project root. Then edit it.

## Copyright

This post is written by chryoung. You can copy/paste if you cite the source.
