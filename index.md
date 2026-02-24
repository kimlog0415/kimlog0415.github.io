---
layout: default
title: Home
permalink: /
---
<h2>Latest Dev Log</h2>

<ul class="post-list">
  {% assign latest = site.devlog | sort: "date" | where_exp: "p", "p.categories contains 'devlog'" | reverse | slice: 0, 5 %}
  {% for post in latest %}
    <li>
      <span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
