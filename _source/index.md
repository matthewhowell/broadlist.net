---
title: Home
layout: page

numberOfRecentLists: 10
numberOfRecentBooks: 10
numberOfRecentCreators: 10
---

Broadlist

*Broadlist* is a collection of books which have been included in longlists, shortlists, and literary prizes from all over the world. Its purpose is to catelogue those lists and help readers find books to read. Read [more about its purpose](/purpose).

To date, Broadlist has collected {{ data.list_years.size }} book lists, spanning {{ data.view_years.size }} years, including {{ data.view_item_details.size }} books from {{ data.view_creator_stats.size }} authors.

## Recently Added Lists
{% assign listCounter = 1 %}
{{ data.view_list_year_details.size }}
{% assign list_years_by_year = data.view_list_year_details | sort: 'created' | reverse %}
{% for l in list_years_by_year %}
<a href="{{ l | getListYearPermalink }}">{{ l.list_year_name }}</a>
{% assign listCounter = listCounter | plus: 1 %}
{% endfor %}

## Recently Added Books
{% assign books_by_date_added = data.view_item_details | sort: 'item_created' | reverse | getFirstItems: numberOfRecentBooks %}
{% for item_details in books_by_date_added %}
<a href="/books/{{ item_details.item_slug }}">{{ item_details.item_title }}</a>
{% endfor %}

## Recently Added Creators
{% assign creators_by_date_added = data.view_creator_details | sort: 'created' | reverse |getFirstItems: numberOfRecentCreators %}
{% for creator in creators_by_date_added %}
<a href="/creators/{{ creator.slug }}">{{ creator.name }}</a>
{% endfor %}