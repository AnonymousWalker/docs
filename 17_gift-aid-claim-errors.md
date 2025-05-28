# Gift Aid Claim Errors

#### Retrieve a gift aid claim error

```
DEFINITION
GET http://apiserver/giftaidclaims/:claimNumber/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/giftaidclaims/18/errors/5");

EXAMPLE RESPONSE
{
    "id": 5,
    "claimNumber": 18,
    "documentNumber": 1234,
    "errorCode": "ERR1",
    "message": "An error has occurred"
}

```

Retrieves the details of an existing gift aid claim error. You need only supply the id.

##### Arguments

* id (required) - The id of the gift aid claim error to be retrieved.

#### List all gift aid claim errors

```
DEFINITION
GET http://apiserver/giftaidclaims/:claimNumber/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/giftaidclaims/18/errors?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": 5,
            "claimNumber": 18,
            "documentNumber": 1234,
            "errorCode": "ERR1",
            "message": "An error has occurred"
        },
        {...},
    ]
}

```

Returns a list of all gift aid claim error.

##### Arguments

* claimNumber (optional) - The id of the claim that the error is associated with
* documentNumber (optional) - The document number associated with the error
* errorCode (optional) - The error code for the error

##### Returns

A dictionary with an items property that contains an array of up to limit gift aid claim error, starting at index offset. Each entry in the array is a separate gift aid claim object. If no more gift aid claim error are available, the resulting array will be empty. This request should never return an error.