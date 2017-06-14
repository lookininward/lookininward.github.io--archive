---
layout: post
title: Fixed-to-Top on Scroll
description: Using jQuery to get navigation bar to fix itself to the top of the window when scrolling.
categories: javascript, jQuery
tags: [javascript, jQuery]
---
<section>
<p>Saw a request on StackOverflow for a way to have a banner that sat above the navigation bar when at the top of the window, and have the navigation bar become fixed to top when scrolling down. This is a simplified example that works using jQuery.</p>

<h3>The HTML Structure</h3>
<p>First, create a div with the className 'banner' above the Bootstrap navbar. The navbar does not have the 'fixed-top' class by default, positioning it under the banner div.</p>

{% highlight html %}
{% raw %}
<div class="banner">
  <h1>Sample Banner</h1>
</div>
<nav class="navbar navbar-light bg-faded" id="navbar">
  <a class="navbar-brand" href="#">Navbar</a>
</nav>
{% endraw %}{% endhighlight %}

</section>
<section>
<h3>Use jQuery to add/remove class</h3>
<p>Take advantage of jQuery since you're using Bootstrap. When the window has been scrolled all the way to the top, the 'fixed-top' class will be removed from the navbar element. In all other instances it will be added to the navbar element.</p>

{% highlight jQuery %}
{% raw %}
$(window).scroll(function(){
   if ($(window).scrollTop() == 0) {
    $(".navbar").removeClass("fixed-top");
 } else {
    $(".navbar").addClass("fixed-top");
 }
});
{% endraw %}{% endhighlight %}

<p>Now when you scroll down, the navbar gets fixed to the top. When you go back up to the top, it drops back under the main banner.</p>

<a href="https://codepen.io/lookininward/pen/RgRmWj" target="_blank">Check out the CodePen for a live example.</a>
</section>