---
layout: page
title: Django
category: Django
---

{% for post in site.posts %}

{% if post.` == page.` %}

  <li>{{ post.date | date: "%Y / %m / %d" }} — <a href="{{ post.url }}">{{ post.title }}</a></li>

{% endif %}

{% endfor %}