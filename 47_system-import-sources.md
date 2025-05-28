# System Import Sources

#### Retrieve a system import source

```
DEFINITION
GET http://apiserver/systemimports/:systemImportId/sources/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571");

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "A",
    "status": "E",
    "source": "DDCSOURCE"
}

```

Retrieves the details of an existing system import source. You need only supply the id.

##### Arguments

* id (required) - The id of the system import source to be retrieved.

#### Update a system import source

```
DEFINITION
POST http://apiserver/systemimports/:importId/sources/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/sources/40812571", {
    "status": "Y"
});

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "A",
    "status": "Y",
    "source": "DDCSOURCE"
}

```

Updates the specified system import source by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* status (optional) - the status to update the source with
* action (optional) - the action to update the source with
* source (optional) - the source code value to update the source with

##### Returns

Returns the system import source object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system import sources

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources?status=E");

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
            "action": "A",
            "status": "E",
            "source": "DDCSOURCE"
        },
        {...},
    ]
}

```

Returns a list of all system import source.

##### Arguments

* status (optional) - the status to filter the list of results on
* action (optional) - the action to filter the list of results on
* source (optional) - the source code value to filter the list of results on

##### Returns

A dictionary with an items property that contains an array of up to limit system import source, starting at index offset. Each entry in the array is a separate system import source object. If no more system import source codes are available, the resulting array will be empty. This request should never return an error.