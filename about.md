---
layout: page
title: About
---
<h2>Contact</h2>

<ul class="post-list">
  {% assign latest = site.devlog | sort: "date" | where_exp: "p", "p.categories contains 'devlog'" | reverse | slice: 0, 5 %}
  {% for post in latest %}
    <li>
      <div style="display:flex; gap:12px; align-items:center; text-decoration:none;">
	      <span class="post-meta">📧</span>
	      <span>kimlog0415@gmail.com</span>
	  </div>
	  <div style="display:flex; gap:12px; align-items:center; text-decoration:none;">
	      <span class="post-meta">▶️</span>
	      <a class="post-link" href="https://www.youtube.com/@kimlog1106">https://www.youtube.com/@kimlog1106</a>
	  </div>
    </li>
  {% endfor %}
</ul>