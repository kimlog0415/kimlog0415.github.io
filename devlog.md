---
layout: page
title: Dev Log
permalink: /devlog/
---

{% assign posts = site.posts | where_exp: "p", "p.tags contains 'devlog'" | sort: "date" | reverse %}  
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}
