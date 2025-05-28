# Inventory Management

### Advanced Purchase Orders

#### Create an advanced purchase order

```
DEFINITION
POST http://apiserver/advancedpurchaseorders

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders", {
    expectedDate: "2015-01-01",
    note: "Advanced PO Notes...",
    advancedPONumber: "PO1",
    vendor: "VNDR",
    warehouse: "WRHSE"
});

EXAMPLE RESPONSE
{
    expectedDate: "2015-01-01",
    externalId: null,
    id: 20,
    advancedPONumber: "PO1",
    note: "Advanced PO Notes...",
    status: "O",
    vendor: "VNDR",
    vendorDescription: "Vendor",
    warehouse: "WRHSE",
    warehouseDescription: "Warehouse"
}

```

Creates a new advanced purchase order.

##### Arguments

* advancedPONumber (required) - The unique advanced purchase order number that is part of the advanced purchase order.
* warehouse (required) - The warehouse code that is part of the advanced purchase order.
* vendor (required) - The vendor id that is part of the advanced purchase order.
* expectedDate (optional) - The expected date that is part of the advanced purchase order. If not specified, today's date will be used.
* note (optional) - The note that is part of the advanced purchase order.

##### Returns

Returns an advanced purchase order object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an advanced purchase order

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/20");

EXAMPLE RESPONSE
{
    expectedDate: "2015-01-01",
    externalId: null,
    id: 20,
    advancedPONumber: "PO1",
    note: "Advanced PO Notes...",
    status: "O",
    vendor: "VNDR",
    vendorDescription: "Vendor",
    warehouse: "WRHSE",
    warehouseDescription: "Warehouse"
}

```

Retrieves the details of an existing advanced purchase order. You need only supply the id.

##### Arguments

* id (required) - The record id of the advanced purchase order to be retrieved.

#### Update an advanced purchase order

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/20", {
    vendor: "VNDR"
});

EXAMPLE RESPONSE
{
    expectedDate: "2015-01-01",
    externalId: null,
    id: 20,
    advancedPONumber: "PO1",
    note: "Advanced PO Notes...",
    status: "O",
    vendor: "VNDR",
    vendorDescription: "Vendor",
    warehouse: "WRHSE",
    warehouseDescription: "Warehouse"
}


```

Updates the specified advanced purchase order by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* advancedPONumber (optional) - The unique advanced purchase order number that is part of the advanced purchase order.
* warehouse (optional) - The warehouse code that is part of the advanced purchase order.
* vendor (optional) - The vendor id that is part of the advanced purchase order.
* expectedDate (optional) - The expected date that is part of the advanced purchase order.
* note (optional) - The note that is part of the advanced purchase order.

##### Returns

Returns the advanced purchase order object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an advanced purchase order

```
DEFINITION
DELETE http://apiserver/advancedpurchaseorders/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedpurchaseorders/20", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an advanced purchase order. It cannot be undone.

##### Arguments

* id (required) - The record id of the advanced purchase order to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the advanced purchase order does not exist, this call returns an error.

#### List all advanced purahase orders

```
DEFINITION
GET http://apiserver/advancedpurchaseorders

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            expectedDate: "2015-01-01",
            externalId: null,
            id: 20,
            advancedPONumber: "PO1",
            note: "Advanced PO Notes...",
            status: "O",
            vendor: "VNDR",
            vendorDescription: "Vendor",
            warehouse: "WRHSE",
            warehouseDescription: "Warehouse"
        },
        {...},
    ]
}

```

Returns a list of all advanced purahase orders.

##### Arguments

* advancedPONumber (optional) - The unique advanced purchase order number that is part of the advanced purchase order.
* warehouse (optional) - The warehouse code that is part of the advanced purchase order.
* vendor (optional) - The vendor id that is part of the advanced purchase order.
* note (optional) - The note that is part of the advanced purchase order.
* externalId (optional) - The external id that is part of the advanced purchase order.

##### Returns

A dictionary with an items property that contains an array of up to limit advanced purahase orders, starting at index offset. Each entry in the array is a separate advanced purchase order object. If no more advanced purahase orders are available, the resulting array will be empty. This request should never return an error.

#### Receive inventory for the advanced purchase order

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/receiving

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/20/receiving", {
    "comment": "Receiving comment...",
    "date": "2015-01-01",
    "reason": "RSN",
    "warehouse": "WRHSE",
    "closePurchaseOrder": true,
    "transactions": [
        {
            "advancedPORecordId": 20,
            "cost": 5,
            "location": "L1",
            "product": "PROD001",
            "quantity": 10,
        }
        {...}
    ]
});

EXAMPLE RESPONSE
204 No Content


```

This action creates inventory transactions for the products in the advanced purchase order.

##### Arguments

* warehouse (required) - The warehouse code that is part of the inventory transactions.
* date (optional) - The date of the inventory transactions. If not specified, today's date will be used.
* reason (optional) - The reason code of the inventory transaction. Must be a defined reason code value.
* comment (optional) - A comment for the inventory transaction.
* transactions (required) - A list of inventory transaction details.
  + advancedPORecordId (required) - The record id for the parent advanced purchase order.
  + cost (required) - The unit cost of the inventory transaction.
  + location (required) - The location code that is part of the inventory transaction.
  + product (required) - The product code that is part of the inventory transaction.
  + quantity (required) - The quantity of the inventory transaction. This number cannot be 0.

##### Returns

Returns a 204 No Content on success.

#### Post purchase requisition to the accounting system

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/purchaserequisition

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/5204/purchaserequisition");

EXAMPLE RESPONSE
200 OK


```

This action creates a Purchase Requisition in the integrated accounting system. (Note, not all of the integrated accounting systems support this action.)

##### Returns

Returns a 200 OK response on success.

### Advanced Purchase Order Products

#### Create an advanced purchase order product

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/products

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/20/products", {
    "expectedDate": "2015-01-01",
    "expectedQuantity": 50,
    "note": "Product note...",
    "price": 5,
    "product": "PROD001",
    "warehouse": "10"
});

EXAMPLE RESPONSE
{
    "advancedPORecordId": 20,
    "expectedDate": "2015-01-01",
    "expectedQuantity": 50,
    "id": "1058",
    "note": "Product note...",
    "price": 5,
    "product": "PROD001",
    "productDescription": "Product 1",
    "receivedQuantity": 0,
    "status": "C",
    "vendor": null,
    "vendorDescription": null,
    "warehouse": "WRHSE",
    "warehouseDescription": "Warehouse"
}

```

Creates a new advanced purchase order product.

##### Arguments

* warehouse (required) - The warehouse of the advanced purchase order product.
* product (required) - The product of the advanced purchase order product.
* expectedQuantity (required) - The expected number of products in the advanced purchase order product.
* price (required) - The price of the product in the advanced purchase order product.
* note (optional) - A note to put on the advanced purchase order product
* expectedDate (optional) - The expected date of the advanced purchase order product. If not provided, will be set to current date.

##### Returns

Returns an advanced purchase order product object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an advanced purchase order product

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/products/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/20/products/1058");

EXAMPLE RESPONSE
{
    "advancedPORecordId": 20,
    "expectedDate": "2015-01-01",
    "expectedQuantity": 50,
    "id": "1058",
    "note": "Product note...",
    "price": 5,
    "product": "PROD001",
    "productDescription": "Product 1",
    "receivedQuantity": 0,
    "status": "C",
    "vendor": null,
    "vendorDescription": null,
    "warehouse": "WRHSE",
    "warehouseDescription": "Warehouse"
}

```

Retrieves the details of an existing advanced purchase order product. You need only supply the id.

##### Arguments

* id (required) - The id of the advanced purchase order product to be retrieved.

#### Update an advanced purchase order product

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/products/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/20/products/1058", {
    "expectedQuantity": 150
    "price": 20
});

EXAMPLE RESPONSE
{
    "advancedPORecordId": 20,
    "expectedDate": "2015-01-01",
    "expectedQuantity": 150,
    "id": "1058",
    "note": "Product note...",
    "price": 20,
    "product": "PROD001",
    "productDescription": "Product 1",
    "receivedQuantity": 0,
    "status": "C",
    "vendor": null,
    "vendorDescription": null,
    "warehouse": "WRHSE",
    "warehouseDescription": "Warehouse"
}


```

Updates the specified advanced purchase order product by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* warehouse (optional) - The warehouse of the advanced purchase order product.
* product (optional) - The product of the advanced purchase order product.
* expectedQuantity (optional) - The expected number of products in the advanced purchase order product.
* price (optional) - The price of the product in the advanced purchase order product.
* note (optional) - A note to put on the advanced purchase order product
* expectedDate (optional) - The expected date of the advanced purchase order product.

##### Returns

Returns the advanced purchase order product object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an advanced purchase order

```
DEFINITION
DELETE http://apiserver/advancedpurchaseorders/:id/products/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedpurchaseorders/20/products/1058", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an advanced purchase order. It cannot be undone.

##### Arguments

* id (required) - The id of the advanced purchase order to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the advanced purchase order does not exist, this call returns an error.

#### List all advanced purchase order products

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/products

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/:id/products?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "advancedPORecordId": 20,
            "expectedDate": "2015-01-01",
            "expectedQuantity": 150,
            "id": "1058",
            "note": "Product note...",
            "price": 20,
            "product": "PROD001",
            "productDescription": "Product 1",
            "receivedQuantity": 0,
            "status": "C",
            "vendor": null,
            "vendorDescription": null,
            "warehouse": "WRHSE",
            "warehouseDescription": "Warehouse"
        },
        {...},
    ]
}

```

Returns a list of all advanced purchase order products.

##### Arguments

* id (optional) - Filter list by the purchase order id
* product (optional) - Filter list by partial match of product.
* warehouse (optional) - Filter list by partial match of warehouse.
* status (optional) - Filter list by the status.

##### Returns

A dictionary with an items property that contains an array of up to limit advanced purchase order products, starting at index offset. Each entry in the array is a separate advanced purchase order object. If no more advanced purchase order products are available, the resulting array will be empty. This request should never return an error.

### Advanced Purchase Order Attachments

#### Create an advanced purchase order attachment

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/attachments", {
    "type":"OTHER",
    "typeDescription":"Other",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new advanced purchase order attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns an advanced purchase order attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve an advanced purchase order attachment

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/attachments/117");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing advanced purchase order attachment. You need only supply the advanced purchase order attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns an advanced purchase order attachment object if a valid id was provided.

#### Update an advanced purchase order attachment

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/attachments/117", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified advanced purchase order attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the advanced purchase order attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined advanced purchase order attachment type code).

#### Delete an advanced purchase order attachment

```
DEFINITION
DELETE http://apiserver/advancedpurchaseorders/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedpurchaseorders/10/attachments/117", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an advanced purchase order attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the advanced purchase order attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the advanced purchase order attachment id does not exist, this call returns an error.

#### List all advanced purchase order attachments

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
                "longComment": "long comment text",
                "dateCreated": "2018-03-12",
                "id": "117",
                "type": "LOGO",
                "typeDescription": "Logo",
                "url": null,
                "fileName": "logo64.png",
                "file": null,
                "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all advanced purchase order attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit advanced purchase order attachments, starting at index offset. Each entry in the array is a separate advanced purchase order attachment object. If no more advanced purchase order attachments are available, the resulting array will be empty. This request should never return an error.

### Advanced Purchase Order Codes

#### Create an advanced purchase order code

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/codes", {
    "type": "APOCODE1",
    "value": "VAL1"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APOCODE1",
    "typeDescription": "APO Code 1",
    "value": "VAL1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Creates a new advanced purchase order code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an advanced purchase order code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an advanced purchase order code

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/codes");

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APOCODE1",
    "typeDescription": "APO Code 1",
    "value": "VAL1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Retrieves the details of an existing advanced purchase order code. You need only supply the advanced purchase order code id.

##### Arguments

* id (required) - The id of the advanced purchase order code to be retrieved.

##### Returns

Returns an advanced purchase order code object if a valid id was provided.

#### Update an advanced purchase order code

```
DEFINITION
POST http://apiserver/advancedpurchaseorder/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorder/10/codes/8096", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APOCODE1",
    "typeDescription": "APO Code 1",
    "value": "VAL1",
    "valueDescription": "Value 1",
    "isActive": false
}


```

Updates the specified advanced purchase order by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the advanced purchase order code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an advanced purchase order code

```
DEFINITION
DELETE http://apiserver/advancedpurchaseorders/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedpurchaseorders/10/codes/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an advanced purchase order code. It cannot be undone.

##### Arguments

* id (required) - The id of the advanced purchase order code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the advanced purchase order code does not exist, this call returns an error.

#### List all advanced purchase order codes

```
DEFINITION
GET http://apiserver/advancedpurchaseorder/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorder/10/codes?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "8096",
            "type": "APOCODE1",
            "typeDescription": "APO Code 1",
            "value": "VAL1",
            "valueDescription": "Value 1",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all advanced purchase order codes.

##### Returns

A dictionary with an items property that contains an array of up to limit advanced purchase order codes, starting at index offset. Each entry in the array is a separate advanced purchase order code object. If no more advanced purchase order codes are available, the resulting array will be empty. This request should never return an error.

### Advanced Purchase Order Dates

#### Create an advanced purchase order date

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/dates", {
    "type": "APODATE1",
    "value": "2015-01-01"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APODATE1",
    "typeDescription": "APO Date 1",
    "value": "2015-01-01",
    "isActive": true
}

```

Creates a new advanced purchase order date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an advanced purchase order date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an advanced purchase order date

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/dates");

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APODATE1",
    "typeDescription": "APO Date 1",
    "value": "2015-01-01",
    "isActive": true
}

```

Retrieves the details of an existing advanced purchase order date. You need only supply the advanced purchase order date id.

##### Arguments

* id (required) - The id of the advanced purchase order date to be retrieved.

##### Returns

Returns an advanced purchase order date object if a valid id was provided.

#### Update an advanced purchase order date

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/dates/8096", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APODATE1",
    "typeDescription": "APO Date 1",
    "value": "2015-01-01",
    "isActive": false
}


```

Updates the specified advanced purchase order by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the advanced purchase order date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an advanced purchase order date

```
DEFINITION
DELETE http://apiserver/advancedpurchaseorders/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedpurchaseorders/10/dates/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an advanced purchase order date. It cannot be undone.

##### Arguments

* id (required) - The id of the advanced purchase order date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the advanced purchase order date does not exist, this call returns an error.

#### List all advanced purchase order dates

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/dates?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "8096",
            "type": "APODATE1",
            "typeDescription": "APO Date 1",
            "value": "2015-01-01",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all advanced purchase order dates.

##### Returns

A dictionary with an items property that contains an array of up to limit advanced purchase order dates, starting at index offset. Each entry in the array is a separate advanced purchase order date object. If no more advanced purchase order dates are available, the resulting array will be empty. This request should never return an error.

### Advanced Purchase Order Notes

#### Create an advanced purchase order note

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/notes", {
    "type": "APODESC",
    "shortComment": "Buy More Paper"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APODESC",
    "typeDescription": "APO description"
    "shortComment": "Buy More Paper",
    "longComment": null
}

```

Creates a new advanced purchase order note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns an advanced purchase order note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve an advanced purchase order note

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/notes/8096");

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APODESC",
    "typeDescription": "APO description"
    "shortComment": "Buy More Paper",
    "longComment": null
}

```

Retrieves the details of an existing advanced purchase order note. You need only supply the advanced purchase order note id.

##### Arguments

* id (required) - The id of the advanced purchase order note to retrieve.

##### Returns

Returns an advanced purchase order note object if a valid id was provided.

#### Update an advanced purchase order note

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/notes/8096", {
    "shortComment": null,
    "longComment": "Buy More Paper"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APODESC",
    "typeDescription": "APO description"
    "shortComment": null,
    "longComment": "Buy More Paper"
}


```

Updates the specified advanced purchase order note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the advanced purchase order note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete an advanced purchase order note

```
DEFINITION
DELETE http://apiserver/advancedpurchaseorders/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedpurchaseorders/10/notes/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an advanced purchase order note. It cannot be undone.

##### Arguments

* id (required) - The id of the advanced purchase order note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the advanced purchase order note id does not exist, this call returns an error.

#### List all advanced purchase order notes

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "8096",
            "type": "APODESC",
            "typeDescription": "APO description"
            "shortComment": null,
            "longComment": "Buy More Paper"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all advanced purchase order notes.

##### Returns

A dictionary with an items property that contains an array of up to limit advanced purchase order notes, starting at index offset. Each entry in the array is a separate advanced purchase order note object. If no more advanced purchase order notes are available, the resulting array will be empty. This request should never return an error.

### Advanced Purchase Order Numbers

#### Create an advanced purchase order number

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/numbers", {
    "type": "APONUMS1",
    "value": 123
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APONUMS1",
    "typeDescription": "APO Numbers 1",
    "value": 123,
    "isActive": true
}

```

Creates a new advanced purchase order number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an advanced purchase order number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an advanced purchase order number

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/numbers");

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APONUMS1",
    "typeDescription": "APO Numbers 1",
    "value": 123,
    "isActive": true
}

```

Retrieves the details of an existing advanced purchase order number. You need only supply the advanced purchase order number id.

##### Arguments

* id (required) - The id of the advanced purchase order number to be retrieved.

##### Returns

Returns an advanced purchase order number object if a valid id was provided.

#### Update an advanced purchase order number

```
DEFINITION
POST http://apiserver/advancedpurchaseorders/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedpurchaseorders/10/numbers/8096", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "APONUMS1",
    "typeDescription": "APO Numbers 1",
    "value": 123,
    "isActive": false
}


```

Updates the specified advanced purchase order by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the advanced purchase order number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an advanced purchase order number

```
DEFINITION
DELETE http://apiserver/advancedpurchaseordernumbers/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedpurchaseordernumbers/10/numbers/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an advanced purchase order number. It cannot be undone.

##### Arguments

* id (required) - The id of the advanced purchase order number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the advanced purchase order number does not exist, this call returns an error.

#### List all advanced purchase order numbers

```
DEFINITION
GET http://apiserver/advancedpurchaseorders/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedpurchaseorders/10/numbers?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "8096",
            "type": "APONUMS1",
            "typeDescription": "APO Numbers 1",
            "value": 123,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all advanced purchase order numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit advanced purchase order numbers, starting at index offset. Each entry in the array is a separate advanced purchase order numbers object. If no more advanced purchase order numbers are available, the resulting array will be empty. This request should never return an error.

### Bulk Discounts

#### Create a bulk discount

```
DEFINITION
POST http://apiserver/bulkdiscounts

EXAMPLE REQUEST
$.post("http://localhost:49195/bulkdiscounts", {
    "name": "Retail Video Media",
    "priceCode": "RP",
    "productCode": null,
    "categoryCode": "VIDEOMEDIA",
    "startDate": "2019-08-01",
    "endDate": "2019-08-31"
});

EXAMPLE RESPONSE
{
    "id": "1234",
    "name": "Retail Video Media",
    "priceCode": "RP",
    "priceCodeDescription": "Retail Price",
    "productCode": null,
    "productDescription": null,
    "categoryCode": "VIDEOMEDIA",
    "categoryCodeDescription": "Video Media",
    "startDate": "2019-08-01",
    "endDate": "2019-08-31",
    "method": "PERCENT"
}

```

Creates a new bulk discount object.

##### Arguments

* name (required) - The name of the bulk discount.
* priceCode (required) - The product price code to which this bulk discount applies. Must be defined as a `DDCPRODPC` code value.
* productCode (see description) - The product code to which this bulk discount applies. Either productCode or categoryCode must be provided.
* categoryCode (see description) - The category to which this bulk discount applies. Must be defined as a `DISCNTCTGY` code value. Either productCode or categoryCode must be provided.
* startDate (required) - The first date that the bulk discount is active.
* endDate (see description) - The last date that the bulk discount is active. If not provided, the bulk discount will remain active.

##### Returns

Returns a bulk discount object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a bulk discount

```
DEFINITION
GET http://apiserver/bulkdiscounts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/bulkdiscounts/1234");

EXAMPLE RESPONSE
{
    "id": "1234",
    "name": "Retail Video Media",
    "priceCode": "RP",
    "priceCodeDescription": "Retail Price",
    "productCode": null,
    "productDescription": null,
    "categoryCode": "VIDEOMEDIA",
    "categoryCodeDescription": "Video Media",
    "startDate": "2019-08-01",
    "endDate": "2019-08-31",
    "method": "PERCENT"
}

```

Retrieves a bulk discount object.

##### Arguments

* id (required) - The id of the bulk discount to be retrieved.

##### Returns

Returns a bulk discount object if a valid id was provided.

#### Update a bulk discount

```
DEFINITION
POST http://apiserver/bulkdiscounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/bulkdiscounts/1234", {
    "name": "Employee Video Media",
    "priceCode": "EP"
});

EXAMPLE RESPONSE
{
    "id": "1234",
    "name": "Employee Video Media",
    "priceCode": "EP",
    "priceCodeDescription": "Employee Price",
    "productCode": null,
    "productDescription": null,
    "categoryCode": "VIDEOMEDIA",
    "categoryCodeDescription": "Video Media",
    "startDate": "2019-08-01",
    "endDate": "2019-08-31",
    "method": "PERCENT"
}

```

Updates the specified bulk discount by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name (optional) - The name of the bulk discount.
* priceCode (optional) - The product price code to which this bulk discount applies. Must be defined as a `DDCPRODPC` code value.
* productCode (optional) - The product code to which this bulk discount applies.
* categoryCode (optional) - The category to which this bulk discount applies. Must be defined as a `DISCNTCTGY` code value.
* startDate (optional) - The first date that the bulk discount is active.
* endDate (optional) - The last date that the bulk discount is active. If not provided, the bulk discount will remain active.

##### Returns

Returns the bulk discount object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a bulk discount

```
DEFINITION
DELETE http://apiserver/bulkdiscounts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/bulkdiscounts/1234", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a bulk discount. It cannot be undone.

