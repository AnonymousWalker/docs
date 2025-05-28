# System Import Source Dates

#### Retrieve a system import source date

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/dates/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "OPENDATE",
    "value": "2015-08-31",
    "isActive": true
}

```

Retrieves the details of an existing system import source date. You need only supply the id.

##### Arguments

* id (required) - The id of the system import source date to be retrieved.

#### Update a system import source date

```
DEFINITION
POST http://apiserver/systemimports/:importId/sources/:sourceId/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/sources/40812571/dates/1", {
    "dateType": "CLOSEDATE"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "OPENDATE",
    "value": "2015-08-31",
    "isActive": true
}

```

Updates the specified system import source date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the date type to update the source date with
* value (optional) - the date value to update the source date with
* isActive (optional) - is the source date active

##### Returns

Returns the system import source date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import source date

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/sources/:sourceId/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/sources/40812571/dates/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import source date. It cannot be undone.

##### Arguments

* id (required) - The id of the system import source date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import source date does not exist, this call returns an error.

#### List all system import source dates

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/:importId/sources/:sourceId/dates?");

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
            "type": "OPENDATE",
            "value": "2015-08-31",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all system import source dates.

##### Returns

A dictionary with an items property that contains an array of up to limit system import source dates, starting at index offset. Each entry in the array is a separate system import source date object. If no more system import source dates are available, the resulting array will be empty. This request should never return an error.