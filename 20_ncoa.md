# NCOA

#### Retrieve a NCOA Run

```
DEFINITION
GET http://apiserver/ncoa/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/ncoa/111");

EXAMPLE RESPONSE
{
    "id": "111",
    "date": "2015-09-08T09:47:23 AM",
    "type": "Export",
    "segmentation": "dbo.NJ539"
}

```

Retrieves the details of an existing NCOA Run. You need only supply the id.

##### Arguments

* id (required) - The id of the NCOA Run to be retrieved.

#### List all NCOA runs

```
DEFINITION
GET http://apiserver/ncoa

EXAMPLE REQUEST
$.get("http://localhost:49195/ncoa?type=EXPORT");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "111",
            "date": "2015-09-08T09:47:23 AM",
            "type": "Export",
            "segmentation": "dbo.NJ539"
        },
        {...},
    ]
}

```

Returns a list of all NCOA runs.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - the run Id to filter the search results on
* date (optional) - the run date to filter the search results on
* type (optional) - the run type to filter the search results on
* segmentation (optional) - the segmentation to filter the search results on

##### Returns

A dictionary with an items property that contains an array of up to limit NCOA runs, starting at index offset. Each entry in the array is a separate NCOA run object. If no more NCOA runs are available, the resulting array will be empty. This request should never return an error.