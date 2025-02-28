{%- assign list_year_verylonglist = lyi | sort: 'item_title' | filterCollectionBy: 'verylonglist', true %}
{%- assign list_year_longlist = lyi | sort: 'item_title' | filterCollectionBy: 'longlist', true %}
{%- assign list_year_shortlist = lyi | sort: 'item_title' | filterCollectionBy: 'shortlist', true %}
{%- assign list_year_winners = lyi | sort: 'item_title' | filterCollectionBy: 'winner', true %}

In {{ ly.year }} the <em>{{ ly.list_name }}</em> list selected {{ lyi.size }} books.

Broadlist has categorized these selections as:
<ul>
{%- if list_year_verylonglist.size > 0 %}
<li><a href="#header-verylonglist">Verylonglist</a> ({{list_year_verylonglist.size}} books)</li>{% endif %}
{%- if list_year_longlist.size > 0 %}
<li><a href="#header-longlist">Longlist</a> ({{list_year_longlist.size}} books)</li>{% endif %}
{%- if list_year_shortlist.size > 0 %}
<li><a href="#header-shortlist">Shortlist</a> ({{list_year_shortlist.size}} books)</li>{% endif %}
{%- if list_year_winners.size > 0 %}
<li><a href="#header-winners">Winners</a> ({{list_year_winners.size}} books)</li>{% endif %}
</ul>

Read more about [how Broadlist categorizes lists](/docs).

<cite>Source: <a href="{{ ly.list_year_source }}">{{ ly.list_year_name }} </a></cite>



{% if list_year_verylonglist.size > 0 %}
<h2 id="header-verylonglist">Very Long List</h2>
<ul class="book-grid-list">
{% for item in list_year_verylonglist -%}
{% assign creator = creator_details_by_id[item.creator_id] %}
{%- assign bookshopURL = item | getBookshopURL %}
{%- if creator.name.size > 0 -%}
	<li>
	<a href="/books/{{ item.item_creator_slug }}/">{{ item.item_title }}</a>
	<a href="/creators/{{ creator.slug }}"><em>{{ item.creator_name }}</em></a>
	{%- if bookshopURL -%}
	<a href="{{ bookshopURL }}">Buy →</a>
	<!-- <img width="16px" src="/_src/images/icon-bag.svg" /> -->
	{%- endif %}
	</li>
{%- endif -%}
{% endfor -%}
</ul>
{% endif %}

{% if list_year_longlist.size > 0 %}
<h2 id="header-longlist">Long List</h2>
<ul>
{% for item in list_year_longlist -%}
{% assign creator = creator_details_by_id[item.creator_id] %}
{%- assign bookshopURL = item | getBookshopURL %}
{%- if creator.name.size > 0 -%}
	<li>
		<a href="/books/{{ item.item_creator_slug }}/">{{ item.item_title }}</a> by <a href="/creators/{{ creator.slug }}">{{ item.creator_name }}</a>
		{% if bookshopURL -%}
		<a href="{{ bookshopURL }}">Buy on Bookshop →</a>
		<!-- <img width="16px" src="/_src/images/icon-bag.svg" /> -->
		{%- endif %}
	</li>
{%- endif -%}
{% endfor -%}
</ul>
{% endif %}

{% if list_year_shortlist.size > 0 %}
<h2 id="header-shortlist">Short List</h2>
<ul class="list-book">
{% for item in list_year_shortlist -%}
{%- if item.shortlist -%}
{% assign creator = creator_details_by_id[item.creator_id] %}
{%- assign bookshopURL = item | getBookshopURL %}
{%- if creator.name.size > 0 -%}
	<li itemscope itemtype="https://schema.org/Book">
		<a itemprop="name" href="/books/{{ item.item_creator_slug }}/">{{ item.item_title }}</a> by <a itemprop="author" href="/creators/{{ creator.slug }}">{{ item.creator_name }}</a>
	{% if bookshopURL -%}
	<a href="{{ bookshopURL }}">Buy on Bookshop →</a>
	<!-- <img width="16px" src="/_src/images/icon-bag.svg" /> -->
	{%- endif %}
	</li>
{%- endif -%}
{% endif -%}
{% endfor -%}
</ul>
{% endif %}

{% if list_year_winners.size > 0 %}
<h2 id="header-winners">Winners</h2>
<ul>
{% for item in list_year_winners -%}
{%- if item.winner -%}

{% assign creator = creator_details_by_id[item.creator_id] %}
{%- if creator.name.size > 0 -%}
	<li>
		<a href="/books/{{ item.item_creator_slug }}/">{{ item.item_title }}</a> by <a href="/creators/{{ creator.slug }}">{{ item.creator_name }}</a>
	</li>
{%- endif -%}
{% endif -%}
{% endfor -%}
</ul>
{% endif %}

<h3>More lists</h3>
<a href="">View the full list on Broadlist.net</>
<a href="">View other years if LIST name</>
<a href="">View other lists from 2025</>

<style>
	ul.list-book { 
		list-style-type: none;
		list-style-image: url('/_src/images/listicon-book.svg');
	}
	ul.list-book li {
		background-color: whitesmoke;
		margin-bottom: 8px;
		padding: 4px;
	}

	ul.list-book li::marker {
  		content: url('/_src/images/listicon-book.svg') ' ';
	}

	.book-grid-list { 
		/* font-family: monospace; */
		font-weight: normal;
		padding:0;
	}

	.book-grid-list > li:hover,
	.book-grid-list > li:has(a:focus)
	{
		outline: 1px solid black;
		box-shadow: 4px 4px 0px black;
		z-index: 2;

		/* position: relative;
		top: -2px;
		left: -0px; */

		/* transition: all .1s ease-in-out; */
	}
/* 
	.book-grid-list > li:has(a:hover),
	.book-grid-list > li:has(a:focus)
	 {
		outline: 1px solid black;
		box-shadow: 3px 3px 0px black;
		position: relative;
		top: -3px;
		left: -3px;
		z-index: 2;
		transition: all .1s ease-in-out;
	} */

	.book-grid-list > li > a {
		/* padding: 0 4px; */
		line-height: 1.5rem;
	}

	.book-grid-list > li > a:hover,
	.book-grid-list > li > a:focus {
		font-weight: bold;
		outline: 1px solid blue;
		outline-style: inset;
	}
 
	.book-grid-list > li {
		display: grid;		
		grid-template-columns: repeat(auto-fit, minmax(12rem, 1fr));
		place-items: center left;
		column-gap: 1rem;
		z-index: 0;
		line-height: 32px;
		padding: 4px 0;
  		/* transition: all 0.1s cubic-bezier(.7,.2,.17,1); */
	}

	ul.book-grid-list li:nth-child(even) {
		background: color-mix(in srgb, indigo, transparent 90%);
	}
	ul.book-grid-list li:nth-child(odd) {
		/* background: white; */
	}

	ul.book-grid-list li > a:nth-child(3) {
		text-transform: uppercase;
		font-size: .75rem;
	}
/* 
	@media (width <= 24rem) {
		.book-grid-list > li {
			grid-template-columns: none;
			grid-template-rows: 1fr 1fr 1fr;
			gap: 0rem 1rem;
			margin-bottom: 1rem;
			line-height: 24px;
		}
	}
/*  */
	
	@media (width <= 48rem) {
		.book-grid-list > li {
			grid-template-columns: none;
			grid-template-rows: auto;
		}
	} */
</style>