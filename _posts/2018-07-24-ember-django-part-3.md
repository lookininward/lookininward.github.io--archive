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

  ## build REST API w/ Django REST Framework
  https://www.youtube.com/watch?v=tG6O8YF91HE

  create new folder /desktop/mysite/items/api
  create new file /desktop/mysite/items/api/__init__.py
</section>

<!-- Install Django REST Framework --->
<section>
  <h4 id="install-framework">Install Django REST Framework</h4>

  <!-- Django REST framework: http://www.django-rest-framework.org/api-guide/viewsets/#genericviewset -->

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
</section>

<!-- Create Serializer for Items ----->
<section>
  <h4 id="create-serializer">Install Django REST Framework</h4>
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
</section>

<!-- Create Views for Items ---------->
<section>
  <h4 id="create-views">Install Django REST Framework</h4>
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
</section>

<!-- URLs Views for Items ------------>
<section>
  <h4 id="create-urls">Install Django REST Framework</h4>
  create new file /desktop/mysite/items/api/urls.py

  {% highlight python %}
  {% raw %}
    from .views import ItemRudView, ItemAPIView

    from django.conf.urls import url

    urlpatterns = [
      url(r'^$', ItemAPIView.as_view(), name='item-create'),
      url(r'^(?P<id>\d+)/$', ItemRudView.as_view(), name='item-rud')
    ]
  {% endraw %}
  {% endhighlight %}
</section>

<!-- Postman to demonstrate working endpoints ---->
<section>
  <h4 id="access-data">Postman</h4>
</section>

<!-- Conclusion ----------------------------------------------------------- -->
<section>
  <h4 id="conclusion">Conclusion</h4>
</section>

