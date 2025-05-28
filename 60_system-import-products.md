# System Import Products

#### Retrieve a system import product

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40823571");

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "P",
    "product": "IT100"
}

```

Retrieves the details of an existing system import product. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product to be retrieved.

#### Update a system import product

```
DEFINITION
POST http://apiserver/systemImports/:importId/products/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemImports/10000047/products/40812571", {
    "status": "Y"
});

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "Y",
    "product": "IT100"
}

```

Updates the specified system import product by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* action (optional) - the action to update the product with
* status (optional) - the status to update the product with
* product (optional) - the product to update the product with

##### Returns

Returns the system import product object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system import products

```
DEFINITION
GET http://apiserver/systemimports/:importId/products

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "40812571",
            "action": "U",
            "status": "P",
            "product": "IT100"
        },
        {...},
    ]
}

```

Returns a list of all system import products.

##### Arguments

* action (optional) - the action to filter the results on
* status (optional) - the status to filter the results on
* product (optional) - the product code to filter the results on

##### Returns

A dictionary with an items property that contains an array of up to limit system import products, starting at index offset. Each entry in the array is a separate system import product object. If no more system import products are available, the resulting array will be empty. This request should never return an error.