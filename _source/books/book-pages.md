---
pagination:
  data: data.view_item_details
  size: 1
  alias: _i
  # tell eleventy to resolve the object keys when paginating
  resolve: values
permalink: "/books/{{ _i.item_creator_slug }}/"
---
{% assign view_item_creators = data.view_item_creators-byid[_i.id] %}
{% assign item_creators = view_item_creators.creators | sort: 'principal' | reverse %}
{%- assign book_lists = data.view_list_year_item_details | filterCollectionBy: 'item_id',  _i.item_id | sort: 'year' | reverse -%}

{% for creator in item_creators %}
	{% if creator.principal %}{% assign principal_creator = creator %}{% endif %}
{% endfor -%}
<article itemscope itemtype="https://schema.org/Book">
<h1 itemprop="name">{{ _i.item_title }}</h1>

<p><em>{{ _i.item_title }}</em> by {{ principal_creator.name }} is includes in {{ book_lists.size }} list{% if book_lists.size > 1 %}s{% endif %} and has a <em>broadscore</em> of {{ _i.item_broadscore }}.</p>

<h2 id="header-creatorlist">Creators</h2>
<ul aria-labelledby="header-creatorlist">
{% for creator in item_creators %}
	<li><a itemprop="{{ creator.type }}" href="/creators/{{ creator.slug }}">{{ creator.name }} ({{ creator.type }})</a></li>
{% endfor %}
</ul>


<h3 id="header-listedlist">Listed</h3>
<p>{{ _i.item_title }} by <a itemprop="{{ creator.type }}" href="/creators/{{ principal_creator.slug }}">{{ principal_creator.name }}</a> is a book on Broadlist because it was included in these {{ book_lists.size }} lists:</p>
<ul aria-labelledby="header-listedlist">
{%- for item in book_lists -%}
{% assign item_award = item | getAward %}
{%- if _i.item_type == 'book' %}
<li>
	<a itemprop="award" href="/lists/{{ item.list_slug }}/{{ item.year | unlessExists: item.list_year_slug }}/">{{ item.list_year_name }}</a>{%- if item_award != false %} ({{ item_award }}){% endif %}
</li>
{% endif -%}
{%- endfor -%}
</ul>

{%- assign bookshopURL = _i | getBookshopURL %}
{% if bookshopURL -%}
<a href="{{ bookshopURL }}">Buy on Bookshop →</a>
<!-- <img width="16px" src="/_src/images/icon-bag.svg" /> -->
{%- endif %}

{% assign creator_details = data.view_creator_details-byid[principal_creator.id] %}

{% assign creator_items = creator_details.items | split: ", " %}
{% if creator_items.size > 0 %}

## Other Books on Broadlist
<p>{{ principal_creator.name }} is a creator of {{ creator_items.size }} books on Broadlist:</p>
<ul>
{%- assign totalBroadscore = 0 -%}
{%- for item_id in creator_items -%}
	{%- assign item_details = data.view_item_details-byid[item_id] -%}
	{%- assign view_item_creators = data.view_item_creators-byid[item_id] -%}
	{%- assign item_creators = view_item_creators.creators -%}
	{%- for creator in item_creators -%}
		{%- if creator.id == _i.id -%}
		{%- capture creator_type %}({{ creator.type | capitalize }}){%- endcapture -%}
		{%- endif -%}	
	{% endfor -%}
	{%- if item_details.item_type == "book" -%}
		{% assign totalBroadscore = totalBroadscore | plus: item_details.item_broadscore %}
		<li><a href="/books/{{ item_details.item_creator_slug }}">{{ item_details.item_title }}</a> {{ creator_type }}</li>
	{%- endif -%}
{%- endfor -%}
</ul>
{% endif %}

They have a total Broadscore of  {{  totalBroadscore }}

</article>
