---
layout: page
title: Tags
permalink: /tags/
---

All the tags used in your posts

{% capture tags %}
  {% for tag in site.tags %}
    {{ tag[0] }}
  {% endfor %}
{% endcapture %}
{% assign sortedtags = tags | split:' ' | sort %}

{% for tag in sortedtags %}
  <h3 id="{{ tag }}">{{ tag }} | and {{ tag.url }}</h3>
  <ul>
  {% for post in site.tags[tag] %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
{% endfor %}
