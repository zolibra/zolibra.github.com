---
layout: page
title: Stay Hunry, Stay Foolish!
tagline: Hacker, Football, Hiking
---
{% include JB/setup %}



## Article
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## About me
<p>twitter:</p><a href="https://twitter.com/zolibra">zolibra</a>
