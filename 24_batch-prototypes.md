# Batch Prototypes

#### Create a Batch Prototype

```
DEFINITION
POST http://apiserver/batchprototypes

EXAMPLE REQUEST
$.post("http://localhost:49195/batchprototypes", {
    "company": "4",
    "date": "2015-06-06",
    "category": "MAIL",
    "currency": "USD"
});

EXAMPLE RESPONSE
{
    "id": 4,
    "company": "4",
    "date": "2015-06-06",
    "category": "MAIL",
    "currency": "USD",
    "defaultPayType": null,
    "defaultSource": null
}

```

Creates a new Batch Prototype.

##### Arguments

* company (required) - The company to associate the batch prototype with.
* date (optional) - The date for the batch prototype. Defaults to the current date.
* category (required) - The batch category for the batch prototype.
* currency (required) - The currency code for the batch prototype.
* defaultPayType (optional) - The default pay type to be used for the batch prototype.
* defaultSource (optional) - The default source code for the batch prototype.

##### Returns

Returns a Batch Prototype object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Batch Prototype

```
DEFINITION
GET http://apiserver/batchPrototypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/batchPrototypes/4");

EXAMPLE RESPONSE
{
    "id": 4,
    "company": "4",
    "date": "2015-06-06",
    "category": "MAIL",
    "currency": "USD",
    "defaultPayType": null,
    "defaultSource": null
}

```

Retrieves the details of an existing Batch Prototype. You need only supply the id.

##### Arguments

* id (required) - The id of the Batch Prototype to be retrieved.

#### Update a Batch Prototype

```
DEFINITION
POST http://apiserver/batchprototypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/batchprototypes/4", {
    "company": "PAYCONEX"
});

EXAMPLE RESPONSE
{
    "id": "4",
    "company": "PAYCONEX",
    "date": "2015-06-06",
    "category": "MAIL",
    "currency": "USD",
    "defaultPayType": null,
    "defaultSource": null
}


```

Updates the specified Batch Prototype by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* company (optional) - The company to associate the batch prototype with.
* date (optional) - The date for the batch prototype. Defaults to the current date.
* category (optional) - The batch category for the batch prototype.
* currency (optional) - The currency code for the batch prototype.
* defaultPayType (optional) - The default pay type to be used for the batch prototype.
* defaultSource (optional) - The default source code for the batch prototype.

##### Returns

Returns the Batch Prototype object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Batch Prototype

```
DEFINITION
DELETE http://apiserver/batchprototypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/batchprototypes/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Batch Prototype. It cannot be undone.

##### Arguments

* id (required) - The id of the Batch Prototype to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Batch Prototype does not exist, this call returns an error.

#### List all Batch Prototypes

```
DEFINITION
GET http://apiserver/batchprototypes

EXAMPLE REQUEST
$.get("http://localhost:49195/batchprototypes", {
    "company": "PAYCONEX"
});

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "company": "PAYCONEX",
            "date": "2015-06-06",
            "category": "MAIL",
            "currency": "USD",
            "defaultPayType": null,
            "defaultSource": null
        },
        {...},
    ]
}

```

Returns a list of all Batch Prototypes.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* company (optional) - The company to filter batch prototypes on.
* date (optional) - The date to filter batch prototypes on.
* category (optional) - The batch category to filter the batch prototypes on.
* currency (optional) - The currency code to filter the batch prototypes on.

##### Returns

A dictionary with an items property that contains an array of up to limit Batch Prototypes, starting at index offset. Each entry in the array is a separate batch prototype object. If no more Batch Prototypes are available, the resulting array will be empty. This request should never return an error.