# System Import Date Ranges

#### Retrieve a system import date range

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/dateranges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/dateranges/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "dateLow": "2015-07-07",
    "dateHigh": "2015-08-26"
}

```

Retrieves the details of an existing system import date range. You need only supply the id.

##### Arguments

* id (required) - The id of the system import date range to be retrieved.

#### Update a system import date range

```
DEFINITION
POST http://apiserver/systemimports/:importId/datatypes/:dataTypeId/dateranges/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalueattributes/1", {
    "dateLow": "2014-12-01"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "dateLow": "2014-12-01",
    "dateHigh": "2015-08-26"
}

```

Updates the specified system import date range by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* dateLow (optional) - the lower date range value
* dateHigh (optional) - the upper date range value

##### Returns

Returns the system import date range object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import date range

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/dataTypes/:dataTypeId/dateranges/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/datatypes/40812571/dateranges/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import date range. It cannot be undone.

##### Arguments

* id (required) - The id of the system import date range to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import date range does not exist, this call returns an error.

#### List all system import date ranges

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/dateranges

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/dateranges");

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
            "dateLow": "2015-07-07",
            "dateHigh": "2015-08-26"
        },
        {...},
    ]
}

```

Returns a list of all system import date ranges.

##### Returns

A dictionary with an items property that contains an array of up to limit system import date ranges, starting at index offset. Each entry in the array is a separate system import date range object. If no more system import date ranges are available, the resulting array will be empty. This request should never return an error.