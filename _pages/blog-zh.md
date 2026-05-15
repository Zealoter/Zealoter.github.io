---
permalink: /zh/blog/
title: "博客与感悟"
author_profile: true
---

<div style="text-align: right; margin-bottom: 10px;"><a href="{{ site.baseurl }}/blog/">English</a> | <strong>中文</strong></div>

# 📝 博客与感悟

{% assign cn_posts = site.posts | where_exp: "post", "post.path contains '_posts/CN/'" %}
{% if cn_posts.size > 0 %}
  {% for post in cn_posts %}
    <article class="post">
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <p class="post-meta">{{ post.date | date: "%Y年%m月%d日" }}</p>
      <div class="post-excerpt">{{ post.excerpt | strip_html | truncate: 200 }}</div>
    </article>
  {% endfor %}
{% else %}
  <p>还没有博客文章，敬请期待！</p>
{% endif %}
