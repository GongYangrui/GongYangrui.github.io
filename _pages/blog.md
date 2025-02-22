---
permalink: /blog
author_profile: true
layout: default
---

<h2>Welcome to my blog!</h2>

<ul>
{% for post in site.posts %}
  <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a> - {{ post.date | date: "%Y-%m-%d" }}</li>
{% endfor %}
</ul>
