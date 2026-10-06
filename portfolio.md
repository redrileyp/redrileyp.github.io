---
layout: default
title: "Art Gallery"
permalink: /portfolio/
---

<h1>My Portfolio</h1>

<div class="art-grid" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 20px;">
  {% for artwork in site.portfolio %}
    <div class="art-item">
      <a href="{{ artwork.url }}">
        <img src="{{ artwork.image }}" alt="{{ artwork.title }}" style="width: 100%; height: auto; object-fit: cover;">
        <h3>{{ artwork.title }}</h3>
      </a>
      <p><em>{{ artwork.medium }} ({{ artwork.year }})</em></p>
    </div>
  {% endfor %}
</div>
