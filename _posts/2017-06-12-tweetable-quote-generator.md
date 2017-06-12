---
layout: post
title:  Tweetable Quote Generator
description: A tweetable quote generator that cycles through quotes and makes them shareable on twitter
categories: javascript 
tags: [javascript]
---


<p>Here is a quote generator that cycles through an array of quotes and outputs them onto the DOM. Every time the "Next Quote" button is clicked the DOM will update with the new quote, its author, and source. The tweet button's href attribute will also be updated so that when clicked, it will open up a twitter share window with a tweet pre-populated with the quote and author, ready to be tweeted. I will use the minimum amount of markup to get the point across.</p>

<section>
<h3>The Structure in HTML</h3>
<p>First let's write the HTML. A div with the class "quote-generator" encapsulates two inner divs, "quote" and "menu". "quote" will house the quote, author name, and source, while "menu" will contain the "Next Quote" and tweet buttons.</p>

{% highlight html %}
{% raw %}
<div class="quote-generator">

  <div class="quote">
    <p id="quote"></p>
     <span id="author"></span>,
     <span id="source"></span>
  </div>

  <div class="menu">
    <a id="shareQuote">
      <img src="https://cdn1.iconfinder.com/data/icons/logotypes/32/twitter-128.png">
    </a><script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
    <button id="button" type="button">Next Quote</button>
  </div>

</div>
{% endraw %}{% endhighlight %}
</section>
<section>
<h3>Write the Logic in JavaScript</h3>
<p>The logic and quote data are contained in the script. The 'data' variable contains the quotes, and associated author and source data.</p>

{% highlight html %}
{% raw %}
// Quote Data
var data = {
  quotes: [{
    id: 1,
    "author": "Shakespeare",
    "source": "Julius Caesar",
    "quote": "Cowards die many times before their deaths. The valiant never taste of death but once."
  },{
    id: 2,
    "author": "Steinbeck",
    "source": "East of Eden",
    "quote": "And this I believe: that the free, exploring mind of the individual human is the most valuable thing in the world."
  },{
    id: 3,
    "author": "Vonnegut",
    "source": "Galápagos",
    "quote": "..you are descended from a long line of determined, resourceful, microscopic tadpoles-- champions every one."
  }]
};
{% endraw %}{% endhighlight %}

<p>Each of the Ids in the HTML are located and held in their corresponding variables, along with the 'myIndex' variable which initializes a starting point for the array.</p>

{% highlight html %}
{% raw %}
	var myIndex = 0;
	var author = document.getElementById('author');
	var source = document.getElementById('source');
	var quote = document.getElementById('quote');
{% endraw %}{% endhighlight %}

<p>The first quote in the array will be visible upon page load.</p>
{% highlight html %}
{% raw %}
	//Print first value of array right away.
	author.innerHTML = data.quotes[myIndex].author;
	source.innerHTML = data.quotes[myIndex].source;
	quote.innerHTML = data.quotes[myIndex].quote;
{% endraw %}{% endhighlight %}

<p>Now we create a function called "updateTweetURL" which generates a prepopulated tweet containing the current quote and author. It is immediately called so that the 'href' attribute for the initial quote is constructed immediately.</p>

{% highlight html %}
{% raw %}
//Generate Tweet with Quote Contents
  function updateTweetURL() {
    var shareQuote = document.getElementById('shareQuote');
    shareQuote.href = 'https://twitter.com/intent/tweet?text=' + data.quotes[myIndex].quote + ' - ' + data.quotes[myIndex].author ;
  }
  updateTweetURL();
{% endraw %}{% endhighlight %}

<p>Next, we'll add an event listener to the 'Next Quote' button that runs a function 'nextElement' everytime its clicked. The 'nextElement' function increments the 'myIndex' variable each time it is clicked, thereby looping through the array of quotes one by one. As it loops through, it runs the 'updateTweetURL' function to ensure that each time a new quote is loaded, the tweet button has an 'href' that corresponds to the quote data. The HTML inside target elements for author, source, and quote are also updated according the the current index.</p>

{% highlight html %}
{% raw %}
// Action when 'Next Quote' is clicked
document.getElementById('button').addEventListener("click", function() {

  //Load next Quote
  function nextElement() {
    myIndex = (myIndex+1)%(data.quotes.length);
    updateTweetURL();
    author.innerHTML = data.quotes[myIndex].author;
    source.innerHTML = data.quotes[myIndex].source;
    quote.innerHTML = data.quotes[myIndex].quote;
  };
  nextElement();
});
{% endraw %}{% endhighlight %}
</section>
<section>
<h3>Some CSS to give it legibility</h3>
<p>Now, let's add some simple css to give the outputted content some legibility.</p>

{% highlight html %}
{% raw %}
.quote-generator {
  margin: 2em;
  padding: 3em;
  max-width: 460px;
  background-color: #F7F5F7;
}
.quote-generator img {
  max-width: 30px;
}
.quote-generator .menu {
  padding: 1em 0 1em 0;
}
{% endraw %}{% endhighlight %}

<p>That's it. Every time the 'Next Quote' button is clicked, it should load the next quote in the 'data' array and generate the corresponding twitter url so that when the tweet button is clicked it opens up a twitter window prepopulated with the quote and author information, ready to be tweeted.</p>

<a href="https://codepen.io/lookininward/pen/yXJeRr" target="_blank">Check out the CodePen</a>
</section>









































