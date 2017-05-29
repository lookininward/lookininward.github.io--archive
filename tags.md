---
layout: page
title: Tags
description: these are the tags used in my posts
permalink: /tags/
---

<div class="row">
	<div class="col col-lg-12">
		<!-- All the tags used in your posts -->

		{% capture tags %}
		  {% for tag in site.tags %}
		    {{ tag[0] }}
		  {% endfor %}
		{% endcapture %}
		{% assign sortedtags = tags | split:' ' | sort %}

		{% for tag in sortedtags %}
		  <h5 id="{{ tag }}">{{ tag }}</h5>
		  <ul class="list-unstyled">
		  {% for post in site.tags[tag] %}
		    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
		  {% endfor %}
		  </ul>
		{% endfor %}
	</div>
</div>

