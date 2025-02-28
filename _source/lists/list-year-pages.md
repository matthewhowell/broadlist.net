---
layout: page.html
pagination:
  data: data.view_list_year_details
  size: 1
  alias: _i
permalink: "{{ _i | getListYearPermalink }}"
---
{%- assign parent_list = data.lists | filterCollectionBy: 'id', _i.list_id -%}
{% for list in parent_list %}
{% for n in list.notes %}
	{{ n }}
{% endfor %}
{% endfor %}

# {{ _i.list_year_name }}

{% if _i.extended_display_name.size > 0 -%}
Also known as the **{{ _i.extended_display_name }}**
{%- endif %}

{% if _i.short_description -%}
**{{ _i.short_description }}**
{%- endif %}
{% assign sorted_items = data.view_list_year_item_details | filterCollectionBy: 'item_type', 'book' | filterCollectionBy: 'list_id', _i.list_id | filterCollectionBy: 'list_year_id', _i.id | filterCollectionBy: 'year', _i.year %}

{% render 'list-year-detail.md', lyi: sorted_items, ly: _i, list_year_name: _i.list_year_name, creator_details_by_id: data.view_creator_details-byid %}

{% render 'list-year-links.md', list_year: _i %}

{% render 'list-year-footer.md', list_year: _i %}
