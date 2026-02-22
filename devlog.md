---
layout: page
title: Dev Log
permalink: /devlog/
---
### Dev Log ― Unreal Engine 5

{% assign ue5_devlog = site.devlog  
| where_exp: "p", "p.categories contains 'ue5'"  
| where_exp: "p", "p.categories contains 'devlog'"  
| sort: "date" | reverse %}
{% if posts.size == 0 %}  
아직 글이 없습니다.  
{% else %}
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}


### Dev Log ― Tools

{% assign ue5_devlog = site.devlog  
| where_exp: "p", "p.categories contains 'tools'"  
| where_exp: "p", "p.categories contains 'devlog'"  
| sort: "date" | reverse %}
{% if posts.size == 0 %}  
아직 글이 없습니다.  
{% else %}
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}