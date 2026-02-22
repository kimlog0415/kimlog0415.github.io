---
layout: page
title: Dev Log
permalink: /devlog/
---

{% assign posts = site.categories.devlog %}

{% if posts %}
  {% assign posts = posts | sort: "date" | reverse %}
{% else %}
  {% assign posts = "" | split: "" %}  {# 빈 배열 만들기 #}
{% endif %}
{% if posts.size == 0 %}
아직 글이 없습니다.
{% else %}
{% for post in posts %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url }})
{% endfor %}
{% endif %}
