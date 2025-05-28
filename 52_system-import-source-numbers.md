# System Import Source Numbers

#### Retrieve a system import source number

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/numbers/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "ACTVUSERS",
    "value": 50,
    "isActive": true
}

```

Retrieves the details of an existing system import source number. You need only supply the id.

##### Arguments

* id (required) - The id of the system import source number to be retrieved.

#### Update a system import source number

```
DEFINITION
POST http://apiserver/systemimports/:importId/sources/:sourceId/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/sources/40812571/numbers/1", {
    "type": "ACTIVUSRS",
    "value": 45
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "ACTIVUSRS",
    "value": 45,
    "isActive": true
}

```

Updates the specified system import source number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the number type to update the source number with
* value (optional) - the value to update the source number with
* isActive (optional) - is the source number active

##### Returns

Returns the system import source number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import source number

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/sources/:sourceId/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/sources/40812571/numbers/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import source number. It cannot be undone.

##### Arguments

* id (required) - The id of the system import source number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import source number does not exist, this call returns an error.

#### List all system import source numbers

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/numbers");

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
            "type": "ACTVUSERS",
            "value": 50,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all system import source numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit system import source numbers, starting at index offset. Each entry in the array is a separate system import source number object. If no more system import source numbers are available, the resulting array will be empty. This request should never return an error.