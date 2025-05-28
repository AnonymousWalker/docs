# System Import Pledges

#### Retrieve a system import pledge

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571");

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "Y",
    "pledgeCode": "SAMPLPLDG"
}

```

Retrieves the details of an existing system import pledge. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge to be retrieved.

#### Update a system import pledge

```
DEFINITION
POST http://apiserver/systemimports/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/pledges/40812571", {
    "status": "E"
});

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "E",
    "pledgeCode": "SAMPLPLDG"
}


```

Updates the specified system import pledge by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* status (optional) - The status to update the system import pledge with

##### Returns

Returns the system import pledge object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system import pledges

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges?status=Y");

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
            "status": "Y",
            "pledgeCode": "SAMPLPLDG"
        },
        {...},
    ]
}

```

Returns a list of all system import pledges.

##### Arguments

* status (optional) - the import status to filter on

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledges, starting at index offset. Each entry in the array is a separate system import pledge object. If no more system import pledges are available, the resulting array will be empty. This request should never return an error.