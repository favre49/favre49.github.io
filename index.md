---
layout: default
title: Home
---

{% for post in site.posts %}
  <article style="overflow: hidden; margin-top: 10px">
    <a href="{{ post.url }}" style="float: left">
      {{ post.title }}
    </a>
    <div style="float:right">
    <time datetime="{{ post.date | date: "%Y-%m-%d" }}" style="font-size: small">{{ post.date | date_to_long_string }}</time>
    </div>
  </article>
{% endfor %}
