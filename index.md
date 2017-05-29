---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
title: Home Page
---

<!-- <div class="row">
	<div class="col col-lg-12">
		<p>This is in <b>index.md</b> This contains the content for the page. Not the layout.</p>
	</div>
</div><hr/> -->

<!-- Latest Posts and Socia Media -->
<div class="row">
	<div class="col col-lg-9">
		<h3>Latest Posts</h3>
		<ul class="list-unstyled">
		{% for post in site.posts limit:3 %}
		  <li>
		    <a href="{{ post.url }}">{{ post.title }}  </a> | {{ post.date | date_to_string }}
		  </li>
		{% endfor %}
		</ul>
	</div>

	<div class="col col-lg-3">
		<h3>Follow Me</h3>
	    <ul class="list-unstyled">
		  <li><a href="https://www.linkedin.com/in/vinothmichaelxavier/" target="_blank">LinkedIn</a></li>
		  <li><a href="https://github.com/lookininward" target="_blank">Github</a></li>
		  <li><a href="http://stackoverflow.com/users/5513243/lookininward" target="_blank">StackOverflow</a></li>
		</ul>
	</div>
</div><hr/>

<!-- Most Recent Post -->
<div class="row">
	<div class="col col-lg-12">
		{% for post in site.posts limit:1 %}
		    <h1 class="display-5">{{ post.title }}</h1>
		    <h6>{{ post.date | date_to_string }}</h6><br/>
		    {{ post.content }}
		{% endfor %}
	</div>
</div>


