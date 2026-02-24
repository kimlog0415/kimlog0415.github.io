---
layout: page
title: Dev Log
permalink: /devlog/
---
{% assign p = site.devlog[0] %}
cats(raw)= {{ p.categories }} / cats(join)= {{ p.categories | join: '|' }}



{% assign base = site.devlog  
| where_exp: "p", "p.categories contains 'devlog'"  
| sort: "date"  
| reverse %}  
  
{%- comment -%}  
other_includes = (ue5/tools/...) 섹션들의 include 값을 전부 모은 리스트  
→ devlog-only = devlog이면서 other_includes 중 어떤 것도 포함하지 않는 글  
{%- endcomment -%}  
  
{% capture inc_csv %}  
{% for sec in site.data.sections %}  
{% assign data = sec[1] %}  
{% for inc in data.include %}{{ inc }},{% endfor %}  
{% endfor %}  
{% endcapture %}  
{% assign other_includes = inc_csv | strip | split: "," | uniq %}  
  
{%- comment -%} 1) ue5/tools/... 섹션 렌더 {%- endcomment -%}  
{% for sec in site.data.sections %}  
{% assign sec_key = sec[0] %}  
{% assign sec_data = sec[1] %}  
{% assign sec_posts = base %}  
  
{% for inc in sec_data.include %}  
{% assign sec_posts = sec_posts | where_exp: "p", "p.categories contains inc" %}  
{% endfor %}  
  
### Dev Log ― {{ sec_data.title }}  
  
{% if sec_posts.size == 0 %}  
아직 글이 없습니다.  
{% else %}  
{% assign groups = sec_posts | group_by: "project" %}  
{% for group in groups %}  
{% assign first = group.items | first %}  
{% assign project_title = first.projectName | default: group.name %}  
{% assign gid = sec_key | append: "-" | append: group.name | replace: " ", "-" | downcase %}  
  
<details open class="devlog-group">  
<summary class="devlog-summary">  
<span class="devlog-title">{{ project_title }}</span>  
<span class="devlog-meta">({{ group.items.size }} posts)</span>  
</summary>  
  
<ul class="devlog-list">  
{% for post in group.items limit: 3 %}  
<li>{{ post.date | date: "%Y-%m-%d" }} · <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>  
{% endfor %}  
</ul>  
  
{% if group.items.size > 3 %}  
<ul class="devlog-list devlog-extra" id="extra-{{ gid }}" hidden>  
{% for post in group.items offset: 3 %}  
<li>{{ post.date | date: "%Y-%m-%d" }} · <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>  
{% endfor %}  
</ul>  
  
<button type="button" class="devlog-toggle" data-target="extra-{{ gid }}" aria-expanded="false">  
더보기 ({{ group.items.size | minus: 3 }}개)  
</button>  
{% endif %}  
</details>  
  
{% endfor %}  
{% endif %}  
  
---  
  
{% endfor %}  
  
{%- comment -%} 2) devlog-only 섹션(자동) {%- endcomment -%}  
  
{% assign devlog_only = base %}  
{% for inc in other_includes %}  
{% if inc != "" %}  
{% assign devlog_only = devlog_only | where_exp: "p", "p.categories contains inc == false" %}  
{% endif %}  
{% endfor %}  
  
### Dev Log ― DevLog  
  
{% if devlog_only.size == 0 %}  
아직 글이 없습니다.  
{% else %}  
{% assign groups = devlog_only | group_by: "project" %}  
{% for group in groups %}  
{% assign first = group.items | first %}  
{% assign project_title = first.projectName | default: group.name %}  
{% assign gid = "devlog-" | append: group.name | replace: " ", "-" | downcase %}  
  
<details open class="devlog-group">  
<summary class="devlog-summary">  
<span class="devlog-title">{{ project_title }}</span>  
<span class="devlog-meta">({{ group.items.size }} posts)</span>  
</summary>  
  
<ul class="devlog-list">  
{% for post in group.items limit: 3 %}  
<li>{{ post.date | date: "%Y-%m-%d" }} · <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>  
{% endfor %}  
</ul>  
  
{% if group.items.size > 3 %}  
<ul class="devlog-list devlog-extra" id="extra-{{ gid }}" hidden>  
{% for post in group.items offset: 3 %}  
<li>{{ post.date | date: "%Y-%m-%d" }} · <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>  
{% endfor %}  
</ul>  
  
<button type="button" class="devlog-toggle" data-target="extra-{{ gid }}" aria-expanded="false">  
더보기 ({{ group.items.size | minus: 3 }}개)  
</button>  
{% endif %}  
</details>  
  
{% endfor %}  
{% endif %}  
  
<script>  
document.addEventListener("click", (e) => {  
const btn = e.target.closest(".devlog-toggle");  
if (!btn) return;  
const extra = document.getElementById(btn.dataset.target);  
if (!extra) return;  
  
const open = !extra.hasAttribute("hidden");  
if (open) {  
extra.setAttribute("hidden", "");  
btn.textContent = btn.textContent.replace("접기", "더보기");  
btn.setAttribute("aria-expanded", "false");  
const count = extra.querySelectorAll("li").length;  
if (!btn.textContent.includes("(")) btn.textContent = `더보기 (${count}개)`;  
} else {  
extra.removeAttribute("hidden");  
btn.textContent = "접기";  
btn.setAttribute("aria-expanded", "true");  
}  
});  
</script>