##### Arguments

* id (required) - The id of the bulk discount to be deleted.

##### Returns

Returns a 204 No Content response on success. If the bulk discount id does not exist, this call returns an error.

#### List all bulk discounts

```
DEFINITION
GET http://apiserver/bulkdiscounts

EXAMPLE REQUEST
$.get("http://localhost:49195/bulkdiscounts?priceCode=RP");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 479
    }
    "items": [
        {
            "id": "1234",
            "name": "Retail Video Media",
            "priceCode": "RP",
            "priceCodeDescription": "Retail Price",
            "productCode": null,
            "productDescription": null,
            "categoryCode": "VIDEOMEDIA",
            "categoryCodeDescription": "Video Media",
            "startDate": "2019-08-01",
            "endDate": "2019-08-31",
            "method": "PERCENT"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all products matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* name (optional) - Filter list by partial match in bulk discount name
* priceCode (optional) - Filter list by partial match in product price code
* productCode (optional) - Filter list by partial match in product code
* categoryCode (optional) - Filter list by partial match in category
* activeDate (optional) - Filter list down to results where the date provided falls on or between the bulk discount's start and end dates.

##### Returns

A dictionary with an items property that contains an array of up to limit bulk discounts, starting at index offset. Each entry in the array is a separate bulk discount object. If no more bulk discounts are available, the resulting array will be empty. This request should never return an error.

#### Copy a bulk discount

```
DEFINITION
POST http://apiserver/bulkdiscounts/:id/copy

EXAMPLE REQUEST
$.post("http://localhost:49195/bulkdiscounts/1234/copy", {
    "name": "Retail Video Media",
    "priceCode": "RP",
    "categoryCode": "VIDEOMEDIA",
    "startDate": "2019-09-01",
    "endDate": "2019-09-30"
});

EXAMPLE RESPONSE
{
    "id": "4321",
    "name": "Retail Video Media",
    "priceCode": "RP",
    "priceCodeDescription": "Retail Price",
    "productCode": null,
    "productDescription": null,
    "categoryCode": "VIDEOMEDIA",
    "categoryCodeDescription": "Video Media",
    "startDate": "2019-09-01",
    "endDate": "2019-09-30",
    "method": "PERCENT"
}

```

Copies the bulk discount structure of the `id` provided and creates a new bulk discount object. The tiers of the existing bulk discount will be copied and applied to the new bulk discount. In this example, the bulk discount with `id: 1234` will remain unchanged. A new bulk discount `"id": "4321"` will be created using the specified parameters.

##### Arguments

* name (required) - The name of the new bulk discount.
* priceCode (required) - The product price code to which the new bulk discount applies. Must be defined as a `DDCPRODPC` code value.
* productCode (see description) - The product to which the new bulk discount applies. Either productCode or categoryCode must be provided.
* categoryCode (see description) - The category to which the new bulk discount applies. Must be defined as a `DISCNTCTGY` code value. Either productCode or categoryCode must be provided.
* startDate (required) - The first date that the new bulk discount is active.
* endDate (see description) - The last date that the new bulk discount is active. If not provided, the bulk discount will remain active.

##### Returns

Returns the newly copied bulk discount object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an applicable bulk discount structure

```
DEFINITION
GET http://apiserver/bulkdiscounts?isApplicable=true

EXAMPLE REQUEST
$.get("http://localhost:49195/bulkdiscounts?isApplicable=true&priceCode=RP&productCode=BK-5SLVG&categoryCode=VIDEOMEDIA");

EXAMPLE RESPONSE
{
    "bulkDiscount" :{
        "id": "1234",
        "name": "Retail Video Media",
        "priceCode": "RP",
        "priceCodeDescription": "Retail Price",
        "productCode": null,
        "productDescription": null,
        "categoryCode": "VIDEOMEDIA",
        "categoryCodeDescription": "Video Media",
        "startDate": "2019-08-01",
        "endDate": "2019-08-31",
        "method": "PERCENT"
    }
    "tiers": [
        {
            "id": "2312",
            "bulkDiscountId": "1234",
            "minimumQuantity": 10,
            "discount": 5.0000
        },
        {
            "id": "2313",
            "bulkDiscountId": "1234",
            "minimumQuantity": 30,
            "discount": 10.0000
        },
        {...},
        {...}
    ]
}

```

Returns the single currently applicable bulk discount structure (the bulk discount and all its tiers) for the provided product price code, product code, and category code. Product type bulk discounts will be given priority over category type bulk discounts. If multiple bulk discounts are active on the same day, the one with the most recent `startDate` will be selected.

##### Arguments

* priceCode (required) - The product price code to filter by.
* productCode (required) - The product code to filter by.
* categoryCode (optional) - The category code to filter by.

##### Returns

The single currently applicable bulk discount structure, and an array of all its tiers. If there is no applicable bulk discount, the results will be empty. If a bulk discount has no tiers, the resulting tiers array will be empty.

### Bulk Discount Pricing Tiers

#### Create a bulk discount tier

```
DEFINITION
POST http://apiserver/bulkdiscounts/:id/tiers

EXAMPLE REQUEST
$.post("http://localhost:49195/bulkdiscounts/1234/tiers", {
    "minimumQuantity": 10,
    "discount": 5
});

EXAMPLE RESPONSE
{
    "id": "2312",
    "bulkDiscountId": "1234",
    "minimumQuantity": 10,
    "discount": 5.0000
}

```

Creates a new bulk discount tier object.

##### Arguments

* minimumQuantity (required) - The quantity at which this tier will become active.
* discount (required) - The value to be applied as a discount

##### Returns

Returns a bulk discount tier object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a bulk discount tier

```
DEFINITION
GET http://apiserver/bulkdiscounts/:id/tiers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/bulkdiscounts/1234/tiers/2312");

EXAMPLE RESPONSE
{
    "id": "2312",
    "bulkDiscountId": "1234",
    "minimumQuantity": 10,
    "discount": 5.0000
}

```

Retrieves a bulk discount tier object.

##### Arguments

* id (required) - The id of the bulk discount tier to be retrieved.

##### Returns

Returns a bulk discount tier object if a valid id was provided.

#### Update a bulk discount tier

```
DEFINITION
POST http://apiserver/bulkdiscounts/:id/tiers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/bulkdiscounts/1234/tiers/2312", {
    "discount": 10
});

EXAMPLE RESPONSE
{
    "id": "2312",
    "bulkDiscountId": "1234",
    "minimumQuantity": 10,
    "discount": 10.0000
}

```

Updates the specified bulk discount tier by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* minimumQuantity (optional) - The quantity at which this tier will become active.
* discount (optional) - The value to be applied as a discount

##### Returns

Returns the bulk discount tier object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a bulk discount tier

```
DEFINITION
DELETE http://apiserver/bulkdiscounts/:id/tiers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/bulkdiscounts/1234/tiers/2312", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a bulk discount tier. It cannot be undone.

##### Arguments

* id (required) - The id of the bulk discount tier to be deleted.

##### Returns

Returns a 204 No Content response on success. If the bulk discount tier id does not exist, this call returns an error.

#### List all bulk discount tiers

```
DEFINITION
GET http://apiserver/bulkdiscounts/:id/tiers

EXAMPLE REQUEST
$.get("http://localhost:49195/bulkdiscounts/1234/tiers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 479
    }
    "items": [
        {
            "id": "2312",
            "bulkDiscountId": "1234",
            "minimumQuantity": 10,
            "discount": 5.0000
        },
        {
            "id": "2313",
            "bulkDiscountId": "1234",
            "minimumQuantity": 30,
            "discount": 10.0000
        },
        {...},
        {...}
    ]
}

```

Returns a list of all bulk discount tiers.

##### Returns

A dictionary with an items property that contains an array of up to limit bulk discount tiers, starting at index offset. Each entry in the array is a separate bulk discount tier object. If no more bulk discount tiers are available, the resulting array will be empty. This request should never return an error.

### Inventory Transactions

#### Create an inventory transaction

```
DEFINITION
POST http://apiserver/inventorytransactions

EXAMPLE REQUEST
$.post("http://localhost:49195/inventorytransactions", {
    "type": "T",
    "product": "BK-5SLVG",
    "warehouse": "UKWH",
    "location": "BIN1",
    "quantity": 15,
    "fromWarehouse": "UKWH",
    "fromLocation": "BIN2"
});

EXAMPLE RESPONSE
{
    transaction: {
        "id": "21346",
        "type": "T",
        "product": "BK-5SLVG",
        "productDescription": "",
        "warehouse": "UKWH",
        "warehouseDescription": "",
        "location": "BIN2",
        "quantity": 15,
        "date": "2013-10-07",
        "cost": 0,
        "reason": null,
        "reasonDescription": null,
        "comment": null
    },
    fromTransaction {
        "id": "21345",
        "type": "T",
        "product": "BK-5SLVG",
        "productDescription": "",
        "warehouse": "UKWH",
        "warehouseDescription": "",
        "location": "BIN1",
        "quantity": -15,
        "date": "2013-10-07",
        "cost": 0,
        "reason": null,
        "reasonDescription": null,
        "comment": null,
        "status": "Y",
        "journalReference": null
    }
}

```

Creates a new inventory transaction object(s).

##### Arguments

* type (required) - The type of the inventory transaction. Must by an [inventory transaction type](#inventory-transaction-type) value.
* product (required) - The product code that is part of the inventory transaction.
* warehouse (required) - The warehouse code that is part of the inventory transaction.
* location (required) - The location code that is part of the inventory transaction.
* quantity (required) - The quantity of the inventory transaction. This number cannot be 0. Except for adjustment type (where quantity can be negative or positive) the quantity must be positive.
* date (optional) - The date of the inventory transaction. If not specified, today's date will be used.
* cost (optional) - The unit cost of the inventory transaction. If not specified, the current product warehouse cost will be used.
* reason (optional) - The reason code of the inventory transaction. Must be a defined reason code value.
* comment (optional) - A comment for the inventory transaction.
* fromWarehouse (optional - only used when type is `T`, then optional) - The warehouse code for the balancing transaction that will be created. If not specified, the transfer will occur between two locations in the same warehouse.
* fromLocation (optional - only used when type is `T`, then required) - The location code for the balancing transaction that will be created.
* purchaseOrder (optional - only used when type is `R`, then optional) - The purchase order for the receiving transaction.
* closePurchaseOrder (optional - only used when type is `R`, then optional) - Whether or not to close the purchase order if the quantity in the inventory transaction does not fully satisfy the purchase order. By default, the purchase order will not be closed.

##### Returns

Returns an object that contains 1 or 2 inventory transaction objects if the call succeeded. If the type is `T`, both transaction and fromTransaction will be set in the returning object. Otherwise, only transaction will be set. Returns an error if create parameters are invalid (e.g. specifying an invalid inventory transaction type or failing to specify a warehouse).

#### Retrieve an inventory transaction

```
DEFINITION
GET http://apiserver/inventorytransactions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/inventorytransactions/21346");

EXAMPLE RESPONSE
{
    "id": "21346",
    "type": "T",
    "product": "BK-5SLVG",
    "productDescription": "",
    "warehouse": "UKWH",
    "warehouseDescription": "",
    "location": "BIN2",
    "quantity": 15,
    "date": "2013-10-07",
    "cost": 0,
    "reason": null,
    "reasonDescription": null,
    "comment": null,
    "status": "Y",
    "journalReference": null
}

```

Retrieves the details of an existing inventory transaction. You need only supply the inventory transaction id.

##### Returns

Returns an inventory transaction object if a valid id was provided.

#### List all inventory transactions

```
DEFINITION
GET http://apiserver/inventorytransactions

EXAMPLE REQUEST
$.get("http://localhost:49195/inventorytransactions?type=T");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 51
    },
    "items": [
        {
            "id": "21346",
            "type": "T",
            "product": "BK-5SLVG",
            "productDescription": "5 Steps to Living (Set)",
            "warehouse": "UKWH",
            "warehouseDescription": "Fulfillment Center",
            "location": "BIN2",
            "quantity": 15,
            "date": "2013-10-07",
            "cost": 0,
            "reason": null,
            "reasonDescription": null,
            "comment": null,
            "shippingGroupId": null,
            "status": "Y",
            "journalReference": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all inventory transactions matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id - Filter list by the unique inventory transaction id (will only return a single transaction)
* product - Filter list by partial match in product code
* warehouse - Filter list by partial match in warehouse code
* location - Filter list by partial match in location code
* reason - Filter list by partial match in reason code
* comment - Filter list by partial match in comment
* startDate - Filter list by date on or after the specified value
* endDate - Filter list by date on or before the specified value
* type - Filter list by partial match of type code
* exactProduct - Filters list by exact product code match. This should not be used with any other arguments
* status - Filters list by exact match on status.
* journalReference - Filters list by journal reference.

  ##### Returns

A dictionary with an items property that contains an array of up to limit inventory transactions, starting at index offset. Each entry in the array is a separate inventory transaction object. If no more inventory transactions are available, the resulting array will be empty. This request should never return an error.

#### Inventory transaction type

* R () - Receiving
* S () - Shipping
* A () - Adjusting
* T () - Transferring

### Inventory Transaction Cost Adjustment

```
DEFINITION
POST http://apiserver/inventorytransactions/:id/costadjustment

EXAMPLE REQUEST
$.post("http://localhost:49195/inventorytransactions/21346/costadjustment", {
        "newCost": 15.24
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* newCost (required) - The new cost for the inventory transaction

##### Returns

Returns a 204 No Content response on success. If there is an error, either a 400 or 500 will be returned.

### Inventory transactions post journal entries

```
DEFINITION
POST http://apiserver/inventorytransactions/post

EXAMPLE REQUEST
$.post("http://localhost:49195/inventorytransactions/post", {
    "start": "2017-09-01",
    "end": "2017-09-07",
    "warehouse":  null,
    "transactionType": null
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* start (required) - specifies the start of the date range for selecting inventory transactions to post
* end (required) - specifies the end of the date range for selecting inventory transactions to post
* warehouse (optional) - filters inventory transactions by warehouse
* transactionType (optional) - filters inventory transactions by types

##### Returns

Returns a 204 No Content response on success. If there is an error, either a 400 or 500 will be returned.

### Order Quick Picks

Order Quick Picks is intended for use in order entry. Order Quick Picks is a list of Source Offerings as defined on the Source and Product Quick Picks as defined in Inventory Management.

#### List all order quick picks

```
DEFINITION
GET http://apiserver/orderquickpicks

EXAMPLE REQUEST
$.get("http://localhost:49195/orderquickpicks?warehouse=10&company=5&currency=USD&priceCode=RP&source=072711");

EXAMPLE RESULT
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "1142CD",
            "description": "Authority in the Church, Part 1",
            "priceCode": "EC",
            "price": 1,
            "availableQuantity": 0,
            "weight": 0,
            "onOrderQuantity": 59,
            "nextReceiveDate": "2013-08-25",
            "cost": 15.95,
            "type": "K",
            "typeDescription": "Kit"
        },
        { ... }
    ]
}

```

##### Arguments

* warehouse (required) - The warehouse code of the order quick pick
* company (required) - The company code for the order quick pick
* currency (required) - The currency code for the order quick pick
* priceCode (optional) - The price code of the order quick pick
* source (optional) - The source code for the order quick pick

##### Returns

Returns order quick picks.

### Products

#### Create a product

```
DEFINITION
POST http://apiserver/products

EXAMPLE REQUEST
$.post("http://localhost:49195/products", {
    "id": "BK-5SLVG",
    "description": "5 Steps to Living (Set)",
    "type": "K",
    "status": "A",
    "packaging": "P"
});

EXAMPLE RESPONSE
{
    "id": "BK-5SLVG",
    "description": "5 Steps to Living (Set)",
    "type": "K",
    "typeDescription": "Kit",
    "status": "A",
    "statusDescription": "Active",
    "packaging": "P",
    "packagingDescription": "Standard Packaged Product",
    "author": null,
    "isbn": null,
    "allowDiscount": true,
    "weight": null,
    "useInStudioOnline": false,
    "glClassCode": null,
    "glClassCodeDescription": null,
    "category": null,
    "categoryDescription": null,
    "discountCategory": null,
    "discountCategoryDescription": null
}

```

Creates a new product object.

##### Arguments

* id (required) - The product code.
* description (required) - The description of the product.
* type (required) - The type code of the product. Must be a valid [product type](#product-type) value.
* status (required) - The status code of the product. Must be a defined product status value.
* packaging (required) - The packaging code of the product. Must be a valid [product packaging](#product-packaging) value.
* author (optional) - The author of the product.
* isbn (optional) - The isbn of the product.
* allowDiscount (optional) - Whether or not a discount is allowed on the product. If not specified, will default to true.
* weight (optional) - The weight of the product.
* useInStudioOnline (optional) - Whether or not to use the product is Studio Online. If not specified, will default to false.
* glClassCode (optional) - Will set an initial GL Class code
* category (optional) - Will put the product in an initial category
* discountCategory (optional) - Will set an initial discount category. Must be defined as a `DISCNTCTGY` code value.

##### Returns

Returns a product object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid product type or an undefined product status).

#### Retrieve a product

```
DEFINITION
GET http://apiserver/products/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG");

EXAMPLE RESPONSE
{
    "id": "BK-5SLVG",
    "description": "5 Steps to Living (Set)",
    "author": null,
    "isbn": "5S33392011",
    "type": "K",
    "typeDescription": "Kit",
    "status": "A",
    "statusDescription": "Active",
    "packaging": "P",
    "packagingDescription": "Standard Packaged Product",
    "allowDiscount": true,
    "weight": 14,
    "useInStudioOnline": false,
    "glClassCode": null,
    "glClassCodeDescription": null,
    "category": null,
    "categoryDescription": null,
    "discountCategory": null,
    "discountCategoryDescription": null
}

```

Retrieves the details of an existing product. You need only supply the product code.

##### Arguments

* id (required) - The product code of the product to retrieve.

##### Returns

Returns a product object if a valid id was provided.

#### Update a product

```
DEFINITION
POST http://apiserver/products/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG", {
    "allowDiscount": false
});

EXAMPLE RESPONSE
{
    "id": "BK-5SLVG",
    "description": "5 Steps to Living (Set)",
    "author": null,
    "isbn": "5S33392011",
    "type": "K",
    "typeDescription": "Kit",
    "status": "A",
    "statusDescription": "Active",
    "packaging": "P",
    "packagingDescription": "Standard Packaged Product",
    "allowDiscount": false,
    "weight": 14,
    "useInStudioOnline": false,
    "glClassCode": null,
    "glClassCodeDescription": null,
    "category": null,
    "categoryDescription": null,
    "discountCategory": null,
    "discountCategoryDescription": null
}


```

Updates the specified product by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the product.
* author (optional) - The author of the product. This will be unset if you POST an empty value.
* isbn (optional) - The isbn of the product. This will be unset if you POST an empty value.
* type (optional) - The type code of the product. Must be a valid [product type](#product-type) value.
* status (optional) - The status code of the product. Must be a defined product status value.
* packaging (optional) - The packaging code of the product. Must be a valid [product packaging](#product-packaging) value.
* allowDiscount (optional) - Whether or not a discount is allowed on the product.
* weight (optional) - The weight of the product.
* useInStudioOnline (optional) - Whether or not to use the product is Studio Online. If not specified, will default to false.
* glClassCode (optional) - Will set a GL Class code
* category (optional) - Will put the product in the category
* discountCategory (optional) - Will set an initial discount category. Must be defined as a `DISCNTCTGY` code value.

##### Returns

Returns the product object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid product type or an undefined product status).

#### Delete a product

```
DEFINITION
DELETE http://apiserver/products/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product. It cannot be undone.

##### Arguments

* id (required) - The product code of the product to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product code does not exist, this call returns an error.

#### List all products

```
DEFINITION
GET http://apiserver/products

EXAMPLE REQUEST
$.get("http://localhost:49195/products?status=A");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 479
    }
    "items": [
        {
            "id": "BK-5SLVG",
            "description": "5 Steps to Living (Set)",
            "author": null,
            "isbn": "5S33392011",
            "type": "K",
            "typeDescription": "Kit",
            "status": "A",
            "statusDescription": "Active",
            "packaging": "P",
            "packagingDescription": "Standard Packaged Product",
            "allowDiscount": true,
            "weight": 14,
            "useInStudioOnline": false,
            "glClassCode": null,
            "glClassCodeDescription": null,
            "category": null,
            "categoryDescription": null,
            "discountCategory": null,
            "discountCategoryDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all products matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match in product code
* description (optional) - Filter list by partial match in product description
* author (optional) - Filter list by partial match in product author
* isbn (optional) - Filter list by partial match in product isbn
* type (optional) - Filter list by partial match in product type code
* status (optional) - Filter list by partial match in product status code
* packaging (optional) - Filter list by partial match in product packaging code
* codeType (optional) - Filter list by product code attribute type
* codeValue (optional) - Filter list by product code attribute value
* noteType (optional) - Filter list by product note attribute type
* shortComment(optional) - Filter list by product note attribute short comment
* longComment(optional) - Filter list by product note attribute long comment

##### Returns

A dictionary with an items property that contains an array of up to limit products, starting at index offset. Each entry in the array is a separate product object. If no more products are available, the resulting array will be empty. This request should never return an error.

#### Product type

* B () - Bill of Material
* K () - Kit
* P () - Single Product

#### Product packaging

* N () - No pick
* P () - Standard Packaged Product
* S () - Ship Separately

### Product Attachments

#### Create a product attachment

```
DEFINITION
POST http://apiserver/products/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/attachments", {
    "type":"PRODIMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "PRODIMAGE",
    "typeDescription": "Product Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new product attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a product attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve a product attachment

