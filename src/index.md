---
layout: home
---

{% rendercontent "shared/section" %}
  {% rendercontent "shared/container" %}
    {% render "site/hero" %}
  {% endrendercontent %}
{% endrendercontent %}

{% rendercontent "shared/section", bg_color: "bg-gray-100" %}
  {% rendercontent "shared/container", direction: "column" %}
    {% render "shared/section/header", text: "Writings"  %}
    {% for post in site.posts limit:3 %}
      {% render "post/item", post: post %}
    {% endfor%}
    <p class="pt-2 text-lg">
      <a class="font-bold text-red-600 no-underline hover:text-red-800" href="/articles">See More</a>
    </p>
  {% endrendercontent %}
{% endrendercontent %}
