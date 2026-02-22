---
layout: page
title: Tools
permalink: /tools/
---
총 posts: {{ site.tools | size }}

### Projects


### Dev Log

{% assign posts = site.devlog  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'tools'"  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'devlog'"  
| sort: "date" | reverse %}  
{% if posts.size == 0 %}  
아직 글이 없습니다.  
{% else %}
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}