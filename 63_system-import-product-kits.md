# System Import Product Kits

#### Retrieve a system import product kit

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/kits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/kits/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "product": "SP_003",
    "quantity": 2,
    "isUseInShoppingCart": true
}

```

Retrieves the details of an existing system import product kit. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product kit to be retrieved.

#### Update a system import product kit

```
DEFINITION
POST http://apiserver/systemimports/:importId/products/:productId/kits/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/products/40812571/kits/1", {
    "quantity": 5
});

EXAMPLE RESPONSE
{
    "id": "1",
    "product": "SP_003",
    "quantity": 5,
    "isUseInShoppingCart": true
}

```

Updates the specified system import product kit by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* quantity (optional) - the quantity to update the kit with
* isUseInShoppingCart (optional) - is the product kit used in StudioOnline

##### Returns

Returns the system import product kit object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import product kit

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/products/:productId/kits/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/products/40812571/kits/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import product kit. It cannot be undone.

##### Arguments

* id (required) - The id of the system import product kit to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import product kit does not exist, this call returns an error.

#### List all system import product kits

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/kits

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/kits");

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
            "product": "SP_003",
            "quantity": 2,
            "isUseInShoppingCart": true
        },
        {...},
    ]
}

```

Returns a list of all system import product kits.

##### Returns

A dictionary with an items property that contains an array of up to limit system import product kits, starting at index offset. Each entry in the array is a separate system import product kit object. If no more system import product kits are available, the resulting array will be empty. This request should never return an error.