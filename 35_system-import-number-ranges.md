# System Import Number Ranges

#### Retrieve a system import number range

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/numberranges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/numberranges/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "numberLow": "15",
    "numberHigh": "75"
}

```

Retrieves the details of an existing system import number range. You need only supply the id.

##### Arguments

* id (required) - The id of the system import number range to be retrieved.

#### Update a system import number range

```
DEFINITION
POST http://apiserver/systemimports/:importId/datatypes/:dataTypeId/numberranges/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/datatypes/40812571/numberranges/1", {
    "numberLow": "5"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "numberLow": "5",
    "numberHigh": "75"
}

```

Updates the specified system import number range by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* numberLow (optional) - the lower number range value
* numberHigh (optional) - the upper number range value

##### Returns

Returns the system import number range object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import number range

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/dataTypes/:dataTypeId/numberranges/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/datatypes/40812571/numberranges/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import number range. It cannot be undone.

##### Arguments

* id (required) - The id of the system import number range to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import number range does not exist, this call returns an error.

#### List all system import number ranges

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/numberranges

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/numberranges");

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
            "numberLow": "15",
            "numberHigh": "75"
        },
        {...},
    ]
}

```

Returns a list of all system import number ranges.

##### Returns

A dictionary with an items property that contains an array of up to limit system import number ranges, starting at index offset. Each entry in the array is a separate system import number range object. If no more system import number ranges are available, the resulting array will be empty. This request should never return an error.