# DACTA

#### Retrieve a DACTA Run

```
DEFINITION
GET http://apiserver/dacta/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/dacta/1000000028");

EXAMPLE RESPONSE
{
    "id": "1000000028",
    "date": "2015-09-07T10:20:00 PM"
}

```

Retrieves the details of an existing DACTA Run. You need only supply the id.

##### Arguments

* id (required) - The id of the DACTA Run to be retrieved.

#### List all DACTA runs

```
DEFINITION
GET http://apiserver/dacta

EXAMPLE REQUEST
$.get("http://localhost:49195/dacta");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000000028",
            "date": "2015-09-07T10:20:00 PM"
        },
        {...},
    ]
}

```

Returns a list of all DACTA runs.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - the run Id to filter the search results on
* date (optional) - the run date to filter the search results on

##### Returns

A dictionary with an items property that contains an array of up to limit DACTA runs, starting at index offset. Each entry in the array is a separate DACTA run object. If no more DACTA runs are available, the resulting array will be empty. This request should never return an error.