```
DEFINITION
GET http://apiserver/products/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/10106/attachments/117");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "PRODIMAGE",
    "typeDescription": "Product Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing product attachment. You need only supply the product attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a product attachment object if a valid id was provided.

#### Update a product attachment

```
DEFINITION
POST http://apiserver/products/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/10106/attachments/117", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified product attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the product attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined product attachment type code).

#### Delete a product attachment

```
DEFINITION
DELETE http://apiserver/products/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG/attachments/117", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the product attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product attachment id does not exist, this call returns an error.

#### List all product attachments

```
DEFINITION
GET http://apiserver/products/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
                "longComment": "long comment text",
                "dateCreated": "2018-03-12",
                "id": "117",
                "type": "LOGO",
                "typeDescription": "Logo",
                "url": null,
                "fileName": "logo64.png",
                "file": null,
                "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit product attachments, starting at index offset. Each entry in the array is a separate product attachment object. If no more product attachments are available, the resulting array will be empty. This request should never return an error.

#### Product Build BOM

```
DEFINITION
POST http://apiserver/products/:id/buildbom

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BKLTPL/buildbom", {
        "warehouse":"10",
        "location":"A1",
        "quantity":2,
        "date":"2015-08-11",
        "reason":"AUTO",
        "comment":"build bom comment",
        "componentLocations": {
            "PTLV1":"A1",
            "PTLV2":"A1",
            "BLBWRAP":"A1"
        }
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* warehouse (required) - The warehouse for the product build BOM process. (Must be a valid warehouse for the product.)
* location (required) - The warehouse location for the product build BOM process. (Must be a valid warehouse location for the product.)
* quantity (required) - The quantity to build for the product build BOM process.
* date (optional) - The date for the transaction for the product build BOM process.
* reason (optional) - The reason code for the transaction for the product build BOM process.
* comment (optional) - The comment for the transaction for the product build BOM process.
* componentLocations (optional) - A dictionary where the key is the product code for the component of the BOM product and the value is the warehouse location of the product. (The dictionary must include all component for the BOM product with valid warehouse locations. The quantity of the product in the BOM times the quantity of BOM product created must be less than or equal to the available quantity of each component product.)

##### Returns

Returns a 204 No Content response on success. If there is an error, either a 400 or 500 will be returned.

### Product Categories

#### Create a product category

```
DEFINITION
POST http://apiserver/products/:productCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.post("http://localhost:49195/products/100BACK/storeconfigurations/1/categories", {
    "categoryId": 20
});

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Creates a new product category for the given StudioOnline store configuration.

##### Arguments

* categoryId (required) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns a product category object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a product category

```
DEFINITION
GET http://apiserver/products/:productCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/100BACK/storeconfigurations/1/categories/14");

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Retrieves the details of an existing product category for the given StudioOnline store configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the product category to be retrieved.

#### Update a product category

```
DEFINITION
POST http://apiserver/products/:productCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/100BACK/storeconfigurations/1/categories/14", {
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": true,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}


```

Updates the specified product category for the given StudioOnline store configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* categoryId (optional) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns the product category object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product category

```
DEFINITION
DELETE http://apiserver/products/:productCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/100BACK/storeconfigurations/1/categories/14", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product category from the given StudioOnline store configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the product category to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the product category does not exist, this call returns an error.

#### List all product categories

```
DEFINITION
GET http://apiserver/products/:productCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.get("http://localhost:49195/products/100BACK/storeconfigurations/1/categories");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "14",
            "categoryId": "20",
            "categoryName": "Best Sellers",
            "isPrimary": true,
            "isActive": true,
            "breadcrumb": "best-sellers",
            "parentCategoryId": null,
            "parentCategoryName": null
        },
        {...},
    ]
}

```

Returns a list of all product categories for the given StudioOnline store configuration.

##### Returns

A dictionary with an items property that contains an array of up to limit product categories, starting at index offset. Each entry in the array is a separate product category object. If no more product categories are available, the resulting array will be empty. This request should never return an error.

### Product codes

#### Create a product code

```
DEFINITION
POST http://apiserver/products/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/codes", {
    "type": "DDCGLCLASS",
    "value": "BKS"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "DDCGLCLASS",
    "value": "BKS",
    "isActive": true
}

```

Creates a new product code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a product code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a product code

```
DEFINITION
GET http://apiserver/products/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/10106/codes/937");

EXAMPLE RESPONSE
{
    "id": "937",
    "type": "ECPRODCAT",
    "value": "69",
    "isActive": true
}

```

Retrieves the details of an existing product code. You need only supply the product code id.

##### Arguments

* id (required) - The id of the product code to retrieve.

##### Returns

Returns a product code object if a valid id was provided.

#### Update a product code

```
DEFINITION
POST http://apiserver/products/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/10106/codes/937", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "937",
    "type": "ECPRODCAT",
    "value": "69",
    "isActive": false
}


```

Updates the specified product code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the product code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a product code

```
DEFINITION
DELETE http://apiserver/products/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG/codes/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product code. It cannot be undone.

##### Arguments

* id (required) - The id of the product code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product code id does not exist, this call returns an error.

#### List all product codes

```
DEFINITION
GET http://apiserver/products/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "8096",
            "type": "DDCGLCLASS",
            "value": "BKS",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product codes.

##### Returns

A dictionary with an items property that contains an array of up to limit product codes, starting at index offset. Each entry in the array is a separate product code object. If no more product codes are available, the resulting array will be empty. This request should never return an error.

### Product Coupons

#### Create a product coupon

```
DEFINITION
POST http://apiserver/productcoupons

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons", {
    "couponCode": "20OFF",
    "description": "Twenty Percent Off",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 5,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "usageApplication": "CPNSGLPROD"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "couponCode": "20OFF",
    "description": "Twenty Percent Off",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 5,
    "minimumOrderAmount": null,
    "minimumOrderQuantity": null,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "discountAmount": null,
    "usageApplication": "CPNSGLPROD"
}

```

Creates a new product coupon.

##### Arguments

* couponCode (required) - The coupon code to be created.
* description (required) - The coupon code's description.
* status (required) - Is the product coupon active or inactive.
* startDate - The start date for product coupon usage.
* endDate - The end date for product coupon usage.
* usageRestrictionType - The way that the coupon can be used. (CPNSYSLMTD: system limited, CPNCSTLMTD: customer limited, CPNUNLMTD: unlimited).
* usageLimit (required if system or customer limited) - If system or customer limited, the number of times the product coupon can be used.
* minimumOrderAmount - The minimum amount for an order before the product coupon can be applied.
* minimumOrderQuantity - The minimum quantity for an order before the product coupon can be applied.
* maximumDiscountAmount - The maximum amount allowed to be deducted using this product coupon.
* couponEffect - What effect this coupon has (CPNDISCPCT: discount percentage, CPNDISCAMT: discount amount)
* discountPercentage (required if discount percent effect) - The percentage deducted by this product coupon.
* discountAmount (required if discount amount effect) - The amount deducted by this product coupon.
* usageApplication (required) - How this coupon should be applied (CPNALLITM: All products in cart, CPNSGLITEM: Single product in cart).

##### Returns

Returns a product coupon object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a product coupon

```
DEFINITION
GET http://apiserver/productcoupons/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "couponCode": "20OFF",
    "description": "Twenty Percent Off",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 5,
    "minimumOrderAmount": null,
    "minimumOrderQuantity": null,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "discountAmount": null,
    "usageApplication": "CPNSGLPROD"
}

```

Retrieves the details of an existing product coupon. You need only supply the id.

##### Arguments

* id (required) - The id of the product coupon to be retrieved.

#### Update a product coupon

```
DEFINITION
POST http://apiserver/productcoupons/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons/1", {
    "usageLimit": 10
});

EXAMPLE RESPONSE
{
    "id": "1",
    "couponCode": "20OFF",
    "description": "Twenty Percent Off",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 10,
    "minimumOrderAmount": null,
    "minimumOrderQuantity": null,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "discountAmount": null,
    "usageApplication": "CPNSGLPROD"
}


```

Updates the specified product coupon by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* couponCode - The coupon code to be created.
* description - The coupon code's description.
* status - Is the product coupon active or inactive.
* startDate - The start date for product coupon usage.
* endDate - The end date for product coupon usage.
* usageRestrictionType - The way that the coupon can be used. (CPNSYSLMTD: system limited, CPNCSTLMTD: customer limited, CPNUNLMTD: unlimited).
* usageLimit - If system or customer limited, the number of times the product coupon can be used.
* minimumOrderAmount - The minimum amount for an order before the product coupon can be applied.
* minimumOrderQuantity - The minimum quantity for an order before the product coupon can be applied.
* maximumDiscountAmount - The maximum amount allowed to be deducted using this product coupon.
* couponEffect - What effect this coupon has (CPNDISCPCT: discount percentage, CPNDISCAMT: discount amount)
* discountPercentage - The percentage deducted by this product coupon.
* discountAmount - The amount deducted by this product coupon.
* usageApplication - How this coupon should be applied (CPNALLITM: All products in cart, CPNSGLITEM: Single product in cart).

##### Returns

Returns the product coupon object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product coupon

```
DEFINITION
DELETE http://apiserver/productcoupons/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/productcoupons/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product coupon. It cannot be undone.

##### Arguments

* id (required) - The id of the product coupon to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the product coupon does not exist, this call returns an error.

#### List all product coupons

```
DEFINITION
GET http://apiserver/productcoupons

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1",
            "couponCode": "20OFF",
            "description": "Twenty Percent Off",
            "status": "A",
            "startDate": "2017-11-09",
            "endDate": "2017-11-30",
            "usageRestrictionType": "CPNCSTLMTD",
            "usageLimit": 10,
            "minimumOrderAmount": null,
            "minimumOrderQuantity": null,
            "maximumDiscountAmount": 100,
            "couponEffect": "CPNDISCPCT",
            "discountPercentage": 20,
            "discountAmount": null,
            "usageApplication": "CPNSGLPROD"
        },
        {...},
    ]
}

```

Returns a list of all product coupons.

##### Arguments

* couponCode - The coupon code to filter search results by.
* description - The description to filter search results by.
* status - The status to filter search results by.

##### Returns

A dictionary with an items property that contains an array of up to limit product coupons, starting at index offset. Each entry in the array is a separate product coupon object. If no more product coupons are available, the resulting array will be empty. This request should never return an error.

### Product Coupon Category Usages

#### Create a product coupon category usage

```
DEFINITION
POST http://apiserver/productcoupons/:couponId/categoryusages

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons/4/categoryusages", {
    "categoryCode": "BOOKS",
    "includeExclude": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "categoryCode": "BOOKS",
    "categoryCodeDescription": "Books",
    "includeExclude": true
}

```

Creates a new product coupon category usage.

##### Arguments

* categoryCode (required) - The category code to associate the product coupon usage with.
* includeExclude - If true, this product coupon usage applies to only this category. If false, It applies to all categories EXCEPT this one.

##### Returns

Returns a product coupon category usage object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a product coupon category usage

```
DEFINITION
GET http://apiserver/productcoupons/:couponId/categoryusages/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons/4/categoryusages/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "categoryCode": "BOOKS",
    "categoryCodeDescription": "Books",
    "includeExclude": true
}

```

Retrieves the details of an existing product coupon category usage. You need only supply the id.

##### Arguments

* id (required) - The id of the product coupon category usage to be retrieved.

#### Update a product coupon category usage

```
DEFINITION
POST http://apiserver/productcoupons/:couponId/categoryusages/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons/4/categoryusages/3", {
    "includeExclude": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "categoryCode": "BOOKS",
    "categoryCodeDescription": "Books",
    "includeExclude": false
}

```

Updates the specified product coupon category usage by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* categoryCode - The category to associate the product coupon usage with.
* includeExclude - If true, this product coupon usage applies to only this category. If false, It applies to all category EXCEPT this one.

##### Returns

Returns the product coupon category usage object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product coupon category usage

```
DEFINITION
DELETE http://apiserver/productcoupons/:couponId/categoryusages/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/productcoupons/4/categoryusages/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product coupon category usage. It cannot be undone.

##### Arguments

* id (required) - The id of the product coupon category usage to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the product coupon category usage does not exist, this call returns an error.

#### List all product coupon category usages

```
DEFINITION
GET http://apiserver/productcoupons/:couponId/categoryusages

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons/:couponId/categoryusages");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "categoryCode": "BOOKS",
            "categoryCodeDescription": "Books",
            "includeExclude": false
        },
        {...},
    ]
}

```

Returns a list of all product coupon category usages.

##### Arguments

* categoryCode - The category to filter search results by.

##### Returns

A dictionary with an items property that contains an array of up to limit product coupon category usages, starting at index offset. Each entry in the array is a separate product coupon category usage object. If no more product coupon category usages are available, the resulting array will be empty. This request should never return an error.

### Product Coupon Geographic Usages

#### Create a product coupon geographic usage

```
DEFINITION
POST http://apiserver/productcoupons/:couponId/geographicusages

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons/4/geographicusages", {
    "country": "USA",
    "postalCodeLow": "75080",
    "postalCodeHigh": "75080",
    "includeExclude": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "country": "USA",
    "postalCodeLow": "75080",
    "postalCodeHigh": "75080-4567",
    "includeExclude": true
}

```

Creates a new product coupon geographic usage.

##### Arguments

* country (required) - The country to associate the product coupon usage with.
* postalCodeLow (required) - The bottom range for valid postal codes to associate the product coupon usage with.
* postalCodHigh (required) - The upper range for valid postal codes to associate the product coupon usage with.
* includeExclude - If true, this product coupon usage applies to only this geographic definition. If false, It applies to all categories EXCEPT this one.

##### Returns

Returns a product coupon geographic usage object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a product coupon geographic usage

```
DEFINITION
GET http://apiserver/productcoupons/:couponId/geographicusages/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons/4/geographicusages/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "country": "USA",
    "postalCodeLow": "75080",
    "postalCodeHigh": "75080-4567",
    "includeExclude": true
}

```

Retrieves the details of an existing product coupon geographic usage. You need only supply the id.

##### Arguments

* id (required) - The id of the product coupon geographic usage to be retrieved.

#### Update a product coupon geographic usage

```
DEFINITION
POST http://apiserver/productcoupons/:couponId/geographicusages/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons/4/geographicusages/3", {
    "includeExclude": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "country": "USA",
    "postalCodeLow": "75080",
    "postalCodeHigh": "75080-4567",
    "includeExclude": false
}

```

Updates the specified product coupon geographic usage by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* country - The country to associate the product coupon usage with.
* postalCodeLow - The bottom range for valid postal codes to associate the product coupon usage with.
* postalCodHigh - The upper range for valid postal codes to associate the product coupon usage with.
* includeExclude - If true, this product coupon usage applies to only this geographic definition. If false, It applies to all categories EXCEPT this one.

##### Returns

Returns the product coupon geographic usage object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product coupon geographic usage

```
DEFINITION
DELETE http://apiserver/productcoupons/:couponId/geographicusages/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/productcoupons/4/geographicusages/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product coupon geographic usage. It cannot be undone.

##### Arguments

* id (required) - The id of the product coupon geographic usage to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the product coupon geographic usage does not exist, this call returns an error.

#### List all product coupon geographic usages

```
DEFINITION
GET http://apiserver/productcoupons/:couponId/geographicusages

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons/:couponId/geographicusages");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "country": "USA",
            "postalCodeLow": "75080",
            "postalCodeHigh": "75080-4567",
            "includeExclude": false
        },
        {...},
    ]
}

```

Returns a list of all product coupon geographic usages.

##### Arguments

* country - The country to filter results by.
* postalCodeLow - The bottom range for valid postal codes to filter results by.
* postalCodHigh - The upper range for valid postal codes to filter results by.

##### Returns

A dictionary with an items property that contains an array of up to limit product coupon geographic usages, starting at index offset. Each entry in the array is a separate product coupon geographic usage object. If no more product coupon geographic usages are available, the resulting array will be empty. This request should never return an error.

### Product Coupon Product Usages

#### Create a product coupon product usage

```
DEFINITION
POST http://apiserver/productcoupons/:couponId/productusages

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons/4/productusages", {
    "productCode": "BK-5SLVG",
    "includeExclude": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "productCode": "BK-5SLVG",
    "productDescription": "5 Steps to Living (Set)",
    "includeExclude": true
}

```

Creates a new product coupon product usage.

##### Arguments

* productCode (required) - The product code to associate the product coupon usage with.
* includeExclude - If true, this product coupon usage applies to only this product code. If false, It applies to all products EXCEPT this one.

##### Returns

Returns a product coupon product usage object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a product coupon product usage

```
DEFINITION
GET http://apiserver/productcoupons/:couponId/productusages/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons/4/productusages/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "productCode": "BK-5SLVG",
    "productDescription": "5 Steps to Living (Set)",
    "includeExclude": true
}

```

Retrieves the details of an existing product coupon product usage. You need only supply the id.

##### Arguments

* id (required) - The id of the product coupon product usage to be retrieved.

#### Update a product coupon product usage

```
DEFINITION
POST http://apiserver/productcoupons/:couponId/productusages/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productcoupons/4/productusages/3", {
    "includeExclude": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "productCode": "BK-5SLVG",
    "productDescription": "5 Steps to Living (Set)",
    "includeExclude": false
}

```

Updates the specified product coupon product usage by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* productCode - The product code to associate the product coupon usage with.
* includeExclude - If true, this product coupon usage applies to only this product code. If false, It applies to all products EXCEPT this one.

##### Returns

Returns the product coupon product usage object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product coupon product usage

```
DEFINITION
DELETE http://apiserver/productcoupons/:couponId/productusages/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/productcoupons/4/productusages/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product coupon product usage. It cannot be undone.

##### Arguments

* id (required) - The id of the product coupon product usage to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the product coupon product usage does not exist, this call returns an error.

#### List all product coupon product usages

```
DEFINITION
GET http://apiserver/productcoupons/:couponId/productusages

EXAMPLE REQUEST
$.get("http://localhost:49195/productcoupons/:couponId/productusages");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "productCode": "BK-5SLVG",
            "productDescription": "5 Steps to Living (Set)",
            "includeExclude": false
        },
        {...},
    ]
}

```

Returns a list of all product coupon product usages.

##### Arguments

* productCode - The product code to filter search results by.

##### Returns

A dictionary with an items property that contains an array of up to limit product coupon product usages, starting at index offset. Each entry in the array is a separate product coupon product usage object. If no more product coupon product usages are available, the resulting array will be empty. This request should never return an error.

### Product Dates

#### Create a product date

```
DEFINITION
POST http://apiserver/products/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/dates", {
    "type": "PRODLSCD",
    "value": "2012-05-17"
});

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "PRODLSCD",
    "value": "2012-05-17",
    "isActive": true
}

```

Creates a new product date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a product date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve a product date

```
DEFINITION
GET http://apiserver/products/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/10106/dates/43");

EXAMPLE RESPONSE
{
    "id": "43",
    "type": "PRODLSCD",
    "value": "2012-05-17",
    "isActive": true
}

```

Retrieves the details of an existing product date. You need only supply the product date id.

##### Arguments

* id (required) - The id of the product date to retrieve.

##### Returns

Returns a product date object if a valid id was provided.

#### Update a product date

```
DEFINITION
POST http://apiserver/products/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/10106/dates/43", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "43",
    "type": "PRODLSCD",
    "value": "2012-05-17",
    "isActive": false
}


```

Updates the specified product date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the product date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a product date

```
DEFINITION
DELETE http://apiserver/products/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG/dates/1601", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product date. It cannot be undone.

##### Arguments

* id (required) - The id of the product date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product date id does not exist, this call returns an error.

#### List all product dates

```
DEFINITION
GET http://apiserver/products/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "1601",
            "type": "PRODLSCD",
            "value": "2012-05-17",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product dates.

##### Returns

A dictionary with an items property that contains an array of up to limit product dates, starting at index offset. Each entry in the array is a separate product date object. If no more product dates are available, the resulting array will be empty. This request should never return an error.

### Product Images

#### Create a product image

```
DEFINITION
POST http://apiserver/products/:productId/images

EXAMPLE REQUEST
$.post("http://localhost:49195/products/100BKLET/images", {
    "imageType": "IMAGEXS",
    "description": "Xtra Small Product Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image",
    "title": "Image Title",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Product Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Creates a new product image.

##### Arguments

* imageType (required) - the ImageType code value for the product image.
* description (optional) - the description for the product image.
* imageUrl (required) - the image URL for the product image.
* alternateText (optional) - the alternate text for the product image.
* title (optional) - the image title for the product image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns a product image object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a product image

```
DEFINITION
GET http://apiserver/products/:productId/images/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/100BKLET/images/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Product Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Retrieves the details of an existing product image. You need only supply the id.

##### Arguments

* id (required) - The id of the product image to be retrieved.

#### Update a product image

```
DEFINITION
POST http://apiserver/products/:productId/images/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/100BKLET/images/6", {
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Product Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}


```

Updates the specified product image by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* imageType (optional) - the ImageType code value to update for the product image.
* description (optional) - the description to update for the product image.
* imageUrl (optional) - the image URL to update for the product image.
* alternateText (optional) - the alternate text to update for the product image.
* title (optional) - the image title to update for the product image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns the product image object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product image

```
DEFINITION
DELETE http://apiserver/products/:productId/images/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/100BKLET/images/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product image. It cannot be undone.

##### Arguments

* id (required) - The id of the product image to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the product image does not exist, this call returns an error.

#### List all product images

```
DEFINITION
GET http://apiserver/products/:productId/images

