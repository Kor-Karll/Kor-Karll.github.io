---
layout: page
title: DB
category: DB
---

{% for post in site.posts %}

{% if post.category == page.category %}

  <li>{{ post.date | date: "%Y / %m / %d" }} — <a href="{{ post.url }}">{{ post.title }}</a></li>

{% endif %}

{% endfor %}