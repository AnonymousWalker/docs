# System Import Warehouse Errors

#### Retrieve a system import warehouse error

```
DEFINITION
GET http://apiserver/systemimports/:importId/warehouses/:warehouseId/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/warehouses/40812571/errors/961");

EXAMPLE RESPONSE
{
    "id": "961",
    "comment": "030 is not a valid Company"
}

```

Retrieves the details of an existing system import warehouse error. You need only supply the id.

##### Arguments

* id (required) - The id of the system import warehouse error to be retrieved.

#### List all system import warehouse errors

```
DEFINITION
GET http://apiserver/systemimports/:importId/warehouses/:warehouseId/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/warehouses/40812571/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "961",
            "comment": "030 is not a valid Company"
        },
        {...},
    ]
}

```

Returns a list of all system import warehouse errors.

##### Returns

A dictionary with an items property that contains an array of up to limit system import warehouse errors, starting at index offset. Each entry in the array is a separate system import warehouse error object. If no more system import warehouse errors are available, the resulting array will be empty. This request should never return an error.