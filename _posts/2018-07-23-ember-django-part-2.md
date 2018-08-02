---
layout: post
title: EmberJS Django - Part Two
description: Connect EmberJS with Django
categories: EmberJS JavaScript Django Python Frontend Backend, Fullstack
tags: [EmberJS, JavaScript, Django, Python, Frontend, Backend, Fullstack]
---

<!-- PART TWO  ---------------------------------------------------------------------------------------------------------------------------------------------->

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
        Welcome to <a>Part 2</a> of my three part tutorial '<b>Django and EmberJS Fullstack: Connecting the Backend to the Frontend</b>'.
      </p>

      <ul>
        <li>
          <a href="#"  target="_blank">
            Part 1
          </a>
        </li>
        <li>Part 2</li>
        <li>
          <a href="#" target="_blank">
            Part 3
          </a>
        </li>
        <li>
          <a href="#" target="_blank">
            Part 4
          </a>
        </li>
      </ul>
    </div>

  </div>
</section>

<!-- CREATE DJANGO PROJECT —————————------------------------------------------>
<section>

  <h3>Backend: Create Django Project, Project App, Models, Views,  </h3>

  <p>
    The first step is to use Django to create the project folder.
  </p>

  {% highlight bash %}
    # cd into your virtual environment folder 'server'
    cd /desktop/server

    # initialize the virtual environment
    source bin/activate

    # use django to create the project site directory
    django-admin startproject myLibrary

    # cd into the project directory ## desktop/server/myLibrary
    cd myLibrary

    #use python to run the django server
    python manage.py runserver
  {% endhighlight %}

  <p>
    Now you can visit localhost:8000 in your browser and confirm that the Django base project is working.
  </p>

  ## screenshot

  <p>
    You can shutdown the server with <code>cmd+ctrl</code>
  </p>
</section>

<!-- Create New App ---------------->
<section>

  <h6 id="create-new-app">Create a new 'App'</h6>

  <p>
    Think of Django apps as modules that plugin into your project 'myLibrary'. We will create an app called 'Books' that will house models, views, serializers. and the api for interacting with the Books data in the database.
  </p>

  <p>
    Check out <a href="https://stackoverflow.com/questions/19350785/what-s-the-difference-between-a-project-and-an-app-in-django-world" target="_blank">this thread</a> to get a clearer understanding of the differences between Projects and Apps.
  </p>

  {% highlight python %}
    # create new app 'books'
    python3 manage.py startapp books

    # creates the directory /desktop/myLibrary/books
  {% endhighlight %}

  <p>
    Now we will install the 'books' app into the 'myLibrary' project. Opening up myLibrary's settings file: <code>desktop/myLibrary/settings.py</code>.
  </p>

  <p>
    Scroll to the <code>INSTALLED_APPS</code> array. Django has installed it's own core apps. Install the 'books' app at the end of the array.
  </p>

  {% highlight python %}
    INSTALLED_APPS = [
      ...
      'books'
    ]
  {% endhighlight %}
</section>

<!-- Describe books model ------------>
<section>
  <h6 id="describe-book-model">Describe the 'book' model</h6>

  <p>
    Now we will describe the 'book' model in the 'books' app. Open up book's models file: <code>desktop/myLibrary/books/models.py</code>.
  </p>

  {% highlight python %}
    from django.db import models

    class Item(models.Model):
      title       = models.CharField(max_length=500)
      author      = models.CharField(max_length=100)
      description = models.TextField()
  {% endhighlight %}

  <p>
    Every 'book' in the database will have a 'title' upto 500 characters in length, an 'author' field upto 100, and a 'description' field with an open-ended number.
  </p>
</section>

<!-- Create views -------------------->
<!-- Is it neccessary to create html views if only using as database? -------->
<section>
  <h6 id="create-views">Create 'views' to access the book data</h6>

  <p>
    Now we will create the 'views' for our 'books' app. Open up book's views file: <code>desktop/myLibrary/books/views.py</code>.
  </p>

  {% highlight python %}
    from django.shortcuts import render
    from django.http import HttpResponse

    from .models import Item

    def home(request):
      items = Item.objects.all()
      return render(request, 'home.html', {'items' : items})

    def item_detail(request, id):
      try:
        item = Item.objects.get(id=id)
      except Item.DoesNotExist:
        raise Http404('Item not found')
      return render(request, 'item_detail.html', {'item' : item})
  {% endhighlight %}
</section>


<!-- Register Admin for Item --------->
<!-- Why do you register the item with the admin? ---------------------------->
<section>
  <h6 id="register-admin">Register the 'book' model in the 'Admin'</h6>

  <p>
    Now we will register the 'book' with the 'admin' for our books app. Open up book's admin file: <code>desktop/myLibrary/books/admin.py</code>.
  </p>

  {% highlight python %}
    from django.contrib import admin

    from .models import Item

    @admin.register(Item)
    class ItemAdmin(admin.ModelAdmin):
      list_display = ['title', 'subtitle', 'author', 'description', 'cover']
  {% endhighlight %}
</section>

<!-- Configure the Item app -------------------------------------------------->
<!-- Why do we configure the Items in apps.py? ------------------------------->
<section>
  <h6 id="register-admin">Register the 'book' model in the 'Admin'</h6>

  <p>
    Now we will configure the 'books' model with our apps (books). Open up book's apps file: <code>desktop/myLibrary/books/apps.py</code>.
  </p>

  {% highlight python %}
    from django.apps import AppConfig

    class ItemsConfig(AppConfig):
        name = 'items'
  {% endhighlight %}
</section>

<!-- CONCLUSION -----------—————————------------------------------------------>
<section>
  <h3>Conclusion</h3>
  <p>
    We've completed the following steps:
  </p>

  <ul>
    <li>Created the Django project called myLibrary</li>
    <li>Created a new app called Books</li>
    <li>Described the books model</li>
    <li>Created views for the books data</li>
    <li>Registered the book model with the admin</li>
    <li>Configured the books data in apps</li>
  </ul>

  <p>In part three we will begin creating the REST API that will deliver data to our frontend EmberJS client.</p>
</section>

