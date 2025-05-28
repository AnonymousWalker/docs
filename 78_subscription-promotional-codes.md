# Subscription Promotional Codes

#### Create a subscription promotional code

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/promotionalcodes

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes", {
    "promoCode": "SUBPROMO",
    "description": "Subscription Promotional Code"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "promoCode": "SUBPROMO",
    "description": "Subscription Promotional Code",
    "startDate": null,
    "endDate": null,
    "overrideSourceCode": null,
    "overrideSourceCodeDescription": null
}

```

Creates a new subscription promotional code.

##### Arguments

* promoCode (required) - the promotional code value to create the subscription promotional code with.
* description - the description to create the subscription promotional code with.
* startDate - the start date to create the subscription promotional code with.
* endDate - the end date to create the subscription promotional code with.
* overrideSourceCode - the source code override value to create the subscription promotional code with.

##### Returns

Returns a subscription promotional code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription promotional code

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/promotionalcodes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "promoCode": "SUBPROMO",
    "description": "Subscription Promotional Code",
    "startDate": null,
    "endDate": null,
    "overrideSourceCode": null,
    "overrideSourceCodeDescription": null
}

```

Retrieves the details of an existing subscription promotional code. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription promotional code to be retrieved.

#### Update a subscription promotional code

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/promotionalcodes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes/1", {
    "startDate": "2019-01-01"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "promoCode": "SUBPROMO",
    "description": "Subscription Promotional Code",
    "startDate": "2019-01-01",
    "endDate": null,
    "overrideSourceCode": null,
    "overrideSourceCodeDescription": null
}

```

Updates the specified subscription promotional code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* promoCode - the promotional code value to update the subscription promotional code with.
* description - the description to update the subscription promotional code with.
* startDate - the start date to update the subscription promotional code with.
* endDate - the end date to update the subscription promotional code with.
* overrideSourceCode - the source code override value to update the subscription promotional code with.

##### Returns

Returns the subscription promotional code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription promotional code

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/promotionalcodes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription promotional code. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription promotional code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription promotional code does not exist, this call returns an error.

#### List all subscription promotional codes

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/promotionalcodes

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes");

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
            "promoCode": "SUBPROMO",
            "description": "Subscription Promotional Code",
            "startDate": "2019-01-01",
            "endDate": null,
            "overrideSourceCode": null,
            "overrideSourceCodeDescription": null
        },
        {...},
    ]
}

```

Returns a list of all subscription promotional codes.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription promotional codes, starting at index offset. Each entry in the array is a separate subscription promotional code object. If no more subscription promotional codes are available, the resulting array will be empty. This request should never return an error.