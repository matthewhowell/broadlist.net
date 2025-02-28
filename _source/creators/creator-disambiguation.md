---
pagination:
  data: data.view_creators_disambiguations
  size: 1
  alias: _i
permalink: /creators/{{ _i.slug }}/

---
# {{ _i.name }} (disambiguation)

{% assign duplicate_creators = _i.buids | split: ", " %}

Why does this page exist? There are {{ duplicate_creators | size }} different creators with the name '{{ _i.name }}'.

{% for creator_buid in duplicate_creators %}
	<a href="/creators/{{ _i.slug }}/{{ creator_buid }}">{{ _i.name }} ({{ creator_buid }})</a>
	<br />
{% endfor %}