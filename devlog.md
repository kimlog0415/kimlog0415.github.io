---
layout: page
title: Dev Log
permalink: /devlog/
---
총 posts: {{ site.devlog | size }}

### Dev Log ― Unreal Engine 5

{% assign ue5_devlog = site.devlog
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


### Dev Log ― Tools

{% assign tools_devlog = site.devlog
  | where_exp: "p", "p.categories contains 'tools'"
  | where_exp: "p", "p.categories contains 'devlog'"
  | sort: "date" | reverse %}

{% if tools_devlog.size > 0 %}
  {% for post in tools_devlog %}
  - {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})
  {% endfor %}
{% else %}
  아직 글이 없습니다.
{% endif %}