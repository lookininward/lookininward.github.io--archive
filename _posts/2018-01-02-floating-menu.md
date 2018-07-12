---
layout: post
title: Floating Menu for Full Bleed Content Pages
description: A simple floating menu for full-bleed content pages
categories: javascript, front-end
tags: [javascript]
---
<section>
<p>
  Sometimes you have applications that demand the maximum amount of content be displayed for users. Here even the smallest vertical or horizontal menus take too much real estate. One relatively simple solution involves a floating menu bar that pops open when you need it and melts away when interacting with the main content.
</p>
<img src="/assets/img/posts/2018/floating-menu.gif" class="img-fluid mt-3">
</section>

<section>
<h3>HTML</h3>
<p>The structure is simple: The 'header' div contains the content that appears when the menu is collapsed and the 'items' div contains the menu items that appear when the menu is expanded.</p>


{% highlight html %}
  <div class="menu" id="menu">
    <div class="header">
      <i class="fa fa-bars" aria-hidden="true"></i>
    </div>
    <div class="items">
      <div class="link">Home</div>
      <div class="link">Office</div>
      <div class="link">Market</div>
      <div class="link">Gym</div>
      <div class="link">Park</div>
    </div>
  </div>
{% endhighlight %}

</section>

<section>
<h3>CSS</h3>
<p>
  The CSS(SCSS) determines that the 'menu' div is collapsed, small, transparent and overlaid over all page content. It maintains its place on the screen while scrolling for ease of access.
</p>

{% highlight scss %}
  .menu {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 99;
    position: fixed;
    top: 24px;
    left: 24px;
    width: 50px;
    height: 50px;
    background-color: #7C93B2;
    border: 2px solid #fff;
    border-radius: 120%;
    color: #fff;
    cursor: pointer;
    opacity: .3;
    transition: .2s;

      &:hover {
       background-color: #3D4049;
       opacity: 1;
    }
  }
{% endhighlight %}

<p>
  When expanded it becomes larger, more rectangular, and visible.
</p>

{% highlight scss %}
  .menu--expanded {
    width: 150px;
    height: 200px;
    background: #7C93B2;
    color: #fff;
    border-radius: 10px;
    opacity: 1;
    transition: .2s;

    &:hover {
     background: #7C93B2;
   }
  }
{% endhighlight %}

<p>
  When the menu is collapsed the header is visible and the items list is hidden. On expansion the opposite happens.
</p>

{% highlight scss %}
  .menu--expanded .header {
    display: none;
  }

  .items {
    display: none;
    width: 100%;
  }

  .menu--expanded .items {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
{% endhighlight %}

<p>
  The 'items' div has a set of 'link' divs. Since they are contained within the 'items' div they are also visible when expanded and invisible when collapsed.
</p>

{% highlight scss %}
  .link {
    margin: 5px 0;
    padding: 4px;
    width: 100%;
    border-radius: 5px;
    font-size: 16px;
    text-align: center;

   &:hover {
    background-color: #3d4049;
   }
  }
{% endhighlight %}
</section>

<section>
<h3>JavaScript</h3>
<p>
  The JavaScript does two things: 1) it grabs the 'menu' div and adds and EventListener that runs the 'expandMenu' function when it is clicked. Clicking adds the 'menu - expanded' modifier class to the 'menu' div which induces the visual changes we've written in the CSS.
</p>

{% highlight javascript %}
  const menu = document.getElementById('menu');

  function expandMenu() {
    if (!menu.classList.contains('menu--expanded')) {
      menu.classList.add('menu--expanded');
    }
  }

  menu.addEventListener("click", expandMenu);
{% endhighlight %}

<p>
  2) It detects when the user clicks away from the 'menu' div onto any other element on screen. When the user clicks outside the 'menu' div the 'menu - expanded' class modifier is removed and we revert to the collapsed menu.
</p>

{% highlight javascript %}
  // Remove menu--expanded class on click away
  document.addEventListener('click', function(event) {

    var clickInside =  menu.contains(event.target);

    if (clickInside) {
    } else {
      menu.classList.remove('menu--expanded');
    }
  });
{% endhighlight %}

<img src="/assets/img/posts/2018/floating-menu-2.gif"
     class="img-fluid mt-3 mb-5">

<a href="https://codepen.io/lookininward/pen/aLJBoE"
   target="_blank"
   class="mt-4">
 Check out the CodePen for a live example.
</a>
</section>