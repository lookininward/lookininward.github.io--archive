---
layout: post
title:  Multiple Github Pages Subsites
description: The simplest, straightforward way to setup github pages subsites
categories: jekyll guide github
tags: [jekyll, guide, github]
---
<section>
	<h3>Setup the Subsite Repository</h3>
	<p>In Github create a new repository. The name of this repo will be part of the URL to access the subsite, like so: <b>username@github.io/repoName</b>. Do not initialize it with <b>README.md</b></p>
	<p>Next, clone the repository to your computer and create an <b>index.html</b> file in the repository's root. Add some basic content like a header.</p>
</section>
<section>
	<h3>Set the Remote URL</h3>
	<p>In terminal, navigate to the repository root, set the branch, and push it to github pages as follows:</p>

	{% highlight terminal %}
	{% raw %}
	$ git branch -m master gh-pages
	$ git push -u origin gh-pages
	{% endraw %}{% endhighlight %}

	<p>Now when you visit the URL <b>username.github.io/repoName</b> it should correctly render the <b>index.html</b> page that we created in the repo with its basic content.</p>

	<p>That's it, now you have a simple github page subsite up and running. As far as I can tell, there are no upper limits to the number of subsites you are able to create.</p>
</section>














































