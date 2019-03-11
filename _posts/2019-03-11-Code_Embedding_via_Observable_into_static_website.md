---
layout: post
title:  "Code Embedding via Observable into static website"
date:   2019-03-11 20:00
categories: diary science
comments: true
---
## Welcome Note

First of all, welcome to my first official blog post. Today, I will talk a little bit about topics related to my daily work in sofware development, which is highly related to client side development using web technologies as JavaScript. I hope you enjoy reading about my newest findings in this client side programming.

## Observable

First of all I want to introduce you to the next tool of professional software developer Mike Bostock, founder of data-driven documents (d3), which is called Observable. This tool empowers notbooks running in browser environments (comparable to jupyter notebooks in python, but in this specific case using JavaScript directly executed on the client side).
Everybody can freely sign up [here][observable] and make use of a huge toolbox for software development in JavaScript.

Probably the most interesting part about Observable is its ability to import and export modularised JavaScript classes and functionality. Therefore, this post is meant to show you how to embed functionality from Observable as responsive notebooks with some visualizations even in static blogs like this. Further reading about how to embed functionality from Observable can be found [here][embedding].

## Code Embeddings
Let's give it a trial. First we import the important elements to our blog post by simply adding a script tag as a JavaScript module:
```html
<script type="module">
  // Load the Observable runtime and inspector.
  import {Runtime, Inspector} from "https://unpkg.com/@observablehq/notebook-runtime?module";

  // Your notebook, compiled as an ES module.
  import notebook from "https://api.observablehq.com/@mircopp/embedding-test-notebook.js";

  // Load the notebook, observing its cells with a default Inspector
  // that simply renders the value of each cell into the provided DOM node.
  Runtime.load(notebook, Inspector.into(document.querySelector('#notebook')));
</script>
```
<div id="notebook"></div>
<script type="module">
  // Load the Observable runtime and inspector.
  import {Runtime, Inspector} from "https://unpkg.com/@observablehq/notebook-runtime?module";

  // Your notebook, compiled as an ES module.
  import notebook from "https://api.observablehq.com/@mircopp/embedding-test-notebook.js";

  // Load the notebook, observing its cells with a default Inspector
  // that simply renders the value of each cell into the provided DOM node.
  Runtime.load(notebook, Inspector.into(document.querySelector('#notebook')));
</script>
    
As we can see it is possible to import the visualization created directly on observable as a executable visualization to this blog. As we can see in the import statement the whole runtime environment is loaded and makes the magic on executing the code at a remote place.
 
This has some very interesting implications for component based architectures in JavaScript e.g. one can write code for some visualization and data analytics loosely coupled within two separated notebooks and connect them by using a third one etc.

I hope I was able to capture huge the potential of such code embeddings on the client side with this short but interactive post and also hope you enjoyed reading this first (small) insight into my daily work.  

[observable]:       https://observablehq.com/
[embedding]:        https://observablehq.com/@observablehq/downloading-and-embedding-notebooks
