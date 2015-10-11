---
title: Chaining CSS :not()
date: '2015-01-19'
category: craft-code
tags:
status: published
---

I found myself using the CSS psuedo class <code>:not()</code> the other day. It proved superbly useful. For those that are unaware, by adding it to your CSS, you can choose <b>not</b> to affect a set of elements.

<pre class="language-css"><code>myelement:not(.ofthisclass) { style: property; }</code></pre>

There's a couple of good resources about it in the <a href="http://css-tricks.com/almanac/selectors/n/not/">CSS Tricks Almanac</a> or the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/:not">MDN docs</a>.

What I was looking for was a way to affect anything but a certain class, plus another certain class. If I had declared both separately in my CSS, the first declared would have been overwritten. In this example the div with a class of blue would still have a crimson background, as the declaration below it would overwrite it.

<pre class="language-css"><code>div:not(.blue) {
  background: crimson;
}
div:not(.green) {
  background: crimson;
}</code></pre>

But wait... there is a way. All we need to do is chain the two <i>nots</i> together:

<pre class="language-css"><code>div:not(.blue):not(.green) {
  background: crimson;
}</code></pre>

Voilà! Just what I was looking for. For a demo, <a href="http://codepen.io/Rumyra/pen/dPWOOL">check out this codepen</a>.

