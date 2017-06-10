---
layout: post
title:  Categories & Tag Lists in Jekyll
description: Guide to setting up a Jekyll blog with Bootstrap 4, unique tag and category pages, among other key blog functionality.
categories: jekyll guide 
tags: [jekyll, guide]
---
<section>
	<h3>Step 1: Create a new page layout template</h3>
	<p>In <b>root/_layouts</b> create a new file called "<b>page.html</b>", with the following:</p>

	{% highlight liquid html %}
	{% raw %}<div class="header">
	  <h1>{{ page.title }}</h1> <!-- This will pull the "title" value from categories.md -->
	  <p>{{ page.description }}</p> <!-- This will pull the "description" value from categories.md -->
	</div>

	<div class="content">
	  {{ content }} <!-- This will pull in the content from categories.md -->
	</div>{% endraw %}
	{% endhighlight %}

	<h3>Step 2: Create a new page to hold categories content</h3>

	<p>In <b>root/</b> create a new file called "<b>categories.md</b>", with the following:</p>

	{% highlight liquid %}{% raw %}
	---
	layout: page <!-- This selects root/_layouts/page.html as the page template for the categories.md page. -->
	title: Categories <!-- This is the value inserted into <h1>{{ page.title }}</h1> in root/_layouts/page.html. -->
	description: these are the categories my posts belong to <!-- This is the value inserted into <p>{{ page.description }}</p> in root/_layouts/page.html. -->
	permalink: /categories/ <!-- The permanent link to this static page - root/categories/ -->
	---
	{% endraw %}{% endhighlight %}

	<p>Underneath this section we can start to capture all the categories that have been assigned to our posts.</p>
	{% highlight liquid %}{% raw %}
	{% capture categories %}
	  {% for category in site.categories %}
	    {{ category[0] }}
	  {% endfor %}
	{% endcapture %}
	{% assign sortedcategories = categories | split:' ' | sort %}
	{% endraw %}{% endhighlight %}

	<p>Captures the string inside of the opening and closing tags and assigns it to a variable. Variables that you create using capture are stored as strings.<a href="https://help.shopify.com/themes/liquid/tags/variable-tags#capture">Link</a></p>

	<p>Next, we loop through the sortedcategories variable that we've assigned with an array of strings of the categories we've captured and output each category and posts tagged with that category through an ordered list.</p>
	{% highlight liquid %}{% raw %}
	{% for category in sortedcategories %}
	  <h5>{{ category }}</h5> <!-- This will pull the "category" value from each unique category used in our posts. -->
	  <ul>
	  {% for post in site.categories[category] %} <!-- Every post under the category is outputted with its title and a direct link to the post. -->
	    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
	  {% endfor %}
	  </ul>
	{% endfor %}
	{% endraw %}{% endhighlight %}

	<h3>Step 3: Make sure everything is being generated correctly</h3>
	<p>The <b>root/categories/</b> page should now have header with the title, page description, and a list of every category used in our posts, as well as each post under that category with a direct link to that post.</p>

	<p>Make sure your posts are within <b>root/_posts/</b> and they contain the following at the top of each post:</p>

	{% highlight liquid %}{% raw %}
	---
	layout: post
	title:  This is a title
	categories: jekyll guide <!-- each of these terms separated by a space is a standalone category. -->
	---
	{% endraw %}{% endhighlight %}

</section>