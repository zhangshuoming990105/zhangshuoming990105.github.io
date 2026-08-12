---
title: "Blog"
permalink: /blogs/
---

{% assign groups = site.blogs | sort: "date" | reverse | group_by: "post_id" %}
<ul>
{% for group in groups %}
  {% assign en = group.items | where: "lang", "en" | first %}
  {% assign zh = group.items | where: "lang", "zh" | first %}
  {% assign main = en | default: zh | default: group.items[0] %}
  <li><b>{{ main.date | date: "%b %d, %Y" }}</b> — <a href="{{ main.url | relative_url }}">{{ main.title }}</a>{% if en and zh %} · <a href="{{ en.url | relative_url }}">EN</a> / <a href="{{ zh.url | relative_url }}">中文</a>{% endif %}</li>
{% endfor %}
</ul>