EXAMPLE REQUEST
$.get("http://localhost:49195/products/100BKLET/images");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 9
    },
    "items": [
        {
            "id": "6",
            "imageType": "IMAGEXS",
            "imageTypeDescription": "Extra Small Image",
            "description": "Xtra Small Product Img",
            "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
            "alternateText": "Image Alt Text",
            "title": "Image Title",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all product images by product code.

##### Returns

A dictionary with an items property that contains an array of up to limit product images, starting at index offset. Each entry in the array is a separate product image object. If no more product images are available, the resulting array will be empty. This request should never return an error.

### Product In Kits

#### List all kits the product is in

```
DEFINITION
GET http://apiserver/products/:id/kits

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/kits");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "21701CD",
            "description": "Authority in the Church",
            "quantity": 1,
            "useInStudioOnline": false,
            "status": "A",
            "statusDescription": "Active"
        },
        { ... }
    ]
}

```

Returns a list of all kits the product is in

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit product kits, starting at index offset. Each entry in the array is a separate product kit object. If no more product kit are available, the resulting array will be empty.

### Product In Variant Groups

#### List all variant groups the product is in

```
DEFINITION
GET http://apiserver/products/:id/variantgroups

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/variantgroups");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "groupCode": "BK-VARIANT",
            "groupDescription": "Book Variant"
            "groupId": "3",
            "sequenceNumber": 1,
            "store": "19",
            "storeDescription": "StudioOnline Store"
        },
        { ... }
    ]
}

```

Returns a list of all variant groups the product is in

##### Returns

A dictionary with an items property that contains an array of up to limit product variant groups, starting at index offset. Each entry in the array is a separate product variant group object. If no more product variant groups are available, the resulting array will be empty.

### Product Kit Components

#### Create a product kit component

```
DEFINITION
POST http://apiserver/products/:id/components

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/components", {
    "componentProduct": "BK-DWOG",
    "quantity": 1,
    "useInStudioOnline": true
});

EXAMPLE RESPONSE
{
    "id": "133",
    "componentProduct": "BK-DWOG",
    "description": "Determining the Will of God",
    "quantity": 1,
    "backorderQuantity": 15,
    "onOrderQuantity": 0,
    "committedQuantity": 360,
    "weight": 0.25,
    "useInStudioOnline": true,
    "status": "A",
    "statusDescription": "Active"
}

```

Creates a new product kit component object.

##### Arguments

* componentProduct (required) - The component product code.
* quantity (required) - The quantity of the product component in the kit.
* useInStudioOnline (required) - Whether to use the product kit component in StudioOnline.

##### Returns

Returns a product kit component object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid componentProduct) or if trying to view components on a product that is not of type `K` (Kit) or type `B` (BOM).

#### Retrieve a product kit component

```
DEFINITION
GET http://apiserver/products/:id/components/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/components/133");

EXAMPLE RESPONSE
{
    "id": "133",
    "componentProduct": "BK-DWOG",
    "description": "Determining the Will of God",
    "quantity": 1,
    "backorderQuantity": 15,
    "onOrderQuantity": 0,
    "committedQuantity": 360,
    "weight": 0.25,
    "useInStudioOnline": true,
    "status": "A",
    "statusDescription": "Active"
}

```

Retrieves the details of an existing product kit component. You need only supply the product code and component id.

##### Arguments

##### Returns

Returns a product kit component object if a valid id was provided.

#### Update a product kit component

```
DEFINITION
POST http://apiserver/products/:id/components/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/components/133", {
    "quantity": 2
});

EXAMPLE RESPONSE
{
    "id": "133",
    "componentProduct": "BK-DWOG",
    "description": "Determining the Will of God",
    "quantity": 2,
    "backorderQuantity": 15,
    "onOrderQuantity": 0,
    "committedQuantity": 360,
    "weight": 0.25,
    "useInStudioOnline": true,
    "status": "A",
    "statusDescription": "Active"
}


```

Updates the specified product kit component by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* componentProduct (optional) - The component product code.
* quantity (optional) - The quantity of the product component in the kit.
* useInStudioOnline (optional) - Whether to use the product kit component in StudioOnline.

##### Returns

Returns the product kit component object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product kit component

```
DEFINITION
DELETE http://apiserver/products/:id/components/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG/components/133", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product kit component. It cannot be undone.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the product kit component does not exist, this call returns an error.

#### List all product kit components

```
DEFINITION
GET http://apiserver/products/:id/components

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/components");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "133",
            "componentProduct": "BK-DWOG",
            "description": "Determining the Will of God",
            "quantity": 2,
            "backorderQuantity": 15,
            "onOrderQuantity": 0,
            "committedQuantity": 360,
            "weight": 0.25,
            "useInStudioOnline": true,
            "status": "A",
            "statusDescription": "Active"
        },
        { ... }
    ]
}

```

Returns a list of all product kit components for the product code.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit product kit components, starting at index offset. Each entry in the array is a separate product kit component object. If no more product kit component are available, the resulting array will be empty. This request will return an error if trying to view components on a product that is not of type `K` (Kit) or type `B` (BOM).

### Product Kit Exploded Components

#### List all product kit exploded components

```
DEFINITION
GET http://apiserver/products/:id/explodedcomponents

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/explodedcomponents");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "BK-DWOG",
            "description": "Determining the Will of God",
            "quantity": 2,
            "backorderQuantity": 15,
            "onOrderQuantity": 0,
            "committedQuantity": 360,
            "weight": 0.25
        },
        { ... }
    ]
}

```

Returns a list of all product kit components that have been exploded recursively for the product code.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit product kit exploded components, starting at index offset. Each entry in the array is a separate product kit exploded component object. If no more product kit exploded component are available, the resulting array will be empty. This request will return an error if trying to view exploded components on a product that is not of type `K` (Kit).

### Product Notes

#### Create a product note

```
DEFINITION
POST http://apiserver/products/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/notes", {
    "type": "PRODSYN",
    "shortComment": "Synopsis"
});

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "PRODSYN",
    "shortComment": "Synopsis",
    "longComment": null
}

```

Creates a new product note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a product note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a product note

```
DEFINITION
GET http://apiserver/products/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/10106/notes/420");

EXAMPLE RESPONSE
{
    "id": "420",
    "type": "PRODSYN",
    "shortComment": "Synopsis",
    "longComment": null
}

```

Retrieves the details of an existing product note. You need only supply the product note id.

##### Arguments

* id (required) - The id of the product note to retrieve.

##### Returns

Returns a product note object if a valid id was provided.

#### Update a product note

```
DEFINITION
POST http://apiserver/products/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/10106/notes/420", {
    "shortComment": null,
    "longComment": "Synopsis"
});

EXAMPLE RESPONSE
{
    "id": "420",
    "type": "PRODSYN",
    "shortComment": null,
    "longComment": "Synopsis"
}


```

Updates the specified product note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the product note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a product note

```
DEFINITION
DELETE http://apiserver/products/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG/notes/5054", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product note. It cannot be undone.

##### Arguments

* id (required) - The id of the product note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product note id does not exist, this call returns an error.

#### List all product notes

```
DEFINITION
GET http://apiserver/products/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5054",
            "type": "PRODSYN",
            "shortComment": "Synopsis",
            "longComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product notes.

##### Returns

A dictionary with an items property that contains an array of up to limit product notes, starting at index offset. Each entry in the array is a separate product note object. If no more product notes are available, the resulting array will be empty. This request should never return an error.

### Product Numbers

#### Create a product number

```
DEFINITION
POST http://apiserver/products/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/numbers", {
    "type": "DDCPRODPAG",
    "value": 155
});

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "DDCPRODPAG",
    "value": 155,
    "isActive": true
}

```

Creates a new product number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a product number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a product number

```
DEFINITION
GET http://apiserver/products/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/10106/numbers/30");

EXAMPLE RESPONSE
{
    "id": "30",
    "type": "DDCPRODPAG",
    "value": 155,
    "isActive": true
}

```

Retrieves the details of an existing product number. You need only supply the product number id.

##### Arguments

* id (required) - The id of the product number to retrieve.

##### Returns

Returns a product number object if a valid id was provided.

#### Update a product number

```
DEFINITION
POST http://apiserver/products/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/10106/numbers/30", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "30",
    "type": "DDCPRODPAG",
    "value": 155,
    "isActive": false
}


```

Updates the specified product number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the product number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a product number

```
DEFINITION
DELETE http://apiserver/products/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG/numbers/828", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product number. It cannot be undone.

##### Arguments

* id (required) - The id of the product number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product number id does not exist, this call returns an error.

#### List all product numbers

```
DEFINITION
GET http://apiserver/products/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "828",
            "type": "DDCPRODPAG",
            "value": 155,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit product numbers, starting at index offset. Each entry in the array is a separate product number object. If no more product numbers are available, the resulting array will be empty. This request should never return an error.

### Product Prices

#### Create a product price

```
DEFINITION
POST http://apiserver/products/:id/prices

EXAMPLE REQUEST
$.post("http://localhost:49195/products/BK-5SLVG/prices", {
    "type": "B",
    "amount": 25,
    "currency": "USD",
    "start": "2013-11-15",
    "end": "2014-01-31"
});

EXAMPLE RESPONSE
{
    "id": "12",
    "type": "B",
    "description": "Benevolent (Free)",
    "amount": 25,
    "currency": "USD",
    "currencyDescription": "US Dollars",
    "start": "2013-11-15",
    "end": "2014-01-31",
    "useInStudioOnline": false
}

```

Creates a new product price object.

##### Arguments

* type (required) - The price code. Must be a defined price code for products.
* amount (required) - The amount of the price.
* currency (required) - The currency code. Must be a defined currency code.
* start (optional) - The start date for which the price is in effect.
* end (optional) - The end date for which the price is in effect.
* useInStudioOnline (optional) - Whether or not to publish to StudioOnline

##### Returns

Returns a product price object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined price code or invalid start and end dates).

#### Retrieve a product price

```
DEFINITION
GET http://apiserver/products/:id/prices/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/10106/prices/973");

EXAMPLE RESPONSE
{
    "id": "973",
    "type": "SP",
    "description": "Special Price",
    "amount": 22.98,
    "currency": "USD",
    "currencyDescription": "US Dollars",
    "start": "2006-02-27",
    "end": "2006-03-04",
    "useInStudioOnline": true
}

```

Retrieves the details of an existing product price. You need only supply the product price id.

##### Arguments

* id (required) - The id of the product price to retrieve.

##### Returns

Returns a product price object if a valid id was provided.

#### Update a product price

```
DEFINITION
POST http://apiserver/products/:id/prices/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/10106/prices/973", {
    "amount": 15,
    "useInStudioOnline": false
});

EXAMPLE RESPONSE
{
    "id": "973",
    "type": "SP",
    "description": "Special Price",
    "amount": 15,
    "currency": "USD",
    "currencyDescription": "US Dollars",
    "start": "2006-02-27",
    "end": "2006-03-04",
    "useInStudioOnline": false
}


```

Updates the specified product price by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The price code. Must be a defined price code for products.
* amount (optional) - The amount of the price.
* currency (optional) - The currency code. Must be a defined currency code.
* start (optional) - The start date for which the price is in effect. Must be less than or equal to end and must not overlap with an existing date range of the same type+currency.
* end (optional) - The end date for which the price is in effect. Must be greater than or equal to start and must not overlap with an existing date range of the same type+currency.
* useInStudioOnline (optional) - Whether or not to publish to StudioOnline

##### Returns

Returns the product price object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined price code or invalid start and end dates).

#### Delete a product price

```
DEFINITION
DELETE http://apiserver/products/:id/prices/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/BK-5SLVG/prices/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product price. It cannot be undone.

##### Arguments

* id (required) - The id of the product price to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product price id does not exist, this call returns an error.

#### List all product prices

```
DEFINITION
GET http://apiserver/products/:id/prices

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/prices");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "12",
            "type": "B",
            "description": "Benevolent (Free)",
            "amount": 15,
            "currency": "USD",
            "currencyDescription": "US Dollars",
            "start": "2013-10-14",
            "end": "2013-10-17",
            "useInStudioOnline": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product prices.

##### Returns

A dictionary with an items property that contains an array of up to limit product prices, starting at index offset. Each entry in the array is a separate product price object. If no more product prices are available, the resulting array will be empty. This request should never return an error.

#### List all product prices for order entry

```
DEFINITION
GET http://apiserver/products/:id/prices?forOrderEntry=true

EXAMPLE REQUEST
$.get("http://localhost:49195/products/BK-5SLVG/prices?forOrderEntry=true&warehouse=10&company=1&currency=USD");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "currency": null,
            "currencyDescription": "null",
            "id": "94",
            "type": "P",
            "description": "Promotional (Free)",
            "amount": 0,
            "start": null,
            "end": null,
            "useInStudioOnline": false
        },
        {
            "currency": null,
            "currencyDescription": "null",
            "id": "91",
            "type": "RP",
            "description": "Retail Price",
            "amount": 24.99,
            "start": null,
            "end": null,
            "useInStudioOnline": false
        },
        { ... }
    ]
}

```

Returns a list of product prices which are valid for order entry. Returns all product prices which are defined on the product as well as the three standard price codes for (P) promotional, (B) benevolent and (I) intercompany.

NOTE: When `forOrderEntry=true`, the `currency`, `currencyDescription`, `start`, `end` and `useInStudioOnline` properties will be `null`.

##### Arguments

* forOrderEntry (required) - Set to `true` to retrieve product prices which are valid for order entry
* company (required) - company code
* currency (required) - currency code
* warehouse (required) - warehouse code
* type (optional) - Filter by partial match on type
* description (optional) - Filter by partial match on description

### Product Quick Picks

#### Create a product quick pick

```
DEFINITION
POST http://apiserver/productquickpicks

EXAMPLE REQUEST
$.post("http://localhost:49195/productquickpicks", {
    "product": "1A100",
    "startDate": "2012-07-11",
    "endDate": "2013-09-27"
});

EXAMPLE RESPONSE
{
    "id": "17",
    "product": "1A100",
    "productDescription": "Defending the Faith",
    "startDate": "2012-07-11",
    "endDate": "2013-09-27"
}

```

Creates a new product quick pick object.

##### Arguments

* product (required) - The product code.
* startDate (optional) - The start date of the product quick pick.
* endDate (optional) - The end date of the product quick pick.

##### Returns

Returns a product quick pick object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid product).

#### Retrieve a product quick pick

```
DEFINITION
GET http://apiserver/productquickpicks/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productquickpicks/17");

EXAMPLE RESPONSE
{
    "id": "17",
    "product": "1A100",
    "productDescription": "Defending the Faith",
    "startDate": "2012-07-11",
    "endDate": "2013-09-27"
}

```

Retrieves the details of an existing product quick pick. You need only supply the product quick pick id.

##### Arguments

* id (required) - The id of the product quick pick to be retrieved.

##### Returns

Returns a product quick pick object if a valid product quick pick id was provided.

#### Update a product quick pick

```
DEFINITION
POST http://apiserver/productquickpicks/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productquickpicks/17", {
    "endDate": "2013-12-31"
});

EXAMPLE RESPONSE
{
    "id": "17",
    "product": "1A100",
    "productDescription": "Defending the Faith",
    "startDate": "2012-07-11",
    "endDate": "2013-12-31"
}


```

Updates the specified product quick pick by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* product (optional) - The product code.
* startDate (optional) - The start date of the product quick pick.
* endDate (optional) - The end date of the product quick pick.

##### Returns

Returns the product quick pick object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid product).

#### Delete a product quick pick

```
DEFINITION
DELETE http://apiserver/productquickpicks/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/productquickpicks/17", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product quick pick. It cannot be undone.

##### Arguments

* id (required) - The id of the product quick pick to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product quick pick id does not exist, this call returns an error.

#### List all product quick picks

```
DEFINITION
GET http://apiserver/productquickpicks

EXAMPLE REQUEST
$.get("http://localhost:49195/productquickpicks?product=1A100");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    }
    "items": [
        {
            "id": "17",
            "product": "1A100",
            "productDescription": "Defending the Faith",
            "startDate": "2012-07-11",
            "endDate": "2013-12-31"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product quick picks matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by product quick pick id
* product () - Filter list by partial match in product code
* startDate () - Filter list by start date
* endDate () - Filter list by end date

##### Returns

A dictionary with an items property that contains an array of up to limit product quick picks, starting at index offset. Each entry in the array is a separate product quick pick object. If no more product quick picks are available, the resulting array will be empty. This request should never return an error.

#### Product Release Backorder

```
DEFINITION
POST http://apiserver/products/releasebackorder

EXAMPLE REQUEST
$.post("http://localhost:49195/products/releasebackorder", {
        "warehouse": "10"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* startingDocumentNumber (optional) - The starting document number for the product release backorder process.
* endingDocumentNumber (optional) - The ending document number for the product release backorder process.
* warehouse (optional) - The warehouse code for the product release backorder process.
* product (optional) - The product code for the product release backorder process.

##### Returns

Returns a 204 No Content response on success.

### Product StudioOnline Publish Data

#### Retrieve the product StudioOnline publish data

```
DEFINITION
GET http://apiserver/products/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.get("http://localhost:49195/products/7399/studioonlinepublishdata");

EXAMPLE RESPONSE
{
    "id": "6440",
    "description": "Product Test",
    "summary": "Summary Test",
    "extendedDescription": "Description Test",
    "isExtendedDescriptionLocked": true,
    "iconImage": "iconImage.png",
    "mediumImage": "mediumImage.jpg",
    "keywords": "Test Keywords",
    "pageLayout": "PRODPACK2",
    "weight": "2"
}

```

Retrieves the details of the existing product StudioOnline publish data. You need only supply the product id.

##### Returns

Returns a product StudioOnline publish data object if a valid id was provided.

#### Update and publish the product StudioOnline publish data

```
DEFINITION
POST http://apiserver/products/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.post("http://localhost:49195/products/7399/studioonlinepublishdata", {
    "extendedDescription": "Product Extended Description",
});

EXAMPLE RESPONSE
{
    "id": "6440",
    "description": "Product Test",
    "summary": "Summary Test",
    "extendedDescription": "Product Extended Description",
    "isExtendedDescriptionLocked": true,
    "iconImage": "iconImage.png",
    "mediumImage": "mediumImage.jpg",
    "keywords": "Test Keywords",
    "pageLayout": "PRODPACK2",
    "weight": "2"
}


```

Updates and publishes the specified product StudioOnline publish data by setting the values of the parameters passed. Any parameters not provided will be left unchanged. Any categories must already have been updated through the Product Codes resources. Any prices and components must already have been updated through their resources

##### Arguments

* description (optional) - The description for the product on StudioOnline.
* summary (optional) - The summary for the product on StudioOnline.
* extendedDescription (optional) - The extended description for the product on StudioOnline.
* updateImages (optional) - Whether or not to update the icon and medium images. If this is selected and the icon or medium image are not provided, they will be deleted.
* iconImage (optional) - The icon image for the product on StudioOnline.
* mediumImage (optional) - The medium image for the product on StudioOnline.
* keywords (optional) - The keywords for the product on StudioOnline.
* pageLayout (optional) - The page layout (XML Package) for the product on StudioOnline.

##### Returns

Returns the product StudioOnline publish data object if the update and publish succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined page layout code).

#### Unpublish the product StudioOnline publish data

```
DEFINITION
DELETE http://apiserver/products/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/7399/studioonlinepublishdata", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Unpublishes the product StudioOnline publish data. The actual data will not be deleted.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the product StudioOnline publish data cannot be unpublished, this call returns an error.

### Product Advanced StudioOnline Configuration

#### Create a product Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/products/:id/storeconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/products/110160/storeconfigurations", {
    "store": "19",
    "useInStudioOnline": true,
    "title": "Daily Devotions",
    "urlOverride": "daily-devotions",
    "description": "365 Daily Devotions"
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "product": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": null,
    "endDate": null,
    "hideFromSearch": false,
    "title": "Daily Devotions",
    "urlOverride": "daily-devotions",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "365 Daily Devotions",
    "keywords": null,
    "layoutOverride": null,
    "hasFreeShipping": false,
    "downloadUrl": null
}

```

Creates a new product Advanced StudioOnline configuration.

##### Arguments

* store (required) - The unique id of the store this configuration is for. Must be a valid store Id.
* title (required) - The online title for the product when used in the specified store.
* description (optional) - The online description for the product when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the product title.
* useInStudioOnline (optional) - Whether the product should be used in the specified store.
* startDate (optional) - The date the product will become visible in the specified store.
* endDate (optional) - The date the product will be removed from the specified store.
* hideFromSearch (optional) - Whether the product should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the product when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default product layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate product that should be shown in StudioOnline if someone tries to navigate to this product.
* hasFreeShipping (optional) - Whether this product is shipped free
* downloadUrl (optional) - The full CDN URL to the digital asset,if this is product is a digital download instead of a physical product.

##### Returns

Returns a product Advanced StudioOnline configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a product Advanced StudioOnline configuration

```
DEFINITION
GET http://apiserver/products/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/products/110160/storeconfigurations/10033");

EXAMPLE RESPONSE
{
    "id": "10033",
    "product": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": null,
    "endDate": null,
    "hideFromSearch": false,
    "title": "Daily Devotions",
    "urlOverride": "daily-devotions",
    "url": "https://www.myministry.com/purchase/daily-devotions",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "365 Daily Devotions",
    "keywords": null,
    "layoutOverride": null,
    "hasFreeShipping": false,
    "downloadUrl": null
}

```

Retrieves the details of a product Advanced StudioOnline configuration. You need only supply the product id and configuration id.

##### Returns

Returns a product Advanced StudioOnline configuration object if valid ids were provided.

#### Update a product Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/products/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/products/110160/storeconfigurations/10033", {
    "startDate": "2017-09-01",
    "endDate": "2018-10-25"
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "product": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2017-09-01",
    "endDate": "2018-10-25",
    "hideFromSearch": false,
    "title": "Daily Devotions",
    "urlOverride": "daily-devotions",
    "url": "https://www.myministry.com/purchase/daily-devotions",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "365 Daily Devotions",
    "keywords": null,
    "layoutOverride": null,
    "hasFreeShipping": false,
    "downloadUrl": null
}


