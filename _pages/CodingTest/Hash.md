---
title: "해시"
layout: archive
permalink: /CodingTest/Hash
author_profile: true
sidebar:
  nav: "categories"
---

<h1>{{ page.major }} / {{ page.minor }}</h1>

{% assign base = site.categories[page.major] %}
{% if base and base.size > 0 %}
  <ul>
  {% for post in base %}
    {% if post.categories contains page.minor %}
      {%- comment -%}
        {% include archive-single.html type=page.entries_layout %}
      {%- endcomment -%}
    {% endif %}
  {% endfor %}
  </ul>
{% endif %}
