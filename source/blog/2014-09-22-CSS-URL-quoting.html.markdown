---
title: CSS URL quoting
date: '2014-09-22'
tags: brain-dribble
category: brain-dribble
status: draft
---

I usually put single quotes around my url's in CSS. Not only does this give back up for any unusual characters in said url strings, but most text editors and IDE's highlight quoted strings in a different colour.

I'm currently correcting my image paths for a build, and it's super easy to scan through my fragmented sass files and just pick out where all my background image url's are.

Even the lovely Lea Verou has included string highlighting in her Prism plugin, which I am using for code on this site:

<pre><code class=“language-css”>
/* Still playing Old Skool */
.my-element {
    background:transparent url('/images/imageName.jpg') no-repeat top left;
}
</code></pre>