```

Updates the specified product Advanced StudioOnline configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title (optional) - The online title for the product when used in the specified store.
* description (optional) - The online description for the product when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the product title.
* useInStudioOnline (optional) - Whether the product should be used in the specified store.
* startDate (optional) - The date the product will become visible in the specified store.
* endDate (optional) - The date the product will be removed from the specified store.
* hideFromSearch (optional) - Whether the product should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the product when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default product layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate product that should be shown in StudioOnline if someone tries to navigate to this product.
* hasFreeShipping (optional) - Whether this product is shipped free
* downloadUrl (optional) - The full CDN URL to the digital asset,if this is product is a digital download instead of a physical product.

##### Returns

Returns a product Advanced StudioOnline configuration object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid permanentRedirect).

#### Delete a product Advanced StudioOnline configuration

```
DEFINITION
DELETE http://apiserver/products/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/products/110160/storeconfigurations/10033", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product Advanced StudioOnline configuration. It cannot be undone.

##### Arguments

* id (required) - The product Advanced StudioOnline configuration id of the configuration to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product Advanced StudioOnline configuration does not exist, this call returns an error.

#### List all product Advanced StudioOnline configurations

```
DEFINITION
GET http://apiserver/products/:id/storeconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/products/110160/storeconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10033",
            "product": "110160",
            "store": "19",
            "storeDescription": "ASO US-English",
            "useInStudioOnline": true,
            "startDate": "2017-09-01",
            "endDate": "2018-10-25",
            "hideFromSearch": false,
            "title": "Daily Devotions",
            "urlOverride": "daily-devotions",
            "url": "https://www.myministry.com/purchase/daily-devotions",
            "permanentRedirect": null,
            "permanentRedirectDescription": null,
            "description": "365 Daily Devotions",
            "keywords": null,
            "layoutOverride": null,
            "hasFreeShipping": false,
            "downloadUrl": null
        }
        {...},
        {...}
    ]
}

```

Returns a list of all product Advanced StudioOnline configurations matching the provided filter criteria.

##### Arguments

* id () - Filter list by an exact match on configuration id
* store () - Filter list by an exact match on store id
* product () - Filter list by an exact match in product code

##### Returns

A dictionary with an items property that contains an array of up to limit product Advanced StudioOnline configurations, starting at index offset. Each entry in the array is a separate product Advanced StudioOnline configuration object. If no more product Advanced StudioOnline configurations are available, the resulting array will be empty. This request should never return an error.

### Product Advanced StudioOnline Store Is Shippable

#### Is product shippable

```
DEFINITION
GET http://apiserver/products/:id/stores/:id/isshippable

EXAMPLE REQUEST
$.get("http://localhost:49195/products/110160/stores/10033/isshippable");

EXAMPLE RESPONSE
{
    "isShippable": true
}

```

Retrieves the details of a whether a product for the Advanced StudioOnline store is shippable. You need only supply the product id and configuration id.

##### Returns

Returns a whether the product for the Advanced StudioOnline store is shippable object if valid ids were provided.

### Product Warehouses

#### Create a product warehouse

```
DEFINITION
POST http://apiserver/productwarehouses

EXAMPLE REQUEST
$.post("http://localhost:49195/productwarehouses", {
    "warehouse": "30",
    "product": "BK-5SLVG",
    "cost": 45,
    "canBackorder": true,
    "checkAvailability": true,
    "onOrderQuantity": 10,
    "reorderQuantity": 0
});

EXAMPLE RESPONSE
{
    "id": 71,
    "warehouse": "30",
    "warehouseDescription": "VOE Warehouse",
    "product": "BK-5SLVG",
    "productDescription": "5 Steps to Living (Set)",
    "productType": "K",
    "cost": 45,
    "canBackorder": false,
    "checkAvailability": false,
    "backorderQuantity": 0,
    "committedQuantity": null,
    "onHandQuantity": null,
    "onOrderQuantity": 10,
    "reorderQuantity": 0,
    "company": "CCONNECT",
    "companyDescription": "Card Connect, Inc."
}

```

Creates a new product warehouse object.

##### Arguments

* warehouse (required) - The warehouse code.
* product (required) - The product code.
* cost (required) - The cost of the product in the warehouse.
* canBackorder (required) - Whether the product can be backordered.
* checkAvailability (required) - Check availability for the product in the warehouse.
* onOrderQuantity (optional) - The on order quantity of the product in the warehouse.
* reorderQuantity (optional) - The reorder quantity of the product in the warehouse.

##### Returns

Returns a product warehouse object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid warehouse).

#### Retrieve a product warehouse

```
DEFINITION
GET http://apiserver/productwarehouses/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productwarehouses/71");

EXAMPLE RESPONSE
{
    "id": 71,
    "warehouse": "30",
    "warehouseDescription": "VOE Warehouse",
    "product": "BK-5SLVG",
    "productDescription": "5 Steps to Living (Set)",
    "productType": "K",
    "cost": 45,
    "canBackorder": false,
    "checkAvailability": false,
    "backorderQuantity": 0,
    "committedQuantity": null,
    "onHandQuantity": null,
    "onOrderQuantity": 10,
    "reorderQuantity": 0,
    "company": "CCONNECT",
    "companyDescription": "Card Connect, Inc."
}

```

Retrieves the details of an existing product warehouse. You need only supply the product code and warehouse code.

##### Arguments

* includeCombinedComponentCost (optional) - If true, the cost of the components of this product will be returned in the property 'combinedComponentCost'. (Only valid for product type `K` or `B`.)

##### Returns

Returns a product warehouse object if a valid id was provided.

#### Update a product warehouse

```
DEFINITION
POST http://apiserver/productwarehouses/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/product/warehouses/71", {
    "cost": 50
});

EXAMPLE RESPONSE
{
    "id": 71,
    "warehouse": "30",
    "warehouseDescription": "VOE Warehouse",
    "product": "BK-5SLVG",
    "productDescription": "5 Steps to Living (Set)",
    "productType": "K",
    "cost": 50,
    "canBackorder": false,
    "checkAvailability": false,
    "backorderQuantity": 0,
    "committedQuantity": null,
    "onHandQuantity": null,
    "onOrderQuantity": 10,
    "reorderQuantity": 0,
    "company": "CCONNECT",
    "companyDescription": "Card Connect, Inc."
}


```

Updates the specified product warehouse by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* cost (optional) - The cost of the product in the warehouse.
* canBackorder (optional) - Whether the product can be backordered.
* checkAvailability (optional) - Check availability for the product in the warehouse.
* onOrderQuantity (optional) - The on order quantity of the product in the warehouse.
* reorderQuantity (optional) - The reorder quantity of the product in the warehouse.

##### Returns

Returns the product warehouse object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product warehouse

```
DEFINITION
DELETE http://apiserver/productwarehouses/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/productwarehouses/71", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product warehouse. It cannot be undone.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the product warehouse does not exist, this call returns an error.

#### List all product warehouses

```
DEFINITION
GET http://apiserver/productwarehouses

EXAMPLE REQUEST
$.get("http://localhost:49195/productwarehouses?product=BK-5SLVG");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 479
    }
    "items": [
        {
            "id": 71,
            "warehouse": "30",
            "warehouseDescription": "VOE Warehouse",
            "product": "BK-5SLVG",
            "productDescription": "5 Steps to Living (Set)",
            "productType": "K",
            "cost": 50,
            "canBackorder": false,
            "checkAvailability": false,
            "backorderQuantity": 0,
            "committedQuantity": null,
            "onHandQuantity": null,
            "onOrderQuantity": 10,
            "reorderQuantity": 0,
            "company": "CCONNECT",
            "companyDescription": "Card Connect, Inc."
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product warehouses for the product code.

##### Arguments

* warehouse () - The warehouse code.
* product () - The product code.
* description () - The product description
* exactMatch () - Whether or not the arguments should be treated as exact matches instead of using a fuzzy search
* company (optional) - The SE company code.
* integrationCompany (optional) - The inventory integration's company. (Not the SE Company).

##### Returns

A dictionary with an items property that contains an array of up to limit product warehouses, starting at index offset. Each entry in the array is a separate product warehouse object. If no more product warehouses are available, the resulting array will be empty. This request should never return an error.

### Product Warehouse Locations

#### Create a product warehouse location

```
DEFINITION
POST http://apiserver/productwarehouses/:id/locations

EXAMPLE REQUEST
$.post("http://localhost:49195/productwarehouses/71/locations", {
    "location": "A4",
    "priority": 1,
    "restockPoint": 5
});

EXAMPLE RESPONSE
{
    "id": "473",
    "location": "A4",
    "priority": 1,
    "committedQuantity": 0,
    "onHandQuantity": 0,
    "restockPoint": 5,
    "printedQuantity": 0
}

```

Creates a new product warehouse object.

##### Arguments

* location (required) - The product's warehouse location.
* priority (required) - The priority of the product's warehouse location.
* restockPoint (optional) - The amount at which the product should be restocked in the warehouse location.

##### Returns

Returns a product warehouse location object if the call succeeded. Returns an error if create parameters are invalid (e.g. if a location or priority is not provided).

#### Retrieve a product warehouse location

```
DEFINITION
GET http://apiserver/productwarehouses/:id/locations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productwarehouses/71/locations/473");

EXAMPLE RESPONSE
{
    "id": "473",
    "location": "A4",
    "priority": 1,
    "committedQuantity": 0,
    "onHandQuantity": 0,
    "restockPoint": 5,
    "printedQuantity": 0
}

```

Retrieves the details of an existing product warehouse location. You need only supply the product code and warehouse code.

##### Arguments

##### Returns

Returns a product warehouse location object if a valid id was provided.

#### Update a product warehouse location

```
DEFINITION
POST http://apiserver/productwarehouses/:id/locations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productwarehouses/71/locations/:id", {
    "location": A5
});

EXAMPLE RESPONSE
{
    "id": "473",
    "location": "A5",
    "priority": 1,
    "committedQuantity": 0,
    "onHandQuantity": 0,
    "restockPoint": 5,
    "printedQuantity": 0
}


```

Updates the specified product warehouse location by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* location (optional) - The product's warehouse location.
* priority (optional) - The priority of the product's warehouse location.
* restockPoint (optional) - The amount at which the product should be restocked in the warehouse location.

##### Returns

Returns the product warehouse location object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a product warehouse location

```
DEFINITION
DELETE http://apiserver/productwarehouses/:id/locations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/productwarehouses/71/locations/473", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a product warehouse location. It cannot be undone.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the product warehouse location does not exist, this call returns an error.

#### List all product warehouse locations

```
DEFINITION
GET http://apiserver/productwarehouses/:id/locations

EXAMPLE REQUEST
$.get("http://localhost:49195/productwarehouses/71/locations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 479
    }
    "items": [
        {
            "id": "473",
            "location": "A5",
            "priority": 1,
            "committedQuantity": 0,
            "onHandQuantity": 0,
            "restockPoint": 5,
            "printedQuantity": 0
        },
        {...},
        {...}
    ]
}

```

Returns a list of all product warehouse locations for the product warehouse.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit product warehouse locations, starting at index offset. Each entry in the array is a separate product warehouse location object. If no more product warehouse locations are available, the resulting array will be empty. This request should never return an error.

### Purchase Orders

#### Create a purchase order

```
DEFINITION
POST http://apiserver/purchaseorders

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders", {
    "warehouse": "10",
    "product": "BK1002",
    "vendor": "BBPG",
    "expectedQuantity": 490,
    "price": 15,
    "note": "PO NOTES...",
    "expectedDate": "2014-09-16"
});

EXAMPLE RESPONSE
{
    "id": "74",
    "warehouse": "10",
    "warehouseDescription": "Fulfillment Center",
    "product": "BK1002",
    "productDescription": "So Long, Insecurity",
    "vendor": "BBPG",
    "vendorDescription": "Baker Books Publishing Group",
    "expectedQuantity": 490,
    "receivedQuantity": 383,
    "price": 15,
    "note": "PO NOTES...",
    "status": "O",
    "expectedDate": "2014-09-16",
    "vendorAccountNumber": 27874
}

```

Creates a new purchase order.

##### Arguments

* warehouse (required) - The warehouse of the purchase order.
* product (required) - The product of the purchase order.
* vendor (required) - The vendor of the purchase order.
* expectedQuantity (required) - The expected number of products in the purchase order.
* price (required) - The price of the product in the purchase order.
* note (optional) - A note to put on the purchase order
* expectedDate (optional) - The expected date of the purchase order. If not provided, will be set to current date.

##### Returns

Returns a purchase order object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a purchase order

```
DEFINITION
GET http://apiserver/purchaseorders/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/74");

EXAMPLE RESPONSE
{
    "id": "74",
    "warehouse": "10",
    "warehouseDescription": "Fulfillment Center",
    "product": "BK1002",
    "productDescription": "So Long, Insecurity",
    "vendor": "BBPG",
    "vendorDescription": "Baker Books Publishing Group",
    "expectedQuantity": 490,
    "receivedQuantity": 383,
    "price": 15,
    "note": "PO NOTES...",
    "status": "O",
    "expectedDate": "2014-09-16",
    "vendorAccountNumber": 27874
}

```

Retrieves the details of an existing purchase order. You need only supply the purchase order id.

##### Arguments

* includeVendorAddress (optional) - Whether or not the vendor address will be included in the response. If true, the following 5 entries may be returned: vendorAddressLine1, vendorAddressLine2, vendorAddressLine3, vendorAddressLine4, vendorAddressLine5.

##### Returns

Returns a purchase order object if a valid id was provided.

#### Update a purchase order

```
DEFINITION
POST http://apiserver/purchaseorders/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/74", {
    "expectedDate": "2014-09-30"
}
});

EXAMPLE RESPONSE
{
    "id": "74",
    "warehouse": "10",
    "warehouseDescription": "Fulfillment Center",
    "product": "BK1002",
    "productDescription": "So Long, Insecurity",
    "vendor": "BBPG",
    "vendorDescription": "Baker Books Publishing Group",
    "expectedQuantity": 490,
    "receivedQuantity": 383,
    "price": 15,
    "note": "PO NOTES...",
    "status": "O",
    "expectedDate": "2014-09-30",
    "vendorAccountNumber": 27874
}


```

Updates the specified purchase order by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* warehouse (optional) - The warehouse of the purchase order.
* product (optional) - The product of the purchase order.
* vendor (optional) - The vendor of the purchase order.
* expectedQuantity (optional) - The expected number of products in the purchase order.
* price (optional) - The price of the product in the purchase order.
* note (optional) - A note to put on the purchase order
* expectedDate (optional) - The expected date of the purchase order.
* status (optional) - The status of the purchase order. When status is `H`, can only change to `O` or `X`. When status is `O`, can only change to `H`, `C` or `X`. When status is `X` or `C`, the status cannot be changed.

##### Returns

Returns the purchase order object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a purchase order

```
DEFINITION
DELETE http://apiserver/purchaseorders/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/purchaseorders/74", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a purchase order. It cannot be undone.

##### Arguments

* id (required) - The id of the purchase order to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the purchase order does not exist, this call returns an error.

#### List all purchase orders

```
DEFINITION
GET http://apiserver/purchaseorders

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders?warehouse=*10*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "74",
            "warehouse": "10",
            "warehouseDescription": "Fulfillment Center",
            "product": "BK1002",
            "productDescription": "So Long, Insecurity",
            "vendor": "BBPG",
            "vendorDescription": "Baker Books Publishing Group",
            "expectedQuantity": 490,
            "receivedQuantity": 383,
            "price": 15,
            "note": "PO NOTES...",
            "status": "O",
            "expectedDate": "2014-09-30",
            "vendorAccountNumber": 27874
        },
        {...},
    ]
}

```

Returns a list of all purchase orders.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by the purchase order id
* product (optional) - Filter list by partial match of product.
* warehouse (optional) - Filter list by partial match of warehouse.
* vendor (optional) - Filter list by partial match of vendor.
* status (optional) - Filter list by the status.
* exactMatch (optional) - Whether or not the arguments should be treated as exact matches instead of using a fuzzy search.

##### Returns

A dictionary with an items property that contains an array of up to limit purchase orders, starting at index offset. Each entry in the array is a separate purchase order object. If no more purchase order are available, the resulting array will be empty. This request should never return an error.

#### Print a purchase order

```
DEFINITION
POST http://apiserver/purchaseorders/:id/print

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/123/print", {

});

EXAMPLE RESPONSE
{
    "purchaseOrderNumber": "123",
    "formType": "MYFORMTP",
    "formTypeDeliveryMethod": "NOTEMAIL",
    "document": {
        "fileName": "Purchase Order Merge Doc.docx",
        "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
        "file": "UEsDBBQAAgAIAKyDe1AemujtOQEAAHcCAAARAAAAZG9jUHJvcHMvY29yZS54bWyVUstOwzAQ/JXI98S..."
    },
    "errors": [{
        "document": {
            "id": "123",
            "sequenceNumber": 10,
            "documentAddress": "\\\\test\\path\\my-file.docx",
            "fileName": null,
            "fileMimeType": null,
            "reportId": null,
            "reportDescription": null
        },
        "message": "Could not find file '\\\\test\\path\\my-file.docx'."
    }]
}

```

Print a purchase order.

##### Arguments

* id (required) - The PurchaseOrderNumber of the Purchase Order to be printed.

##### Returns

This will perform the merge and return the Purchase Order object along with the generated document and any document errors. Returns an error if the Purchase Order print parameters are invalid.

### Purchase Order Attachments

#### Create a purchase order attachment

```
DEFINITION
POST http://apiserver/purchaseorders/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/attachments", {
    "type":"OTHER",
    "typeDescription":"Other",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new purchase order attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a purchase order attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve a purchase order attachment

```
DEFINITION
GET http://apiserver/purchaseorders/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/attachments/117");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing purchase order attachment. You need only supply the purchase order attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a purchase order attachment object if a valid id was provided.

#### Update a purchase order attachment

```
DEFINITION
POST http://apiserver/purchaseorders/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/attachments/117", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified purchase order attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the purchase order attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined purchase order attachment type code).

#### Delete a purchase order attachment

```
DEFINITION
DELETE http://apiserver/purchaseorders/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/purchaseorders/10/attachments/117", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a purchase order attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the purchase order attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the purchase order attachment id does not exist, this call returns an error.

#### List all purchase order attachments

```
DEFINITION
GET http://apiserver/purchaseorders/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
                "longComment": "long comment text",
                "dateCreated": "2018-03-12",
                "id": "117",
                "type": "LOGO",
                "typeDescription": "Logo",
                "url": null,
                "fileName": "logo64.png",
                "file": null,
                "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all purchase order attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit purchase order attachments, starting at index offset. Each entry in the array is a separate purchase order attachment object. If no more purchase order attachments are available, the resulting array will be empty. This request should never return an error.

### Purchase Order codes

#### Create a purchase order code

```
DEFINITION
POST http://apiserver/purchaseorders/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/codes", {
    "type": "POCODE1",
    "value": "VAL1"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "POCODE1",
    "typeDescription": "PO Code 1",
    "value": "VAL1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Creates a new purchase order code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a purchase order code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a purchase order code

```
DEFINITION
GET http://apiserver/purchaseorders/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/codes/8096");

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "POCODE1",
    "typeDescription": "PO Code 1",
    "value": "VAL1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Retrieves the details of an existing purchase order code. You need only supply the purchase order code id.

##### Arguments

* id (required) - The id of the purchase order code to retrieve.

##### Returns

Returns a purchase order code object if a valid id was provided.

#### Update a purchase order code

```
DEFINITION
POST http://apiserver/purchaseorders/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10106/codes/8096", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "POCODE1",
    "typeDescription": "PO Code 1",
    "value": "VAL1",
    "valueDescription": "Value 1",
    "isActive": false
}


```

Updates the specified purchase order code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the purchase order code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a purchase order code

```
DEFINITION
DELETE http://apiserver/purchaseorders/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/purchaseorders/10/codes/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a purchase order code. It cannot be undone.

##### Arguments

* id (required) - The id of the purchase order code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the purchase order code id does not exist, this call returns an error.

#### List all purchase order codes

```
DEFINITION
GET http://apiserver/purchaseorders/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "8096",
            "type": "POCODE1",
            "typeDescription": "PO Code 1",
            "value": "VAL1",
            "valueDescription": "Value 1",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all purchase order codes.

##### Returns

A dictionary with an items property that contains an array of up to limit purchase order codes, starting at index offset. Each entry in the array is a separate purchase order code object. If no more purchase order codes are available, the resulting array will be empty. This request should never return an error.

### Purchase Order Dates

#### Create a purchase order date

```
DEFINITION
POST http://apiserver/purchaseorders/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/dates", {
    "type": "PODATE1",
    "value": "2012-05-17"
});

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "PODATE1",
    "typeDescription": "PO Date 1"
    "value": "2012-05-17",
    "isActive": true
}

```

Creates a new purchase order date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a purchase order date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve a purchase order date

```
DEFINITION
GET http://apiserver/purchaseorders/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/dates/1601");

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "PODATE1",
    "typeDescription": "PO Date 1"
    "value": "2012-05-17",
    "isActive": true
}

```

Retrieves the details of an existing purchase order date. You need only supply the purchase order date id.

##### Arguments

* id (required) - The id of the purchase order date to retrieve.

##### Returns

Returns a purchase order date object if a valid id was provided.

#### Update a purchase order date

```
DEFINITION
POST http://apiserver/purchaseorders/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/dates/1601", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "PODATE1",
    "typeDescription": "PO Date 1"
    "value": "2012-05-17",
    "isActive": false
}


```

Updates the specified purchase order date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the purchase order date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a purchase order date

```
DEFINITION
DELETE http://apiserver/purchaseorders/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/purchaseorders/10/dates/1601", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a purchase order date. It cannot be undone.

##### Arguments

