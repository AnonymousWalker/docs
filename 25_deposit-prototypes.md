# Deposit Prototypes

#### Create a Deposit Prototype

```
DEFINITION
POST http://apiserver/depositprototypes

EXAMPLE REQUEST
$.post("http://localhost:49195/depositprototypes", {
    "company": "4",
    "currency": "USD",
    "payType": "CC",
    "bankCode": "BOA",
    "paymentGatewayCode": "CCONNECT"
});

EXAMPLE RESPONSE
{
    "id": "15"
    "company": "4",
    "currency": "USD",
    "payType": "CC",
    "endTime": null,
    "bankCode": "BOA",
    "paymentGatewayCode": "CCONNECT",
    "paymentGatewayDescription": "Clover Connect"
}

```

Creates a new Deposit Prototype.

##### Arguments

* company (required) - The company code for the deposit prototype.
* currency (required) - The currency code for the deposit prototype.
* payType (required) - The payment type for the deposit prototype.
* endTime (optional) - The end time for the deposit prototype. Provide in 12-hour format with AM/PM.
* bankCode (required) - The bank code for the deposit prototype.
* paymentGatewayCode (optional) - The code of the company payment gateway to be used for CC and EFT payment types.

##### Returns

Returns a Deposit Prototype object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Deposit Prototype

```
DEFINITION
GET http://apiserver/depositprototypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/depositprototypes/15");

EXAMPLE RESPONSE
{
    "id": "15"
    "company": "4",
    "currency": "USD",
    "payType": "CC",
    "endTime": null,
    "bankCode": "BOA",
    "paymentGatewayCode": "CCONNECT",
    "paymentGatewayDescription": "Clover Connect"
}

```

Retrieves the details of an existing Deposit Prototype. You need only supply the id.

##### Arguments

* id (required) - The id of the Deposit Prototype to be retrieved.

#### Update a Deposit Prototype

```
DEFINITION
POST http://apiserver/depositprototypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/depositprototypes/15", {
    "currency": "CND",
    "payType": "CK"
});

EXAMPLE RESPONSE
{
    "id": "15"
    "company": "4",
    "currency": "CND",
    "payType": "CK",
    "endTime": null,
    "bankCode": "BOA",
    "paymentGatewayCode": "CCONNECT",
    "paymentGatewayDescription": "Clover Connect"
}


```

Updates the specified Deposit Prototype by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* company (optional) - The company code for the deposit prototype.
* currency (optional) - The currency code for the deposit prototype.
* payType (optional) - The payment type for the deposit prototype.
* endTime (optional) - The end time for the deposit prototype. Provide in 12-hour format with AM/PM.
* bankCode (optional) - The bank code for the deposit prototype.
* paymentGatewayCode (optional) - The code of the company payment gateway to be used for CC and EFT payment types.

##### Returns

Returns the Deposit Prototype object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Deposit Prototype

```
DEFINITION
DELETE http://apiserver/depositprototypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/depositprototypes/15", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Deposit Prototype. It cannot be undone.

##### Arguments

* id (required) - The id of the Deposit Prototype to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Deposit Prototype does not exist, this call returns an error.

#### List all Deposit Prototypes

```
DEFINITION
GET http://apiserver/depositprototypes

EXAMPLE REQUEST
$.get("http://localhost:49195/depositprototypes", {
    "currency": "CND",
    "payType": "CK"
});

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "15"
            "company": "4",
            "currency": "CND",
            "payType": "CK",
            "endTime": null,
            "bankCode": "BOA",
            "paymentGatewayCode": "CCONNECT",
            "paymentGatewayDescription": "Clover Connect"
        },
        {...},
    ]
}

```

Returns a list of all Deposit Prototypes.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* company (optional) - The company code for the deposit prototype.
* currency (optional) - The currency code for the deposit prototype.
* payType (optional) - The payment type for the deposit prototype.
* bankCode (optional) - The bank code for the deposit prototype.

##### Returns

A dictionary with an items property that contains an array of up to limit Deposit Prototypes, starting at index offset. Each entry in the array is a separate Deposit Prototype object. If no more Deposit Prototypes are available, the resulting array will be empty. This request should never return an error.