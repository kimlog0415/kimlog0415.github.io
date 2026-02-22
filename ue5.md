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

{% assign ue5_devlog = site.posts
  | where_exp: "p", "p.categories contains 'ue5'"
  | where_exp: "p", "p.categories contains 'devlog'"
  | sort: "date" | reverse %}

{% if ue5_devlog.size > 0 %}
  {% for post in ue5_devlog %}
  - {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})
  {% endfor %}
{% else %}
  아직 글이 없습니다.
{% endif %}