* id (required) - The id of the purchase order date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the purchase order date id does not exist, this call returns an error.

#### List all purchase order dates

```
DEFINITION
GET http://apiserver/purchaseorders/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "1601",
            "type": "PODATE1",
            "typeDescription": "PO Date 1"
            "value": "2012-05-17",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all purchase order dates.

##### Returns

A dictionary with an items property that contains an array of up to limit purchase order dates, starting at index offset. Each entry in the array is a separate purchase order date object. If no more purchase order dates are available, the resulting array will be empty. This request should never return an error.

### Purchase Order Notes

#### Create a purchase order note

```
DEFINITION
POST http://apiserver/purchaseorders/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/notes", {
    "type": "PODESC",
    "shortComment": "Buy More Paper"
});

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "PODESC",
    "typeDescription": "PO description"
    "shortComment": "Buy More Paper",
    "longComment": null
}

```

Creates a new purchase order note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a purchase order note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a purchase order note

```
DEFINITION
GET http://apiserver/purchaseorders/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/notes/5054");

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "PODESC",
    "typeDescription": "PO description"
    "shortComment": "Buy More Paper",
    "longComment": null
}

```

Retrieves the details of an existing purchase order note. You need only supply the purchase order note id.

##### Arguments

* id (required) - The id of the purchase order note to retrieve.

##### Returns

Returns a purchase order note object if a valid id was provided.

#### Update a purchase order note

```
DEFINITION
POST http://apiserver/purchaseorders/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/notes/5054", {
    "shortComment": null,
    "longComment": "Buy More Paper"
});

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "PODESC",
    "typeDescription": "PO description"
    "shortComment": null,
    "longComment": "Buy More Paper"
}


```

Updates the specified purchase order note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the purchase order note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a purchase order note

```
DEFINITION
DELETE http://apiserver/purchaseorders/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/purchaseorders/10/notes/5054", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a purchase order note. It cannot be undone.

##### Arguments

* id (required) - The id of the purchase order note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the purchase order note id does not exist, this call returns an error.

#### List all purchase order notes

```
DEFINITION
GET http://apiserver/purchaseorders/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5054",
            "type": "PODESC",
            "typeDescription": "PO description"
            "shortComment": null,
            "longComment": "Buy More Paper"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all purchase order notes.

##### Returns

A dictionary with an items property that contains an array of up to limit purchase order notes, starting at index offset. Each entry in the array is a separate purchase order note object. If no more purchase order notes are available, the resulting array will be empty. This request should never return an error.

### Purchase Order Numbers

#### Create a purchase order number

```
DEFINITION
POST http://apiserver/purchaseorders/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/numbers", {
    "type": "PONUM",
    "value": 123
});

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "PONUM",
    "typeDescription": "PO Number"
    "value": 123,
    "isActive": true
}

```

Creates a new purchase order number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a purchase order number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a purchase order number

```
DEFINITION
GET http://apiserver/purchaseorders/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/numbers/828");

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "PONUM",
    "typeDescription": "PO Number"
    "value": 123,
    "isActive": true
}

```

Retrieves the details of an existing purchase order number. You need only supply the purchase order number id.

##### Arguments

* id (required) - The id of the purchase order number to retrieve.

##### Returns

Returns a purchase order number object if a valid id was provided.

#### Update a purchase order number

```
DEFINITION
POST http://apiserver/purchaseorders/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/purchaseorders/10/numbers/828", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "PONUM",
    "typeDescription": "PO Number"
    "value": 123,
    "isActive": false
}


```

Updates the specified purchase order number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the purchase order number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a purchase order number

```
DEFINITION
DELETE http://apiserver/purchaseorders/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/purchaseorders/10/numbers/828", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a purchase order number. It cannot be undone.

##### Arguments

* id (required) - The id of the purchase order number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the purchase order number id does not exist, this call returns an error.

#### List all purchase order numbers

```
DEFINITION
GET http://apiserver/purchaseorders/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/purchaseorders/10/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "828",
            "type": "PONUM",
            "typeDescription": "PO Number"
            "value": 123,
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all purchase order numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit purchase order numbers, starting at index offset. Each entry in the array is a separate purchase order number object. If no more purchase order numbers are available, the resulting array will be empty. This request should never return an error.

### RMAs

#### Create an RMA

```
DEFINITION
POST http://apiserver/rmas

EXAMPLE REQUEST
$.post("http://localhost:49195/rmas", {
    "account": "27416",
    "source": "072711",
    "company": "1",
    "warehouse": "10",
    "expectedReceiveDate": "2013-12-18"
});

EXAMPLE RESPONSE
{
    "id": "13",
    "status": "I",
    "statusDescription": "Initiated",
    "account": "27416",
    "accountName": "Jones Foundation",
    "source": "072711",
    "sourceDescription": "New Accounts",
    "company": "1",
    "companyDescription": "SON Media",
    "warehouse": "10",
    "warehouseDescription": "Fulfillment Center",
    "transactionDate": null,
    "expectedReceiveDate": "2013-12-18",
    "shortComment": null,
    "longComment": null,
    "documentNumber": null
}

```

Creates a new RMA.

##### Arguments

* account (required) - The account of the RMA.
* source (optional) - The source of the RMA.
* company (optional) - The company of the RMA.
* warehouse (optional) - The warehouse of the RMA.
* expectedReceiveDate (optional) - The date products are expected to be received for the RMA.
* shortComment (optional) - Short comment of the RMA.
* longComment (optional) - Long comment of the RMA.

##### Returns

Returns an RMA object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an RMA

```
DEFINITION
GET http://apiserver/rmas/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/rmas/13");

EXAMPLE RESPONSE
{
    "id": "13",
    "status": "I",
    "statusDescription": "Initiated",
    "account": "27416",
    "accountName": "Jones Foundation",
    "source": "072711",
    "sourceDescription": "New Accounts",
    "company": "1",
    "companyDescription": "SON Media",
    "warehouse": "10",
    "warehouseDescription": "Fulfillment Center",
    "transactionDate": null,
    "expectedReceiveDate": "2013-12-18",
    "shortComment": null,
    "longComment": null,
    "documentNumber": null
}

```

Retrieves the details of an existing RMA. You need only supply the RMA id.

##### Arguments

##### Returns

Returns an RMA object if a valid id was provided.

#### Update an RMA

```
DEFINITION
POST http://apiserver/rmaa/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/rmaa/13", {
    "shortComment": "RMA for ABC Booklet"
}
});

EXAMPLE RESPONSE
{
    "id": "13",
    "status": "I",
    "statusDescription": "Initiated",
    "account": "27416",
    "accountName": "Jones Foundation",
    "source": "072711",
    "sourceDescription": "New Accounts",
    "company": "1",
    "companyDescription": "SON Media",
    "warehouse": "10",
    "warehouseDescription": "Fulfillment Center",
    "transactionDate": null,
    "expectedReceiveDate": "2013-12-18",
    "shortComment": "RMA for ABC Booklet",
    "longComment": null,
    "documentNumber": null
}


```

Updates the specified RMA by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* account (optional) - The account of the RMA.
* status (optional) - The status of the RMA. (Possible values: `I` (Initiated), `A` (Cost Approved), `R` (Product Received), `F` (Credit Finalized) )
* source (optional) - The source of the RMA.
* company (optional) - The company of the RMA.
* warehouse (optional) - The warehouse of the RMA.
* expectedReceiveDate (optional) - The date products are expected to be received for the RMA.
* shortComment (optional) - Short comment of the RMA.
* longComment (optional) - Long comment of the RMA.

##### Returns

Returns the RMA object if the update succeeded. Returns an error if update parameters are invalid or if the status is `F`.

#### Delete an RMA

```
DEFINITION
DELETE http://apiserver/rmas/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/rmas/13", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an RMA. It cannot be undone.

##### Arguments

* id (required) - The id of the RMA to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the RMA has a status of `F`, this call returns an error.

#### List all RMAs

```
DEFINITION
GET http://apiserver/rmas

EXAMPLE REQUEST
$.get("http://localhost:49195/rmas?warehouse=*10*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "74",
            "warehouse": "10",
            "warehouseDescription": "Fulfillment Center",
            "product": "BK1002",
            "productDescription": "So Long, Insecurity",
            "vendor": "BBPG",
            "vendorDescription": "Baker Books Publishing Group",
            "expectedQuantity": 490,
            "receivedQuantity": 383,
            "price": 15,
            "note": "PO NOTES...",
            "status": "O",
            "expectedDate": "2014-09-30"
        },
        {...},
    ]
}

```

Returns a list of all RMAs.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by the RMA id
* account (optional) - Filter list by the account number
* source (optional) - Filter list by the source
* company (optional) - Filter list by the company
* warehouse (optional) - Filter list by the warehouse
* transationDate (optional) - Filter by the transaction date
* expectedReceiveDate (optional) - Filter by the expected receive date
* shortComment (optional) - Filter list by the shortComment
* longComment (optional) - Filter list by the the longComment
* documentNumber (optional) - Filter list by the document number
* status (optional) - Filter list by the status (can put multiple statuses together to find multiple, like `IAR`)

##### Returns

A dictionary with an items property that contains an array of up to limit RMAs, starting at index offset. Each entry in the array is a separate RMA object. If no more RMAs are available, the resulting array will be empty. This request should never return an error.

### RMA Details

#### Create an RMA detail

```
DEFINITION
POST http://apiserver/rmas/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/rmas/13/details", {
    "product": "100STPR1",
    "price": 7.50,
    "quantityExpected": 125,
    "cost": 5.00
});

EXAMPLE RESPONSE
{
    "id": "25",
    "product": "100STPR1",
    "productDescription": "ABC Booklet",
    "location": null,
    "referenceNumber": null,
    "price": 7.5,
    "quantityExpected": 125,
    "cost": 5,
    "quantityReceived": null,
    "quantityUsable": null
}

```

Creates a new RMA Detail.

##### Arguments

* product (required) - The product of the RMA detail.
* price (required) - The price of the product.
* quantityExpected (required) - The expected quantity returned of the product.
* cost (required) - The cost of the product.
* location (optional) - The location in the warehouse of the product.
* referenceNumber (optional) - The reference number of the RMA detail.

##### Returns

Returns an RMA detail object if the call succeeded. Returns an error if create parameters are invalid. If the RMA status of the RMA detail is not `I` (Initiated), this call returns an error.

#### Retrieve an RMA detail

```
DEFINITION
GET http://apiserver/rmas/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/rmas/13/details/25");

EXAMPLE RESPONSE
{
    "id": "25",
    "product": "100STPR1",
    "productDescription": "ABC Booklet",
    "location": null,
    "referenceNumber": null,
    "price": 7.5,
    "quantityExpected": 125,
    "cost": 5,
    "quantityReceived": null,
    "quantityUsable": null
}

```

Retrieves the details of an existing RMA detail. You need only supply the RMA detail id.

##### Arguments

##### Returns

Returns an RMA detail object if a valid id was provided.

#### Update an RMA detail

```
DEFINITION
POST http://apiserver/rmas/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/rmas/13/details/25", {
    "location": "1"
}
});

EXAMPLE RESPONSE
{
    "id": "25",
    "product": "100STPR1",
    "productDescription": "ABC Booklet",
    "location": "1",
    "referenceNumber": null,
    "price": 7.5,
    "quantityExpected": 125,
    "cost": 5,
    "quantityReceived": null,
    "quantityUsable": null
}


```

Updates the specified RMA by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* product (optional) - The product of the RMA detail.
* price (optional) - The price of the product.
* quantityExpected (optional) - The expected quantity returned of the product.
* cost (optional) - The cost of the product.
* location (optional) - The location in the warehouse of the product.
* referenceNumber (optional) - The reference number of the RMA detail.
* quantityReceived (optional) - The actual quantity received of the product. (Can only be set when status of the RMA is `A` (Cost Approved))
* quantityUsable (optional) - The quantity of received products that can be used/sold again. (Can only be set when status of the RMA is `A` (Cost Approved))

##### Returns

Returns the RMA detail object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an RMA detail

```
DEFINITION
DELETE http://apiserver/rmas/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/rmas/13/details/25", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an RMA detail. It cannot be undone.

##### Arguments

* id (required) - The id of the RMA detail to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the RMA status of the RMA detail is not `I` (Initiated), this call returns an error.

#### List all RMA Details

```
DEFINITION
GET http://apiserver/rmas/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/rmas/13/details?product=100*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "25",
            "product": "100STPR1",
            "productDescription": "ABC Booklet",
            "location": "1",
            "referenceNumber": null,
            "price": 7.5,
            "quantityExpected": 125,
            "cost": 5,
            "quantityReceived": null,
            "quantityUsable": null
        },
        {...},
    ]
}

```

Returns a list of all RMA details.

##### Arguments

* id (optional) - Filter list by the RMA detail id
* product (optional) - List list by the product
* location (optional) - List list by the location
* referenceNumber (optional) - List list by the reference number
* price (optional) - List list by the price
* quantityExpected (optional) - List list by the quantityExpected
* cost (optional) - List list by the cost
* quantityReceived (optional) - List list by the quantityReceived
* quantityUsable (optional) - List list by the quantityUsable

##### Returns

A dictionary with an items property that contains an array of up to limit RMA details, starting at index offset. Each entry in the array is a separate RMA detail object. If no more RMA details are available, the resulting array will be empty. This request should never return an error.

### Variant Groups

#### Create a variant group

```
DEFINITION
POST http://apiserver/variantgroups

EXAMPLE REQUEST
$.post("http://localhost:49195/variantgroups", {
    "code": "CONFTSHIRT",
    "store": "1",
    "description": "Conference T-Shirt"
});

EXAMPLE RESPONSE
{
    "id": "123",
    "code": "CONFTSHIRT",
    "description": "Conference TShirt",
    "store": "1",
    "storeDescription": "Advanced StudioOnline"
}

```

Creates a new variant group.

##### Arguments

* code (required) - The code for the variant group.
* description (required) - The description for the variant group.
* store (required) - Store Id for the variant group.

##### Returns

Returns a variant group object if the call succeeded. Returns an error if create parameters are invalid. A variant group is unique across code and store.

#### Retrieve a variant group

```
DEFINITION
GET http://apiserver/variantgroups/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/variantgroups/123");

EXAMPLE RESPONSE
{
    "id": "123",
    "code": "CONFTSHIRT",
    "description": "Conference TShirt",
    "store": "1",
    "storeDescription": "Advanced StudioOnline"
}

```

Retrieves the details of an existing variant group. You need only supply the id.

##### Arguments

* id (required) - The id of the variant group to be retrieved.

#### Update a variant group

```
DEFINITION
POST http://apiserver/variantgroups/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/variantgroups/123", {
    "description": "Conference T-Shirt"
});

EXAMPLE RESPONSE
{
    "id": "123",
    "code": "CONFTSHIRT",
    "description": "Conference T-Shirt",
    "store": "1",
    "storeDescription": "Advanced StudioOnline"
}


```

Updates the specified variant group by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description for the Variant Group.

##### Returns

Returns the variant group object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a variant group

```
DEFINITION
DELETE http://apiserver/variantgroups/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/variantgroups/123", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a variant group. It cannot be undone.

##### Arguments

* id (required) - The id of the variant group to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the variant group does not exist, this call returns an error.

#### List all variant groups

```
DEFINITION
GET http://apiserver/variantgroups

EXAMPLE REQUEST
$.get("http://localhost:49195/variantgroups?description=*Shirt*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "123",
            "code": "CONFTSHIRT",
            "description": "Conference T-Shirt",
            "store": "1",
            "storeDescription": "Advanced StudioOnline"
        },
        {...},
    ]
}

```

Returns a list of all variant groups.

##### Arguments

* code (optional) - Filter list by partial match on the code of the variant group.
* description (optional) - Filter list by partial match on the description of the variant group.
* store (optional) - Filter list by the code of the variant group.

##### Returns

A dictionary with an items property that contains an array of up to limit variant groups, starting at index offset. Each entry in the array is a separate variant group object. If no more variant groups are available, the resulting array will be empty. This request should never return an error.

### Variant Group Products

#### Create a variant group product

```
DEFINITION
POST http://apiserver/variantgroups/:variantGroupId/productvariants

EXAMPLE REQUEST
$.post("http://localhost:49195/variantgroups/123/productvariants", {
    "productCode": "SHIRT1000",
    "sequenceNumber": 1
});

EXAMPLE RESPONSE
{
    "id": "5",
    "code": "CONFTSHIRT",
    "description": "Conference TShirt",
    "productCode": "SHIRT1000",
    "productDescription": "Small Conference T-Shirt",
    "sequenceNumber": 1
}

```

Creates a new variant group product.

##### Arguments

* productCode (required) - The product code for the variant group product.
* sequenceNumber (required) - Sequence number for the order of the variant group product.

##### Returns

Returns a variant group product object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a variant group product

```
DEFINITION
GET http://apiserver/variantgroups/:variantGroupId/productvariants/:productVariantId

EXAMPLE REQUEST
$.get("http://localhost:49195/variantgroups/123/productvariants/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "code": "CONFTSHIRT",
    "description": "Conference TShirt",
    "productCode": "SHIRT1000",
    "productDescription": "Small Conference T-Shirt",
    "sequenceNumber": 1
}

```

Retrieves the details of an existing variant group product. You need only supply the id.

##### Arguments

* variantGroupId (required) - The id of the variant group of the product variant product to be retrieved.
* productVariantId (require) - The id of the product variant product to be retrieved.

#### Update a variant group product

```
DEFINITION
POST http://apiserver/variantgroups/:variantGroupId/productvariants/:productVariantId

EXAMPLE REQUEST
$.post("http://localhost:49195/variantgroups/123/productvariants/5", {
    "sequenceNumber": "3"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "code": "CONFTSHIRT",
    "description": "Conference TShirt",
    "productCode": "SHIRT1000",
    "productDescription": "Small Conference T-Shirt",
    "sequenceNumber": 3
}


```

Updates the specified variant group product by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* productCode (optional) - The product code for the variant group product.
* sequenceNumber (optional) - Sequence number for the order of the variant group product.

##### Returns

Returns the variant group product object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a variant group product

```
DEFINITION
DELETE http://apiserver/variantgroups/:variantGroupId/productvariants/:productVariantId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/variantgroups/123/productvariants/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a variant group product. It cannot be undone.

##### Arguments

* id (required) - The id of the variant group product to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the variant group does not exist, this call returns an error.

#### List all variant group products

```
DEFINITION
GET http://apiserver/variantgroups/:variantGroupId/productvariants

EXAMPLE REQUEST
$.get("http://localhost:49195/variantgroups/123/productvariants");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5",
            "code": "CONFTSHIRT",
            "description": "Conference TShirt",
            "productCode": "SHIRT1000",
            "productDescription": "Small Conference T-Shirt",
            "sequenceNumber": 3
        },
        {...},
    ]
}

```

Returns a list of all variant group products for a variant group.

##### Returns

A dictionary with an items property that contains an array of up to limit variant group products, starting at index offset. Each entry in the array is a separate variant grou product object. If no more variant group products are available, the resulting array will be empty. This request should never return an error.

### Vendors

#### Create a vendor

```
DEFINITION
POST http://apiserver/vendors

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors", {
    "vendor": "CBO",
    "description": "Christian Book Distributors",
    "isActive": true,
    "mailingAddress": {
        "line1": "1234 Main Street",
        "state": "TX",
        "postalCode": "75080",
        "city": "Richardson",
        "country": "USA"
    }
});

EXAMPLE RESPONSE
{
    "id": "10029",
    "vendor": "CBO",
    "description": "Christian Book Distributors",
    "account": "27874",
    "isActive": true,
    "mailingAddress": {
        "id": "1000028072",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000028073",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000028074",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    }
}

```

Creates a new vendor.

##### Arguments

* vendor (required) - The vendor Id.
* description (optional) - The vendor name (will be sent from `vendor` if not supplied).
* mailingAddress (optional) - The mailing address of the vendor. country are required. postalCode and state must be valid for the country and postalCode is required for some countries. city, line1, line2, line3, and line4 are optional. At least one of mailingAddress, billingAddress or shippingAddress are required.
* billingAddress (optional) - The billing address of the vendor. Set to null or do not provide to use the mailingAddress for billingAddress as well.
* shippingAddress (optional) - The shipping address of the vendor. Set to null or do not provide to use the mailingAddress for shippingAddress as well.

##### Returns

Returns a vendor object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a vendor

```
DEFINITION
GET http://apiserver/vendors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/vendor/10029");

EXAMPLE RESPONSE
{
    "id": "10029",
    "vendor": "CBO",
    "description": "Christian Book Distributors",
    "account": "27874",
    "isActive": true,
    "mailingAddress": {
        "id": "1000028072",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000028073",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000028074",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    }
}

```

Retrieves the details of an existing vendor. You need only supply the id.

##### Arguments

* id (required) - The id of the vendor to be retrieved.

#### Update a vendor

```
DEFINITION
POST http://apiserver/vendors/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10029", {
    "billingAddress": {
        "line1": "789 Main Street",
        "postalCode": "75098",
        "city": "Wylie",
        "country": "USA"
    }
}
});

EXAMPLE RESPONSE
{
    "id": "10029",
    "vendor": "CBO2",
    "description": "Christian Book Distributors2",
    "account": "27874",
    "isActive": true,
    "mailingAddress": {
        "id": "1000028072",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000028075",
        "line1": "789 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Wylie",
        "state": "TX",
        "postalCode": "75098",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000028074",
        "line1": "1234 Main Street",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    }
}


```

Updates the specified vendor by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* vendor (optional) - The vendor Id.
* description (optional) - The vendor name.
* mailingAddress (optional) - The mailing address of the vendor. country are required. postalCode and state must be valid for the country and postalCode is required for some countries. city, line1, line2, line3, and line4 are optional.
* billingAddress (optional) - The billing address of the vendor.
* shippingAddress (optional) - The shipping address of the vendor.

##### Returns

Returns the vendor object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a vendor

```
DEFINITION
DELETE http://apiserver/vendors/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/vendors/10029", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a vendor. It cannot be undone.

