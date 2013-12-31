---
layout: default
title: Blog
---

# Blog articles

{% for post in site.posts %}
<p><a href="{{ post.url }}">{{ post.title }}</a> <small>({{ post.date | date: "%b %-e, %Y" }})</small></p>
{% endfor %}
