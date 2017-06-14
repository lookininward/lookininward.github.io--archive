---
layout: post
title:  Setting up a Jekyll Blog with Bootstrap 4 - Part 1
description: Guide to setting up a Jekyll blog with Bootstrap 4, unique tag and category pages, among other key blog functionality.
categories: jekyll guide 
tags: [jekyll, guide]
---
<!-- Table of Contents -->
<section>
	<h3>This guide covers the following:</h3>

	<ul>
	<li>set up a fresh new Jekyll blog</li>
	<li>install boostrap 4 and plug into Jekyll</li>
	<li>code unique tag pages functionality</li>
	<li>code unique category pages functionality</li>
	</ul>

	This is no definitive guide on how to implement this functionality, nor am I a Jekyll expert. I use it regularly to run my blog and these are the steps I take to manage it.
</section>

<!-- Part 1 - Set up Blog and Configure -->
<section>
	<h3>1.1 Set up a fresh new Jekyll blog and configure it</h3>
	
	First install Jekyll using the <a href="https://jekyllrb.com/docs/quickstart/" target="_blank">official guide</a>. It's a straightforward process. In the directory of your choice create a new jekyll blog named <b>fresh_start</b>:

	{% highlight liquid %}
		# Create a new Jekyll site at ./fresh_start
		~ $ jekyll new fresh_start
	{% endhighlight %}

	<p>In<b>_config.yml</b>change the variables:</p>
	{% highlight yaml %}
		title: [Site_Title]
		permalink: none
	{% endhighlight %}
</section>



<!-- Part 2 - Setup the first page layout and add bootstrap class -->
<section>
	<h3>1.2 Create First Page Layout and Override the Default Theme</h3>
	<p>
	Go to the <b>_layouts</b> folder and create a new file called <b>home.html</b>. This will be the page that's rendered at the site's baseurl. Add a header with a boostrap class. Although default fonts will be used, Once boostrap is installed into the project, the header will look like this: insert image
	</p>

	{% highlight liquid %}
		<h1 class="display-3">page.title = {.{ page.title }}</h1>
	{% endhighlight %}
</section>

<!-- Install Boostrap 3 as a CDN and Local -->
<section>
	<h3>1.3 Install Bootstrap 4</h3>
	This guide is intended for the setup of key functionality. Not for installing boostrap.

	As a CDN: 

	{% highlight html %}
		<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/css/bootstrap.min.css" 
		integrity="sha384-rwoIResjU2yc3z8GV/NPeZWAv56rSmLldC3R/AZzGRnGxQQKnKkoFVhFQhNUwEyJ" crossorigin="anonymous">
		<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/js/bootstrap.min.js" integrity="
		sha384-vBWWzlZJ8ea9aCX4pEW3rVHjgjt7zpkNpZk+02D9phzyeVkE+jo0ieGizqPLForn" crossorigin="anonymous"></script>
	{% endhighlight %}

	As local files.

	For the full method of installing boostrap source files for use in your site <a href="#">click here</a>.

</section>


<section>
<h3>1.4 Go back to the base url home.html and confirm that the h1's styling has been updated</h3>
</section>


1.5 in _includes create header.html and footer.html
1.6 in _layouts/home.html include header.html and footer.html
check all the pages to make sure that the header and footer appear on every page
1.7 in _layouts create page.html
1.8 in _layouts create post.html
1.9 in /fresh_start create 

	about.md

	portfolio.md

	tags.md
		in /fresh_start create the "tags" folder
		create a new folder for every tag
		create a index.html file in each folder

	categories.md, 
		in /fresh_start create the "categories" folder
		create a new folder for every category
		create a index.html file in each folder

	articles.md

2.0 in _posts incude the following markdown files (download from git)


Bootstrap
- in /fresh_start create a js, scss, _data (portfolio) folders.













































