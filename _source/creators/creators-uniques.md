---
pagination:
  data: data.view_creators_uniques
  size: 1
  alias: _i
permalink: /creators/{{ _i.slug }}/
someother: 123
---

# {{ _i.name }}
{% if _i.extended_display_name.size > 0 -%}
({{ _i.extended_display_name }})
{%- endif -%}

{% include "creator-page-detail.md" %}