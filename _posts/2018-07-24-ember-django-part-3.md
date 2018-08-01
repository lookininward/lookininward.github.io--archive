---
layout: post
title: EmberJS Django - Part Three
description: Connect EmberJS with Django
categories: EmberJS JavaScript Django Python
tags: [EmberJS, JavaScript, Django, Python]
---

// PART 3 ----------------------------------------------------------------------------------------------------------------------------------------------------




// Setup EmberJS ---------------------------------------------------------------------------------------------------------------------------------------------

// Installation ---------------------------------------------------------------

// NodeJS -------------------------------------------------
  Installation File: http://nodejs.org/en/download/

// NodeJS with Brew ---------------------------------------
  Install Brew: /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

  brew install node

Check Versions of Node and NPM

  node --version
  npm --version




// Install EmberJS ------------------------------------------------------------

  npm install -g ember-cli
  npm --version


// Create Project
// Run server to verify works -- ember s


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




// Create Items Route ---------------------------------------------------------

  ember g route items

  file client/app/router.js

```
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
```

  file client/app/routes/items.js

```
  import Route from '@ember/routing/route';
  import { inject as service } from '@ember/service';

  export default Route.extend({
    store: service(),

    model() {
      return this.get('store').findAll('item');
    }
  });
```

  file client/app/templates/items.hbs

```
  <div class="items">

    {{#each items as |item|}}

      {{item.title}}
      {{item.description}}

    {{/each}}

  </div>
```




// Create Item Model ----------------------------------------------------------

```
  import DS from 'ember-data';

  export default DS.Model.extend({
    title: DS.attr(),
    description: DS.attr()
  });
```




// Create Adapter -------------------------------------------------------------

  /desktop/client/app/adapters/application.js

  Direct Ember Data to host

```
  import Ember from 'ember';
  import DS from 'ember-data';

  const { computed } = Ember;

  export default DS.JSONAPIAdapter.extend({
    host: computed(function(){
      return 'http://localhost:8000';
    }),

    namespace: 'api'
  });
```

// Conclusion ------------------------------------------------------------------------------------------------------------------------------------------------

// Demonstrate server works and captures data ---------------------------------
// Do GET request
