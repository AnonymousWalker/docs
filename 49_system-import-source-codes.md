# System Import Source Codes

#### Retrieve a system import source code

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/codes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "oldType": "OLDTYPE",
    "oldValue": "VALOLD",
    "newType": "CODENEW",
    "newValue": "VALNEW",
    "isActive": false
}

```

Retrieves the details of an existing system import source code. You need only supply the id.

##### Arguments

* id (required) - The id of the system import source code to be retrieved.

#### Update a system import source code

```
DEFINITION
POST http://apiserver/systemimports/:importId/sources/:sourceId/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/sources/40812571/codes/1", {
    "oldType": "OLDCODE"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "oldType": "OLDCODE",
    "oldValue": "VALOLD",
    "newType": "CODENEW",
    "newValue": "VALNEW",
    "isActive": false
}

```

Updates the specified system import source code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* oldType (optional) - the old code type to update the source code with
* oldValue (optional) - the old code value to update the source code with
* newType (optional) - the new code type to update the source code with
* newValue (optional) - the new code value to update the source code with
* isActive (optional) - Is the source code active

##### Returns

Returns the system import source code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import source code

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/sources/:sourceId/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/sources/40812571/codes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import source code. It cannot be undone.

##### Arguments

* id (required) - The id of the system import source code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import source code does not exist, this call returns an error.

#### List all system import source codes

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/codes");

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
            "oldType": "OLDTYPE",
            "oldValue": "VALOLD",
            "newType": "CODENEW",
            "newValue": "VALNEW",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all system import source codes.

##### Returns

A dictionary with an items property that contains an array of up to limit system import source codes, starting at index offset. Each entry in the array is a separate system import source code object. If no more system import source codes are available, the resulting array will be empty. This request should never return an error.