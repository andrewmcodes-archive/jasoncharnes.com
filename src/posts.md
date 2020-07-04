---
layout: page
title: Posts
permalink: /posts/
---

{% for category in site.categories %}
  {% render "shared/section/header", text: category[0] %}
  {% for post in category[1] %}
    {% render "post/item", post: post %}
  {% endfor %}
{% endfor %}
