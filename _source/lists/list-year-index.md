---
layout: page.html
pagination:
  data: data.view_year_lists
  size: 1
  alias: _i
permalink: "lists/{{ _i.list_year }}/"
---
{% assign year_details = _i.list_years %}
#  {{ _i.list_year }}

<h2 id="header-mostlistedbooks"> {{ _i.awards_year }} Most Listed Books</h2>
{% assign most_listed_books = data.view_list_year_item_totals | filterCollectionBy: 'awards_year', _i.awards_year | getFirstItems: 10 %}

<ul aria-labelledby="header-mostlistedbooks">{% for i in most_listed_books %}
{%- if i.listed_total > 1 -%}
{%- assign item = data.view_item_details-byid[i.item_id] -%}
{%- assign creator = data.view_creator_details-byid[i.creator_id] -%}
<li><a href="/books/{{ item.item_creator_slug }}/">{{ item.item_title }}</a> by <a href="/creators/{{ creator.slug }}">{{ creator.name }}</a> (appears on {{ i.listed_total }} lists)</li>
{%- endif -%}
{% endfor %}</ul>

<h2 id="header-{{ _i.year }}lists">{{ _i.awards_year }} Lists</h2>
{% if year_details.size > 0 %}
Broadlist has collected {{ year_details.size }} lists from {{ _i.awards_year }}

<ul aria-labelledby="header-{{ _i.awards_year }}lists">
{% for y in year_details -%}
	
	<li><a href="/lists/{{ y.slug }}/{{ _i.awards_year | unlessExists: y.year_slug }}/">{{ y.name | removeListYear }}</a> {{ _i.awards_year }}</li>
{% endfor -%}
</ul>
{% endif %}

{% assign broadscore_books = data.view_list_year_item_totals | filterCollectionBy: 'year', _i.year | sort: "broadscore" | reverse | getFirstItems: 10 %}
<h2 id="header-broadscore">{{ _i.year }} Broadscore</h2>
{% if broadscore_books.size > 0 %}
<ul aria-labelledby="header-broadrank">
{% for i in broadscore_books -%}
	{%- assign item = data.view_item_details-byid[i.item_id] -%}
	{%- assign creator = data.view_creator_details-byid[i.creator_id] -%}
	{{ i.broadscore }} - {{ item.item_title }} <br />
{% endfor -%}
</ul>
{% endif %}

{% assign every_listed_book = data.view_list_year_item_totals | filterCollectionBy: 'year', _i.year | sort_natural: 'item_title' %}
## Every Listed Book from {{ _i.year }}
Broadlist has collected {{ every_listed_book.size }} books from lists in {{ _i.year }}

<sortable-table class="table-wrapper" tabindex="0" role="region" aria-labelledby="table-everylistedbook">
<table class="sortable-books">
	<caption id="table-everylistedbook">Every Listed Book from {{ _i.year }}</caption>
 	<thead>
		<tr>
			<th scope="col" data-sort="alpha">
        		<button>Book<span aria-hidden="true"></span></button>
			</th>
			<th scope="col" data-sort="alpha">
				<button>Author<span aria-hidden="true"></span></button>
			</th>
			<th scope="col" data-sort="numeric">
				<button>Lists<span aria-hidden="true"></span></button>
				</th>
			<th scope="col" data-sort="numeric">
				<button>Broadscore<span aria-hidden="true"></span></button>
			</th>
		</tr>
 	</thead>
	<tbody>

{% for i in every_listed_book %}
{%- assign item = data.view_item_details-byid[i.item_id] -%}
{%- assign creator = data.view_creator_details-byid[i.creator_id] -%}
	<tr>
		<th scope="row"><a href="/books/{{ item.item_creator_slug }}/">{{ item.item_title }}</a></th>
		<td><a href="/creators/{{ creator.slug }}">{{ creator.name }}</a></td>
		<td>{{ i.listed_total }}</td>
		<td>{{ i.broadscore }}</td>
	</tr>
{% endfor %}</ul>
	</tbody>
	<tfoot>
		<tr>
			<th scope="row">Total books listed in {{ _i.year }}</th>
			<td></td>
			<td>{{ every_listed_book.size }}</td>
		</tr>
	</tfoot>