##### Arguments

* id (required) - The id of the vendor to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the vendor does not exist, this call returns an error.

#### List all vendors

```
DEFINITION
GET http://apiserver/vendors

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors?description=*Book*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10029",
            "vendor": "CBO",
            "description": "Christian Book Distributors",
            "account": "27874",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all vendors.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* vendor (optional) - Filter list by partial match of vendor id.
* description (optional) - Filter list by partial match of description.
* isActive (optional) - Filter list by whether the vendor is active or not.
* lastName (optional) - Filter list by partial match of any contact with the last name.
* firstName (optional) - Filter list by partial match of any contact with the first name.

##### Returns

A dictionary with an items property that contains an array of up to limit vendors, starting at index offset. Each entry in the array is a separate vendor object. If no more vendors are available, the resulting array will be empty. This request should never return an error.

### Vendor Attachments

#### Create a vendor attachment

```
DEFINITION
POST http://apiserver/vendors/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/attachments", {
    "type":"OTHER",
    "typeDescription":"Other",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new vendor attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a vendor attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve a vendor attachment

```
DEFINITION
GET http://apiserver/vendors/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/attachments/117");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing vendor attachment. You need only supply the vendor attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a vendor attachment object if a valid id was provided.

#### Update a vendor attachment

```
DEFINITION
POST http://apiserver/vendors/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/attachments/117", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified vendor attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the vendor attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined vendor attachment type code).

#### Delete a vendor attachment

```
DEFINITION
DELETE http://apiserver/vendors/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/vendors/10/attachments/117", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a vendor attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the vendor attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the vendor attachment id does not exist, this call returns an error.

#### List all vendor attachments

```
DEFINITION
GET http://apiserver/vendors/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
                "longComment": "long comment text",
                "dateCreated": "2018-03-12",
                "id": "117",
                "type": "LOGO",
                "typeDescription": "Logo",
                "url": null,
                "fileName": "logo64.png",
                "file": null,
                "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all vendor attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit vendor attachments, starting at index offset. Each entry in the array is a separate vendor attachment object. If no more vendor attachments are available, the resulting array will be empty. This request should never return an error.

### Vendor codes

#### Create a vendor code

```
DEFINITION
POST http://apiserver/vendors/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/codes", {
    "type": "VENDCODE1",
    "value": "PART"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "VENDCODE1",
    "typeDescription": "Vendor Return Policies",
    "value": "PART",
    "valueDescription": "Partial Returns Allowed",
    "isActive": true
}

```

Creates a new vendor code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a vendor code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a vendor code

```
DEFINITION
GET http://apiserver/vendors/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/codes/8096");

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "VENDCODE1",
    "typeDescription": "Vendor Return Policies",
    "value": "PART",
    "valueDescription": "Partial Returns Allowed",
    "isActive": true
}

```

Retrieves the details of an existing vendor code. You need only supply the vendor code id.

##### Arguments

* id (required) - The id of the vendor code to retrieve.

##### Returns

Returns a vendor code object if a valid id was provided.

#### Update a vendor code

```
DEFINITION
POST http://apiserver/vendors/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10106/codes/8096", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "VENDCODE1",
    "typeDescription": "Vendor Return Policies",
    "value": "PART",
    "valueDescription": "Partial Returns Allowed",
    "isActive": false
}


```

Updates the specified vendor code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the vendor code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a vendor code

```
DEFINITION
DELETE http://apiserver/vendors/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/vendors/10/codes/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a vendor code. It cannot be undone.

##### Arguments

* id (required) - The id of the vendor code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the vendor code id does not exist, this call returns an error.

#### List all vendor codes

```
DEFINITION
GET http://apiserver/vendors/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "8096",
            "type": "VENDCODE1",
            "typeDescription": "Vendor Return Policies",
            "value": "PART",
            "valueDescription": "Partial Returns Allowed",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all vendor codes.

##### Returns

A dictionary with an items property that contains an array of up to limit vendor codes, starting at index offset. Each entry in the array is a separate vendor code object. If no more vendor codes are available, the resulting array will be empty. This request should never return an error.

### Vendor Dates

#### Create a vendor date

```
DEFINITION
POST http://apiserver/vendors/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/dates", {
    "type": "VENDDATE1",
    "value": "2012-05-17"
});

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "VENDDATE1",
    "typeDescription": "Vendor Re-Evaluation Date"
    "value": "2012-05-17",
    "isActive": true
}

```

Creates a new vendor date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a vendor date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve a vendor date

```
DEFINITION
GET http://apiserver/vendors/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/dates/1601");

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "VENDDATE1",
    "typeDescription": "Vendor Re-Evaluation Date"
    "value": "2012-05-17",
    "isActive": true
}

```

Retrieves the details of an existing vendor date. You need only supply the vendor date id.

##### Arguments

* id (required) - The id of the vendor date to retrieve.

##### Returns

Returns a vendor date object if a valid id was provided.

#### Update a vendor date

```
DEFINITION
POST http://apiserver/vendors/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/dates/1601", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "VENDDATE1",
    "typeDescription": "Vendor Re-Evaluation Date"
    "value": "2012-05-17",
    "isActive": false
}


```

Updates the specified vendor date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the vendor date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a vendor date

```
DEFINITION
DELETE http://apiserver/vendors/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/vendors/10/dates/1601", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a vendor date. It cannot be undone.

##### Arguments

* id (required) - The id of the vendor date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the vendor date id does not exist, this call returns an error.

#### List all vendor dates

```
DEFINITION
GET http://apiserver/vendors/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "1601",
            "type": "VENDDATE1",
            "typeDescription": "Vendor Re-Evaluation Date"
            "value": "2012-05-17",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all vendor dates.

##### Returns

A dictionary with an items property that contains an array of up to limit vendor dates, starting at index offset. Each entry in the array is a separate vendor date object. If no more vendor dates are available, the resulting array will be empty. This request should never return an error.

### Vendor Notes

#### Create a vendor note

```
DEFINITION
POST http://apiserver/vendors/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/notes", {
    "type": "VENDDESC",
    "shortComment": "Supplies office supplies"
});

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "VENDDESC",
    "typeDescription": "Vendor description"
    "shortComment": "Supplies office supplies",
    "longComment": null
}

```

Creates a new vendor note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a vendor note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a vendor note

```
DEFINITION
GET http://apiserver/vendors/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/notes/5054");

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "VENDDESC",
    "typeDescription": "Vendor description"
    "shortComment": "Supplies office supplies",
    "longComment": null
}

```

Retrieves the details of an existing vendor note. You need only supply the vendor note id.

##### Arguments

* id (required) - The id of the vendor note to retrieve.

##### Returns

Returns a vendor note object if a valid id was provided.

#### Update a vendor note

```
DEFINITION
POST http://apiserver/vendors/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/notes/5054", {
    "shortComment": null,
    "longComment": "Supplies office supplies"
});

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "VENDDESC",
    "typeDescription": "Vendor description"
    "shortComment": null,
    "longComment": "Supplies office supplies"
}


```

Updates the specified vendor note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the vendor note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a vendor note

```
DEFINITION
DELETE http://apiserver/vendors/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/vendors/10/notes/5054", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a vendor note. It cannot be undone.

##### Arguments

* id (required) - The id of the vendor note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the vendor note id does not exist, this call returns an error.

#### List all vendor notes

```
DEFINITION
GET http://apiserver/vendors/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5054",
            "type": "VENDDESC",
            "typeDescription": "Vendor description"
            "shortComment": null,
            "longComment": "Supplies office supplies"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all vendor notes.

##### Returns

A dictionary with an items property that contains an array of up to limit vendor notes, starting at index offset. Each entry in the array is a separate vendor note object. If no more vendor notes are available, the resulting array will be empty. This request should never return an error.

### Vendor Numbers

#### Create a vendor number

```
DEFINITION
POST http://apiserver/vendors/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/numbers", {
    "type": "VENQUAN",
    "value": 123
});

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "VENQUAN",
    "typeDescription": "Vendor Quantity"
    "value": 123,
    "isActive": true
}

```

Creates a new vendor number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a vendor number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a vendor number

```
DEFINITION
GET http://apiserver/vendors/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/numbers/828");

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "VENQUAN",
    "typeDescription": "Vendor Quantity"
    "value": 123,
    "isActive": true
}

```

Retrieves the details of an existing vendor number. You need only supply the vendor number id.

##### Arguments

* id (required) - The id of the vendor number to retrieve.

##### Returns

Returns a vendor number object if a valid id was provided.

#### Update a vendor number

```
DEFINITION
POST http://apiserver/vendors/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/vendors/10/numbers/828", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "VENQUAN",
    "typeDescription": "Vendor Quantity"
    "value": 123,
    "isActive": false
}


```

Updates the specified vendor number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the vendor number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a vendor number

```
DEFINITION
DELETE http://apiserver/vendors/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/vendors/10/numbers/828", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a vendor number. It cannot be undone.

##### Arguments

* id (required) - The id of the vendor number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the vendor number id does not exist, this call returns an error.

#### List all vendor numbers

```
DEFINITION
GET http://apiserver/vendors/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/vendors/10/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "828",
            "type": "VENQUAN",
            "typeDescription": "Vendor Quantity"
            "value": 123,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all vendor numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit vendor numbers, starting at index offset. Each entry in the array is a separate vendor number object. If no more vendor numbers are available, the resulting array will be empty. This request should never return an error.

### Warehouses

#### Create a warehouse

```
DEFINITION
POST http://apiserver/warehouses

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses", {
    "id": "UKWH",
    "description": "UK Warehouse",
    "company": "010",
    "isVirtual": false,
    "inVirtualWarehouse": false,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "UKWH",
    "description": "UK Warehouse",
    "company": "010",
    "companyDescription": "SON Media",
    "account": null,
    "accountName": null
}

```

Creates a new warehouse object.

##### Arguments

* id (required) - The warehouse code.
* company (required) - The company of the warehouse.
* description (optional) - The description of the warehouse.
* account (optional) - The account of the warehouse.
* isVirtual (optional) - Whether the warehouse is the database's designated virtual warehouse for use with automatic product allocation. Only one virtual warehouse is allowed. Cannot be set to true if "inVirtualWarehouse" is true. Cannot be set to true if the warehouse has any products or locations. Defaults to false.
* inVirtualWarehouse (optional) - Whether the warehouse is considered during automatic product allocation. Cannot be set to true if "isVirtual" is true. Defaults to false.
* isActive (optional) - Whether the warehouse is selectable in transaction entry and in StudioOnline. Defaults to true.

##### Returns

Returns a warehouse object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid company).

#### Retrieve a warehouse

```
DEFINITION
GET http://apiserver/warehouses/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/UKWH");

EXAMPLE RESPONSE
{
    "id": "UKWH",
    "description": "UK Warehouse",
    "company": "010",
    "companyDescription": "SON Media",
    "account": null,
    "accountName": null,
    "isVirtual": false,
    "inVirtualWarehouse": false,
    "isActive": true
}

```

Retrieves the details of an existing warehouse. You need only supply the warehouse code.

##### Arguments

* id (required) - The warehouse code of the warehouse to be retrieved.

##### Returns

Returns a warehouse object if a valid warehouse code was provided.

#### Update a warehouse

```
DEFINITION
POST http://apiserver/warehouses/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/UKWH", {
    "description": "UK Headquarters Warehouse"
});

EXAMPLE RESPONSE
{
    "id": "10",
    "description": "UK Headquarters Warehouse",
    "company": "2",
    "companyDescription": "SON Missions - Auth.net",
    "account": "40328",
    "accountName": "Joe Nonerland ",
    "isVirtual": false,
    "inVirtualWarehouse": false,
    "isActive": false
}


```

Updates the specified warehouse by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the warehouse.
* company (optional) - The company of the warehouse.
* account (optional) - The account of the warehouse.
* isVirtual (optional) - Whether the warehouse is the database's designated virtual warehouse for use with automatic product allocation. Only one virtual warehouse is allowed. Cannot be set to true if "inVirtualWarehouse" is true. Cannot be set to true if the warehouse has any products or locations.
* inVirtualWarehouse (optional) - Whether the warehouse is considered during automatic product allocation. Cannot be set to true if "isVirtual" is true.
* isActive (optional) - Whether the warehouse is selectable in transaction entry and in StudioOnline.

  ##### Returns

Returns the warehouse object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid company).

#### Delete a warehouse

```
DEFINITION
DELETE http://apiserver/warehouses/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/UKWH", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse. It cannot be undone.

##### Arguments

* id (required) - The warehouse code of the warehouse to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse code does not exist, this call returns an error.

#### List all warehouses

```
DEFINITION
GET http://apiserver/warehouses

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses?description=UK");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    }
    "items": [
        {
            "id": "UKWH",
            "description": "UK Warehouse",
            "company": "010",
            "companyDescription": "SON Media",
            "account": null,
            "accountName": null,
            "isVirtual": false,
            "inVirtualWarehouse": false,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all warehouses matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match in warehouse code
* description (optional) - Filter list by partial match in description
* company (optional) - Filter list by partial match in company code
* isVirtual (optional) - Whether the warehouse is the database's designated virtual warehouse for use with automatic product allocation. Only one virtual warehouse is allowed. Cannot be set to true if "inVirtualWarehouse" is true. Cannot be set to true if the warehouse has any products or locations.
* inVirtualWarehouse (optional) - Whether the warehouse is considered during automatic product allocation. Cannot be set to true if "isVirtual" is true.
* isActive (optional) - Whether the warehouse is selectable in transaction entry and in StudioOnline.

##### Returns

A dictionary with an items property that contains an array of up to limit warehouses, starting at index offset. Each entry in the array is a separate warehouse object. If no more warehouses are available, the resulting array will be empty. This request should never return an error.

### Warehouse Attachments

#### Create a warehouse attachment

```
DEFINITION
POST http://apiserver/warehouses/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/attachments", {
    "type":"OTHER",
    "typeDescription":"Other",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new warehouse attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a warehouse attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve a warehouse attachment

```
DEFINITION
GET http://apiserver/warehouses/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/attachments/117");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing warehouse attachment. You need only supply the warehouse attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a warehouse attachment object if a valid id was provided.

#### Update a warehouse attachment

```
DEFINITION
POST http://apiserver/warehouses/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/attachments/117", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "117",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified warehouse attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the warehouse attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined warehouse attachment type code).

#### Delete a warehouse attachment

```
DEFINITION
DELETE http://apiserver/warehouses/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/10/attachments/117", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the warehouse attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse attachment id does not exist, this call returns an error.

#### List all warehouse attachments

```
DEFINITION
GET http://apiserver/warehouses/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
                "longComment": "long comment text",
                "dateCreated": "2018-03-12",
                "id": "117",
                "type": "LOGO",
                "typeDescription": "Logo",
                "url": null,
                "fileName": "logo64.png",
                "file": null,
                "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all warehouse attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit warehouse attachments, starting at index offset. Each entry in the array is a separate warehouse attachment object. If no more warehouse attachments are available, the resulting array will be empty. This request should never return an error.

### Warehouse codes

#### Create a warehouse code

```
DEFINITION
POST http://apiserver/warehouses/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/codes", {
    "type": "WHSTYPE",
    "value": "SMALL"
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "WHSTYPE",
    "typeDescription": "Warehouse type",
    "value": "SMALL",
    "valueDescription": "Small Warehouse",
    "isActive": true
}

```

Creates a new warehouse code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a warehouse code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a warehouse code

```
DEFINITION
GET http://apiserver/warehouses/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/codes/8096");

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "WHSTYPE",
    "typeDescription": "Warehouse type",
    "value": "SMALL",
    "valueDescription": "Small Warehouse",
    "isActive": true
}

```

Retrieves the details of an existing warehouse code. You need only supply the warehouse code id.

##### Arguments

* id (required) - The id of the warehouse code to retrieve.

##### Returns

Returns a warehouse code object if a valid id was provided.

#### Update a warehouse code

```
DEFINITION
POST http://apiserver/warehouses/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10106/codes/8096", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8096",
    "type": "WHSTYPE",
    "typeDescription": "Warehouse type",
    "value": "SMALL",
    "valueDescription": "Small Warehouse",
    "isActive": false
}


```

Updates the specified warehouse code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the warehouse code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a warehouse code

```
DEFINITION
DELETE http://apiserver/warehouses/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/10/codes/8096", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse code. It cannot be undone.

##### Arguments

* id (required) - The id of the warehouse code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse code id does not exist, this call returns an error.

#### List all warehouse codes

```
DEFINITION
GET http://apiserver/warehouses/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
                "id": "8096",
                "type": "WHSTYPE",
                "typeDescription": "Warehouse type",
                "value": "SMALL",
                "valueDescription": "Small Warehouse",
                "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all warehouse codes.

##### Returns

A dictionary with an items property that contains an array of up to limit warehouse codes, starting at index offset. Each entry in the array is a separate warehouse code object. If no more warehouse codes are available, the resulting array will be empty. This request should never return an error.

### Warehouse Dates

#### Create a warehouse date

```
DEFINITION
POST http://apiserver/warehouses/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/dates", {
    "type": "OPENING",
    "value": "2012-05-17"
});

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "OPENING",
    "typeDescription": "Opening date"
    "value": "2012-05-17",
    "isActive": true
}

```

Creates a new warehouse date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a warehouse date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve a warehouse date

```
DEFINITION
GET http://apiserver/warehouses/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/dates/1601");

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "OPENING",
    "typeDescription": "Opening date"
    "value": "2012-05-17",
    "isActive": true
}

```

Retrieves the details of an existing warehouse date. You need only supply the warehouse date id.

##### Arguments

* id (required) - The id of the warehouse date to retrieve.

##### Returns

Returns a warehouse date object if a valid id was provided.

#### Update a warehouse date

```
DEFINITION
POST http://apiserver/warehouses/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/dates/1601", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1601",
    "type": "OPENING",
    "typeDescription": "Opening date"
    "value": "2012-05-17",
    "isActive": false
}


```

Updates the specified warehouse date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the warehouse date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a warehouse date

```
DEFINITION
DELETE http://apiserver/warehouses/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/10/dates/1601", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse date. It cannot be undone.

##### Arguments

* id (required) - The id of the warehouse date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse date id does not exist, this call returns an error.

#### List all warehouse dates

```
DEFINITION
GET http://apiserver/warehouses/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
                "id": "1601",
                "type": "OPENING",
                "typeDescription": "Opening date"
                "value": "2012-05-17",
                "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all warehouse dates.

##### Returns

A dictionary with an items property that contains an array of up to limit warehouse dates, starting at index offset. Each entry in the array is a separate warehouse date object. If no more warehouse dates are available, the resulting array will be empty. This request should never return an error.

### Warehouse Notes

#### Create a warehouse note

```
DEFINITION
POST http://apiserver/warehouses/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/notes", {
    "type": "WHDESC",
    "shortComment": "Processes orders"
});

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "WHDESC",
    "typeDescription": "Warehouse description"
    "shortComment": "Processes orders",
    "longComment": null
}

```

Creates a new warehouse note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a warehouse note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a warehouse note

```
DEFINITION
GET http://apiserver/warehouses/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/notes/5054");

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "WHDESC",
    "typeDescription": "Warehouse description"
    "shortComment": "Processes orders",
    "longComment": null
}

```

Retrieves the details of an existing warehouse note. You need only supply the warehouse note id.

##### Arguments

* id (required) - The id of the warehouse note to retrieve.

##### Returns

Returns a warehouse note object if a valid id was provided.

#### Update a warehouse note

```
DEFINITION
POST http://apiserver/warehouses/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/notes/5054", {
    "shortComment": null,
    "longComment": "Processes orders"
});

EXAMPLE RESPONSE
{
    "id": "5054",
    "type": "WHDESC",
    "typeDescription": "Warehouse description"
    "shortComment": null,
    "longComment": "Processes orders"
}


```

Updates the specified warehouse note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the warehouse note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a warehouse note

```
DEFINITION
DELETE http://apiserver/warehouses/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/10/notes/5054", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse note. It cannot be undone.

##### Arguments

* id (required) - The id of the warehouse note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse note id does not exist, this call returns an error.

#### List all warehouse notes

```
DEFINITION
GET http://apiserver/warehouses/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5054",
            "type": "WHDESC",
            "typeDescription": "Warehouse description"
            "shortComment": null,
            "longComment": "Processes orders"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all warehouse notes.

##### Returns

A dictionary with an items property that contains an array of up to limit warehouse notes, starting at index offset. Each entry in the array is a separate warehouse note object. If no more warehouse notes are available, the resulting array will be empty. This request should never return an error.

### Warehouse Numbers

#### Create a warehouse number

```
DEFINITION
POST http://apiserver/warehouses/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/numbers", {
    "type": "MAXORSZ",
    "value": 155
});

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "MAXORSZ",
    "typeDescription": "Max Order Size"
    "value": 155,
    "isActive": true
}

```

Creates a new warehouse number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a warehouse number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a warehouse number

```
DEFINITION
GET http://apiserver/warehouses/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/numbers/828");

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "MAXORSZ",
    "typeDescription": "Max Order Size"
    "value": 155,
    "isActive": true
}

```

Retrieves the details of an existing warehouse number. You need only supply the warehouse number id.

##### Arguments

* id (required) - The id of the warehouse number to retrieve.

##### Returns

Returns a warehouse number object if a valid id was provided.

#### Update a warehouse number

```
DEFINITION
POST http://apiserver/warehouses/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/numbers/828", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "828",
    "type": "MAXORSZ",
    "typeDescription": "Max Order Size"
    "value": 155,
    "isActive": false
}


```

Updates the specified warehouse number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the warehouse number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a warehouse number

```
DEFINITION
DELETE http://apiserver/warehouses/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/10/numbers/828", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse number. It cannot be undone.

