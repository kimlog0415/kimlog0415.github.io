---
layout: page
title: Tools
permalink: /tools/
---
### Tools
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
| where_exp: "p", "p.categories contains 'tools'"  
| where_exp: "p", "p.categories contains 'devlog'"  
| sort: "date" | reverse %}  
{% if ue5_devlog.size > 0 %}
  {% for post in posts %}
  - {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})
  {% endfor %}
{% else %}
  아직 글이 없습니다.
{% endif %}