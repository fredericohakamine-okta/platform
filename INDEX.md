---
layout: simple
title: Ice Platform Training
category: page
---

# Ice Platform Training

## Labs

{% for lab in site.pages | sort:number %}
  {% if lab.category == 'lab' %}
  - [{{ lab.number }}: {{lab.title}}]({{ lab.url }})
  {% endif %}
{% endfor %}
