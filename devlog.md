---
layout: page
title: Dev Log
permalink: /devlog/
---
site.devlog size = {{ site.devlog | size }}
첫 글 categories = {{ site.devlog[0].categories }}

### Today I Learn
{% assign ue5_devlog = site.devlog  
| where_exp: "p", "p.categories contains 'ue5'"  
| where_exp: "p", "p.project contains 'today-i-learn'"  
| sort: "date" | reverse %}

{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}

### Dev Log ― Unreal Engine 5

{% assign ue5_devlog = site.devlog  
| where_exp: "p", "p.categories contains 'ue5'"  
| where_exp: "p", "p.categories contains 'devlog'"  
| sort: "date" | reverse %}

{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}


### Dev Log ― Tools

{% assign ue5_devlog = site.devlog  
| where_exp: "p", "p.categories contains 'tools'"  
| where_exp: "p", "p.categories contains 'devlog'"  
| sort: "date" | reverse %}

{% for post in posts %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}