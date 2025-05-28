# System Import Pledge Dates

#### Retrieve a system import pledge date

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/dates/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "dateType": "OPENDATE",
    "dateValue": "2015-08-31",
    "isActive": true
}

```

Retrieves the details of an existing system import pledge date. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge date to be retrieved.

#### Update a system import pledge date

```
DEFINITION
POST http://apiserver/systemimports/:importId/pledges/:pledgeId/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/:importId/pledges/:pledgeId/dates/1", {
    "dateType": "CLOSEDATE"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "dateType": "OPENDATE",
    "dateValue": "2015-08-31",
    "isActive": true
}

```

Updates the specified system import pledge date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* dateType (optional) - the date type to update the pledge date with
* dateValue (optional) - the date value to update the pledge date with
* isActive (optional) - is the pledge date active

##### Returns

Returns the system import pledge date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import pledge date

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/pledges/:pledgeId/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/pledges/40812571/dates/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import pledge date. It cannot be undone.

##### Arguments

* id (required) - The id of the system import pledge date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import pledge date does not exist, this call returns an error.

#### List all system import pledge dates

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/:importId/pledges/:pledgeId/dates?");

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
            "dateType": "OPENDATE",
            "dateValue": "2015-08-31",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all system import pledge dates.

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledge dates, starting at index offset. Each entry in the array is a separate system import pledge date object. If no more system import pledge dates are available, the resulting array will be empty. This request should never return an error.