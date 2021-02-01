---
layout: post
title: Responsive Progress Bar
description: Simple and effective reponsive progress bar
categories: CSS JavaScript
tags: [CSS, JavaScript]
---
<section>
<img src="/assets/img/posts/2018/progress-bar.png"
     class="img-fluid align-self-center mb-3 mb-md-0">

<p>
  Simple and effective reponsive progress bar that does the following:
</p>

<ul>
  <li>Has four steps to completion</li>
  <li>Each step has a default, active, and complete state</li>
  <li>Animation for active step, and when progressing to next step</li>
</ul>
</section>

<section>
<h3>HTML</h3>
<p>
  The progress bar uses very basic markup. There is a container <code>progress</code>, a background track <code>progress-track</code>, and steps <code>progress-step</code> with ids corresponding to their position.
</p>

<p>
  Let's also drop in a button to cycle through our steps. On clicking it, the function <code>next()</code> will run, advancing to the next step. We'll write out the function in the <b>JavaScript</b> section.
</p>

{% highlight html %}
  <div class="progress">
    <div class="progress-track"></div>
    <div id="step1" class="progress-step">
      Step One
    </div>
    <div id="step2" class="progress-step">
      Step Two
    </div>
    <div id="step3" class="progress-step">
      Step Three
    </div>
    <div id="step4" class="progress-step">
      Complete
    </div>
  </div>

  <button onClick=next()>Next Step</button>
{% endhighlight %}

</section>

<section>
<h3>CSS</h3>
<p>
  This is where we do the heavy lifting. First, let's define some colours to work with:
</p>

{% highlight scss %}
  $grey:  #777;
  $grey2: #dfe3e4;
  $blue:  #2183dd;
  $green: #009900;
  $white: #fff;
{% endhighlight %}

<p>
  Now we define the <code>.progress</code> class which is the container that holds the progress bar contents together.
</p>

{% highlight scss %}
  .progress {
    position: relative;
    display: flex;
  }
{% endhighlight %}

<p>
  Our progress bar needs a <code>.progress-track</code> that the progress steps will run over. This will be grey, covered over by the coloured bar as it advances to the next step.
</p>

{% highlight scss %}
  .progress-track {
    position: absolute;
    top: 5px;
    width: 100%;
    height: 5px;
    background-color: $grey2;
    z-index: -1;
  }
{% endhighlight %}

<p>
  Each <code>.progress-step</code> contains the round step that will be highlight and filled in as the progress bar advances. It also contains the label text and it's own progress track that will cover over <code>.progress-track</code> as it advances forward.
</p>

{% highlight scss %}
  // Each Step on the Progress Bar
  .progress-step {
    position: relative;
    width: 100%;
    font-size: 12px;
    text-align: center;

    // Hide the final step's progress bar
    &:last-child:after {
      display: none;
    }
  }
{% endhighlight %}

<p>
  Let's continue to nest inside <code>.progress-step</code> and define the step in it's <b>default</b> state.
</p>

{% highlight scss %}
  // Step's circle in default state
  &:before {
    content: "\f00c";
    display: flex;
    margin: 0 auto;
    margin-bottom: 10px;
    width: 10px;
    height: 10px;
    background: $white;
    border: 4px solid $grey2;
    border-radius: 100%;
    color: $white;
  }

  // Step's progress bar in default state
  &:after {
    content: "";
    position: absolute;
    top: 6px;
    left: 50%;
    width: 0%;
    transition: width 1s ease-in;
    height: 5px;
    background: $grey2;
    z-index: -1;
  }
{% endhighlight %}

<p>
  Let's continue to nest inside <code>.progress-step</code> and define the step in it's <b>active</b> state.
</p>

{% highlight scss %}
  // Step's active state
  &.is-active {
    color: $blue;

    &:before {
      border: 4px solid $grey;
      animation: pulse 2s infinite;
    }
  }
{% endhighlight %}

<p>
  Let's continue to nest inside <code>.progress-step</code> and define the step in it's <b>complete</b> state.
</p>

{% highlight scss %}
  // Step's complete state
  &.is-complete {
    color: $green;

    // Step's circle in complete state
    &:before {
      font-family: FontAwesome;
      font-size: 10px;
      color: $white;
      background: $green;
      border: 4px solid transparent;
    }

    // Step's progress bar in complete state
    &:after {
      background: $blue;
      animation: nextStep 1s;
      animation-fill-mode: forwards;
    }
  }
{% endhighlight %}



<p>
  Two simple animations will highlight a step when it is active and grow a step's progress bar on the track as it advances to the next step.
</p>

{% highlight scss %}
  // Pulse animation for Step's circle in active state
  @keyframes pulse {
    0% { box-shadow: 0 0 0 0 rgba(33,131,221, 0.4); }
    70% { box-shadow: 0 0 0 10px rgba(33,131,221, 0); }
    100% { box-shadow: 0 0 0 0 rgba(33,131,221, 0); }
  }
{% endhighlight %}

<img src="/assets/img/posts/2018/progress-pulse.gif"
     class="img-fluid align-self-center mt-3 mb-5">

{% highlight scss %}
  // Progressing to next step animation for Step's progress bar
  @keyframes nextStep {
    0% { width: 0%; }
    100% { width: 100%; }
  }
{% endhighlight %}

<img src="/assets/img/posts/2018/progress-next.gif"
     class="img-fluid align-self-center mt-3 mb-5">
</section>

<section>
  <h3>JavaScript</h3>
<p>
  This is obviously going to greatly differ based on how you end up implementing this, what frameworks, patterns you use, etc. Just doing it quick and dirty in vanilla JS to show it working.
</p>

<p>
  It is bascially just adding and removing the <code>.is-active</code>, and <code>.is-complete</code> classes based on the current step.
</p>

{% highlight javascript %}
  let step = 'step1';

  const step1 = document.getElementById('step1');
  const step2 = document.getElementById('step2');
  const step3 = document.getElementById('step3');
  const step4 = document.getElementById('step4');

  function next() {
    if (step === 'step1') {
      step = 'step2';
      step1.classList.remove("is-active");
      step1.classList.add("is-complete");
      step2.classList.add("is-active");

    } else if (step === 'step2') {
      step = 'step3';
      step2.classList.remove("is-active");
      step2.classList.add("is-complete");
      step3.classList.add("is-active");

    } else if (step === 'step3') {
      step = 'step4d';
      step3.classList.remove("is-active");
      step3.classList.add("is-complete");
      step4.classList.add("is-active");

    } else if (step === 'step4d') {
      step = 'complete';
      step4.classList.remove("is-active");
      step4.classList.add("is-complete");

    } else if (step === 'complete') {
      step = 'step1';
      step4.classList.remove("is-complete");
      step3.classList.remove("is-complete");
      step2.classList.remove("is-complete");
      step1.classList.remove("is-complete");
      step1.classList.add("is-active");
    }
  }
{% endhighlight %}

</section>

<section>
<h3>Conclusion</h3>
<p>
  At the end of it all you have this:
</p>
<img src="/assets/img/posts/2018/progress-bar.gif"
   class="img-fluid align-self-center mt-3 mb-5">

<a href="https://codepen.io/lookininward/pen/dKmGrb"
   target="_blank"
   class="mt-4 align-self-center">
 Check out the CodePen for a live example.
</a>
</section>
