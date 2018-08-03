---
layout: post
title: EmberJS Django - Part Three
description: Connect EmberJS with Django
categories: EmberJS JavaScript Django Python Frontend Backend, Fullstack
tags: [EmberJS, JavaScript, Django, Python, Frontend, Backend, Fullstack]
---

<!-- PART THREE  -------------------------------------------------------------------------------------------------------------------------------------------->

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
        Welcome to <a>Part 3</a> of my 5 part tutorial '<b>Django and EmberJS Fullstack: Connecting the Backend to the Frontend</b>'.
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
        <li>Part 3</li>
        <li>
          <a href="#" target="_blank">
            Part 4
          </a>
        </li>
        <li>
          <a href="#" target="_blank">
            Part 5
          </a>
        </li>
      </ul>
    </div>

  </div>
</section>

<!-- Create API -------------------------------------------------------------->
<section>
  <h3>Backend: Create Django Project, Project App, Models, Views</h3>
</section>

<!-- Install Django REST Framework --->
<section>
  <h4 id="install-framework">Install Django REST Framework</h4>

  <p>Let's start by installed the Django REST Framework. With your virtualenv activated run the following commands:</p>

  <p>
    For more information checkout out the <a href="http://www.django-rest-framework.org/#installation" target="_blank"> Django REST Framework documentation</a>
  </p>

  {% highlight bash %}
    pip install djangorestframework
    pip install markdown
    pip install django-filter
  {% endhighlight %}

  <p>
    Now let's open up <code>/desktop/server/myLibrary/myLibrary/settings.py</code> and install the 'books' app into the 'myLibrary' project.
  </p>

  {% highlight python %}
    INSTALLED_APPS = [
    ...
      'rest_framework',
      'books'
    ]
  {% endhighlight %}

  <p>
    To finish things off, let's create a new folder called 'api' within the 'books' app and an empty '__init__.py' file (why, so it knows its a ??) like so: <code>/desktop/server/myLibrary/books/api/__init__.py</code>
  </p>
</section>

<!-- Create Serializer for Books ----->
<section>
  <h4 id="create-serializer">Create Serializer</h4>

  <p>
    Let's create the serializer in <code>/desktop/myLibrary/books/api/serializers.py</code>
  </p>

  <p>
    What does the serializer do?
  </p>

  {% highlight python %}
    from rest_framework import serializers
    from books.models import book

    class bookSerializer(serializers.ModelSerializer):
      class Meta:
        model = book
        fields = (
          'id',
          'title',
          'author',
          'description',
        ) # converts to JSON

  {% endhighlight %}

  <p>
    Let's validate any of the data that may be passed in. Adding on in the same file.
  </p>

  {% highlight python %}
    # validations for data passed
    def validate_title(self, value):
      qs = book.objects.filter(title__iexact=value)
      if self.instance:
          qs = qs.exclude(id=self.instance.id)
      if qs.exists():
        raise serializers.ValidationError("This title has already been used")
      return value
  {% endhighlight %}
</section>

<!-- Create Views for Books ---------->
<section>
  <h4 id="create-views">Create Views for Books</h4>

  <p>
    Let's create the view file in <code>/desktop/myLibrary/books/api/views.py</code>
  </p>

  <!-- Django REST framework: http://www.django-rest-framework.org/api-guide/viewsets/#genericviewset -->

  {% highlight python %}
    from django.db.models import Q
    from rest_framework import generics, mixins
    from items.models import book
    from .serializers import  bookSerializer

    class bookAPIView(mixins.CreateModelMixin, generics.ListAPIView):
      pass
      lookup_field        = 'id'
      serializer_class    = bookSerializer

      def get_queryset(self):
        qs = book.objects.all()
        query = self.request.GET.get('q')
        if query is not None:
          qs = qs.filter(Q(title__icontains=query)|Q(description__icontains=query)).distinct()
        return qs

      def post(self, request, *args, **kwargs):
        return self.create(request, *args, **kwargs)
  {% endhighlight %}

  <p>
    What is this doing?
  </p>

  <p>
    Adding on in the same file.
  </p>

  {% highlight python %}
    class bookRudView(generics.RetrieveUpdateDestroyAPIView): # DetailView
      pass
      lookup_field        = 'id'
      serializer_class    = bookSerializer

      def get_queryset(self):
        return book.objects.all()
  {% endhighlight %}

  <p>
    What is this doing?
  </p>
</section>

<!-- URLs Views for Books ------------>
<section>
  <h4 id="create-urls">Create URLS</h4>

  <p>
    Let's create the view file in <code>/desktop/myLibrary/books/api/urls.py</code>
  </p>

  {% highlight python %}
  {% raw %}
    from .views import bookRudView, bookAPIView

    from django.conf.urls import url

    urlpatterns = [
      url(r'^$', bookAPIView.as_view(), name='book-create'),
      url(r'^(?P<id>\d+)/$', bookRudView.as_view(), name='book-rud')
    ]
  {% endraw %}
  {% endhighlight %}

  <p>
    What is this doing?
  </p>
</section>

<!-- Postman to demonstrate working endpoints ---->
<section>
  <h4 id="access-data">Postman</h4>

  <p>
    Now that we have the base REST framework setup. Let's see the data that the backend is returning to us.
  </p>
</section>

<!-- Conclusion ----------------------------------------------------------- -->
<section>
  <h3 id="conclusion">Conclusion</h3>
  <p>
    We've completed the following steps:
  </p>

  <ul>
    <li>Installed Django REST Framework into our project</li>
    <li>Created a serializer for books</li>
    <li>Created views for books</li>
    <li>Created URLs for books</li>
    <li>Caputuring data sent from the backend</li>
  </ul>

  <p>
    In <a href="#">part four</a> we will start our EmberJS project which will serve as the front-end client.
  </p>
</section>

<!-- ## build REST API w/ Django REST Framework -->
<!-- https://www.youtube.com/watch?v=tG6O8YF91HE -->