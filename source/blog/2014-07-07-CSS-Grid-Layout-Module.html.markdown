---
title: CSS Grid Layout Module
date: '2014-07-07'
category: craft-code
tags:
- code
- css
- grid
- craft-code
status: published
---

So I had a chance recently to play around with the <a href="http://www.w3.org/TR/css-grid-1/">CSS Grid Layout Module</a>. It has up until recently only been supported by IE (I know, don't worry I felt a bit weird typing that). I personally don't have a very accessible way to develop in IE, so was pleased to discover it is now supported by Chrome if you enabled the 'Experimental Web Platform' flag.

The best resource for using it in Chrome is <a href="http://www.rachelandrew.co.uk/archives/2014/06/27/css-grid-layout-getting-to-grips-with-the-chrome-implementation/">Rachel Andrews' post here</a> (Thanks <a href="https://twitter.com/justinavery">@justinavery</a>). She did write <a href="http://24ways.org/2012/css3-grid-layout/">another great one for 24 Ways</a>, however as it was only supported by IE at the time, it uses IE syntax which is slightly different to the syntax Chrome uses and thus confused me to start with. Similarly with the <a href="http://css-tricks.com/almanac/properties/g/grid/">CSS Tricks post here</a>, which is also good, but if you are using Chrome can be confusing.

## Some things to share

I discovered I don't need vendor prefixes, I was originally using `-webkit-`, once I removed this I had that 'Yes' moment when I refreshed my page.

READMORE

The initial setting up of your grid seemed pretty straight forward. Declare your display type to be grid on the container and then specify your columns and rows via their sizes (Rachel's article above explains this much better than me :) ).

<pre class="css">
.container {
  display: grid;
  grid-template-columns:200px 200px 200px 200px 200px 200px 200px 200px;/*8 columns*/
  grid-template-rows:200px 200px 200px 200px;/*4 rows*/
}</pre>

<p>You can of course use the shorthand syntax here (as it's explained in other posts so I originally didn't mention it here, thanks for the nudge <a href="https://twitter.com/stopsatgreen">@stopsatgreen</a>).

<pre><code class="language-css">
.container {
  display: grid;
  grid-template-columns:repeat(8, 200px);/*repeats 8 200px columns*/
  grid-template-rows:repeat(4, 200px);/*repeats 4 200px rows*/
}</code></pre>

<p>The design I was working with is laid out like a simplified periodic table, with images in specific cells. I wanted to mark it up so I could change the position of these images easily and play around with the design. It would have also been a bonus to make it easy for anyone else who came to look at the code do the same thing.</p>
<p>I had 4 rows and 8 columns worth of cells. To start I positioned each of the images into their appropriate cells by using the <code>grid-row</code> and <code>grid-column</code> properties:</p>

<pre><code class="language-css">
img:nth-of-type(1) {
  grid-row:1;
  grid-column:1;
}</code></pre>

<p>Then I thought it maybe easier to specify names for my grid cells. I like the idea of letters across for each of my columns and numbers for each of my rows. To do this I needed to specify them on the containing element. I realised quite quickly numerical characters didn't work.</p>

<p>When you declare the name of the cell on the element with <code>grid-area</code> this is actually shorthand for <code>grid-row-start</code> <code>grid-column-start</code> <code>grid-row-end</code> &amp; <code>grid-column-end</code> and if you use a numerical character you would need to declare it with quotes:</p>

<pre class="language-css"><code>
img:nth-of-type(1) {
  grid-area:'1A';
}</code></pre>

<p>Thus rendering Chrome to think you're only declaring <code>grid-column-start</code>. You could of course do something like this:</p>

<pre class="language-css"><code>
img:nth-of-type(1) {
  grid-area:'1A'/'1A'/'1A'/'1A';
}</code></pre>

<p>N.B. My initial thoughts were this may just be a Chrome implementation quirk, something confirmed by a tweet from <a href="https://twitter.com/tabatkins">@tabatkins</a>. I will keep my eye on it and update here if it changes. Another thing to mention is <a href="https://twitter.com/tabatkins/status/486265776874078209">strings are not in the syntax anymore</a>.

<p>But by this point I may as well have just stuck with <code>grid-row</code> and <code>grid-column</code>. (Again check our Rachel Andrews article as she recommends naming lines not cells).</p>

<p>I settled on trying this out:</p>

<pre class="language-css"><code>
.container {
  grid-template-areas:&quot;oneA oneB oneC oneD oneE oneF oneG oneH&quot;
  &quot;twoA twoB twoC twoD twoE twoF twoG twoH&quot;
  &quot;threeA threeB threeC threeD threeE threeF threeG threeH&quot;
  &quot;fourA fourB fourC fourD fourE fourF fourG fourH&quot;
}

img:nth-of-type(1) {
  grid-area:oneA;
}</code></pre>

<p>You need to specify a name (string) or '.' (which signifies put nothing in here) for every cell you've declared with sizing. Leaving one or more out will cause things not to render properly. (Probably worth noting this 'put nothing here' space can be taken up with overlapping content - another feature of grid layouts which I'm not going to go into here.)</p>
<h2>So…</h2><p>I haven't tried this naming method out with my devs yet, I may refer back to <code>grid-row</code> and <code>grid-column</code>. The naming has become more of a chance to get to know Grid Layout, it'll be interesting to see what my colleagues prefer.</p>
<p>I wonder if my use case is an edge case and actually most peeps will start using grid layout for their main page structure and grid systems. Something about the way I've used it wants me to have default values for cells tho. For some reason I like the idea of '1A' or '5G'… I could of course be the only one.</p>
<p>One last thing is: I am glad I chose the Grid Layout for this specific design, (I'll post it when it's ready for release), as I do think it works perfectly for what I needed it for. It was a more precise layout than something I would choose Flexbox for. I am also very interested to see how others implement Grid Layout. <a href="https://twitter.com/Rumyra">Tweet me</a> if you have a chance to use it :).

