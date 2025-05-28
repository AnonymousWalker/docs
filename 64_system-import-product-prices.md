# System Import Product Prices

#### Retrieve a system import product price

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/prices/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/prices/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "priceCode": "E",
    "price": 17,
    "currency": "USD",
    "start": "2015-01-05",
    "end": "2015-05-05",
    "isUseInShoppingCart": false
}

```

Retrieves the details of an existing system import product price. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product price to be retrieved.

#### Update a system import product price

```
DEFINITION
POST http://apiserver/systemimports/:importId/products/:productId/prices/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/products/40812571/prices/1", {
    "end": "2016-05-05"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "priceCode": "E",
    "price": 17,
    "currency": "USD",
    "start": "2015-01-05",
    "end": "2016-05-05",
    "isUseInShoppingCart": false
}

```

Updates the specified system import product price by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* priceCode (optional) - the price code to update the product price with
* price (optional) - the price to update the product price with
* currency (optional) - the currency code to update the product price with
* start (optional) - the start date to update the product price with
* end (optional) - the end date to update the product price with
* isUseInShoppingCart (optional) - is the product price used in StudioOnline

##### Returns

Returns the system import product price object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import product price

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/products/:productId/prices/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/products/40812571/prices/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import product price. It cannot be undone.

##### Arguments

* id (required) - The id of the system import product price to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import product price does not exist, this call returns an error.

#### List all system import product prices

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/prices

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/prices?");

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
            "priceCode": "E",
            "price": 17,
            "currency": "USD",
            "start": "2015-01-05",
            "end": "2015-05-05",
            "isUseInShoppingCart": false
        },
        {...},
    ]
}

```

Returns a list of all system import product prices.

##### Returns

A dictionary with an items property that contains an array of up to limit system import product prices, starting at index offset. Each entry in the array is a separate system import product price object. If no more system import product prices are available, the resulting array will be empty. This request should never return an error.