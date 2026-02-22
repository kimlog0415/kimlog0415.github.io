---
layout: page
title: Tools
permalink: /tools/
---
### Projects


### Dev Log ― Tools  
  
{% assign items = site.devlog | sort: "date" | reverse %}  
{% assign count = 0 %}  
  
{% for post in items %}  
{% assign cats = post.categories | join: "," | downcase %}  
{% if cats contains "devlog" and cats contains "tools" %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% assign count = count | plus: 1 %}  
{% endif %}  
{% endfor %}  
  
{% if count == 0 %}  
아직 글이 없습니다.  
{% endif %}