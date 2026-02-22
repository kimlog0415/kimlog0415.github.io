---
layout: page
title: Dev Log
permalink: /devlog/
---
### Dev Log ― Unreal Engine 5 
{% assign posts = site.posts  
| where_exp: "p", "p.tags contains 'ue5'"  
| where_exp: "p", "p.tags contains 'devlog'"  
| sort: "date" | reverse %}  
  
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}

### Dev Log ― Tools
{% assign posts = site.posts  
| where_exp: "p", "p.tags contains 'tools'"  
| where_exp: "p", "p.tags contains 'devlog'"  
| sort: "date" | reverse %}  
  
{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}