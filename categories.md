---
layout: page
title: Categories
permalink: /categories/
---

List of all the categories used in your posts.

{% capture categories %}
  {% for category in site.categories %}
    {{ category[0] }}
  {% endfor %}
{% endcapture %}
{% assign sortedtags = categories | split:' ' | sort %}

{% for category in sortedtags %}
  <h3 id="{{ tag }}">{{ category }}</h3>
  <ul>
  {% for post in site.categories[category] %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
{% endfor %}