---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
title: Home Page
---


This is in index.md This contains the content for the page. Not the layout.


<h3>List of Posts with Links to Post Page</h3>
<ul>
{% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">
      {{ post.title }}
    </a>
  </li>
{% endfor %}
</ul>