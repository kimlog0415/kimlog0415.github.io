---
layout: page
title: Dev Log
permalink: /devlog/
---
{% assign p = site.devlog[0] %}
cats(raw)= {{ p.categories }} / cats(join)= {{ p.categories | join: '|' }}



{% assign base = site.devlog | where_exp: "p", "p.categories contains 'devlog'" %}  
  
{% comment %} =========================  
Section: Dev Log ― Unreal Engine 5  
========================= {% endcomment %}  
## Dev Log ― Unreal Engine 5  
  
{% assign ue5_posts = base  
| where_exp: "p", "p.categories contains 'ue5'"  
| sort: "date"  
| reverse %}  
  
{% if ue5_posts.size == 0 %}  
아직 글이 없습니다.  
{% else %}  
{% assign ue5_groups = ue5_posts | group_by: "project" %}  
  
{% for group in ue5_groups %}  
{% assign first = group.items | first %}  
{% assign project_title = first.projectName | default: group.name %}  
  
<details open class="devlog-group">  
<summary class="devlog-summary">  
<span class="devlog-title">{{ project_title }}</span>  
<span class="devlog-meta">({{ group.items.size }} posts)</span>  
</summary>  
  
<ul class="devlog-list">  
{% for post in group.items limit: 3 %}  
<li>  
{{ post.date | date: "%Y-%m-%d" }} ·  
<a href="{{ post.url | relative_url }}">{{ post.title }}</a>  
</li>  
{% endfor %}  
</ul>  
</details>  
  
{% endfor %}  
{% endif %}  
  
---  
  
{% comment %} =========================  
Section: Dev Log ― Tools  
========================= {% endcomment %}  
## Dev Log ― Tools  
  
{% assign tools_posts = base  
| where_exp: "p", "p.categories contains 'tools'"  
| sort: "date"  
| reverse %}  
  
{% if tools_posts.size == 0 %}  
아직 글이 없습니다.  
{% else %}  
{% assign tools_groups = tools_posts | group_by: "project" %}  
  
{% for group in tools_groups %}  
{% assign first = group.items | first %}  
{% assign project_title = first.projectName | default: group.name %}  
  
<details open class="devlog-group">  
<summary class="devlog-summary">  
<span class="devlog-title">{{ project_title }}</span>  
<span class="devlog-meta">({{ group.items.size }} posts)</span>  
</summary>  
  
<ul class="devlog-list">  
{% for post in group.items limit: 3 %}  
<li>  
{{ post.date | date: "%Y-%m-%d" }} ·  
<a href="{{ post.url | relative_url }}">{{ post.title }}</a>  
</li>  
{% endfor %}  
</ul>  
</details>  
  
{% endfor %}  
{% endif %}
  
{% if count == 0 %}  
아직 글이 없습니다.  
{% endif %}