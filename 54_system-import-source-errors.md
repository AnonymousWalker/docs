# System Import Source Errors

#### Retrieve a system import source error

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/errors/957");

EXAMPLE RESPONSE
{
    "id": "957",
    "comment": "SAMPLEPLDG is not a valid source Code"
}

```

Retrieves the details of an existing system import source error. You need only supply the id.

##### Arguments

* id (required) - The id of the system import source error to be retrieved.

#### List all system import source errors

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/errors");

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
            "comment": "SAMPLEPLDG is not a valid source Code"
        },
        {...},
    ]
}

```

Returns a list of all system import source errors.

##### Returns

A dictionary with an items property that contains an array of up to limit system import source errors, starting at index offset. Each entry in the array is a separate system import source error object. If no more system import source errors are available, the resulting array will be empty. This request should never return an error.