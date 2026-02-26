---
layout: page
title: Tools
permalink: /tools/
---
## Projects
{% assign posts = site.devlog  
| where_exp: "p", "p.categories contains 'tools'"  
| where_exp: "p", "p.project"  
| sort: "date" | reverse %}
  
{% assign projects = posts  
| map: "project"  
| compact  
| uniq  
| sort %}
  
{% for proj in projects %}  

### {{ proj }}

{% assign group = posts | where: "project", proj %}

{% for post in group %}
- {{ post.date | date: "%Y-%m-%d" }} ｜ [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}

{% endfor %}

## Dev Log ― Tools  
  
{% assign items = site.devlog | sort: "date" | reverse %}  
{% assign count = 0 %}  
  
{% for post in items %}  
{% assign cats = post.categories | join: "," | downcase %}  
{% if cats contains "devlog" and cats contains "tools" %}  
- {{ post.date | date: "%Y-%m-%d" }} ｜ [{{ post.title }}]({{ post.url | relative_url }})  
{% assign count = count | plus: 1 %}  
{% endif %}  
{% endfor %} 