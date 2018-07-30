---
layout: post
title: EmberJS Django - Part One
description: Connect EmberJS with Django
categories: EmberJS JavaScript Django Python Frontend Backend, Fullstack
tags: [EmberJS, JavaScript, Django, Python, Frontend, Backend, Fullstack]
---

<!-- INTRODUCTION ------------------------------------------------------------>

<section>
<div class="row">
  <div class="col col-12 col-md-4">
    <img src="/assets/img/posts/2018/emberjs.png"
         class="img-fluid align-self-center mb-3 mb-md-0">
  </div>

  <div class="col col-12 col-md-8">
    <p>
      Welcome to my three part tutorial connecting a Django backend to a EmberJS front end.
    </p>

    <ul>
      <li>Part 1</li>
      <li>
        <a>
          Part 2
        </a>
      </li>
      <li>
        <a>
          Part 3
        </a>
      </li>
    </ul>
  </div>
</div>
</section>


<!-- Installation ------------------------------------------------------------>

<section>
<h3>Installation & Setup</h3>
<ul>
  <li>
    <a href="https://pip.pypa.io/en/latest/installing/#installing-with-get-pip-py"
       target="_blank">
      Pip
    </a>
  </li>
  <li>
    <a href="https://virtualenv.pypa.io/en/stable/installation/"
       target="_blank">
     virtualenv
    </a>
   </li>
  <li>
    <a href="https://docs.djangoproject.com/en/1.11/topics/install/"
       target="_blank">
      Django
    </a>
  </li>
</ul>


<!-- Pip ---------------------------------------->

<h6>pip</h6>
<p>
  Simply put, pip (Pip Installs Packages) is 'is a package management system used to install and manage software packages written in Python.'. We'll ultimately use pip to install virtualenv, and Django.
</p>

{% highlight bash %}
  curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
  python get-pip.py
  pip —version
{% endhighlight %}


<!-- virtualenv --------------------------------->

<h6>virtualenv</h6>
<p>
  virtualenv 'is a tool to create isolated Python environments... It creates an environment that has its own installation directories, that doesn’t share libraries with other virtualenv environments (and optionally doesn’t access the globally installed libraries either).' You can install, modify and play with python packages and libraries without affecting your global environment.
</p>

<p>Let's install virtualenv and confirm it has been installed:</p>

{% highlight bash %}
  $ [sudo] pip install virtualenv
  virtualenv —version
{% endhighlight %}

<p>Create a virtual environment for our project:</p>

{% highlight bash %}
  $ mkdir ~/.virtualenvs
  $ python3 -m venv ~/.virtualenvs/djangodev
  $ source ~/.virtualenvs/djangodev/bin/activate
  activate with: source bin/activate
{% endhighlight %}

<!-- https://pip.pypa.io/en/latest/installing/#upgrading-pip -->


<!-- Django ------------------------------------------------------------------>

<h6>Django 1.11</h6>
<p>
  Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.
</p>

{% highlight bash %}
  pip install Django
  python3
  import django
  print(django.get_version())
{% endhighlight %}

</section>


<!-- Create Django Project —————————------------------------------------------>

<section>
  django-admin startproject mysite
  cd into /desktop/mysite
  python manage.py runserver ## success @localhost:8000
  cmd+ctrl ## stop server

<!-- // Create new app ----------------------------------------- -->

{% highlight python %}
  python3 manage.py startapp items ## create new 'app' items
  cd into /desktop/mysite/items

  /desktop/mysite/settings.py
{% endhighlight %}

{% highlight python %}
  INSTALLED_APPS = [
    ...
    'items',
    ...
  ]
{% endhighlight %}


<!-- Create model ------------------------------------------------------------>

  create new file /desktop/mysite/items/models.py

{% highlight python %}
  from django.db import models

  class Item(models.Model):
    title       = models.CharField(max_length=500)
    subtitle    = models.CharField(max_length=500, blank=True, null=True)
    author      = models.CharField(max_length=100)
    description = models.TextField()
    cover       = models.CharField(max_length=100, blank=True, null=True)
{% endhighlight %}


