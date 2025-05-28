# Reassign Warehouse Runs

#### Retrieve a reassign warehouse run

```
DEFINITION
GET http://apiserver/reassignwarehouses/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/reassignwarehouses/1000000004");

EXAMPLE RESPONSE
{
    "id": "1000000004",
    "runDate": "2015-09-15T09:25:41 AM",
    "product": "BK1001",
    "currentWarehouse": "10",
    "newWarehouse": "10"
}

```

Retrieves the details of an existing reassign warehouse run. You need only supply the id.

##### Arguments

* id (required) - The id of the reassign warehouse run to be retrieved.

#### List all reassign warehouse runs

```
DEFINITION
GET http://apiserver/reassignwarehouses

EXAMPLE REQUEST
$.get("http://localhost:49195/reassignwarehouses?product=BK1001");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000000004",
            "runDate": "2015-09-15T09:25:41 AM",
            "product": "BK1001",
            "currentWarehouse": "10",
            "newWarehouse": "10"
        },
        {...},
    ]
}

```

Returns a list of all reassign warehouse runs.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - the run id to filter the results on
* runDate (optional) - the run date to filter the results on
* product (optional) - the product to filter the results on
* currentWarehouse (optional) - the current warehouse to filter the results on
* newWarehouse (optional) - the new warehouse to filter the results on

##### Returns

A dictionary with an items property that contains an array of up to limit reassign warehouse runs, starting at index offset. Each entry in the array is a separate reassign warehouse run object. If no more reassign warehouse runs are available, the resulting array will be empty. This request should never return an error.