---
permalink: /blog/
title: "Blog & Thoughts"
author_profile: true
---

<div style="text-align: right; margin-bottom: 10px;"><strong>English</strong> | <a href="{{ site.baseurl }}/zh/blog/">中文</a></div>

# 📝 Blog & Thoughts

{% assign en_posts = site.posts | where_exp: "post", "post.path contains '_posts/EN/'" %}
{% if en_posts.size > 0 %}
  {% for post in en_posts %}
    <article class="post">
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
      <div class="post-excerpt">{{ post.excerpt | strip_html | truncate: 200 }}</div>
    </article>
  {% endfor %}
{% else %}
  <p>No blog posts yet. Check back soon!</p>
{% endif %}
