---
layout: post
title: iTerm2, AppleScript, and Jumping Quickly into Your Workflow
description: Take advantage of iTerm2's Apple Script integration to get your development environments up and running in seconds
categories: iTerm AppleScript Workflow
tags: [iTerm, AppleScript, Workflow]
---
<section>
<p>
  What you'll need: <a href="https://www.iterm2.com/" target="_blank">iTerm2</a>, Computer running <a href="https://en.wikipedia.org/wiki/MacOS" target="_blank">macOs</a>
</p>

<p>
  As you pile on local servers and instances, jumping quickly into your workflow can start to be an issue. Volumes need to be mounted, terminal windows organized, servers SSHed into, and startup commands run.
</p>

<p>
  A fully online development environment for me takes 22 different terminal commands from the ground up. This excludes the opening and setup of terminal tabs and panes.
</p>

<p>
  If you are using <strong>iTerm2</strong> as your terminal and running on <strong>macOS</strong>, you can take advantage of <a href="https://www.iterm2.com/documentation-scripting.html" target="_blank">iTerm2's Apple Script integration</a> to set up a script to get your development environments up and running in seconds as opposed to minutes.
</p>
</section>

<section>
<h3>How It's Done</h3>
<ol>
  <li>
    Create a new file called <strong>setup.scpt</strong> on the desktop and open it up in an editor.
  </li>
  <li>
    Create a code block that will tell iTerm2 to run a set of actions for us. <i>Apple Script comments start with <code>--</code></i>
  </li>
</ol>

{% highlight html %}
  tell application "iTerm2"
    -- commands we will issue to the terminal
  end tell
{% endhighlight %}

<p>
  Let's open up a new tab with the default profile.
</p>

{% highlight html %}
  tell current window
    create tab with profile "default"
  end tell
{% endhighlight %}

<ol start="3">
  <li>
    Now, if we open up an iTerm2 terminal, cd into the directory with our script, and run:
  </li>
</ol>

{% highlight html %}
  osascript setup.scpt
{% endhighlight %}

<p>
  We should see this:
</p>

<img src="/assets/img/posts/2018/iterm_2.gif"
     class="img-fluid align-self-center mt-3 mb-5">

<p>
  The rest of the process is similarly straightforward.
</p>

<ol start="4">
  <li>
    We'll set the name of the session pane to <strong>SERVER 1</strong>, SSH into a server from this directory, run some commands in the virtual environment, then split the session pane horizontally and vertically to have more panes in the same tab to run related processes.
  </li>
</ol>

{% highlight html %}
  tell first session of current tab of current window
    set name to "SERVER"
    write text "vagrant ssh"
    write text "cd myDir && source .env && source bin/activate"
    write text "python manage.py runserver 10.0.0.199:8000"
    split horizontally with profile "default"
    split vertically with profile "default"
  end tell
{% endhighlight %}

<ol start="5">
  <li>
    Next, I'll target the second session pane, set its name to <strong>SERVER 2</strong>, run commands, and split the pane vertically.
  </li>
</ol>

{% highlight html %}
  tell second session of current tab of current window
    set name to "SERVER 2"
    write text "vagrant ssh"
    write text "cd myDir && source .env && source bin/activate"
    write text "celery -A app worker -l info -Q celery,slow -E"
    split vertically with profile "devbox"
  end tell
{% endhighlight %}

<p>
  You can run almost any command:
</p>

{% highlight html %}
  tell second session of current tab of current window
    write text "cd anotherDir"
    write text "git branch"
  end tell
{% endhighlight %}

<ol start="6">
  <li>
    With all said and done, we have a script that makes this happen:
  </li>
</ol>

<img src="/assets/img/posts/2018/iterm_3.gif"
     class="img-fluid align-self-center mt-3 mb-5">

<img src="/assets/img/posts/2018/iterm_4.gif"
     class="img-fluid align-self-center mb-5">

<p>
  And it this is what it takes to make that happen:
</p>

{% highlight html %}
  tell application "iTerm2"

   -- TAB 1 - - - - - - - - - - - - - - - - - - - - - - - - - - -
   tell current window
     create tab with profile "default"
   end tell

   -- PANE 1 - SERVER
   tell first session of current tab of current window
     set name to "SERVER"
     split horizontally with profile "default"
     write text "vagrant ssh"
     write text "cd /myDir && source .env && source bin/activate"
     write text "python manage.py runserver 10.0.0.199:8000"
     split vertically with profile "default"
   end tell

   -- PANE 2 - CELERY
   tell second session of current tab of current window
     set name to "SERVER 2"
     write text "vagrant ssh"
     write text "cd /myDir && source .env && source bin/activate"
     write text "cd /myDir && celery -A server worker -l info -Q celery,slow -E"
     split vertically with profile "default"
   end tell

   -- PANE 3 - SERVER 2
   tell third session of current tab of current window
     set name to "SERVER 2"
     write text "vagrant ssh"
     write text "cd /myDir2 && source .env && source bin/activate"
     write text "python manage.py runserver 10.0.0.199:8001"
   end tell

   -- PANE 4 - APP
   tell fourth session of current tab of current window
     set name to "APP"
     write text "cd /myApp && ember s"
     split vertically with profile "devbox"
   end tell

  -- PANE 5 - APP 2
   tell fifth session of current tab of current window
     set name to "APP 2"
     write text "cd /myApp2 && ember s"
   end tell

   -- TAB 2 - - - - - - - - - - - - - - - - - - - - - - - - - - -
   tell current window
     create tab with profile "default"
   end tell

   -- PANE 1 - APP 3
   tell first session of current tab of current window
     set name to "APP 3"
     write text "cd /myApp3 && git branch"
     split horizontally with profile "default"
   end tell

   -- PANE 2 - APP 4
   tell second session of current tab of current window
     set name to "APP 4"
     write text "cd /myApp4 && git branch"
   end tell

  end tell
{% endhighlight %}

<p>
  Any set of consistent actions is ripe for automation. Saves a lot of frustration in the morning and let's me jump right into work without wasting time with setup. Hope you find this article useful and use it to customize and automate your own workflow startup processes.
</p>

<p>
  <strong>NOTE</strong>: If you have processes that require password input you may have to add exceptions to <code>/etc/sudoers</code>
</p>

<a href="https://askubuntu.com/questions/412525/vagrant-up-and-annoying-nfs-password-asking"
   class="align-self-center"
   target="_blank">
  This is an example to deal with Vagrant, but can be repurposed to your needs.
</a>
</section>
