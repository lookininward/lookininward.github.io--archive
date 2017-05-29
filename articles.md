---
layout: page
title: Articles
description: these are all the articles I've written
permalink: /articles/
---

<!-- <div class="row justify-content-start">
	<div class="col col-lg-12"> -->
<!-- This is the content for the articles page. It is encapsulated by the structure in <b>_layouts/page.html</b>.
 -->
<!-- <h3>Full List of Posts with Links to Post Page</h3> -->
<ul>
{% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }} </a>| {{ post.date | date_to_string }}
  </li>
{% endfor %}
</ul>
<!-- 	</div>
</div> -->
