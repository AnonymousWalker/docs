# Gift Aid Claim Donations

#### List all gift aid claim donations

```
DEFINITION
GET http://apiserver/giftaidclaims/:claimNumber/donations

EXAMPLE REQUEST
$.get("http://localhost:49195/giftaidclaims/18/donations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "amount": 140
            "date": "2018-05-03"
            "documentNumber": "1234"
            "firstName": "John"
            "lastName": "Doe"
            "project": "PROJ1"
            "projectDescription": "Project 1"
            "zipPostal": "N1 0AA"
        },
        {...},
    ]
}

```

Returns a list of all gift aid claim donations. You need only supply the claim number.

##### Arguments

* claimNumber (required) - The id of the claim number the donations are associated to.

##### Returns

A dictionary with an items property that contains an array of up to limit gift aid claim donations, starting at index offset. Each entry in the array is a separate gift aid claim object. If no more gift aid claim donations are available, the resulting array will be empty. This request should never return an error.

#### Remove a gift aid claim donation

```
DEFINITION
DELETE http://apiserver/giftaidclaims/:claimNumber/donations/:documentNumber

EXAMPLE REQUEST
$.ajax("http://localhost:49195/giftaidclaims/18/donations/1234", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Removes a gift aid claim donation from the gift aid claim. This will remove all donations under the given document number.

##### Arguments

* documentNumer (required) - The document number for donation to be removed.

##### Returns

Returns a `204 No Content` response on success. If the gift aid claim donation does not exist, this call returns an error.