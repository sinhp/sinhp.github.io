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

<p> with Michail Karatarakis <br/> 
<strong> A Lean4 mechanization of GNNs in Monoidal Locuses</strong>  <br/>

<p> with Peter Lumsdaine <br/> 
<strong> Mechanization of Essentially Algebraic Theories in Arithmetic Universes (Rocq and Lean 4) </strong> <br/>
See [Peter's talk](https://progetto-itaca.github.io/fests/fest25.html#lumsdaine) at Itaca Fest 2025<br>
<!-- <a href="https://sinhp.github.io/au/"><code>Lean blueprint</code></a> &nbsp;  -->
<!-- <a href="https://github.com/sinhp/au"><code>Code</code></a></p> -->


<h2 id="pub"><font color="#002d72">Selected Publications</font></h2>

{% if site.author.googlescholar %}
  <div class="wordwrap">You can find the full list of my articles on <a href="{{site.author.googlescholar}}"><font color="#800020">my Google Scholar profile</font></a>.</div>
{% endif %}


{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
