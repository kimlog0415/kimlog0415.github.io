---
layout: page
title: Dev Log
permalink: /devlog/
---

프로젝트 기반 Dev Log & TIL

{% assign posts = site.categories.devlog | sort: "date" | reverse %} {% for post in posts %}

[{{ post.title }}]({{ post.url }})
{{ post.date | date: "%Y-%m-%d" }}

{% endfor %}
