---
layout: page
title: Unreal Engine 5
permalink: /ue5/
---
### Projects
{% assign posts = site.devlog
  | where_exp: "p", "p.categories contains 'ue5'"
  | sort: "date" | reverse %}

{% assign projects = posts | map: "project" | uniq | sort %}

{% for proj in projects %}

## {{ proj }}

{% assign group = posts | where: "project", proj %}

{% for post in group %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}

{% endfor %}

### Dev Log

{% assign items = site.devlog | sort: "date" | reverse %}  
{% assign count = 0 %}  
  
{% for post in items %}  
{% assign cats = post.categories | join: "," | downcase %}  
{% if cats contains "devlog" and cats contains "ue5" %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% assign count = count | plus: 1 %}  
{% endif %}  
{% endfor %}  
  
{% if count == 0 %}  
아직 글이 없습니다.  
{% endif %}