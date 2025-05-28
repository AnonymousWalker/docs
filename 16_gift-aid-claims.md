# Gift Aid Claims

#### Create a gift aid claim

```
DEFINITION
POST http://apiserver/giftaidclaims

EXAMPLE REQUEST
$.post("http://localhost:49195/giftaidclaims", {
    "startDate": "2018-05-01"
    "endDate": "2018-05-02"
    "company": "0"
});

EXAMPLE RESPONSE
204 No Content

```

Creates a new gift aid claim.

##### Arguments

* startDate (required) - The start date for the gift aid claim
* endDate (required) - The end date for the gift aid claim
* company (required) - The company for the gift aid claim

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any invalid values are provided, this call will return an error.

#### Retrieve a gift aid claim

```
DEFINITION
GET http://apiserver/giftaidclaims/:claimNumber

EXAMPLE REQUEST
$.get("http://localhost:49195/giftaidclaims/18");

EXAMPLE RESPONSE
{
    "id": "18",
    "startDate": "2018-05-01",
    "endDate": "2018-05-31",
    "company": "CMPNY1",
    "status": "R",
    "statusDescription": "Ready For Submission",
    "amountTransmitted": null,
    "totalLineItemsTransmitted": null,
    "amountReceived": null
}

```

Retrieves the details of an existing gift aid claim. You need only supply the id.

##### Arguments

* claimNumber (required) - The id of the gift aid claim to be retrieved.

#### Validate a gift aid claim

```
DEFINITION
POST http://apiserver/giftaidclaims/:claimNumber/validate

EXAMPLE REQUEST
$.post("http://localhost:49195/giftaidclaims/18/validate", {});

EXAMPLE RESPONSE
204 No Content

```

Validates an existing gift aid claim. You need only supply the id.

##### Arguments

* claimNumber (required) - The id of the gift aid claim to be retrieved.

#### Submit a gift aid claim

```
DEFINITION
POST http://apiserver/giftaidclaims/:claimNumber/submit

EXAMPLE REQUEST
$.post("http://localhost:49195/giftaidclaims/18/submit", {});

EXAMPLE RESPONSE
204 No Content

```

Submits an existing gift aid claim. You need only supply the id.

##### Arguments

* claimNumber (required) - The id of the gift aid claim to be retrieved.

#### Reconcile a gift aid claim

```
DEFINITION
POST http://apiserver/giftaidclaims/:claimNumber

EXAMPLE REQUEST
$.post("http://localhost:49195/giftaidclaims/18", {
    "amountReceived": 123,
    "status": "C"
});

EXAMPLE RESPONSE
{
    "id": "18",
    "startDate": "2018-05-01",
    "endDate": "2018-05-31",
    "company": "CMPNY1",
    "status": "C",
    "statusDescription": "Complete",
    "amountTransmitted": 120,
    "totalLineItemsTransmitted": 15,
    "amountReceived": 123
}


```

Reconciles the specified gift aid claim by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* amountReceived (required): The amount that was actually received from the gift aid claim
* status (required): The new status of the gift aid claim (this must be "C")

##### Returns

Returns the gift aid claim object if the reconcile succeeded. Returns an error if update parameters are invalid.

#### Delete a gift aid claim

```
DEFINITION
DELETE http://apiserver/giftaidclaims/:claimNumber

EXAMPLE REQUEST
$.ajax("http://localhost:49195/giftaidclaims/18", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a gift aid claim. It cannot be undone.

##### Arguments

* claimNumber (required) - The id of the gift aid claim to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the gift aid claim does not exist, this call returns an error.

#### List all gift aid claims

```
DEFINITION
GET http://apiserver/giftaidclaims

EXAMPLE REQUEST
$.get("http://localhost:49195/giftaidclaims?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "18",
            "startDate": "2018-05-01",
            "endDate": "2018-05-31",
            "company": "CMPNY1",
            "status": "C",
            "statusDescription": "Complete",
            "amountTransmitted": 120,
            "totalLineItemsTransmitted": 15,
            "amountReceived": 123
        },
        {...},
    ]
}

```

Returns a list of all gift aid claim.

##### Arguments

* claimNumber (optional) - The identifier of the gift aid claim
* startDate (optional) - The start date of the gift aid claim
* endDate (optional) - The end date of the gift aid claim
* status (optional) - The status of the gift aid claim

##### Returns

A dictionary with an items property that contains an array of up to limit gift aid claim, starting at index offset. Each entry in the array is a separate gift aid claim object. If no more gift aid claim are available, the resulting array will be empty. This request should never return an error.