---
title: Home
layout: page.html
---

# lists

<ul>
{% for list in data.lists %}
  <li><a href="/lists/{{ list.slug }}">{{ list.name }}</a></li>
{% endfor %}
</ul>