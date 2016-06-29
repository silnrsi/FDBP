---
published: true
layout: homepage
weight: 0
title: Font Development Best Practices
---

<ol class="rectangle-list">
  {% assign pageList = site.pages | sort: 'weight' %}
  {% for p in pageList %}
    {% if p.path contains 'en-US' and p.title != page.title %}
      <li>
        <span class="outlevel">
          {{ p.outlevel }}
        </span>
        <a {% if p.url == page.url %}class="active"{% endif %} href="{{site.baseurl}}{{ p.url }}">
          {{ p.title }}
        </a>
      </li>
    {% endif %}
  {% endfor %}
</ol>
