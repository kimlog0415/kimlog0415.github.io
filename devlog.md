---
layout: page
title: Dev Log
permalink: /devlog/
---

{%- comment -%}
1) devlog 카테고리 가진 글만 base로
{%- endcomment -%}
{% assign base = site.devlog
  | where_exp: "p", "p.categories contains 'devlog'"
  | sort: "date"
  | reverse
%}

{%- comment -%}
2) other_includes 만들기 (sections.yml의 include 전체를 1차원 배열로)
{%- endcomment -%}
{% capture inc_csv %}
{% for sec in site.data.sections %}
  {% assign sec_data = sec[1] %}
  {% for inc in sec_data.include %}{{ inc }},{% endfor %}
{% endfor %}
{% endcapture %}
{% assign other_includes = inc_csv | strip | split: "," | uniq %}

{%- comment -%}
========================
A) DevLog-only 섹션 (항상 최상단)
- 조건: categories에 devlog는 있고, sections include(ue5/tools/...)는 하나도 없는 글
- push 없이: group_by 후, group 내부에서 조건 검사 + 카운팅 + 3개 출력/나머지 hidden
========================
{%- endcomment -%}

### Dev Log ― DevLog

{% assign groups_all = base | group_by: "project" %}
{% assign any_devlog_only = 0 %}

{% for group in groups_all %}
  {%- assign total = 0 -%}
  {%- assign shown = 0 -%}
  {%- assign extra_id = "devlog-" | append: group.name | replace: " ", "-" | downcase -%}

  {%- comment -%} projectName은 그룹 첫 글에서 끌어오되, 없으면 project 값 {%- endcomment -%}
  {% assign first = group.items | first %}
  {% assign project_title = first.projectName | default: group.name %}

  {%- comment -%}
  1) 먼저 devlog-only에 해당되는 글이 이 project에 있는지 total을 계산
  {%- endcomment -%}
  {% for post in group.items %}
    {% assign is_other = false %}
    {% for inc in other_includes %}
      {% if inc != "" and post.categories contains inc %}
        {% assign is_other = true %}
      {% endif %}
    {% endfor %}
    {% unless is_other %}
      {% assign total = total | plus: 1 %}
    {% endunless %}
  {% endfor %}

  {% if total > 0 %}
    {% assign any_devlog_only = 1 %}

    <details open class="devlog-group">
      <summary class="devlog-summary">
        <span class="devlog-title">{{ project_title }}</span>
        <span class="devlog-meta">({{ total }} posts)</span>
      </summary>

      <ul class="devlog-list">
        {% for post in group.items %}
          {% assign is_other = false %}
          {% for inc in other_includes %}
            {% if inc != "" and post.categories contains inc %}
              {% assign is_other = true %}
            {% endif %}
          {% endfor %}

          {% unless is_other %}
            {% if shown < 3 %}
              <li>{{ post.date | date: "%Y-%m-%d" }} · <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
            {% endif %}
            {% assign shown = shown | plus: 1 %}
          {% endunless %}
        {% endfor %}
      </ul>

      {% if total > 3 %}
        <ul class="devlog-list devlog-extra" id="extra-{{ extra_id }}" hidden>
          {% assign idx = 0 %}
          {% for post in group.items %}
            {% assign is_other = false %}
            {% for inc in other_includes %}
              {% if inc != "" and post.categories contains inc %}
                {% assign is_other = true %}
              {% endif %}
            {% endfor %}

            {% unless is_other %}
              {% if idx >= 3 %}
                <li>{{ post.date | date: "%Y-%m-%d" }} · <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
              {% endif %}
              {% assign idx = idx | plus: 1 %}
            {% endunless %}
          {% endfor %}
        </ul>

        <button type="button" class="devlog-toggle" data-target="extra-{{ extra_id }}" aria-expanded="false">
          더보기 ({{ total | minus: 3 }}개)
        </button>
      {% endif %}
    </details>
  {% endif %}
{% endfor %}

{% if any_devlog_only == 0 %}
아직 글이 없습니다.
{% endif %}

---

{%- comment -%}
========================
B) 나머지 섹션들: "섹션 최신 업데이트 순"으로 정렬해서 출력
========================
{%- endcomment -%}

{% capture sec_keys_raw %}{% endcapture %}

{% for sec in site.data.sections %}
  {% assign sec_key = sec[0] %}
  {% assign sec_data = sec[1] %}

  {% assign sec_posts = base %}
  {% for inc in sec_data.include %}
    {% assign sec_posts = sec_posts | where_exp: "p", "p.categories contains inc" %}
  {% endfor %}

  {% assign latest = sec_posts | first %}
  {% if latest %}
    {% capture one %}{{ latest.date | date: "%s" }}::{{ sec_key }}{% endcapture %}
  {% else %}
    {% capture one %}0::{{ sec_key }}{% endcapture %}
  {% endif %}

  {% capture sec_keys_raw %}{{ sec_keys_raw }}
{{ one }}{% endcapture %}
{% endfor %}

{% assign sec_keys = sec_keys_raw | strip | split: "\n" | sort | reverse %}

{% for line in sec_keys %}
  {% assign parts = line | split: "::" %}
  {% assign sec_key = parts[1] %}
  {% assign sec_data = site.data.sections[sec_key] %}

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

<style>
  .devlog-toggle{
    margin: 6px 0 14px;
    padding: 6px 10px;
    border: 1px solid #d0d7de;
    border-radius: 8px;
    background: #f6f8fa;
    font-size: 13px;
    line-height: 1.2;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    gap: 6px;
  }
  .devlog-toggle:hover{ background:#eef2f6; }
  .devlog-toggle:active{ transform: translateY(1px); }
  .devlog-toggle[aria-expanded="true"]{
    background:#fff;
    border-color:#b6c2cf;
  }
  .devlog-summary{
    display:flex;
    align-items:baseline;
    gap:8px;
  }
  .devlog-title{ font-weight: 700; }
  .devlog-meta{ color:#6b7280; font-size:12px; }
  .devlog-list{ margin: 8px 0 0 18px; }
</style>

<script>
document.addEventListener("click", (e) => {
  const btn = e.target.closest(".devlog-toggle");
  if (!btn) return;

  const extra = document.getElementById(btn.dataset.target);
  if (!extra) return;

  const isOpen = !extra.hasAttribute("hidden");
  if (isOpen) {
    extra.setAttribute("hidden", "");
    btn.setAttribute("aria-expanded", "false");
    const count = extra.querySelectorAll("li").length;
    btn.textContent = `더보기 (${count}개)`;
  } else {
    extra.removeAttribute("hidden");
    btn.setAttribute("aria-expanded", "true");
    btn.textContent = "접기";
  }
});
</script>