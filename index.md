---
title: 联机托管说明
permalink: index.html
layout: home
---

# 内容目录

下面列出了每个实验室练习和演示的超链接。

## 实验室

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 练习 | 任务 |
| --- | --- |
{% for activity in labs  %}| {{ activity.lab.exercise }} | [{{ activity.lab.task }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
