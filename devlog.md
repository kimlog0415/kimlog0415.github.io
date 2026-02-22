---
layout: page
title: Dev Log
permalink: /devlog/
---
site.devlog size = {{ site.devlog | size }}
첫 글 categories = {{ site.devlog[0].categories }}

## Today I Learn
{% assign items = site.devlog | sort: "date" | reverse %}  
{% assign count = 0 %}  
  
{% for post in items %}  
{% assign cats = post.categories | join: "," | downcase %}  
{% if cats contains "devlog" and cats project "today-i-learn" %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% assign count = count | plus: 1 %}  
{% endif %}  
{% endfor %}  
  
{% if count == 0 %}  
아직 글이 없습니다.  
{% endif %}
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