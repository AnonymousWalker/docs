# System Import Data Types

#### Retrieve a system import data type

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571");

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "P",
    "type": "DDCPRODPC"
}

```

Retrieves the details of an existing system import data type. You need only supply the ids.

##### Arguments

* importId (required) - The id of the system import associated with the data type.
* dataTypeId (required) - The id of the system import data type to be retrieved.

#### Update a system import data type

```
DEFINITION
POST http://apiserver/systemimports/:importId/datatypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/datatypes/40812571", {
    "status": "E"
});

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "E",
    "type": "DDCPRODPC"
}

```

Updates the specified system import data type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* status (optional) - The status to update the data type with.

##### Returns

Returns the system import data type object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system import data types

```
DEFINITION
GET http://apiserver/systemimports/10000047/datatypes/40812571

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "40812571",
            "action": "U",
            "status": "P",
            "type": "DDCPRODPC"
        },
        {...},
    ]
}

```

Returns a list of all system import data types.

##### Returns

A dictionary with an items property that contains an array of up to limit system import data types, starting at index offset. Each entry in the array is a separate system import object. If no more system import data types are available, the resulting array will be empty. This request should never return an error.