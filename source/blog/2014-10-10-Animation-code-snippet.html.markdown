---
title: Animation code snippet
date: '2014-10-10'
category: craft-code
tags:
- animation
- css
- mixin
- sass
status: published
---

Because I keep referring back to it:

<pre><code class=“language-css”>
@include simple-vendor-prefix(animation,
    animation-name(name [default:none])
    animation-duration(Xs | Xms [default:0s])
    animation-timing-function(ease | ease-in | ease-out | ease-in-out | linear | cubic-bezier(x1,y1,x2,y2) | step-start | step-end | steps(X start|end) [default:ease])
    animation-delay(Xs | Xms [default:0s])
    animation-iteration-count(X | infinite [default:1])
    animation-direction(normal | reverse | alternate | alternate-reverse [default:normal])
    animation-fill-mode(none | forwards | backwards | both [default:none])
    animation-play-state(running | paused [default:running])
    )
</code></pre>

This is the <a href="http://sass-lang.com/" rel="external">Sass</a> I use for declaring CSS animations. It's a good list of all the parameters you can get for the CSS <code>animation</code> property, with their parameter format and default value.

READMORE

For this reason I keep referring back to it, just to check things like <i>keywords for timing functions</i>. However if you want to use it in your Sass, firstly you would need the <code>simple-vendor-prefix</code> mixin:

<pre><code class=“language-css”>
@mixin simple-vendor-prefix($name, $argument) {
  -webkit-#{$name}: $argument;
  -ms-#{$name}: $argument;
  -moz-#{$name}: $argument;
  -o-#{$name}: $argument;
  #{$name}: $argument;
}
</code></pre>

You would also need to create your animation with <code>@keyframes</code>:

<pre><code class=“language-css”>
@keyframes fadeIn {
  0% {opacity:0;}
  100% {opacity:1;}
}
</code></pre>

Then you would declare the animation something like:

<pre><code class=“language-css”>
@include simple-vendor-prefix(animation, fadeIn 2s infinite);
</code></pre>

You can include as many or as little of the above listed properties in the second part of the mixin's parameters.



