---
layout: page
title: Dev Log
permalink: /devlog/
---

{% assign posts = site.devlog | sort: "date" | reverse %}

{% for post in posts %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url }})
{% endfor %}
