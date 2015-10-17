---
title: code xample
date: '2014-03-06'
tags: brain-dribble
category: brain-dribble
status: draft
---

<pre class="language-ruby"><code>def ask_yoda(question)
  yoda_array = ['do', 'do not']
  message = yoda_array.join(' or ') + ' there is no ' + question
  return message unless yoda_array.include?(question)
  'you are strong with the force'
end</code></pre>
