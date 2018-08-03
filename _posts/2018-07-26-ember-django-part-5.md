---
layout: post
title: EmberJS Django - Part Five
description: Connect EmberJS with Django
categories: EmberJS JavaScript Django Python
tags: [EmberJS, JavaScript, Django, Python]
---

<!-- PART FIVE  --------------------------------------------------------------------------------------------------------------------------------------------->

<!-- INTRODUCTION ------------------------------------------------------------>
<section>
  <div class="row">

    <div class="col col-12 col-md-5">
      <img src="/assets/img/posts/2018/emberjs.png"
           class="img-fluid align-self-center mb-3 mb-md-0">

      <img src="/assets/img/posts/2018/python.jpg"
           class="img-fluid align-self-center mb-3 mb-md-0">

      <img src="/assets/img/posts/2018/django.png"
           class="img-fluid align-self-center mb-3 mb-md-0">
    </div>

    <div class="col col-12 col-md-7">
      <p>
        Welcome to <a>Part 5</a> of my 5 part tutorial '<b>Django and EmberJS Fullstack: Connecting the Backend to the Frontend</b>'.
      </p>

      <ul>
        <li>
          <a href="{{site.baseurl}}/emberjs/javascript/django/python/frontend/backend,/fullstack,/multipart/ember-django-part-1">
            Part 1
          </a>
        </li>
        <li>
          <a href="{{site.baseurl}}/emberjs/javascript/django/python/frontend/backend,/fullstack/ember-django-part-2">
            Part 2
          </a>
        </li>
        <li>
          <a href="{{site.baseurl}}/emberjs/javascript/django/python/frontend/backend,/fullstack/ember-django-part-3">
            Part 3
          </a>
        </li>
        <li>Part 4</li>
        <li>Part 5</li>
      </ul>
    </div>

  </div>
</section>

<!-- Setup JSON API ------------------>
<section>
  <!-- // Django -->
    Django REST framework JSON API: https://github.com/django-json-api/django-rest-framework-json-api

     <!-- // JSONAPI Adapter -->
    <!-- https://www.emberjs.com/api/ember-data/release/classes/DS.JSONAPIAdapter -->

  <!-- // Cleanup -->

  <!-- // Item Component -->
  {% highlight handlebars %}
    {% raw %}
      {{lb-item
        item=item
      }}
    {% endraw %}
  {% endhighlight %}
</section>

<!-- Books Route Template ------------->
<section>
  <h4 id="books-route-template">Books Route Template</h4>

  <!-- // Items Route Template -->
  {% highlight handlebars %}
  {% raw %}
    <div class="items">
      {{#each items as |item|}}
        {{lb-item
          item=item
        }}
      {{/each}}

    </div>
  {% endraw %}
  {% endhighlight %}
</section>

<!-- Book Detail Route --------------->
<section>
  <h4 id="book-detail-route">Book Detail Route</h4>
</section>

<!-- Book Detail Template ------------>
<section>
  <h4 id="book-detail-template">Book Detail Template</h4>
</section>

<!-- Conclusion -------------------------------------------------------------->
<section>
  <h3 id="conclusion">Conclusion</h3>
  <!-- // Show that get request works and the data being return is corrently formatted and Ember is able to display it properly without areas -->
</section>

