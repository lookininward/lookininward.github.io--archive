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
        Welcome to <a>Part 2</a> of my 5 part tutorial '<b>Django and EmberJS Fullstack: Connecting the Backend to the Frontend</b>'.
      </p>

      <ul>
        <li>
          <a href="{{site.baseurl}}/emberjs/javascript/django/python/frontend/backend,/fullstack,/multipart/ember-django-part-1">
            Part 1
          </a>
        </li>
        <li>Part 2</li>
        <li>
          <a href="{{site.baseurl}}/emberjs/javascript/django/python/frontend/backend,/fullstack/ember-django-part-3">
            Part 3
          </a>
        </li>
        <li>
          <a href="#">
            Part 4
          </a>
        </li>
        <li>
          <a href="#">
            Part 5
          </a>
        </li>
      </ul>
    </div>

  </div>
</section>

<!-- CREATE DJANGO PROJECT —————————------------------------------------------>
<section>

  <h3>Backend: Create Django Project, Project App, Models, Views</h3>

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
    Now you can visit localhost:8000 in your browser and confirm that the Django base project is working. Ignore the console errors regarding migrations for the moment.
  </p>

  <img src="/assets/img/posts/2018/django-server.png"
           class="img-fluid align-self-center mb-2">

  <p>
    You can shutdown the server with <code>cmd+ctrl</code>
  </p>
</section>

<!-- Create Superuser Account -------->
<section>

  <h4 id="create-superuser">Create the administrative account (superuser)</h4>

  <p>
    Let's create a 'superuser' that will allow us to login to the admin site and handle our database data.
  </p>

  {% highlight python %}
    # create superuser
    python3 manage.py createsuperuser
  {% endhighlight %}

  <p>
    Fill in the field for Username, Email Address (optional), and Password. You should get a message saying <code>Superuser created successfully</code>.
  </p>

  <p>
    Now run the server with <code>python3 manage.py runserver</code> and go to <code>http://localhost:8000/admin/</code> to see the admin login page. Enter your superuser account details and you will be logged in.
  </p>

  <img src="/assets/img/posts/2018/django-admin.png"
           class="img-fluid align-self-center mt-5 mb-5">
</section>

<!-- Create New App ---------------->
<section>

  <h4 id="create-new-app">Create a new 'App'</h4>

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
    Now we will install the 'books' app into the 'myLibrary' project. Opening up myLibrary's settings file: <code>desktop/server/myLibrary/myLibrary/settings.py</code>.
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
  <h4 id="describe-book-model">Describe the 'book' model</h4>

  <p>
    Now we will describe the 'book' model in the 'books' app. Open up book's models file: <code>desktop/server/myLibrary/books/models.py</code>.
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

<!-- Register Admin for Item --------->
<section>
  <h4 id="register-admin">Register the 'book' model in the 'Admin'</h4>

  <p>
    Now we will register the 'book' with the 'admin' for our books app so that we can view it in the admin panel and manipulate the books data from there Open up book's admin file: <code>desktop/server/myLibrary/books/admin.py</code>.
  </p>

  {% highlight python %}
    from django.contrib import admin

    from .models import book

    @admin.register(book)
    class bookAdmin(admin.ModelAdmin):
      list_display = ['title', 'author', 'description']
  {% endhighlight %}

  <p>
    Now run the server with <code>python3 manage.py runserver</code> and go to <code>http://localhost:8000/admin/</code> and login. Now that the book model has been registered with the admin it is displayed in the admin panel.
  </p>

  <img src="/assets/img/posts/2018/django-admin-2.png"
       class="img-fluid align-self-center mt-5 mb-5">

  <p>
    If you click on books you will see an empty list. Click 'Add Book' to begin creating a new database item.
  </p>

  <img src="/assets/img/posts/2018/django-admin-3.png"
       class="img-fluid align-self-center mt-5 mb-5">

  <p>
    Once you save and go back to the list, you will see it displayed along with it's title, author, and description (<code>list_display</code>).
  </p>

  <img src="/assets/img/posts/2018/django-admin-4.png"
       class="img-fluid align-self-center mt-5 mb-5">

  <p>
    Congrats now we can view out database items in the admin panel, and create, edit, and delete items from the database.
  </p>
</section>

<!-- Optional ----------------------------------------------------------------------------------------------------------------------------------------------->

<!-- Create views -------------------->
<!-- <section>
  <h4 id="create-views">Create 'views' to access the book data</h4>

   <p>
    Before we create our views let's create a folder called 'templates' and an html document called 'home' inside the books folder: <code>desktop/server/myLibrary/books/templates/home.html</code>.
  </p>

  <p>
    In the final stage of the application we will not have to use these templates because Django will act as backend only, serving up data to our frontend client (EmberJS). This is simply show the data loading for demonstrative purposes.
  </p>

  {% highlight html %}
  {% raw %}
    <div>
      {% for book in books %}
        <div class="book-name">
          <h3>{{ book.title }}</h3>
          <p>{{ book.author }}</p>
          <p>{{ book.description }}</p>
        </div>
      {% endfor %}
    </div>
  {% endraw %}
  {% endhighlight %}

  <p>
    Now we will create the 'views' for our 'books' app. Open up book's views file: <code>desktop/server/myLibrary/books/views.py</code>.
  </p>

  {% highlight python %}
    from django.shortcuts import render
    from django.http import HttpResponse

    from .models import book

    def home(request):
      books = book.objects.all()
      return render(request, 'home.html', {'books' : books})
  {% endhighlight %}
</section> -->


<!-- Configure the Item app -------------------------------------------------->
<!-- Why do we configure the Items in apps.py? ------------------------------->
<!-- https://stackoverflow.com/questions/32795227/what-is-the-purpose-of-apps-py-in-django-1-9 -->
<!-- <section>
  <h4 id="register-admin">Register the 'book' model in the 'Admin'</h4>

  <p>
    Now we will configure the 'books' model with our apps (books). Open up book's apps file: <code>desktop/server/myLibrary/books/apps.py</code>.
  </p>

  {% highlight python %}
    from django.apps import AppConfig

    class ItemsConfig(AppConfig):
        name = 'items'
  {% endhighlight %}
</section>
 -->

<!-- CONCLUSION -----------—————————------------------------------------------>
<section>
  <h3 id="conclusion">Conclusion</h3>
  <p>
    We've completed the following steps:
  </p>

  <ul>
    <li>Created the Django project called myLibrary</li>
    <li>Created a new app called Books</li>
    <li>Described the books model</li>
    <li>Registered the book model with the admin</li>
    <!-- <li>Created views for the books data</li> -->
    <!-- <li>Configured the books data in apps</li> -->
  </ul>

  <p>In <a href="#">part three</a> we will begin creating the REST API that will deliver data to our frontend EmberJS client.</p>
</section>

<!-- https://stackoverflow.com/questions/34548768/django-no-such-table-exception -->
<!-- https://stackoverflow.com/questions/32795227/what-is-the-purpose-of-apps-py-in-django-1-9 -->
<!-- https://docs.djangoproject.com/en/2.1/ref/contrib/admin/ -->