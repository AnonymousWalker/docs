# System Import Pledge Codes

#### Retrieve a system import pledge code

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/codes/1");

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

Retrieves the details of an existing system import pledge code. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge code to be retrieved.

#### Update a system import pledge code

```
DEFINITION
POST http://apiserver/systemimports/:importId/pledges/:pledgeId/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/pledges/40812571/codes/1", {
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

Updates the specified system import pledge code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* oldType (optional) - the old code type to update the pledge code with
* oldValue (optional) - the old code value to update the pledge code with
* newType (optional) - the new code type to update the pledge code with
* newValue (optional) - the new code value to update the pledge code with
* isActive (optional) - Is the pledge code active

##### Returns

Returns the system import pledge code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import pledge code

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/pledges/:pledgeId/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/pledges/40812571/codes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import pledge code. It cannot be undone.

##### Arguments

* id (required) - The id of the system import pledge code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import pledge code does not exist, this call returns an error.

#### List all system import pledge codes

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/codes");

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

Returns a list of all system import pledge codes.

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledge codes, starting at index offset. Each entry in the array is a separate system import pledge code object. If no more system import pledge codes are available, the resulting array will be empty. This request should never return an error.