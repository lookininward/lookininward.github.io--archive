---
layout: page
title: Categories
description: these are the categories my posts belong to
permalink: /categories/
---

<!-- List of all the categories used in your posts. -->

{% capture categories %}
  {% for category in site.categories %}
    {{ category[0] }}
  {% endfor %}
{% endcapture %}
{% assign sortedcategories = categories | split:' ' | sort %}

{% for category in sortedcategories %}
  <h5 id="{{ category }}">{{ category }}</h5>
  <ul class="list-unstyled">
  {% for post in site.categories[category] %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
{% endfor %}