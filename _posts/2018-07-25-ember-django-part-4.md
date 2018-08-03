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

  <p>
    There are a few ways to install NodeJS and NPM onto your machine. Let's stick with the most straightforward by downloading the <a href="http://nodejs.org/en/download/" target="_blank"> installation file from the official site</a>.
  </p>

  <p>
    Once installation is complete check that everything is installed:
  </p>

  {% highlight bash %}
    node --version
    npm --version
  {% endhighlight %}
</section>

<!-- Setup EmberJS ------------------->
<section>
  <h4 id="install-ember">EmberJS</h4>

  <p>
    Now that we have NPM installed, we can use it to install the Ember CLI:
  </p>

  {% highlight bash %}
    npm install -g ember-cli
    ember-cli --version
  {% endhighlight %}

  <p>
    Let's run the server using <code>ember s</code> and verify that it's working @localhost:4200.
  </p>

  ## Screenshot of Ember start screen
</section>

<!-- Setup DOM ----------------------->
<section>
  <h4 id="setup-dom">Setup DOM</h4>

  <p>
    Locate the file <code>client/app/templates/application.hbs</code>.
  </p>

  {% highlight handlebars %}
  {% raw %}

    <div class="container">
      {{outlet}}
    </div>
  {% endraw %}
  {% endhighlight %}

  <p>
    Locate the file <code>client/app/styles/app.scss</code>.
  </p>

  {% highlight scss %}
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
  {% endhighlight %}
</section>

<!-- Create Book Model --------------->
<section>
  <h4 id="create-book-model">Create Book Model</h4>

  <p>
    Let's generate a model of the books data for Ember Data: <code>ember g model book</code>.
  </p>

  {% highlight javascript %}
    import DS from 'ember-data';

    export default DS.Model.extend({
      title: DS.attr(),
      description: DS.attr()
    });
  {% endhighlight %}
</section>

<!-- Create Books Route -------------->
<section>
  <h4 id="create-books-route">Create Books Route</h4>

  <p>
    Let's generate a new route that will display all of the books in our database: <code>ember g route books</code>.
  </p>

  <p>
    The router file <code>client/app/router.js</code> will now be update with:
  </p>

  {% highlight javascript %}
    import EmberRouter from '@ember/routing/router';
    import config from './config/environment';

    const Router = EmberRouter.extend({
      location: config.locationType,
      rootURL: config.rootURL
    });

    Router.map(function() {
      this.route('books', function() {});
    });

    export default Router;
  {% endhighlight %}

  <p>
    Let's edit the books route <code>client/app/routes/books.js</code> to load all books from the database.
  </p>

  {% highlight javascript %}
    import Route from '@ember/routing/route';
    import { inject as service } from '@ember/service';

    export default Route.extend({
      store: service(),

      model() {
        return this.get('store').findAll('book');
      }
    });
  {% endhighlight %}

  <p>
    Let's edit the books route template <code>client/app/templates/books.hbs</code> display the books that are returned in the model.
  </p>

  {% highlight handlebars %}
    {% raw %}
    <div class="books">

      {{#each books as |book|}}

        {{book.title}}
        {{book.description}}

      {{/each}}

    </div>
    {% endraw %}
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

  <p>
    Show how the API data isn't correctly structured
  </p>
</section>

<!-- Conclusion ---------------------->
<section>
  <h3 id="conclusion">Conclusion</h3>

  <p>
    We've completed the following steps:
  </p>

  <ul>
    <li>Installed NodeJS and NPM</li>
    <li>Installed the Ember CLI and created a new client project</li>
    <li>Basic DOM setup</li>
    <li>Created a Books route and template to load and display books from our database</li>
    <li>Created an application adapter to capture JSON data coming from our Django backend</li>
  </ul>

  <p>
    In <a href="#">part five</a> we will go back to Django and structure the data in a way that is amenable to Ember Data's uses.
  </p>
</section>

<!-- https://www.emberjs.com/api/ember-data/release/classes/DS.JSONAPIAdapter -->