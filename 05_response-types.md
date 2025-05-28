# Response Types

### Paged Response

A paged response is returned when a request returns a list or a collection of items. The response object has two properties: `paging` and `items`. The `items` property is an array. The `paging` object has three properties:

* limit () - Specifies the max number of items returned. `items.length` will not exceed `limit` but `limit` may exceed `items.length` based on `offset` and `total`
* offset () - Specifies the first item in the collection that should be return. 0-based.
* total () - Specifies the total number of items in the collection, though a subset may be returned in items based on `limit` and `offset`

Any request that returns a paged response accepts the following argument in addition to `limit` and `offset`

* all () - Whether or not to include all items

Any request for a component may be sorted by almost any column by passing a column criteria object to the below property

* columnCriteria () - The object containing the columns to sort by.

Example Column Criteria Request:

$.get("<https://apiserver/accounts?lastName=Smith&addressPostalCode=75080&columnCriteria[columnSorts][0][column]=address.city&columnCriteria[columnSorts][0][sortOrder]=D")>;

### Error Response - General

An error response is returned when a request was unable to be fulfilled. The response object has a `message` property which is a string that contains a message detailing the error.

### Error Response - Validation

An error reponse for validation purposes contains a `message` property as well as a `messagesByField` property. This is a map that contains field names and error message strings for any field in the request that was invalid.