---
layout: page
title: Dev Log
permalink: /devlog/
---

프로젝트 기반 Dev Log & TIL

{% assign posts = site.categories.devlog | default: empty | sort: "date" | reverse %}

{% if posts.size == 0 %}
아직 글이 없습니다.
{% else %}
{% for post in posts %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url }})
{% endfor %}
{% endif %}
