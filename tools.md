---
layout: page
title: Tools
permalink: /tools/
---
### Tools
{% assign posts = site.tools | where_exp: "p", "p.categories contains 'ue5'" | sort: "date" | reverse %}  
{% assign projects = tools | map: "project" | uniq | sort %}  
  
{% for proj in projects %}  
#### {{ proj }}  
  
{% assign group = posts | where: "project", proj %}  
{% for post in group %}  
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})  
{% endfor %}  
  
{% endfor %}

### Dev Log

{% assign tools_devlog = site.tools
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