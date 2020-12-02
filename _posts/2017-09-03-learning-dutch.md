---
layout: single
title: "Learning Dutch"
author: Sina Hazratpour
excerpt: "My way of learning dutch"
tags:
permalink: /posts/2017/09/learning-dutch
date: 2017-09-03
use_math: true
location: "Utrecht, NL"
---




{% include base_path %}
{% capture written_year %}'None'{% endcapture %}
{% for post in site.nl %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year != written_year %}
    <h2 id="{{ year | slugify }}" class="archive__subtitle">{{ year }}</h2>
    {% capture written_year %}{{ year }}{% endcapture %}
  {% endif %}
  {% include archive-single.html %}
{% endfor %}


