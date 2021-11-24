---
layout: default
title: Home
---

{% for post in site.posts %}
  <article style="overflow: hidden; margin-top: 10px">
    <a href="{{ post.url }}" style="float: left">
      {{ post.title }}
    </a>
    <time datetime="{{ post.date | date: "%Y-%m-%d" }}" style="float: right; font-size: small">{{ post.date | date_to_long_string }}</time>
  </article>
{% endfor %}
