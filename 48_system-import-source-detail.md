# System Import Source Detail

#### Retrieve a system import source detail

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:id/detail

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/detail");

EXAMPLE RESPONSE
{
    "description": "DDC Source Import",
    "elementGroup": "D01L9",
    "start": "2015-09-03",
    "end": "2015-09-03",
    "isActive": true,
    "defaultProject": "012000",
    "defaultSubscription": "ANNUAL",
    "defaultEvent": "2DAC"
}

```

Retrieves the details of an existing system import source detail. You need only supply the id.

##### Arguments

* id (required) - The id of the system import source detail to be retrieved.

#### Update a system import source detail

```
DEFINITION
POST http://apiserver/systemimports/:importId/sources/:sourceId/detail/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/:importId/sources/:sourceId/detail/", {
    "elementGroup": "AFP02"
});

EXAMPLE RESPONSE
{
    "description": "DDC Source Import",
    "elementGroup": "AFP02",
    "start": "2015-09-03",
    "end": "2015-09-03",
    "isActive": true,
    "defaultProject": "012000",
    "defaultSubscription": "ANNUAL",
    "defaultEvent": "2DAC"
}

```

Updates the specified system import source detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - the description to update the source detail with
* elementGroup (optional) - the element group code to update the source detail with
* start (optional) - the start date to update the source detail with
* end (optional) - the end date to update the source detail with
* isActive (optional) - is the source detail active
* defaultProject (optional) - the default project code to update the source detail with
* defaultSubscription (optional) - the default subscription code to update the source detail with
* defaultEvent (optional) - the default event code to update the source detail with

##### Returns

Returns the system import source detail object if the update succeeded. Returns an error if update parameters are invalid.