---
layout: default
title: Blog
---

## Blog articles

{% for post in site.posts %}
<p><a href="{{ post.url }}">{{ post.title }}</a></p>
{% endfor %}
