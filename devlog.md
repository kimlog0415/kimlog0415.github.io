---
layout: page
title: Dev Log
permalink: /devlog/
---
{% assign p = site.devlog[0] %}
cats(raw)= {{ p.categories }} / cats(join)= {{ p.categories | join: '|' }}

## Today I Learn
{% assign posts = site.devlog  
| where_exp: "p", "p.categories contains 'devlog' and p.project"
| sort: "date"  
| reverse %}  
  
{% assign groups = posts | group_by: "project" %}  
  
{% for group in groups %}  
### {{ group.name }}  
  
{% for post in group.items %}  
- {{ post.date | date: "%Y-%m-%d" }} ·  
[{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}  
  
{% endfor %}

## Dev Log ― Unreal Engine 5  
  
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

## Dev Log ― Tools  
  
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