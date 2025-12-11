---
layout: page
title: Stay Hunry, Stay Foolish!
tagline: Hacker, Football, Hiking
---
{% include JB/setup %}



## Article
<ul class="posts">
  {% assign count = 0 %}
  {% assign one_year_seconds = 31536000 %}
  {% capture current_time_minus_year %}{{ site.time | date: "%s" | minus: one_year_seconds }}{% endcapture %}
  {% for post in site.posts %}
    {% capture post_time_seconds %}{{ post.date | date: "%s" }}{% endcapture %}
    {% assign post_time_int = post_time_seconds | plus: 0 %}
    {% assign cutoff_time_int = current_time_minus_year | plus: 0 %}
    {% if post_time_int > cutoff_time_int and count < 20 %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
      {% assign count = count | plus: 1 %}
    {% endif %}
  {% endfor %}
</ul>

<p><em>Showing recent posts from the last year (max 20). <a href="{{ BASE_PATH }}/archive.html">View all posts in the archive</a>.</em></p>

## About me
<p>twitter:</p><a href="https://twitter.com/zolibra">zolibra</a>
