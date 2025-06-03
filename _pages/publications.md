---
layout: archive
title: "Selected Publications"
permalink: /publications/
author_profile: true
---

{% if site.author.googlescholar %}
  <div class="wordwrap">You can find the full list of my articles on <a href="{{site.author.googlescholar}}"><font color="#800020">my Google Scholar profile</font></a>.</div>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
