# System Import Pledge Errors

#### Retrieve a system import pledge error

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/errors/957");

EXAMPLE RESPONSE
{
    "id": "957",
    "comment": "SAMPLEPLDG is not a valid Pledge Code"
}

```

Retrieves the details of an existing system import pledge error. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge error to be retrieved.

#### List all system import pledge errors

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "957",
            "comment": "SAMPLEPLDG is not a valid Pledge Code"
        },
        {...},
    ]
}

```

Returns a list of all system import pledge errors.

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledge errors, starting at index offset. Each entry in the array is a separate system import pledge error object. If no more system import pledge errors are available, the resulting array will be empty. This request should never return an error.