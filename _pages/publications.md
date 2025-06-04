---
layout: archive
title: "Research"
permalink: /publications/
author_profile: true
---

{% include base_path %}

<h2 id="wip"><font color="#002d72">Work in Progress 🛠️ <i class="fa fa-exclamation-triangle" aria-hidden="true" style="color:#FFA500;" title="Work in progress"></i> 
<i class="fa fa-wrench" style="color:white; font-size: 0.6em; margin-top: 0.2em;"></i>
</font></h2>

<p> with Peter Lumsdaine <br/> 
<strong> Gödel's Incompleteness Theorems in Lean 4 </strong> <br/>
A Lean blueprint for Gödel's incompleteness theorems and its categorification in Arithmetic Universes <br>
<!-- <a href="https://sinhp.github.io/au/"><code>Lean blueprint</code></a> &nbsp;  -->
<a href="https://github.com/sinhp/au"><code>Code</code></a></p>


<h2 id="pub"><font color="#002d72">Selected Publications</font></h2>

{% if site.author.googlescholar %}
  <div class="wordwrap">You can find the full list of my articles on <a href="{{site.author.googlescholar}}"><font color="#800020">my Google Scholar profile</font></a>.</div>
{% endif %}


{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
