# System Import Projects

#### Retrieve a system import project

```
DEFINITION
GET http://apiserver/systemimports/:importId/projects/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/projects/40812571");

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "Y",
    "project": "001871"
}

```

Retrieves the details of an existing system import project. You need only supply the id.

##### Arguments

* id (required) - The id of the system import project to be retrieved.

#### Update a system import project

```
DEFINITION
POST http://apiserver/systemimports/:importId/projects/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/:importId/projects/40812571", {
    "status": "E"
});

EXAMPLE RESPONSE
{
    "id": "40812571",
    "action": "U",
    "status": "E",
    "project": "001871"
}

```

Updates the specified system import project by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* action (optional) - the action to update the project with
* status (optional) - the status to update the project with
* project (optional) - the project code to update the project with

##### Returns

Returns the system import project object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system import projects

```
DEFINITION
GET http://apiserver/systemimports/:importId/projects

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/projects?");

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
            "action": "U",
            "status": "Y",
            "project": "001871"
        },
        {...},
    ]
}

```

Returns a list of all system import projects.

##### Arguments

* action (optional) - the action to filter the results on
* status (optional) - the status to filter the results on
* project (optional) - the project code to filter the results on

##### Returns

A dictionary with an items property that contains an array of up to limit system import projects, starting at index offset. Each entry in the array is a separate system import project object. If no more system import projects are available, the resulting array will be empty. This request should never return an error.