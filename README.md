# PagedList
Javascript PagedList component for easily creating paginated lists in the browser.

PagedList is a javascript library to create html lists (or tables) with pagination and auto rendering features. Columns and buttons can be configured.

Columns are configurable to enable sorting and filtering. Buttons are default shown for each row, but can be configured to be visible dependent on row data. Callback functions can be applied on buttons. The row data will be passed to the callback function when a button is clicked.

The list gets refreshed automatically when the user changes sorting or filtering (or browse to an other page). Refreshing can also be done manually by calling `myList.refresh()`. Debouncing will prevent too many refreshes.

Columns can be configured to expand and collapse, which inserts and deletes an html-element below the clicked row. Refreshing will keep expanded items intact.

The data source can be server-side or client-side. This also means filtering, sorting (and paging) will be done server- or client-side. For server-side you need to implement it yourself. For client-side this library will take care.

Documentation as generated by Sphinx (<http://www.sphinx-doc.org/en/stable/>) can be found by downloading folder <b>docs\sphinx\_build\html\ </b> and opening <b> pagedListDoc.html </b>

This library is generated from Python using Transcrypt <https://www.transcrypt.org/>

How it looks
================
The styling is fully customizable, but with some defaults it will look like:

![alt text](https://raw.githubusercontent.com/pjbonestroo/pagedList/master/docs/sphinx/_build/html/_images/example.png)

Installation
============
Add dependencies to your html file:
- jQuery (required) <https://jquery.com/>
- Bootstrap (optional) <http://getbootstrap.com/>

Add `pagedList.min.js` or `pagedList.js` to your html file, like:
`<script src="pagedList.min.js"></script>`
The Javascript files can be found in the `python/__javascript__/` folder.

Code examples
=============
Add a new list to an existing html element with `id=myListId`, using `PagedList`:
```
var myList = new pagedList.PagedList("#myListId", "http://myURL/getListItems");
```
Add a column with sorting and filtering capabilities, using `addColumn`:
```
var column_one = myList.addColumn("Name", "Name")
     .enableFilter()
     .enableSort();
```
Define how the column content will be rendered, based on the row data, using `itemToHtml` (alternatively use `itemToElement`):
```
column_one.itemToHtml(function (item) {
     return "<div>" + item.Name + "</div>";
});
```
Add a button to the list, including style classes, which will be visible dependent on row data, using `addButton`:
```
myList.addButton("Edit", "Edit", "btn btn-primary btn-xs")
     .onclick(function (item) {
         console.log("Todo: edit item");
     }).showIf(function (item) {
         return item.CanEdit == true;
     });
```
For more examples, download the standalone example page (docs/example), which shows a PagedList with data from a fake server.

For the full API, download the Sphinx documentation as described above.
