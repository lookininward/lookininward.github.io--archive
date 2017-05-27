---
layout: page
title: Portfolio
permalink: /portfolio/
variable: hello
---

A Place to Keep the Projects You've Worked On

<ul>
{% for project in site.data.projects %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {{ project.title }}
    </a>
  </li>
{% endfor %}
</ul>