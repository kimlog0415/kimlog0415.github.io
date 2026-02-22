---
layout: page
title: Dev Log
permalink: /devlog/
---
총 posts: {{ site.devlog | size }}

### Dev Log ― Unreal Engine 5

{% assign posts = site.devlog  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'ue5'"  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'devlog'"  
| sort: "date" | reverse %}  
{% if posts.size == 0 %}  
아직 글이 없습니다.  
{% else %}
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}


### Dev Log ― Tools

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