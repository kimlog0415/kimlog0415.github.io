---
layout: page
title: Unreal Engine 5
permalink: /ue5/
---

### Projects
{% assign posts = site.posts | where_exp: "p", "p.tags contains 'ue5'" | sort: "date" | reverse %}
{% if posts.size == 0 %}
아직 글이 없습니다.
{% else %}
{% assign projects = posts | map: "project" | uniq | sort %}  
  
{% for proj in projects %}  
#### {{ proj }}  
  
{% assign group = posts | where: "project", proj %}  
{% for post in group %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}  
  
{% endfor %}

### Dev Log
{% assign posts = site.posts  
| where_exp: "p", "p.tags contains 'ue5'"  
| where_exp: "p", "p.tags contains 'devlog'"  
| sort: "date" | reverse %}
{% if posts.size == 0 %}
아직 글이 없습니다.
{% else %}
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}