</table>
</sortable-table>


<style>
.table-wrapper {
	overflow: scroll;
}
body {
	font-family: 'Open Sans', sans-serif;
	line-height: 1.5;
}
table {
	text-align: left;
	border-collapse: collapse;
	caption-side: bottom;
}

tr {
	border-bottom: 1px solid;
}

th:first-child {
	position: sticky;
	z-index: 2;
	inset-inline-start: 0;
	left: 0;
	border-inline-end: none;
}

td:first-of-type,
:where(thead, tfoot) th:nth-child(2) {
	border-inline-start: none;
}


thead th,
tfoot th {
	background: whitesmoke;
}

th,
caption {
	text-align: start;
}

th:first-child::after {
	content: '';
	position: absolute;
	inset-block-start: 0;
	inset-inline-end: 0;
	width: 1px;
	height: 100%;
	background: lightgrey;
}

td:nth-child(3),
td:nth-child(4) {
	text-align: end;
	font-family: monospace;
	font-size: 1rem;
}
thead {
	border-block-end: 2px solid;
	background: whitesmoke;
}

tfoot {
	border-block: 2px solid;
	background: whitesmoke;
}

th,
td {
	border: 1px solid lightgrey;
	padding: 0.25rem 0.75rem;
	vertical-align: baseline;
}

table {
	--color: #d0d0f5;
}

thead,
tfoot {
	background: var(--color);
}

tbody tr:nth-child(even) {
	background: color-mix(in srgb, var(--color), transparent 60%);
}

/* add outline to indicate keyboard focus */
[role="region"][aria-labelledby][tabindex]:focus {
  outline: .1em solid rgba(0,0,0,.1);
}


thead th {
	vertical-align: bottom;
}

thead th:is(:last-child) {
	width: 3rem;
}




table.sortable th[aria-sort="descending"] span::after {
  content: "▼";
  color: currentcolor;
  font-size: 100%;
  top: 0;
}

table.sortable th[aria-sort="ascending"] span::after {
  content: "▲";
  color: currentcolor;
  font-size: 100%;
  top: 0;
}

table.show-unsorted-icon th:not([aria-sort]) button span::after {
  content: "♢";
  color: currentcolor;
  font-size: 100%;
  position: relative;
  top: -3px;
  left: -4px;
}

table.sortable th button:focus,
table.sortable th button:hover {
  padding: 2px;
  border: 2px solid currentcolor;
  background-color: #e5f4ff;
}

table.sortable th button:focus span,
table.sortable th button:hover span {
  right: 2px;
}

table.sortable th:not([aria-sort]) button:focus span::after,
table.sortable th:not([aria-sort]) button:hover span::after {
  content: "▼";
  color: currentcolor;
  font-size: 100%;
  top: 0;
}

</style>
	
<script>
// https://www.w3.org/WAI/ARIA/apg/patterns/table/examples/sortable-table/
// function sortTableRowsByColumn( table, columnIndex, ascending ) {
//     const rows = Array.from( table.querySelectorAll( ':scope > tbody > tr' ) );

// 	const alphaColumns = [0, 1];
// 	const numericColumns = [2, 3];

//     rows.sort( ( x, y ) => {

// 		// gather the text content of the two table cells to compare
//         const xValue = x.cells[columnIndex].textContent;
//         const yValue = y.cells[columnIndex].textContent;

// 		// if numeric column
// 		if (numericColumns.includes(columnIndex)) {
// 			const xNum = parseInt( xValue );
// 			const yNum = parseInt( yValue );
// 			return ascending ? ( xNum - yNum ) : ( yNum - xNum );
// 		} else if (alphaColumns.includes(columnIndex)) {
// 			if (ascending) {
// 				if (xValue > yValue) {
// 					return 1;
// 				} else {
// 					return -1;
// 				}
// 			} else {
// 				if (xValue > yValue) {
// 					return -1;
// 				} else {
// 					return 1;
// 				}
// 			}
// 		}

