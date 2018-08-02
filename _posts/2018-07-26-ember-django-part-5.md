---
layout: post
title: EmberJS Django - Part Five
description: Connect EmberJS with Django
categories: EmberJS JavaScript Django Python
tags: [EmberJS, JavaScript, Django, Python]
---

<!-- PART FIVE  --------------------------------------------------------------------------------------------------------------------------------------------->

<section>
  // Django
    Django REST framework JSON API: https://github.com/django-json-api/django-rest-framework-json-api

  // Cleanup

  // Item Component
  ```
    {{lb-item
      item=item
    }}
  ```

  // Items Route Template
  ```
    <div class="items">
      {{#each items as |item|}}
        {{lb-item
          item=item
        }}
      {{/each}}

    </div>
  ```

  // Item Detail Route
  // Item Detail view

  // JSONAPI Adapter
    https://www.emberjs.com/api/ember-data/release/classes/DS.JSONAPIAdapter

  // Conclusion PART 3 -----------------------------------------------------------------------------------------------------------------------------------------

  // Show that get request works and the data being return is corrently formatted and Ember is able to display it properly without areas
</section>

