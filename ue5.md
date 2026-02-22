---
layout: page
title: Unreal Engine 5
permalink: /ue5/
---

### Projects
{% assign posts = site.posts | where_exp: "p", "p.categories contains 'ue5'" | sort: "date" | reverse %}  
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
| where_exp: "p", "p.categories contains 'ue5'"  
| where_exp: "p", "p.categories contains 'devlog'"  
| sort: "date" | reverse %}  
  
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}
