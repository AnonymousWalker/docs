# System Import Data Type Errors

#### Retrieve a system import data type error

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/errors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/errors/956");

EXAMPLE RESPONSE
{
    "id": "956",
    "comment": "DONOR is not a valid Code Value"
}

```

Retrieves the details of an existing system import data type error. You need only supply the id.

##### Arguments

* id (required) - The id of the system import data type error to be retrieved.

#### List all system import data type errors

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "956",
            "comment": "DONOR is not a valid Code Value"
        },
        {...},
    ]
}

```

Returns a list of all system import data type errors.

##### Returns

A dictionary with an items property that contains an array of up to limit system import data type errors, starting at index offset. Each entry in the array is a separate system import data type error object. If no more system import data type errors are available, the resulting array will be empty. This request should never return an error.