# System Import Project Errors

#### Retrieve a system import project error

```
DEFINITION
GET http://apiserver/systemimports/:importId/projects/:projectId/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/projects/40812571/errors/960");

EXAMPLE RESPONSE
{
    "id": "960",
    "comment": "F200 is not a valid Project"
}

```

Retrieves the details of an existing system import project error. You need only supply the id.

##### Arguments

* id (required) - The id of the system import project error to be retrieved.

#### List all system import project errors

```
DEFINITION
GET http://apiserver/systemimports/:importId/projects/:projectId/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/projects/40812571/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "960",
            "comment": "F200 is not a valid Project"
        },
        {...},
    ]
}

```

Returns a list of all system import project errors.

##### Returns

A dictionary with an items property that contains an array of up to limit system import project errors, starting at index offset. Each entry in the array is a separate system import project error object. If no more system import project errors are available, the resulting array will be empty. This request should never return an error.