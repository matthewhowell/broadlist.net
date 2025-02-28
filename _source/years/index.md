---
title: Home
layout: page.html
---

# lists

<ul>
{% assign years = data.view_years | reverse %}
{% for y in years %}
  <li><a href="/lists/{{ y.list_year }}">{{ y.list_year }} ({{y.total_lists}} list{% if y.total_lists > 1 %}s{% endif %})</a></li>
{% endfor %}
</ul>
