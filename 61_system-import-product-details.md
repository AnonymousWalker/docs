# System Import Product Details

#### Retrieve a system import product detail

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:id/detail

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/detail");

EXAMPLE RESPONSE
{
    "id": null,
    "description": "5K T-Shirts (Mens)",
    "author": "Johnathan Doe Sr.",
    "isbn": "123456768789",
    "type": "P",
    "status": "A",
    "packaging": "P",
    "isUseInShoppingCart": false,
    "weight": 0,
    "isDiscountAllowed": true
}

```

Retrieves the details of an existing system import product detail. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product detail to be retrieved.

#### Update a system import product detail

```
DEFINITION
POST http://apiserver/systemimports/:importId/products/:id/detail

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/products/40812571/detail {
    "author": "John Doe Jr."
});

EXAMPLE RESPONSE
{
    "id": null,
    "description": "5K T-Shirts (Mens)",
    "author": "John Doe Jr.",
    "isbn": "123456768789",
    "type": "P",
    "status": "A",
    "packaging": "P",
    "isUseInShoppingCart": false,
    "weight": 0,
    "isDiscountAllowed": true
}

```

Updates the specified system import product detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - the description to update the product detail with
* author (optional) - the author to update the product detail with
* isbn (optional) - the ISBN to update the product detail with
* type (optional) - the product type to update the product detail with
* status (optional) - the status to update the product detail with
* packaging (optional) - the packaging type to update the product detail with
* isUseInShoppingCart (optional) - is the product used in StudioOnline
* weight (optional) - the weight the weight to update the product detail with
* isDiscountAllowed (optional) - is a discount allowed

##### Returns

Returns the system import product detail object if the update succeeded. Returns an error if update parameters are invalid.