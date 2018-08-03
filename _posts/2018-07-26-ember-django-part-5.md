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

<!-- The Problem --------------------->
<section>

  <p>
    At the end of Part 4 we saw how Ember was picking up the JSON data from Django, however it wasn't structured in the way that Django likes.
  </p>

  <p>
    Before
  </p>

  <p>
    After
  </p>
</section>

<!-- Install JSON API ---------------->
<section>
  <h4 id="install-node">Install JSON API</h4>
  <p>
    Install <code>$ pip install djangorestframework-jsonapi</code>
    <a href="https://github.com/django-json-api/django-rest-framework-json-api" target="_blank">Documentation</a>
  </p>

  <p>
    Install inside myLibrary:
  </p>

  {% highlight python %}
    REST_FRAMEWORK = {
      'PAGE_SIZE': 10,
      'EXCEPTION_HANDLER': 'rest_framework_json_api.exceptions.exception_handler',
      'DEFAULT_PAGINATION_CLASS':
          'rest_framework_json_api.pagination.JsonApiPageNumberPagination',
      'DEFAULT_PARSER_CLASSES': (
          'rest_framework_json_api.parsers.JSONParser',
          'rest_framework.parsers.FormParser',
          'rest_framework.parsers.MultiPartParser'
      ),
      'DEFAULT_RENDERER_CLASSES': (
          'rest_framework_json_api.renderers.JSONRenderer',
          'rest_framework.renderers.BrowsableAPIRenderer',
      ),
      'DEFAULT_METADATA_CLASS': 'rest_framework_json_api.metadata.JSONAPIMetadata',
      'DEFAULT_FILTER_BACKENDS': (
          'rest_framework.filters.OrderingFilter',
      ),
      'ORDERING_PARAM': 'sort',
      'TEST_REQUEST_RENDERER_CLASSES': (
          'rest_framework_json_api.renderers.JSONRenderer',
      ),
      'TEST_REQUEST_DEFAULT_FORMAT': 'vnd.api+json'
  }
  {% endhighlight %}
</section>

<!-- Books Route Template ------------>
<section>
  <h4 id="books-route-template">Books Route Template</h4>

  <p>
    Let's update the books route template to list any books coming through:
  </p>

  {% highlight handlebars %}
  {% raw %}
    {{#each model as |book|}}
      <div class="book">
        <div class="book-title">{{book.title}}</div>
        <div class="book-description">{{book.description}}</div>
      </div>
    {{/each}}
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

<!-- Conclusion ---------------------->
<section>
  <!-- // Show that get request works and the data being return is corrently formatted and Ember is able to display it properly without areas -->
  <h3 id="conclusion">Conclusion</h3>

  <p>
    We've completed the following steps:
  </p>

  <ul>
    <li>Identified the problem with the data coming from Django</li>
    <li>Installed JSON API into Django</li>
    <li>Updated the Books Route Template</li>
    <li>Created the book detail route and template</li>
    <li>Successfully viewing, editing, and deleting records from the db from EmberJS client</li>
  </ul>

  <p>
    Thank you for sticking with it.
  </p>
</section>

