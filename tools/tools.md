---
layout: page
title: Tools
permalink: /tool/
---

[PDF Editor](./pdf-editor/index.html)

{% assign posts = site.categories.tool %}

{% if posts %}
  {% assign posts = posts | sort: "date" | reverse %}
{% else %}
  {% assign posts = "" | split: "" %}
{% endif %}
{% if posts.size == 0 %}
아직 글이 없습니다.
{% else %}
{% for post in posts %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url }})
{% endfor %}
{% endif %}