<!-- Create views ------------------------------------------------------------>

Is it neccessary to create html views if only using as database?

  create new file /desktop/mysite/items/views.py

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


<!-- Register Admin for Item ------------------------------------------------->

Why do you register the item with the admin?

  create new file /desktop/mysite/items/admin.py

{% highlight python %}
  from django.contrib import admin

  from .models import Item

  @admin.register(Item)
  class ItemAdmin(admin.ModelAdmin):
    list_display = ['title', 'subtitle', 'author', 'description', 'cover']
{% endhighlight %}

<!-- // Configure the Item app -->

  create new file /desktop/mysite/items/apps.py

{% highlight python %}
  from django.apps import AppConfig

  class ItemsConfig(AppConfig):
      name = 'items'
{% endhighlight %}
</section>


<!-- Create API -------------------------------------------------------------->

  ## build REST API w/ Django REST Framework
  https://www.youtube.com/watch?v=tG6O8YF91HE

  create new folder /desktop/mysite/items/api
  create new file /desktop/mysite/items/api/__init__.py

<!-- // Install Django REST Framework ------------------------------------- -->

  Django REST framework: http://www.django-rest-framework.org/api-guide/viewsets/#genericviewset

{% highlight bash %}
  pip install djangorestframework
  pip install markdown
  pip install django-filter
{% endhighlight %}

  /desktop/mysite/settings.py

{% highlight python %}
  INSTALLED_APPS = [
  ...
    'rest_framework',
  ...
    'items',
  ...
  ]
{% endhighlight %}


<!-- Create Serialier for Items ---------------------------------------------->

  create new file /desktop/mysite/items/api/serializers.py

{% highlight python %}
  from rest_framework import serializers
  from items.models import Item

  class ItemSerializer(serializers.ModelSerializer):
    class Meta:
      model = Item
      fields = (
        'id',
        'title',
        'subtitle',
        'author',
        'description',
        'cover',
      ) # converts to JSON

    # validations for data passed
    def validate_title(self, value):
      qs = Item.objects.filter(title__iexact=value)
      if self.instance:
          qs = qs.exclude(id=self.instance.id)
      if qs.exists():
        raise serializers.ValidationError("This title has already been used")
      return value
{% endhighlight %}


<!-- Create Views for Items -------------------------------------------------->

  create new file /desktop/mysite/items/api/views.py

{% highlight python %}
  from django.db.models import Q
  from rest_framework import generics, mixins
  from items.models import Item
  from .serializers import  ItemSerializer

  class ItemAPIView(mixins.CreateModelMixin, generics.ListAPIView):
    pass
    lookup_field        = 'id'
    serializer_class    = ItemSerializer

    def get_queryset(self):
      qs = Item.objects.all()
      query = self.request.GET.get('q')
      if query is not None:
        qs = qs.filter(Q(title__icontains=query)|Q(description__icontains=query)).distinct()
      return qs

    def post(self, request, *args, **kwargs):
      return self.create(request, *args, **kwargs)

  class ItemRudView(generics.RetrieveUpdateDestroyAPIView): # DetailView
    pass
    lookup_field        = 'id'
    serializer_class    = ItemSerializer

    def get_queryset(self):
      return Item.objects.all()
{% endhighlight %}


<!-- URLs Views for Items ---------------------------------------------------->

  create new file /desktop/mysite/items/api/urls.py

{% highlight python %}
  from .views import ItemRudView, ItemAPIView

  from django.conf.urls import url

  urlpatterns = [
    url(r'^$', ItemAPIView.as_view(), name='item-create'),
    url(r'^(?P<id>\d+)/$', ItemRudView.as_view(), name='item-rud')
  ]
{% endhighlight %}

<!-- Create superuser -------------------------------------------------------->
  <!-- // what is the superuser able to do? -->

<!-- Conclusion ----------------------------------------------------------- -->
<!-- Use Postman to demonstrate the end points working to return api data ---->
