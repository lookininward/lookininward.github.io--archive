---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
title: Michael Xavier
subtitle: software developer, product designer (ux/ui)
---

<!-- Latest Posts and Socia Media -->
<div class="flex-column flex-md-row-reverse mb-5">

	<div class="col col-12 col-lg-3 text-center text-md-left mb-3">
	    <div class="social-media">
	    <h3>Follow Me</h3>
		  <a href="https://www.linkedin.com/in/vinothmichaelxavier/" target="_blank"><img src="/assets/img/icons/linkedin2.svg"></a>
		  <a href="https://github.com/lookininward" target="_blank"><img src="/assets/img/icons/github.svg"></a>
		  <a href="http://stackoverflow.com/users/5513243/lookininward" target="_blank"><img src="/assets/img/icons/stackoverflow.svg"></a>
		</div>
	</div>

	<div class="col col-lg-9">
		<h3 class="text-center text-md-left">Latest Posts</h3>
		<ul class="list-unstyled text-center">
		{% for post in site.posts limit:3 %}
		  <li class="d-block d-md-flex">
		    <a href="{{post.url}}" class="mr-md-2">{{ post.title }} </a>
		    <div class="d-none d-md-flex">
		    	| {{ post.date | date_to_string }}
		    </div>
		  </li>
		{% endfor %}
		</ul>
	</div>
</div>

<div class="horizontal-divider"></div>

<!-- Most Recent Post -->
<div class="row">
	<div class="col col-lg-12 align-self-center">
		<div class="recent-posts">
		{% for post in site.posts limit:2 %}
		    <h1 class="display-5"><a href="{{ post.url }}">{{ post.title }}</a></h1>
		    <h6>{{ post.date | date_to_string }}</h6><br/>
		    {{ post.content }}
		    <div class="horizontal-divider"></div>
		{% endfor %}
		</div>
	</div>
</div>
