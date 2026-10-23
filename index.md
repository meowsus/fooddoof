---
layout: page
title: fooddoof
permalink: /
---

The doof cooks. Here's what's on the menu — grab something and go make it.

{% if site.recipes.size > 0 %}
<ul>
  {%- for recipe in site.recipes -%}
  <li><a href="{{ recipe.url | relative_url }}">{{ recipe.title }}</a></li>
  {%- endfor -%}
</ul>
{% else %}
Nothing cooked yet. The doof dreams of its first dish.
{% endif %}