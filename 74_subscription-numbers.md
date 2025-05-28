# Subscription Numbers

#### Create a subscription number

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/numbers", {
    "type": "DDCSUBNR1",
    "value": 1289
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCSUBNR1",
    "typeDescription": "Subscription Number 1",
    "value": 1289,
    "isActive": true
}

```

Creates a new subscription number.

##### Arguments

* type (required) - the type to create the subscription number with
* value (required) - the value to create the subscription number with
* isActive (optional: defaults to true) - is the subscription number active

##### Returns

Returns a subscription number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription number

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/numbers/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCSUBNR1",
    "typeDescription": "Subscription Number 1",
    "value": 1289,
    "isActive": true
}

```

Retrieves the details of an existing subscription number. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription number to be retrieved.

#### Update a subscription number

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/numbers/8", {
    "value": 1521
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCSUBNR1",
    "typeDescription": "Subscription Number 1",
    "value": 1521,
    "isActive": true
}

```

Updates the specified subscription number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the type to update the subscription number with
* value (optional) - the value to update the subscription number with
* isActive (optional) - is the subscription number active

##### Returns

Returns the subscription number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription number

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/numbers/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription number. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription number does not exist, this call returns an error.

#### List all subscription numbers

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/:subscriptionCode/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "8",
            "type": "DDCSUBNR1",
            "typeDescription": "Subscription Number 1",
            "value": 1289,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all subscription numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription numbers, starting at index offset. Each entry in the array is a separate subscription number object. If no more subscription numbers are available, the resulting array will be empty. This request should never return an error.