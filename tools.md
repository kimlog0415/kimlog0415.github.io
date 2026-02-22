---
layout: page
title: Tools
permalink: /tool/
---

[PDF Editor](./_tools/pdf-editor/index.html)

{% assign posts = site.tool | sort: "date" | reverse %}

{% if posts.size == 0 %}
아직 글이 없습니다.
{% else %}
{% for post in posts %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url }})
{% endfor %}
{% endif %}
