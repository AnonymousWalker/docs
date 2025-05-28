# Custom Entity Objects

### Create a custom entity object

```
DEFINITION
POST http://apiserver/componentcustomentities/:componentId

EXAMPLE REQUEST
$.post("http://localhost:49195/componentcustomentities/302", {
    "state": "TX",
    "account": "16630"
});

EXAMPLE RESPONSE
{
    "id": "34",
    "state": "TX",
    "stateDescription": "Texas",
    "account": "16630",
    "accountName": "DonorDirect"
}

```

Creates a new custom entity object.

#### Arguments

* componentId (required) - The id/type of the component to create.

Additional arguments are determined by the component.
These can be set up in System Administration.

#### Returns

Returns a custom entity object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).
NOTE: null fields are not returned.

### Retrieve a custom entity object

```
DEFINITION
GET http://apiserver/componentcustomentities/:componentId/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/componentcustomentities/302/34");

EXAMPLE RESPONSE
{
    "id": "34",
    "state": "TX",
    "stateDescription": "Texas",
    "account": "16630",
    "accountName": "DonorDirect"
}

```

Retrieves the details of an existing custom entity object. You need only supply the component id and custom entity object id.

#### Arguments

* componentId (required) - The id/type of the component to retrieve.
* id (required) - The id of the custom entity object to retrieve.

#### Returns

Returns a custom entity object if a valid id was provided.
NOTE: null fields are not returned.

### Update a custom entity object

```
DEFINITION
POST http://apiserver/componentcustomentities/:componentId/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/componentcustomentities/302/34", {
    "state": "TX",
    "account": "16630",
    "description": "Area team for DDC"
});

EXAMPLE RESPONSE
{
    "id": "34",
    "state": "TX",
    "stateDescription": "Texas",
    "account": "16630",
    "accountName": "DonorDirect",
    "description": "Area team for DDC"
}

```

Updates the specified campaign by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

#### Arguments

* componentId (required) - The id/type of the component to update.
* id (required) - The id of the custom entity object to update.

Additional arguments are determined by the component.
These can be set up in System Administration.
NOTE: all fields are required when updating custom entity objects. Unspecified fields are interpreted as null.
NOTE: null fields are not returned.

#### Returns

Returns the custom entity object if the update succeeded. Returns an error if update parameters are invalid (e.g. not including required field).

### Delete a custom entity object

```
DEFINITION
DELETE http://apiserver/componentcustomentities/:componentId/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/componentcustomentities/302/34", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a custom entity object. It cannot be undone.

#### Arguments

* componentId (required) - The id/type of the component to delete.
* id (required) - The id of the custom entity object to delete.

#### Returns

Returns a 204 No Content response on success. If the custom entity object does not exist, this call returns an error.

### List all custom entity objects

```
DEFINITION
GET http://apiserver/componentcustomentities/:componentId

EXAMPLE REQUEST
$.get("http://localhost:49195/componentcustomentities/302");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 28
    }
    "items": [
        {
            "id": "34",
            "state": "TX",
            "stateDescription": "Texas",
            "account": "16630",
            "accountName": "DonorDirect",
            "description": "Area team for DDC"
        },
        {
            "id": "35",
            "state": "AK",
            "stateDescription": "Alaska"
        },
        {...}
    ]
}

```

Returns a list of all custom entity objects matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting. However use the following syntax for the column criteria parameter:
columnCriteria=[{"column":"TransType","sortOrder":"D"}]

#### Arguments

* componentId (required) - The id/type of the component to retrieve objects for.

Additional arguments are determined by the component.
These can be set up in System Administration.

#### Returns

A dictionary with an items property that contains an array of up to limit custom entity objects, starting at index offset. Each entry in the array is a separate custom entity object. If no more custom entity objects are available, the resulting array will be empty. This request should never return an error.
NOTE: null fields are not returned.