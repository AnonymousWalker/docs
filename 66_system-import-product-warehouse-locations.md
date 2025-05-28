# System Import Product Warehouse Locations

#### Retrieve a system import product warehouse location

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/warehouselocations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/warehouselocations/23");

EXAMPLE RESPONSE
{
    "id": "23",
    "warehouse": "SAVCHLD-MAIN",
    "location": "FA6",
    "priority": 50000,
    "restockPoint": 1
}

```

Retrieves the details of an existing system import product warehouse location. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product warehouse location to be retrieved.

#### Update a system import product warehouse location

```
DEFINITION
POST http://apiserver/systemimports/:importId/products/:productId/warehouselocations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/products/40812571/warehouselocations/23", {
    "location": "PS5"
});

EXAMPLE RESPONSE
{
    "id": "23",
    "warehouse": "SAVCHLD-MAIN",
    "location": "PS5",
    "priority": 50000,
    "restockPoint": 1
}

```

Updates the specified system import product warehouse location by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* location (optional) - the location to update the warehouse location with
* priority (optional) - the priority to update the warehouse location with
* restockPoint (optional) - the restock point to update the warehouse location with

##### Returns

Returns the system import product warehouse location object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import product warehouse location

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/products/:productId/warehouselocations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/products/40812571/warehouselocations/23", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import product warehouse location. It cannot be undone.

##### Arguments

* id (required) - The id of the system import product warehouse location to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import product warehouse location does not exist, this call returns an error.

#### List all system import product warehouse locations

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/warehouselocations

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/warehouselocations");

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
            "warehouse": "SAVCHLD-MAIN",
            "location": "FA6",
            "priority": 50000,
            "restockPoint": 1
        },
        {...},
    ]
}

```

Returns a list of all system import product warehouse locations.

##### Returns

A dictionary with an items property that contains an array of up to limit system import product warehouse locations, starting at index offset. Each entry in the array is a separate system import product warehouse location object. If no more system import product warehouse locations are available, the resulting array will be empty. This request should never return an error.