##### Arguments

* id (required) - The id of the warehouse number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse number id does not exist, this call returns an error.

#### List all warehouse numbers

```
DEFINITION
GET http://apiserver/warehouses/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "828",
            "type": "MAXORSZ",
            "typeDescription": "Max Order Size"
            "value": 155,
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all warehouse numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit warehouse numbers, starting at index offset. Each entry in the array is a separate warehouse number object. If no more warehouse numbers are available, the resulting array will be empty. This request should never return an error.

### Warehouse Products

#### Create a warehouse product

```
DEFINITION
POST http://apiserver/warehouses/:id/products

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/20/products", {
    "id": "1A200",
    "cost": 1.50,
    "backorderQuantity": 0,
    "checkAvailability": true,
    "canBackorder": true
});

EXAMPLE RESPONSE
{
    "id": "1A200",
    "description": null,
    "type": null,
    "weight": null,
    "cost": 1.5,
    "canBackorder": true,
    "checkAvailability": true,
    "allowDiscount": null,
    "isTaxExempt": null,
    "availableQuantity": null,
    "backorderQuantity": 0,
    "committedQuantity": 0,
    "onHandQuantity": null,
    "onOrderQuantity": null,
    "reorderQuantity": null,
    "nextReceiveDate": null,
    "discountCategory": null
}

```

Creates a new warehouse product object.

##### Arguments

* id (required) - The product code.
* cost (required) - The cost of the product.
* onOrderQuantity (required) - The quantity of the product that is on order.
* checkAvailability (required) - Whether or not to validate available quantity of the product.
* canBackorder (required) - Whether or not the product can be backordered.
* reorderQuantity (optional) - The quantity at which the product should be re-ordered.

##### Returns

Returns a warehouse product object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying a negative cost or a negative quantity).

#### Retrieve a warehouse product

```
DEFINITION
GET http://apiserver/warehouses/:id/products/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/products/BK1003");

EXAMPLE RESPONSE
{
    "id": "BK1003",
    "description": null,
    "type": "P",
    "weight": null,
    "cost": 1.5,
    "canBackorder": false,
    "checkAvailability": true,
    "allowDiscount": null,
    "isTaxExempt": null,
    "availableQuantity": null,
    "backorderQuantity": 0,
    "committedQuantity": 0,
    "onHandQuantity": null,
    "onOrderQuantity": 500,
    "reorderQuantity": 0,
    "nextReceiveDate": "2016-06-08",
    "discountCategory": null,
    "status": "A"
}

```

Retrieves the details of an existing warehouse product. You need only supply the warehouse product id.

##### Arguments

* id (required) - The id of the warehouse product object to be retrieved.
* getProductAttributes (optional) - Forces the population of the `canBackorder`, `checkAvailability`, `type`, `allowDiscount`, `isTaxExempt` and `nextReceiveDate` fields.
* getAvailableQuantity (optional) - Forces the population of the `availableQuantity` field.
* getWeight (optional) - Forces the population of the 'weight' field.
* company (optional unless `getProductAttributes=true`, `getAvailableQuantity=true` or `getWeight=true`) - Company

##### Returns

Returns a warehouse product object if a valid id was provided.

#### Update a warehouse product

```
DEFINITION
POST http://apiserver/warehouses/:id/products/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/20/products/1A200", {
    "cost": 2.6
});

EXAMPLE RESPONSE
{
    "id": "1A200",
    "description": null,
    "type": null,
    "weight": null,
    "cost": 2.6,
    "canBackorder": true,
    "checkAvailability": true,
    "allowDiscount": null,
    "isTaxExempt": null,
    "availableQuantity": null,
    "backorderQuantity": 0,
    "committedQuantity": 0,
    "onHandQuantity": null,
    "onOrderQuantity": null,
    "reorderQuantity": null,
    "nextReceiveDate": null,
    "discountCategory": null
}

```

Updates the specified warehouse product by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - The product code.
* cost (optional) - The cost of the product.
* onOrderQuantity (optional) - The quantity of the product that is on order.
* reorderQuantity (optional) - The quantity at which the product should be re-ordered.
* checkAvailability (optional) - Whether or not to validate available quantity of the product.
* canBackorder (optional) - Whether or not the product can be backordered.

##### Returns

Returns the warehouse product object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined product code).

#### Delete a warehouse product

```
DEFINITION
DELETE http://apiserver/warehouses/:id/products/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/UKWH/products/BK-5SLVG", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse product. It cannot be undone.

##### Arguments

* id (required) - The product code of the warehouse product to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse product id does not exist, this call returns an error.

#### List all warehouse products

```
DEFINITION
GET http://apiserver/warehouses/:id/products

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/products");

{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 194
    },
    "items": [
        {
            "id": "BK1000",
            "description": "So Long, Insecurity",
            "type": "P",
            "typeDescription": "Single Product",
            "weight": null,
            "cost": 5.35,
            "canBackorder": true,
            "checkAvailability": true,
            "allowDiscount": null,
            "isTaxExempt": null,
            "availableQuantity": null,
            "backorderQuantity": 0,
            "committedQuantity": 108,
            "onHandQuantity": 2006,
            "onOrderQuantity": 100,
            "reorderQuantity": 5,
            "nextReceiveDate": null,
            "discountCategory": null
        },
        { ... }
}

```

Returns a list of all warehouse products matching the provided filter criteria.

##### Arguments

* id (optional) - -Filter list by partial match in id
* description (optional) - -Filter list by partial match in description
* forOrderEntry (optional) - -Forces the population of the following fields: `weight`, `availableQuantity`, `committedQuantity`, `onOrderQuantity`, `nextReceiveDate`, `cost`, `type`, and `typeDescription`. The other fields will be `null`.
* company (option unless `forOrderEntry=true`) - -Company for order entry
* codeType (optional) - Filter list by product code attribute type. Only applies to `forOrderEntry=true`
* codeValue (optional) - Filter list by product code attribute type. Only applies to `forOrderEntry=true`

##### Returns

A dictionary with an items property that contains an array of up to limit warehouse products, starting at index offset. Each entry in the array is a separate warehouse product object. If no more warehouse products are available, the resulting array will be empty. This request should never return an error.

### Warehouse Product Locations

#### Create a warehouse product location

```
DEFINITION
POST http://apiserver/warehouses/:id/products/:id/locations

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/UKWH/products/73/locations", {
    "id": "A1"
});

EXAMPLE RESPONSE
{
    "id": "A1",
    "priority": 0,
    "onHandQuantity": 0,
    "committedQuantity": 0,
    "restockQuantity": null
}

```

Creates a new warehouse product location object.

##### Arguments

* id (required) - The location code.
* priority (optional) - The order in which to process commitments.
* restockQuantity (optional) - The quantity at which the product should be re-stocked.

##### Returns

Returns a warehouse product location object if the call succeeded.

#### Retrieve a warehouse product location

```
DEFINITION
GET http://apiserver/warehouses/:id/products/:id/locations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/10/products/10106/locations/B2");

EXAMPLE RESPONSE
{
    "id": "B2",
    "priority": 2,
    "onHandQuantity": 0,
    "committedQuantity": 0,
    "restockQuantity": null
}

```

Retrieves the details of an existing warehouse product. You need only supply the warehouse product location id.

##### Arguments

* id (required) - The id of the warehouse product location object to be retrieved.

##### Returns

Returns a warehouse product location object if a valid id was provided.

#### Update a warehouse product location

```
DEFINITION
POST http://apiserver/warehouses/:id/products/:id/locations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/10/products/10106/locations/B2", {
    "priority": 1
});

EXAMPLE RESPONSE
{
    "id": "B2",
    "priority": 1,
    "onHandQuantity": 0,
    "committedQuantity": 0,
    "restockQuantity": null
}


```

Updates the specified warehouse product location by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The location code.
* priority (optional) - The order in which to process commitments.
* restockQuantity (optional) - The quantity at which the product should be re-stocked.

##### Returns

Returns the warehouse product location object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined product code).

#### Delete a warehouse product location

```
DEFINITION
DELETE http://apiserver/warehouses/:id/products/:id/locations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/UKWH/products/73/locations/A1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a warehouse product location. It cannot be undone.

##### Arguments

* id (required) - The id of the warehouse product location to be deleted.

##### Returns

Returns a 204 No Content response on success. If the warehouse product location id does not exist, this call returns an error.

#### List all warehouse product locations

```
DEFINITION
GET http://apiserver/warehouses/:id/products/:id/locations

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/UKWH/products/73/locations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    }
    "items": [
        {
            "id": "A1",
            "priority": 0,
            "onHandQuantity": 0,
            "committedQuantity": 0,
            "restockQuantity": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all warehouse product locations matching the provided filter criteria.

##### Arguments

* id () - Filter list by partial match in location code

##### Returns

A dictionary with an items property that contains an array of up to limit warehouse product locations, starting at index offset. Each entry in the array is a separate warehouse product location object. If no more warehouse product locations are available, the resulting array will be empty. This request should never return an error.

### Warehouse Minimum Thresholds

#### Create a Warehouse Minimum Threshold

```
DEFINITION
POST http://apiserver/warehouses/:id/minimumthresholds

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/WH1/minimumthresholds", {
    "product": "PROD1",
    "thresholdQuantity": 123
});

EXAMPLE RESPONSE
{
    "id": "2",
    "product": "PROD1",
    "productDescription": "Product 1",
    "thresholdQuantity": 123,
    "warehouse": "WH1"
    "warehouseDescription": "Warehouse 1"
}

```

Creates a new Warehouse Minimum Threshold.

##### Arguments

* thresholdQuantity (required) - The minimum product quantity
* product (required) - The product code for the minimum threshold

##### Returns

Returns a Warehouse Minimum Threshold object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Warehouse Minimum Threshold

```
DEFINITION
GET http://apiserver/warehouses/:id/minimumthresholds/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/WH1/minimumthresholds/2");

EXAMPLE RESPONSE
{
    "id": "2",
    "warehouse": "WH1"
    "warehouseDescription": "Warehouse 1",
    "thresholdQuantity": 123,
    "product": "PROD1",
    "productDescription": "Product 1"
}

```

Retrieves the details of an existing Warehouse Minimum Threshold. You need only supply the id.

##### Arguments

* id (required) - The id of the Warehouse Minimum Threshold to be retrieved.

#### Update a Warehouse Minimum Threshold

```
DEFINITION
POST http://apiserver/warehouses/:id/minimumthresholds/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouses/WH1/minimumthresholds/2", {
    "thresholdQuantity": 321
});

EXAMPLE RESPONSE
{
    "id": "2",
    "warehouse": "WH1"
    "warehouseDescription": "Warehouse 1",
    "thresholdQuantity": 321,
    "product": "PROD1",
    "productDescription": "Product 1"
}


```

Updates the specified Warehouse Minimum Threshold by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The id of the Warehouse Minimum Threshold
* thresholdQuantity (optional) - The minimum product quantity
* product (option) - The product code for the minimum threshold

##### Returns

Returns the Warehouse Minimum Threshold object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Warehouse Minimum Threshold

```
DEFINITION
DELETE http://apiserver/warehouses/:id/minimumthresholds/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouses/WH1/minimumthresholds/2", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Warehouse Minimum Threshold. It cannot be undone.

##### Arguments

* id (required) - The id of the Warehouse Minimum Threshold to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Warehouse Minimum Threshold does not exist, this call returns an error.

#### List all Warehouse Minimum Thresholds

```
DEFINITION
GET http://apiserver/warehouses/:id/minimumthresholds

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouses/WH1/minimumthresholds?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "2",
            "warehouse": "WH1"
            "warehouseDescription": "Warehouse 1",
            "thresholdQuantity": 321,
            "product": "PROD1",
            "productDescription": "Product 1"
        },
        {...},
    ]
}

```

Returns a list of all Warehouse Minimum Thresholds.

##### Returns

A dictionary with an items property that contains an array of up to limit Warehouse Minimum Thresholds, starting at index offset. Each entry in the array is a separate warehouse minimum threshold object. If no more Warehouse Minimum Thresholds are available, the resulting array will be empty. This request should never return an error.

### Warehouse Assignment Rules

#### Create a Warehouse Assignment Rule

```
DEFINITION
POST http://apiserver/warehouseassignmentrules

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouseassignmentrules", {
    "assignmentWarehouse": "WH1",
    "criteria": [
        {
            "criteriaType": "DDCZIPCODE",
            "tableId": "A03",
            "field": "ZipPostal",
            "comparisonType": "CONTAIN",
            "comparisonValue": "55555"
        }
    ],
    "sequence": 1,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "11",
    "assignmentWarehouse": "WH1",
    "assignmentWarehouseDescription": "Warehouse 1",
    "criteria": [
        {
            "criteriaType": "DDCZIPCODE",
            "tableId": "A03",
            "field": "ZipPostal",
            "comparisonType": "CONTAIN",
            "comparisonValue": "55555"
        }
    ],
    "sequence": 1,
    "isActive": true
}

```

Creates a new Warehouse Assignment Rule.

##### Arguments

* assignmentWarehouse (required) - The warehouse the assignment rule applies for.
* criteria (required) - Json rule criteria
* sequence (required) - The sequence the assignment rule will run in
* isActive (required) - If the rule is active

##### Returns

Returns a Warehouse Assignment Rule object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Warehouse Assignment Rule

```
DEFINITION
GET http://apiserver/warehouseassignmentrules/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouseassignmentrules/11");

EXAMPLE RESPONSE
{
    "id": "11",
    "assignmentWarehouse": "WH1",
    "assignmentWarehouseDescription": "Warehouse 1",
    "criteria": [
        {
            "criteriaType": "DDCZIPCODE",
            "tableId": "A03",
            "field": "ZipPostal",
            "comparisonType": "CONTAIN",
            "comparisonValue": "55555"
        }
    ],
    "sequence": 1,
    "isActive": true
}

```

Retrieves the details of an existing Warehouse Assignment Rule. You need only supply the id.

##### Arguments

* id (required) - The id of the Warehouse Assignment Rule to be retrieved.

#### Update a Warehouse Assignment Rule

```
DEFINITION
POST http://apiserver/warehouseassignmentrules/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouseassignmentrules/11", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "11",
    "assignmentWarehouse": "WH1",
    "assignmentWarehouseDescription": "Warehouse 1",
    "criteria": [
        {
            "criteriaType": "DDCZIPCODE",
            "tableId": "A03",
            "field": "ZipPostal",
            "comparisonType": "CONTAIN",
            "comparisonValue": "55555"
        }
    ],
    "sequence": 1,
    "isActive": false
}


```

Updates the specified Warehouse Assignment Rule by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The id of the Warehouse Assignment Rule
* assignmentWarehouse (optional) - The warehouse the assignment rule applies for.
* criteria (optional) - Json rule criteria
* sequence (optional) - The sequence the assignment rule will run in
* isActive (optional) - If the rule is active

##### Returns

Returns the Warehouse Assignment Rule object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Warehouse Assignment Rule

```
DEFINITION
DELETE http://apiserver/warehouseassignmentrules/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/warehouseassignmentrules/11", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Warehouse Assignment Rule. It cannot be undone.

##### Arguments

* id (required) - The id of the Warehouse Assignment Rule to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Warehouse Assignment Rule does not exist, this call returns an error.

#### List all Warehouse Assignment Rules

```
DEFINITION
GET http://apiserver/warehouseassignmentrules

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouseassignmentrules?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "11",
            "assignmentWarehouse": "WH1",
            "assignmentWarehouseDescription": "Warehouse 1",
            "criteria": [
                {
                    "criteriaType": "DDCZIPCODE",
                    "tableId": "A03",
                    "field": "ZipPostal",
                    "comparisonType": "CONTAIN",
                    "comparisonValue": "55555"
                }
            ],
            "sequence": 1,
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all Warehouse Assignment Rules.

##### Returns

A dictionary with an items property that contains an array of up to limit Warehouse Assignment Rules, starting at index offset. Each entry in the array is a separate warehouse assignment rule object. If no more Warehouse Assignment Rules are available, the resulting array will be empty. This request should never return an error.

### Warehouse Allocation Runs

#### Retrieve a Warehouse Allocation Run

```
DEFINITION
GET http://apiserver/warehouseallocationruns/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouseallocationruns/138?");

EXAMPLE RESPONSE
{
    "id": "138",
    "runDate": "2019-03-18T02:10:06 PM",
    "hasErrors": true,
    "productionRunId": "3688"
}

```

Retrieves the details of an existing Warehouse Allocation Run. You need only supply the id.

##### Arguments

* id (required) - The id of the Warehouse Allocation Run to be retrieved.

#### List all Warehouse Allocation Runs

```
DEFINITION
GET http://apiserver/warehouseallocationruns

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouseallocationruns?");

EXAMPLE RESPONSE
{
    "paging": {
    "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "139",
            "runDate": "2019-03-19T12:26:47 PM",
            "hasErrors": false,
            "productionRunId": null
        },
        {
            "id": "138",
            "runDate": "2019-03-18T02:10:06 PM",
            "hasErrors": true,
            "productionRunId": "3688"
        },
        {
            "id": "137",
            "runDate": "2019-03-18T02:00:28 PM",
            "hasErrors": false,
            "productionRunId": null
        }
    ]
}

```

Returns a list of all Warehouse Allocation Runs.

##### Returns

A dictionary with an items property that contains an array of up to limit Warehouse Allocation Runs, starting at index offset. Each entry in the array is a separate warehouse allocation run object. If no more Warehouse Allocation Runs are available, the resulting array will be empty. This request should never return an error.

### Warehouse Allocation Run Process

#### Process a new Warehouse Allocation Run

```
DEFINITION
POST http://apiserver/warehouseallocationruns/process

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouseallocationruns/process" {
    "company": "BEAN"
});

EXAMPLE RESPONSE
204 No Content

```

Executes a new warehouse allocation run process.

##### Arguments

* company - The company to filter on. Warehouse Allocation will only occur on transactions that use this company code.

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any invalid values are provided, this call will return an error.

### Warehouse Allocation Run Results

#### Update Warehouse Allocation Run Results

```
DEFINITION
POST http://apiserver/warehouseallocationruns/:id/results/

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouseallocationruns/134/results", {
    "runId":"134",
    "overrideCriteria": [
                            {"id":"659978","moveToWarehouse":"30"},
                            {"id":"659977","reset":1}
                        ]
})

EXAMPLE RESPONSE
204 No Content

```

Updates the warehouse allocation run results by overriding the run results with the values of the parameters passed.

##### Arguments

* runId (required) - The id of the Warehouse Allocation Run that the results are found in
* overrideCriteria (required) - An array consisting of the id of the Warehouse Allocation Run Result and either the Warehouse it is moving to, or a flag to reset it.

##### Returns

Returns a 204 No Content status code

#### List all Warehouse Allocation Run Results

```
DEFINITION
GET http://apiserver/warehouseallocationruns/:id/results/

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouseallocationruns/138/results");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 2
    },
    "items": [
        {
            "id": "659980",
            "orderId": 614436,
            "documentNumber": 1142456,
            "productCode": "10",
            "productDescription": "Product like the 10 Project",
            "quantity": 1,
            "warehouseCode": "20",
            "availableQuantity": 0,
            "backOrderQuantity": 10
        },
        {
            "id": "659979",
            "orderId": 614436,
            "documentNumber": 1142456,
            "productCode": "100BACK",
            "productDescription": "Another Available Product",
            "quantity": 1,
            "warehouseCode": "20",
            "availableQuantity": 376,
            "backOrderQuantity": 0
        }
    ]
}

```

Returns a list of all Warehouse Allocation Run Results in a Run.

##### Arguments

* id (required) - The run id of the warehouse allocation run that the results are found in.

##### Returns

A dictionary with an items property that contains an array of up to limit Warehouse Allocation Run Results, starting at index offset. Each entry in the array is a separate warehouse allocation run result object. If no more Warehouse Allocation Runs are available, the resulting array will be empty. This request should never return an error.

### Warehouse Allocation Run Errors

#### Reset Warehouse Allocation Run Errors

```
DEFINITION
DELETE http://apiserver/warehouseallocationruns/:id/errors

EXAMPLE REQUEST
$.delete("http://localhost:49195/warehouseallocationruns/1234/errors", { [649880,649883] });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes warehouse allocation run errors on a run. This also removes the warehouse allocation run id from the responses .It cannot be undone.

##### Arguments

* id (required) - Id of the Warehouse Allocation Run.
* error ids (required) - Array of ids of the errors to be deleted/reset.

##### Returns

Returns a `204 No Content` response on success. If the accessor dashboard view does not exist, this call returns an error.

#### List all Warehouse Allocation Run Errors

```
DEFINITION
GET http://apiserver/warehouseallocationruns/:id/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/warehouseallocationruns/138/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "recordId": 418,
            "runId": 138,
            "t03RecordId": 659981,
            "message": "Could not assign Product 'DVD002'. The Product is not in Warehouse'20'.",
            "documentNumber": 1142456,
            "productCode": "DVD002",
            "orderId": 614437
        }
    ]
}

```

Returns a list of all Warehouse Allocation Run Errors.

##### Returns

A dictionary with an items property that contains an array of up to limit Warehouse Allocation Run Errors, starting at index offset. Each entry in the array is a separate warehouse allocation run error object. If no more Warehouse Allocation Run Errors are available, the resulting array will be empty. This request should never return an error.

### Warehouse Allocation Run Explode Kits

#### Explode the kits on a warehouse allocation run

```
DEFINITION
POST http://apiserver/warehouseallocationruns/process

EXAMPLE REQUEST
$.post("http://localhost:49195/warehouseallocationruns/process" {
    "company": "BEAN"
});

EXAMPLE RESPONSE
204 No Content

```

Explodes all kits on a warehouse allocation run.

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any invalid values are provided, this call will return an error.