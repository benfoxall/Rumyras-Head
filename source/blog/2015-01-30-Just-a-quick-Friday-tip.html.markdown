---
title: Just a quick Friday tip
date: '2015-01-30'
tags:
- article
- comment
- containing-element
- div
- section
category: craft-code
status: published
---

I know a lot of you out there are already aware of this and to you it will seem obvious, however, I've found myself giving this tip a few times over the past couple of weeks, so think it's worth quickly noting.

If you have a containing element, (div, article, section etc...), with a lot of content inside, reference which one it is at the closing tag. E.g:

<pre class="language-markup"><code>&lt;section role="main">

  &lt;!-- ALL the page's content here -->

&lt;/section>&lt;!-- this is the end of section[role="main"] -->
</code></pre>

This is particularly helpful if you have your HTML file split into partials. You may close a container in a different file to that which it starts.
