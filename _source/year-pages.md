<!-- ---
layout: page.md
pagination:
  data: data.list_years
  size: 1
  alias: item
permalink: "years/{{ item.year }}/"
---

# {{ item.year }}

<ul>
{% for listYear in data.list_years %}
  {% if listYear.year == item.year %}
  <li><a href="/lists/{{ item.name | slugify | remove_first: item.year | remove_first: '-' }}/{{ listYear.year}}">{{ listYear.name }}</a></li>
  {% endif %}
{% endfor %}
</ul> -->
