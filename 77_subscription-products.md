# Subscription Products

#### Create a subscription product

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/products

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/products", {
    "product": "100BKLET",
    "fulfillmentDate": "2015-10-20",
    "quantityFulfilled": 1,
    "numberOfSubscriptions": 1
});

EXAMPLE RESPONSE
{
    "id": "44",
    "product": "100BKLET",
    "description": "Small Booklet",
    "fulfillmentDate": "2015-10-20",
    "quantityFulfilled": 1,
    "numberOfSubscriptions": 1
}

```

Creates a new subscription product.

##### Arguments

* product (required) - the product code to create the subscription product with
* fulfillmentDate (required) - the fulfillment date to create the subscription product with
* quantityFulfilled (required) - the number of fulfilled products to create the subscription product with
* numberOfSubscriptions (required) - the number of subscriptions to create the subscription product with

##### Returns

Returns a subscription product object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription product

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/products/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/products/44");

EXAMPLE RESPONSE
{
    "id": "44",
    "product": "100BKLET",
    "description": "Small Booklet",
    "fulfillmentDate": "2015-10-20",
    "quantityFulfilled": 1,
    "numberOfSubscriptions": 1
}

```

Retrieves the details of an existing subscription product. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription product to be retrieved.

#### Update a subscription product

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/products/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/products/44", {
    "fulfillmentDate": "2015-08-20"
});

EXAMPLE RESPONSE
{
    "id": "44",
    "product": "100BKLET",
    "description": "Small Booklet",
    "fulfillmentDate": "2015-08-20",
    "quantityFulfilled": 1,
    "numberOfSubscriptions": 1
}

```

Updates the specified subscription product by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* product (optional) - the product code to update the subscription product with
* fulfillmentDate (optional) - the fulfillment date to update the subscription product with
* quantityFulfilled (optional) - the number of fulfilled products to update the subscription product with
* numberOfSubscriptions (optional) - the number of subscriptions to update the subscription product with

##### Returns

Returns the subscription product object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription product

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/products/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/products/44", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription product. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription product to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription product does not exist, this call returns an error.

#### List all subscription products

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/products

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/products");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "44",
            "product": "100BKLET",
            "description": "Small Booklet",
            "fulfillmentDate": "2015-10-20",
            "quantityFulfilled": 1,
            "numberOfSubscriptions": 1
        },
        {...},
    ]
}

```

Returns a list of all subscription products.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription products, starting at index offset. Each entry in the array is a separate subscription product object. If no more subscription products are available, the resulting array will be empty. This request should never return an error.