---
layout: default
title: Home
permalink: /
---

<div class="hero">
  <h1>Kim Log</h1>
  <p class="subtitle">Project-based builder · Unreal Engine · Web Tools · Backend</p>
  <div class="hero-actions">
    <a class="btn primary" href="/UE5/">Unreal</a>
    <a class="btn" href="/webtools/">Web Tools</a>
    <a class="btn" href="/backend/">Backend</a>
  </div>
</div>

<h2>Featured</h2>

<div class="cards">
  <a class="card" href="/ue5/">
    <div class="card-title">Unreal Engine</div>
    <div class="card-desc">Number Run · RPS Machine · MIDI interaction</div>
    <div class="card-meta">View posts →</div>
  </a>

  <a class="card" href="/webtools/">
    <div class="card-title">Web Tools</div>
    <div class="card-desc">PDF tools · Image converter · Browser utilities</div>
    <div class="card-meta">View tools →</div>
  </a>
  
</div>

<h2>Latest Dev Log</h2>

<ul class="post-list">
  {% assign latest = site.posts | sort: "date" | reverse | slice: 0, 5 %}
  {% for post in latest %}
    <li>
      <span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
