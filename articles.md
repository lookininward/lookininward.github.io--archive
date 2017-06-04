---
layout: page
title: Articles
description: all the articles I've written
permalink: /articles/
---

<div class="container">
<!-- Article List -->
<h3>By Date</h3>
<ul class="list-unstyled">
{% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }} </a>| {{ post.date | date_to_string }}
  </li>
{% endfor %}
</ul><br/>


<!-- Category List  -->
<h3>By Category</h3>
{% capture categories %}
  {% for category in site.categories %}
    {{ category[0] }}
  {% endfor %}
{% endcapture %}
{% assign sortedtags = categories | split:' ' | sort %}

{% for category in sortedtags %}
  <h5 id="{{ tag }}">{{ category }}</h5>
  <ul class="list-unstyled">
  {% for post in site.categories[category] %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
{% endfor %}
</div>