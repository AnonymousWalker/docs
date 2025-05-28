# Email Service Imports

#### Retrieve an email service import

```
DEFINITION
GET http://apiserver/emailserviceimports/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/emailserviceimports/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "importId": null,
    "emailService": "SILVERPOP",
    "syncFromDate": "2015-01-01",
    "status": "R",
    "syncStartDate": "2015-07-15T10:49:20 AM",
    "syncEndDate": null,
    "numberOfImportDetails": 0
}

```

Retrieves the details of an existing email service import. You need only supply the id.

##### Arguments

* id (required) - The id of the email service import to be retrieved.

#### List all email service imports

```
DEFINITION
GET http://apiserver/emailserviceimports

EXAMPLE REQUEST
$.get("http://localhost:49195/emailserviceimports?emailService=SILVERPOP");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5",
            "importId": null,
            "emailService": "SILVERPOP",
            "syncFromDate": "2015-01-01",
            "status": "R",
            "syncStartDate": "2015-07-15T10:49:20 AM",
            "syncEndDate": null,
            "numberOfImportDetails": 0
        },
        {...},
    ]
}

```

Returns a list of all email service imports.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* emailService (optional) - the email service code to filter the results on
* status (optional) - the status to filter the results on
* importId (optional) - the import id to filter the results on

##### Returns

A dictionary with an items property that contains an array of up to limit email service imports, starting at index offset. Each entry in the array is a separate email service import object. If no more email service imports are available, the resulting array will be empty. This request should never return an error.