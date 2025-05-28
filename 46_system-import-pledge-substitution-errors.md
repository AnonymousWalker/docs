# System Import Pledge Substitution Errors

#### Retrieve a system import pledge substitution error

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledgesubstitutions/:pledgeSubstitutionId/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledgesubstitutions/40812571/errors/958");

EXAMPLE RESPONSE
{
    "id": "958",
    "comment": "DDCPLDGE is not a valid Pledge Code"
}

```

Retrieves the details of an existing system import pledge substitution error. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge substitution error to be retrieved.

#### List all system import pledge substitution errors

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledgesubstitutions/:pledgeSubstitutionId/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledgesubstitutions/40812571/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "958",
            "comment": "DDCPLDGE is not a valid Pledge Code"
        },
        {...},
    ]
}

```

Returns a list of all system import pledge substitution errors.

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledge substitution errors, starting at index offset. Each entry in the array is a separate system import pledge substitution error object. If no more system import pledge substitution errors are available, the resulting array will be empty. This request should never return an error.