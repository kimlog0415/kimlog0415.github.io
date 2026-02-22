---
layout: page
title: Unreal Engine 5
permalink: /ue5/
---

{% assign posts = site.categories.ue5 %}

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
