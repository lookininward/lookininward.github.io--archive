---
layout: post
title: EmberJS Django - Part Four
description: Connect EmberJS with Django
categories: EmberJS JavaScript Django Python
tags: [EmberJS, JavaScript, Django, Python]
---

<!-- PART FOUR  --------------------------------------------------------------------------------------------------------------------------------------------->

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
        Welcome to <a>Part 4</a> of my 5 part tutorial '<b>Django and EmberJS Fullstack: Connecting the Backend to the Frontend</b>'.
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
        <li>
          <a href="#">
            Part 5
          </a>
        </li>
      </ul>
    </div>

  </div>
</section>

<!-- Setup NodeJS -------------------->
<section>
  <h4 id="install-node">NodeJS and NPM</h4>

  <!-- // NodeJS ------------------ -->
    Installation File: http://nodejs.org/en/download/

  <!-- // NodeJS with Brew -------- -->
    Install Brew: /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    brew install node

  <!-- Check Versions ------------- -->
    node --version
    npm --version
</section>

<!-- Setup EmberJS ------------------->
<section>
  <h4 id="install-ember">EmberJS</h4>

    npm install -g ember-cli
    npm --version

  <!--
    // Create Project
    // Run server to verify works -- ember s -->


    file client/app/templates/application.hbs

    <div class="container">
      {{outlet}}
    </div>

    file client/app/styles/app.scss

    body {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
    }

    .container {
      display: flex;
      flex-direction: column;
      width: 100%;
      height: 100%
    }
</section>

<!-- Create Books Route -------------->
<section>
  <h4 id="create-biijs-route">Create Books Route</h4>
    ember g route items

    file client/app/router.js

  {% highlight javascript %}
    import EmberRouter from '@ember/routing/router';
    import config from './config/environment';

    const Router = EmberRouter.extend({
      location: config.locationType,
      rootURL: config.rootURL
    });

    Router.map(function() {
      this.route('items', function() {});
    });

    export default Router;
  {% endhighlight %}

    file client/app/routes/items.js

  {% highlight javascript %}
    import Route from '@ember/routing/route';
    import { inject as service } from '@ember/service';

    export default Route.extend({
      store: service(),

      model() {
        return this.get('store').findAll('item');
      }
    });
  {% endhighlight %}

    file client/app/templates/items.hbs

  {% highlight handlebars %}
    {% raw %}
    <div class="items">

      {{#each items as |item|}}

        {{item.title}}
        {{item.description}}

      {{/each}}

    </div>
    {% endraw %}
  {% endhighlight %}
</section>

<!-- Create Book Model --------------->
<section>
  <h4 id="create-book-model">Create Item Model</h4>

  {% highlight javascript %}
    import DS from 'ember-data';

    export default DS.Model.extend({
      title: DS.attr(),
      description: DS.attr()
    });
  {% endhighlight %}
</section>

<!-- Create Application Adapter ------>
<section>
  <h4 id="create-app-adapter">Create Application Adapter</h4>
    /desktop/client/app/adapters/application.js

    Direct Ember Data to host

  {% highlight javascript %}
    import Ember from 'ember';
    import DS from 'ember-data';

    const { computed } = Ember;

    export default DS.JSONAPIAdapter.extend({
      host: computed(function(){
        return 'http://localhost:8000';
      }),

      namespace: 'api'
    });
  {% endhighlight %}
</section>

<!-- Conclusion ---------------------->
<section>
  <h3 id="conclusion">Conclusion</h3>

  <!-- // Demonstrate server works and captures data ---------------------------------
  // Do GET request -->
</section>

