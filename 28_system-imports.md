# System Imports

#### Retrieve a system import

```
DEFINITION
GET http://apiserver/systemimports/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/8");

EXAMPLE RESPONSE
{
    "id": "10000047",
    "creationDate": "2013-12-12T11:59:48 AM",
    "dataSource": "SYLMISSION",
    "description": "Sync Price Codes from SylogistMission to SE",
    "status": "P"
}

```

Retrieves the details of an existing system import. You need only supply the id.

##### Arguments

* id (required) - The id of the system import to be retrieved.

#### Update a system import

```
DEFINITION
POST http://apiserver/systemimports/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047", {
    "status": "L"
});

EXAMPLE RESPONSE
{
    "id": "10000047",
    "creationDate": "2013-12-12T11:59:48 AM",
    "dataSource": "SYLMISSION",
    "description": "Sync Price Codes from SylogistMission to SE",
    "status": "L"
}

```

Updates the specified system import by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* status (optional) - Change the status of the import (Used for reactivation).

##### Returns

Returns the system import object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system imports

```
DEFINITION
GET http://apiserver/systemimports

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports?status=P");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10000047",
            "creationDate": "2013-12-12T11:59:48 AM",
            "dataSource": "SYLMISSION",
            "description": "Sync Price Codes from SylogistMission to SE",
            "status": "P"
        },
        {...},
    ]
}

```

Returns a list of all system imports.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - the import Id to lookup
* status (optional) - the status to filter system imports on
* creationDate (optional) - the creation date to filter on (See notes on datetime-type values above)
* dataSource (optional) - the import data source to filter on
* description (optional) - the import description to filter on

##### Returns

A dictionary with an items property that contains an array of up to limit system imports, starting at index offset. Each entry in the array is a separate system import object. If no more system imports are available, the resulting array will be empty. This request should never return an error.

### System import process

```
DEFINITION
POST http://apiserver/systemimports/:id/process

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/process");

EXAMPLE RESPONSE
{
    "id": "10000047",
    "creationDate": "2013-12-12T11:59:48 AM",
    "dataSource": "SYLMISSION",
    "description": "Sync Price Codes from SylogistMission to SE",
    "status": "L"
}

```

Runs the system import process for the selected system import.

#### Returns

Returns the updated state of the system import if the call succeeded. If the import is in an invalid state for processing - (R)unning, (P)rocessing, (E)rror - the call will fail.