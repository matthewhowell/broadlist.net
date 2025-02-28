---json
{
  "permalink": "lists/feed.xml",
  "eleventyExcludeFromCollections": true,
  "metadata": {
    "title": "Broadlist: Latest Lists",
    "description": "The most recent lists added to broadlist.net",
    "language": "en",
    "base": "https://broadlist.net",
    "author": {
      "name": "Broadlist"
    }
  }
}
---
<?xml version="1.0" encoding="utf-8"?>
{%- assign list_years_by_year = data.list_years | sort: 'created' | reverse -%}
{%- assign feed_last_updated = list_years_by_year | getNewestCollectionItemDate | getDateObject | dateToRfc3339 -%}
<feed xmlns="http://www.w3.org/2005/Atom" xml:lang="{{ metadata.language }}">
  <title>{{ metadata.title }}</title>
  <subtitle>{{ metadata.description }}</subtitle>
  <link href="{{ metadata.base}}/{{ permalink }}" rel="self" />
  <link href="{{ metadata.base }}" />
  <updated>{{ feed_last_updated }}</updated>
  <id>{{ metadata.base | addPathPrefixToFullUrl }}</id>
  <author>
    <name>{{ metadata.author.name }}</name>
  </author>
{%- for entry in list_years_by_year -%}
	{%- capture relativeEntryUrl %}/lists/{{ entry.slug }}/{{ listYear.year }}{% endcapture %}
	{%- capture absoluteEntryUrl %}{{ metadata.base }}{{relativeEntryUrl}}{% endcapture %}
	{%- assign list_year_items = data.view_list_year_item_details | filterCollectionBy: 'list_year_id', entry.id | sort: 'item_title' %}
	TODO filter collections for 
	longlist
	shortlist
	winner

	only show if list.size
<entry>
	<title>{{ entry.name }}</title>
	<link href="{{ absoluteEntryUrl }}" />
	<updated>{{ entry.created | getDateObject | dateToRfc3339 }}</updated>
	<id>{{ absoluteEntryUrl }}</id>
	<content type="html"><![CDATA[
<h1>{{ entry.name }}</h1>
{% render 'list-year-detail.md', lyi: list_year_items, list_year_name: entry.name, vcd: data.view_creator_details %}
]]></content>
</entry>{%- endfor %}
</feed>