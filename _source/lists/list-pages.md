---
layout: page.html
pagination:
  data: data.lists
  size: 1
  alias: _i
permalink: "lists/{{ _i.slug }}/"
---

# {{ _i.name }}

{% assign yearsOfList = data.view_list_year_details | sort: 'year' | reverse | filterCollectionBy: 'list_id', _i.id %}
<ul>
{% for listYear in yearsOfList %}
  {% if listYear.list_id == _i.id %}
  <li><a href="{{ listYear | getListYearPermalink }}">{{ listYear.list_year_name }}</a></li>
  {% endif %}
{% endfor %}
</ul>