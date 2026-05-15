---
permalink: /zh/blog/
title: ""
excerpt: ""
author_profile: true
lang: zh
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

<span class='anchor' id='blog'></span>

# 📝 博客与感悟

{% assign cn_posts = site.posts | where_exp: "post", "post.path contains '_posts/CN/'" | sort: 'date' | reverse %}
{% if cn_posts.size > 0 %}
{% for post in cn_posts %}
<div class="paper-box" style="margin-bottom: 30px;">
  <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
  <p class="page__meta">{{ post.date | date: "%Y年%m月%d日" }}</p>
  <div class="archive__item-excerpt">
    {{ post.excerpt | strip_html | truncate: 200 }}
  </div>
</div>
{% endfor %}
{% else %}
<p>还没有博客文章，敬请期待！</p>
{% endif %}
