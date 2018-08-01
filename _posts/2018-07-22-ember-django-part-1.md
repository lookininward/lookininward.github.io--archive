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
        Welcome to my three part tutorial '<b>Django and EmberJS Fullstack: Connecting the Backend to the Frontend</b>'. This is written as an introduction to everyone including <b><i>absolute beginners</i></b> so if you don't need the hand holding just push on through to the sections relevant to you. Each part is also kept relatively short and to the point so that no one's head explodes and you have natural points at which you can go back and look at what you've done or saved your state using github, etc.
      </p>

      <ul>
        <li>Part 1</li>
        <li>
          <a href="#" target="_blank">
            Part 2
          </a>
        </li>
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


<!-- BACKEND ----------------------------------------------------------------->

<section>

  <h3>Backend: Install Required Software</h3>

  <p>
    The first step is to install the software required to develop the backend of our application. Let's go ahead and install the following:
  </p>

  <ul>
    <li><a href="#install-pip">Pip</a></li>
    <li><a href="#install-virtualenv">virtualenv</a></li>
    <li><a href="#install-django">Django</a></li>
  </ul>

  <!-- Pip --------------------------->

  <h6 id="install-pip">pip</h6>
  <p>
    Simply put, pip (Pip Installs Packages) is '<em>a package management system used to install and manage software packages written in Python</em>'. Full installation documentation can be found <a href="https://pip.pypa.io/en/latest/installing/#installing-with-get-pip-py" target="_blank">here</a>.
  </p>

  <p>
    Now, open up the terminal:
  </p>

  {% highlight bash %}
    # cd into your desktop directory
    cd ~/desktop

    # download the pip python script
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

    # run the script you downloaded
    python get-pip.py

    # once installation completes, verify that it's installed
    pip —version
  {% endhighlight %}

  <p class="mb-5">
    Now that pip is installed, we'll use pip to install virtualenv, and Django.
  </p>

  <!-- virtualenv -------------------->

  <h6 id="install-virtualenv">virtualenv</h6>
  <p>
    virtualenv '<em>is a tool to create isolated Python environments... It creates an environment that has its own installation directories, that doesn’t share libraries with other virtualenv environments (and optionally doesn’t access the globally installed libraries either)</em>'. You can install, modify and play with python packages and libraries without messing up your global environment. Full installation documentation can be found <a href="https://virtualenv.pypa.io/en/stable/installation/" target="_blank">here</a>.
  </p>

  <p>
    Now, open up the terminal:
  </p>

  {% highlight bash %}
    # we are still in the desktop directory

    # use pip to install virtualenv
    pip install virtualenv

    # once installation completes, verify that it's installed
    virtualenv —version
  {% endhighlight %}

  <p>Now, we can create a virtual environment for our project:</p>

  {% highlight bash %}
    # create a virtualenv folder called 'server' on the desktop
    virtualenv server

    # cd into the 'server' directory
    cd server

    # activate the virtual environment
    source bin/activate
  {% endhighlight %}

  <p class="mb-5">
    Now that we've created a virtual environment called 'server', make sure that the environment is activated before installing, updating packages within the 'server' folder.
  </p>

  <!-- Django ------------------------>

  <!-- updgrade pip -->

  <h6 id="install-django">Django 1.11</h6>
  <p>
    Django is described by it's creators as a '<em>high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel</em>'.
  </p>

   <p>
    Checkout out <a href="https://tutorial.djangogirls.org/en/django/" target="_blank">this DjangoGirls article</a> to learn more about Django and why it's used.
  </p>

  <p>
    Although Django is fully capable of handling both frontend and backend tasks, we will be using Django solely to handle the backend in this project. Full installation documentation can be found <a href="https://docs.djangoproject.com/en/1.11/topics/install/" target="_blank">here</a>.
  </p>

  {% highlight bash %}

    # inside the 'server' directory with virtualenv activated
    pip install Django

    # once installation completes, verify that it's installed
    # open up the python3 shell
    python3

    # access the django library and get the version (should be 1.11)
    import django
    print(django.get_version())
  {% endhighlight %}

</section>


<section>
  <h3>Conclusion</h3>
  <p>
    We've completed the following steps:
  </p>

  <ul>
    <li>Installed the pip package manager</li>
    <li>Used pip to install virtualenv</li>
    <li>Created a virtual environment on the desktop called 'server'</li>
    <li>Activated the 'server' environment and upgraded pip</li>
    <li>Installed Django 1.11 LTS within the 'server' environment</li>
  </ul>

  <p>In part two we will create our Django project.</p>
</section>
