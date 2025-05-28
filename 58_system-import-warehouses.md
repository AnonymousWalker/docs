# System Import Warehouses

#### Retrieve a system import warehouse

```
DEFINITION
GET http://apiserver/systemimports/:importId/warehouses/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/warehouses/40812571");

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "A",
    "status": "P",
    "warehouse": "MAIN"
}

```

Retrieves the details of an existing system import warehouse. You need only supply the id.

##### Arguments

* id (required) - The id of the system import warehouse to be retrieved.

#### Update a system import warehouse

```
DEFINITION
POST http://apiserver/systemimports/:importId/warehouses/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/warehouses/40812571", {
    "action": "U"
});

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "P",
    "warehouse": "MAIN"
}


```

Updates the specified system import warehouse by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* action (optional) - the action to update the warehouse with
* status (optional) - the status to update the warehouse with
* warehouse (optional) - the warehouse code to update the warehouse with

##### Returns

Returns the system import warehouse object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system import warehouses

```
DEFINITION
GET http://apiserver/systemimports/:importId/warehouses

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/:importId/warehouses?");

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
            "status": "P",
            "warehouse": "MAIN"
        },
        {...},
    ]
}

```

Returns a list of all system import warehouses.

##### Arguments

* action (optional) - the action to filter the results on
* status (optional) - the status to filter the results on
* warehouse (optional) - the warehouse code to filter the results on

##### Returns

A dictionary with an items property that contains an array of up to limit system import warehouses, starting at index offset. Each entry in the array is a separate system import warehouse object. If no more system import warehouses are available, the resulting array will be empty. This request should never return an error.

#### Retrieve a system import warehouse detail

```
DEFINITION
GET http://apiserver/systemimports/:importId/warehouses/:id/detail

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/warehouses/40812571/detail");

EXAMPLE RESPONSE
{
    "description": "Main - No bins",
    "company": "010"
}

```

Retrieves the details of an existing system import warehouse detail. You need only supply the id.

##### Arguments

* id (required) - The id of the system import warehouse detail to be retrieved.

#### Update a system import warehouse detail

```
DEFINITION
POST http://apiserver/systemimports/:importId/warehouses/:id/detail

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/warehouses/40812571/detail", {
    "description": "Main - No blue bins"
});

EXAMPLE RESPONSE
{
    "description": "Main - No blue bins",
    "company": "010"
}

```

Updates the specified system import warehouse detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - the description to update the warehouse detail with
* company (optional) - the company to update the warehouse detail with

##### Returns

Returns the system import warehouse detail object if the update succeeded. Returns an error if update parameters are invalid.