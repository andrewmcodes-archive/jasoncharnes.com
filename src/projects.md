---
layout: page
title: Projects
permalink: /projects/
---

{% for project in site.data.projects %}
  {% render "project/card", project: project %}
{% endfor %}
