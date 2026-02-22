---
layout: page
title: Tools
permalink: /tools/
---

{% assign posts = site.posts | where_exp: "p", "p.tags contains 'tools'" | sort: "date" | reverse %}  
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}