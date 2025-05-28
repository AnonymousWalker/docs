# Recurring Transaction Errors

#### List all recurring transaction errors

```
DEFINITION
GET http://apiserver/recurringtransactions/1000000398/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/recurringtransactions/1000000398/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10841",
            "error": "Source code is invalid."
        },
        {...},
    ]
}

```

Returns a list of all recurring transaction errors.

##### Returns

A dictionary with an items property that contains an array of up to limit recurring transaction errors, starting at index offset. Each entry in the array is a separate recurring transaction error object. If no more recurring transaction errors are available, the resulting array will be empty. This request should never return an error.

### Shipping Groups

#### Retrieve a shipping group

```
DEFINITION
GET http://apiserver/shippinggroups/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippinggroups/680");

EXAMPLE RESPONSE
{
    "id": "680",
    "shipDate": "2015-01-07",
    "runDate": "2015-01-07",
    "company": "1",
    "journalReference": "1288",
    "status": "P"
}

```

Returns the shipping group with the specified shipping group id.

##### Returns

A shipping group object if the call was successful. If an invalid shipping group id was provided, this call will return an error.

#### List all shipping groups

```
DEFINITION
GET http://apiserver/shippinggroups

EXAMPLE REQUEST
$.get("http://localhost:49195/shippinggroups", {
    "status": "P"
});

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 16
    },
    "items": [
        {
            "id": "691",
            "shipDate": "2015-04-23",
            "runDate": "2015-04-23",
            "company": "4",
            "journalReference": "1349",
            "status": "P"
        },
        { ... },
        { ... }
    ]
}

```

Returns all shipping groups that match the specified criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* company (optional) - The company to filter on.
* shipDate (optional) - The shipping date of the shipping group.
* journalReference (optional) - The journal reference id to filter on.
* status (optional) - The shipping group status to filter on. If not provided, all statuses are returned.
* id (optional) - The shipping group id. If provided, no other criteria will be considered.

##### Returns

A dictionary with an items property that contains an array of up to limit shipping groups, starting at index offset. Each entry in the array is a separate shipping group object. If no more shipping groups are available, the resulting array will be empty. This request should never return an error.

#### Shipping Groups Process

```
DEFINITION
POST http://apiserver/shippinggroups/process

EXAMPLE REQUEST
$.post("http://localhost:49195/shippinggroups/process", {
    "company": "4",
    "shipDate": "2015-06-01",
    "updateInventory": true,
    "postJournalEntry": false
});

EXAMPLE RESPONSE
HTTP 204 NoContent

```

Processes shipping groups for a specified company

##### Arguments

* company (required) - The company to process shipping groups for.
* shipDate (required) - The shipping date for the shipping group.
* updateInventory (required) - Whether the system should update inventory during process.
* postJournalEntry (required) - Whether the system should post a journal entry for the created shipping group.

##### Returns

Returns a 204 No Content response if the asynchronous shipping group process was successfully initiated.

#### Shipping Groups Available Orders

```
DEFINITION
GET http://apiserver/shippinggroups/shippedorders/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippinggroups/shippedorders/4");

EXAMPLE RESPONSE
{
    "count": 1
}

```

Returns a count of shipped orders available for the specified company.

##### Arguments

* id (required) - A valid company to get the available shipped orders for.

##### Returns

Returns the count of available shipped products for the specified company. This request should never return an error.

#### Shipping Groups Post Journal Entry

```
DEFINITION
POST http://apiserver/shippinggroups/:id/post

EXAMPLE REQUEST
$.post("http://localhost:49195/shippinggroups/719/post", {
    "shipDate": "2015-06-15",
    "updateInventory": true,
    "postJournalEntry": false
});

EXAMPLE RESPONSE
HTTP 204 NoContent

```

Performs a journal entry post for the specified shipping group.

##### Arguments

* shipDate (required) - The shipping date for the shipping group.
* updateInventory (required) - Whether the system should update inventory during process.
* postJournalEntry (required) - Whether the system should post a journal entry for the created shipping group.

##### Returns

Returns a 204 No Content response if the asynchronous shipping group journal entry posting was successfully initiated.

### Shipping Groups Ship Single

#### Retrieve shipping interface by response id

```
DEFINITION
GET http://apiserver/shippinggroups/singleship

EXAMPLE REQUEST
$.get("http://localhost:49195/shippinggroups/singleship?responseId=476720");

EXAMPLE RESPONSE
{
    "recordId": "176",
    "documentNumber": "241545"
}

```

Returns the shipping item information associated with the provided response id.

##### Arguments

* responseId (required) - A response id to look up shiping item information for.

##### Returns

Returns an object containing the shipping item information. If an invalid or unsupported response id is provided, this request will return an error.

