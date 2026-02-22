---
layout: page
title: Dev Log
permalink: /devlog/
---
### Dev Log ― Unreal Engine 5

{% assign posts = site.devlog  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'ue5'"  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'devlog'"  
| sort: "date" | reverse %}  
  
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}


### Dev Log ― Tools

{% assign posts = site.devlog  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'ue5'"  
| where_exp: "p", "(p.categories | join: ',' | downcase) contains 'devlog'"  
| sort: "date" | reverse %}  
  
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}