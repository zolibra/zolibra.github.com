---
layout: page
title: This is Anfield!
tagline: Liverpool, Geek, Hiking
---
{% include JB/setup %}



## Article
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## About me


