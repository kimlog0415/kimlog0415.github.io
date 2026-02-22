---
layout: page
title: Tools
permalink: /tool/
---

{% assign posts = site.categories.tool | sort: "date" | reverse %}
{% for post in posts %}
### [{{ post.title }}]({{ post.url }})
<small>{{ post.date | date: "%Y-%m-%d" }}</small>

---
{% endfor %}
