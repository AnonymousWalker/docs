# Gift Aid Claim Donations By Project

#### List all gift aid claim donations by project

```
DEFINITION
GET http://apiserver/giftaidclaims/:claimNumber/donations

EXAMPLE REQUEST
$.get("http://localhost:49195/giftaidclaims/18/donationsbyproject?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "project": "PROJ1"
            "projectDescription": "Project 1"
            "amount": 247
            "glSegment1": null
            "glSegment2": null
            "glSegment3": null
            "glSegment4": null
            "glSegment5": null
            "glSegment6": null
            "glSegment7": null
            "glSegment8": null
            "glSegment9": null
            "glSegment10": null
        },
        {...},
    ]
}

```

Returns a list of all gift aid claim donations grouped by their project. You need only supply the claim number.

##### Arguments

* claimNumber (required) - The id of the claim number the donations are associated to.

##### Returns

A dictionary with an items property that contains an array of up to limit gift aid claim donations by project, starting at index offset. Each entry in the array is a separate gift aid claim object. If no more gift aid claim donations are available, the resulting array will be empty. This request should never return an error.