---
title: Compressing images
date: '2015-05-12'
category: craft-code
tags:
- image
- image-compression
- middleman
- wordpress
status: published
---

I'm currently doing a <a href="https://wordpress.org/">Wordpress</a> -> <a href="https://middlemanapp.com/">Middleman</a> shuffle for our team blog at work. This came from a review of all our infrastructure and where we could do some cost cutting. We decided to decommission the Wordpress site, as the content was primarily flat, (just blog posts), and we could host that for free on <a href="https://pages.github.com/">Github pages</a>.

Most of the build was pretty straight forward. As a quick run down I chose to use middleman as I was already familiar with it, I added the <a href="https://github.com/middleman/middleman-blog">middleman-blog</a> and <a href="https://github.com/middleman-contrib/middleman-deploy">middleman-deploy</a> gems to make my life easier and translated all the posts to markdown using the <a href="https://github.com/mdb/wp2middleman">wp2middleman command line tool</a>. There are plenty of good tutorials out there that run you through this.

When it came to transferring over the media it became important to me to keep the size of the images down to a minimum. Page weights are getting heavier these days (imo) unnecessarily. So when asking in the wonderful <a href="">Front End London Slack</a> about what I could use for batch image compression I received the following responses:

READMORE
<ul>
<li><a href="https://imageoptim.com/">ImageOptim (Software/GUI)</a></li>
<li><a href="https://github.com/JamieMason/ImageOptim-CLI">ImageOptim CLI</a></li>
<li><a href="http://www.jpegmini.com/">JPEGmini</a></li>
<li><a href="http://pngmini.com/">ImageAlpha</a></li>
</ul>

Thanks to <a href="https://twitter.com/patrickhamann">Patrick</a>, <a href="https://twitter.com/philhawksworth">Phil</a>, <a href="https://twitter.com/ianfeather">Ian</a>, <a href="https://twitter.com/danielknell">Dan</a> and <a href="https://twitter.com/arranrp">Arran</a>.

Then the lovely <a href="https://twitter.com/charlotteis">Charlotte</a> said:

<blockquote>@rumyra: I recently took a day at work and investigated all the available tools out there. ImageOptim CLI is your best bet as it uses both lossy and lossless compression, actually works and is free. The CLI uses more tools than just imageoptim, so all the bases are covered. The repo has some ace stats too</blockquote>

Sums it up nicely - I'm sold!