//     });

//     for( let row of rows ) {
//         table.tBodies[0].appendChild(row);
//     }
// }

// function onColumnHeaderClicked( ev ) {
    
//     const th = ev.currentTarget;
//     const table = th.closest( 'table' );
//     const thIndex = Array.from( th.parentElement.children ).indexOf( th );
//     const ascending = !( 'sort' in th.dataset ) || th.dataset.sort != 'asc';
//     sortTableRowsByColumn( table, thIndex, ascending );

//     const allTh = table.querySelectorAll( ':scope > thead > tr > th' );
//     for( let th2 of allTh ) {
//         delete th2.dataset['sort'];
//     }
 
//     th.dataset['sort'] = ascending ? 'asc' : 'desc';
// }

// window.addEventListener( 'DOMContentLoaded', function() {

//     for (var i = 0; i < this.columnHeaders.length; i++) {
//       var ch = this.columnHeaders[i];
//       var buttonNode = ch.querySelector('button');
//       if (buttonNode) {
//         this.sortColumns.push(i);
//         buttonNode.setAttribute('data-column-index', i);
//         buttonNode.addEventListener('click', this.handleClick.bind(this));
//       }

//     const table = document.querySelector( 'table.sortable-books' );
//     const tb = table.tBodies[0];
// });



class SortableTable extends HTMLElement {
  constructor() {
    super();
	this.tableColumns = [];
    this.tableRows = [];
    this.lastSort = null;
    this.sortAsc = true;
  }
  
  connectedCallback() {
    let table = this.querySelector('table');

    // sortable-table requires a <table> child element
    if(!table) {
      return;
    }
    
	this.tableColumns = Array.from(this.querySelectorAll('thead th[scope="col"]'));
	console.log(this.tableColumns);

    // let numericColumns = [];
    // if(this.hasAttribute('numeric')) {
    //   numericColumns = this.getAttribute('numeric').split(',').map(x => parseInt(x-1,10));
    // }
    
    // // require tbody and thead
    // let tbody = table.querySelector('tbody');
    // let thead = table.querySelector('thead');
    // if(!tbody || !thead) {
    //   console.warn('table-sort: No tbody or thead found. Exiting.');
    //   return;     
    // }
    
    // let rows = tbody.querySelectorAll('tr');
    // rows.forEach(r => {
    //   let datum = [];
    //   let row = r.querySelectorAll('td');
    //   row.forEach((r,i) => {
    //     if(numericColumns.indexOf(i) >= 0) datum[i] = parseInt(r.innerText,10);
    //     else datum[i] = r.innerText;
    //   });
    //   this.data.push(datum);
    // });
    
    // // Get our headers
    // let headers = thead.querySelectorAll('th');
    // headers.forEach((h,i) => {
    //   h.style.cursor = 'pointer';
    //   h.addEventListener('click', e => {
    //       this.sortCol(e,i);
    //   });
    // });
    
    // // copy body to this scope so we can use it again later
    // this.tbody = tbody;

  }
  
  renderTable() {
    // let newHTML = '';
    // for(let i=0;i<this.data.length;i++) {
    //   let row = '<tr>';
    //   for(let c in this.data[i]) {
    //     row += `<td>${this.data[i][c]}</td>`;
    //   }
    //   row += '</tr>';
    //   newHTML += row;
    // }
    // this.tbody.innerHTML = newHTML;
  }
  
  sortCol(e,i) {
    // let sortToggle = 1;
    // if(this.lastSort === i) {
    //   this.sortAsc = !this.sortAsc;
    //   if(!this.sortAsc) sortToggle = -1;
    // } else this.sortAsc = true;
    
    // this.lastSort = i;
    
    // this.data.sort((a,b) => {
    //   if(a[i] < b[i]) return -1 * sortToggle;
    //   if(a[i] > b[i]) return 1 * sortToggle;
    //   return 0;
    // });
    
    // this.renderTable();
  }
}

if (!customElements.get('sortable-table')) {
	customElements.define('sortable-table', SortableTable);
}
</script>