# System Import Data Type Code Values

#### Retrieve a system import data type code value

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevalues/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalues/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "value": "DONOR",
    "description": "Major Donor",
    "isActive": true
}

```

Retrieves the details of an existing system import data type code value. You need only supply the id.

##### Arguments

* id (required) - The id of the system import data type code value to be retrieved.

#### Update a system import data type code value

```
DEFINITION
POST http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevalues/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalues/1", {
    "description": "Major Donor - L1"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "value": "DONOR",
    "description": "Major Donor - L1",
    "isActive": true
}

```

Updates the specified system import data type code value by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* value (optional) - the new code value
* description (optional) - the new code value description
* isActive (optional) - boolean is the code value active

##### Returns

Returns the system import data type code value object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import data type code value

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevalues/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalues/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import data type code value. It cannot be undone.

##### Arguments

* id (required) - The id of the system import data type code value to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import data type code value does not exist, this call returns an error.

#### List all system import data type code values

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevalues

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalues");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1",
            "value": "DONOR",
            "description": "Major Donor",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all system import data type code values.

##### Returns

A dictionary with an items property that contains an array of up to limit system import data type code values, starting at index offset. Each entry in the array is a separate system import data type code value object. If no more system import data type code values are available, the resulting array will be empty. This request should never return an error.