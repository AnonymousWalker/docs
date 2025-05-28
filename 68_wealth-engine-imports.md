# Wealth Engine Imports

#### Retrieve a wealth engine import

```
DEFINITION
GET http://apiserver/wealthengineimports/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/wealthengineimports/27");

EXAMPLE RESPONSE
{
    "id": "27",
    "job": "556",
    "segment": null,
    "importId": null,
    "numberOfAccounts": 2,
    "status": "P",
    "message": "There has been a problem getting the account Wealth Engine data.",
    "fileUploaded": null,
    "statusDate": "2015-03-31T07:08:25 AM",
    "requestedStartDate": "2015-03-31T07:08:10 AM",
    "processEndDate": null
}

```

Retrieves the details of an existing wealth engine import. You need only supply the id.

##### Arguments

* id (required) - The id of the wealth engine import to be retrieved.

#### List all wealth engine imports

```
DEFINITION
GET http://apiserver/wealthengineimports

EXAMPLE REQUEST
$.get("http://localhost:49195/wealthengineimports?job=556");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "27",
            "job": "556",
            "segment": null,
            "importId": null,
            "numberOfAccounts": 2,
            "status": "P",
            "message": "There has been a problem getting the account Wealth Engine data.",
            "fileUploaded": null,
            "statusDate": "2015-03-31T07:08:25 AM",
            "requestedStartDate": "2015-03-31T07:08:10 AM",
            "processEndDate": null
        },
        {...},
    ]
}

```

Returns a list of all wealth engine imports.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - the import run id to filter the results by
* requestedStartDate (optional) - the request date to filter the results by
* job (optional) - the segmentation job number to filter the results by
* segment (optional) - the segment number to filter the results by
* status (optional) - the current status to filter the results by

##### Returns

A dictionary with an items property that contains an array of up to limit wealth engine imports, starting at index offset. Each entry in the array is a separate wealth engine import object. If no more wealth engine imports are available, the resulting array will be empty. This request should never return an error.