---
permalink: /blog/
author_profile: true
---


<div class="post-list">
  {% for post in site.posts %}
    <div class="post-card">
      <a class="post-link" href="{{ post.url | relative_url }}" target="_self">{{ post.title }}</a>
      <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <p class="post-excerpt">{{ post.excerpt }}</p>
    </div>
  {% endfor %}
</div>






