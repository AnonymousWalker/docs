# System Import Pledge Numbers

#### Retrieve a system import pledge number

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/numbers/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "ACTVUSERS",
    "value": 50,
    "isActive": true
}

```

Retrieves the details of an existing system import pledge number. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge number to be retrieved.

#### Update a system import pledge number

```
DEFINITION
POST http://apiserver/systemimports/:importId/pledges/:pledgeId/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/pledges/40812571/numbers/1", {
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

Updates the specified system import pledge number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the number type to update the pledge number with
* value (optional) - the value to update the pledge number with
* isActive (optional) - is the pledge number active

##### Returns

Returns the system import pledge number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import pledge number

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/pledges/:pledgeId/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/pledges/40812571/numbers/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import pledge number. It cannot be undone.

##### Arguments

* id (required) - The id of the system import pledge number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import pledge number does not exist, this call returns an error.

#### List all system import pledge numbers

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/numbers");

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

Returns a list of all system import pledge numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledge numbers, starting at index offset. Each entry in the array is a separate system import pledge number object. If no more system import pledge numbers are available, the resulting array will be empty. This request should never return an error.