# System Import Product Warehouses

#### Retrieve a system import product warehouse

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/warehouses/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/warehouses/23");

EXAMPLE RESPONSE
{
    "id": "23",
    "warehouse": "SAVCHLD-EVT2",
    "cost": 15,
    "isCheckAvailability": false,
    "isAllowBackorder": false
}

```

Retrieves the details of an existing system import product warehouse. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product warehouse to be retrieved.

#### Update a system import product warehouse

```
DEFINITION
POST http://apiserver/systemimports/:importId/products/:productId/warehouses/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/products/40812571/warehouses/23", {
    "cost": 25
});

EXAMPLE RESPONSE
{
    "id": "23",
    "warehouse": "SAVCHLD-EVT2",
    "cost": 25,
    "isCheckAvailability": false,
    "isAllowBackorder": false
}

```

Updates the specified system import product warehouse by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* warehouse (optional) - the warehouse code to update the product warehouse with
* cost (optional) - the cost to update the product warehouse with
* isCheckAvailability - should the import check availability
* isAllowBackorder - does the warehouse allow backordering

##### Returns

Returns the system import product warehouse object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import product warehouse

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/products/:productId/warehouses/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/products/40812571/warehouses/23", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import product warehouse. It cannot be undone.

##### Arguments

* id (required) - The id of the system import product warehouse to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import product warehouse does not exist, this call returns an error.

#### List all system import product warehouses

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/warehouses

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/warehouses?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "23",
            "warehouse": "SAVCHLD-EVT2",
            "cost": 15,
            "isCheckAvailability": false,
            "isAllowBackorder": false
        },
        {...},
    ]
}

```

Returns a list of all system import product warehouses.

##### Returns

A dictionary with an items property that contains an array of up to limit system import product warehouses, starting at index offset. Each entry in the array is a separate system import product warehouse object. If no more system import product warehouses are available, the resulting array will be empty. This request should never return an error.