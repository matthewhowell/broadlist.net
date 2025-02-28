{% assign creator_details = data.view_creator_details-byid[_i.id] %}

## Listed Books
<p>{{ creator_details.name }} is a creator on Broadlist because they were the creator of these listed books:</p>
<ul>
{% assign creator_items = creator_details.items | split: ", " %}
{% for item_id in creator_items %}
	{% assign item_details = data.view_item_details-byid[item_id] %}
	{% assign view_item_creators = data.view_item_creators-byid[item_id] %}
	{% assign item_creators = view_item_creators.creators %}
	{% for creator in item_creators %}
		{% if creator.id == _i.id %}
		{% capture creator_type %}({{ creator.type | capitalize }}){% endcapture %}
		{% endif %}	
	{% endfor %}

	{% if item_details.item_type == "book" %}
		<li>
		<a href="/books/{{ item_details.item_creator_slug }}">{{ item_details.item_title }}</a> {{ creator_type }}
		</li>
	{% endif %}
{% endfor %}
</ul>
