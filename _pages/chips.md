---
layout: page
title: chips
permalink: /chips/
description:
nav: true
nav_order: 1
---

<div class="chip-gallery">
  {% for chip in site.data.chips %}
    <a class="chip-card" href="{{ chip.url | relative_url }}" aria-label="Learn more about {{ chip.name }}">
      {% include figure.html path=chip.image title=chip.name alt=chip.tagline class="img-fluid" %}
      <div class="caption">
        <span>{{ chip.tagline }}</span>
        <i class="fa-solid fa-arrow-right chip-card-arrow" aria-hidden="true"></i>
      </div>
    </a>
  {% endfor %}
</div>