#### Perform single ship

```
DEFINITION
POST http://apiserver/shippinggroups/singleship

EXAMPLE REQUEST
$.post("http://apiserver/shippinggroups/singleship", {
    "recordId": "176",
    "shipMethod": "USPS",
    "shipCost": "5",
    "trackingNumber": "M0911753661"

});

EXAMPLE RESPONSE
HTTP 204 NO CONTENT

```

Performs a single ship process on the specified shipping item.

##### Arguments

* recordId (required) - A valid record id for a shippable item.
* shipMethod (optional) - The actual method used for shipping.
* shipCost (optional) - The actual shipping cost.
* trackingNumber (optional) - The shipping tracking number.

##### Returns

Returns a 204 No Content if the shipping process was executed successfully.

### Shipping Information

#### Retrieve shipping information

```
DEFINITION
GET http://apiserver/shippinginfo/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippinginfo/2059302");

EXAMPLE RESPONSE
{
    "id": "2059302",
    "printGroupId": 4765,
    "accountNumber": 42820,
    "documentNumber": 1142570,
    "formattedName": "Robert Jameson",
    "addressLine1": "2435 N. Central Expressway",
    "addressLine2": "Ste. 950",
    "addressLine3": "",
    "addressLine4": "",
    "city": "Richardson",
    "state": "TX",
    "zipPostal": "75080",
    "country": "USA",
    "isAddressPOBox": false,
    "shippingAddressLine1": "Robert Jameson",
    "shippingAddressLine2": "2435 N. Central Expressway",
    "shippingAddressLine3": "Ste. 950",
    "shippingAddressLine4": "Richardson, TX 75080",
    "shippingAddressLine5": "",
    "shippingAddressLine6": "",
    "shippingAddressLine7": "",
    "emailAddress": "",
    "shipMethod": "GROUND",
    "productWeight": 0.25000,
    "trackingNumber": "9274 8999 9374 5757 3020 5930 24",
    "actualShipMethod": null,
    "shippingCost": 0.0,
    "status": "Y",
    "formattedPhone": "(111) 111-1111",
    "routingCode": "750802769",
    "intelligentMailBarcode": "FADTDDDADDDTFTTTTATDAFTFFDFATAAFDTDDATATATDTTFTTATATATFTFFFTDTAFF"
}

```

Returns the shipping information for the specified response id.

##### Returns

A shipping information object if the call was successful. If an invalid response id was provided, this call will return an error.

#### Update shipping information

```
DEFINITION
POST http://apiserver/shippinginfo/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippinginfo/2059302", {
    "actualShipMethod": "2DAY",
    "shippingCost": 12.34,
    "status": "R",
    "trackingNumber": "9274 8999 9374 5757 3020 5930 24"
});

EXAMPLE RESPONSE
{
    "id": "2059302",
    "printGroupId": 4765,
    "accountNumber": 42820,
    "documentNumber": 1142570,
    "formattedName": "Robert Jameson",
    "addressLine1": "2435 N. Central Expressway",
    "addressLine2": "Ste. 950",
    "addressLine3": "",
    "addressLine4": "",
    "city": "Richardson",
    "state": "TX",
    "zipPostal": "75080",
    "country": "USA",
    "isAddressPOBox": false,
    "shippingAddressLine1": "Robert Jameson",
    "shippingAddressLine2": "2435 N. Central Expressway",
    "shippingAddressLine3": "Ste. 950",
    "shippingAddressLine4": "Richardson, TX 75080",
    "shippingAddressLine5": "",
    "shippingAddressLine6": "",
    "shippingAddressLine7": "",
    "emailAddress": "",
    "shipMethod": "GROUND",
    "productWeight": 0.25000,
    "trackingNumber": "9274 8999 9374 5757 3020 5930 24",
    "actualShipMethod": "2DAY",
    "shippingCost": 12.3400,
    "status": "R",
    "formattedPhone": "(111) 111-1111",
    "routingCode": "750802769",
    "intelligentMailBarcode": "FADTDDDADDDTFTTTTATDAFTFFDFATAAFDTDDATATATDTTFTTATATATFTFFFTDTAFF"
}

```

Updates the specified shipping information by setting the values of the parameters passed. Only shipping information with a status of 'Y' can be updated. Any parameters not provided will be left unchanged.

##### Arguments

* actualShipMethod (optional) - The actual shipping method of the shipping information record.
* shippingCost (optional) - The shipping cost of the shipping information record.
* status (optional) - The status of the shipping information. Valid values include 'Y' and 'R'.
* trackingNumber (optional) - The tracking number of the shipping information record.

##### Returns

Returns the shipping information object if the update succeeded. Returns an error if update parameters are invalid.