# System Import Product Errors

#### Retrieve a system import product error

```
DEFINITION
GET http://apiserver/ssytemimports/:importId/products/:productId/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/ssytemimports/10000047/products/40812571/errors/232");

EXAMPLE RESPONSE
{
    "id": "232",
    "comment": "Product IT100 already exists in warehouse SAVCHLD-MAIN at location FA1."
}

```

Retrieves the details of an existing system import product error. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product error to be retrieved.

#### List all system import product errors

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "232",
            "comment": "Product IT100 already exists in warehouse SAVCHLD-MAIN at location FA1."
        },
        {...},
    ]
}

```

Returns a list of all ssytem import product errors.

##### Returns

A dictionary with an items property that contains an array of up to limit ssytem import product errors, starting at index offset. Each entry in the array is a separate system import product error object. If no more ssytem import product errors are available, the resulting array will be empty. This request should never return an error.