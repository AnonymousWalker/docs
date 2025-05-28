# Marketing and Analysis

### Analytics Dashboards

#### Create an analytics dashboard

```
DEFINITION
POST http://apiserver/analyticsdashboards

EXAMPLE REQUEST
$.post("http://localhost:49195/analyticsdashboards", {
    "description": "Top 5 Element Groups",
    "category": "MAILINGS",
    "categoryDescription": "Mailings",
    "SAWId": "A0000001",
    "URL": "http://moss02/sites/BI/Dashboards/Top%205%20Element%20Groups/Top%205%20Element%20Groups.aspx"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "description": "Top 5 Element Groups",
    "category": "MAILINGS",
    "categoryDescription": "Mailings",
    "SAWId": "A0000001",
    "SAWIdDescription": "Account lookup modules",
    "URL": "http://moss02/sites/BI/Dashboards/Top%205%20Element%20Groups/Top%205%20Element%20Groups.aspx"
}

```

Creates a new analytics dashboard.

##### Arguments

* description (required) - Description for the analytics dashboard
* category (required) - Category for the analytics dashboard
* SAWId (required) - SAW Id for the analytics dashboard
* URL (required) - URL of the analytics dashboard

##### Returns

Returns an analytics dashboard object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an analytics dashboard

```
DEFINITION
GET http://apiserver/analyticsdashboards/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/analyticsdashboards/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "description": "Top 5 Element Groups",
    "category": "MAILINGS",
    "categoryDescription": "Mailings",
    "SAWId": "A0000001",
    "SAWIdDescription": "Account lookup modules",
    "URL": "http://moss02/sites/BI/Dashboards/Top%205%20Element%20Groups/Top%205%20Element%20Groups.aspx"
}

```

Retrieves the details of an existing analytics dashboard. You need only supply the id.

##### Arguments

* id (required) - The id of the analytics dashboard to be retrieved.

#### Update an analytics dashboard

```
DEFINITION
POST http://apiserver/analyticsdashboards/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/analyticsdashboards/3", {
    "URL": "http://web02/sites/BI/Dashboards/Top%205%20Element%20Groups/Top%205%20Element%20Groups.aspx"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "description": "Top 5 Element Groups",
    "category": "MAILINGS",
    "categoryDescription": "Mailings",
    "SAWId": "A0000001",
    "SAWIdDescription": "Account lookup modules",
    "URL": "http://web02/sites/BI/Dashboards/Top%205%20Element%20Groups/Top%205%20Element%20Groups.aspx"
}


```

Updates the specified analytics dashboard by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description
* category
* SAWId
* URL

##### Returns

Returns the analytics dashboard object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an analytics dashboard

```
DEFINITION
DELETE http://apiserver/analyticsdashboards/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/analyticsdashboards/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an analytics dashboard. It cannot be undone.

##### Arguments

* id (required) - The id of the analytics dashboard to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the analytics dashboard does not exist, this call returns an error.

#### List all analytics dashboards

```
DEFINITION
GET http://apiserver/analyticsdashboards

EXAMPLE REQUEST
$.get("http://localhost:49195/analyticsdashboards?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "description": "Top 5 Element Groups",
            "category": "MAILINGS",
            "categoryDescription": "Mailings",
            "SAWId": "A0000001",
            "SAWIdDescription": "Account lookup modules",
            "URL": "http://web02/sites/BI/Dashboards/Top%205%20Element%20Groups/Top%205%20Element%20Groups.aspx"
        },
        {...},
    ]
}

```

Returns a list of all analytics dashboards.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* description
* category
* SAWId

##### Returns

A dictionary with an items property that contains an array of up to limit analytics dashboards, starting at index offset. Each entry in the array is a separate analytics dashboard object. If no more analytics dashboards are available, the resulting array will be empty. This request should never return an error.

### Campaigns

#### Create a campaign

```
DEFINITION
POST http://apiserver/campaigns

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns", {
    "id": "G15",
    "description": "2015 General Fund",
    "start": "2015-01-01",
    "end": "2015-12-31"
});

EXAMPLE RESPONSE
{
    "id": "G15",
    "description": "2015 General Fund",
    "start": "2015-01-01",
    "end": "2015-12-31"
}

```

Creates a new campaign.

##### Arguments

* id (required) - The unique code for the new campaign.
* description (optional) - The description of the campaign.
* start (optional) - The start date of the campaign.
* end (optional) - The end date of the campaign.

##### Returns

Returns a campaign object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve a campaign

```
DEFINITION
GET http://apiserver/campaigns/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15");

EXAMPLE RESPONSE
{
    "id": "G15",
    "description": "2015 General Fund",
    "start": "2015-01-01",
    "end": "2015-12-31"
}

```

Retrieves the details of an existing campaign. You need only supply the campaign code.

##### Arguments

* id (required) - The campaign code of the campaign to retrieve.

##### Returns

Returns a campaign object if a valid id was provided.

#### Update a campaign

```
DEFINITION
POST http://apiserver/campaigns/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15", {
    "start": "2015-01-31"
});

EXAMPLE RESPONSE
{
    "id": "G15",
    "description": "2015 General Fund",
    "start": "2015-01-31",
    "end": "2015-12-31"
}

```

Updates the specified campaign by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the campaign.
* start (optional) - The start date of the campaign.
* end (optional) - The end date of the campaign.

##### Returns

Returns the campaign object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid default project, subscription, or event code).

#### Delete a campaign

```
DEFINITION
DELETE http://apiserver/campaigns/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/campaigns/G15", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a campaign. It cannot be undone.

##### Arguments

* id (required) - The campaign code of the campaign to be deleted.

##### Returns

Returns a 204 No Content response on success. If the campaign does not exist, this call returns an error.

#### List all campaigns

```
DEFINITION
GET http://apiserver/campaigns

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 20
    }
    "items": [
        {
            "id": "G15",
            "description": "2015 General Fund",
            "start": "2015-01-31",
            "end": "2015-12-31"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all campaigns matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in campaign code
* description () - Filter list by partial match in campaign description
* status () - Filter list by status

##### Returns

A dictionary with an items property that contains an array of up to limit campaigns, starting at index offset. Each entry in the array is a separate campaign object. If no more campaigns are available, the resulting array will be empty. This request should never return an error.

### Campaign Attachments

#### Create a campaign attachment

```
DEFINITION
POST http://apiserver/campaigns/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new campaign attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a campaign attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a campaign attachment

```
DEFINITION
GET http://apiserver/campaigns/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing campaign attachment. You need only supply the campaign id and campaign attachment id.

##### Arguments

* id (required) - The id of the account attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a campaign attachment object if a valid id was provided.

#### Update a campaign attachment

```
DEFINITION
POST http://apiserver/campaigns/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/attachments/49", {
    "type": "LOGO",
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Updates the specified campaign attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the campaign attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a campaign attachment

```
DEFINITION
DELETE http://apiserver/campaigns/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/campaigns/G15/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a campaign attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the campaign attachment id does not exist, this call returns an error.

#### List all campaign attachments

```
DEFINITION
GET http://apiserver/campaigns/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all campaign attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit campaign attachments, starting at index offset. Each entry in the array is a separate campaign attachment object. If no more campaign attachments are available, the resulting array will be empty. This request should never return an error.

### Campaign Codes

#### Create a campaign code

```
DEFINITION
POST http://apiserver/campaigns/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/codes", {
    "type": "SCAMPSCOPE",
    "value": "N"
});

EXAMPLE RESPONSE
{
    "id": "12",
    "type": "SCAMPSCOPE",
    "typeDescription": null,
    "value": "N",
    "valueDescription": "National",
    "isActive": true
}

```

Creates a new campaign code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a campaign code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a campaign code

```
DEFINITION
GET http://apiserver/campaigns/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/codes/12");

EXAMPLE RESPONSE
{
    "id": "12",
    "type": "SCAMPSCOPE",
    "typeDescription": null,
    "value": "N",
    "valueDescription": "National",
    "isActive": true
}

```

Retrieves the details of an existing campaign code. You need only supply the campaign id and campaign code id.

##### Returns

Returns a campaign code object if a valid id was provided.

#### Update a campaign code

```
DEFINITION
POST http://apiserver/campaigns/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/codes/12", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "12",
    "type": "SCAMPSCOPE",
    "typeDescription": null,
    "value": "N",
    "valueDescription": "National",
    "isActive": false
}

```

Updates the specified campaign code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the campaign code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a campaign code

```
DEFINITION
DELETE http://apiserver/campaigns/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/campaigns/G15/codes/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a campaign code. It cannot be undone.

##### Arguments

* id (required) - The id of the account code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the campaign code id does not exist, this call returns an error.

#### List all campaign codes

```
DEFINITION
GET http://apiserver/campaigns/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "12",
            "type": "SCAMPSCOPE",
            "typeDescription": null,
            "value": "N",
            "valueDescription": "National",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all campaign codes.

##### Returns

A dictionary with an items property that contains an array of up to limit campaign codes, starting at index offset. Each entry in the array is a separate campaign code object. If no more campaign codes are available, the resulting array will be empty. This request should never return an error.

### Campaign Dates

#### Create a campaign date

```
DEFINITION
POST http://apiserver/campaigns/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/dates", {
    "type": "SCAMPDATE",
    "value": "2008-08-15"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SCAMPDATE",
    "typeDescription": null,
    "value": "2008-08-15",
    "isActive": true
}

```

Creates a new campaign date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a campaign date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a campaign date

```
DEFINITION
GET http://apiserver/campaigns/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/dates/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SCAMPDATE",
    "typeDescription": null,
    "value": "2008-08-15",
    "isActive": true
}

```

Retrieves the details of an existing campaign date. You need only supply the campaign id and campaign date id.

##### Returns

Returns a campaign date object if a valid id was provided.

#### Update a campaign date

```
DEFINITION
POST http://apiserver/campaigns/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/dates/9", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SCAMPDATE",
    "typeDescription": null,
    "value": "2008-08-15",
    "isActive": false
}

```

Updates the specified campaign date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the campaign date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a campaign date

```
DEFINITION
DELETE http://apiserver/campaigns/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/campaigns/G15/dates/9", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a campaign date. It cannot be undone.

##### Arguments

* id (required) - The id of the account date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the campaign date id does not exist, this call returns an error.

#### List all campaign dates

```
DEFINITION
GET http://apiserver/campaigns/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "9",
            "type": "SCAMPDATE",
            "typeDescription": null,
            "value": "2008-08-15",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all campaign dates.

##### Returns

A dictionary with an items property that contains an array of up to limit campaign dates, starting at index offset. Each entry in the array is a separate campaign date object. If no more campaign dates are available, the resulting array will be empty. This request should never return an error.

### Campaign Notes

#### Create a campaign note

```
DEFINITION
POST http://apiserver/campaigns/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/notes", {
    "type": "TESTNOTE",
    "shortComment": "Notes about the campaign"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "TESTNOTE",
    "typeDescription": "Testing Notes",
    "shortComment": "Notes about the campaign",
    "longComment": null
}

```

Creates a new campaign note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a campaign note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Retrieve a campaign note

```
DEFINITION
GET http://apiserver/campaigns/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/notes/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "TESTNOTE",
    "typeDescription": "Testing Notes",
    "shortComment": "Notes about the campaign",
    "longComment": null
}

```

Retrieves the details of an existing campaign note. You need only supply the campaign id and campaign note id.

##### Returns

Returns a campaign note object if a valid id was provided.

#### Update a campaign note

```
DEFINITION
POST http://apiserver/campaigns/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/notes/5", {
    "longComment": "now we have a\nlong comment"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "TESTNOTE",
    "typeDescription": "Testing Notes",
    "shortComment": "Notes about the campaign",
    "longComment": "now we have a\nlong comment"
}

```

Updates the specified campaign note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the campaign note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a campaign note

```
DEFINITION
DELETE http://apiserver/campaigns/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/campaigns/G15/notes/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a campaign note. It cannot be undone.

##### Arguments

* id (required) - The id of the account note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the campaign note id does not exist, this call returns an error.

#### List all campaign notes

```
DEFINITION
GET http://apiserver/campaigns/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/notes");

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
            "type": "TESTNOTE",
            "typeDescription": "Testing Notes",
            "shortComment": "Notes about the campaign",
            "longComment": "now we have a\nlong comment"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all campaign notes.

##### Returns

A dictionary with an items property that contains an array of up to limit campaign notes, starting at index offset. Each entry in the array is a separate campaign note object. If no more campaign notes are available, the resulting array will be empty. This request should never return an error.

### Campaign Numbers

#### Create a campaign number

```
DEFINITION
POST http://apiserver/campaigns/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/numbers", {
    "type": "TESTNUMS",
    "value": 7
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "TESTNUMS",
    "typeDescription": "Test Single Number",
    "value": 7,
    "isActive": true
}

```

Creates a new campaign number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be a defined value of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a campaign number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Retrieve a campaign number

```
DEFINITION
GET http://apiserver/campaigns/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/numbers/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "TESTNUMS",
    "typeDescription": "Test Single Number",
    "value": 7,
    "isActive": true
}

```

Retrieves the details of an existing campaign number. You need only supply the campaign id and campaign number id.

##### Returns

Returns a campaign number object if a valid id was provided.

#### Update a campaign number

```
DEFINITION
POST http://apiserver/campaigns/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/campaigns/G15/numbers/3", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "TESTNUMS",
    "typeDescription": "Test Single Number",
    "value": 7,
    "isActive": false
}

```

Updates the specified campaign number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be a defined value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the campaign number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a campaign number

```
DEFINITION
DELETE http://apiserver/campaigns/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/campaigns/G15/numbers/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a campaign number. It cannot be undone.

##### Arguments

* id (required) - The id of the account number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the campaign number id does not exist, this call returns an error.

#### List all campaign numbers

```
DEFINITION
GET http://apiserver/campaigns/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/campaigns/G15/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "type": "TESTNUMS",
            "typeDescription": "Test Single Number",
            "value": 7,
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all campaign numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit campaign numbers, starting at index offset. Each entry in the array is a separate campaign number object. If no more campaign numbers are available, the resulting array will be empty. This request should never return an error.

### Cultivation Tracks

#### Create a cultivation track

```
DEFINITION
POST http://apiserver/cultivationtracks

EXAMPLE REQUEST
$.post("http://localhost:49195/cultivationtracks", {
    "code": "DONDEV",
    "description": "Donor Development Cultivation Track",
    "jobNumber": "539",
    "runDate": "2013-05-10",
    "startTime": "11:30:00 AM",
    "isFriday": true,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "4",
    "code": "DONDEV",
    "description": "Donor Development Cultivation Track",
    "jobNumber": "539",
    "jobDescription": "Club52 Product Subscriptions",
    "runDate": "2013-05-10",
    "startTime": "11:30:00 AM",
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": true,
    "isSaturday": false,
    "isActive": true
}

```

Creates a new cultivation track.

##### Arguments

* code (required) - The code of the cultivation track.
* description (required) - The description of the cultivation track.
* jobNumber (required) - The segmentation job number of the cultivation track.
* startTime (required) - The start time of products in the cultivation track.
* runDate (optional) - The run date in the cultivation track.
* isSunday (optional) - Whether the cultivation track runs on Sunday. (At least one day of the week must be set to `true`.)
* isMonday (optional) - Whether the cultivation track runs on Monday. (At least one day of the week must be set to `true`.)
* isTuesday (optional) - Whether the cultivation track runs on Tuesday. (At least one day of the week must be set to `true`.)
* isWednesday (optional) - Whether the cultivation track runs on Wednesday. (At least one day of the week must be set to `true`.)
* isThursday (optional) - Whether the cultivation track runs on Thursday. (At least one day of the week must be set to `true`.)
* isFriday (optional) - Whether the cultivation track runs on Friday. (At least one day of the week must be set to `true`.)
* isSaturday (optional) - Whether the cultivation track runs on Saturday. (At least one day of the week must be set to `true`.)
* isActive (optional) - Whether the cultivation track is activ eor not. If not provided, will be set to `true`.

##### Returns

Returns a cultivation track object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cultivation track

```
DEFINITION
GET http://apiserver/cultivationtracks/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cultivationtracks/4");

EXAMPLE RESPONSE
{
    "id": "4",
    "code": "DONDEV",
    "description": "Donor Development Cultivation Track",
    "jobNumber": "539",
    "jobDescription": "Club52 Product Subscriptions",
    "runDate": "2013-05-10",
    "startTime": "11:30:00 AM",
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": true,
    "isSaturday": false,
    "isActive": true
}

```

Retrieves the details of an existing cultivation track. You need only supply the cultivation track id.

##### Arguments

##### Returns

Returns a cultivation track object if a valid id was provided.

#### Update a cultivation track

```
DEFINITION
POST http://apiserver/cultivationtracks/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/cultivationtracks/4", {
    "isActive": "false"
}
});

EXAMPLE RESPONSE
{
    "id": "4",
    "code": "DONDEV",
    "description": "Donor Development Cultivation Track",
    "jobNumber": "539",
    "jobDescription": "Club52 Product Subscriptions",
    "runDate": "2013-05-10",
    "startTime": "11:30:00 AM",
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": true,
    "isSaturday": false,
    "isActive": false
}


```

Updates the specified cultivation track by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* code (optional) - The code of the cultivation track.
* description (optional) - The description of the cultivation track.
* jobNumber (optional) - The segmentation job number of the cultivation track.
* startTime (optional) - The start time of products in the cultivation track.
* runDate (optional) - The run date in the cultivation track.
* isSunday (optional) - Whether the cultivation track runs on Sunday. (At least one day of the week must be set to `true`.)
* isMonday (optional) - Whether the cultivation track runs on Monday. (At least one day of the week must be set to `true`.)
* isTuesday (optional) - Whether the cultivation track runs on Tuesday. (At least one day of the week must be set to `true`.)
* isWednesday (optional) - Whether the cultivation track runs on Wednesday. (At least one day of the week must be set to `true`.)
* isThursday (optional) - Whether the cultivation track runs on Thursday. (At least one day of the week must be set to `true`.)
* isFriday (optional) - Whether the cultivation track runs on Friday. (At least one day of the week must be set to `true`.)
* isSaturday (optional) - Whether the cultivation track runs on Saturday. (At least one day of the week must be set to `true`.)
* isActive (optional) - Whether the cultivation track is activ eor not. If not provided, will be set to `true`.

##### Returns

Returns the cultivation track object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cultivation track

```
DEFINITION
DELETE http://apiserver/cultivationtracks/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/cultivationtracks/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cultivation track. It cannot be undone.

##### Arguments

* id (required) - The id of the cultivation track to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cultivation track does not exist, this call returns an error.

#### List all cultivation tracks

```
DEFINITION
GET http://apiserver/cultivationtracks

EXAMPLE REQUEST
$.get("http://localhost:49195/cultivationtracks?code=*DON*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "code": "DONDEV",
            "description": "Donor Development Cultivation Track",
            "jobNumber": "539",
            "jobDescription": "Club52 Product Subscriptions",
            "runDate": "2013-05-10",
            "startTime": "11:30:00 AM",
            "isSunday": false,
            "isMonday": false,
            "isTuesday": false,
            "isWednesday": false,
            "isThursday": false,
            "isFriday": true,
            "isSaturday": false,
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all cultivation tracks.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* code (optional) - Filter list by the partial match of cultivation track code
* description (optional) - Filter list by partial match of description.
* isActive (optional) - Filter list by whether the cultivation track is active or not.
* id (optional) - Filter list by id.

##### Returns

A dictionary with an items property that contains an array of up to limit cultivation tracks, starting at index offset. Each entry in the array is a separate cultivation track object. If no more cultivation track are available, the resulting array will be empty. This request should never return an error.

### Cultivation Track Details

#### Create a cultivation track detail

```
DEFINITION
POST http://apiserver/cultivationtracks/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/cultivationtracks/4/details", {
    "segmentCode": "Major",
    "description": "Major Donors",
    "processingPriority": 10,
    "segmentNumber": 42,
    "letter": "DCTMAJOR",
    "Source": "0700",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "35",
    "segmentCode": "Major",
    "description": "Major Donors",
    "processingPriority": 10,
    "segmentNumber": 42,
    "segmentDescription": "Club 52 Product",
    "letter": "DCTMAJOR",
    "letterDescription": "Donor Cultivation Track - Major Donor",
    "Source": "0700",
    "sourceDescription": "Direct Mail Appeal 2010 April",
    "product": null,
    "productDescription": null,
    "warehouse": null,
    "warehouseDescription": null,
    "isActive": true
}

```

Creates a new cultivation track detail.

##### Arguments

* segmentCode (required) - The cultivation track segment code of the cultivation track detail.
* description (required) - The description of the cultivation track detail.
* processingPriority (required) - The processing priority of the cultivation track detail.
* segmentNumber (required) - The segment number of the cultivation track detail.
* isActive (required) - Whether the cultivation track detail is required or not.
* letter (optional) - The letter code of the cultivation track detail.
* source (optional) - The source code of the cultivation track detail. (Required if `letter` or `product` is specified.)
* product (optional) - The product code of the cultivation track detail. (Must exist in the specified `warehouse`.)
* warehouse (optional) - The warehouse code of the cultivation track detail. (Required if `product` is specified.)

##### Returns

Returns a cultivation track detail object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cultivation track detail

```
DEFINITION
GET http://apiserver/cultivationtracks/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cultivationtracks/4/details/35");

EXAMPLE RESPONSE
{
    "id": "35",
    "segmentCode": "Major",
    "description": "Major Donors",
    "processingPriority": 10,
    "segmentNumber": 42,
    "segmentDescription": "Club 52 Product",
    "letter": "DCTMAJOR",
    "letterDescription": "Donor Cultivation Track - Major Donor",
    "Source": "0700",
    "sourceDescription": "Direct Mail Appeal 2010 April",
    "product": null,
    "productDescription": null,
    "warehouse": null,
    "warehouseDescription": null,
    "isActive": true
}

```

Retrieves the details of an existing cultivation track detail. You need only supply the cultivation track detail id.

##### Arguments

##### Returns

Returns a cultivation track detail object if a valid id was provided.

#### Update a cultivation track detail

```
DEFINITION
POST http://apiserver/cultivationtracks/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/cultivationtracks/4/details/35", {
    "isActive": "false"
}
});

EXAMPLE RESPONSE
{
    "id": "35",
    "segmentCode": "Major",
    "description": "Major Donors",
    "processingPriority": 10,
    "segmentNumber": 42,
    "segmentDescription": "Club 52 Product",
    "letter": "DCTMAJOR",
    "letterDescription": "Donor Cultivation Track - Major Donor",
    "Source": "0700",
    "sourceDescription": "Direct Mail Appeal 2010 April",
    "product": null,
    "productDescription": null,
    "warehouse": null,
    "warehouseDescription": null,
    "isActive": false
}


```

Updates the specified cultivation track detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* segmentCode (optional) - The cultivation track segment code of the cultivation track detail.
* description (reqoptionaluired) - The description of the cultivation track detail.
* processingPriority (optional) - The processing priority of the cultivation track detail.
* segmentNumber (optional) - The segment number of the cultivation track detail.
* isActive (required) - Whether the cultivation track detail is required or not.
* letter (optional) - The letter code of the cultivation track detail.
* source (optional) - The source code of the cultivation track detail. (Required if `letter` or `product` is specified.)
* product (optional) - The product code of the cultivation track detail. (Must exist in the specified `warehouse`.)
* warehouse (optional) - The warehouse code of the cultivation track detail. (Required if `product` is specified.)

##### Returns

Returns the cultivation track detail object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cultivation track detail

```
DEFINITION
DELETE http://apiserver/cultivationtracks/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/cultivationtracks/4/details/35", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cultivation track detail. It cannot be undone.

##### Arguments

* id (required) - The id of the cultivation track detail to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cultivation track detail does not exist, this call returns an error.

#### List all cultivation track details

```
DEFINITION
GET http://apiserver/cultivationtracks/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/cultivationtracks/4/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "35",
            "segmentCode": "Major",
            "description": "Major Donors",
            "processingPriority": 10,
            "segmentNumber": 42,
            "segmentDescription": "Club 52 Product",
            "letter": "DCTMAJOR",
            "letterDescription": "Donor Cultivation Track - Major Donor",
            "Source": "0700",
            "sourceDescription": "Direct Mail Appeal 2010 April",
            "product": null,
            "productDescription": null,
            "warehouse": null,
            "warehouseDescription": null,
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all cultivation track details.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit cultivation track details, starting at index offset. Each entry in the array is a separate cultivation track detail object. If no more cultivation track detail are available, the resulting array will be empty. This request should never return an error.

### Cultivation Track Detail Actuals

#### Retrieve a cultivation track detail actual

```
DEFINITION
GET http://apiserver/cultivationtracks/:id/details/:id/actuals/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cultivationtracks/4/details/35/actuals/169");

EXAMPLE RESPONSE
{
    "id": "169",
    "runDate": "2013-05-10",
    "numberInTrack": 7509,
    "numberRetained": 7406,
    "numberAddedFirstTimeIn": 2,
    "numberAddedMovingUp": 0,
    "numberAddedMovingDown": 101,
    "numberLostMovingUp": 0,
    "numberLostMovingDown": 0,
    "numberLostMovingOut": 0
}

```

Retrieves the details of an existing cultivation track detail actual. You need only supply the cultivation track detail actual id.

##### Arguments

##### Returns

Returns a cultivation track detail actual object if a valid id was provided.

#### List all cultivation track detail actuals

```
DEFINITION
GET http://apiserver/cultivationtracks/:id/details/:id/actuals

EXAMPLE REQUEST
$.get("http://localhost:49195/cultivationtracks/4/details/35/actuals");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "169",
            "runDate": "2013-05-10",
            "numberInTrack": 7509,
            "numberRetained": 7406,
            "numberAddedFirstTimeIn": 2,
            "numberAddedMovingUp": 0,
            "numberAddedMovingDown": 101,
            "numberLostMovingUp": 0,
            "numberLostMovingDown": 0,
            "numberLostMovingOut": 0
        },
        {...},
    ]
}

```

Returns a list of all cultivation track detail actuals.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit cultivation track detail actuals, starting at index offset. Each entry in the array is a separate cultivation track detail actual object. If no more cultivation track detail actual are available, the resulting array will be empty. This request should never return an error.

### Element Groups

#### Create an element group

```
DEFINITION
POST http://apiserver/elementgroups

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups", {
    "id": "SAVCHLD",
    "description": "This is an element group for saving children.",
    "campaignProgram": "G14D",
    "start": "2015-03-23",
    "end": "2015-03-31"
});

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "This is an element group for saving children.",
    "campaignProgram": "G14D",
    "campaignProgramDescription": "Give 14 Dollars",
    "start": "2015-03-23",
    "end": "2015-03-31"
}

```

Creates a new element group.

##### Arguments

* id (required) - The unique code for the new element group.
* campaignProgram (required) - The campaign program of the element group.
* description (optional) - The description of the element group.
* start (optional) - The start date of the element group.
* end (optional) - The end date of the element group.

##### Returns

Returns a element group object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve an element group

```
DEFINITION
GET http://apiserver/elementgroups/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD");

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "This is an element group for saving children.",
    "campaignProgram": "G14D",
    "campaignProgramDescription": "Give 14 Dollars",
    "start": "2015-03-23",
    "end": "2015-03-31"
}

```

Retrieves the details of an existing element group. You need only supply the element group code.

##### Arguments

* id (required) - The element group code of the element group to retrieve.

##### Returns

Returns a element group object if a valid id was provided.

#### Update an element group

```
DEFINITION
POST http://apiserver/elementgroups/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD", {
    "end": "2015-04-31"
});

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "This is an element group for saving children.",
    "campaignProgram": "G14D",
    "campaignProgramDescription": "Give 14 Dollars",
    "start": "2015-03-23",
    "end": "2015-04-31"
}

```

Updates the specified element group by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* campaignProgram (optional) - The campaign program of the element group.
* description (optional) - The description of the element group.
* start (optional) - The start date of the element group.
* end (optional) - The end date of the element group.

##### Returns

Returns the element group object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid campaign program).

#### Delete an element group

```
DEFINITION
DELETE http://apiserver/elementgroups/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/elementgroups/SAVCHLD", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a element group. It cannot be undone.

##### Arguments

* id (required) - The element group code of the element group to be deleted.

##### Returns

Returns a 204 No Content response on success. If the element group does not exist, this call returns an error.

#### List all element groups

```
DEFINITION
GET http://apiserver/elementgroups

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 91
    }
    "items": [
        {
            "id": "D10D",
            "description": "Direct Mail Appeal 2010 April",
            "campaignProgram": "11DRAPPEAL",
            "campaignProgramDescription": "Give 14 Dollars",
            "status": null,
            "start": "2010-04-07",
            "end": "2013-11-28"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all element groups matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in element group code
* description () - Filter list by partial match in element group description
* start () - Filter list by start date on or after the specified value
* end () - Filter list by end date on or before the specified value
* status () - Filter list by status

##### Returns

A dictionary with an items property that contains an array of up to limit element groups, starting at index offset. Each entry in the array is a separate element group object. If no more element groups are available, the resulting array will be empty. This request should never return an error.

### Element Group Attachments

#### Create an element group attachment

```
DEFINITION
POST http://apiserver/elementgroups/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new element group attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns an element group attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve an element group attachment

```
DEFINITION
GET http://apiserver/elementgroups/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing element group attachment. You need only supply the element group id and element group attachment id.

##### Arguments

* id (required) - The id of the account attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns an element group attachment object if a valid id was provided.

#### Update an element group attachment

```
DEFINITION
POST http://apiserver/elementgroups/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/attachments/49", {
    "type": "LOGO",
});

EXAMPLE RESPONSE
{

    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}



```

Updates the specified element group attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the element group attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete an element group attachment

```
DEFINITION
DELETE http://apiserver/elementgroups/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/elementgroups/SAVCHLD/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an element group attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the element group attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the element group attachment id does not exist, this call returns an error.

#### List all element group attachments

```
DEFINITION
GET http://apiserver/elementgroups/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all element group attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit element group attachments, starting at index offset. Each entry in the array is a separate element group attachment object. If no more element group attachments are available, the resulting array will be empty. This request should never return an error.

### Element Group Codes

#### Create an element group code

```
DEFINITION
POST http://apiserver/elementgroups/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/codes", {
    "type": "VENDOR",
    "value": "LAKE"
});

EXAMPLE RESPONSE
{
    "id": "45",
    "type": "VENDOR",
    "typeDescription": "Broker",
    "value": "LAKE",
    "valueDescription": "Lake Group Media",
    "isActive": true
}

```

Creates a new element group code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an element group code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve an element group code

```
DEFINITION
GET http://apiserver/elementgroups/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/codes/45");

EXAMPLE RESPONSE
{
    "id": "45",
    "type": "VENDOR",
    "typeDescription": "Broker",
    "value": "LAKE",
    "valueDescription": "Lake Group Media",
    "isActive": true
}

```

Retrieves the details of an existing element group code. You need only supply the element group id and element group code id.

##### Returns

Returns an element group code object if a valid id was provided.

#### Update an element group code

```
DEFINITION
POST http://apiserver/elementgroups/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/codes/45", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "45",
    "type": "VENDOR",
    "typeDescription": "Broker",
    "value": "LAKE",
    "valueDescription": "Lake Group Media",
    "isActive": false
}

```

Updates the specified element group code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the element group code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete an element group code

```
DEFINITION
DELETE http://apiserver/elementgroups/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/elementgroups/SAVCHLD/codes/45", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an element group code. It cannot be undone.

##### Arguments

* id (required) - The id of the element group code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the element group code id does not exist, this call returns an error.

#### List all element group codes

```
DEFINITION
GET http://apiserver/elementgroups/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "45",
            "type": "VENDOR",
            "typeDescription": "Broker",
            "value": "LAKE",
            "valueDescription": "Lake Group Media",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all element group codes.

##### Returns

A dictionary with an items property that contains an array of up to limit element group codes, starting at index offset. Each entry in the array is a separate element group code object. If no more element group codes are available, the resulting array will be empty. This request should never return an error.

### Element Group Dates

#### Create an element group date

```
DEFINITION
POST http://apiserver/elementgroups/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/dates", {
    "type": "ELEMDATS",
    "value": "2013-03-24"
});

EXAMPLE RESPONSE
{
    "id": "17",
    "type": "ELEMDATS",
    "typeDescription": null,
    "value": "2013-03-24",
    "isActive": true
}

```

Creates a new element group date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an element group date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve an element group date

```
DEFINITION
GET http://apiserver/elementgroups/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/dates/17");

EXAMPLE RESPONSE
{
    "id": "17",
    "type": "ELEMDATS",
    "typeDescription": null,
    "value": "2013-03-24",
    "isActive": true
}

```

Retrieves the details of an existing element group date. You need only supply the element group id and element group date id.

##### Returns

Returns an element group date object if a valid id was provided.

#### Update an element group date

```
DEFINITION
POST http://apiserver/elementgroups/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/dates/17", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "17",
    "type": "ELEMDATS",
    "typeDescription": null,
    "value": "2013-03-24",
    "isActive": false
}

```

Updates the specified element group date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the element group date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete an element group date

```
DEFINITION
DELETE http://apiserver/elementgroups/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/elementgroups/SAVCHLD/dates/17", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an element group date. It cannot be undone.

##### Arguments

* id (required) - The id of the element group date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the element group date id does not exist, this call returns an error.

#### List all element group dates

```
DEFINITION
GET http://apiserver/elementgroups/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "17",
            "type": "ELEMDATS",
            "typeDescription": null,
            "value": "2013-03-24",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all element group dates.

##### Returns

A dictionary with an items property that contains an array of up to limit element group dates, starting at index offset. Each entry in the array is a separate element group date object. If no more element group dates are available, the resulting array will be empty. This request should never return an error.

### Element Group Notes

#### Create an element group note

```
DEFINITION
POST http://apiserver/elementgroups/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/notes", {
    "type": "NOTETYPE_E",
    "shortComment": "demo"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "NOTETYPE_E",
    "typeDescription": "Element Note Type",
    "shortComment": "demo",
    "longComment": null
}

```

Creates a new element group note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns an element group note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Retrieve an element group note

```
DEFINITION
GET http://apiserver/elementgroups/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/notes/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "NOTETYPE_E",
    "typeDescription": "Element Note Type",
    "shortComment": "demo",
    "longComment": null
}

```

Retrieves the details of an existing element group note. You need only supply the element group id and element group note id.

##### Returns

Returns an element group note object if a valid id was provided.

#### Update an element group note

```
DEFINITION
POST http://apiserver/elementgroups/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/notes/9", {
    "longComment": "now we have a long comment"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "NOTETYPE_E",
    "typeDescription": "Element Note Type",
    "shortComment": "demo",
    "longComment": "now we have a long comment"
}

```

Updates the specified element group note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the element group note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete an element group note

```
DEFINITION
DELETE http://apiserver/elementgroups/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/elementgroups/SAVCHLD/notes/9", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an element group note. It cannot be undone.

##### Arguments

* id (required) - The id of the element group note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the element group note id does not exist, this call returns an error.

#### List all element group notes

```
DEFINITION
GET http://apiserver/elementgroups/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "9",
            "type": "NOTETYPE_E",
            "typeDescription": "Element Note Type",
            "shortComment": "demo",
            "longComment": "now we have a long comment"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all element group notes.

##### Returns

A dictionary with an items property that contains an array of up to limit element group notes, starting at index offset. Each entry in the array is a separate element group note object. If no more element group notes are available, the resulting array will be empty. This request should never return an error.

### Element Group Numbers

#### Create an element group number

```
DEFINITION
POST http://apiserver/elementgroups/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/numbers", {
    "type": "ELEMNUMS",
    "value": 10
});

EXAMPLE RESPONSE
{
    "id": "12",
    "type": "ELEMNUMS",
    "typeDescription": "Element Group Numbers Single",
    "value": 10,
    "isActive": true
}

```

Creates a new element group number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be a defined value of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an element group number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Retrieve an element group number

```
DEFINITION
GET http://apiserver/elementgroups/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/numbers/12");

EXAMPLE RESPONSE
{
    "id": "12",
    "type": "ELEMNUMS",
    "typeDescription": "Element Group Numbers Single",
    "value": 10,
    "isActive": true
}

```

Retrieves the details of an existing element group number. You need only supply the element group id and element group number id.

##### Returns

Returns an element group number object if a valid id was provided.

#### Update an element group number

```
DEFINITION
POST http://apiserver/elementgroups/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/SAVCHLD/numbers/12", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "12",
    "type": "ELEMNUMS",
    "typeDescription": "Element Group Numbers Single",
    "value": 10,
    "isActive": false
}

```

Updates the specified element group number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be a defined value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the element group number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete an element group number

```
DEFINITION
DELETE http://apiserver/elementgroups/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/elementgroups/SAVCHLD/numbers/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an element group number. It cannot be undone.

##### Arguments

* id (required) - The id of the element group number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the element group number id does not exist, this call returns an error.

#### List all element group numbers

```
DEFINITION
GET http://apiserver/elementgroups/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/SAVCHLD/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "12",
            "type": "ELEMNUMS",
            "typeDescription": "Element Group Numbers Single",
            "value": 10,
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all element group numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit element group numbers, starting at index offset. Each entry in the array is a separate element group number object. If no more element group numbers are available, the resulting array will be empty. This request should never return an error.

### Element Group Offerings

#### Create an element group offering

```
DEFINITION
POST http://apiserver/elementgroups/:id/offerings

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/D10D/offerings", {
    "product": "1025",
    "price": "B",
    "amount": 10,
    "isPrimaryOffering": true
});

EXAMPLE RESPONSE
{
    "id": "10521",
    "codeType": "ELEMENT",
    "product": "1025",
    "productDescription": "Book Series",
    "price": "B",
    "priceDescription": "Benevolent (Free)",
    "amount": 10,
    "isPrimaryOffering": true
}

```

Creates a new element group offering.

##### Arguments

* product (required) - The product code. Must be a defined product.
* price (required) - The price code. Must be a defined price code.
* amount (required) - The amount.
* isPrimaryOffering (optional) - Whether or not the offering is a primary offering.

#### Retrieve an element group offering

```
DEFINITION
GET http://apiserver/elementgroups/:id/offerings/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/D10D/offerings/10521");

EXAMPLE RESPONSE
{
    "id": "10521",
    "codeType": "ELEMENT",
    "product": "1025",
    "productDescription": "Book Series",
    "price": "B",
    "priceDescription": "Benevolent (Free)",
    "amount": 10,
    "isPrimaryOffering": true
}

```

Retrieves the details of an existing element group offering. You need only supply the id of the element group offering.

##### Arguments

* id (required) - The id of the element group offering to retrieve

##### Returns

Returns an element group offering if a valid id was provided.

#### Update an element group offering

```
DEFINITION
POST http://apiserver/elementgroups/:id/offerings/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/elementgroups/D10D/offerings/10521", {
    "price": "EP"
});

EXAMPLE RESPONSE
{
    "id": "10521",
    "codeType": "ELEMENT",
    "product": "1025",
    "productDescription": "Book Series",
    "price": "EP",
    "priceDescription": "Employee Price",
    "amount": 10,
    "isPrimaryOffering": true
}

```

Updates the specified element group offering by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* product (optional) - The product code. Must be a defined product.
* price (optional) - The price code. Must be a defined price code.
* amount (optional) - The amount.
* isPrimaryOffering (optional) - Whether or not the offering is a primary offering.

##### Returns

Returns the element group offering object if the update succeeded. Returns an error if parameters are invalid.

#### Delete an element group offering

```
DEFINITION
DELETE http://apiserver/elementgroups/:id/offerings/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/elementgroups/D10D/offerings/10521", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an element group offering. It cannot be undone.

##### Arguments

* id (required) - The id of the element group offering to be deleted.

##### Returns

Returns a 204 No Content response on success. If the element group offering id does not exist, this call returns an error.

#### List all element group offerings

```
DEFINITION
GET http://apiserver/elementgroups/:id/offerings

EXAMPLE REQUEST
$.get("http://localhost:49195/elementgroups/D10D/offerings");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "10521",
            "codeType": "ELEMENT",
            "product": "1025",
            "productDescription": "Book Series",
            "price": "B",
            "priceDescription": "Benevolent (Free)",
            "amount": 10,
            "isPrimaryOffering": true
        },
        { ... }
    ]
}

```

Returns a list of offerings for an element group.

##### Returns

A dictionary with an items property that contains an array of up to limit element group offerings, starting at index offset. Each entry in the array is a separate element group offering object. If no more element group offerings are available, the resulting array will be empty. This request should never return an error.

### Evaluation Types

#### Create an evaluation type

```
DEFINITION
POST http://apiserver/eventevaluationtypes

EXAMPLE REQUEST
$.post("http://localhost:49195/eventevaluationtypes", {
    "id": "LNGSURV",
    "description": "Long survey"
});

EXAMPLE RESPONSE
{
    "id": "LNGSURV",
    "description": "Long survey",
    "isActive": true
}

```

Creates a new evaluation type.

##### Arguments

* id (required) - The evaluation type code for the evaluation type.
* description (required) - The description of the evaluation type.
* isActive (optional : default true) - Indicates whether the evaluation type is active.

##### Returns

Returns an evaluation type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an evaluation type

```
DEFINITION
GET http://apiserver/eventevaluationtypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventevaluationtypes/LNGSURV");

EXAMPLE RESPONSE
{
    "id": "LNGSURV",
    "description": "Long survey",
    "isActive": true
}

```

Retrieves the details of an existing evaluation type. You need only supply the id.

##### Arguments

* id (required) - The id of the evaluation type to be retrieved.

#### Update an evaluation type

```
DEFINITION
POST http://apiserver/eventevaluationtypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventevaluationtypes/LNGSURV", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "LNGSURV",
    "description": "Long survey",
    "isActive": false
}


```

Updates the specified evaluation type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the evaluation type.
* isActive (optional) - Indicates whether the evaluation type is active.

##### Returns

Returns the evaluation type object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an evaluation type

```
DEFINITION
DELETE http://apiserver/eventevaluationtypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventevaluationtypes/LNGSURV", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an evaluation type. It cannot be undone.

##### Arguments

* id (required) - The id of the evaluation type to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the evaluation type does not exist, this call returns an error.

#### List all evaluation types

```
DEFINITION
GET http://apiserver/eventevaluationtypes

EXAMPLE REQUEST
$.get("http://localhost:49195/eventevaluationtypes?isActive=false");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "LNGSURV",
            "description": "Long survey",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all evaluation types.

##### Arguments

* type (optional) - Filter list by partial match on evaluation type code.
* description (optional) - Filter list by partial match on description.
* isActive (optional) - Filter list by whether active or not.

##### Returns

A dictionary with an items property that contains an array of up to limit evaluation types, starting at index offset. Each entry in the array is a separate evaluation type object. If no more evaluation types are available, the resulting array will be empty. This request should never return an error.

### Evaluation Type Questions

#### Create an evaluation type question

```
DEFINITION
POST http://apiserver/eventevaluationtypes/:id/questions

EXAMPLE REQUEST
$.post("http://localhost:49195/eventevaluationtypes/SURV1/questions", {
    "sequence": 2,
    "code": "EVALFUN",
    "question": "Was it fun?"
});

EXAMPLE RESPONSE
{
    "id": "11",
    "question": "Was it fun?",
    "code": "EVALFUN",
    "codeDescription": "Event fun level",
    "sequence": 2,
    "isRequired": true
}

```

Creates a new evaluation type question.

##### Arguments

* sequence (required) - The sequence number of the question.
* code (required) - The code type to use for the question, must be a valid `XO2` with datatype `X04` and category `EVENTEVAL`.
* isRequired (optional : default true) - Indicates whether the question is required for evaluations.
* question (optional) - The textual question to display on the evaluation form.

##### Returns

Returns an evaluation type question object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an evaluation type question

```
DEFINITION
GET http://apiserver/eventevaluationtypes/:id/questions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventevaluationtypes/SURV1/questions/11");

EXAMPLE RESPONSE
{
    "id": "11",
    "question": "Was it fun?",
    "code": "EVALFUN",
    "codeDescription": "Event fun level",
    "sequence": 2,
    "isRequired": true
}

```

Retrieves the details of an existing evaluation type question. You need only supply the id.

##### Arguments

* id (required) - The id of the evaluation type question to be retrieved.

#### Update an evaluation type question

```
DEFINITION
POST http://apiserver/eventevaluationtypes/:id/questions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventevaluationtypes/SURV1/questions/11", {
    "isRequired": false
});

EXAMPLE RESPONSE
{
    "id": "11",
    "question": "Was it fun?",
    "code": "EVALFUN",
    "codeDescription": "Event fun level",
    "sequence": 2,
    "isRequired": false
}


```

Updates the specified evaluation type question by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sequence (optional) - The sequence number of the question.
* code (optional) - The code type to use for the question, must be a valid `XO2` with datatype `X04` and category `EVENTEVAL`.
* isRequired (optional) - Indicates whether the question is required for evaluations.
* question (optional) - The textual question to display on the evaluation form.

##### Returns

Returns the evaluation type question object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an evaluation type question

```
DEFINITION
DELETE http://apiserver/eventevaluationtypes/:id/questions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventevaluationtypes/SURV1/questions/11", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an evaluation type question. It cannot be undone.

##### Arguments

* id (required) - The id of the evaluation type question to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the evaluation type question does not exist, this call returns an error.

#### List all evaluation type questions

```
DEFINITION
GET http://apiserver/eventevaluationtypes/:id/questions

EXAMPLE REQUEST
$.get("http://localhost:49195/eventevaluationtypes/SURV1/questions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "11",
            "question": "Was it fun?",
            "code": "EVALFUN",
            "codeDescription": "Event fun level",
            "sequence": 2,
            "isRequired": false
        },
        {...},
    ]
}

```

Returns a list of all evaluation type questions.

##### Returns

A dictionary with an items property that contains an array of up to limit evaluation type questions, starting at index offset. Each entry in the array is a separate evaluation type question object. If no more evaluation type questions are available, the resulting array will be empty. This request should never return an error.

### Event Attachments

#### Create an event attachment

```
DEFINITION
POST http://apiserver/events/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "8",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new event attachment.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns an event attachment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event attachment

```
DEFINITION
GET http://apiserver/events/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/attachments/8");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "8",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing event attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the media network attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

#### Update an event attachment

```
DEFINITION
POST http://apiserver/events/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/attachments/8", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "8",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified event attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the event attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event attachment

```
DEFINITION
DELETE http://apiserver/events/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/attachments/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the event attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event attachment does not exist, this call returns an error.

#### List all event attachments

```
DEFINITION
GET http://apiserver/events/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "8",
            "type": "OTHER",
            "typeDescription": "Other",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
    ]
}

```

Returns a list of all event attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit event attachments, starting at index offset. Each entry in the array is a separate event attachment object. If no more event attachments are available, the resulting array will be empty. This request should never return an error.

### Event Categories

#### Create an event category

```
DEFINITION
POST http://apiserver/events/:eventId/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/storeconfigurations/1/categories", {
    "categoryId": 20
});

EXAMPLE RESPONSE
{
    "id": "12",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Creates a new event category for the given StudioOnline store configuration.

##### Arguments

* categoryId (required) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns an event category object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event category

```
DEFINITION
GET http://apiserver/events/:eventId/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/storeconfigurations/1/categories/12");

EXAMPLE RESPONSE
{
    "id": "12",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Retrieves the details of an existing event category for the given StudioOnline store configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the event category to be retrieved.

#### Update an event category

```
DEFINITION
POST http://apiserver/events/:eventId/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/storeconfigurations/1/categories/12", {
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "12",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": true,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}


```

Updates the specified event category for the given StudioOnline store configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* categoryId (optional) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns the event category object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event category

```
DEFINITION
DELETE http://apiserver/events/:eventId/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/storeconfigurations/1/categories/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event category from a given StudioOnline store configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the event category to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event category does not exist, this call returns an error.

#### List all event categories

```
DEFINITION
GET http://apiserver/events/:eventId/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/storeconfigurations/1/categories");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "12",
            "categoryId": "20",
            "categoryName": "Best Sellers",
            "isPrimary": true,
            "isActive": true,
            "breadcrumb": "best-sellers",
            "parentCategoryId": null,
            "parentCategoryName": null
        },
        {...},
    ]
}

```

Returns a list of all event categories for the StudioOnline store.

##### Returns

A dictionary with an items property that contains an array of up to limit event categories, starting at index offset. Each entry in the array is a separate event category object. If no more event categories are available, the resulting array will be empty. This request should never return an error.

### Event Codes

#### Create an event code

```
DEFINITION
POST http://apiserver/events/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/codes", {
    "type": "ROOMINFO",
    "value": "HNDCP"
});

EXAMPLE RESPONSE
{
    "id": "106",
    "type": "ROOMINFO",
    "typeDescription": null,
    "value": "HNDCP",
    "valueDescription": "Handicap Access",
    "isActive": true
}

```

Creates a new event code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an event code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event code

```
DEFINITION
GET http://apiserver/events/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/codes/106");

EXAMPLE RESPONSE
{
    "id": "106",
    "type": "ROOMINFO",
    "typeDescription": "Room info",
    "value": "HNDCP",
    "valueDescription": "Handicap Access",
    "isActive": true
}

```

Retrieves the details of an existing event code. You need only supply the id.

##### Arguments

* id (required) - The id of the event code to be retrieved.

#### Update an event code

```
DEFINITION
POST http://apiserver/events/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/codes/106", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "106",
    "type": "ROOMINFO",
    "typeDescription": "Room info",
    "value": "HNDCP",
    "valueDescription": "Handicap Access",
    "isActive": false
}


```

Updates the specified event code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the event code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event code

```
DEFINITION
DELETE http://apiserver/events/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/codes/106", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event code. It cannot be undone.

##### Arguments

* id (required) - The id of the event code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event code does not exist, this call returns an error.

#### List all event codes

```
DEFINITION
GET http://apiserver/events/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "106",
            "type": "ROOMINFO",
            "typeDescription": "Room info",
            "value": "HNDCP",
            "valueDescription": "Handicap Access",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all event codes.

##### Returns

A dictionary with an items property that contains an array of up to limit event codes, starting at index offset. Each entry in the array is a separate event code object. If no more event codes are available, the resulting array will be empty. This request should never return an error.

### Event Dates

#### Create an event date

```
DEFINITION
POST http://apiserver/events/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/dates", {
    "type": "ETRIPFPD",
    "value": "2011-10-14"
});

EXAMPLE RESPONSE
{
    "id": "173",
    "type": "ETRIPFPD",
    "typeDescription": null,
    "value": "2011-10-14",
    "isActive": true
}

```

Creates a new event date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an event date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event date

```
DEFINITION
GET http://apiserver/events/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/dates/173");

EXAMPLE RESPONSE
{
    "id": "173",
    "type": "ETRIPFPD",
    "typeDescription": "Full Paid Date",
    "value": "2011-10-14",
    "isActive": true
}

```

Retrieves the details of an existing event date. You need only supply the id.

##### Arguments

* id (required) - The id of the event date to be retrieved.

#### Update an event date

```
DEFINITION
POST http://apiserver/events/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/dates/173", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "173",
    "type": "ETRIPFPD",
    "typeDescription": "Full Paid Date",
    "value": "2011-10-14",
    "isActive": false
}


```

Updates the specified event date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the event date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event date

```
DEFINITION
DELETE http://apiserver/events/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/dates/173", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event date. It cannot be undone.

##### Arguments

* id (required) - The id of the event date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event date does not exist, this call returns an error.

#### List all event dates

```
DEFINITION
GET http://apiserver/events/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "173",
            "type": "ETRIPFPD",
            "typeDescription": "Full Paid Date",
            "value": "2011-10-14",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all event dates.

##### Returns

A dictionary with an items property that contains an array of up to limit event dates, starting at index offset. Each entry in the array is a separate event date object. If no more event dates are available, the resulting array will be empty. This request should never return an error.

### Event Images

#### Create an event image

```
DEFINITION
POST http://apiserver/events/:eventId/images

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/images", {
    "imageType": "IMAGEXS",
    "description": "Extra Small Event Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image",
    "title": "Image Title",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Event Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Creates a new event image.

##### Arguments

* imageType (required) - the ImageType code value for the event image.
* description (optional) - the description for the event image.
* imageUrl (required) - the image URL for the event image.
* alternateText (optional) - the alternate text for the event image.
* title (optional) - the image title for the event image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns a event image object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event image

```
DEFINITION
GET http://apiserver/events/:eventId/images/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/images/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Event Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Retrieves the details of an existing event image. You need only supply the id.

##### Arguments

* id (required) - The id of the event image to be retrieved.

#### Update an event image

```
DEFINITION
POST http://apiserver/events/:eventId/images/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/images/6", {
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Event Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}


```

Updates the specified event image by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* imageType (optional) - the ImageType code value to update for the event image.
* description (optional) - the description to update for the event image.
* imageUrl (optional) - the image URL to update for the event image.
* alternateText (optional) - the alternate text to update for the event image.
* title (optional) - the image title to update for the event image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns the event image object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event image

```
DEFINITION
DELETE http://apiserver/events/:eventId/images/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/images/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a event image. It cannot be undone.

##### Arguments

* id (required) - The id of the event image to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event image does not exist, this call returns an error.

#### List all event images

```
DEFINITION
GET http://apiserver/events/:eventId/images

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/images");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 9
    },
    "items": [
        {
            "id": "6",
            "imageType": "IMAGEXS",
            "imageTypeDescription": "Extra Small Image",
            "description": "Extra Small Event Img",
            "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
            "alternateText": "Image Alt Text",
            "title": "Image Title",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all event images by event code.

##### Returns

A dictionary with an items property that contains an array of up to limit event images, starting at index offset. Each entry in the array is a separate event image object. If no more event images are available, the resulting array will be empty. This request should never return an error.

### Event Invitations

#### Create an event invitation

```
DEFINITION
POST http://apiserver/events/:eventId/invitations

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/invitations", {
    "account": "12345",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "account": "12345",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
}

```

Creates a new event invitation.

##### Arguments

* eventId (required) - the event code for the invitation.
* account (required) - the account number on the invitation .
* firstName (required) - first name on the invitation.
* lastName (required) - last name on the invitation.
* email (required) - email address on the invitation.
* registrationType (optional) - event registration type.
* status (required) - status on the event invitation.

##### Returns

Returns a event invitation object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event invitation

```
DEFINITION
GET http://apiserver/events/:eventId/invitations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/invitations/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "account": "12345",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "registrationTypeDescription": "REGTYPE Description",
    "status": "A"
}

```

Retrieves the details of an existing event invitation. You need only supply the id.

##### Arguments

* id (required) - The id of the event invitation to be retrieved.

#### Update an event invitation

```
DEFINITION
POST http://apiserver/events/:eventId/invitations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/invitations/6", {
    "account": "12345",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "account": "12345",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
}


```

Updates the specified event invitation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - the unique identifier for the event invitation.
* eventId (required) - the event code for the invitation.
* account (required) - the account number on the invitation .
* firstName (required) - first name on the invitation.
* lastName (required) - last name on the invitation.
* email (required) - email address on the invitation.
* registrationType (required) - event registration type.
* status (required) - status on the event invitation.

##### Returns

Returns the event invitation object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event invitation

```
DEFINITION
DELETE http://apiserver/events/:eventId/invitations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/invitations/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a event invitation. It cannot be undone.

##### Arguments

* id (required) - The id of the event invitation to be deleted.
* eventId (required) - The event code for the invitation.

##### Returns

Returns a `204 No Content` response on success. If the event invitation does not exist, this call returns an error.

#### List all event invitations

```
DEFINITION
GET http://apiserver/events/:eventId/invitations

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/invitations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 9
    },
    "items": [
        {
            "id": "6",
            "account": "12345",
            "firstName": "John",
            "lastName": "Smith",
            "email": "john.smith@test.com",
            "registrationType": "REGTYPE",
            "registrationTypeDescription": "REGTYPE Description",
            "status": "A"
        },
        {...},
    ]
}

```

Returns a list of all event invitations by event code.

##### Arguments

* eventId (required) - The event code for the invitation.

##### Returns

A dictionary with an items property that contains an array of up to limit event invitations, starting at index offset. Each entry in the array is a separate event invitation object. If no more event invitations are available, the resulting array will be empty. This request should never return an error.

### Event Notes

#### Create an event note

```
DEFINITION
POST http://apiserver/events/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/notes", {
    "type": "SOEVTKEYWD",
    "shortComment": "fun"
});

EXAMPLE RESPONSE
{
    "id": "14",
    "type": "SOEVTKEYWD",
    "typeDescription": null,
    "shortComment": "fun",
    "longComment": null
}

```

Creates a new event note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns an event note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event note

```
DEFINITION
GET http://apiserver/events/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/notes/14");

EXAMPLE RESPONSE
{
    "id": "14",
    "type": "SOEVTKEYWD",
    "typeDescription": "Event Keywords",
    "shortComment": "fun",
    "longComment": null
}

```

Retrieves the details of an existing event note. You need only supply the id.

##### Arguments

* id (required) - The id of the event note to be retrieved.

#### Update an event note

```
DEFINITION
POST http://apiserver/events/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/notes/14", {
    "longComment": "fun, fun, fun!"
});

EXAMPLE RESPONSE
{
    "id": "14",
    "type": "SOEVTKEYWD",
    "typeDescription": "Event Keywords",
    "shortComment": "fun",
    "longComment": "fun, fun, fun!"
}


```

Updates the specified event note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the event note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event note

```
DEFINITION
DELETE http://apiserver/events/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/notes/14", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event note. It cannot be undone.

##### Arguments

* id (required) - The id of the event note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event note does not exist, this call returns an error.

#### List all event notes

```
DEFINITION
GET http://apiserver/events/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "14",
            "type": "SOEVTKEYWD",
            "typeDescription": "Event Keywords",
            "shortComment": "fun",
            "longComment": "fun, fun, fun!"
        },
        {...},
    ]
}

```

Returns a list of all event notes.

##### Returns

A dictionary with an items property that contains an array of up to limit event notes, starting at index offset. Each entry in the array is a separate event note object. If no more event notes are available, the resulting array will be empty. This request should never return an error.

### Event Numbers

#### Create an event number

```
DEFINITION
POST http://apiserver/events/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/numbers", {
    "type": "DDCVOLCAP",
    "value": 7
});

EXAMPLE RESPONSE
{
    "id": "10100",
    "type": "DDCVOLCAP",
    "typeDescription": null,
    "value": 7,
    "isActive": true
}

```

Creates a new event number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an event number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event number

```
DEFINITION
GET http://apiserver/events/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/numbers/10100");

EXAMPLE RESPONSE
{
    "id": "10100",
    "type": "DDCVOLCAP",
    "typeDescription": "Event Volunteers Needed",
    "value": 7,
    "isActive": true
}

```

Retrieves the details of an existing event number. You need only supply the id.

##### Arguments

* id (required) - The id of the event number to be retrieved.

#### Update an event number

```
DEFINITION
POST http://apiserver/events/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/numbers/10100", {
    "value": 10
});

EXAMPLE RESPONSE
{
    "id": "10100",
    "type": "DDCVOLCAP",
    "typeDescription": "Event Volunteers Needed",
    "value": 10,
    "isActive": true
}


```

Updates the specified event number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the event number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event number

```
DEFINITION
DELETE http://apiserver/events/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/numbers/10100", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event number. It cannot be undone.

##### Arguments

* id (required) - The id of the event number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event number does not exist, this call returns an error.

#### List all event numbers

```
DEFINITION
GET http://apiserver/events/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10100",
            "type": "DDCVOLCAP",
            "typeDescription": "Event Volunteers Needed",
            "value": 10,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all event numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit event numbers, starting at index offset. Each entry in the array is a separate event number object. If no more event numbers are available, the resulting array will be empty. This request should never return an error.

### Event Registrants

#### Retrieve an event registrant

```
DEFINITION
GET http://apiserver/events/:id/registrants/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/PC11MAYDEN/registrants/1000007943");

EXAMPLE RESPONSE
{
    "id": "1000007943",
    "attended": false,
    "account": "22595",
    "firstName": "John",
    "lastName": "Smith",
    "accountName": "John Smith",
    "addressLine1": "234 Park Ave",
    "city": "Beverly Hills",
    "state": "CA",
    "zipCode": "90210",
    "quantity": "1",
    "status": "C",
    "priceCode": "I",
    "price": 25,
    "group": null,
    "comment": null,
    "source": "PH8002013",
    "sourceDescription": "800 Phone Line - 2013",
    "documentNumber": "174850"
}

```

Retrieves the details of an existing event registrant. You need only supply the id.

##### Arguments

* id (required) - The id of the event registrant to be retrieved.

#### Update an event registrant

```
DEFINITION
POST http://apiserver/events/:id/registrants/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/PC11MAYDEN/registrants/1000007943", {
    "attended": true
});

EXAMPLE RESPONSE
{
    "id": "1000007943",
    "attended": true,
    "account": "22595",
    "firstName": "John",
    "lastName": "Smith",
    "accountName": "John Smith",
    "addressLine1": "234 Park Ave",
    "city": "Beverly Hills",
    "state": "CA",
    "zipCode": "90210",
    "quantity": "1",
    "status": "C",
    "priceCode": "I",
    "price": 25,
    "group": null,
    "comment": null,
    "source": "PH8002013",
    "sourceDescription": "800 Phone Line - 2013",
    "documentNumber": "174850"
}


```

Updates the specified event registrant by setting the values of the parameters passed. Any parameters not provided will be left unchanged.
This resource is used for checking registrants in or out.

##### Arguments

* attended (optional) - Indicates whether the registrant attended the event.

##### Returns

Returns the event registrant object if the update succeeded. Returns an error if update parameters are invalid.

#### Check in all event registrants

```
DEFINITION
POST http://apiserver/events/:id/checkeverybodyin

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/checkeverybodyin", {});

EXAMPLE RESPONSE
204 No Content

```

Checks in all event registrants for this event.

##### Returns

Returns a `204 No Content` response on success. If the event does not exist this call returns an error.

#### Confirm an event registrant

```
DEFINITION
POST http://apiserver/events/:id/registrants/:id/confirm

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/registrants/1000007943/confirm", {});

EXAMPLE RESPONSE
204 No Content

```

Confirms an event registrant (moves from waiting to confirmed).

##### Returns

Returns a `204 No Content` response on success. If the event does not exist, there is no availability, or the confirmation is not successful, this call returns an error.

#### Retrieve event evaluation for registrant

```
DEFINITION
GET http://apiserver/events/:id/registrants/:id/evaluation

EXAMPLE REQUEST
$.get("http://localhost:49195/events/PC11MAYDEN/registrants/1000007943/evaluation");

EXAMPLE RESPONSE
{
    "id": "10",
    "comment": "The event was great!",
    "details": [
        {
            "id": "13",
            "question": "2",
            "value": "YES"
        },
        {
            "id": "10015",
            "question": "4",
            "value": "NO"
        }
    ]
}

```

Retrieves the details of an existing evaluation. You need only supply the id.

##### Arguments

* id (required) - The id of the event and registrant to retrieve evaluation for.

#### Submit event evaluation for registrant

```
DEFINITION
POST http://apiserver/events/:id/registrants/:id/evaluation

EXAMPLE REQUEST
$.post("http://localhost:49195/events/PC11MAYDEN/registrants/1000007943/evaluation", {
    "comment": "The event was great!",
    "details": [
        {
            "question": "2",
            "value": "YES"
        },
        {
            "question": "4",
            "value": "NO"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "10",
    "comment": "The event was great!",
    "details": [
        {
            "id": "13",
            "question": "2",
            "value": "YES"
        },
        {
            "id": "10015",
            "question": "4",
            "value": "NO"
        }
    ]
}

```

Creates or updates an evaluation.
NOTE: Any fields not provided will be overwritten.

##### Arguments

* comment (optional) - A text field for comments about the event.
* details (optional\*) - The answers to questions on the evaluation. These are derived from the evaluation type for the event and questions can be set to required. Details is an array of objects.
* details[].question (required) - Each detail must have a question field which represents the id of the corresponding evaluation type question.
* details[].value (optional\*) - Each detail can have a value field which represents the answer to the question, must be a valid code value for the evaluation type question. The value can only be empty if the question is not required. No value indicates an unanswered question.

##### Returns

Returns an evaluation object if the call succeeded. Returns an error if create parameters are invalid.

#### Transfer an event registrant

```
DEFINITION
POST http://apiserver/events/:id/registrants/:id/transfer

EXAMPLE REQUEST
$.post("http://localhost:49195/events/PC11MAYDEN/registrants/1000007943/transfer", {
    "event": "10DAL",
    "asOfDate": "2015-09-23"
});

EXAMPLE RESPONSE
204 No Content

```

Transfer the registrant to another Event.

##### Arguments

* event (required) - The Event Code of the event to transfer registrant to. Must be a valid event (DDCEVENTCA).
* asOfDate (required) - Date from which to transfer.

##### Returns

Returns a `204 No Content` response on success. If the parameters are not valid, this call returns an error.

#### List all event registrants

```
DEFINITION
GET http://apiserver/events/:id/registrants

EXAMPLE REQUEST
$.get("http://localhost:49195/events/PC11MAYDEN/registrants?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000007914",
            "attended": true,
            "account": "22782",
            "firstName": "Donny",
            "lastName": "Cramer",
            "accountName": "Mr. Donny Cramer",
            "addressLine1": "9328 Apple Way",
            "city": "Richardson",
            "state": "TX",
            "zipCode": "75080",
            "quantity": "1",
            "status": "C",
            "priceCode": "COUPLE",
            "price": 50,
            "group": null,
            "comment": null,
            "source": "PH8002013",
            "sourceDescription": "800 Phone Line - 2013",
            "documentNumber": "174816"
        },
        {...},
    ]
}

```

Returns a list of all event registrants.

##### Returns

A dictionary with an items property that contains an array of up to limit event registrants, starting at index offset. Each entry in the array is a separate event registrant object. If no more event registrants are available, the resulting array will be empty. This request should never return an error.

### Event StudioOnline Publish Data

#### Retrieve the event StudioOnline publish data

```
DEFINITION
GET http://apiserver/events/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.get("http://localhost:49195/events/BMWEVNT/studioonlinepublishdata");

EXAMPLE RESPONSE
{
    "id": "6468",
    "description": "BMW Event 1",
    "summary": "BMW Event 1",
    "extendedDescription": null,
    "isExtendedDescriptionLocked": false,
    "iconImage": null,
    "mediumImage": null,
    "keywords": " bmw event",
    "pageLayout": "EVENTPACK1"
}

```

Retrieves the details of the existing event StudioOnline publish data. You need only supply the event id.

##### Returns

Returns an event StudioOnline publish data object if a valid id was provided.

#### Update and publish the event StudioOnline publish data

```
DEFINITION
POST http://apiserver/events/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.post("http://localhost:49195/events/BMWEVNT/studioonlinepublishdata", {
    "extendedDescription": "Extended Description",
});

EXAMPLE RESPONSE
{
    "id": "6468",
    "description": "BMW Event 1",
    "summary": "BMW Event 1",
    "extendedDescription": "Extended Description",
    "isExtendedDescriptionLocked": false,
    "iconImage": null,
    "mediumImage": null,
    "keywords": " bmw event",
    "pageLayout": "EVENTPACK1"
}


```

Updates and publishes the specified event StudioOnline publish data by setting the values of the parameters passed. Any parameters not provided will be left unchanged. Any categories must already have been updated through the Event Codes resources. Any prices and sessions must already have been updated through their resources.

##### Arguments

* description (optional) - The description for the event on StudioOnline.
* summary (optional) - The summary for the event on StudioOnline.
* extendedDescription (optional) - The extended description for the event on StudioOnline.
* updateImages (optional) - Whether or not to update the icon and medium images. If this is selected and the icon or medium image are not provided, they will be deleted.
* iconImage (optional) - The icon image for the event on StudioOnline.
* mediumImage (optional) - The medium image for the event on StudioOnline.
* keywords (optional) - The keywords for the event on StudioOnline.
* pageLayout (optional) - The page layout (XML Package) for the event on StudioOnline.

##### Returns

Returns the event StudioOnline publish data object if the update and publish succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined page layout code).

#### Unpublish the event StudioOnline publish data

```
DEFINITION
DELETE http://apiserver/events/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/BMWEVNT/studioonlinepublishdata", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Unpublishes the event StudioOnline publish data. The actual data will not be deleted.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the event StudioOnline publish data cannot be unpublished, this call returns an error.

### Events

#### Create an event

```
DEFINITION
POST http://apiserver/events

EXAMPLE REQUEST
$.post("http://localhost:49195/events", {
    "id": "PRWR15",
    "venue": "1STBAPTATL",
    "primaryRoom": "SANCTUARY"
});

EXAMPLE RESPONSE
{
    "id": "PRWR15",
    "type": null,
    "description": null,
    "venue": "1STBAPTATL",
    "venueDescription": "First Baptist Church Atlanta",
    "numberConfirmed": 0,
    "numberOnWaiting": 0,
    "numberAttended": 0,
    "capacity": 100,
    "primaryRoom": "SANCTUARY",
    "numberAvailable": 0,
    "start": null,
    "end": null,
    "isActive": true,
    "canExceedCapacity": true,
    "canWaitlist": true,
    "journalReference": "0",
    "jeStatus": "Y",
    "evaluationType": null,
    "warehouse": null,
    "location": null,
    "isInvitationOnly": false,
    "useInStudioOnline": false
}

```

Creates a new event.

##### Arguments

* id (required) - The event code for the event, must be unique.
* venue (required) - The venue for the event, must be a valid event venue.
* primaryRoom (required) - The main room for the event, must be a valid room for the selected venue.
* type (required) - The event type, must be a valid DDCEVENTTP code.
* description (optional) - The description of the event.
* start (optional) - The beginning date for the event.
* end (optional) - The end date of the event.
* evaluationType (optional) - The evaluation type for the event, must be a valid evaluation type (DDCEVALTYP).
* warehouse (optional) - The warehouse for the event materials, must be a valid warehouse (DDCWAREHSE).
* location (optional) - The location name for the warehouse.
* canExceedCapacity (optional : default true) - Indicates whether the event can be overbooked.
* canWaitlist (optional : default true) - Indicates whether the event supports waitlist processing.
* isActive (optional : default true) - Indicates whether the event is active.
* isInvitationOnly (optional : default false) - Indicates whether the event is an invitation-only event.
* useInStudioOnline (optional : default false) - Indicates whether the event should be shown in StudioOnline.

##### Returns

Returns an event object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event

```
DEFINITION
GET http://apiserver/events/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/PRWR15?getEventAvailability=true");

EXAMPLE RESPONSE
{
    "id": "PRWR15",
    "type": null,
    "description": null,
    "venue": "1STBAPTATL",
    "venueDescription": "First Baptist Church Atlanta",
    "numberConfirmed": 0,
    "numberOnWaiting": 0,
    "numberAttended": 0,
    "capacity": 100,
    "primaryRoom": "SANCTUARY",
    "numberAvailable": 100,
    "start": null,
    "end": null,
    "isActive": true,
    "canExceedCapacity": true,
    "canWaitlist": true,
    "journalReference": "0",
    "jeStatus": "Y",
    "evaluationType": null,
    "warehouse": null,
    "location": null,
    "isInvitationOnly": false,
    "useInStudioOnline": false
}

```

Retrieves the details of an existing event. You need only supply the event code.

##### Arguments

* id (required) - The event code of the event to retrieve.
* getEventAvailability (optional) - Indicates whether to return the event availability (numberAvailable will not be populated unless this flag is passed).
* numberWaiting (optional) - Number of attendees the asking party already has waiting.

##### Returns

Returns an event object if a valid id was provided.

#### Update an event

```
DEFINITION
POST http://apiserver/events/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/PRWR15", {
    "type": "WTR",
    "description": "Praise and Worship 2015"
});

EXAMPLE RESPONSE
{
    "id": "PRWR15",
    "type": "WTR",
    "description": "Praise and Worship 2015",
    "venue": "1STBAPTATL",
    "venueDescription": "First Baptist Church Atlanta",
    "numberConfirmed": 0,
    "numberOnWaiting": 0,
    "numberAttended": 0,
    "capacity": 100,
    "primaryRoom": "SANCTUARY",
    "numberAvailable": 0,
    "start": null,
    "end": null,
    "isActive": true,
    "canExceedCapacity": true,
    "canWaitlist": true,
    "journalReference": "0",
    "jeStatus": "Y",
    "evaluationType": null,
    "warehouse": null,
    "location": null,
    "isInvitationOnly": false,
    "useInStudioOnline": false
}


```

Updates the specified event by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - The event code for the event, must be unique.
* venue (optional) - The venue for the event, must be a valid event venue.
* primaryRoom (optional) - The main room for the event, must be a valid room for the selected venue.
* type (optional) - The event type, must be a valid DDCEVENTTP code.
* description (optional) - The description of the event.
* start (optional) - The beginning date for the event.
* end (optional) - The end date of the event.
* evaluationType (optional) - The evaluation type for the event, must be a valid evaluation type (DDCEVALTYP).
* warehouse (optional) - The warehouse for the event materials, must be a valid warehouse (DDCWAREHSE).
* location (optional) - The location name for the warehouse.
* canExceedCapacity (optional) - Indicates whether the event can be overbooked.
* canWaitlist (optional) - Indicates whether the event supports waitlist processing.
* isActive (optional) - Indicates whether the event is active.
* isInvitationOnly (optional) - Indicates whether the event is an invitation-only event.
* useInStudioOnline (optional) - Indicates whether the event should be shown in StudioOnline.

##### Returns

Returns the event object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event

```
DEFINITION
DELETE http://apiserver/events/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/PRWR15", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event. It cannot be undone.

##### Arguments

* id (required) - The id of the event to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event does not exist, this call returns an error.

#### Build Journal Entry for an event

```
DEFINITION
POST http://apiserver/events/:id/buildje

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/buildje", {
    "company": "1"
});

EXAMPLE RESPONSE
204 No Content

```

Build the Journal Entry for the specified event.

##### Arguments

* company (required) - The company code for the event journal entry.

##### Returns

Returns a `204 No Content` response on success. If the event does not exist, the company is invalid, or Journal entry has already been built, this call returns an error.

#### Site Transfer for an event

```
DEFINITION
POST http://apiserver/events/:id/sitetransfer

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sitetransfer", {
    "toHome": false,
    "event": "10DAL"
});

EXAMPLE RESPONSE
204 No Content

```

Transfer the site materials to Home Warehouse or another Event.

##### Arguments

* toHome (required : unless event given) - Indicates whether the materials should be transferred home. Control records must have warehouse and location (EMTHOMEWH, EMTHOMELOC respectively).
* event (required : unless toHome is true) - The Event Code of the event to transfer site materials to. Must be a valid, active event with a warehouse and location (DDCEVENTCD).

##### Returns

Returns a `204 No Content` response on success. If the event does not exist, the source or destination is missing a warehouse or location, or the event is not valid, this call returns an error. This resource also validates that event is not given if toHome is true.

#### List all events

```
DEFINITION
GET http://apiserver/events

EXAMPLE REQUEST
$.get("http://localhost:49195/events?type=WTR");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 22
    }
    "items": [
        {
            "id": "PRWR15",
            "type": "WTR",
            "description": "Praise and Worship 2015",
            "venue": "1STBAPTATL",
            "venueDescription": "First Baptist Church Atlanta",
            "numberConfirmed": 0,
            "numberOnWaiting": 0,
            "numberAttended": 0,
            "capacity": 100,
            "primaryRoom": "SANCTUARY",
            "numberAvailable": 0,
            "start": null,
            "end": null,
            "isActive": true,
            "canExceedCapacity": true,
            "canWaitlist": true,
            "journalReference": "0",
            "jeStatus": "Y",
            "evaluationType": null,
            "warehouse": null,
            "location": null,
            "isInvitationOnly": false,
            "useInStudioOnline": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all events matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match in event code
* type (optional) - Filter list by partial match in event type
* description (optional) - Filter list by partial match in event description
* start (optional) - Filter list by start date on or after the specified value
* end (optional) - Filter list by end date on or before the specified value
* isActive (optional) - Filter list by whether active or not
* forEventEntry (optional) - Affects the fields returned, if this list is being used for event entry, it will not have numberConfirmed, numberOnWaiting, numberAttended, or capacity, numberAvailable will be populated, and it will additionally have fields price and mileage. (see resource below for example)

##### Returns

A dictionary with an items property that contains an array of up to limit events, starting at index offset. Each entry in the array is a separate event object. If no more events are available, the resulting array will be empty. This request should never return an error.

#### List all events for event entry

```
DEFINITION
GET http://apiserver/events

EXAMPLE REQUEST
$.get("http://localhost:49195/events?type=WTR&forEventEntry=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 22
    }
    "items": [
        {
            "id": "PRWR15",
            "type": "WTR",
            "description": "Praise and Worship 2015",
            "venue": "1STBAPTATL",
            "venueDescription": "First Baptist Church Atlanta",
            "primaryRoom": "SANCTUARY",
            "numberAvailable": 100,
            "start": null,
            "end": null,
            "isActive": true,
            "canExceedCapacity": true,
            "canWaitlist": true,
            "journalReference": "0",
            "jeStatus": "Y",
            "evaluationType": null,
            "warehouse": null,
            "location": null,
            "useInStudioOnline": false,
            "price": 0,
            "mileage": 0,
            "isInvitationOnly": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all events matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match in event code
* type (optional) - Filter list by partial match in event type
* description (optional) - Filter list by partial match in event description
* start (optional) - Filter list by start date on or after the specified value
* end (optional) - Filter list by end date on or before the specified value
* isActive (optional) - Filter list by whether active or not

##### Returns

A dictionary with an items property that contains an array of up to limit events, starting at index offset. Each entry in the array is a separate event object. If no more events are available, the resulting array will be empty. This request should never return an error.

### Event Coupons

#### Create an event coupon

```
DEFINITION
POST http://apiserver/eventcoupons

EXAMPLE REQUEST
$.post("http://localhost:49195/eventcoupons", {
    "couponCode": "20OFFEVT",
    "description": "Twenty Percent Off Event",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 5,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "usageApplication": "CPNSGLPROD"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "couponCode": "20OFFEVT",
    "description": "Twenty Percent Off Event",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 5,
    "minimumRegistrationAmount": null,
    "minimumRegistrationQuantity": null,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "discountAmount": null,
    "usageApplication": "CPNSGLPROD"
}

```

Creates a new coupon.

##### Arguments

* couponCode (required) - The coupon code to be created.
* description (required) - The coupon code's description.
* status (required) - Is the coupon active or inactive.
* startDate - The start date for coupon usage.
* endDate - The end date for coupon usage.
* usageRestrictionType - The way that the coupon can be used. (CPNSYSLMTD: system limited, CPNCSTLMTD: customer limited, CPNUNLMTD: unlimited).
* usageLimit (required if system or customer limited) - If system or customer limited, the number of times the coupon can be used.
* minimumRegistrationAmount - The minimum amount for an event registration before the coupon can be applied.
* minimumRegistrationQuantity - The minimum quantity of event registrations before the coupon can be applied.
* maximumDiscountAmount - The maximum amount allowed to be deducted using this coupon.
* couponEffect - What effect this coupon has (CPNDISCPCT: discount percentage, CPNDISCAMT: discount amount)
* discountPercentage (required if discount percent effect) - The percentage deducted by this coupon.
* discountAmount (required if discount amount effect) - The amount deducted by this coupon.
* usageApplication (required) - How this coupon should be applied (CPNALLITM: All event registrations in cart, CPNSGLITEM: Single event registration in cart).

##### Returns

Returns an event coupon object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event coupon

```
DEFINITION
GET http://apiserver/eventcoupons/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventcoupons/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "couponCode": "20OFFEVT",
    "description": "Twenty Percent Off Event",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 5,
    "minimumRegistrationAmount": null,
    "minimumRegistrationQuantity": null,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "discountAmount": null,
    "usageApplication": "CPNSGLPROD"
}

```

Retrieves the details of an existing event coupon. You need only supply the id.

##### Arguments

* id (required) - The id of the coupon to be retrieved.

#### Update an event coupon

```
DEFINITION
POST http://apiserver/eventcoupons/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventcoupons/1", {
    "usageLimit": 10
});

EXAMPLE RESPONSE
{
    "id": "1",
    "couponCode": "20OFFEVT",
    "description": "Twenty Percent Off Event",
    "status": "A",
    "startDate": "2017-11-09",
    "endDate": "2017-11-30",
    "usageRestrictionType": "CPNCSTLMTD",
    "usageLimit": 10,
    "minimumRegistrationAmount": null,
    "minimumRegistrationQuantity": null,
    "maximumDiscountAmount": 100,
    "couponEffect": "CPNDISCPCT",
    "discountPercentage": 20,
    "discountAmount": null,
    "usageApplication": "CPNSGLPROD"
}


```

Updates the specified event coupon by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* couponCode - The coupon code to be created.
* description - The coupon code's description.
* status - Is the coupon active or inactive.
* startDate - The start date for coupon usage.
* endDate - The end date for coupon usage.
* usageRestrictionType - The way that the coupon can be used. (CPNSYSLMTD: system limited, CPNCSTLMTD: customer limited, CPNUNLMTD: unlimited).
* usageLimit - If system or customer limited, the number of times the coupon can be used.
* minimumRegistrationAmount - The minimum amount for event registrations before the coupon can be applied.
* minimumRegistrationQuantity - The minimum quantity for event registrations before the coupon can be applied.
* maximumDiscountAmount - The maximum amount allowed to be deducted using this coupon.
* couponEffect - What effect this coupon has (CPNDISCPCT: discount percentage, CPNDISCAMT: discount amount)
* discountPercentage - The percentage deducted by this coupon.
* discountAmount - The amount deducted by this coupon.
* usageApplication (required) - How this coupon should be applied (CPNALLITM: All event registrations in cart, CPNSGLITEM: Single event registration in cart).

##### Returns

Returns the event coupon object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event coupon

```
DEFINITION
DELETE http://apiserver/eventcoupons/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventcoupons/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event coupon. It cannot be undone.

##### Arguments

* id (required) - The id of the coupon to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event coupon does not exist, this call returns an error.

#### List all event coupons

```
DEFINITION
GET http://apiserver/eventcoupons

EXAMPLE REQUEST
$.get("http://localhost:49195/eventcoupons");

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
            "couponCode": "20OFFEVT",
            "description": "Twenty Percent Off Event",
            "status": "A",
            "startDate": "2017-11-09",
            "endDate": "2017-11-30",
            "usageRestrictionType": "CPNCSTLMTD",
            "usageLimit": 10,
            "minimumRegistrationAmount": null,
            "minimumRegistrationQuantity": null,
            "maximumDiscountAmount": 100,
            "couponEffect": "CPNDISCPCT",
            "discountPercentage": 20,
            "discountAmount": null,
            "usageApplication": "CPNSGLPROD"
        },
        {...},
    ]
}

```

Returns a list of all event coupons.

##### Arguments

* couponCode - The coupon code to filter search results by.
* description - The description to filter search results by.
* status - The status to filter search results by.

##### Returns

A dictionary with an items property that contains an array of up to limit event coupons, starting at index offset. Each entry in the array is a separate event coupon object. If no more event coupons are available, the resulting array will be empty. This request should never return an error.

### Event Coupon Event Type Usages

#### Create an event coupon event type usage

```
DEFINITION
POST http://apiserver/eventcoupons/:id/eventtypeusages

EXAMPLE REQUEST
$.post("http://localhost:49195/eventcoupons/1/eventtypeusages", {
    "eventType": "DONCONF",
    "includeExclude": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "eventType": "DONCONF",
    "eventTypeDescription": "Donor Conference",
    "includeExclude": true
}

```

Creates a new event coupon event type usage.

##### Arguments

* eventType (required) - The event type to associate the coupon usage with.
* includeExclude - If true, this coupon usage applies to only this event type. If false, It applies to all event types EXCEPT this one.

##### Returns

Returns an event coupon event type usage object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event coupon event type usage

```
DEFINITION
GET http://apiserver/eventcoupons/:id/eventtypeusages/:usageId

EXAMPLE REQUEST
$.get("http://localhost:49195/eventcoupons/1/eventtypeusages/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "eventType": "DONCONF,
    "eventTypeDescription": "Donor Conference",
    "includeExclude": true
}

```

Retrieves the details of an existing event coupon event type usage. You need only supply the id.

##### Arguments

* id (required) - The id of the event coupon event type usage to be retrieved.

#### Update an event coupon event type usage

```
DEFINITION
POST http://apiserver/eventcoupons/:id/eventtypeusages/:usageId

EXAMPLE REQUEST
$.post("http://localhost:49195/eventcoupons/1/eventtypeusages/3", {
    "includeExclude": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "eventType": "DONCONF",
    "eventTypeDescription": "Donor Conference",
    "includeExclude": false
}

```

Updates the specified event coupon event type usage by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* eventType - The event type to associate the coupon usage with.
* includeExclude - If true, this coupon usage applies to only this event type. If false, It applies to all event types EXCEPT this one.

##### Returns

Returns the event coupon event type usage object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event coupon event type usage

```
DEFINITION
DELETE http://apiserver/eventcoupons/:id/eventtypeusages/:usageId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventcoupons/1/eventtypeusages/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event coupon event type usage. It cannot be undone.

##### Arguments

* id (required) - The id of the event coupon event type usage to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event coupon event type usage does not exist, this call returns an error.

#### List all event coupon event type usages

```
DEFINITION
GET http://apiserver/eventcoupons/:id/eventtypeusages

EXAMPLE REQUEST
$.get("http://localhost:49195/eventcoupons/:id/eventtypeusages");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "eventType": "DONCONF",
            "eventTypeDescription": "Donor Conference",
            "includeExclude": false
        },
        {...},
    ]
}

```

Returns a list of all event coupon event type usages.

##### Arguments

* eventType - The event type to filter search results by.

##### Returns

A dictionary with an items property that contains an array of up to limit event coupon event type usages, starting at index offset. Each entry in the array is a separate event coupon event type object. If no more event coupon event type usages are available, the resulting array will be empty. This request should never return an error.

### Event Coupon Event Code Usages

#### Create an event coupon event code usage

```
DEFINITION
POST http://apiserver/eventcoupons/:id/eventcodeusages

EXAMPLE REQUEST
$.post("http://localhost:49195/eventcoupons/1/eventcodeusages", {
    "eventCode": "CONFDAL",
    "includeExclude": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "eventCode": "CONFDAL",
    "eventCodeDescription": "Donor Conference - Dallas",
    "includeExclude": true
}

```

Creates a new event coupon event code usage.

##### Arguments

* eventCode (required) - The event code to associate the coupon usage with.
* includeExclude - If true, this coupon usage applies to only this event code. If false, It applies to all event codes EXCEPT this one.

##### Returns

Returns an event coupon event code usage object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event coupon event code usage

```
DEFINITION
GET http://apiserver/eventcoupons/:id/eventcodeusages/:usageId

EXAMPLE REQUEST
$.get("http://localhost:49195/eventcoupons/1/eventcodeusages/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "eventCode": "CONFDAL,
    "eventCodeDescription": "Donor Conference - Dallas",
    "includeExclude": true
}

```

Retrieves the details of an existing event coupon event code usage. You need only supply the id.

##### Arguments

* id (required) - The id of the event coupon event code usage to be retrieved.

#### Update an event coupon event code usage

```
DEFINITION
POST http://apiserver/eventcoupons/:id/eventcodeusages/:usageId

EXAMPLE REQUEST
$.post("http://localhost:49195/eventcoupons/1/eventcodeusages/3", {
    "includeExclude": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "eventCode": "CONFDAL",
    "eventCodeDescription": "Donor Conference - Dallas",
    "includeExclude": false
}

```

Updates the specified event coupon event code usage by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* eventCode - The event code to associate the coupon usage with.
* includeExclude - If true, this coupon usage applies to only this event code. If false, It applies to all event codes EXCEPT this one.

##### Returns

Returns the event coupon event code usage object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event coupon event code usage

```
DEFINITION
DELETE http://apiserver/eventcoupons/:id/eventcodeusages/:usageId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventcoupons/1/eventcodeusages/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event coupon event code usage. It cannot be undone.

##### Arguments

* id (required) - The id of the event coupon event code usage to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event coupon event code usage does not exist, this call returns an error.

#### List all event coupon event code usages

```
DEFINITION
GET http://apiserver/eventcoupons/:id/eventcodeusages

EXAMPLE REQUEST
$.get("http://localhost:49195/eventcoupons/:id/eventcodeusages");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "eventCode": "CONFDAL",
            "eventCodeDescription": "Donor Conference - Dallas",
            "includeExclude": false
        },
        {...},
    ]
}

```

Returns a list of all event coupon event code usages.

##### Arguments

* eventCode - The event code to filter search results by.

##### Returns

A dictionary with an items property that contains an array of up to limit event coupon event code usages, starting at index offset. Each entry in the array is a separate event coupon event code usage object. If no more event coupon event code usages are available, the resulting array will be empty. This request should never return an error.

### Event Advanced StudioOnline Configuration

#### Create an event Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/events/:id/storeconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/events/2019DAL/storeconfigurations", {
    "store": "19",
    "useInStudioOnline": true,
    "title": "Dallas Event 2019",
    "urlOverride": "dallas-event-2019",
    "description": "Main Dallas Event for 2019",
    "startDate": "2019-01-01",
    "endDate": "2019-10-05"
});

EXAMPLE RESPONSE
{
    "id": "10004",
    "event": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2019-01-01",
    "endDate": "2019-10-05",
    "hideFromSearch": false,
    "title": "Dallas Event 2019",
    "urlOverride": "dallas-event-2019",
    "url": "https://store.aso.com/register/dallas-event-2019",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Main Dallas Event for 2019",
    "keywords": null,
    "layoutOverride": null
}

```

Creates a new event Advanced StudioOnline configuration.

##### Arguments

* store (required) - The unique id of the store this configuration is for. Must be a valid store Id.
* title (required) - The online title for the event when used in the specified store.
* description (optional) - The online description for the event when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the event title.
* useInStudioOnline (optional) - Whether the event should be used in the specified store.
* startDate (optional) - The date the event will become visible in the specified store.
* endDate (optional) - The date the event will be removed from the specified store.
* hideFromSearch (optional) - Whether the event should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the event when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default event layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate event that should be shown in StudioOnline if someone tries to navigate to this event.

##### Returns

Returns an event Advanced StudioOnline configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event Advanced StudioOnline configuration

```
DEFINITION
GET http://apiserver/events/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/2019DAL/storeconfigurations/10004");

EXAMPLE RESPONSE
{
    "id": "10004",
    "event": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2019-01-01",
    "endDate": "2019-10-05",
    "hideFromSearch": false,
    "title": "Dallas Event 2019",
    "urlOverride": "dallas-event-2019",
    "url": "https://store.aso.com/register/dallas-event-2019",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Main Dallas Event for 2019",
    "keywords": null,
    "layoutOverride": null
}

```

Retrieves the details of a event Advanced StudioOnline configuration. You need only supply the event id and configuration id.

##### Returns

Returns an event Advanced StudioOnline configuration object if valid ids were provided.

#### Update an event Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/events/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/2019DAL/storeconfigurations/10004", {
    "startDate": "2018-12-15",
    "endDate": "2019-10-15"
});

EXAMPLE RESPONSE
{
    "id": "10004",
    "event": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2018-12-15",
    "endDate": "2019-10-15",
    "hideFromSearch": false,
    "title": "Dallas Event 2019",
    "urlOverride": "dallas-event-2019",
    "url": "https://store.aso.com/register/dallas-event-2019",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Main Dallas Event for 2019",
    "keywords": null,
    "layoutOverride": null
}


```

Updates the specified event Advanced StudioOnline configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title (optional) - The online title for the event when used in the specified store.
* description (optional) - The online description for the event when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the event title.
* useInStudioOnline (optional) - Whether the event should be used in the specified store.
* startDate (optional) - The date the event will become visible in the specified store.
* endDate (optional) - The date the event will be removed from the specified store.
* hideFromSearch (optional) - Whether the event should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the event when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default event layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate event that should be shown in StudioOnline if someone tries to navigate to this event.

##### Returns

Returns an event Advanced StudioOnline configuration object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid permanentRedirect).

#### Delete an event Advanced StudioOnline configuration

```
DEFINITION
DELETE http://apiserver/events/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/2019DAL/storeconfigurations/10004", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event Advanced StudioOnline configuration. It cannot be undone.

##### Arguments

* id (required) - The event Advanced StudioOnline configuration id of the configuration to be deleted.

##### Returns

Returns a 204 No Content response on success. If the event Advanced StudioOnline configuration does not exist, this call returns an error.

#### List all event Advanced StudioOnline configurations

```
DEFINITION
GET http://apiserver/events/:id/storeconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/events/2019DAL/storeconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10004",
            "event": "110160",
            "store": "19",
            "storeDescription": "ASO US-English",
            "useInStudioOnline": true,
            "startDate": "2018-12-15",
            "endDate": "2019-10-15",
            "hideFromSearch": false,
            "title": "Dallas Event 2019",
            "urlOverride": "dallas-event-2019",
            "url": "https://store.aso.com/register/dallas-event-2019",
            "permanentRedirect": null,
            "permanentRedirectDescription": null,
            "description": "Main Dallas Event for 2019",
            "keywords": null,
            "layoutOverride": null
        }
        {...},
        {...}
    ]
}

```

Returns a list of all event Advanced StudioOnline configurations matching the provided filter criteria.

##### Arguments

* event () - Filter list by an exact match in event code

##### Returns

A dictionary with an items property that contains an array of up to limit event Advanced StudioOnline configurations, starting at index offset. Each entry in the array is a separate event Advanced StudioOnline configuration object. If no more event Advanced StudioOnline configurations are available, the resulting array will be empty. This request should never return an error.

#### Generate Event Advanced StudioOnline Url

```
DEFINITION
GET http://apiserver/events/:id/stores/:id/generateurl

EXAMPLE REQUEST
$.post("http://localhost:49195/events/2019DAL/stores/19/generateurl", {
    "urlOverride": "dallas-event-2019"
});

EXAMPLE RESPONSE
{
    "url": "https://store.aso.com/register/dallas-event-2019"
}

```

##### Arguments

* urlOverride (required) - The properly formatted Advanced StudioOnline urlOverride for the event. If the urlOverride is not properly formatted, it will be properly formatted first.

##### Returns

Returns the url that is used in Advanced StudioOnline to view the event. Returns an error if urlOverride is empty.

### Event Assignments

#### Create an event assignment

```
DEFINITION
POST http://apiserver/events/:eventId/assignments

EXAMPLE REQUEST
$.post("http://localhost:49195/events/OCC/assignments", {
    "assignedToAccessor": "6630",
    "functionalCategory": "OCC",
    "type": "VOLUNTEER",
    "start": "2015-02-20",
    "isPrimary": true,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "1011",
    "eventCode": "OCC",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "OCC",
    "functionalCategoryDescription": "Operation Christmas Child"
    "type": "VOLUNTEER",
    "typeDescription": "Region volunteer"
    "start": "2015-02-20",
    "end": null,
    "isPrimary": true,
    "isActive": true
}

```

Creates a new event assignment object.

##### Arguments

* assignedToAccessor (required) - The accessor of the user or authorized account assigned to the event.
* functionalCategory (required) - The function of the assignment. This can be used to denote the department of the accessor.
* type (optional) - The type of the assignment.
* start (required) - When the assignment starts.
* end (optional) - When the assignment ends.
* isPrimary (optional) - Whether or not the assignment is primary for the functional category. Defaulted to false.
* isActive (optional) - Whether or not the assignment is active. Defaulted to false.

##### Returns

Returns an event assignment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined accessor).

#### Retrieve an event assignment

```
DEFINITION
GET http://apiserver/events/:eventId/assignments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/OCC/assignments/1011");

EXAMPLE RESPONSE
{
    "id": "1011",
    "eventCode": "OCC",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "OCC",
    "functionalCategoryDescription": "Operation Christmas Child"
    "type": "VOLUNTEER",
    "typeDescription": "Region volunteer"
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20",
    "end": null
}

```

Retrieves the details of an existing event assignment.

##### Arguments

* id (required) - The id of the event assignment to retrieve.

##### Returns

Returns an event assignment object if a valid id was provided.

#### Update an event assignment

```
DEFINITION
POST http://apiserver/events/:eventId/assignments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/OCC/assignments/1011", {
    "functionalCategory": "DM",
    "type": "REGIONDIR"
});

EXAMPLE RESPONSE
{
    "id": "1011",
    "eventCode": "OCC",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Donor Ministries"
    "type": "REGIONDIR",
    "typeDescription": "Regional Director"
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20",
    "end": null
}


```

Updates the specified event assignment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the event.
* functionalCategory (optional) - The function of the assignment. This can be used to denote the department of the accessor.
* type (optional) - The type of the assignment.
* isPrimary (optional) - Whether or not the assignment is primary for the functionalCategory.
* isActive (optional) - Whether or not the assignment is active.
* start (optional) - When the assignment starts.
* end (optional) - When the assignment ends.

##### Returns

Returns the event assignment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined event or accessor).

#### Delete an event assignment

```
DEFINITION
DELETE http://apiserver/events/:eventId/assignments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/OCC/assignments/1011", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event assignment.

##### Arguments

* id (required) - The id of the event assignment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the event assignment does not exist, this call returns an error.

#### List all event assignments

```
DEFINITION
GET http://apiserver/events/:eventId/assignments

EXAMPLE REQUEST
$.get("http://localhost:49195/events/OCC/assignments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1011",
            "eventCode": "OCC",
            "assignedToAccessor": "6630",
            "assignedToAccessorDescription": "Webber Bradley",
            "functionalCategory": "OCC",
            "functionalCategoryDescription": "Operation Christmas Child"
            "type": "VOLUNTEER",
            "typeDescription": "Region volunteer"
            "start": "2015-02-20",
            "end": null,
            "isPrimary": true,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all event assignments.

##### Returns

A dictionary with an items property that contains an array of up to limit event assignments, starting at index offset. Each entry in the array is a separate event assignment object. If no more event assignments are available, the resulting array will be empty. This request should never return an error.

### Event Groups

#### Create an event group

```
DEFINITION
POST http://apiserver/eventgroups

EXAMPLE REQUEST
$.post("http://localhost:49195/eventgroups", {
    "description": "DonorDirect",
    "account": "27494",
    "area": "DALLAS",
    "defaultPriceCode": "GRPDISC",
    "start": "2014-09-09",
    "end": "2016-10-11"
});

EXAMPLE RESPONSE
{
    "id": "4",
    "description": "DonorDirect",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "area": "DALLAS",
    "areaDescription": "Dallas Event Area",
    "defaultPriceCode": "GRPDISC",
    "defaultPriceDescription": "Group price code",
    "registrants": 0,
    "start": "2014-09-09",
    "end": "2016-10-11",
    "isActive": true
}

```

Creates a new event group.

##### Arguments

* description (optional) - The description of the group.
* account (required) - The account number for the group.
* area (required) - The event area code for the group. Must be a valid `DDCEVAREA` code.
* defaultPriceCode (optional) - The default price code for the group. Must be a valid `DDCEVTPRCD` code.
* start (optional) - The start date for the group.
* end (optional) - The end date for the group.
* isActive (optional : default true) - Indicates whether the group is active.

##### Returns

Returns an event group object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event group

```
DEFINITION
GET http://apiserver/eventgroups/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventgroups/4");

EXAMPLE RESPONSE
{
    "id": "4",
    "description": "DonorDirect",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "area": "DALLAS",
    "areaDescription": "Dallas Event Area",
    "defaultPriceCode": "GRPDISC",
    "defaultPriceDescription": "Group price code",
    "registrants": 0,
    "start": "2014-09-09",
    "end": "2016-10-11",
    "isActive": true
}

```

Retrieves the details of an existing event group. You need only supply the id.

##### Arguments

* id (required) - The id of the event group to be retrieved.

#### Retrieve an event group by group code

```
DEFINITION
GET http://apiserver/eventgroups/groupcode/:groupcode

EXAMPLE REQUEST
$.get("http://localhost:49195/eventgroups/groupcode/DDC");

EXAMPLE RESPONSE
{
    "id": "4",
    "groupCode": "DDC",
    "description": "DonorDirect",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "area": "DALLAS",
    "areaDescription": "Dallas Event Area",
    "defaultPriceCode": "GRPDISC",
    "defaultPriceDescription": "Group price code",
    "registrants": 0,
    "start": "2014-09-09",
    "end": "2016-10-11",
    "isActive": true
}

```

Retrieves the details of an existing event group. You need only supply the group code.

##### Arguments

* groupcode (required) - The group code of the event group to be retrieved.

#### Update an event group

```
DEFINITION
POST http://apiserver/eventgroups/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventgroups/4", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "4",
    "description": "DonorDirect",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "area": "DALLAS",
    "areaDescription": "Dallas Event Area",
    "defaultPriceCode": "GRPDISC",
    "defaultPriceDescription": "Group price code",
    "registrants": 0,
    "start": "2014-09-09",
    "end": "2016-10-11",
    "isActive": false
}


```

Updates the specified event group by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the group.
* account (optional) - The account number for the group.
* area (optional) - The event area code for the group. Must be a valid `DDCEVAREA` code.
* defaultPriceCode (optional) - The default price code for the group. Must be a valid `DDCEVTPRCD` code.
* start (optional) - The start date for the group.
* end (optional) - The end date for the group.
* isActive (optional) - Indicates whether the group is active.

##### Returns

Returns the event group object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event group

```
DEFINITION
DELETE http://apiserver/eventgroups/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventgroups/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event group. It cannot be undone.

##### Arguments

* id (required) - The id of the event group to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event group does not exist, this call returns an error.

#### List all event groups

```
DEFINITION
GET http://apiserver/eventgroups

EXAMPLE REQUEST
$.get("http://localhost:49195/eventgroups?area=DALLAS");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "description": "DonorDirect",
            "account": "27494",
            "accountName": "Captain Jean-Luc Picard",
            "area": "DALLAS",
            "areaDescription": "Dallas Event Area",
            "defaultPriceCode": "GRPDISC",
            "defaultPriceDescription": "Group price code",
            "registrants": 0,
            "start": "2014-09-09",
            "end": "2016-10-11",
            "isActive": false,
            "groupCode": "DD"
        },
        {...},
    ]
}

```

Returns a list of all event groups.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filters list by exact match on group id.
* description (optional) - Filters list by partial match on description.
* account (optional) - Filters list by exact match on account number.
* area (optional) - Filters list by partial match on event area code.
* defaultPriceCode (optional) - Filters list by partial match on default price code.
* groupCode (optional) - Filters list by partial match on group code.

##### Returns

A dictionary with an items property that contains an array of up to limit event groups, starting at index offset. Each entry in the array is a separate event group object. If no more event groups are available, the resulting array will be empty. This request should never return an error.

### Event Group View Accounts

#### Retrieve an event group view account

```
DEFINITION
GET http://apiserver/eventgroups/:id/viewaccounts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventgroups/1/viewaccounts/1000008116");

EXAMPLE RESPONSE
{
    "id": "1000008116",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "event": "CRZYLVE",
    "eventDescription": "Pastor's Conference with Francis Chan"
}

```

Retrieves the details of an existing event group view account. You need only supply the attendee id.

##### Arguments

* id (required) - The attendee id of the event group view account to be retrieved.

#### List all event group view accounts

```
DEFINITION
GET http://apiserver/eventgroups/:id/viewaccounts

EXAMPLE REQUEST
$.get("http://localhost:49195/eventgroups/1/viewaccounts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000008116",
            "account": "27494",
            "accountName": "Captain Jean-Luc Picard",
            "event": "CRZYLVE",
            "eventDescription": "Pastor's Conference with Francis Chan"
        },
        {...},
    ]
}

```

Returns a list of all event group view accounts.

##### Returns

A dictionary with an items property that contains an array of up to limit event group view accounts, starting at index offset. Each entry in the array is a separate view account object. If no more event group view accounts are available, the resulting array will be empty. This request should never return an error.

### Event Prices

#### Create an event price

```
DEFINITION
POST http://apiserver/events/:id/prices

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/prices", {
    "type": "CHILD",
    "amount": 55.55
});

EXAMPLE RESPONSE
{
    "id": "141",
    "type": "CHILD",
    "description": "Child Price 6-12",
    "amount": 55.55,
    "start": null,
    "end": null,
    "useInStudioOnline": false,
    "isActive": true
}

```

Creates a new event price.

##### Arguments

* type (required) - The type of the price, must be a valid event price code (DDCEVTPRCD).
* amount (required) - The amount of the price.
* start (optional) - The start date for this price.
* end (optional) - The end date for this price.
* useInStudioOnline (optional : default false) - Indicates whether to use this price in StudioOnline.
* isActive (optional : default true) - Indicates whether this price is active.

##### Returns

Returns an event price object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event price

```
DEFINITION
GET http://apiserver/events/:id/prices/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/prices/141");

EXAMPLE RESPONSE
{
    "id": "141",
    "type": "CHILD",
    "description": "Child Price 6-12",
    "amount": 55.55,
    "start": null,
    "end": null,
    "useInStudioOnline": false,
    "isActive": true
}

```

Retrieves the details of an existing event price. You need only supply the id.

##### Arguments

* id (required) - The id of the event price to be retrieved.

#### Update an event price

```
DEFINITION
POST http://apiserver/events/:id/prices/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/prices/141", {
    "amount": 55.00,
    "start": "2015-09-04",
    "end": "2015-09-14"
});

EXAMPLE RESPONSE
{
    "id": "141",
    "type": "CHILD",
    "description": "Child Price 6-12",
    "amount": 55,
    "start": "2015-09-04",
    "end": "2015-09-14",
    "useInStudioOnline": false,
    "isActive": true
}


```

Updates the specified event price by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of the price, must be a valid event price code (DDCEVTPRCD).
* amount (optional) - The amount of the price.
* start (optional) - The start date for this price.
* end (optional) - The end date for this price.
* useInStudioOnline (optional) - Indicates whether to use this price in StudioOnline.
* isActive (optional) - Indicates whether this price is active.

##### Returns

Returns the event price object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event price

```
DEFINITION
DELETE http://apiserver/events/:id/prices/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/prices/141", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event price. It cannot be undone.

##### Arguments

* id (required) - The id of the event price to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event price does not exist, this call returns an error.

#### List all event prices

```
DEFINITION
GET http://apiserver/events/:id/prices

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/prices?forEventEntry=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "141",
            "type": "CHILD",
            "description": "Child Price 6-12",
            "amount": 55,
            "start": "2015-09-04",
            "end": "2015-09-14",
            "useInStudioOnline": false,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all event prices.

##### Arguments

* forEventEntry (optional) - `forEventEntry=true` filters the list of event price codes to only the active price codes available for event entry

##### Returns

A dictionary with an items property that contains an array of up to limit event prices, starting at index offset. Each entry in the array is a separate event price object. If no more event prices are available, the resulting array will be empty. This request should never return an error.

### Event Session Advanced StudioOnline Configuration

#### Create an event session Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/events/:id/sessionconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/events/2019DAL/sessionconfigurations", {
    "session": "S101",
    "useInStudioOnline": true,
    "title": "Dallas Event 2019 - Opening - Day 1",
    "description": "Day 1 General Session that will open the conference"
    "showVenueInformation": false
});

EXAMPLE RESPONSE
{
    "id": "10015",
    "session": "S101",
    "sessionDescription": "Opening = Day 1",
    "useInStudioOnline": true,
    "title": "Dallas Event 2019 - Opening - Day 1",
    "description": "Day 1 General Session that will open the conference",
    "showVenueInformation": false
}

```

Creates a new event session Advanced StudioOnline configuration.

##### Arguments

* session (required) - The event session id for this configuration. Must be a valid session for the event.
* title (required) - The online title for the event session configuration.
* description (optional) - The online description for the event session configuration.
* useInStudioOnline (optional) - Whether the event session should be used for StudioOnline.
* showVenueInformation (optional) - Whether the venue information of the event session will be sent to StudioOnline.

##### Returns

Returns an event session Advanced StudioOnline configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session Advanced StudioOnline configuration

```
DEFINITION
GET http://apiserver/events/:id/sessionconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/2019DAL/sessionconfigurations/10015");

EXAMPLE RESPONSE
{
    "id": "10015",
    "session": "S101",
    "sessionDescription": "Opening = Day 1",
    "useInStudioOnline": true,
    "title": "Dallas Event 2019 - Opening - Day 1",
    "description": "Day 1 General Session that will open the conference",
    "showVenueInformation": false
}

```

Retrieves the details of a event session Advanced StudioOnline configuration. You need only supply the event id and configuration id.

##### Returns

Returns an event session Advanced StudioOnline configuration object if valid ids were provided.

#### Update an event session Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/events/:id/sessionconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/2019DAL/sessionconfigurations/10015", {
    "showVenueInformation": true
});

EXAMPLE RESPONSE
{
    "id": "10015",
    "session": "S101",
    "sessionDescription": "Opening = Day 1",
    "useInStudioOnline": true,
    "title": "Dallas Event 2019 - Opening - Day 1",
    "description": "Day 1 General Session that will open the conference",
    "showVenueInformation": true
}


```

Updates the specified event session Advanced StudioOnline configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title (optional) - The online title for the event session configuration.
* description (optional) - The online description for the event session configuration.
* useInStudioOnline (optional) - Whether the event session should be used for StudioOnline.
* showVenueInformation (optional) - Whether the venue information of the event session will be sent to StudioOnline.

##### Returns

Returns an event session Advanced StudioOnline configuration object if the update succeeded. Returns an error if update parameters are invalid (e.g. the `title` is more than 900 characters).

#### Delete an event session Advanced StudioOnline configuration

```
DEFINITION
DELETE http://apiserver/events/:id/sessionconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/2019DAL/sessionconfigurations/10015", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session Advanced StudioOnline configuration. It cannot be undone.

##### Arguments

* id (required) - The event session Advanced StudioOnline configuration id of the configuration to be deleted.

##### Returns

Returns a 204 No Content response on success. If the event session Advanced StudioOnline configuration does not exist, this call returns an error.

#### List all event session Advanced StudioOnline configurations

```
DEFINITION
GET http://apiserver/events/:id/sessionconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/events/2019DAL/sessionconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10015",
            "session": "S101",
            "sessionDescription": "Opening = Day 1",
            "useInStudioOnline": true,
            "title": "Dallas Event 2019 - Opening - Day 1",
            "description": "Day 1 General Session that will open the conference",
            "showVenueInformation": true
        }
        {...},
        {...}
    ]
}

```

Returns a list of all event session Advanced StudioOnline configurations matching the provided filter criteria.

##### Arguments

* event (required) - Filter list by an exact match in event code

##### Returns

A dictionary with an items property that contains an array of up to limit event session Advanced StudioOnline configurations, starting at index offset. Each entry in the array is a separate event session Advanced StudioOnline configuration object. If no more event session Advanced StudioOnline configurations are available, the resulting array will be empty. This request should never return an error.

### Event Session Attachments

#### Create an event session attachment

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/attachments", {
    "type":"IMAGE",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "4",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new event session attachment.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns an event session attachment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session attachment

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/attachments/4");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "4",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing event session attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the event session attachment to be retrieved.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

#### Update an event session attachment

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/attachments/4", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "4",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified event session attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the event session attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session attachment

```
DEFINITION
DELETE http://apiserver/events/:id/sessions/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S104/attachments/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the event session attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session attachment does not exist, this call returns an error.

#### List all event session attachments

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
    "dateCreated": "2018-03-12",
            "id": "4",
            "type": "OTHER",
            "typeDescription": "Other",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
    ]
}

```

Returns a list of all event session attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit event session attachments, starting at index offset. Each entry in the array is a separate event session attachment object. If no more event session attachments are available, the resulting array will be empty. This request should never return an error.

### Event Session Codes

#### Create an event session code

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/codes", {
    "type": "EVTSESSCOD",
    "value": "EVTSESSC1"
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "EVTSESSCOD",
    "typeDescription": null,
    "value": "EVTSESSC1",
    "valueDescription": "Event Sponsor on Location",
    "isActive": true
}

```

Creates a new event session code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an event session code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session code

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/codes/4");

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "EVTSESSCOD",
    "typeDescription": "Event Session Code",
    "value": "EVTSESSC1",
    "valueDescription": "Event Sponsor on Location",
    "isActive": true
}

```

Retrieves the details of an existing event session code. You need only supply the id.

##### Arguments

* id (required) - The id of the event session code to be retrieved.

#### Update an event session code

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/codes/4", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "EVTSESSCOD",
    "typeDescription": "Event Session Code",
    "value": "EVTSESSC1",
    "valueDescription": "Event Sponsor on Location",
    "isActive": false
}


```

Updates the specified event session code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the event session code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session code

```
DEFINITION
DELETE http://apiserver/events/:id/sessions/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S104/codes/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session code. It cannot be undone.

##### Arguments

* id (required) - The id of the event session code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session code does not exist, this call returns an error.

#### List all event session codes

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/codes?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "type": "EVTSESSCOD",
            "typeDescription": "Event Session Code",
            "value": "EVTSESSC1",
            "valueDescription": "Event Sponsor on Location",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all event session codes.

##### Returns

A dictionary with an items property that contains an array of up to limit event session codes, starting at index offset. Each entry in the array is a separate event session code object. If no more event session codes are available, the resulting array will be empty. This request should never return an error.

### Event Session Dates

#### Create an event session date

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/dates", {
    "type": "EVTSESSDAT",
    "value": "2015-09-15"
});

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "EVTSESSDAT",
    "typeDescription": null,
    "value": "2015-09-15",
    "isActive": true
}

```

Creates a new event session date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an event session date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session date

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/dates/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "EVTSESSDAT",
    "typeDescription": "Event Session Date",
    "value": "2015-09-15",
    "isActive": true
}

```

Retrieves the details of an existing event session date. You need only supply the id.

##### Arguments

* id (required) - The id of the event session date to be retrieved.

#### Update an event session date

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/dates/7", {
    "value": "2015-09-20"
});

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "EVTSESSDAT",
    "typeDescription": "Event Session Date",
    "value": "2015-09-20",
    "isActive": true
}


```

Updates the specified event session date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the event session date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session date

```
DEFINITION
DELETE http://apiserver/events/:id/sessions/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S104/dates/7", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session date. It cannot be undone.

##### Arguments

* id (required) - The id of the event session date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session date does not exist, this call returns an error.

#### List all event session dates

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "type": "EVTSESSDAT",
            "typeDescription": "Event Session Date",
            "value": "2015-09-20",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all event session dates.

##### Returns

A dictionary with an items property that contains an array of up to limit event session dates, starting at index offset. Each entry in the array is a separate event session date object. If no more event session dates are available, the resulting array will be empty. This request should never return an error.

### Event Session Notes

#### Create an event session note

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/notes", {
    "type": "EVTSESSLOC",
    "shortComment": "In the middle of nowhere"
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "EVTSESSLOC",
    "typeDescription": null,
    "shortComment": "In the middle of nowhere",
    "longComment": null
}

```

Creates a new event session note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns an event session note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session note

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/notes/4");

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "EVTSESSLOC",
    "typeDescription": "Event Session Location",
    "shortComment": "In the middle of nowhere",
    "longComment": null
}

```

Retrieves the details of an existing event session note. You need only supply the id.

##### Arguments

* id (required) - The id of the event session note to be retrieved.

#### Update an event session note

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/notes/4", {
    "longComment": "take a left at the rock and keep going until you get to the tree with the mark on it, then turn right"
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "EVTSESSLOC",
    "typeDescription": "Event Session Location",
    "shortComment": "In the middle of nowhere",
    "longComment": "take a left at the rock and keep going until you get to the tree with the mark on it, then turn right"
}


```

Updates the specified event session note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the event session note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session note

```
DEFINITION
DELETE http://apiserver/events/:id/sessions/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S104/notes/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session note. It cannot be undone.

##### Arguments

* id (required) - The id of the event session note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session note does not exist, this call returns an error.

#### List all event session notes

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "type": "EVTSESSLOC",
            "typeDescription": "Event Session Location",
            "shortComment": "In the middle of nowhere",
            "longComment": "take a left at the rock and keep going until you get to the tree with the mark on it, then turn right"
        },
        {...},
    ]
}

```

Returns a list of all event session notes.

##### Returns

A dictionary with an items property that contains an array of up to limit event session notes, starting at index offset. Each entry in the array is a separate event session note object. If no more event session notes are available, the resulting array will be empty. This request should never return an error.

### Event Session Numbers

#### Create an event session number

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/numbers", {
    "type": "DDCVOLNEED",
    "value": 55
});

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "DDCVOLNEED",
    "typeDescription": null,
    "value": 55,
    "isActive": true
}

```

Creates a new event session number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an event session number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session number

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/numbers/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "DDCVOLNEED",
    "typeDescription": "Event Session Volunteers Needed",
    "value": 55,
    "isActive": true
}

```

Retrieves the details of an existing event session number. You need only supply the id.

##### Arguments

* id (required) - The id of the event session number to be retrieved.

#### Update an event session number

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/numbers/7", {
    "value": 60
});

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "DDCVOLNEED",
    "typeDescription": "Event Session Volunteers Needed",
    "value": 60,
    "isActive": true
}


```

Updates the specified event session number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the event session number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session number

```
DEFINITION
DELETE http://apiserver/events/:id/sessions/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S104/numbers/7", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session number. It cannot be undone.

##### Arguments

* id (required) - The id of the event session number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session number does not exist, this call returns an error.

#### List all event session numbers

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/numbers?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "type": "DDCVOLNEED",
            "typeDescription": "Event Session Volunteers Needed",
            "value": 60,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all event session numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit event session numbers, starting at index offset. Each entry in the array is a separate event session number object. If no more event session numbers are available, the resulting array will be empty. This request should never return an error.

### Event Session Prices

#### Create an event session price

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/prices

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/prices", {
    "type": "EB",
    "amount": 10.00
});

EXAMPLE RESPONSE
{
    "id": "10123",
    "type": "EB",
    "description": "Early Bird",
    "amount": 10
}

```

Creates a new event session price.

##### Arguments

* type (required) - The type of the price, must be a valid session price code (DDCSESSPCD).
* amount (required) - The amount of the price.

##### Returns

Returns an event session price object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session price

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/prices/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/prices/10123");

EXAMPLE RESPONSE
{
    "id": "10123",
    "type": "EB",
    "description": "Early Bird",
    "amount": 10
}

```

Retrieves the details of an existing event session price. You need only supply the id.

##### Arguments

* id (required) - The id of the event session price to be retrieved.

#### Update an event session price

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/prices/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/prices/10123", {
    "amount": 12.50
});

EXAMPLE RESPONSE
{
    "id": "10123",
    "type": "EB",
    "description": "Early Bird",
    "amount": 12.5
}


```

Updates the specified event session price by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of the price, must be a valid session price code (DDCSESSPCD).
* amount (optional) - The amount of the price.

##### Returns

Returns the event session price object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session price

```
DEFINITION
DELETE http://apiserver/events/:id/sessions/:id/prices/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S104/prices/10123", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session price. It cannot be undone.

##### Arguments

* id (required) - The id of the event session price to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session price does not exist, this call returns an error.

#### List all event session prices

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/prices

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/prices?type=E");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "10123",
            "type": "EB",
            "description": "Early Bird",
            "amount": 12.5
        },
        {...},
    ]
}

```

Returns a list of all event session prices.

##### Arguments

* type (optional) - Filter by partial match on type

##### Returns

A dictionary with an items property that contains an array of up to limit event session prices, starting at index offset. Each entry in the array is a separate event session price object. If no more event session prices are available, the resulting array will be empty. This request should never return an error.

### Event Session Staff

#### Create an event session staff

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/staff

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/staff", {
    "account": "27494",
    "type": "SEC"
});

EXAMPLE RESPONSE
{
    "id": "28",
    "account": "27494",
    "name": "Captain Jean-Luc Picard",
    "type": "SEC",
    "typeDescription": "Security"
}

```

Creates a new event session staff.

##### Arguments

* account (required) - Account number of the staff member. Must be unique. Must be a valid account for given event (DDCEVENTSS).
* type (optional) - The event staff type for the staff member, must be a valid staff type (DDCEVENTST).

##### Returns

Returns an event session staff object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session staff

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/staff/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/staff/28");

EXAMPLE RESPONSE
{
    "id": "28",
    "account": "27494",
    "name": "Captain Jean-Luc Picard",
    "type": "SEC",
    "typeDescription": "Security"
}

```

Retrieves the details of an existing event session staff. You need only supply the id.

##### Arguments

* id (required) - The id of the event session staff to be retrieved.

#### Update an event session staff

```
DEFINITION
POST http://apiserver/events/:id/sessions/:id/staff/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S104/staff/28", {
    "type": "SPK"
});

EXAMPLE RESPONSE
{
    "id": "28",
    "account": "27494",
    "name": "Captain Jean-Luc Picard",
    "type": "SPK",
    "typeDescription": "Speaker"
}


```

Updates the specified event session staff by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* account (optional) - Account number of the staff member. Must be unique. Must be a valid account for given event (DDCEVENTSS).
* type (optional) - The event staff type for the staff member, must be a valid staff type (DDCEVENTST).

##### Returns

Returns the event session staff object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session staff

```
DEFINITION
DELETE http://apiserver/events/:id/sessions/:id/staff/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S104/staff/28", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session staff. It cannot be undone.

##### Arguments

* id (required) - The id of the event session staff to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session staff does not exist, this call returns an error.

#### List all event session staff

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id/staff

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S104/staff");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "28",
            "account": "27494",
            "name": "Captain Jean-Luc Picard",
            "type": "SPK",
            "typeDescription": "Speaker"
        },
        {...},
    ]
}

```

Returns a list of all event session staff.

##### Returns

A dictionary with an items property that contains an array of up to limit event session staff, starting at index offset. Each entry in the array is a separate event session staff object. If no more event session staff are available, the resulting array will be empty. This request should never return an error.

### Event Sessions

#### Create an event session

```
DEFINITION
POST http://apiserver/events/:id/sessions

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions", {
    "id": "S114",
    "type": "SEM",
    "description": "What Every Marriage Needs",
    "venue": "RENNRICH",
    "room": "WOODLAND",
    "date": "2010-09-02",
    "start": "10:45 AM",
    "end": "12:30 PM"
});

EXAMPLE RESPONSE
{
    "id": "S114",
    "type": "SEM",
    "typeDescription": "Seminar",
    "description": "What Every Marriage Needs",
    "venue": "RENNRICH",
    "venueDescription": "Rennaissance Hotel Richardson",
    "room": "WOODLAND",
    "roomDescription": "Large Dining Room",
    "date": "2010-09-02",
    "start": "10:45 AM",
    "end": "12:30 PM",
    "canExceedCapacity": true,
    "useInStudioOnline": false
}

```

Creates a new event session.

##### Arguments

* id (required) - The session code for the session.
* venue (required) - The venue for the session, must be a valid venue (DDCEVENTVN).
* room (required) - The room for the session, must be a valid room for the given venue (DDCEVENTRM).
* type (optional) - The session type, must be a valid type (DDCEVENTTP).
* description (optional) - The description for the session.
* date (optional) - The date of the session.
* start (optional) - The start time of the session.
* end (optional) - The end time of the session.
* canExceedCapacity (optional : default true) - Indicates whether the session can be booked beyond room capacity.
* useInStudioOnline (optional : default false) - Indicates whether to use in StudioOnline.

##### Returns

Returns an event session object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event session

```
DEFINITION
GET http://apiserver/events/:id/sessions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions/S114");

EXAMPLE RESPONSE
{
    "id": "S114",
    "type": "SEM",
    "typeDescription": "Seminar",
    "description": "What Every Marriage Needs",
    "venue": "RENNRICH",
    "venueDescription": "Rennaissance Hotel Richardson",
    "room": "WOODLAND",
    "roomDescription": "Large Dining Room",
    "date": "2010-09-02",
    "start": "10:45 AM",
    "end": "12:30 PM",
    "canExceedCapacity": true,
    "useInStudioOnline": false
}

```

Retrieves the details of an existing event session. You need only supply the event session code.

##### Arguments

* id (required) - The session code of the event session to retrieve.

##### Returns

Returns an event session object if a valid id was provided.

#### Update an event session

```
DEFINITION
POST http://apiserver/events/:id/events/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10ALT1/sessions/S114", {
    "type": "CRT"
});

EXAMPLE RESPONSE
{
    "id": "S114",
    "type": "CRT",
    "typeDescription": "Concert",
    "description": "What Every Marriage Needs",
    "venue": "RENNRICH",
    "venueDescription": "Rennaissance Hotel Richardson",
    "room": "WOODLAND",
    "roomDescription": "Large Dining Room",
    "date": "2010-09-02",
    "start": "10:45 AM",
    "end": "12:30 PM",
    "canExceedCapacity": true,
    "useInStudioOnline": false
}


```

Updates the specified event session by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - The session code for the session.
* venue (optional) - The venue for the session, must be a valid venue (DDCEVENTVN).
* room (optional) - The room for the session, must be a valid room for the given venue (DDCEVENTRM).
* type (optional) - The session type, must be a valid type (DDCEVENTTP).
* description (optional) - The description for the session.
* date (optional) - The date of the session.
* start (optional) - The start time of the session.
* end (optional) - The end time of the session.
* canExceedCapacity (optional) - Indicates whether the session can be booked beyond room capacity.
* useInStudioOnline (optional) - Indicates whether to use in StudioOnline.

##### Returns

Returns the event session object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event session

```
DEFINITION
DELETE http://apiserver/events/:id/events/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10ALT1/sessions/S114", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event session. It cannot be undone.

##### Arguments

* id (required) - The id of the event session to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event session does not exist, this call returns an error.

#### List all event sessions

```
DEFINITION
GET http://apiserver/events/:id/sessions

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10ALT1/sessions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 6
    },
    "items": [
        {
            "id": "S109",
            "type": "SEM",
            "typeDescription": "Seminar",
            "description": "How Marriages Thrive",
            "venue": "RENNRICH",
            "venueDescription": "Rennaissance Hotel Richardson",
            "room": "WOODLAND",
            "roomDescription": "Large Dining Room",
            "date": "2010-09-03",
            "start": "10:30 AM",
            "end": "11:30 AM",
            "canExceedCapacity": true,
            "useInStudioOnline": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all event sessions.

##### Returns

A dictionary with an items property that contains an array of up to limit event sessions, starting at index offset. Each entry in the array is a separate event session object. If no more event sessions are available, the resulting array will be empty. This request should never return an error.

#### List all event sessions for event entry

```
DEFINITION
GET http://apiserver/events/:id/sessions?forEventEntry=true

EXAMPLE REQUEST
$.get("http://localhost:49195/events/PC11MAYDEN/sessions?forEventEntry=true&priceCode=I");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 6
    },
    "items": [
        {
            "id": "S104",
            "type": "SEM",
            "typeDescription": "Seminar",
            "description": "What Every Marriage Needs",
            "venue": "RENNRICH",
            "venueDescription": "Rennaissance Hotel Richardson",
            "room": "WOODLAND",
            "roomDescription": "Large Dining Room",
            "date": "2010-09-02",
            "start": "10:45 AM",
            "end": "12:30 PM",
            "canExceedCapacity": true,
            "useInStudioOnline": false,
            "price": 20
        },
        {...},
        {...}
    ]
}

```

#### Arguments

* forEventEntry (required) - Set to a value of `true`
* priceCode (optional) - `price` will be determined by the priceCode. If priceCode is not specified, then `price` will be zero
* id (optional) - Filter sessions by id
* description (optional) - Filter sessions by description

#### Returns

Returns event sessions valid for event entry. Response includes `price` in the response

### Event Staff

#### Create an event staff

```
DEFINITION
POST http://apiserver/events/:id/staff

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/staff", {
    "account": "27494",
    "staffType": "SPK"
});

EXAMPLE RESPONSE
{
    "id": "34",
    "account": "27494",
    "name": "Captain Jean-Luc Picard",
    "staffType": "SPK",
    "staffTypeDescription": "Speaker"
}

```

Creates a new event staff.

##### Arguments

* account (required) - Account number of the staff member. Must be unique.
* staffType (optional) - The event staff type for the staff member, must be a valid staff type (DDCEVENTST).

##### Returns

Returns an event staff object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event staff

```
DEFINITION
GET http://apiserver/events/:id/staff/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/staff/34");

EXAMPLE RESPONSE
{
    "id": "34",
    "account": "27494",
    "name": "Captain Jean-Luc Picard",
    "staffType": "SPK",
    "staffTypeDescription": "Speaker"
}

```

Retrieves the details of an existing event staff. You need only supply the id.

##### Arguments

* id (required) - The id of the event staff to be retrieved.

#### Update an event staff

```
DEFINITION
POST http://apiserver/events/:id/staff/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/events/10DAL1/staff/34", {
    "staffType": "SEC"
});

EXAMPLE RESPONSE
{
    "id": "34",
    "account": "27494",
    "name": "Captain Jean-Luc Picard",
    "staffType": "SEC",
    "staffTypeDescription": "Security"
}


```

Updates the specified event staff by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* account (optional) - Account number of the staff member. Must be unique.
* staffType (optional) - The event staff type for the staff member, must be a valid staff type (DDCEVENTST).

##### Returns

Returns the event staff object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event staff

```
DEFINITION
DELETE http://apiserver/events/:id/staff/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/events/10DAL1/staff/34", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event staff. It cannot be undone.

##### Arguments

* id (required) - The id of the event staff to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event staff does not exist, this call returns an error.

#### List all event staff

```
DEFINITION
GET http://apiserver/events/:id/staff

EXAMPLE REQUEST
$.get("http://localhost:49195/events/10DAL1/staff");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "34",
            "account": "27494",
            "name": "Captain Jean-Luc Picard",
            "staffType": "SEC",
            "staffTypeDescription": "Security"
        },
        {...},
    ]
}

```

Returns a list of all event staff.

##### Returns

A dictionary with an items property that contains an array of up to limit event staff, starting at index offset. Each entry in the array is a separate event staff object. If no more event staff are available, the resulting array will be empty. This request should never return an error.

### Event Types

#### Create an event type

```
DEFINITION
POST http://apiserver/eventtypes

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes", {
    "id": "RAF",
    "description": "Random Awesome Fun",
    "category": "CRS"
});

EXAMPLE RESPONSE
{
    "id": "RAF",
    "description": "Random Awesome Fun",
    "category": "CRS",
    "categoryDescription": "Cruise",
    "isInvitationOnly": false,
    "isActive": true,
    "defaultEvaluationType": null,
    "defaultEvaluationTypeDescription": null
}

```

Creates a new event type.

##### Arguments

* id (required) - The Event Type Code. Uniquely identifies an event type.
* description (optional) - Description of the event type.
* category (required) - The category of the event type, must be a valid 'DDCEVENTCT' code.
* isInvitationOnly (required) - Indicates whether or not events created from this event type should default to invitation-only.
* isActive (optional) - Indicates whether the event type is active.
* defaultEvaluationType (optional) - Default evaluation type for the event type, must be a valid 'DDCEVALTYP' code.

##### Returns

Returns an event type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event type

```
DEFINITION
GET http://apiserver/eventtypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes/RAF");

EXAMPLE RESPONSE
{
    "id": "RAF",
    "description": "Random Awesome Fun",
    "category": "CRS",
    "categoryDescription": "Cruise",
    "isInvitationOnly": false,
    "isActive": true,
    "defaultEvaluationType": null,
    "defaultEvaluationTypeDescription": null
}

```

Retrieves the details of an existing event type. You need only supply the id.

##### Arguments

* id (required) - The id of the event type to be retrieved.

#### Update an event type

```
DEFINITION
POST http://apiserver/eventtypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes/RAF", {
    "category": "BANQ"
});

EXAMPLE RESPONSE
{
    "id": "RAF",
    "description": "Random Awesome Fun",
    "category": "BANQ",
    "categoryDescription": "Banquet",
    "isInvitationOnly": false,
    "isActive": true,
    "defaultEvaluationType": null,
    "defaultEvaluationTypeDescription": null
}


```

Updates the specified event type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - Description of the event type.
* category (optional) - The category of the event type, must be a valid 'DDCEVENTCT' code.
* isInvitationOnly (optional) - Indicates whether or not events created from this event type should default to invitation-only
* isActive (optional) - Indicates whether the event type is active.
* defaultEvaluationType (optional) - Default evaluation type for the event type, must be a valid 'DDCEVALTYP' code.

##### Returns

Returns the event type object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event type

```
DEFINITION
DELETE http://apiserver/eventtypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventtypes/RAF", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event type. It cannot be undone.

##### Arguments

* id (required) - The id of the event type to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event type does not exist, this call returns an error.

#### List all event types

```
DEFINITION
GET http://apiserver/eventtypes

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes?category=BANQ");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "RAF",
            "description": "Random Awesome Fun",
            "category": "BANQ",
            "categoryDescription": "Banquet",
            "isInvitationOnly": false,
            "isActive": true,
            "defaultEvaluationType": null,
            "defaultEvaluationTypeDescription": null
        },
        {...},
    ]
}

```

Returns a list of all event types.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match on event type.
* description (optional) - Filter list by partial match on description.
* category (optional) - Filter list by partial match on category.
* activeOnly (optional) - Filters list based on whether the event type is active or not.

##### Returns

A dictionary with an items property that contains an array of up to limit event types, starting at index offset. Each entry in the array is a separate event type object. If no more event types are available, the resulting array will be empty. This request should never return an error.

### Event Type Session Prototypes

#### Create an event type session prototype

```
DEFINITION
POST http://apiserver/eventtypes/:id/sessionprototypes

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes/RAF/sessionprototypes", {
    "sessionCode": "S111"
});

EXAMPLE RESPONSE
{
    "id": "54",
    "sessionCode": "S111",
    "type": null,
    "typeDescription": null,
    "description": null,
    "start": null,
    "end": null,
    "occursOnDay": 0,
    "displaySequence": 0,
    "evaluationSequence": 0
}

```

Creates a new event type session prototype.

##### Arguments

* sessionCode (required) - The session code for the session prototype, must be unique.
* type (required) - The type of the session prototype. Must be a valid 'DDCEVENTSE' code.
* description (optional) - The description of the session prototype.
* start (optional) - The start time of the session prototype.
* end (optional) - The end time of the session prototype.
* occursOnDay (optional : default 0) - Indicates the day of the event that the session occurs on.
* displaySequence (optional : default 0) - The display sequence of the session prototype.
* evaluationSequence (optional : default 0) - The evaluation sequence of the session prototype.

##### Returns

Returns an event type session prototype object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event type session prototype

```
DEFINITION
GET http://apiserver/eventtypes/:id/sessionprototypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes/RAF/sessionprototypes/54");

EXAMPLE RESPONSE
{
    "id": "54",
    "sessionCode": "S111",
    "type": null,
    "typeDescription": null,
    "description": null,
    "start": null,
    "end": null,
    "occursOnDay": 0,
    "displaySequence": 0,
    "evaluationSequence": 0
}

```

Retrieves the details of an existing event type session prototype. You need only supply the id.

##### Arguments

* id (required) - The id of the event type session prototype to be retrieved.

#### Update an event type session prototype

```
DEFINITION
POST http://apiserver/eventtypes/:id/sessionprototypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes/RAF/sessionprototypes/54", {
    "type": "BFAST",
    "description": "The best breakfast ever!",
    "start": "08:00:00 AM",
    "end": "10:00:00 AM",
    "occursOnDay": 1
});

EXAMPLE RESPONSE
{
    "id": "54",
    "sessionCode": "S111",
    "type": "BFAST",
    "typeDescription": "Breakfast",
    "description": "The best breakfast ever!",
    "start": "08:00:00 AM",
    "end": "10:00:00 AM",
    "occursOnDay": 1,
    "displaySequence": 0,
    "evaluationSequence": 0
}


```

Updates the specified event type session prototype by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sessionCode (optional) - The session code for the session prototype, must be unique. Cannot be changed if dependent records exist, such as speaker kits.
* type (optional) - The type of the session prototype. Must be a valid 'DDCEVENTSE' code.
* description (optional) - The description of the session prototype.
* start (optional) - The start time of the session prototype.
* end (optional) - The end time of the session prototype.
* occursOnDay (optional) - Indicates the day of the event that the session occurs on.
* displaySequence (optional) - The display sequence of the session prototype.
* evaluationSequence (optional) - The evaluation sequence of the session prototype.

##### Returns

Returns the event type session prototype object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event type session prototype

```
DEFINITION
DELETE http://apiserver/eventtypes/:id/sessionprototypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventtypes/RAF/sessionprototypes/57", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event type session prototype . It cannot be undone.

##### Arguments

* id (required) - The id of the event type session prototype to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event type session prototype does not exist, this call returns an error.

#### List all event type session prototypes

```
DEFINITION
GET http://apiserver/eventtypes/:id/sessionprototypes

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes/RAF/sessionprototypes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "54",
            "sessionCode": "S111",
            "type": "BFAST",
            "typeDescription": "Breakfast",
            "description": "The best breakfast ever!",
            "start": "08:00:00 AM",
            "end": "10:00:00 AM",
            "occursOnDay": 1,
            "displaySequence": 0,
            "evaluationSequence": 0
        },
        {...},
    ]
}

```

Returns a list of all event type session prototypes.

##### Returns

A dictionary with an items property that contains an array of up to limit event type session prototypes, starting at index offset. Each entry in the array is a separate session prototype object. If no more event type session prototypes are available, the resulting array will be empty. This request should never return an error.

### Event Type Speaker Kits

#### Create an event type speaker kit

```
DEFINITION
POST http://apiserver/eventtypes/:id/speakerkits

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes/RAF/speakerkits", {
    "session": "S101",
    "account": "27494",
    "product": "1025"
});

EXAMPLE RESPONSE
{
    "id": "15",
    "session": "S101",
    "sessionDescription": "Why Marriages Fail",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "product": "1025",
    "productDescription": "Book Series"
}

```

Creates a new event type speaker kit.

##### Arguments

* session (required) - The session code for the speaker kit.
* account (required) - The account number for the speaker kit.
* product (required) - The product code for the speaker kit.

##### Returns

Returns an event type speaker kit object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an event type speaker kit

```
DEFINITION
GET http://apiserver/eventtypes/:id/speakerkits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes/RAF/speakerkits/15");

EXAMPLE RESPONSE
{
    "id": "15",
    "session": "S101",
    "sessionDescription": "Why Marriages Fail",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "product": "1025",
    "productDescription": "Book Series"
}

```

Retrieves the details of an existing event type speaker kit. You need only supply the id.

##### Arguments

* id (required) - The id of the event type speaker kit to be retrieved.

#### Update an event type speaker kit

```
DEFINITION
POST http://apiserver/eventtypes/:id/speakerkits/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes/RAF/speakerkits/15", {
    "session": "S102",
    "product": "50801"
});

EXAMPLE RESPONSE
{
    "id": "15",
    "session": "S102",
    "sessionDescription": "Unlocking the Mystery",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "product": "50801",
    "productDescription": "Salvation Package"
}


```

Updates the specified event type speaker kit by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* session (optional) - The session code for the speaker kit.
* account (optional) - The account number for the speaker kit.
* product (optional) - The product code for the speaker kit.

##### Returns

Returns the event type speaker kit object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an event type speaker kit

```
DEFINITION
DELETE http://apiserver/eventtypes/:id/speakerkits/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventtypes/RAF/speakerkits/15", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event type speaker kit. It cannot be undone.

##### Arguments

* id (required) - The id of the event type speaker kit to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the event type speaker kit does not exist, this call returns an error.

#### List all event type speaker kits

```
DEFINITION
GET http://apiserver/eventtypes/:id/speakerkits

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes/RAF/speakerkits");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "15",
            "session": "S102",
            "sessionDescription": "Unlocking the Mystery",
            "account": "27494",
            "accountName": "Captain Jean-Luc Picard",
            "product": "50801",
            "productDescription": "Salvation Package"
        },
        {...},
    ]
}

```

Returns a list of all event type speaker kits.

##### Returns

A dictionary with an items property that contains an array of up to limit event type speaker kits, starting at index offset. Each entry in the array is a separate speaker kit object. If no more event type speaker kits are available, the resulting array will be empty. This request should never return an error.

### Event Type Assignments

#### Create an event type assignment

```
DEFINITION
POST http://apiserver/eventtypes/:eventTypeId/assignments

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes/OCC/assignments", {
    "assignedToAccessor": "6630",
    "functionalCategory": "OCC",
    "type": "VOLUNTEER",
    "start": "2015-02-20",
    "isPrimary": true,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "1011",
    "eventType": "OCC",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "OCC",
    "functionalCategoryDescription": "Operation Christmas Child"
    "type": "VOLUNTEER",
    "typeDescription": "Region volunteer"
    "start": "2015-02-20",
    "end": null,
    "isPrimary": true,
    "isActive": true
}

```

Creates a new event type assignment object.

##### Arguments

* assignedToAccessor (required) - The accessor of the user or authorized account assigned to the event type.
* functionalCategory (required) - The function of the assignment. This can be used to denote the department of the accessor.
* type (optional) - The type of the assignment.
* start (required) - When the assignment starts.
* end (optional) - When the assignment ends.
* isPrimary (optional) - Whether or not the assignment is primary for the functional category. Defaulted to false.
* isActive (optional) - Whether or not the assignment is active. Defaulted to false.

##### Returns

Returns an event type assignment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined accessor).

#### Retrieve an event type assignment

```
DEFINITION
GET http://apiserver/eventtypes/:eventTypeId/assignments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes/OCC/assignments/1011");

EXAMPLE RESPONSE
{
    "id": "1011",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "OCC",
    "functionalCategoryDescription": "Operation Christmas Child"
    "type": "VOLUNTEER",
    "typeDescription": "Region volunteer"
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20",
    "end": null
}

```

Retrieves the details of an existing event type assignment.

##### Arguments

* id (required) - The id of the event type assignment to retrieve.

##### Returns

Returns an event type assignment object if a valid id was provided.

#### Update an event type assignment

```
DEFINITION
POST http://apiserver/eventtypes/:eventTypeId/assignments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/eventtypes/OCC/assignments/1011", {
    "functionalCategory": "DM",
    "type": "REGIONDIR"
});

EXAMPLE RESPONSE
{
    "id": "1011",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Donor Ministries"
    "type": "REGIONDIR",
    "typeDescription": "Regional Director"
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20",
    "end": null
}


```

Updates the specified event type assignment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the event type.
* functionalCategory (optional) - The function of the assignment. This can be used to denote the department of the accessor.
* type (optional) - The type of the assignment.
* isPrimary (optional) - Whether or not the assignment is primary for the functionalCategory.
* isActive (optional) - Whether or not the assignment is active.
* start (optional) - When the assignment starts.
* end (optional) - When the assignment ends.

##### Returns

Returns the event type assignment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined event type or accessor).

#### Delete an event type assignment

```
DEFINITION
DELETE http://apiserver/eventtypes/:eventTypeId/assignments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/eventtypes/OCC/assignments/1011", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an event type assignment.

##### Arguments

* id (required) - The id of the event type assignment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the event type assignment does not exist, this call returns an error.

#### List all event type assignments

```
DEFINITION
GET http://apiserver/eventtypes/:eventTypeId/assignments

EXAMPLE REQUEST
$.get("http://localhost:49195/eventtypes/OCC/assignments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1011",
            "eventType": "OCC",
            "assignedToAccessor": "6630",
            "assignedToAccessorDescription": "Webber Bradley",
            "functionalCategory": "OCC",
            "functionalCategoryDescription": "Operation Christmas Child"
            "type": "VOLUNTEER",
            "typeDescription": "Region volunteer"
            "start": "2015-02-20",
            "end": null,
            "isPrimary": true,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all event type assignments.

##### Returns

A dictionary with an items property that contains an array of up to limit event type assignments, starting at index offset. Each entry in the array is a separate event type assignment object. If no more event type assignments are available, the resulting array will be empty. This request should never return an error.

### Hotels

#### Create a hotel

```
DEFINITION
POST http://apiserver/hotels

EXAMPLE REQUEST
$.post("http://localhost:49195/hotels", {
    "event": "BMWEVNT",
    "venue": "BESTHOTEL",
    "checkInTime": "03:00:00 PM",
    "checkOutTime": "11:00:00 AM"
});

EXAMPLE RESPONSE
{
    "id": "12",
    "event": "BMWEVNT",
    "eventDescription": "BMW Event 1",
    "venue": "BESTHOTEL",
    "venueDescription": null,
    "isPrimary": true,
    "checkInTime": "03:00:00 PM",
    "checkOutTime": "11:00:00 AM",
    "promoNights": null,
    "isContractSigned": true,
    "resortFee": null,
    "otherCharges": null,
    "otherChargesNotes": null,
    "guestParking": null,
    "commuterParking": null,
    "valetParking": null,
    "reservationUrl": null,
    "mapUrl": null
}

```

Creates a new hotel.

##### Arguments

* event (required) - The event code for the hotel.
* venue (required) - The venue code for the hotel.
* isPrimary (optional : default true) - Indicates whether the hotel is primary or alternative.
* checkInTime (optional) - The check in time for the hotel.
* checkOutTime (optional) - The check out time for the hotel
* promoNights (optional) - The number of promo nights for the hotel.
* isContractSigned (optional : default true) - Indicates whether a contract is signed.
* resortFee (optional) - The resort fee for the hotel.
* otherCharges (optional) - Any other charges for the hotel.
* otherChargesNotes (optional) - Notes about the other charges for the hotel.
* guestParking (optional) - The cost for guest parking.
* commuterParking (optional) - The cost for commuter parking.
* valetParking (optional) - The cost for valet parking.
* reservationUrl (optional) - The URL for reservations.
* mapUrl (optional) - The URL for a map to the hotel.

##### Returns

Returns a hotel object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a hotel

```
DEFINITION
GET http://apiserver/hotels/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/hotels/12");

EXAMPLE RESPONSE
{
    "id": "12",
    "event": "BMWEVNT",
    "eventDescription": "BMW Event 1",
    "venue": "BESTHOTEL",
    "venueDescription": null,
    "isPrimary": true,
    "checkInTime": "03:00:00 PM",
    "checkOutTime": "11:00:00 AM",
    "promoNights": null,
    "isContractSigned": true,
    "resortFee": null,
    "otherCharges": null,
    "otherChargesNotes": null,
    "guestParking": null,
    "commuterParking": null,
    "valetParking": null,
    "reservationUrl": null,
    "mapUrl": null
}

```

Retrieves the details of an existing hotel. You need only supply the id.

##### Arguments

* id (required) - The id of the hotel to be retrieved.

#### Update a hotel

```
DEFINITION
POST http://apiserver/hotels/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/hotels/12", {
    "valetParking": 29.99
});

EXAMPLE RESPONSE
{
    "id": "12",
    "event": "BMWEVNT",
    "eventDescription": "BMW Event 1",
    "venue": "BESTHOTEL",
    "venueDescription": null,
    "isPrimary": true,
    "checkInTime": "03:00:00 PM",
    "checkOutTime": "11:00:00 AM",
    "promoNights": null,
    "isContractSigned": true,
    "resortFee": null,
    "otherCharges": null,
    "otherChargesNotes": null,
    "guestParking": null,
    "commuterParking": null,
    "valetParking": 29.99,
    "reservationUrl": null,
    "mapUrl": null
}


```

Updates the specified hotel by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* event (optional) - The event code for the hotel.
* venue (optional) - The venue code for the hotel.
* isPrimary (optional) - Indicates whether the hotel is primary or alternative.
* checkInTime (optional) - The check in time for the hotel.
* checkOutTime (optional) - The check out time for the hotel
* promoNights (optional) - The number of promo nights for the hotel.
* isContractSigned (optional) - Indicates whether a contract is signed.
* resortFee (optional) - The resort fee for the hotel.
* otherCharges (optional) - Any other charges for the hotel.
* otherChargesNotes (optional) - Notes about the other charges for the hotel.
* guestParking (optional) - The cost for guest parking.
* commuterParking (optional) - The cost for commuter parking.
* valetParking (optional) - The cost for valet parking.
* reservationUrl (optional) - The URL for reservations.
* mapUrl (optional) - The URL for a map to the hotel.

##### Returns

Returns the hotel object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a hotel

```
DEFINITION
DELETE http://apiserver/hotels/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/hotels/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a hotel. It cannot be undone.

##### Arguments

* id (required) - The id of the hotel to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the hotel does not exist, this call returns an error.

#### List all hotels

```
DEFINITION
GET http://apiserver/hotels

EXAMPLE REQUEST
$.get("http://localhost:49195/hotels?venueCode=BEST");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "12",
            "event": "BMWEVNT",
            "eventDescription": null,
            "venue": "BESTHOTEL",
            "venueDescription": null,
            "isPrimary": true,
            "checkInTime": "03:00:00 PM",
            "checkOutTime": "11:00:00 AM",
            "promoNights": null,
            "isContractSigned": true,
            "resortFee": null,
            "otherCharges": null,
            "otherChargesNotes": null,
            "guestParking": null,
            "commuterParking": null,
            "valetParking": 29.99,
            "reservationUrl": null,
            "mapUrl": null
        },
        {...},
    ]
}

```

Returns a list of all hotels.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* eventCode (optional) - Filter list by partial match on event code.
* venueCode (optional) - Filter list by partial match on venue code.

##### Returns

A dictionary with an items property that contains an array of up to limit hotels, starting at index offset. Each entry in the array is a separate hotel object. If no more hotels are available, the resulting array will be empty. This request should never return an error.

### Hotel Rooms

#### Create a hotel room

```
DEFINITION
POST http://apiserver/hotels/:id/rooms

EXAMPLE REQUEST
$.post("http://localhost:49195/hotels/13/rooms", {
    "roomType": "1K"
});

EXAMPLE RESPONSE
{
    "id": "7",
    "roomType": "1K",
    "roomTypeDescription": "1 King size bed",
    "description": null,
    "blockDate": null,
    "startDate": null,
    "rackRate": null,
    "negotiatedRate": null,
    "reservationCutoffDate": null,
    "roomsNeededForComp": null,
    "roomsReserved": null,
    "roomBlockGuaranteePercent": null,
    "minimumPickup": null,
    "actualPickup": null,
    "additionalPickup": null
}

```

Creates a new hotel room.

##### Arguments

* roomType (required) - The type of room. Must be a valid 'DDCLODG' code.
* description (optional) - The description of the room.
* blockDate (optional) - The block date for the room.
* startDate (optional) - The start date for the room.
* rackRate (optional) - The rack rate for the room.
* negotiatedRate (optional) - The negotiated rate for the room.
* reservationCutoffDate (optional) - The reservation cutoff date for the room.
* roomsNeededForComp (optional) - The number of rooms needed for comp.
* roomsReserved (optional) - The number of rooms reserved.
* roomBlockGuaranteePercent (optional) - The block guarantee percentage for the room.
* minimumPickup (optional) - The minimum pickup for the room.
* actualPickup (optional) - The actual pickup for the room.
* additionalPickup (optional) - The additional pickup for the room.

##### Returns

Returns a hotel room object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a hotel room

```
DEFINITION
GET http://apiserver/hotels/:id/rooms/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/hotels/13/rooms/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "roomType": "1K",
    "roomTypeDescription": "1 King size bed",
    "description": null,
    "blockDate": null,
    "startDate": null,
    "rackRate": null,
    "negotiatedRate": null,
    "reservationCutoffDate": null,
    "roomsNeededForComp": null,
    "roomsReserved": null,
    "roomBlockGuaranteePercent": null,
    "minimumPickup": null,
    "actualPickup": null,
    "additionalPickup": null
}

```

Retrieves the details of an existing hotel room. You need only supply the id.

##### Arguments

* id (required) - The id of the hotel room to be retrieved.

#### Update a hotel room

```
DEFINITION
POST http://apiserver/hotels/:id/rooms/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/hotels/13/rooms/7", {
    "startDate": "2015-10-09"
});

EXAMPLE RESPONSE
{
    "id": "7",
    "roomType": "1K",
    "roomTypeDescription": "1 King size bed",
    "description": null,
    "blockDate": null,
    "startDate": "2015-10-09",
    "rackRate": null,
    "negotiatedRate": null,
    "reservationCutoffDate": null,
    "roomsNeededForComp": null,
    "roomsReserved": null,
    "roomBlockGuaranteePercent": null,
    "minimumPickup": null,
    "actualPickup": null,
    "additionalPickup": null
}


```

Updates the specified hotel room by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* roomType (optional) - The type of room. Must be a valid 'DDCLODG' code.
* description (optional) - The description of the room.
* blockDate (optional) - The block date for the room.
* startDate (optional) - The start date for the room.
* rackRate (optional) - The rack rate for the room.
* negotiatedRate (optional) - The negotiated rate for the room.
* reservationCutoffDate (optional) - The reservation cutoff date for the room.
* roomsNeededForComp (optional) - The number of rooms needed for comp.
* roomsReserved (optional) - The number of rooms reserved.
* roomBlockGuaranteePercent (optional) - The block guarantee percentage for the room.
* minimumPickup (optional) - The minimum pickup for the room.
* actualPickup (optional) - The actual pickup for the room.
* additionalPickup (optional) - The additional pickup for the room.

##### Returns

Returns the hotel room object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a hotel room

```
DEFINITION
DELETE http://apiserver/hotels/:id/rooms/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/hotels/13/rooms/7", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a hotel room. It cannot be undone.

##### Arguments

* id (required) - The id of the hotel room to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the hotel room does not exist, this call returns an error.

#### List all hotel rooms

```
DEFINITION
GET http://apiserver/hotels/:id/rooms

EXAMPLE REQUEST
$.get("http://localhost:49195/hotels/13/rooms");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "roomType": "1K",
            "roomTypeDescription": "1 King size bed",
            "description": null,
            "blockDate": null,
            "startDate": "2015-10-09",
            "rackRate": null,
            "negotiatedRate": null,
            "reservationCutoffDate": null,
            "roomsNeededForComp": null,
            "roomsReserved": null,
            "roomBlockGuaranteePercent": null,
            "minimumPickup": null,
            "actualPickup": null,
            "additionalPickup": null
        },
        {...},
    ]
}

```

Returns a list of all hotel rooms.

##### Returns

A dictionary with an items property that contains an array of up to limit hotel rooms, starting at index offset. Each entry in the array is a separate hotel room object. If no more hotel rooms are available, the resulting array will be empty. This request should never return an error.

### Material Shipments

#### Create a material shipment

```
DEFINITION
POST http://apiserver/materialshipments

EXAMPLE REQUEST
$.post("http://localhost:49195/materialshipments", {
    "eventCode": "10DAL1",
    "description": "Dallas Event - 10",
    "needBy": "2015-12-12",
    "estimatedAttendees": 150
    "kitCodes": [
        "1A200",
        "1025"
    ]
});

EXAMPLE RESPONSE
{
    "id": "10030",
    "eventCode": "10DAL2",
    "eventType": "WTR",
    "description": "Dallas Event - 10",
    "status": "Y",
    "warehouse": "30",
    "location": "DALLAS",
    "needBy": "2015-12-12",
    "addDate": "2015-10-22T03:22:57 PM",
    "shipDate": null,
    "dateReceived": null,
    "estimatedAttendance": 150
}

```

Creates a new material shipment.

##### Arguments

* eventCode (required) - the event code for the material shipment request.
* description (required) - the description for the material shipment request.
* needBy (required) - the date that the material shipment needs to be completed by.
* estimatedAttendance (optional) - the estimated attendance for the event.
* kitCodes (optional) - list of kit codes that will be shipped for the event.

##### Returns

Returns a material shipment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a material shipment

```
DEFINITION
GET http://apiserver/materialshipments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/materialshipments/10030");

EXAMPLE RESPONSE
{
    "id": "10030",
    "eventCode": "10DAL2",
    "eventType": "WTR",
    "description": "Dallas Event - 10",
    "status": "Y",
    "warehouse": "30",
    "location": "DALLAS",
    "needBy": "2015-12-12",
    "addDate": "2015-10-22T03:22:57 PM",
    "shipDate": null,
    "dateReceived": null,
    "estimatedAttendance": 150
}

```

Retrieves the details of an existing material shipment. You need only supply the id.

##### Arguments

* id (required) - The id of the material shipment to be retrieved.

#### Update a material shipment

```
DEFINITION
POST http://apiserver/materialshipments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/materialshipments/10030", {
    "description": "DFW Event - 10"
});

EXAMPLE RESPONSE
{
    "id": "10030",
    "eventCode": "10DAL2",
    "eventType": "WTR",
    "description": "DFW Event - 10",
    "status": "Y",
    "warehouse": "30",
    "location": "DALLAS",
    "needBy": "2015-12-12",
    "addDate": "2015-10-22T03:22:57 PM",
    "shipDate": null,
    "dateReceived": null,
    "estimatedAttendance": 150
}

```

Updates the specified material shipment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - the updated description for the material shipment request.
* needBy (optional) - the updated date that the material shipment needs to be completed by.
* estimatedAttendance (optional) - updated value for the estimated attendance for the event.

##### Returns

Returns the material shipment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a material shipment

```
DEFINITION
DELETE http://apiserver/materialshipments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/materialshipments/10030", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a material shipment. It cannot be undone.

##### Arguments

* id (required) - The id of the material shipment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the material shipment does not exist, this call returns an error.

#### List all material shipments

```
DEFINITION
GET http://apiserver/materialshipments

EXAMPLE REQUEST
$.get("http://localhost:49195/materialshipments?eventType=WTR");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10030",
            "eventCode": "10DAL2",
            "eventType": "WTR",
            "description": "DFW Event - 10",
            "status": "Y",
            "warehouse": "30",
            "location": "DALLAS",
            "needBy": "2015-12-12",
            "addDate": "2015-10-22T03:22:57 PM",
            "shipDate": null,
            "dateReceived": null,
            "estimatedAttendance": 150
        },
        {...},
    ]
}

```

Returns a list of all material shipments.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* eventCode (optional) - the event code to filter results on.
* eventType (optional) - the event type to filter results on.

##### Returns

A dictionary with an items property that contains an array of up to limit material shipments, starting at index offset. Each entry in the array is a separate material shipment object. If no more material shipments are available, the resulting array will be empty. This request should never return an error.

#### Material Shipment Change Status

```
DEFINITION
POST http://materialshipments/:shipmentId/changestatus

EXAMPLE REQUEST
$.post("http://localhost:49195/materialshipments/:shipmentId/changestatus", {
    "newStatus": "C"
});

EXAMPLE RESPONSE
{
    "id":"10030",
    "oldStatus":"Y",
    "newStatus":"C",
    "message":"Transaction 292693 was created to commit the transfer quantity for each product to the Home Warehouse."
}

```

Performs a status change for the specified material shipment to the provided status.

##### Arguments

* newStatus (required) - The status to update the material shipment request to.

##### Returns

Returns a status change object if the call succeeded. Returns an error if the status change throws an error.

### Material Shipment Details

#### Create a material shipment detail

```
DEFINITION
POST http://apiserver/materialshipments/:shipmentId/details

EXAMPLE REQUEST
$.post("http://localhost:49195/materialshipments/10030/details", {
    "product": "100BKLET",
    "quantityRequired": 15,
    "quantityToTransfer": "15"
});

EXAMPLE RESPONSE
{
    "id": "30188",
    "product": "100BKLET",
    "productDescription": "Small Booklet",
    "quantityRequired": 1,
    "quantityAtSite": 0,
    "quantityAtHome": 10,
    "quantityToTransfer": 1,
    "quantityToShip": 0,
    "orderDetailRecordId": null
}

```

Creates a new material shipment detail.

##### Arguments

* product (required) - The product code required for the material shipment detail.
* quantityRequired (required) - The number of the product required for the material shipment detail.

##### Returns

Returns a material shipment detail object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a material shipment detail

```
DEFINITION
GET http://apiserver/materialshipments/:shipmentId/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/materialshipments/10030/details/30188");

EXAMPLE RESPONSE
{
    "id": "30188",
    "product": "100BKLET",
    "productDescription": "Small Booklet",
    "quantityRequired": 1,
    "quantityAtSite": 0,
    "quantityAtHome": 10,
    "quantityToTransfer": 1,
    "quantityToShip": 0,
    "orderDetailRecordId": null
}

```

Retrieves the details of an existing material shipment detail. You need only supply the id.

##### Arguments

* id (required) - The id of the material shipment detail to be retrieved.

#### Update a material shipment detail

```
DEFINITION
POST http://apiserver/materialshipments/:shipmentId/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/materialshipments/10030/details/30188", {
    "quantityRequired": 3
});

EXAMPLE RESPONSE
{
    "id": "30188",
    "product": "100BKLET",
    "productDescription": "Small Booklet",
    "quantityRequired": 3,
    "quantityAtSite": 0,
    "quantityAtHome": 0,
    "quantityToTransfer": 1,
    "quantityToShip": 0,
    "orderDetailRecordId": null
}

```

Updates the specified material shipment detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged. NOTE - material shipment details can only be updated when the status of the parent material shipment is 'Y' (Ready).

##### Arguments

* product (optional) - The updated product code to be shipped.
* quantityRequired (optional) - The updated required item count to be shipped to the event warehouse. Only used when material shipment status is uncommitted.
* quantityToTransfer (optional) - The updated item count to transfer to the event warehouse. Only used when material shipment status is committed.

##### Returns

Returns the material shipment detail object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a material shipment detail

```
DEFINITION
DELETE http://apiserver/materialshipments/:shipmentId/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/materialshipments/10030/details/30188", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a material shipment detail. It cannot be undone.

##### Arguments

* id (required) - The id of the material shipment detail to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the material shipment detail does not exist, this call returns an error.

#### List all material shipment details

```
DEFINITION
GET http://apiserver/materialshipments/:shipmentId/details

EXAMPLE REQUEST
$.get("http://localhost:49195/materialshipments/10030/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "30188",
            "product": "100BKLET",
            "productDescription": "Small Booklet",
            "quantityRequired": 3,
            "quantityAtSite": 0,
            "quantityAtHome": 0,
            "quantityToTransfer": 1,
            "quantityToShip": 0,
            "orderDetailRecordId": null
        },
        {...},
    ]
}

```

Returns a list of all material shipment details.

##### Returns

A dictionary with an items property that contains an array of up to limit material shipment details, starting at index offset. Each entry in the array is a separate material shipment detail object. If no more material shipment details are available, the resulting array will be empty. This request should never return an error.

#### Material Shipment Detail Product Quantities

```
DEFINITION
POST http://materialshipments/:shipmentId/productquantities/:productCode

EXAMPLE REQUEST
$.post("http://localhost:49195/materialshipments/10030/productquantities/100BKLET");

EXAMPLE RESPONSE
{
    quantityAtSite: 0,
    quantityAtHome: 10
}

```

Returns the quantities of the specified product at the home warehouse location, as well as the event warehouse location.

##### Returns

Returns a product quantity count object if the call succeeded. Returns an error if the product code is invalid.

### Media Calendars

#### Create a media calendar

```
DEFINITION
POST http://apiserver/mediacalendars

EXAMPLE REQUEST
$.post("http://localhost:49195/mediacalendars", {
    "month": 11,
    "year": 2015,
    "start": "2015-11-01",
    "end": "2015-11-30"
});

EXAMPLE RESPONSE
{
    "id": "39",
    "year": 2015,
    "month": 11,
    "start": "2015-11-01",
    "end": "2015-11-30"
}

```

Creates a new media calendar.

##### Arguments

* year (required) - The year of the media calendar to create.
* month (required) - The month of the media calendar to create.
* start (required) - The start date of the media calendar.
* end (required) - The end date of the media calendar.

##### Returns

Returns a media calendar object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media calendar

```
DEFINITION
GET http://apiserver/mediacalendars/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediacalendars/39");

EXAMPLE RESPONSE
{
    "id": "39",
    "year": 2015,
    "month": 11,
    "start": "2015-11-01",
    "end": "2015-11-30"
}

```

Retrieves the details of an existing media calendar. You need only supply the id.

##### Arguments

* id (required) - The id of the media calendar to be retrieved.

#### Update a media calendar

```
DEFINITION
POST http://apiserver/mediacalendars/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediacalendars/39", {
    "start": "2015-11-02",
    "end": "2015-11-27"
});

EXAMPLE RESPONSE
{
    "id": "39",
    "year": 2015,
    "month": 11,
    "start": "2015-11-02",
    "end": "2015-11-27"
}


```

Updates the specified media calendar by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* year (optional) - The year of the media calendar to create.
* month (optional) - The month of the media calendar to create.
* start (optional) - The start date of the media calendar.
* end (optional) - The end date of the media calendar.

##### Returns

Returns the media calendar object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media calendar

```
DEFINITION
DELETE http://apiserver/mediacalendars/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediacalendars/33", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media calendar. It cannot be undone.

##### Arguments

* id (required) - The id of the media calendar to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media calendar does not exist, this call returns an error.

#### List all media calendars

```
DEFINITION
GET http://apiserver/mediacalendars

EXAMPLE REQUEST
$.get("http://localhost:49195/mediacalendars?year=2015");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "30",
            "year": 2015,
            "month": 7,
            "start": "2015-07-15",
            "end": "2015-07-31"
        },
        {...},
    ]
}

```

Returns a list of all media calendars.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* year (optional) - The year of the media calendar to create.
* month (optional) - The month of the media calendar to create.

##### Returns

A dictionary with an items property that contains an array of up to limit media calendars, starting at index offset. Each entry in the array is a separate media calendar object. If no more media calendars are available, the resulting array will be empty. This request should never return an error.

### Media Message Attachments

#### Create a media message attachment

```
DEFINITION
POST http://apiserver/mediamessages/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new media message attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a media message attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a media message attachment

```
DEFINITION
GET http://apiserver/mediamessages/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing media message attachment. You need only supply the media message id and media message attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a media message attachment object if a valid id was provided.

#### Update a media message attachment

```
DEFINITION
POST http://apiserver/mediamessages/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified media message attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type. Must be a defined attachment type.
* url (optional) - The url of the attachment type.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the media message attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a media message attachment

```
DEFINITION
DELETE http://apiserver/mediamessages/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediamessages/32/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media message attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the media message attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media message attachment id does not exist, this call returns an error.

#### List all media message attachments

```
DEFINITION
GET http://apiserver/mediamessages/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media message attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit media message attachments, starting at index offset. Each entry in the array is a separate media message attachment object. If no more media message attachments are available, the resulting array will be empty. This request should never return an error.

### Media Message Codes

#### Create a media message code

```
DEFINITION
POST http://apiserver/mediamessages/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/codes", {
    "isActive": true,
    "type": "MSGCODE1",
    "value": "MATERIALS"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "MSGCODE1",
    "typeDescription": null,
    "value": "MATERIALS",
    "valueDescription": "Requesting specific materials",
    "isActive": true
}

```

Creates a new media message code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a media message code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a media message code

```
DEFINITION
GET http://apiserver/mediamessages/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/codes/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "MSGCODE1",
    "typeDescription": "Media Message Code 1",
    "value": "MATERIALS",
    "valueDescription": "Requesting specific materials",
    "isActive": true
}

```

Retrieves the details of an existing media message code. You need only supply the media message id and media message code id.

##### Returns

Returns a media message code object if a valid id was provided.

#### Update a media message code

```
DEFINITION
POST http://apiserver/mediamessages/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/codes/8", {
    "value": "VOLUNTEER"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "MSGCODE1",
    "typeDescription": "Media Message Code 1",
    "value": "VOLUNTEER",
    "valueDescription": "Requesting specific materials",
    "isActive": true
}

```

Updates the specified media message code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the media message code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a media message code

```
DEFINITION
DELETE http://apiserver/mediamessages/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediamessages/32/codes/45", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media message code. It cannot be undone.

##### Arguments

* id (required) - The id of the media message code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media message code id does not exist, this call returns an error.

#### List all media message codes

```
DEFINITION
GET http://apiserver/mediamessages/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10",
            "type": "MSGADS",
            "typeDescription": "Message Advertisements",
            "value": "TRIP2011",
            "valueDescription": "Trip 2011",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media message codes.

##### Returns

A dictionary with an items property that contains an array of up to limit media message codes, starting at index offset. Each entry in the array is a separate media message code object. If no more media message codes are available, the resulting array will be empty. This request should never return an error.

### Media Message Dates

#### Create a media message date

```
DEFINITION
POST http://apiserver/mediamessages/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/dates", {
    "type": "MSGDATE1",
    "value": "2015-07-01",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "MSGDATE1",
    "typeDescription": null,
    "value": "2015-07-01",
    "isActive": true
}

```

Creates a new media message date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a media message date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a media message date

```
DEFINITION
GET http://apiserver/mediamessages/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/dates/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "MSGDATE1",
    "typeDescription": "Media Message Date 2",
    "value": "2015-07-01",
    "isActive": true
}

```

Retrieves the details of an existing media message date. You need only supply the media message id and media message date id.

##### Returns

Returns a media message date object if a valid id was provided.

#### Update a media message date

```
DEFINITION
POST http://apiserver/mediamessages/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/dates/5", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "MSGDATE1",
    "typeDescription": "Media Message Date 2",
    "value": "2015-07-16",
    "isActive": false
}

```

Updates the specified media message date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the media message date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a media message date

```
DEFINITION
DELETE http://apiserver/mediamessages/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediamessages/32/dates/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media message date. It cannot be undone.

##### Arguments

* id (required) - The id of the media message date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media message date id does not exist, this call returns an error.

#### List all media message dates

```
DEFINITION
GET http://apiserver/mediamessages/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "type": "MSGDATE1",
            "typeDescription": "Media Message Date 2",
            "value": "2015-07-01",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media message dates.

##### Returns

A dictionary with an items property that contains an array of up to limit media message dates, starting at index offset. Each entry in the array is a separate media message date object. If no more media message dates are available, the resulting array will be empty. This request should never return an error.

### Media Message Notes

#### Create a media message note

```
DEFINITION
POST http://apiserver/mediamessages/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/notes", {
    "type": "MSGNOTE1",
    "shortComment": "demo"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "MSGNOTE1",
    "typeDescription": null,
    "shortComment": "demo",
    "longComment": null
}

```

Creates a new media message note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a media message note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Retrieve a media message note

```
DEFINITION
GET http://apiserver/mediamessages/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/notes/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "MSGNOTE1",
    "typeDescription": "Media Message Note 1",
    "shortComment": "demo",
    "longComment": null
}

```

Retrieves the details of an existing media message note. You need only supply the media message id and media message note id.

##### Returns

Returns a media message note object if a valid id was provided.

#### Update a media message note

```
DEFINITION
POST http://apiserver/mediamessages/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/notes/3", {
    "longComment": "now we have a long comment"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "MSGNOTE1",
    "typeDescription": "Media Message Note 1",
    "shortComment": "demo",
    "longComment": "now we have a long comment"
}

```

Updates the specified media message note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the media message note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a media message note

```
DEFINITION
DELETE http://apiserver/mediamessages/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediamessages/32/notes/9", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media message note. It cannot be undone.

##### Arguments

* id (required) - The id of the media message note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media message note id does not exist, this call returns an error.

#### List all media message notes

```
DEFINITION
GET http://apiserver/mediamessages/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "type": "MSGNOTE1",
            "typeDescription": "Media Message Note 1",
            "shortComment": "demo",
            "longComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media message notes.

##### Returns

A dictionary with an items property that contains an array of up to limit media message notes, starting at index offset. Each entry in the array is a separate media message note object. If no more media message notes are available, the resulting array will be empty. This request should never return an error.

### Media Message Numbers

#### Create a media message number

```
DEFINITION
POST http://apiserver/mediamessages/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/numbers", {
    "type": "MSGNUMB1",
    "value": 10
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "MSGNUMB1",
    "typeDescription": null,
    "value": 10,
    "isActive": true
}

```

Creates a new media message number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a media message number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Retrieve a media message number

```
DEFINITION
GET http://apiserver/mediamessages/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/numbers/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "MSGNUMB1",
    "typeDescription": "Media Message Number 1",
    "value": 10,
    "isActive": true
}

```

Retrieves the details of an existing media message number. You need only supply the media message id and media message number id.

##### Returns

Returns a media message number object if a valid id was provided.

#### Update a media message number

```
DEFINITION
POST http://apiserver/mediamessages/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/numbers/3", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "MSGNUMB1",
    "typeDescription": "Media Message Number 1",
    "value": 10,
    "isActive": false
}

```

Updates the specified media message number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the media message number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a media message number

```
DEFINITION
DELETE http://apiserver/mediamessages/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediamessages/32/numbers/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media message number. It cannot be undone.

##### Arguments

* id (required) - The id of the media message number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media message number id does not exist, this call returns an error.

#### List all media message numbers

```
DEFINITION
GET http://apiserver/mediamessages/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "type": "MSGNUMB1",
            "typeDescription": "Media Message Number 1",
            "value": 10,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media message numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit media message numbers, starting at index offset. Each entry in the array is a separate media message number object. If no more media message numbers are available, the resulting array will be empty. This request should never return an error.

### Media Message Products

#### Create a media message product

```
DEFINITION
POST http://apiserver/mediamessages/:id/products

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/products", {
    "productCode": "100BKLET"
});

EXAMPLE RESPONSE
{
    "id": "12",
    "productCode": "100BKLET",
    "productCodeDescription": null
}

```

Creates a new media message product.

##### Arguments

* productCode (required) - The product code to add. Must be a valid code.

##### Returns

Returns a media message product object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media message product

```
DEFINITION
GET http://apiserver/mediamessages/:id/products/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/products/12");

EXAMPLE RESPONSE
{
    "id": "12",
    "productCode": "100BKLET",
    "productCodeDescription": "Small Booklet"
}

```

Retrieves the details of an existing media message product. You need only supply the id.

##### Arguments

* id (required) - The id of the media message product to be retrieved.

#### Update a media message product

```
DEFINITION
POST http://apiserver/mediamessages/:id/products/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32/products/12", {
    "productCode": "CD1000"
});

EXAMPLE RESPONSE
{
    "id": "12",
    "productCode": "CD1000",
    "productCodeDescription": "Putting Your Faith into Action "
}


```

Updates the specified media message product by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* productCode (optional) - The product code to add. Must be a valid code.

##### Returns

Returns the media message product object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media message product

```
DEFINITION
DELETE http://apiserver/mediamessages/:id/products/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediamessages/32/products/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media message product. It cannot be undone.

##### Arguments

* id (required) - The id of the media message product to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media message product does not exist, this call returns an error.

#### List all media message products

```
DEFINITION
GET http://apiserver/mediamessage/:id/products

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32/products");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "9",
            "productCode": "100BKLET",
            "productCodeDescription": "Small Booklet"
        },
        {...},
    ]
}

```

Returns a list of all media message products.

##### Returns

A dictionary with an items property that contains an array of up to limit media message products, starting at index offset. Each entry in the array is a separate media message product object. If no more media message products are available, the resulting array will be empty. This request should never return an error.

### Media Messages

#### Create a media message

```
DEFINITION
POST http://apiserver/mediamessages

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages", {
    "messageCode": "M1234",
    "description": "What Would Jesus Do?"
});

EXAMPLE RESPONSE
{
    "id": "32",
    "messageCode": "M1234",
    "description": "What Would Jesus Do?",
    "comment": null,
    "date": null
}

```

Creates a new media message.

##### Arguments

* messageCode (required) - The message code for the message. Must be unique.
* description (required) - The description of the media message.
* comment (optional) - The long comment for the message.
* date (optional) - The message date.

##### Returns

Returns a media message object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media message

```
DEFINITION
GET http://apiserver/mediamessages/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages/32");

EXAMPLE RESPONSE
{
    "id": "32",
    "messageCode": "M1234",
    "description": "What Would Jesus Do?",
    "comment": null,
    "date": null
}

```

Retrieves the details of an existing media message. You need only supply the id.

##### Arguments

* id (required) - The recordId of the media message to be retrieved.

#### Update a media message

```
DEFINITION
POST http://apiserver/mediamessages/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediamessages/32", {
    "date": "2015-05-01"
});

EXAMPLE RESPONSE
{
    "id": "32",
    "messageCode": "M1234",
    "description": "What Would Jesus Do?",
    "comment": null,
    "date": "2015-05-01"
}


```

Updates the specified media message by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* messageCode (optional) - The message code for the message. Must be unique.
* description (optional) - The description of the media message.
* comment (optional) - The long comment for the message.
* date (optional) - The message date.

##### Returns

Returns the media message object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media message

```
DEFINITION
DELETE http://apiserver/mediamessages/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediamessages/32", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media message. It cannot be undone.

##### Arguments

* id (required) - The id of the media message to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media message does not exist, this call returns an error.

#### List all media messages

```
DEFINITION
GET http://apiserver/mediamessages

EXAMPLE REQUEST
$.get("http://localhost:49195/mediamessages?description=*Jesus*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "32",
            "messageCode": "M1234",
            "description": "What Would Jesus Do?",
            "comment": null,
            "date": "2015-05-01"
        },
        {...},
    ]
}

```

Returns a list of all media messages.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* messageCode (optional) - The message code (id) to search with.
* description (optional) - The description of the media message.

##### Returns

A dictionary with an items property that contains an array of up to limit media messages, starting at index offset. Each entry in the array is a separate media message object. If no more media messages are available, the resulting array will be empty. This request should never return an error.

### Media Network Attachments

#### Create a media network attachment

```
DEFINITION
POST http://apiserver/medianetworks/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "6",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new media network attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a media network attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve a media network attachment

```
DEFINITION
GET http://apiserver/medianetworks/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/attachments/6");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "6",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing media network attachment. You need only supply the media network attachment id.

##### Arguments

* id (required) - The id of the media network attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a media network attachment object if a valid id was provided.

#### Update a media network attachment

```
DEFINITION
POST http://apiserver/medianetworks/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/attachments/6", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "6",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified media network attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the media network attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined media network attachment type code).

#### Delete a media network attachment

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/32/attachments/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the media network attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media network attachment id does not exist, this call returns an error.

#### List all media network attachments

```
DEFINITION
GET http://apiserver/medianetworks/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "6",
            "type": "OTHER",
            "typeDescription": "Other",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media network attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit media network attachments, starting at index offset. Each entry in the array is a separate media network attachment object. If no more media network attachments are available, the resulting array will be empty. This request should never return an error.

### Media Network Codes

#### Create a media network code

```
DEFINITION
POST http://apiserver/medianetworks/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/codes", {
    "type": "NETTYPE",
    "value": "RELIGIOUS",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "NETTYPE",
    "typeDescription": null,
    "value": "RELIGIOUS",
    "valueDescription": "Religious",
    "isActive": true
}

```

Creates a new media network code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a media network code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a media network code

```
DEFINITION
GET http://apiserver/medianetworks/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/codes/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "NETTYPE",
    "typeDescription": "Network Type",
    "value": "RELIGIOUS",
    "valueDescription": "Religious",
    "isActive": true
}

```

Retrieves the details of an existing media network code. You need only supply the media network id and media network code id.

##### Returns

Returns a media network code object if a valid id was provided.

#### Update a media network code

```
DEFINITION
POST http://apiserver/medianetworks/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/codes/7", {
    "value": "SECULAR"
});

EXAMPLE RESPONSE
{
    "id": "7",
    "type": "NETTYPE",
    "typeDescription": "Network Type",
    "value": "SECULAR",
    "valueDescription": "Secular",
    "isActive": true
}

```

Updates the specified media network code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the media network code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a media network code

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/32/codes/7", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network code. It cannot be undone.

##### Arguments

* id (required) - The id of the media network code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media network code id does not exist, this call returns an error.

#### List all media network codes

```
DEFINITION
GET http://apiserver/medianetworks/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "type": "NETTYPE",
            "typeDescription": "Network Type",
            "value": "SECULAR",
            "valueDescription": "Secular",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media network codes.

##### Returns

A dictionary with an items property that contains an array of up to limit media network codes, starting at index offset. Each entry in the array is a separate media network code object. If no more media network codes are available, the resulting array will be empty. This request should never return an error.

### Media Network Contracts

#### Create a media network contract

```
DEFINITION
POST http://apiserver/medianetworks/:id/contracts

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/3/contracts", {
    "type": "N",
    "startDate": "2011-03-30",
    "endDate": "2011-04-01",
    "isActive": true,
    "referenceNumber": "123456",
    "comment": "comment"
});

EXAMPLE RESPONSE
{
    "network": "ACN",
    "type": "N",
    "id": "24",
    "contractId": "1000000013",
    "startDate": "2011-03-30",
    "endDate": "2011-04-01",
    "isActive": true,
    "referenceNumber": "123456",
    "comment": "comment"
}

```

Creates a new media network contract.

##### Arguments

* type (required) - The type of contract, can be "N" for network only, or "O" for outlets.
* startDate (required) - The start date of the contract.
* endDate (optional) - The end date of the contract.
* isActive (optional : default true) - Indicates whether the contract is active.
* referenceNumber (optional) - The reference number for the contract.
* comment (optional) - A long text field for comments.

##### Returns

Returns a media network contract object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media network contract

```
DEFINITION
GET http://apiserver/medianetworks/:id/contracts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/3/contracts/24");

EXAMPLE RESPONSE
{
    "network": "ACN",
    "type": "N",
    "id": "24",
    "contractId": "1000000013",
    "startDate": "2011-03-30",
    "endDate": "2011-04-01",
    "isActive": true,
    "referenceNumber": "123456",
    "comment": "comment"
}

```

Retrieves the details of an existing media network contract. You need only supply the id.

##### Arguments

* id (required) - The id of the media network contract to be retrieved.

#### Update a media network contract

```
DEFINITION
POST http://apiserver/medianetworks/:id/contracts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/3/contracts/24", {
    "comment": "Document number 123"
});

EXAMPLE RESPONSE
{
    "network": "ACN",
    "type": "N",
    "id": "24",
    "contractId": "1000000013",
    "startDate": "2011-03-30",
    "endDate": "2011-04-01",
    "isActive": true,
    "referenceNumber": "123456",
    "comment": "Document number 123"
}


```

Updates the specified media network contract by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of contract, can be "N" for network only, or "O" for outlets.
* startDate (optional) - The start date of the contract.
* endDate (optional) - The end date of the contract.
* isActive (optional) - Indicates whether the contract is active.
* referenceNumber (optional) - The reference number for the contract.
* comment (optional) - A long text field for comments.

##### Returns

Returns the media network contract object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media network contract

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/contracts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/3/contracts/24", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network contract. It cannot be undone.

##### Arguments

* id (required) - The id of the media network contract to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media network contract does not exist, this call returns an error.

#### List all media network contracts

```
DEFINITION
GET http://apiserver/medianetworks/:id/contracts

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/3/contracts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "network": "ACN",
            "type": "N",
            "id": "24",
            "contractId": "1000000013",
            "startDate": "2011-03-30",
            "endDate": "2011-04-01",
            "isActive": true,
            "referenceNumber": "123456",
            "comment": "Document number 123"
        },
        {...},
    ]
}

```

Returns a list of all media network contracts.

##### Returns

A dictionary with an items property that contains an array of up to limit media network contracts, starting at index offset. Each entry in the array is a separate media network contract object. If no more media network contracts are available, the resulting array will be empty. This request should never return an error.

#### Copy a media network contract

```
DEFINITION
POST http://apiserver/medianetworks/:id/contracts/:id/copy

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/3/contracts/23/copy");

EXAMPLE RESPONSE
204 No Content

```

Copies the specified contract to dependent outlets.

##### Returns

Returns a `204 No Content` response on success. If the media network contract does not exist or is not the correct type, this call returns an error.
Contracts must be type outlet ("O") in order to be copied.

### Media Network Cost Total

#### Retrieve a media network cost total

```
DEFINITION
GET http://apiserver/medianetworks/:id/costtotal?:arguments

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/costtotal?transactiondate=2010-07-30&starttime=03:00:00 am&endtime=12:59:00 pm");

EXAMPLE RESPONSE
{
    "amount": 300
}

```

Determines the total amount for a given transaction date, start time, and end time. This resource is intended to be used with Media Network Costs.

##### Arguments

* transactionDate (required) - The transaction date to be used for calculating the total.
* startTime (required) - The start time to be used for calculating the total.
* endTime (required) - The end time to be used for calculating the total.

### Media Network Costs

#### Create a media network cost

```
DEFINITION
POST http://apiserver/medianetworks/:id/costs

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/costs", {
    "transactionDate": "2010-07-30",
    "totalAmount": 300.00,
    "comment": "Advertising"
});

EXAMPLE RESPONSE
{
    "id": "22",
    "transactionDate": "2010-07-30",
    "totalAmount": 300,
    "comment": "Advertising",
    "isCostAdjustment": false
}

```

Creates a new media network cost.

##### Arguments

* comment (required) - The comment for the cost.
* transactionDate (optional) - The date for the cost.
* totalAmount (optional) - The amount of the cost.
* isCostAdjustment (optional : defaults to false) - Indicates whether the cost is a cost adjustment.

##### Returns

Returns a media network cost object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media network cost

```
DEFINITION
GET http://apiserver/medianetworks/:id/costs/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/costs/22");

EXAMPLE RESPONSE
{
    "id": "22",
    "transactionDate": "2010-07-30",
    "totalAmount": 300,
    "comment": "Advertising",
    "isCostAdjustment": false
}

```

Retrieves the details of an existing media network cost. You need only supply the id.

##### Arguments

* id (required) - The id of the media network cost to be retrieved.

#### Update a media network cost

```
DEFINITION
POST http://apiserver/medianetworks/:id/costs/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/costs/22", {
    "totalAmount": 500
});

EXAMPLE RESPONSE
{
    "id": "22",
    "transactionDate": "2010-07-30",
    "totalAmount": 500,
    "comment": "Advertising",
    "isCostAdjustment": false
}


```

Updates the specified media network cost by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* comment (optional) - The comment for the cost.
* transactionDate (optional) - The date for the cost.
* totalAmount (optional) - The amount of the cost.
* isCostAdjustment (optional) - Indicates whether the cost is a cost adjustment.

##### Returns

Returns the media network cost object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media network cost

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/costs/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/32/costs/22", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network cost. It cannot be undone.

##### Arguments

* id (required) - The id of the media network cost to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media network cost does not exist, this call returns an error.

#### List all media network costs

```
DEFINITION
GET http://apiserver/medianetworks/:id/costs

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/costs");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "22",
            "transactionDate": "2010-07-30",
            "totalAmount": 500,
            "comment": "Advertising",
            "isCostAdjustment": false
        },
        {...},
    ]
}

```

Returns a list of all media network costs.

##### Returns

A dictionary with an items property that contains an array of up to limit media network costs, starting at index offset. Each entry in the array is a separate media network cost object. If no more media network costs are available, the resulting array will be empty. This request should never return an error.

### Media Network Dates

#### Create a media network date

```
DEFINITION
POST http://apiserver/medianetworks/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/dates", {
    "type": "MSGDATE1",
    "value": "2015-07-01",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "NTWKINC",
    "typeDescription": null,
    "value": "2015-07-30",
    "isActive": true
}

```

Creates a new media network date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a media network date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a media network date

```
DEFINITION
GET http://apiserver/medianetworks/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/dates/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "NTWKINC",
    "typeDescription": "Network Inception Date",
    "value": "2015-07-30",
    "isActive": true
}

```

Retrieves the details of an existing media network date. You need only supply the media network id and media network date id.

##### Returns

Returns a media network date object if a valid id was provided.

#### Update a media network date

```
DEFINITION
POST http://apiserver/medianetworks/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/dates/3", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "NTWKINC",
    "typeDescription": "Network Inception Date",
    "value": "2015-07-30",
    "isActive": false
}

```

Updates the specified media network date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the media network date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a media network date

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/32/dates/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network date. It cannot be undone.

##### Arguments

* id (required) - The id of the media network date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media network date id does not exist, this call returns an error.

#### List all media network dates

```
DEFINITION
GET http://apiserver/medianetworks/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "type": "NTWKINC",
            "typeDescription": "Network Inception Date",
            "value": "2015-07-30",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media network dates.

##### Returns

A dictionary with an items property that contains an array of up to limit media network dates, starting at index offset. Each entry in the array is a separate media network date object. If no more media network dates are available, the resulting array will be empty. This request should never return an error.

### Media Network Notes

#### Create a media network note

```
DEFINITION
POST http://apiserver/medianetworks/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/notes", {
    "type": "MSGNOTE1",
    "shortComment": "demo"
});

EXAMPLE RESPONSE
{
    "id": "2",
    "type": "NTWKNOTE",
    "typeDescription": null,
    "shortComment": "demo",
    "longComment": null
}

```

Creates a new media network note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a media network note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Retrieve a media network note

```
DEFINITION
GET http://apiserver/medianetworks/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/notes/2");

EXAMPLE RESPONSE
{
    "id": "2",
    "type": "NTWKNOTE",
    "typeDescription": "Network Note Type",
    "shortComment": "demo",
    "longComment": null
}

```

Retrieves the details of an existing media network note. You need only supply the media network id and media network note id.

##### Returns

Returns a media network note object if a valid id was provided.

#### Update a media network note

```
DEFINITION
POST http://apiserver/medianetworks/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/notes/2", {
    "longComment": "now we have a long comment"
});

EXAMPLE RESPONSE
{
    "id": "2",
    "type": "NTWKNOTE",
    "typeDescription": "Network Note Type",
    "shortComment": "demo",
    "longComment": "now we have a long comment"
}

```

Updates the specified media network note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the media network note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a media network note

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/32/notes/9", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network note. It cannot be undone.

##### Arguments

* id (required) - The id of the media network note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media network note id does not exist, this call returns an error.

#### List all media network notes

```
DEFINITION
GET http://apiserver/medianetworks/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "2",
            "type": "NTWKNOTE",
            "typeDescription": "Network Note Type",
            "shortComment": "demo",
            "longComment": "now we have a long comment"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media network notes.

##### Returns

A dictionary with an items property that contains an array of up to limit media network notes, starting at index offset. Each entry in the array is a separate media network note object. If no more media network notes are available, the resulting array will be empty. This request should never return an error.

### Media Network Numbers

#### Create a media network number

```
DEFINITION
POST http://apiserver/medianetworks/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/numbers", {
    "type": "MSGNUMB1",
    "value": 10
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCSTANBR",
    "typeDescription": null,
    "value": 55,
    "isActive": true
}

```

Creates a new media network number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a media network number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Retrieve a media network number

```
DEFINITION
GET http://apiserver/medianetworks/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/numbers/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCSTANBR",
    "typeDescription": "Station Numbers",
    "value": 55,
    "isActive": true
}

```

Retrieves the details of an existing media network number. You need only supply the media network id and media network number id.

##### Returns

Returns a media network number object if a valid id was provided.

#### Update a media network number

```
DEFINITION
POST http://apiserver/medianetworks/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/32/numbers/8", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCSTANBR",
    "typeDescription": "Station Numbers",
    "value": 55,
    "isActive": false
}

```

Updates the specified media network number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the media network number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a media network number

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/32/numbers/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network number. It cannot be undone.

##### Arguments

* id (required) - The id of the media network number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the media network number id does not exist, this call returns an error.

#### List all media network numbers

```
DEFINITION
GET http://apiserver/medianetworks/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/32/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "8",
            "type": "DDCSTANBR",
            "typeDescription": "Station Numbers",
            "value": 55,
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all media network numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit media network numbers, starting at index offset. Each entry in the array is a separate media network number object. If no more media network numbers are available, the resulting array will be empty. This request should never return an error.

### Media Network Placements

#### Create a media network placement

```
DEFINITION
POST http://apiserver/medianetworks/:id/contracts/:id/placements

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/3/contracts/16/placements", {
    "program": "AIO",
    "paymentType": "PD",
    "deliveryType": "FTP"
});

EXAMPLE RESPONSE
{
    "network": "ACN",
    "id": "17",
    "contract": 1000000005,
    "program": "AIO",
    "isActive": true,
    "startDate": null,
    "endDate": null,
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": false,
    "isSaturday": false,
    "leadInProgram": null,
    "leadOutProgram": null,
    "deliveryType": "FTP",
    "paymentType": "PD",
    "perShowAmount": null,
    "perShowPercent": null,
    "perShowMinimum": null,
    "perShowMaximum": null,
    "monthlyMinimum": null,
    "monthlyMaximum": null,
    "monthlyBase": null
}

```

Creates a new media network placement.

##### Arguments

* program (required) - The program code for the placement. Should be a valid "DDCPROGR" value.
* isActive (optional : default true) - Indicates whether the placement is active.
* startDate (optional) - The start date of the placement.
* endDate (optional) - The end date of the placement.
* isMonday (optional : default false) - Indicates whether the placement applies to Monday.
* isTuesday (optional : default false) - Indicates whether the placement applies to Tuesday.
* isWednesday (optional : default false) - Indicates whether the placement applies to Wednesday.
* isThursday (optional : default false) - Indicates whether the placement applies to Thursday.
* isFriday (optional : default false) - Indicates whether the placement applies to Friday.
* isSaturday (optional : default false) - Indicates whether the placement applies to Saturday.
* isSunday (optional : default false) - Indicates whether the placement applies to Sunday.
* leadInProgram (optional) - The lead in program for the placement.
* leadOutProgram (optional) - The lead out program for the placement.
* paymentType (required) - The payment type for the placement. Should be a valid "DDCMPTP" value.
* deliveryType (required) - The delivery type for the placement. Should be a valid "DDCDELIV" value.
* perShowAmount (optional) - The amount per show for the placement.
* perShowPercent (optional) - The percent per show for the placement.
* perShowMinimum (optional) - The minimum per show for the placement.
* perShowMaximum (optional) - The maximum per show for the placement.
* monthlyMinimum (optional) - The monthly minimum for the placement.
* monthlyMaximum (optional) - The monthly maximum for the placement.
* monthlyBase (optional) - The monthly base for the placement.

##### Returns

Returns a media network placement object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media network placement

```
DEFINITION
GET http://apiserver/medianetworks/:id/contracts/:id/placements/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/3/contracts/16/placements/17");

EXAMPLE RESPONSE
{
    "network": "ACN",
    "id": "17",
    "contract": 1000000005,
    "program": "AIO",
    "isActive": true,
    "startDate": null,
    "endDate": null,
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": false,
    "isSaturday": false,
    "leadInProgram": null,
    "leadOutProgram": null,
    "deliveryType": "FTP",
    "paymentType": "PD",
    "perShowAmount": null,
    "perShowPercent": null,
    "perShowMinimum": null,
    "perShowMaximum": null,
    "monthlyMinimum": null,
    "monthlyMaximum": null,
    "monthlyBase": null
}

```

Retrieves the details of an existing media network placement. You need only supply the id.

##### Arguments

* id (required) - The id of the media network placement to be retrieved.

#### Update a media network placement

```
DEFINITION
POST http://apiserver/medianetworks/:id/contracts/:id/placements/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/3/contracts/16/placements/17", {
    "isMonday": true
});

EXAMPLE RESPONSE
{
    "network": "ACN",
    "id": "17",
    "contract": 1000000005,
    "program": "AIO",
    "isActive": true,
    "startDate": null,
    "endDate": null,
    "isSunday": false,
    "isMonday": true,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": false,
    "isSaturday": false,
    "leadInProgram": null,
    "leadOutProgram": null,
    "deliveryType": "FTP",
    "paymentType": "PD",
    "perShowAmount": null,
    "perShowPercent": null,
    "perShowMinimum": null,
    "perShowMaximum": null,
    "monthlyMinimum": null,
    "monthlyMaximum": null,
    "monthlyBase": null
}


```

Updates the specified media network placement by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* program (optional) - The program code for the placement. Should be a valid "DDCPROGR" value.
* isActive (optional) - Indicates whether the placement is active.
* startDate (optional) - The start date of the placement.
* endDate (optional) - The end date of the placement.
* isMonday (optional) - Indicates whether the placement applies to Monday.
* isTuesday (optional) - Indicates whether the placement applies to Tuesday.
* isWednesday (optional) - Indicates whether the placement applies to Wednesday.
* isThursday (optional) - Indicates whether the placement applies to Thursday.
* isFriday (optional) - Indicates whether the placement applies to Friday.
* isSaturday (optional) - Indicates whether the placement applies to Saturday.
* isSunday (optional) - Indicates whether the placement applies to Sunday.
* leadInProgram (optional) - The lead in program for the placement.
* leadOutProgram (optional) - The lead out program for the placement.
* paymentType (optional) - The payment type for the placement. Should be a valid "DDCMPTP" value.
* deliveryType (optional) - The delivery type for the placement. Should be a valid "DDCDELIV" value.
* perShowAmount (optional) - The amount per show for the placement.
* perShowPercent (optional) - The percent per show for the placement.
* perShowMinimum (optional) - The minimum per show for the placement.
* perShowMaximum (optional) - The maximum per show for the placement.
* monthlyMinimum (optional) - The monthly minimum for the placement.
* monthlyMaximum (optional) - The monthly maximum for the placement.
* monthlyBase (optional) - The monthly base for the placement.

##### Returns

Returns the media network placement object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media network placement

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/contracts/:id/placements/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/3/contracts/16/placements/17", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network placement. It cannot be undone.

##### Arguments

* id (required) - The id of the media network placement to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media network placement does not exist, this call returns an error.

#### List all media network placements

```
DEFINITION
GET http://apiserver/medianetworks/:id/contracts/:id/placements

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/3/contracts/16/placements");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "network": "ACN",
            "id": "14",
            "contract": 1000000005,
            "program": "AIO",
            "isActive": true,
            "startDate": "2011-03-30",
            "endDate": "2011-04-01",
            "isSunday": false,
            "isMonday": false,
            "isTuesday": false,
            "isWednesday": false,
            "isThursday": false,
            "isFriday": false,
            "isSaturday": false,
            "leadInProgram": null,
            "leadOutProgram": null,
            "deliveryType": "FTP",
            "paymentType": "PD",
            "perShowAmount": null,
            "perShowPercent": null,
            "perShowMinimum": null,
            "perShowMaximum": null,
            "monthlyMinimum": null,
            "monthlyMaximum": null,
            "monthlyBase": null
        },
        {...},
    ]
}

```

Returns a list of all media network placements.

##### Returns

A dictionary with an items property that contains an array of up to limit media network placements, starting at index offset. Each entry in the array is a separate media network placement object. If no more media network placements are available, the resulting array will be empty. This request should never return an error.

### Media Network Placement Times

#### Create a media network placement time

```
DEFINITION
POST http://apiserver/medianetworks/:id/contracts/:id/placements/:id/times

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/3/contracts/16/placements/14/times", {
    "time": "01:00:00 PM",
    "timeZone": "CT",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "1",
    "time": "01:00:00 PM",
    "timeZone": "CT",
    "timeZoneDescription": "Central Time",
    "isActive": true
}

```

Creates a new media network placement time.

##### Arguments

* time (required) - The time of the show.
* timeZone (optional) - The time zone for this time, must be a valid DDCTIMEZON code.
* isActive (optional) - Indicates whether the placement time is active.

##### Returns

Returns a media network placement time object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media network placement time

```
DEFINITION
GET http://apiserver/medianetworks/:id/contracts/:id/placements/:id/times/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/3/contracts/16/placements/14/times/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "time": "01:00:00 PM",
    "timeZone": "CT",
    "timeZoneDescription": "Central Time",
    "isActive": true
}

```

Retrieves the details of an existing media network placement time. You need only supply the id.

##### Arguments

* id (required) - The id of the media network placement time to be retrieved.

#### Update a media network placement time

```
DEFINITION
POST http://apiserver/medianetworks/:id/contracts/:id/placements/:id/times/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/3/contracts/16/placements/14/times/1", {
    "time": "02:00:00 PM"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "time": "02:00:00 PM",
    "timeZone": "CT",
    "timeZoneDescription": "Central Time",
    "isActive": true
}


```

Updates the specified media network placement time by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* time (optional) - The time of the show.
* timeZone (optional) - The time zone for this time, must be a valid DDCTIMEZON code.
* isActive (optional) - Indicates whether the placement time is active.

##### Returns

Returns the media network placement time object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media network placement time

```
DEFINITION
DELETE http://apiserver/medianetworks/:id/contracts/:id/placements/:id/times/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/3/contracts/16/placements/14/times/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network placement time. It cannot be undone.

##### Arguments

* id (required) - The id of the media network placement time to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media network placement time does not exist, this call returns an error.

#### List all media network placement times

```
DEFINITION
GET http://apiserver/medianetworks/:id/contracts/:id/placements/:id/times

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/3/contracts/16/placements/14/times");

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
            "time": "02:00:00 PM",
            "timeZone": "CT",
            "timeZoneDescription": "Central Time",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all media network placement times.

##### Returns

A dictionary with an items property that contains an array of up to limit media network placement times, starting at index offset. Each entry in the array is a separate media network placement time object. If no more media network placement times are available, the resulting array will be empty. This request should never return an error.

### Media Networks

#### Create a media network

```
DEFINITION
POST http://apiserver/medianetworks

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks", {
    "network": {
        "networkId": "EXP",
        "description": "The best example network around",
        "website": "example.com"
    },
    "mailingAddress": {
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "state": "TX",
        "postalCode": "75080",
        "country": "USA"
    },
    "billingAddress": null,
    "shippingAddress": null
});

EXAMPLE RESPONSE
{
    "id": "28",
    "network": {
        "id": "28",
        "networkId": "EXP",
        "description": "The best example network around",
        "accountNumber": 27575,
        "website": "example.com"
    },
    "phone": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": null,
        "isActive": null,
        "functionalCategory": null
    },
    "fax": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": null,
        "isActive": null,
        "functionalCategory": null
    },
    "mailingAddress": {
        "id": "1000027529",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000027530",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000027531",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "formattedPhone": null,
    "formattedFax": null
}

```

Creates a new media network.

##### Arguments

* network (required) - The network information of the media network. networkId is required. description, and website are optional.
* mailingAddress (required) - The mailing address of the media network. country is required. postalCode and state must be valid for the country and postalCode is required for some countries. city, line1, line2, line3, and line4 are optional.
* billingAddress (required) - The billing address of the media network. Set to null to use the mailingAddress for billingAddress as well.
* shippingAddress (required) - The shipping address of the media network. Set to null to use the mailingAddress for shippingAddress as well.
* phone (optional) - The phone number of the media network. Ignored unless type, areaCode, and phoneNumber are provided. extension and internationalCode are optional.
* fax (optional) - The fax number of the media network. Ignored unless areaCode, and phoneNumber are provided. extension and internationalCode are optional.

##### Returns

Returns a media network object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media network

```
DEFINITION
GET http://apiserver/medianetworks/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks/28");

EXAMPLE RESPONSE
{
    "id": "28",
    "network": {
        "id": "28",
        "networkId": "EXP",
        "description": "The best example network around",
        "accountNumber": 27575,
        "website": "example.com"
    },
    "phone": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": null,
        "isActive": null,
        "functionalCategory": null
    },
    "fax": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": null,
        "isActive": null,
        "functionalCategory": null
    },
    "mailingAddress": {
        "id": "1000027529",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000027530",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000027531",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "formattedPhone": null,
    "formattedFax": null
}

```

Retrieves the details of an existing media network. You need only supply the id.

##### Arguments

* id (required) - The id of the media network to be retrieved.

#### Update a media network

```
DEFINITION
POST http://apiserver/medianetworks/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/medianetworks/28", {
    "phone": {
        "type": "HOME",
        "areaCode": "555",
        "phoneNumber": "555-5555"
    }
});

EXAMPLE RESPONSE
{
    "id": "28",
    "network": {
        "id": "28",
        "networkId": "EXP",
        "description": "The best example network around",
        "accountNumber": 27575,
        "website": "example.com"
    },
    "phone": {
        "id": "44647",
        "type": "HOME",
        "internationalCode": null,
        "areaCode": "555",
        "phoneNumber": "555-5555",
        "extension": null,
        "isPrimary": true,
        "isActive": true,
        "functionalCategory": null
    },
    "fax": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": null,
        "isActive": null,
        "functionalCategory": null
    },
    "mailingAddress": {
        "id": "1000027529",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000027530",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000027531",
        "line1": "1234 Mailing Address",
        "line2": "Apt ####",
        "line3": null,
        "line4": null,
        "city": null,
        "state": "TX",
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "formattedPhone": "(555) 555-5555",
    "formattedFax": null
}


```

Updates the specified media network by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* network (optional) - The network information of the media network. networkId is required. description, and website are optional.
* phone (optional) - The phone number of the media network. When adding a new phone, it will be ignored unless type, areaCode, and phoneNumber are provided.
* fax (optional) - The fax number of the media network. When adding a new fax, it will be ignored unless areaCode, and phoneNumber are provided.
* mailingAddress (optional) - The mailing address of the media network. country is required. postalCode and state must be valid for the country and postalCode is required for some countries.
* billingAddress (optional) - The billing address of the media network.
* shippingAddress (optional) - The shipping address of the media network.

##### Returns

Returns the media network object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media network

```
DEFINITION
DELETE http://apiserver/medianetworks/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/medianetworks/27", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media network. It cannot be undone.

##### Arguments

* id (required) - The id of the media network to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media network does not exist, this call returns an error.

#### List all media networks

```
DEFINITION
GET http://apiserver/medianetworks

EXAMPLE REQUEST
$.get("http://localhost:49195/medianetworks?description=*the best*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "28",
            "networkId": "EXP",
            "description": "The best example network around",
            "accountNumber": 27575,
            "website": "example.com"
        },
        {...},
    ]
}

```

Returns a list of all media networks.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* networkId (optional) - The networkId. Supports wildcards.
* description (optional) - The description of the network. Supports wildcards.
* website (optional) - The website of the network. Supports wildcards.
* accountNumber (optional) - The account number of the network.

##### Returns

A dictionary with an items property that contains an array of up to limit media networks, starting at index offset. Each entry in the array is a separate media network object. If no more media networks are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Airings

#### List all media outlet airings

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/airings

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/airings?startDate=2010-07-01");

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
            "program": "AIO",
            "show": "MYSHOW3",
            "description": "Mine, all mine",
            "airingDate": "2010-07-21",
            "airingTime": "03:00:00 PM",
            "source": "AIOF00915D"
        },
        {...},
    ]
}

```

Returns a list of all media outlet airings.

##### Arguments

* startDate (optional) - Beginning of the date range to filter airing date by.
* endDate (optional) - End of the date range to filter airing date by.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet airings, starting at index offset. Each entry in the array is a separate media outlet airing object. If no more media outlet airings are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Aliases

#### Create a media outlet alias

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/aliases

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/aliases", {
    "alias": "ASDF"
});

EXAMPLE RESPONSE
{
    "id": "24",
    "alias": "ASDF"
}

```

Creates a new media outlet alias.

##### Arguments

* alias (required) - The alias to add to the outlet.

##### Returns

Returns a media outlet alias object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet alias

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/aliases/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/aliases/24");

EXAMPLE RESPONSE
{
    "id": "24",
    "alias": "ASDF"
}

```

Retrieves the details of an existing media outlet alias. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet alias to be retrieved.

#### Update a media outlet alias

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/aliases/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/aliases/24", {
    "alias": "JIMM"
});

EXAMPLE RESPONSE
{
    "id": "24",
    "alias": "JIMM"
}


```

Updates the specified media outlet alias by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* alias (optional) - The alias value for the outlet.

##### Returns

Returns the media outlet alias object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet alias

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/aliases/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/aliases/23", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet alias. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet alias to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet alias does not exist, this call returns an error.

#### List all media outlet aliases

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/aliases

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/aliases");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "24",
            "alias": "JIMM"
        },
        {...},
    ]
}

```

Returns a list of all media outlet aliases.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet aliases, starting at index offset. Each entry in the array is a separate media outlet alias object. If no more media outlet aliases are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Attachments

#### Create a media outlet attachment

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAD1ZJREFUeNrMW8uLZkcVr1P39owihPaFy8zSZbvwBUanQdGdihsXgpO1SJiNghJnxiwCgowu4irgzEJwl/wBkR7BTQhKL9WFtAsXimCTlTPfrTrWeVWduo/uL5Nkxg+q697v3u/eOr8673MawuzzoVe+clima2Wc62yf85XvznTu7vvbX8/p+6Owxwdi+TPoHKGMcgyB5wBB/oD7AdqMckxTLnOmuZwkPcbV15194pdvnXXvd4TTgu+Wcb2MB2X8voxb7t617+7o3N1XAKDvTy4lHpT4QYgXEHRVdA5L+o12JpzmjA4EDGgApM3XEgA3CxCvB32dEX+ixD+RT0f8ADrTeTkeIUS9FvW8jnoe5J5y3H4v1+tz1z/Era/984VPf6MCoDt/+NSIj23xc6JDIZQG6MzHDii53z+HxElFKV64jF/Tn1Flfq+dh5Xv8HEQWCVeFm5iACoKJgZ0ACrY6GQfQGQkQmF//gHymsrdgb/BTX1wWLjg+niZsqIHm2hGlUdwhKvo6QyXAgLuYQviByV+MEXY9EDdAgyNKDqgr0CBUNLpItp99Mxpez3j5oXyaxKnUbiJjyP0nIAd8UUBl7dOeAkLxeVOV+LVGoBxhu38DHUmrryQiMYGwp2P/PjN2++UGRcADOWBRPQV0S1BdQwTP7Q1VbZKlXgZ0yWyXwlzQHRgeLGoYgAOAEVciZdrfOHWf17+3C0si8CJrIBahElmXF/Y8eg3h3b9oLz0oJxcjUL8qIRHBWKLA5h4Hdvy1Ij3IFS2V6KrJo+eE/SFKN8RgQwCS75j+0zPo2NgLkF6PnPLui4YjaCDQvyVKDtPMwFgHFC5wMwGNFb0HHARAJWNTa7rrDtv3KHExwF6gLz/k5uPJBuBAgwTLEBBFt1gihRhXWOPkS0NMsFE+AdmHHDgRQDci3GFA/IFIuCVWafdGzABmk4IJg6D6oFoLBdU06ue5+8ITOTfNMuAFYDu3XMArpjMK/FXFYAPGgcoEBeKgHEAXCwCEPoFmWxDBaQHwcRCuEVR55etsXy4V4C4D2oGqwIlkJqemH9OR5b50Ii/6sTAiKdZAMCFGUwFZgNgKOgPeAkHwDoYDQhwekKIN3GoW0rbzLtNnIHiBodwo1y6MX+m57qwFIPj8Yqy+YFq/qtC/OHVITxL7z2I1SQeDjE8G/rnPJsL9Mb+sSx4yHs4UwDr5x6M0HSDiQOzNyrBJttOyYhKbOj252v0swgIkVfcKOdHZdePWDyUE8r7j8pmHAF0CulG3X3apHIyAexhfbGuSvwZrE5OHaGfmWhl+xoFziIkfAz3dBydsjtQdmdAyCQOTQSIC2J0VsApQRKDSTUzIF5OuidwTqxqdETnZgZxg9kCpBYGc/Q3fwZuALLhEo9j6Ikfje3teBDilQvEG/RmkFgfTTeALFryBg8WlGPvzYXQ3FqQ747K7w9BtTlfTCLzwgFKSEJ3XgG5V47v4/xdGDaDAVaCg2r3avNjI9iODZChKJxoGlsVMsl9zB2Nhy8898zhwxTuPCxK6r/FUaCxw3D61o03zi/ijrd/8fmT8vDrRKC8Qr2X6B0hAYeSHzJrIiSHGySSlgxBdCKzLRbHHQDRHQsgDYiDot4HxwXMgWT3s1lkeh8WSwRH5fJJdMpc13+84IoV+WBizByqnWdtbwrPJUCqu4vy7rDkisb6G0wwRmiRnhxjO1aCaeeHaKKBFYBUNSJyJJiimMH6ezeGPRQTVjDRBT1q6rpskO5+alkgHjU1NgNkO0XGXB/izPRCBaPnCiJ+HORY5FZ87uwIJUckskly4TPsp5EljeVAMCcnL3VJef9ZIf6sigO6vGB2RHtuWH7Oxzh3Smbhd/CAKBAkDjmLAwTVgZGFw0ryhMGI+wJgixb31mx+F80IQffv/PY7r7/LTNbZiDMLBCvpnplIseznMAf24mQI7mObcxNhyOhYMjTB6JXb3XeZxzweK5dgizU6zjGOyiLztJAMQizZfosFsj4j49L65D0BMBtPco81sMHqI1VF+di5uBUdkB3Rnggf5MSyoClYTN00Ml2f0gyIAO0Zjvi8nw64X268TnLPQHDSIyz9WHzvAIieUPPqUs3wADs6ic0dhF0h9pGOnY6Jr4snyM/ILTvkn7sPAB+98+a9sut3cgrnnNWhbA5ndCzL03/ngr423ikHTCpqyaW1mGgI6t6CpRzY1JmmD3qeLQ+gIFlSxMDLel7m030W9LGfcl7v9r9/8tnrCN6CYO8vFAU2DPAlgGW+Gi17nGXlF4nfaHk8WziHtOzdoTMMwA9N0UwbhDDPBSgX1OEyROX03h+fv9gLXAHiwWX3/OiLz7fkSqdsQfVa8xYzrgPBHACq0CYxu+zaclyesSoxAmVAM3chNKdMdnpSTtjxAJ7Ld2fluwfl8Ob7UWAZime25mNU4imoYpcZRbFmMt/YqY/xkZ4NSnj0GZ8oxodMRYqWEgPvlvPLfvOt30F4Cp9hdABAi9B8HJArAMj6iZKYOTduGHfqaDBr52UhlrR6YlcWq3cYZimxp/XhWL4WRebyj9WfMACAgizi4MKyOSGvfdypXeXdjxqrO4ckaUTKesFpWu8rPK3PsAKAgbAEIMvaE/0kytYWOseHWVxun+hEDeuJ8FEBqL7+zCbnpwwAzCpHGJzyQ2wApODSynQUubBSlKAWF7JzdRWAyaXFB+hrg/83IhChqxFYaJwNAGJ1Io4Ti1mLD7nSOlpm92HQHykAxPoU/u60Qj0HAJ0leGoccOA4YGYBSKQzV4QKqxcNDkFBINYosT1ibgD49HZWe0+7T/rBKkOmAGdJ0fdVBO587dXbhc2/Hod4VJyeUOYwlEFp8qjpcgMAND4JKv+0mSz3TLyvZSvxg0AyzoO/R+zBIQMwrw0+SQ64/dVXb0OEW1QgEWKFeAaCOkiKxo56zUBApwBZ6+eoXmuW9JoRT+Zdg4zV8rhxw46UROjLYnMdQOOTL/3hEChlHqCW0FsYjeow4elfXnxub2+wPO+7TCBAJTQq8cIFBQwDIMLCAiQ1e0w86zkhHvR+oKAOL+gPEDQhPLI+BGgRP9ScvtToPh6B6gUn7CRBl79kk0JiRSAUoO5Rg9KfX/zC+SW7XwCFa7yz0QEQbeeFExgIIwi8AlT7XVk+tJ3XkbWeOO6VqnI+9lrTDGvj4MpaoaYKxeBkiSUKEDeyKI3nL9l9KcC4He6AMOI9CIpAdjtvLB+N6Oh1hjx/fC/kldjRHJJFYIJSsjabHAH360eCZt7agntQBqcXQDO1uSA81WxyZhHKs2dI18k74IBLAZhxAIDP3NhikB2PMq7tQ3yrEYJbMLikreoH4oJRuIABT+TVZtnt2nugv7XYFloilACgOP34XbW9DbEvb0Or9pitBDAA9jCc0APRJ1ihAzoqGMQJOaPKtsVG0LLSviTvhHkc/v5D2pFby14hCFfKQw8GmW1Etcdsg4lwMRGH4OSrS1ywCGh2N4VLm/f6ZCwuiqCS4EDn9orvQjF5DYOrznLHs/oguhaZ1T5BYzEyNTZibWxyg+VPbbJzSoLKYVatnAFb78o+9NcKMKoYYUveOm2fVOFlpwMo0lu7X+FwlaINHWBFjSEqe+kwswRaNoIBqkmqjomypKWikhKfyiJTCGGvrJ3tYmi7VvVIxprY4ExMsEStWQEDIatIzMCoZXb5blxvjrTdBHcsqETwHNBM0aBaOTq3VHzy4lWm5oomjPvQf1rGcVsoajEW7xZLcpQq8eLb59hEDxUA4oxEYuEAwwUYWxywUtszGbekAOhum3iMQ+OEWj4nFoXa2SRltHL6mVf+dIK0uCnzInOZH5X5oc6/KvPDhKFPXoWbL/3jX+eZgxuN6dW5geiyVBoKJxUFen5KDQQeMw7orIB4zM1sGAeEbufZ87trjonsfnNOTNNWNkX1vKIkW8vpdfSt8OC1e29J3OeQd34K6t4Gfqc9t/VRitdZRYDC4Zw7bkDHDdYrfLJhiTZrfcGJiPfUzDOrqSkUD4zByqAVZdCihwwhHl05HVYLbZnBjLLTQ66y762PxQJLEHBxTrWFeFFHF/i+vtl1HxFCpyDFMYoKhPX6ds1asNI6t4W2D9KMpac2CiHHaUphKsfTrsw7ZvmbieYJ231Tvkm/n4MQL2xWwFk9LmydN2XFSojZLavywi53OO9YwbDWJ7RRO51UuysIROz373/7ARNdxjTZ9+lUZF/kn+6fJjxl6zDjhHGL+Owdj+p8YLWnoAhZpBdVwUBoCiYvtG9r17Bjan7KAV1xFjeTrSzHTqQsDE5T7vqW0LvfubE/F3csI6yKcdUVzm5LEGv7k2SP5cJR2em7OYZqdxPxPjsgkm0N5gQlic1TtjxdqA1O6Cq9nYdnYK0BoEoPY1O2tPPzThMMPQCmBI144dKwVILVvaSbo3aBZmmRCfpAjrXBPLzCXik2zRybgmDE9eUCgLCepa2sjJxnFekNX/EayTS51VTlyeqTVA6YO1HKAeYI0T38OtMDVhdYd0SMtZH/CULcWWAQpIlJ082gO888U/wAckpyqC2c9pyUsBcHJd4qNPYu/94VEbhGOgDNHScQHAeAzwhZHJCby5wnBSI1K7GZEmsNkFIRSjoozESQ6gmqJ5aDmib1yCL0ANQFqNlh5WiurHNMmFOwccOqFZg0pUUb4EQg7dLiP0q60hiGyvKL2uA2ACo7AOzNJe4Xlq5r+j8i7l/SrEtCtcnZkg/QRWWy6+qIpDayEj1lAzlUTlj7FE1elB/WZAasiEAfP/RcsPUPE6v5gOwWk2teD6V5o/jj1J8jD2ye3rxI0TUrGvurCSJAOPusI5myyrhpDbM2R0L/rzLF7KGvjfZ6AC/pD9Bw+GTJBSgNEjV8JQ+MdjoWvz9zVpU7uTDq//xIWxvCWkvbzAV1xO+SByJLbL9PftLdl1Je+jD7ZrPe/tmXz0L7H+BZerztEC2OorpdmXepNydZAxobrY3FXUtt8HP0WclxQMqPV2zt4/69n3H28ze/98B0ADUwvLYKgjo3wmKi7VELDQPKkG5OTUHBzLGzNlat1zHBKCBOjgtozk+u1kxp+W8G82sKF7yuqerzNZabdNd3WXaNQlY/piR+t+22uaHZfHa6r1znkJd/b89qxCd8YsRT682nyu6fdlaggEBFi3vP/OCNo3n3Jao4UMEx+b4hVUKo/7paU9kzZSrVIdR2Ou8ZNj9jH5YtY6szdK7ETze++3AhvNvk/wkwAHX7faDFX68AAAAAAElFTkSuQmCC",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "5",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new media outlet attachment.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a media outlet attachment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet attachment

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/attachments/5");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "5",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing media outlet attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the media network attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a media network attachment object if a valid id was provided.

#### Update a media outlet attachment

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/attachments/5", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "5",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified media outlet attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the media outlet attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet attachment

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/attachments/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet attachment does not exist, this call returns an error.

#### List all media outlet attachments

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "5",
            "type": "OTHER",
            "typeDescription": "Other",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
    ]
}

```

Returns a list of all media outlet attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet attachments, starting at index offset. Each entry in the array is a separate media outlet attachment object. If no more media outlet attachments are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Codes

#### Create a media outlet code

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/codes", {
    "type": "MEDSIZE",
    "value": "SMALL"
});

EXAMPLE RESPONSE
{
    "id": "223",
    "type": "MEDSIZE",
    "typeDescription": null,
    "value": "SMALL",
    "valueDescription": "Small Size",
    "isActive": true
}

```

Creates a new media outlet code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a media outlet code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet code

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/codes/223");

EXAMPLE RESPONSE
{
    "id": "223",
    "type": "MEDSIZE",
    "typeDescription": "Media Size Type",
    "value": "SMALL",
    "valueDescription": "Small Size",
    "isActive": true
}

```

Retrieves the details of an existing media outlet code. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet code to be retrieved.

##### Returns

Returns a media outlet code object if a valid id was provided.

#### Update a media outlet code

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/codes/223", {
    "value": "MEDIUM"
});

EXAMPLE RESPONSE
{
    "id": "223",
    "type": "MEDSIZE",
    "typeDescription": "Media Size Type",
    "value": "MEDIUM",
    "valueDescription": "Medium Size",
    "isActive": true
}


```

Updates the specified media outlet code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the media outlet code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet code

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/codes/224", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet code. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet code does not exist, this call returns an error.

#### List all media outlet codes

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "223",
            "type": "MEDSIZE",
            "typeDescription": "Media Size Type",
            "value": "MEDIUM",
            "valueDescription": "Medium Size",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all media outlet codes.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet codes, starting at index offset. Each entry in the array is a separate media outlet code object. If no more media outlet codes are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Contracts

#### Create a media outlet contracts

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/contracts

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/contracts", {
    "startDate": "2015-08-01",
    "endDate": "2016-08-31"
});

EXAMPLE RESPONSE
{
    "outlet": "KCMOO",
    "id": "96",
    "contractId": "1000000023",
    "startDate": "2015-08-01",
    "endDate": "2016-08-31",
    "isActive": true,
    "referenceNumber": null,
    "comment": null
}

```

Creates a new media outlet contracts.

##### Arguments

* startDate (optional) - The start date for the contract.
* endDate (optional) - The end date for the contract.
* isActive (optional : default true) - Indicates whether the contract is active.
* referenceNumber (optional) - The reference number for the contract.
* comment (optional) - Large text field for additional comments.

##### Returns

Returns a media outlet contracts object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet contract

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/contracts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/contracts/96");

EXAMPLE RESPONSE
{
    "outlet": "KCMOO",
    "id": "96",
    "contractId": "1000000023",
    "startDate": "2015-08-01",
    "endDate": "2016-08-31",
    "isActive": true,
    "referenceNumber": null,
    "comment": null
}

```

Retrieves the details of an existing media outlet contract. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet contract to be retrieved.

#### Update a media outlet contract

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/contracts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/contracts/96", {
    "endDate": "2016-08-01",
    "referenceNumber": "DOC-123"
});

EXAMPLE RESPONSE
{
    "outlet": "KCMOO",
    "id": "96",
    "contractId": "1000000023",
    "startDate": "2015-08-01",
    "endDate": "2016-08-01",
    "isActive": true,
    "referenceNumber": "DOC-123",
    "comment": null
}


```

Updates the specified media outlet contract by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* startDate (optional) - The start date for the contract.
* endDate (optional) - The end date for the contract.
* isActive (optional) - Indicates whether the contract is active.
* referenceNumber (optional) - The reference number for the contract.
* comment (optional) - Large text field for additional comments.

##### Returns

Returns the media outlet contract object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet contract

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/contracts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/contracts/95", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet contract. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet contract to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet contract does not exist, this call returns an error.

#### List all media outlet contracts

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/contracts

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/contracts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "outlet": "KCMOO",
            "id": "96",
            "contractId": "1000000023",
            "startDate": "2015-08-01",
            "endDate": "2016-08-01",
            "isActive": true,
            "referenceNumber": "DOC-123",
            "comment": null
        },
        {...},
    ]
}

```

Returns a list of all media outlet contracts.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet contracts, starting at index offset. Each entry in the array is a separate media outlet contract object. If no more media outlet contracts are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Costs

#### Create a media outlet cost

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/costs

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/costs", {
    "transactionDate": "2015-08-18",
    "comment": "new shoes"
});

EXAMPLE RESPONSE
{
    "id": "518",
    "transactionDate": "2015-08-18",
    "totalAmount": 0,
    "comment": "new shoes",
    "isCostAdjustment": false
}

```

Creates a new media outlet cost.

##### Arguments

* comment (required) - The comment for the cost.
* transactionDate (required) - The date for the cost.
* totalAmount (optional) - The amount of the cost.
* isCostAdjustment (optional : defaults to false) - Indicates whether the cost is a cost adjustment.

##### Returns

Returns a media outlet cost object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet cost

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/costs/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/costs/518");

EXAMPLE RESPONSE
{
    "id": "518",
    "transactionDate": "2015-08-18",
    "totalAmount": 0,
    "comment": "new shoes",
    "isCostAdjustment": false
}

```

Retrieves the details of an existing media outlet cost. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet cost to be retrieved.

#### Update a media outlet cost

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/costs/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/costs/518", {
    "totalAmount": 500
});

EXAMPLE RESPONSE
{
    "id": "518",
    "transactionDate": "2015-08-18",
    "totalAmount": 500,
    "comment": "new shoes",
    "isCostAdjustment": false
}


```

Updates the specified media outlet cost by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* comment (optional) - The comment for the cost.
* transactionDate (optional) - The date for the cost.
* totalAmount (optional) - The amount of the cost.
* isCostAdjustment (optional) - Indicates whether the cost is a cost adjustment.

##### Returns

Returns the media outlet cost object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet cost

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/costs/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/costs/518", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet cost. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet cost to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet cost does not exist, this call returns an error.

#### List all media outlet costs

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/costs

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/costs");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "518",
            "transactionDate": "2015-08-18",
            "totalAmount": 500,
            "comment": "new shoes",
            "isCostAdjustment": false
        },
        {...},
    ]
}

```

Returns a list of all media outlet costs.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet costs, starting at index offset. Each entry in the array is a separate media outlet cost object. If no more media outlet costs are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Coverage Areas

#### Create a media outlet coverage area

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/coverageareas

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/coverageareas", {
    "country": "USA",
    "postalCode": "75080"
});

EXAMPLE RESPONSE
{
    "id": "10135",
    "city": null,
    "state": null,
    "postalCode": "75080",
    "country": "USA",
    "useAsPrimary": false,
    "isTranslator": false,
    "callLetters": null,
    "frequency": null
}

```

Creates a new media outlet coverage area.

##### Arguments

* country (required) - The country of the coverage area.
* postalCode (optional) - The postal code of the coverage area, must be valid for country and is required for some countries.
* city (optional) - The city of the coverage area.
* state (optional) - The state of the coverage area, must be valid for country.
* useAsPrimary (optional) - Indicates whether the coverage area is the primary.
* isTranslator (optional) - Indicates whether the coverage area is a translator.
* callLetters (optional) - The call letters of the translator.
* frequency (optional) - The frequency of the translator.

##### Returns

Returns a media outlet coverage area object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet coverage area

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/coverageareas/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/coverageareas/10135");

EXAMPLE RESPONSE
{
    "id": "10135",
    "city": null,
    "state": null,
    "postalCode": "75080",
    "country": "USA",
    "useAsPrimary": false,
    "isTranslator": false,
    "callLetters": null,
    "frequency": null
}

```

Retrieves the details of an existing media outlet coverage area. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet coverage area to be retrieved.

#### Update a media outlet coverage area

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/coverageareas/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/coverageareas/10135", {
    "city": "Richardson",
    "state": "TX"
});

EXAMPLE RESPONSE
{
    "id": "10135",
    "city": "Richardson",
    "state": "TX",
    "postalCode": "75080",
    "country": "USA",
    "useAsPrimary": false,
    "isTranslator": false,
    "callLetters": null,
    "frequency": null
}


```

Updates the specified media outlet coverage area by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* country (optional) - The country of the coverage area.
* postalCode (optional) - The postal code of the coverage area, must be valid for country.
* city (optional) - The city of the coverage area.
* state (optional) - The state of the coverage area, must be valid for country.
* useAsPrimary (optional) - Indicates whether the coverage area is the primary.
* isTranslator (optional) - Indicates whether the coverage area is a translator.
* callLetters (optional) - The call letters of the translator.
* frequency (optional) - The frequency of the translator.

##### Returns

Returns the media outlet coverage area object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet coverage area

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/coverageareas/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/coverageareas/10135", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet coverage area. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet coverage area to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet coverage area does not exist, this call returns an error.

#### List all media outlet coverage areas

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/coverageareas

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/coverageareas");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10135",
            "city": "Richardson",
            "state": "TX",
            "postalCode": "75080",
            "country": "USA",
            "useAsPrimary": false,
            "isTranslator": false,
            "callLetters": null,
            "frequency": null
        },
        {...},
    ]
}

```

Returns a list of all media outlet coverage areas.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet coverage areas, starting at index offset. Each entry in the array is a separate media outlet coverage area object. If no more media outlet coverage areas are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Daily Summaries

#### List all media outlet daily summaries

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/dailysummaries

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/dailysummaries?dateFrom=2010-07-01&dateTo=2010-07-31");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1074",
            "date": "2010-07-08",
            "donationIncome": 0,
            "numberOfDonations": 0,
            "productSaleIncome": 0,
            "numberOfProductSales": 0,
            "subscriptionIncome": 0,
            "numberOfSubscriptions": 0,
            "registrationIncome": 0,
            "numberOfRegistrations": 0,
            "totalNumberOfResponses": 0
        },
        {...},
    ]
}

```

Returns a list of all media outlet daily summaries.

##### Arguments

* dateFrom (optional) - Beginning of the date range to filter date by.
* dateTo (optional) - End of the date range to filter date by.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet daily summaries, starting at index offset. Each entry in the array is a separate media outlet daily summary object. If no more media outlet daily summaries are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Dates

#### Create a media outlet date

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/dates", {
    "type": "DDCMEDFOND",
    "value": "2008-08-14"
});

EXAMPLE RESPONSE
{
    "id": "26",
    "type": "DDCMEDFOND",
    "typeDescription": null,
    "value": "2008-08-14",
    "isActive": true
}

```

Creates a new media outlet date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a media outlet date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet date

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/dates/26");

EXAMPLE RESPONSE
{
    "id": "26",
    "type": "DDCMEDFOND",
    "typeDescription": "Founded",
    "value": "2008-08-14",
    "isActive": true
}

```

Retrieves the details of an existing media outlet date. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet date to be retrieved.

##### Returns

Returns a media outlet date object if a valid id was provided.

#### Update a media outlet date

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/dates/26", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "26",
    "type": "DDCMEDFOND",
    "typeDescription": "Founded",
    "value": "2008-08-14",
    "isActive": false
}


```

Updates the specified media outlet date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the media outlet date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet date

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/dates/27", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet date. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet date does not exist, this call returns an error.

#### List all media outlet dates

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "26",
            "type": "DDCMEDFOND",
            "typeDescription": "Founded",
            "value": "2008-08-14",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all media outlet dates.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet dates, starting at index offset. Each entry in the array is a separate media outlet date object. If no more media outlet dates are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Month End

#### Retrieve the media calendar for the current month

```
DEFINITION
GET http://apiserver/mediaoutlets/monthend

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/monthend");

EXAMPLE RESPONSE
{
    "year": 2014,
    "month": 6,
    "start": "2014-06-02",
    "end": "2014-06-30",
    "mediaCurrentMonth": "06/2014"
}

```

Retrieves the details of an existing media calendar for the current month, as well as the media month control record (MEDIACAL).

#### Run media outlet month end

```
DEFINITION
POST http://apiserver/mediaoutlets/monthend

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/monthend", {});

EXAMPLE RESPONSE
204 No Content

```

Runs month end process in media management.

##### Returns

Returns a `204 No Content` response on success. If the month end process fails to start, this call returns an error.

### Media Outlet Monthly Summaries

#### List all media outlet monthly summaries

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/monthlysummaries

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/monthlysummaries");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1130",
            "year": 2013,
            "month": 7,
            "totalAccounts": 37,
            "newAccounts": 1,
            "netDonationIncome": 445.5,
            "totalCost": 0,
            "giftIncome": 445.5,
            "numberOfGifts": 7,
            "salesIncome": 0,
            "numberOfSales": 2,
            "subscriptionIncome": 60,
            "numberOfSubscriptions": 3,
            "registrationIncome": 0,
            "numberOfRegistrations": 1,
            "totalNumberOfResponses": 11
        },
        {...},
    ]
}

```

Returns a list of all media outlet monthly summaries.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet monthly summaries, starting at index offset. Each entry in the array is a separate media outlet monthly summary object. If no more media outlet monthly summaries are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Notes

#### Create a media outlet note

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/notes", {
    "type": "DDCMENOTTY",
    "shortComment": "demo"
});

EXAMPLE RESPONSE
{
    "id": "14",
    "type": "DDCMENOTTY",
    "typeDescription": null,
    "shortComment": "demo",
    "longComment": null
}

```

Creates a new media outlet note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a media outlet note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet note

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/notes/14");

EXAMPLE RESPONSE
{
    "id": "14",
    "type": "DDCMENOTTY",
    "typeDescription": "Media Note Type",
    "shortComment": "demo",
    "longComment": null
}

```

Retrieves the details of an existing media outlet note. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet note to be retrieved.

##### Returns

Returns a media outlet note object if a valid id was provided.

#### Update a media outlet note

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/notes/14", {
    "longComment": "now we have a long comment"
});

EXAMPLE RESPONSE
{
    "id": "14",
    "type": "DDCMENOTTY",
    "typeDescription": "Media Note Type",
    "shortComment": "demo",
    "longComment": "now we have a long comment"
}


```

Updates the specified media outlet note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the media outlet note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet note

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/notes/14", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet note. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet note does not exist, this call returns an error.

#### List all media outlet notes

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "14",
            "type": "DDCMENOTTY",
            "typeDescription": "Media Note Type",
            "shortComment": "demo",
            "longComment": "now we have a long comment"
        },
        {...},
    ]
}

```

Returns a list of all media outlet notes.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet notes, starting at index offset. Each entry in the array is a separate media outlet note object. If no more media outlet notes are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Numbers

#### Create a media outlet number

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/numbers", {
    "type": "DDCMEDEMPL",
    "value": 7
});

EXAMPLE RESPONSE
{
    "id": "60",
    "type": "DDCMEDEMPL",
    "typeDescription": null,
    "value": 7,
    "isActive": true
}

```

Creates a new media outlet number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a media outlet number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet number

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/numbers/60");

EXAMPLE RESPONSE
{
    "id": "60",
    "type": "DDCMEDEMPL",
    "typeDescription": "Employees",
    "value": 7,
    "isActive": true
}

```

Retrieves the details of an existing media outlet number. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet number to be retrieved.

##### Returns

Returns a media outlet number object if a valid id was provided.

#### Update a media outlet number

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/numbers/60", {
    "value": 10
});

EXAMPLE RESPONSE
{
    "id": "60",
    "type": "DDCMEDEMPL",
    "typeDescription": "Employees",
    "value": 10,
    "isActive": true
}


```

Updates the specified media outlet number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the media outlet number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet number

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/numbers/60", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet number. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet number does not exist, this call returns an error.

#### List all media outlet numbers

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "60",
            "type": "DDCMEDEMPL",
            "typeDescription": "Employees",
            "value": 10,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all media outlet numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet numbers, starting at index offset. Each entry in the array is a separate media oultet number object. If no more media outlet numbers are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Placements

#### Create a media outlet placement

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/contracts/:id/placements

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/contracts/96/placements", {
    "program": "AIO",
    "paymentType": "PD",
    "deliveryType": "FTP"
});

EXAMPLE RESPONSE
{
    "outlet": "KCMOO",
    "id": "136",
    "contract": 1000000023,
    "program": "AIO",
    "isActive": true,
    "startDate": null,
    "endDate": null,
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": false,
    "isSaturday": false,
    "leadInProgram": null,
    "leadOutProgram": null,
    "deliveryType": "FTP",
    "paymentType": "PD",
    "perShowAmount": null,
    "perShowPercent": null,
    "perShowMinimum": null,
    "perShowMaximum": null,
    "monthlyMinimum": null,
    "monthlyMaximum": null,
    "monthlyBase": null
}

```

Creates a new media outlet placement.

##### Arguments

* program (required) - The program code for the placement. Should be a valid "DDCPROGR" value.
* isActive (optional : default true) - Indicates whether the placement is active.
* startDate (optional) - The start date of the placement.
* endDate (optional) - The end date of the placement.
* isMonday (optional : default false) - Indicates whether the placement applies to Monday.
* isTuesday (optional : default false) - Indicates whether the placement applies to Tuesday.
* isWednesday (optional : default false) - Indicates whether the placement applies to Wednesday.
* isThursday (optional : default false) - Indicates whether the placement applies to Thursday.
* isFriday (optional : default false) - Indicates whether the placement applies to Friday.
* isSaturday (optional : default false) - Indicates whether the placement applies to Saturday.
* isSunday (optional : default false) - Indicates whether the placement applies to Sunday.
* leadInProgram (optional) - The lead in program for the placement.
* leadOutProgram (optional) - The lead out program for the placement.
* paymentType (required) - The payment type for the placement. Should be a valid "DDCMPTP" value.
* deliveryType (required) - The delivery type for the placement. Should be a valid "DDCDELIV" value.
* perShowAmount (optional) - The amount per show for the placement.
* perShowPercent (optional) - The percent per show for the placement.
* perShowMinimum (optional) - The minimum per show for the placement.
* perShowMaximum (optional) - The maximum per show for the placement.
* monthlyMinimum (optional) - The monthly minimum for the placement.
* monthlyMaximum (optional) - The monthly maximum for the placement.
* monthlyBase (optional) - The monthly base for the placement.

##### Returns

Returns a media outlet placement object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet placement

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/contracts/96/placements/136");

EXAMPLE RESPONSE
{
    "outlet": "KCMOO",
    "id": "136",
    "contract": 1000000023,
    "program": "AIO",
    "isActive": true,
    "startDate": null,
    "endDate": null,
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": false,
    "isSaturday": false,
    "leadInProgram": null,
    "leadOutProgram": null,
    "deliveryType": "FTP",
    "paymentType": "PD",
    "perShowAmount": null,
    "perShowPercent": null,
    "perShowMinimum": null,
    "perShowMaximum": null,
    "monthlyMinimum": null,
    "monthlyMaximum": null,
    "monthlyBase": null
}

```

Retrieves the details of an existing media outlet placement. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet placement to be retrieved.

#### Update a media outlet placement

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/1/contracts/96/placements/136", {
    "startDate": "2015-08-01",
    "endDate": "2016-08-01"
});

EXAMPLE RESPONSE
{
    "outlet": "KCMOO",
    "id": "136",
    "contract": 1000000023,
    "program": "AIO",
    "isActive": true,
    "startDate": "2015-08-01",
    "endDate": "2016-08-01",
    "isSunday": false,
    "isMonday": false,
    "isTuesday": false,
    "isWednesday": false,
    "isThursday": false,
    "isFriday": false,
    "isSaturday": false,
    "leadInProgram": null,
    "leadOutProgram": null,
    "deliveryType": "FTP",
    "paymentType": "PD",
    "perShowAmount": null,
    "perShowPercent": null,
    "perShowMinimum": null,
    "perShowMaximum": null,
    "monthlyMinimum": null,
    "monthlyMaximum": null,
    "monthlyBase": null
}


```

Updates the specified media outlet placement by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* program (optional) - The program code for the placement. Should be a valid "DDCPROGR" value.
* isActive (optional) - Indicates whether the placement is active.
* startDate (optional) - The start date of the placement.
* endDate (optional) - The end date of the placement.
* isMonday (optional) - Indicates whether the placement applies to Monday.
* isTuesday (optional) - Indicates whether the placement applies to Tuesday.
* isWednesday (optional) - Indicates whether the placement applies to Wednesday.
* isThursday (optional) - Indicates whether the placement applies to Thursday.
* isFriday (optional) - Indicates whether the placement applies to Friday.
* isSaturday (optional) - Indicates whether the placement applies to Saturday.
* isSunday (optional) - Indicates whether the placement applies to Sunday.
* leadInProgram (optional) - The lead in program for the placement.
* leadOutProgram (optional) - The lead out program for the placement.
* paymentType (optional) - The payment type for the placement. Should be a valid "DDCMPTP" value.
* deliveryType (optional) - The delivery type for the placement. Should be a valid "DDCDELIV" value.
* perShowAmount (optional) - The amount per show for the placement.
* perShowPercent (optional) - The percent per show for the placement.
* perShowMinimum (optional) - The minimum per show for the placement.
* perShowMaximum (optional) - The maximum per show for the placement.
* monthlyMinimum (optional) - The monthly minimum for the placement.
* monthlyMaximum (optional) - The monthly maximum for the placement.
* monthlyBase (optional) - The monthly base for the placement.

##### Returns

Returns the media outlet placement object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet placement

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/1/contracts/96/placements/135", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet placement. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet placement to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet placement does not exist, this call returns an error.

#### List all media outlet placements

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/contracts/:id/placements

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/1/contracts/96/placements?isActive=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "outlet": "KCMOO",
            "id": "136",
            "contract": 1000000023,
            "program": "AIO",
            "isActive": true,
            "startDate": "2015-08-01",
            "endDate": "2016-08-01",
            "isSunday": false,
            "isMonday": false,
            "isTuesday": false,
            "isWednesday": false,
            "isThursday": false,
            "isFriday": false,
            "isSaturday": false,
            "leadInProgram": null,
            "leadOutProgram": null,
            "deliveryType": "FTP",
            "paymentType": "PD",
            "perShowAmount": null,
            "perShowPercent": null,
            "perShowMinimum": null,
            "perShowMaximum": null,
            "monthlyMinimum": null,
            "monthlyMaximum": null,
            "monthlyBase": null
        },
        {...},
    ]
}

```

Returns a list of all media outlet placements.

##### Arguments

* isActive (optional) - Indicates whether the placement is active.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet placements, starting at index offset. Each entry in the array is a separate media outlet placement object. If no more media outlet placements are available, the resulting array will be empty. This request should never return an error.

### Media Outlet Placement Times

#### Create a media outlet placement time

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id/times

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/2/contracts/1/placements/1/times", {
    "time": "01:00:00 PM",
    "timeZone": "CT",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "10031",
    "time": "01:00:00 PM",
    "timeZone": "CT",
    "timeZoneDescription": "Central Time",
    "isActive": true
}

```

Creates a new media outlet placement time.

##### Arguments

* time (required) - The time of the show.
* timeZone (optional) - The time zone for this time, must be a valid DDCTIMEZON code.
* isActive (optional) - Indicates whether the placement time is active.

##### Returns

Returns a media outlet placement time object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet placement time

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id/times/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/2/contracts/1/placements/1/times/10031");

EXAMPLE RESPONSE
{
    "id": "10031",
    "time": "01:00:00 PM",
    "timeZone": "CT",
    "timeZoneDescription": "Central Time",
    "isActive": true
}

```

Retrieves the details of an existing media outlet placement time. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet placement time to be retrieved.

#### Update a media outlet placement time

```
DEFINITION
POST http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id/times/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/2/contracts/1/placements/1/times/10031", {
    "time": "02:00:00 PM"
});

EXAMPLE RESPONSE
{
    "id": "10031",
    "time": "02:00:00 PM",
    "timeZone": "CT",
    "timeZoneDescription": "Central Time",
    "isActive": true
}


```

Updates the specified media outlet placement time by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* time (optional) - The time of the show.
* timeZone (optional) - The time zone for this time, must be a valid DDCTIMEZON code.
* isActive (optional) - Indicates whether the placement time is active.

##### Returns

Returns the media outlet placement time object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet placement time

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id/times/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/2/contracts/1/placements/1/times/10031", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet placement time. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet placement time to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet placement time does not exist, this call returns an error.

#### List all media outlet placement times

```
DEFINITION
GET http://apiserver/mediaoutlets/:id/contracts/:id/placements/:id/times

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/2/contracts/1/placements/1/times");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10031",
            "time": "02:00:00 PM",
            "timeZone": "CT",
            "timeZoneDescription": "Central Time",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all media outlet placement times.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlet placement times, starting at index offset. Each entry in the array is a separate media outlet placement time object. If no more media outlet placement times are available, the resulting array will be empty. This request should never return an error.

### Media Outlets

#### Create a media outlet

```
DEFINITION
POST http://apiserver/mediaoutlets

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets", {
    "outlet": {
        "mediaId": "JIMM"
    },
    "coverageArea": {
        "country": "USA",
        "postalCode": "75080"
    },
    "mailingAddress": {
        "country": "USA",
        "postalCode": "75080"
    }
});

EXAMPLE RESPONSE
{
    "id": "97",
    "outlet": {
        "id": "97",
        "mediaId": "JIMM",
        "description": "JIMM",
        "frequency": null,
        "owner": null,
        "accountNumber": 27686,
        "website": null,
        "useMediaCalendar": false,
        "network": null,
        "isActive": true,
        "primaryZipPostal": "75080"
    },
    "type": null,
    "dma": null,
    "category": null,
    "coverageArea": {
        "id": "10132",
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA"
    },
    "phone": null,
    "fax": null,
    "mailingAddress": {
        "id": "1000027785",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null
    },
    "billingAddress": {
        "id": "1000027786",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null
    },
    "shippingAddress": {
        "id": "1000027787",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null
    },
    "formattedPhone": null,
    "formattedFax": null
}

```

Creates a new media outlet.

##### Arguments

* outlet (required) - The outlet information of the media outlet. mediaId is required. description, frequency, owner, network, isActive, and website are optional.
* type (optional) - The type of the media outlet, must be a valid DDCMEDTYPE code.
* dma (optional) - The designated market area of the media outlet, must be a valid DDCMEDDMA code.
* category (optional) - The category of the media outlet, must be a valid DDCMEDCAT code.
* coverageArea (required) - The coverage area of the media outlet. country is required. postalCode and state must be valid for the country and postalCode is required for some countries.
* mailingAddress (required) - The mailing address of the media outlet. country is required. postalCode and state must be valid for the country and postalCode is required for some countries. city, line1, line2, line3, and line4 are optional.
* billingAddress (required) - The billing address of the media outlet. Set to null to use the mailingAddress for billingAddress as well.
* shippingAddress (required) - The shipping address of the media outlet. Set to null to use the mailingAddress for shippingAddress as well.
* phone (optional) - The phone number of the media outlet. Ignored unless type, areaCode, and phoneNumber are provided. extension and internationalCode are optional.
* fax (optional) - The fax number of the media outlet. Ignored unless areaCode, and phoneNumber are provided. extension and internationalCode are optional.
* useMediaCalendar (optional; defaults to `false`) - Determines if the Media Calendar should be used.

##### Returns

Returns a media outlet object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media outlet

```
DEFINITION
GET http://apiserver/mediaoutlets/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets/97");

EXAMPLE RESPONSE
{
    "id": "97",
    "outlet": {
        "id": "97",
        "mediaId": "JIMM",
        "description": "JIMM",
        "frequency": null,
        "owner": null,
        "accountNumber": 27686,
        "website": null,
        "useMediaCalendar": false,
        "network": null,
        "isActive": true,
        "primaryZipPostal": "75080"
    },
    "type": {
        "id": null,
        "type": null,
        "typeDescription": null,
        "value": null,
        "valueDescription": null,
        "isActive": true
    },
    "dma": {
        "id": null,
        "type": null,
        "typeDescription": null,
        "value": null,
        "valueDescription": null,
        "isActive": true
    },
    "category": {
        "id": null,
        "type": null,
        "typeDescription": null,
        "value": null,
        "valueDescription": null,
        "isActive": true
    },
    "coverageArea": {
        "id": "10132",
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA"
    },
    "phone": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": false,
        "isActive": true,
        "functionalCategory": null
    },
    "fax": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": false,
        "isActive": true,
        "functionalCategory": null
    },
    "mailingAddress": {
        "id": "1000027785",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null
    },
    "billingAddress": {
        "id": "1000027786",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null
    },
    "shippingAddress": {
        "id": "1000027787",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null
    },
    "formattedPhone": null,
    "formattedFax": null
}

```

Retrieves the details of an existing media outlet. You need only supply the id.

##### Arguments

* id (required) - The id of the media outlet to be retrieved.

#### Update a media outlet

```
DEFINITION
POST http://apiserver/mediaoutlets/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaoutlets/97", {
    "phone": {
        "type": "HOME",
        "areaCode": "555",
        "phoneNumber": "555-5555"
    }
});

EXAMPLE RESPONSE
{
    "id": "97",
    "outlet": {
        "id": "97",
        "mediaId": "JIMM",
        "description": "JIMM",
        "frequency": null,
        "owner": null,
        "accountNumber": 27686,
        "website": null,
        "useMediaCalendar": false,
        "network": null,
        "isActive": true,
        "primaryZipPostal": "75080"
    },
    "type": {
        "id": null,
        "type": null,
        "typeDescription": null,
        "value": null,
        "valueDescription": null,
        "isActive": true
    },
    "dma": {
        "id": null,
        "type": null,
        "typeDescription": null,
        "value": null,
        "valueDescription": null,
        "isActive": true
    },
    "category": {
        "id": null,
        "type": null,
        "typeDescription": null,
        "value": null,
        "valueDescription": null,
        "isActive": true
    },
    "coverageArea": {
        "id": "10132",
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA"
    },
    "phone": {
        "id": "44674",
        "type": "HOME",
        "internationalCode": null,
        "areaCode": "555",
        "phoneNumber": "555-5555",
        "extension": null,
        "isPrimary": true,
        "isActive": true,
        "functionalCategory": null
    },
    "fax": {
        "id": null,
        "type": null,
        "internationalCode": null,
        "areaCode": null,
        "phoneNumber": null,
        "extension": null,
        "isPrimary": false,
        "isActive": true,
        "functionalCategory": null
    },
    "mailingAddress": {
        "id": "1000027785",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null
    },
    "billingAddress": {
        "id": "1000027786",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null
    },
    "shippingAddress": {
        "id": "1000027787",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null
    },
    "formattedPhone": "(555) 555-5555",
    "formattedFax": null
}


```

Updates the specified media outlet by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* outlet (optional) - The outlet information of the media outlet.
* type (optional) - The type of the media outlet, must be a valid DDCMEDTYPE code.
* dma (optional) - The designated market area of the media outlet, must be a valid DDCMEDDMA code.
* category (optional) - The category of the media outlet, must be a valid DDCMEDCAT code.
* coverageArea (optional) - The coverage area of the media outlet.
* mailingAddress (optional) - The mailing address of the media outlet.
* billingAddress (optional) - The billing address of the media outlet.
* shippingAddress (optional) - The shipping address of the media outlet.
* phone (optional) - The phone number of the media outlet. When adding a new phone, it will be ignored unless type, areaCode, and phoneNumber are provided.
* fax (optional) - The fax number of the media outlet. When adding a new fax, it will be ignored unless areaCode, and phoneNumber are provided.
* useMediaCalendar (optional) - Determines if the Media Calendar should be used.

##### Returns

Returns the media outlet object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media outlet

```
DEFINITION
DELETE http://apiserver/mediaoutlets/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaoutlets/97", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media outlet. It cannot be undone.

##### Arguments

* id (required) - The id of the media outlet to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media outlet does not exist, this call returns an error.

#### List all media outlets

```
DEFINITION
GET http://apiserver/mediaoutlets

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaoutlets?mediaid=jimm");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "97",
            "mediaId": "JIMM",
            "description": "JIMM",
            "frequency": null,
            "owner": null,
            "accountNumber": 27686,
            "website": null,
            "useMediaCalendar": false,
            "network": null,
            "isActive": true,
            "primaryZipPostal": "75080"
        },
        {...},
    ]
}

```

Returns a list of all media outlets.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* mediaid (optional) - Filter list by partial match in media outlet id.
* description (optional) - Filter list by partial match in media outlet description.
* mediafrequency (optional) - Filter list by partial match in media outlet frequency.
* networkId (optional) - Filter list by partial match in media outlet network.
* website (optional) - Filter list by partial match in media outlet website.
* owner (optional) - Filter list by partial match in media outlet owner.
* accountnumber (optional) - Filter list by exact match on media outlet account number.
* active (optional) - Filter list by whether media outlet is active or not.
* lastname (optional) - Filter list by partial match in media outlet contacts last name.
* firstname (optional) - Filter list by partial match in media outlet contacts first name.
* country (optional) - Filter list by partial match in media outlet coverage country.
* zippostal (optional) - Filter list by partial match in media outlet coverage postal code.
* city (optional) - Filter list by partial match in media outlet coverage city.
* state (optional) - Filter list by partial match in media outlet coverage state.
* codetype (optional) - Filter list by exact match on media outlet code type.
* codevalue (optional) - Filter list by exact match on media outlet code value.
* datetype (optional) - Filter list by exact match on media outlet date type.
* datevalue (optional) - Filter list by exact match on media outlet date value.
* numbertype (optional) - Filter list by exact match on media outlet number type.
* numbervalue (optional) - Filter list by exact match on media outlet number value.
* notetype (optional) - Filter list by exact match on media outlet note type.
* noteshortcomment (optional) - Filter list by partial match in media outlet note short comment.
* notelongcomment (optional) - Filter list by partial match in media outlet note long comment.
* aliasdescription (optional) - Filter list by partial match in media outlet alias.

##### Returns

A dictionary with an items property that contains an array of up to limit media outlets, starting at index offset. Each entry in the array is a separate media outlet object. If no more media outlets are available, the resulting array will be empty. This request should never return an error.

### Media Program Show Source Offerings

#### List all media program show source offerings

```
DEFINITION
GET http://apiserver/mediaprograms/:id/shows/:id/offerings

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaprograms/29/shows/18/offerings");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "codeType": "SOURCE",
            "product": "DV1002",
            "productDescription": "Once Upon an Avalanche",
            "price": "RP",
            "priceDescription": "Retail Price",
            "amount": 13.5,
            "isPrimaryOffering": false
        },
        {...},
    ]
}

```

Returns a list of all media program show source offerings.

##### Returns

A dictionary with an items property that contains an array of up to limit media program show source offerings, starting at index offset. Each entry in the array is a separate offering object. If no more media program show source offerings are available, the resulting array will be empty. This request should never return an error.

### Media Program Shows

#### Create a media program show

```
DEFINITION
POST http://apiserver/mediaprograms/:id/shows

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaprograms/29/shows", {
    "id": "SHOW1",
    "description": "the best show around"
});

EXAMPLE RESPONSE
{
    "id": "18",
    "showCode": "SHOW1",
    "description": "the best show around",
    "airing": null,
    "source": null,
    "sourceDescription": null,
    "rebroadcast": null,
    "language": null,
    "languageDescription": null,
    "series": null,
    "host": null,
    "guest": null,
    "shortComment": null,
    "comment": null,
    "message": null,
    "messageDescription": null
}

```

Creates a new media program show.

##### Arguments

* showCode (required) - The show code of the media program show. Must be unique.
* description (required) - The description of the media program show.
* airing (optional) - The airing date of the media program show.
* source (optional) - The source code of the media program show. Must be a valid code if provided.
* rebroadcast (optional) - Indicates whether the media program show is a rebroadcast.
* language (optional) - The language code of the media program show. Must be a valid code if provided.
* series (optional) - The series of the media program show.
* host (optional) - The host of the media program show.
* guest (optional) - The guest of the media program show.
* shortComment (optional) - The short comment of the media program show.
* comment (optional) - The long comment of the media program show.
* message (optional) - The message code of the media program show. Must be a valid code if provided.

##### Returns

Returns a media program show object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media program show

```
DEFINITION
GET http://apiserver/mediaprograms/:id/shows/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaprograms/29/shows/18");

EXAMPLE RESPONSE
{
    "id": "18",
    "showCode": "SHOW1",
    "description": "the best show around",
    "airing": null,
    "source": null,
    "sourceDescription": null,
    "rebroadcast": null,
    "language": null,
    "languageDescription": null,
    "series": null,
    "host": null,
    "guest": null,
    "shortComment": null,
    "comment": null,
    "message": null,
    "messageDescription": null
}

```

Retrieves the details of an existing media program show. You need only supply the id.

##### Arguments

* id (required) - The id of the media program show to be retrieved.

#### Update a media program show

```
DEFINITION
POST http://apiserver/mediaprograms/:id/shows/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaprograms/29/shows/18", {
    "message": "M1234"
});

EXAMPLE RESPONSE
{
    "id": "18",
    "showCode": "SHOW1",
    "description": "the best show around",
    "airing": null,
    "source": null,
    "sourceDescription": null,
    "rebroadcast": null,
    "language": null,
    "languageDescription": null,
    "series": null,
    "host": null,
    "guest": null,
    "shortComment": null,
    "comment": null,
    "message": "M1234",
    "messageDescription": "What Would Jesus Do?"
}


```

Updates the specified media program show by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* showCode (optional) - The show code of the media program show. Must be unique.
* description (optional) - The description of the media program show.
* airing (optional) - The airing date of the media program show.
* source (optional) - The source code of the media program show. Must be a valid code if provided.
* rebroadcast (optional) - Indicates whether the media program show is a rebroadcast.
* language (optional) - The language code of the media program show. Must be a valid code if provided.
* series (optional) - The series of the media program show.
* host (optional) - The host of the media program show.
* guest (optional) - The guest of the media program show.
* shortComment (optional) - The short comment of the media program show.
* comment (optional) - The long comment of the media program show.
* message (optional) - The message code of the media program show. Must be a valid code if provided.

##### Returns

Returns the media program show object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media program show

```
DEFINITION
DELETE http://apiserver/mediaprograms/:id/shows/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaprograms/29/shows/18", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media program show. It cannot be undone.

##### Arguments

* id (required) - The id of the media program show to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media program show does not exist, this call returns an error.

#### List all media program shows

```
DEFINITION
GET http://apiserver/mediaprograms/:id/shows

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaprograms/29/shows");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "18",
            "showCode": "SHOW1",
            "description": "the best show around",
            "airing": null,
            "source": null,
            "sourceDescription": null,
            "rebroadcast": null,
            "language": null,
            "languageDescription": null,
            "series": null,
            "host": null,
            "guest": null,
            "shortComment": null,
            "comment": null,
            "message": "M1234",
            "messageDescription": "What Would Jesus Do?"
        },
        {...},
    ]
}

```

Returns a list of all media program shows.

##### Returns

A dictionary with an items property that contains an array of up to limit media program shows, starting at index offset. Each entry in the array is a separate media program show object. If no more media program shows are available, the resulting array will be empty. This request should never return an error.

### Media Programs

#### Create a media program

```
DEFINITION
POST http://apiserver/mediaprograms

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaprograms", {
    "programCode": "PROG01",
    "description": "the first program"
});

EXAMPLE RESPONSE
{
    "id": "29",
    "programCode": "PROG01",
    "description": "the first program",
    "type": null,
    "typeDescription": null,
    "length": null,
    "frequency": null,
    "frequencyDescription": null,
    "isActive": true
}

```

Creates a new media program.

##### Arguments

* programCode (required) - The program code of the media program. Must be unique.
* description (required) - The description of the media program.
* type (optional) - The type of the media program, must be a valid code if provided.
* length (optional) - The length, in minutes, of the media program.
* frequency (optional) - The frequency of the media program, must be a valid code if provided.
* isActive (optional) - Indicates whether the media program is active.

##### Returns

Returns a media program object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a media program

```
DEFINITION
GET http://apiserver/mediaprograms/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaprograms/29");

EXAMPLE RESPONSE
{
    "id": "29",
    "programCode": "PROG01",
    "description": "the first program",
    "type": null,
    "typeDescription": null,
    "length": null,
    "frequency": null,
    "frequencyDescription": null,
    "isActive": true
}

```

Retrieves the details of an existing media program. You need only supply the id.

##### Arguments

* id (required) - The id of the media program to be retrieved.

#### Update a media program

```
DEFINITION
POST http://apiserver/mediaprograms/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/mediaprograms/29", {
    "length": 5
});

EXAMPLE RESPONSE
{
    "id": "29",
    "programCode": "PROG01",
    "description": "the first program",
    "type": null,
    "typeDescription": null,
    "length": 5,
    "frequency": null,
    "frequencyDescription": null,
    "isActive": true
}


```

Updates the specified media program by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* programCode (optional) - The program code of the media program. Must be unique.
* description (optional) - The description of the media program.
* type (optional) - The type of the media program, must be a valid code if provided.
* length (optional) - The length, in minutes, of the media program.
* frequency (optional) - The frequency of the media program, must be a valid code if provided.
* isActive (optional) - Indicates whether the media program is active.

##### Returns

Returns the media program object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a media program

```
DEFINITION
DELETE http://apiserver/mediaprograms/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/mediaprograms/29", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a media program. It cannot be undone.

##### Arguments

* id (required) - The id of the media program to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the media program does not exist, this call returns an error.

#### List all media programs

```
DEFINITION
GET http://apiserver/mediaprograms

EXAMPLE REQUEST
$.get("http://localhost:49195/mediaprograms?frequency=DAILY");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 6
    },
    "items": [
        {
            "id": "12",
            "programCode": "BBYTLK",
            "description": "Baby Talk",
            "type": "RD",
            "typeDescription": "Radio",
            "length": 10,
            "frequency": "DAILY",
            "frequencyDescription": "Daily",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all media programs.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* programCode (optional) - The program code of the media program.
* description (optional) - The description of the media program.
* frequency (optional) - The frequency of the media program.
* active (optional) - Indicates whether the media program is active.

##### Returns

A dictionary with an items property that contains an array of up to limit media programs, starting at index offset. Each entry in the array is a separate media program object. If no more media programs are available, the resulting array will be empty. This request should never return an error.

### Pledges

#### Retrieve a pledge

```
DEFINITION
GET http://apiserver/pledges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/FEED2010");

EXAMPLE RESPONSE
{
    "id": "FEED2010",
    "description": "Feed the Hungry 2010",
    "type": "PROJECT",
    "defaultFrequency": "M",
    "defaultStart": "2010-03-01",
    "defaultEnd": "2011-03-01",
    "defaultAmountPer": 25,
    "defaultQuantity": 12,
    "defaultSource": "11DRA100",
    "defaultIsOpenEnded": false,
    "isSecure": false,
    "isSponsorship": false,
    "pledgeFrequencyDefaults": [
        {
            "id": "0",
            "isPrimary": true,
            "frequency": "S",
            "frequencyDescription": "Semi-Annual",
            "startDate": "2024-01-10",
            "endDate": null,
            "amountPerGift": 1.2500,
            "numberPledged": 1,
            "isOpenEnded": null
        },
        {...}
    ],
    "isMultipleSponsorship": false,
    "isAvailable": true,
    "isSponsored": true,
    "remainingMonthlyAmount": null,
    "amtPerMonthPledged": 100.00,
    "pledgeData": null
}

```

Retrieves the details of an existing pledge. You need only supply the pledge code.

##### Arguments

* id (required) - The pledge code of the pledge to retrieve.
* store (optional) - StudioOnline store Id; when provided, returns json that represents the pledge.

##### Returns

Returns a pledge object if a valid id was provided.

#### List all pledges

```
DEFINITION
GET http://apiserver/pledges

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 327
    }
    "items": [
        {
            "id": "FEED2010",
            "description": "Feed the Hungry 2010",
            "type": "PROJECT",
            "defaultFrequency": "M",
            "defaultStart": "2010-03-01",
            "defaultEnd": "2011-03-01",
            "defaultAmountPer": 25,
            "defaultQuantity": 12,
            "defaultSource": "11DRA100",
            "defaultIsOpenEnded": false,
            "isSecure": false,
            "isSponsorship": false,
            "isMultipleSponsorship": false,
            "isAvailable": true,
            "isSponsored": true,
            "remainingMonthlyAmount": null,
            "amtPerMonthPledged": 100.00
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pledges matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in pledge code
* type () - Filter list by partial match in pledge type
* description () - Filter list by partial match in pledge description
* isActive () - Filter list by whether active or not
* getPageContainingId (optional) - Will return the page of account pledges that contains the pledge with this id.
* restrictBasedOnAccessorId (optional) - If provided, return only results where the pledge code is defined in the PledgeAccessors table for the given accessor Id.

##### Returns

A dictionary with an items property that contains an array of up to limit pledges, starting at index offset. Each entry in the array is a separate pledge object. If no more pledges are available, the resulting array will be empty. This request should never return an error.

#### Print a pledge profile

```
DEFINITION
POST http://apiserver/pledges/:id/printprofile

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/050098/printprofile", {
    "description": "August 2011 Fund",
    "pledgeType": "PROJECT"
});

EXAMPLE RESPONSE
{
    "runId": "1000000008",
    "pledgeCode": "050098",
    "formType": {
        "id": "10171",
        "formType": "PLDGPROF",
        "description": "Test Pledge Profile",
        "communicationType": "PLDGPROFL",
        "communicationTypeDescription": "Pledge Profiles",
        "deliveryMethod": "NOTEMAIL",
        "deliveryMethodDescription": "Not Email",
        "dataSource": null,
        "documentFilterQuery": "SELECT * FROM \"L12_CheckoutPrintGroup\" WHERE RunId = {RunId}",
        "isDocumentMergedOnServer": true,
        "maxMergedDocumentRecordCount": 1000,
        "isActive": true,
        "emailSubject": null,
        "documents": [],
        "documentCollection": []
    },
    "document": {
        "fileName": "Pledge Profile.docx",
        "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
        "file": "UEsDBBQAAAAIAJqFrlKvbOy6nAEAAGsJAAATAAAAW0NvbnRlbnRfV..."
    },
    "errors": []
}

```

Performs a checkout on the print group and returns the form type to use for mail merge.

##### Arguments

* description (optional) - Description of the print group. Usually description of the pledge.
* pledgeType (optional) - Type of the pledge.

##### Returns

If successful, returns the ID of the checkout print group created, the Pledge Profile Form Type, and the resulting merged document if isDocumentMergedOnServer is true on the Form Type. If no control record exists for Pledge Profile Form Type or the Form Type Delivery Method is not NOTEMAIL, this call will return an error.

#### Replace a pledge

```
DEFINITION
POST http://apiserver/pledges/:id/replace

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/PLEDGE01/replace", {
    "id": "PLEDGE02",
    "description": "Replacement for PLEDGE01"
});

EXAMPLE RESPONSE
{
    "id": "PLEDGE02",
    "description": "Replacement for PLEDGE01",
    "company": "CCONNECT",
    "companyDescription": "Card Connect, Inc.",
    "isActive": true,
    "defaultFrequency": "M",
    "defaultFrequencyDescription": "Monthly",
    "defaultStart": "2021-07-01",
    "defaultEnd": null,
    "defaultAmountPer": 2.00,
    "defaultQuantity": 12,
    "defaultSource": "007",
    "defaultSourceDescription": "Direct Mail Appeal 2010 April",
    "defaultIsOpenEnded": true,
    "totalNumberOfPledges": 1,
    "totalNumberActive": 1,
    "totalNumberFulfilled": 0,
    "totalNumberExpired": 0,
    "totalNumberCancelled": 0,
    "totalNumberPending": 0,
    "totalNumberOnHold": 0,
    "totalAmountPledged": 24.00,
    "totalAmountPledgedActive": 24.00,
    "totalAmountPledgedFulfilled": 0.00,
    "totalAmountPledgedExpired": 0.00,
    "totalAmountPledgedCancelled": 0.00,
    "totalAmountPledgedPending": 0.00,
    "totalAmountPledgedOnHold": 0.00,
    "totalDonationsGiven": 0.00,
    "totalDonationsGivenActive": 0.00,
    "totalDonationsGivenFulfilled": 0.00,
    "totalDonationsGivenExpired": 0.00,
    "totalDonationsGivenCancelled": 0.00,
    "totalDonationsGivenPending": 0.00,
    "totalDonationsGivenOnHold": 0.00,
    "type": "CHILD",
    "typeDescription": "Child Sponorship",
    "sponsorshipType": "S",
    "totalAmountRequiredMonthly": 50.00,
    "useInStudioOnline": true,
    "defaultProject": "GENCHILD",
    "defaultProjectDescription": "General Sponsorship Fund",
    "isAvailable": false,
    "isCheckedOut": true,
    "isSponsored": false,
    "amtPerMonthPledged": 2.00,
    "isSponsorship": true
}

```

Creates a replacement of the pledge using the new ID and Description. The replacement pledge will copy all data from the original pledge, which will then be unpublished and deactivated after being successfully replaced. All active and pending account pledges for the original pledge will be continued to the new replacement pledge.

##### Arguments

* id (required) - The pledge code for the replacement pledge.
* description (optional) - The description for the replacement pledge.

##### Returns

If successful, returns the replacement pledge object. Returns an error if parameters are invalid (e.g. specifying an invalid replacement pledge `id` or `description`).

### Pledge Accounts

#### List all pledge accounts

```
DEFINITION
GET http://apiserver/pledges/:id/accounts

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/FEED2010/accounts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3109",
            "status": "A",
            "accountNumber": 857469,
            "accountName": "John Smith",
            "totalAmount": 150.0000,
            "amountPerGift": 50.0000,
            "numberPledged": 3,
            "totalAmountDonated": 50.0000,
            "frequency": "M",
            "start": "2024-12-19",
            "end": "2025-02-28,
            "openEnded": true,
            "sourceCode": "070000",
            "sourceDescription": "Test",
            "currencyCode": "USD",
            "cancelReasonCode": null,
            "cancelDate": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pledge accounts by id (pledge code).

##### Arguments

* id (required) - Return pledge accounts that contain the following id (pledge code).
* accountNumber (optional) - Filter list by exact match on account number.
* amountPerGift (optional) - Filter list by exact match on amount per gift.
* pledgeFrequency (optional) - Filter list by partial match on pledge frequency.
* startDateBegin (optional) - Filter list to return pledge accounts where the start date occurs on or after the startDateBegin.
* startDateEnd (optional) - Filter list to return pledge accounts where the start date occurs before or on the startDateEnd.
* pledgeStatus (optional) - Filter list by exact match on pledge status.
* originalPledgeId (optional) - Filter list by exact match on original pledge id.
* assignedToAccessor (optional) - Filter list by exact match on assigned to accessor.
* getPageContainingId (optional) - Return the page of pledge accounts that contains the pledge account with this pledgeId (not the same as the id).

##### Returns

A dictionary with an items property that contains an array of up to limit pledge accounts, starting at index offset. Each entry in the array is a separate pledge account object. If no more pledge accounts are available, the resulting array will be empty. This request should never return an error.

### Pledge Attachments

#### Create a pledge attachment

```
DEFINITION
POST http://apiserver/pledges/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/FEED2010/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new pledge attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a pledge attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a pledge attachment

```
DEFINITION
GET http://apiserver/pledges/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/FEED2010/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing pledge attachment. You need only supply the pledge id and pledge attachment id.

##### Arguments

* id (required) - The id of the account attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a pledge attachment object if a valid id was provided.

#### Update a pledge attachment

```
DEFINITION
POST http://apiserver/pledges/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/FEED2010/attachments/49", {
    "type": "LOGO",
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Updates the specified pledge attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the pledge attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a pledge attachment

```
DEFINITION
DELETE http://apiserver/pledges/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/FEED2010/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the pledge attachment id does not exist, this call returns an error.

#### List all pledge attachments

```
DEFINITION
GET http://apiserver/pledges/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/FEED2010/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pledge attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge attachments, starting at index offset. Each entry in the array is a separate pledge attachment object. If no more pledge attachments are available, the resulting array will be empty. This request should never return an error.

### Pledge Categories

#### Create a pledge category

```
DEFINITION
POST http://apiserver/pledges/:pledgeCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/1000000/storeconfigurations/1/categories", {
    "categoryId": 20
});

EXAMPLE RESPONSE
{
    "id": "13",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Creates a new pledge category for the given StudioOnline store configuration.

##### Arguments

* categoryId (required) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns a pledge category object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge category

```
DEFINITION
GET http://apiserver/pledges/:pledgeCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/1000000/storeconfigurations/1/categories/13");

EXAMPLE RESPONSE
{
    "id": "13",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Retrieves the details of an existing pledge category for the given StudioOnline store configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge category to be retrieved.

#### Update a pledge category

```
DEFINITION
POST http://apiserver/pledges/:pledgeCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/1000000/storeconfigurations/1/categories/13", {
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "13",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": true,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}


```

Updates the specified pledge category for the given StudioOnline store configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* categoryId (optional) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns the pledge category object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge category

```
DEFINITION
DELETE http://apiserver/pledges/:pledgeCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/1000000/storeconfigurations/1/categories/13", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge category from the given StudioOnline store configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge category to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge category does not exist, this call returns an error.

#### List all pledge categories

```
DEFINITION
GET http://apiserver/pledges/:pledgeCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/1000000/storeconfigurations/1/categories");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "13",
            "categoryId": "20",
            "categoryName": "Best Sellers",
            "isPrimary": true,
            "isActive": true,
            "breadcrumb": "best-sellers",
            "parentCategoryId": null,
            "parentCategoryName": null
        },
        {...},
    ]
}

```

Returns a list of all pledge categories for the given StudioOnline store configuration.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge categories, starting at index offset. Each entry in the array is a separate pledge category object. If no more pledge categories are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group Checkin

#### Check in a pledge

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/checkin

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/checkin", {
    "pledgeCode": "100008"
});

EXAMPLE RESPONSE
204 No Content

```

Checks in a pledge.

##### Arguments

* pledgeCode (required) - The code of the pledge to be checked in.
* runId (optional) - The runId of the checkout group to check the pledge in for. This is used when multiple checkouts are supported. Which is controlled with control record MULTICHKOT.

##### Returns

Returns a `204 No Content` response.

### Pledge Checkout Group Codes

#### Create a pledge checkout group code

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000429/codes", {
    "type": "COCODE1",
    "value": "COVALUE2"
});

EXAMPLE RESPONSE
{
    "id": "11",
    "type": "COCODE1",
    "typeDescription": null,
    "value": "COVALUE2",
    "valueDescription": "Value 2",
    "isActive": true
}

```

Creates a new pledge checkout group code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active. Default is true.

##### Returns

Returns a pledge checkout group code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge checkout group code

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/codes/11");

EXAMPLE RESPONSE
{
    "id": "11",
    "type": "COCODE1",
    "typeDescription": "Checkout Code 1",
    "value": "COVALUE2",
    "valueDescription": "Value 2",
    "isActive": true
}

```

Retrieves the details of an existing pledge checkout group code. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout group code to be retrieved.

#### Update a pledge checkout group code

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000429/codes/11", {
    "value": "COVALUE1"
});

EXAMPLE RESPONSE
{
    "id": "11",
    "type": "COCODE1",
    "typeDescription": "Checkout Code 1",
    "value": "COVALUE1",
    "valueDescription": "Value 2",
    "isActive": true
}


```

Updates the specified pledge checkout group code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the pledge checkout group code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge checkout group code

```
DEFINITION
DELETE http://apiserver/pledgecheckoutgroups/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckoutgroups/1000000429/codes/11", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout group code. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout group code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout group code does not exist, this call returns an error.

#### List all pledge checkout group codes

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "type": "COCODE1",
            "typeDescription": "Checkout Code 1",
            "value": "COVALUE1",
            "valueDescription": "Value 1",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all pledge checkout group codes.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout group codes, starting at index offset. Each entry in the array is a separate pledge checkout group code object. If no more pledge checkout group codes are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group Criteria

#### List all pledge checkout group criteria

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/criteria

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/criteria?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "criteria": {
            "criteriaArray": [
                {
                    "id": "11072",
                    "checkoutGroupId": "1000000434",
                    "criteriaType": "PLEDGETYPE",
                    "comparisonType": "EQ",
                    "comparisonValue": "CHILD",
                    "processingSequence": 0,
                    "percentage": 0,
                    "isActive": true
                }
            ]
            },
            "criteriaSql": {
                "sqlFromStatement": "SELECT distinct L11.RunId,\r\n\t\t\tL01.PledgeCode  FROM dbo.L01_PledgeMaster as L01 WITH (NOLOCK)\r\n\t\t\tCROSS APPLY [dbo].[GetPledgeCurrentMonthlyAmount]([L01].[PledgeCode]) A10_AMT\r\n\t\t\tCROSS APPLY [dbo].[IsPledgeFullySponsored]([L01].[SingleOrMultipleSponsorship], [L01].[TotalAmountRequiredMonthly], [A10_AMT].[CurrentMonthlyAmount], [A10_AMT].[TotalPledges]) SPONSOR\r\n\t\t\tCROSS APPLY [dbo].[IsPledgeCheckedOut]([L01].[PledgeCode]) CHECKOUT\r\n\t\t\tCROSS APPLY [dbo].[IsPledgeAvailable]([L01].[SingleOrMultipleSponsorship], [L01].[Active], [SPONSOR].[IsFullySponsored], [CHECKOUT].[IsCheckedOut], 1) AVAIL\r\n\t\t\tJOIN dbo.L11_CheckoutRunCriteria as L11 WITH (NOLOCK) ON L01.PledgeType = L11.ComparisonValue ",
                "sqlWhereStatement": "WHERE ([AVAIL].[IsAvailable] = 1 and L11.CriteriaType = 'PLEDGETYPE' and L11.Runid = 1000000434 and NOT EXISTS (SELECT Pledgecode\r\n\t\tFROM dbo.L01cPledgeCodes WITH (NOLOCK)\r\n\t\tWHERE PledgeCode = L01.PledgeCode and CodeType in ('LMHOLD','LCHOLD')) )"
            }
        },
        {...},
    ]
}

```

Returns a list of all pledge checkout group criteria.

##### Arguments

* id (required) - The id of the pledge checkout group to retrieve criteria for.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout group criteria, starting at index offset. Each entry in the array is a separate pledge checkout group criteria object. If no more pledge checkout group criteria are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group Dates

#### Create a pledge checkout group date

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000429/dates", {
    "type": "CODATE1",
    "value": "2015-06-29"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "CODATE1",
    "typeDescription": null,
    "value": "2015-06-29",
    "isActive": true
}

```

Creates a new pledge checkout group date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a pledge checkout group date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge checkout group date

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/dates/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "CODATE1",
    "typeDescription": null,
    "value": "2015-06-29",
    "isActive": true
}

```

Retrieves the details of an existing pledge checkout group date. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout group date to be retrieved.

#### Update a pledge checkout group date

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000429/dates/8", {
    "value": "2015-06-30"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "CODATE1",
    "typeDescription": "Checkout Date 1",
    "value": "2015-06-30",
    "isActive": true
}


```

Updates the specified pledge checkout group date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the pledge checkout group date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge checkout group date

```
DEFINITION
DELETE http://apiserver/pledgecheckoutgroups/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckoutgroups/1000000429/dates/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout group date. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout group date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout group date does not exist, this call returns an error.

#### List all pledge checkout group dates

```
DEFINITION
GET http://apiserver/pledgecheckoutgroup/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroup/1000000429/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "type": "CODATE1",
            "typeDescription": "Checkout Date 1",
            "value": "2015-06-29",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all pledge checkout group dates.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout group dates, starting at index offset. Each entry in the array is a separate pledge checkout group date object. If no more pledge checkout group dates are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group Details

#### List all pledge checkout group details

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000329/details?limit=2&getPageContainingId=11784");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 2,
        "offset": 4,
        "total": 6
    },
    "items": [
        {
            "id": "11784",
            "checkoutGroupId": "1000000329",
            "pledge": "CH1009",
            "pledgeDescription": "Jimmy John",
            "status": "O",
            "statusDescription": "Checked Out",
            "source": "1109A328",
            "sourceDescription": "Donor Mail 2yr Low $10.00",
            "start": "2015-01-27",
            "end": "2015-02-05",
            "expiration": null
        },
        {...},
    ]
}

```

Returns a list of all pledge checkout group details.

##### Arguments

* getPageContainingId (optional) - Will return the page of pledge checkout groups that contains the checkout group detail with this id.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout group details, starting at index offset. Each entry in the array is a separate pledge checkout group detail object. If no more pledge checkout group details are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group Merged Documents

#### Retrieve a pledge checkout group merged document

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/documents/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000329/documents/81382");

EXAMPLE RESPONSE
{
    "id": "81382",
    "checkoutGroupId": "1000000329",
    "sequenceNumber": 5,
    "fileName": "PledgeStatement.docx",
    "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
    "printDate": "2018-07-15T02:31:37 PM"
}

```

Retrieves the details of an existing pledge checkout group merged document. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout group merged document to be retrieved.
* download (optional) - A `true` value will force the `file` to be retrieved as a Base64 string. Otherwise, `file` will be `null`.

#### Delete a pledge checkout group merged document

```
DEFINITION
DELETE http://apiserver/pledgecheckoutgroups/:id/documents/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckoutgroups/1000000329/documents/81382", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout group merged document. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout group merged document to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout group merged document does not exist, this call returns an error.

#### List all pledge checkout group merged documents

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/documents

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000329/documents");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "81382",
            "checkoutGroupId": "1000000329",
            "sequenceNumber": 5,
            "fileName": "PledgeAcknowledgement.docx",
            "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
            "printDate": "2018-07-15T02:31:37 PM"
        },
        { ... },
        { ... }
    ]
}

```

Returns pledge checkout group merged documents for the specified print group.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout group merged documents, starting at index offset. Each entry in the array is a separate pledge checkout group merged document object. If no more pledge checkout group merged documents are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group Notes

#### Create a pledge checkout group note

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000429/notes", {
    "date": "2015-06-30T15:55:43",
    "longComment": "l",
    "shortComment": "s",
    "type": "CONOTE1"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "CONOTE1",
    "typeDescription": null,
    "shortComment": "s",
    "longComment": "l"
}

```

Creates a new pledge checkout group note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a pledge checkout group note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge checkout group note

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/notes/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "CONOTE1",
    "typeDescription": null,
    "shortComment": "s",
    "longComment": "l"
}

```

Retrieves the details of an existing pledge checkout group note. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout group note to be retrieved.

#### Update a pledge checkout group note

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000429/notes/6", {
    "longComment": "long comment"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "CONOTE1",
    "typeDescription": "Checkout Note 1",
    "shortComment": "s",
    "longComment": "long comment"
}


```

Updates the specified pledge checkout group note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the pledge checkout group note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge checkout group note

```
DEFINITION
DELETE http://apiserver/pledgecheckoutgroups/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckoutgroups/1000000429/notes/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout group note. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout group note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout group note does not exist, this call returns an error.

#### List all pledge checkout group notes

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/notes");

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
            "type": "CONOTE1",
            "typeDescription": "Checkout Note 1",
            "shortComment": "s",
            "longComment": "l"
        },
        {...},
    ]
}

```

Returns a list of all pledge checkout group notes.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout group notes, starting at index offset. Each entry in the array is a separate pledge checkout group note object. If no more pledge checkout group notes are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group Numbers

#### Create a pledge checkout group number

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups", {
    "type": "CONUMBER1",
    "value": 55
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "CONUMBER1",
    "typeDescription": null,
    "value": 55,
    "isActive": true
}

```

Creates a new pledge checkout group number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be a defined value of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a pledge checkout group number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge checkout group number

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/numbers/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "CONUMBER1",
    "typeDescription": "Checkout Number 1",
    "value": 55,
    "isActive": true
}

```

Retrieves the details of an existing pledge checkout group number. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout group number to be retrieved.

#### Update a pledge checkout group number

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000429/numbers/6", {
    "value": 56
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "CONUMBER1",
    "typeDescription": "Checkout Number 1",
    "value": 56,
    "isActive": true
}


```

Updates the specified pledge checkout group number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be a defined value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the pledge checkout group number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge checkout group number

```
DEFINITION
DELETE http://apiserver/pledgecheckoutgroups/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckoutgroups/1000000429/numbers/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout group number. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout group number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout group number does not exist, this call returns an error.

#### List all pledge checkout group numbers

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000429/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "type": "CONUMBER1",
            "typeDescription": "Checkout Number 1",
            "value": 59,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all pledge checkout group numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout group numbers, starting at index offset. Each entry in the array is a separate pledge checkout group number object. If no more pledge checkout group numbers are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Group StudioOnline Publish Data

#### Retrieve the pledge checkout group StudioOnline publish data

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000374/studioonlinepublishdata");

EXAMPLE RESPONSE
{
    "id": "1000000374",
    "pageLayout": "PLDGPACK1",
    "categories": [
        {
            "id": "22",
            "type": "ECPLDGCAT",
            "typeDescription": "EC Pledge Category",
            "value": "8",
            "valueDescription": "Pledges",
            "isActive": true
        }
    ]
}

```

Retrieves the details of the existing pledge checkout group StudioOnline publish data. You need only supply the pledge checkout group id.

##### Returns

Returns a pledge checkout group StudioOnline publish data object if a valid id was provided.

#### Update and publish the pledge checkout group StudioOnline publish data

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000374/studioonlinepublishdata", {
    "pageLayout": "PLDGPACK2",
});

EXAMPLE RESPONSE
{
    "id": "1000000374",
    "pageLayout": "PLDGPACK2",
    "categories": [
        {
            "id": "22",
            "type": "ECPLDGCAT",
            "typeDescription": "EC Pledge Category",
            "value": "8",
            "valueDescription": "Pledges",
            "isActive": true
        }
    ]
}


```

Updates and publishes the specified pledge checkout group StudioOnline publish data by setting the values of the parameters passed. Any parameters not provided will be left unchanged. Any categories must already have been updated through the Pledge Checkout Group Codes resource.

##### Arguments

* pageLayout (optional) - The page layout (XML Package) for the pledge checkout group on StudioOnline.

##### Returns

Returns the pledge checkout group StudioOnline publish data object if the update and publish succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined page layout code).

#### Unpublish the pledge checkout group StudioOnline publish data

```
DEFINITION
DELETE http://apiserver/pledgecheckoutgroups/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckoutgroups/1000000374/studioonlinepublishdata", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Unpublishes the pledge checkout group StudioOnline publish data. The actual data will not be deleted.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the pledge checkout group StudioOnline publish data cannot be unpublished, this call returns an error.

### Pledge Checkout Groups

#### Run a pledge checkout group

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups", {
    "description": "Christmas Card Outreach",
    "sourceCode": "070000",
    "sortOrder": "M",
    "criteria": {
        "criteriaArray": [
            "criteriaType": "PLEDGETYPE",
            "comparisonType": "EQ",
            "comparisonValue": "CHILD",
            "isActive": true
        ]
    }
});

EXAMPLE RESPONSE
{
    "isTemporaryCheckoutGroup": null,
    "runCheckout": null,
    "assignCode": null,
    "pledgeType": null,
    "codeType": null,
    "codeValue": null,
    "printProfile": null,
    "sortOrder": "M",
    "criteria": {
        "criteriaArray": [
            {
                "id": "11072",
                "checkoutGroupId": "1000000434",
                "criteriaType": "PLEDGETYPE",
                "comparisonType": "EQ",
                "comparisonValue": "CHILD",
                "processingSequence": 0,
                "percentage": 0,
                "isActive": true
            }
        ]
    },
    "id": "1000000424",
    "description": "Christmas Card Outreach",
    "end": null,
    "expiration": null,
    "quantity": 0,
    "runDate": null,
    "sourceCode": "070000",
    "sourceCodeDescription": null,
    "elementGroup": null,
    "elementGroupDescription": null,
    "start": null,
    "status": null,
    "statusDescription": null,
    "useInShoppingCart": null
}

```

Creates a new pledge checkout group.

##### Arguments

* description (required) - The description of the checkout group. Is not used for temporary checkout groups.
* sourceCode (required) - The id of the source code for the checkout group. Is not used for temporary checkout groups.
* sortOrder (required) - The sort order for multi-sponsor pledges. (Allowed values are "M": most pledges needed, "L": least pledges needed) Is not used for temporary checkout groups.
* start (required) - Start date of the checkout group. Is not used for temporary checkout groups.
* end (required) - End date (Respond by date) of the checkout group. Is not used for temporary checkout groups.
* expiration (required) - Expiration date of the checkout group. Is not used for temporary checkout groups.
* quantity (required) - The number of pledges to include in the checkout group.
* isTemporaryCheckoutGroup (optional) - Intended for use with Account Pledges Sponsorship lookup, if the checkout group is temporary then the description, sourceCode, sortOrder, start, end, and expiration are not required.
* runCheckout (optional) - Indicates whether to run the checkout. Is not used for temporary checkout groups.
* assignCode (optional) - Indicates whether to assign a code. Is not used for temporary checkout groups.
* pledgeType (optional) - The pledge type of the code to assign. Used with assignCode, must be provided when assignCode is true. Is not used for temporary checkout groups.
* codeType (optional) - The type of the code to assign. Used with assignCode, must be provided when assignCode is true. Is not used for temporary checkout groups.
* codeValue (optional) - The value of the code to assign. Used with assignCode, must be provided when assignCode is true. Is not used for temporary checkout groups.
* printProfile (optional) - Determines whether to print the profile. Must not be true unless runCheckout is true. Is not used for temporary checkout groups.
* useInShoppingCart (optional) - Indicates whether to use the checkout group in StudioOnline. Is not used for temporary checkout groups.
* criteria (optional) - Object containing criteriaArray which is an array of objects. Each of these objects should have criteriaType, comparisonType, comparisonValue, and isActive.

##### Returns

Returns a pledge checkout group object if the call succeeded. Returns an error if create parameters are invalid.

#### Rerun a pledge checkout group

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/rerun

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000446/rerun");

EXAMPLE RESPONSE
204 No Content

```

Reruns an existing pledge checkout group. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout group to rerun.

#### Retrieve a pledge checkout group

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups/1000000434");

EXAMPLE RESPONSE
{
    "id": "1000000434",
    "description": "Christmas Card Outreach",
    "end": null,
    "expiration": null,
    "quantity": 1,
    "runDate": "2015-06-29",
    "sourceCode": "070000",
    "sourceCodeDescription": "Test",
    "elementGroup": null,
    "elementGroupDescription": null,
    "start": null,
    "status": null,
    "statusDescription": null,
    "useInShoppingCart": false
}

```

Retrieves the details of an existing pledge checkout group. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout group to be retrieved.

#### Print profiles for a pledge checkout group

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id/printprofile

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000434/printprofile", {
    "shouldCreatePrintGroup": false
});

EXAMPLE RESPONSE
{
    "runId": 1000000434,
    "formType": {
        "id": "123456",
        "formType": "PLDGPROF",
        "description": "BP-PledgeProfile-Print",
        "communicationType": "PLDGPROFL",
        "communicationTypeDescription": "Pledge Profiles",
        "deliveryMethod": "NOTEMAIL",
        "deliveryMethodDescription": "Not Email",
        "isDocumentMergedOnServer": false,
        "maxMergedDocumentRecordCount": null,
        "dataSource": "C:\test.ods",
        "documentFilterQuery": "SELECT * FROM \"L12_CheckoutPrintGroup\" WHERE RunId = {RunId}",
        "isActive": true,
        "emailSubject": null,
        "documents": [
            "C:\test\path\doc1.docx",
            "C:\test\path\doc2.docx"
        ],
        "documentCollection": [
            {
                "id": "20117",
                "sequenceNumber": 1,
                "documentAddress": "C:\test\path\doc1.docx",
                "reportId": null,
                "reportDescription": null
            },
            {
                "id": "20118",
                "sequenceNumber": 2,
                "documentAddress": "C:\test\path\doc2.docx",
                "reportId": null,
                "reportDescription": null
            }
        ]
    }
}

```

Performs a checkout on the print group if requested and returns the form type to use for mail merge.

##### Arguments

* shouldCreatePrintGroup (optional) - Indicates whether to create the print group. Standard usage is to send false for newly created groups and true for existing groups. Default value is false.

##### Returns

Returns the ID of the checkout group run and the Pledge Profile Form Type if successful. If no control record exists for Pledge Profile Form Type or the Form Type does not have a NOTEMAIL Delivery Method, this call will return an error.

#### Update a pledge checkout group

```
DEFINITION
POST http://apiserver/pledgecheckoutgroups/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckoutgroups/1000000434", {
    "description": "Christmas Card Outreach 2015"
});

EXAMPLE RESPONSE
{
    "id": "1000000434",
    "description": "Christmas Card Outreach 2015",
    "end": null,
    "expiration": null,
    "quantity": 1,
    "runDate": "2015-06-29",
    "sourceCode": "070000",
    "sourceCodeDescription": "Test",
    "elementGroup": null,
    "elementGroupDescription": null,
    "start": null,
    "status": null,
    "statusDescription": null,
    "useInShoppingCart": false
}


```

Updates the specified pledge checkout group by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the checkout group.
* sourceCode (optional) - The id of the source code for the checkout group.
* quantity (optional) - The number of pledges to include in the checkout group.
* start (optional) - Start date of the checkout group.
* end (optional) - End date (Respond by date) of the checkout group.
* expiration (optional) - Expiration date of the checkout group.
* useInShoppingCart (optional) - Indicates whether to use the checkout group in StudioOnline.
* status (optional) - The status of the checkout group.

##### Returns

Returns the pledge checkout group object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge checkout group

```
DEFINITION
DELETE http://apiserver/pledgecheckoutgroups/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckoutgroups/1000000434", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout group. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout group to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout group does not exist, this call returns an error.

#### List all pledge checkout groups

```
DEFINITION
GET http://apiserver/pledgecheckoutgroups

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckoutgroups?sourceCode=070000");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000000434",
            "description": "Christmas Card Outreach 2015",
            "end": null,
            "expiration": null,
            "quantity": 1,
            "runDate": "2015-06-29",
            "sourceCode": "070000",
            "sourceCodeDescription": "Test",
            "elementGroup": null,
            "elementGroupDescription": null,
            "start": null,
            "status": null,
            "statusDescription": null,
            "useInShoppingCart": false
        },
        {...},
    ]
}

```

Returns a list of all pledge checkout groups.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout groups, starting at index offset. Each entry in the array is a separate pledge checkout object. If no more pledge checkout groups are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Template Details

#### Create a pledge checkout template detail

```
DEFINITION
POST http://apiserver/pledgecheckouttemplates/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckouttemplates/1000000010/details", {
    "comparisonType": "EQ",
    "comparisonValue": "25",
    "criteriaType": "AGE",
    "percentage": "12"
});

EXAMPLE RESPONSE
{
    "id": "67",
    "criteriaType": "AGE",
    "processingSequence": 0,
    "comparisonType": "EQ",
    "comparisonValue": "25",
    "percentage": 12,
    "isActive": true
}

```

Creates a new pledge checkout template detail.

##### Arguments

* criteriaType (required) - A valid criteria Type.
* comparisonType (required) - A valid comparison type for the provided criteria type.
* comparisonValue (required) - A valid comparison value for the provided comparison type.
* isActive (optional) - Whether or not the detail record is active. Defaults to true.
* processingSequence (optional) - If multiple detail records exist, the order of processing.
* percentage (optional) - Percentage for the detail.

##### Returns

Returns a pledge checkout template detail object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge checkout template detail

```
DEFINITION
GET http://apiserver/pledgecheckouttemplates/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckouttemplates/1000000010/details/72");

EXAMPLE RESPONSE
{
    "id": "72",
    "criteriaType": "AGE",
    "processingSequence": 55,
    "comparisonType": "EQ",
    "comparisonValue": "25",
    "percentage": 12,
    "isActive": true
}

```

Retrieves the details of an existing pledge checkout template detail. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout template detail to be retrieved.

#### Update a pledge checkout template detail

```
DEFINITION
POST http://apiserver/pledgecheckouttemplates/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckouttemplates/1000000010/details/72", {
    "processingSequence": 59
});

EXAMPLE RESPONSE
{
    "id": "72",
    "criteriaType": "AGE",
    "processingSequence": 59,
    "comparisonType": "EQ",
    "comparisonValue": "25",
    "percentage": 12,
    "isActive": true
}


```

Updates the specified pledge checkout template detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* criteriaType (optional) - A valid criteria Type.
* comparisonType (optional) - A valid comparison type for the provided criteria type.
* comparisonValue (optional) - A valid comparison value for the provided comparison type.
* isActive (optional) - Whether or not the detail record is active. Defaults to true.
* processingSequence (optional) - If multiple detail records exist, the order of processing.
* percentage (optional) - Percentage for the detail.

##### Returns

Returns the pledge checkout template detail object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge checkout template detail

```
DEFINITION
DELETE http://apiserver/pledgecheckouttemplates/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckouttemplates/1000000010/details/72", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout template detail. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout template detail to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout template detail does not exist, this call returns an error.

#### List all pledge checkout template details

```
DEFINITION
GET http://apiserver/pledgecheckouttemplates/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckouttemplates/7/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    }
    "items": [
        {
            "id": "8",
            "criteriaType": "PLEDGETYPE",
            "processingSequence": 0,
            "comparisonType": "EQ",
            "comparisonValue": "CHILD",
            "percentage": 0,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pledge checkout template details for the provded pledge checkout template.

##### Arguments

* id (required) - pledge checkout template unique identifier

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout template details, starting at index offset. Each entry in the array is a separate pledge checkout template detail object. If no more pledge checkout template details are available, the resulting array will be empty. This request should never return an error.

### Pledge Checkout Templates

#### Create a pledge checkout template

```
DEFINITION
POST http://apiserver/pledgecheckouttemplates

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckouttemplates", {
    "description": "Teamplate",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "1000000017",
    "description": "Teamplate",
    "isActive": true
}

```

Creates a new pledge checkout template.

##### Arguments

* description (required) - description of the pledge checkout template
* isActive (optional) - indicates whether the pledge checkout template is active. true by default

##### Returns

Returns a pledge checkout template object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge checkout template

```
DEFINITION
GET http://apiserver/pledgecheckout/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckout/1000000017");

EXAMPLE RESPONSE
{
    "id": "1000000017",
    "description": "Teamplate",
    "isActive": true
}

```

Retrieves the details of an existing pledge checkout template. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge checkout template to be retrieved.

#### Update a pledge checkout template

```
DEFINITION
POST http://apiserver/pledgecheckouttemplates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecheckouttemplates/1000000017", {
    "description": "Template 1"
});

EXAMPLE RESPONSE
{
    "id": "1000000017",
    "description": "Template 1",
    "isActive": true
}


```

Updates the specified pledge checkout template by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - description of the pledge checkout template
* isActive (optional) - indicates whether the pledge checkout template is active

##### Returns

Returns the pledge checkout template object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge checkout template

```
DEFINITION
DELETE http://apiserver/pledgecheckouttemplates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecheckouttemplates/1000000017", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge checkout template. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge checkout template to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge checkout template does not exist, this call returns an error.

#### List all pledge checkout templates

```
DEFINITION
GET http://apiserver/pledgecheckouttemplates

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecheckouttemplates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 8
    }
    "items": [
        {
            "id": "7",
            "description": "Mix of Boys and Girls",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pledge checkout templates.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* description (optional) - Filters list based on pledge checkout template description
* isActive (optional) - Filters list based on if active or not, defaults to true.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge checkout templates, starting at index offset. Each entry in the array is a separate pledge checkout template object. If no more pledge checkout templates are available, the resulting array will be empty. This request should never return an error.

### Pledge Criteria Types

#### Create a pledge criteria type

```
DEFINITION
POST http://apiserver/pledgecriteriatypes

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecriteriatypes", {
    "id": "PLGDESC",
    "description": "Pledge Description",
    "category": "PLEDGES",
    "dataType": "STRING",
    "tableId": "L01",
    "field": "DESCRIPTION",
    "isActive": true,
    "isSearchableInStudioOnline": false
});

EXAMPLE RESPONSE
{
    "id": "PLGDESC",
    "description": "Pledge Description",
    "category": "PLEDGES",
    "dataType": "STRING",
    "tableId": "L01",
    "field": "DESCRIPTION",
    "codeType": null,
    "isActive": true,
    "isSearchableInStudioOnline": false
}

```

Creates a new pledge criteria type.

##### Arguments

* id (required) - The criteria type.
* description (required) - The description of the criteria type.
* category (required) - The category of the criteria type.
* dataType (required) - The data type of the criteria type. (Some possible values are "DATE", "AMOUNT", "STRING", "ACCESSOR".)
* tableId (required) - The database table id of the criteria type.
* field (optional) - The database field or column of the criteria type.
* codeType (optional) - The code type of the criteria type.
* isActive (optional) - Whether the criteria type is active. (If not provided, isActive will be defaulted to 'true'.)
* isSearchableInStudioOnline (optional) - Indicates whether the criteria type is able to be searched in StudioOnline. (If not provided, isSearchableInStudioOnline will be defaulted to 'false'.)

##### Returns

Returns a pledge criteria type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge criteria type

```
DEFINITION
GET http://apiserver/pledgecriteriatypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecriteriatypes/age");

EXAMPLE RESPONSE
{
    "id": "AGE",
    "description": "Age",
    "category": "BDCALC",
    "dataType": "AMOUNT",
    "tableId": "L01d",
    "field": null,
    "codeType": "AGE",
    "isActive": true,
    "isSearchableInStudioOnline": false
}

```

Retrieves the details of an existing pledge criteria type. You need only supply the pledge criteria type.

##### Arguments

* id (required) - The pledge criteria type to retrieve.

##### Returns

Returns a pledge criteria type object if a valid id was provided.

#### Update a pledge criteria type

```
DEFINITION
POST http://apiserver/pledgecriteriatypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgecriteriatypes/plgdesc", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "PLGDESC",
    "description": "Pledge Description",
    "category": "PLEDGES",
    "dataType": "STRING",
    "tableId": "L01",
    "field": "DESCRIPTION",
    "codeType": null,
    "isActive": false,
    "isSearchableInStudioOnline": false
}


```

Updates the specified pledge criteria type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the criteria type.
* category (optional) - The category of the criteria type.
* dataType (optional) - The data type of the criteria type. (Some possible values are "DATE", "AMOUNT", "STRING", "ACCESSOR".)
* tableId (optional) - The database table id of the criteria type.
* field (optional) - The database field or column of the criteria type.
* codeType (optional) - The code type of the criteria type.
* isActive (optional) - Whether the criteria type is active. (If not provided, isActive will be defaulted to 'true'.)
* isSearchableInStudioOnline (optional) - Indicates whether the criteria type is able to be searched in StudioOnline.

##### Returns

Returns the pledge criteria type object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge criteria type

```
DEFINITION
DELETE http://apiserver/pledgecriteriatypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgecriteriatypes/plgdesc", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge criteria type. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge criteria type to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge criteria type does not exist, this call returns an error.

#### List all pledge criteria types

```
DEFINITION
GET http://apiserver/pledgecriteriatypes

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgecriteriatypes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 33
    }
    "items": [
        {
            "id": "AGE",
            "description": "Age",
            "category": "BDCALC",
            "dataType": "AMOUNT",
            "tableId": "L01d",
            "field": null,
            "codeType": "AGE",
            "isActive": true,
            "isSearchableInStudioOnline": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pledge criteria types matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filters list by exact match on id (criteria type).
* category () - Filters list by partial match on category.
* description () - Filters list by partial match on description.
* codeType () - Filters list by partial match on codeType.
* isActive () - Filters list based on if active or not.
* isSearchableInStudioOnline () - Filters list based on if searchable in StudioOnline.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge criteria types, starting at index offset. Each entry in the array is a separate pledge criteria type object. If no more pledge criteria types are available, the resulting array will be empty. This request should never return an error.

### Pledge Codes

#### Create a pledge code

```
DEFINITION
POST http://apiserver/pledges/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/codes", {
    "type": "CHILDCOMM",
    "value": "PE"
});

EXAMPLE RESPONSE
{
    "id": "20707",
    "type": "CHILDCOMM",
    "typeDescription": "Location Code",
    "value": "PE",
    "valueDescription": "Peru",
    "isActive": true
}

```

Creates a new pledge code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a pledge code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge code

```
DEFINITION
GET http://apiserver/pledges/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/CHILD2010/codes/20707");

EXAMPLE RESPONSE
{
    "id": "20707",
    "type": "CHILDCOMM",
    "typeDescription": "Location Code",
    "value": "PE",
    "valueDescription": "Peru",
    "isActive": true
}

```

Retrieves the details of an existing pledge code. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge code to be retrieved.

#### Update a pledge code

```
DEFINITION
POST http://apiserver/pledges/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/codes/20707", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "20707",
    "type": "CHILDCOMM",
    "typeDescription": "Location Code",
    "value": "PE",
    "valueDescription": "Peru",
    "isActive": false
}


```

Updates the specified pledge code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type - The code type. Must be a defined code type.
* value - The value of the code type. Must be a defined value of the code type.
* isActive - Whether or not the code is active.

##### Returns

Returns the pledge code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge code

```
DEFINITION
DELETE http://apiserver/pledges/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/CHILD2010/codes/20707", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge code. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge code does not exist, this call returns an error.

#### List All Pledge Codes

```
DEFINITION
GET http://apiserver/pledges/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/FEED2010/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "20707",
            "type": "CHILDCOMM",
            "typeDescription": "Location Code",
            "value": "PE",
            "valueDescription": "Peru",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

### Pledge Dates

#### Create a pledge date

```
DEFINITION
POST http://apiserver/pledges/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/dates", {
    "type": "DDCCHLDBD",
    "value": "2001-02-03"
});

EXAMPLE RESPONSE
{
    "id": "20094",
    "type": "DDCCHLDBD",
    "typeDescription": "Birth Date",
    "value": "2001-02-03",
    "isActive": true
}

```

Creates a new pledge date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a pledge date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge date

```
DEFINITION
GET http://apiserver/pledges/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/CHILD2010/dates/20094");

EXAMPLE RESPONSE
{
    "id": "20094",
    "type": "DDCCHLDBD",
    "typeDescription": "Birth Date",
    "value": "2001-02-03",
    "isActive": true
}

```

Retrieves the details of an existing pledge date. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge date to be retrieved.

#### Update a pledge date

```
DEFINITION
POST http://apiserver/pledges/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/dates/20094", {
    "value": "2000-02-05"
});

EXAMPLE RESPONSE
{
    "id": "20094",
    "type": "DDCCHLDBD",
    "typeDescription": "Birth Date",
    "value": "2000-02-05",
    "isActive": true
}


```

Updates the specified pledge date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type - The date type. Must be a defined date type.
* value - The value of the date type. Must be within an active range of the specified date type.
* isActive - Whether or not the date is active.

##### Returns

Returns the pledge date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge date

```
DEFINITION
DELETE http://apiserver/pledges/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/CHILD2010/dates/20094", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge date. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge date does not exist, this call returns an error.

#### List all pledge dates

```
DEFINITION
GET http://apiserver/pledges/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/CHILD2010/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20094",
            "type": "DDCCHLDBD",
            "typeDescription": "Birth Date",
            "value": "2000-02-05",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all pledge dates.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge dates, starting at index offset. Each entry in the array is a separate pledge date object. If no more pledge dates are available, the resulting array will be empty. This request should never return an error.

### Pledge Images

#### Create a pledge image

```
DEFINITION
POST http://apiserver/pledges/:pledgeId/images

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/200CHILD/images", {
    "imageType": "IMAGEXS",
    "description": "Xtra Small Pledge Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image",
    "title": "Image Title",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Pledge Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Creates a new pledge image.

##### Arguments

* imageType (required) - the ImageType code value for the pledge image.
* description (optional) - the description for the pledge image.
* imageUrl (required) - the image URL for the pledge image.
* alternateText (optional) - the alternate text for the pledge image.
* title (optional) - the image title for the pledge image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns a pledge image object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge image

```
DEFINITION
GET http://apiserver/pledges/:pledgeId/images/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/200CHILD/images/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Pledge Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Retrieves the details of an existing pledge image. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge image to be retrieved.

#### Update a pledge image

```
DEFINITION
POST http://apiserver/pledges/:pledgeId/images/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/200CHILD/images/6", {
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Pledge Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}


```

Updates the specified pledge image by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* imageType (optional) - the ImageType code value to update for the pledge image.
* description (optional) - the description to update for the pledge image.
* imageUrl (optional) - the image URL to update for the pledge image.
* alternateText (optional) - the alternate text to update for the pledge image.
* title (optional) - the image title to update for the pledge image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns the pledge image object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge image

```
DEFINITION
DELETE http://apiserver/pledges/:pledgeId/images/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/200CHILD/images/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge image. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge image to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge image does not exist, this call returns an error.

#### List all pledge images

```
DEFINITION
GET http://apiserver/pledges/:pledgeId/images

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/200CHILD/images");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 9
    },
    "items": [
        {
            "id": "6",
            "imageType": "IMAGEXS",
            "imageTypeDescription": "Extra Small Image",
            "description": "Xtra Small Pledge Img",
            "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
            "alternateText": "Image Alt Text",
            "title": "Image Title",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all pledge images by pledge code.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge images, starting at index offset. Each entry in the array is a separate pledge image object. If no more pledge images are available, the resulting array will be empty. This request should never return an error.

### Pledge Notes

#### Create a pledge note

```
DEFINITION
POST http://apiserver/pledges/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/notes", {
    "type": "CHLDNOTE",
    "shortComment": "Child Update",
    "longComment": "Child has moved to a new community."
});

EXAMPLE RESPONSE
{
    "id": "49",
    "type": "CHLDNOTE",
    "typeDescription": "Child Note",
    "shortComment": "Child Update",
    "longComment": "Child has moved to a new community."
}

```

Creates a new pledge note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a pledge note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge note

```
DEFINITION
GET http://apiserver/pledges/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/CHILD2010/notes/49");

EXAMPLE RESPONSE
{
    "id": "49",
    "type": "CHLDNOTE",
    "typeDescription": "Child Note",
    "shortComment": "Child Update",
    "longComment": "Child has moved to a new community."
}

```

Retrieves the details of an existing pledge note. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge note to be retrieved.

#### Update a pledge note

```
DEFINITION
POST http://apiserver/pledges/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/notes/49", {
    "longComment": "Child has moved to a new community.  Please update child profile."
});

EXAMPLE RESPONSE
{
    "id": "49",
    "type": "CHLDNOTE",
    "typeDescription": "Child Note",
    "shortComment": "Child Update",
    "longComment": "Child has moved to a new community.  Please update child profile."
}


```

Updates the specified pledge note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type - The note type. Must be a defined note type.
* shortComment - The short comment of the note.
* longComment - The long comment of the note.

##### Returns

Returns the pledge note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge note

```
DEFINITION
DELETE http://apiserver/pledges/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/CHILD2010/notes/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge note. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge note does not exist, this call returns an error.

#### List all pledge notes

```
DEFINITION
GET http://apiserver/pledges/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/CHILD2010/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "49",
            "type": "CHLDNOTE",
            "typeDescription": "Child Note",
            "shortComment": "Child Update",
            "longComment": "Child has moved to a new community.  Please update child profile."
        },
        {...},
    ]
}

```

Returns a list of all pledge notes.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge notes, starting at index offset. Each entry in the array is a separate pledge note object. If no more pledge notes are available, the resulting array will be empty. This request should never return an error.

### Pledge Numbers

#### Create a pledge number

```
DEFINITION
POST http://apiserver/pledges/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/numbers", {
    "type": "CHLDNBRBRO",
    "value": 3
});

EXAMPLE RESPONSE
{
    "id": "10111",
    "type": "CHLDNBRBRO",
    "typeDescription": "Number of Brothers",
    "value": 3,
    "isActive": true
}

```

Creates a new pledge number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a pledge number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge number

```
DEFINITION
GET http://apiserver/pledges/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/CHILD2010/numbers/10111");

EXAMPLE RESPONSE
{
    "id": "10111",
    "type": "CHLDNBRBRO",
    "typeDescription": "Number of Brothers",
    "value": 3,
    "isActive": true
}

```

Retrieves the details of an existing pledge number. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge number to be retrieved.

#### Update a pledge number

```
DEFINITION
POST http://apiserver/pledges/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/CHILD2010/numbers/10111", {
    "value": 4
});

EXAMPLE RESPONSE
{
    "id": "10111",
    "type": "CHLDNBRBRO",
    "typeDescription": "Number of Brothers",
    "value": 4,
    "isActive": true
}

```

Updates the specified pledge number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type - The number type. Must be a defined number type.
* value - The value of the number type. Must be within an active range of the specified number type.
* isActive - Whether or not the number is active.

##### Returns

Returns the pledge number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge number

```
DEFINITION
DELETE http://apiserver/pledges/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/CHILD2010/numbers/10111", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge number. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge number does not exist, this call returns an error.

#### List all pledge numbers

```
DEFINITION
GET http://apiserver/pledges/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/CHILD2010/numbers?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10111",
            "type": "CHLDNBRBRO",
            "typeDescription": "Number of Brothers",
            "value": 4,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all pledge numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge numbers, starting at index offset. Each entry in the array is a separate pledge number object. If no more pledge numbers are available, the resulting array will be empty. This request should never return an error.

### Pledge Premiums

#### Retrieve a pledge premium

```
DEFINITION
GET http://apiserver/pledges/:id/premiums/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/FEED2010/premiums/8290");

EXAMPLE RESPONSE
{
    "id": "8290",
    "warehouse": "UKWH",
    "product": "BK-5SLVG",
    "quantity": 1,
    "shippingMethod": "2DAY",
    "fulfillmentActivity": "1",
    "amount": null,
    "isAutoAdd": false
}

```

Retrieves the details of an existing pledge premium. You need only supply the pledge premium code.

##### Arguments

* id (required) - The pledge premium code of the pledge premium to retrieve.

##### Returns

Returns a pledge premium object if a valid id was provided.

#### List all pledge premiums

```
DEFINITION
GET http://apiserver/pledges/:id/premiums

EXAMPLE REQUEST
$.get("http://localhost:49195/pledge/FEED2010/premiums");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    }
    "items": [
        {
            "id": "8290",
            "warehouse": "UKWH",
            "product": "BK-5SLVG",
            "quantity": 1,
            "shippingMethod": "2DAY",
            "fulfillmentActivity": "1",
            "amount": null,
            "isAutoAdd": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pledge premiums matching the provided filter criteria.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge premiums, starting at index offset. Each entry in the array is a separate pledge premium object. If no more pledge premiums are available, the resulting array will be empty. This request should never return an error.

### Pledge Selections

#### Run a pledge selection

```
DEFINITION
POST http://apiserver/pledgeselections

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgeselections", {
    "description": "Active Not Checked Out",
    "active": "Y",
    "sponsored": "A",
    "checkedOut": "N",
    "criteria": [
        {
            "criteriaType": "PLEDGETYPE",
            "comparisonType": "EQ",
            "comparisonValue": "CHILD"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "7",
    "runDate": "2015-10-26",
    "description": "Active Not Checked Out",
    "quantity": 74,
    "active": "Y",
    "sponsored": "A",
    "checkedOut": "N"
}

```

Creates and runs a new pledge selection.

##### Arguments

* description (required) - The description of the pledge selection.
* active (optional) - Indicates if the group should be filtered on active, must be 'Y', 'N', or 'A' for 'Yes', 'No', or 'All', respectively.
* sponsored (optional) - Indicates if the group should be filtered on sponsored, must be 'Y', 'N', or 'A' for 'Yes', 'No', or 'All', respectively.
* checkedOut (optional) - Indicates if the group should be filtered on checked out, must be 'Y', 'N', or 'A' for 'Yes', 'No', or 'All', respectively.
* criteria (optional) - The criteria to filter the group on. An array of criteria objects, each of which should have criteriaType, comparisonType, and comparisonValue.

##### Returns

Returns a pledge selection object if the call succeeded. Returns an error if create parameters are invalid.

#### Rerun a pledge selection

```
DEFINITION
POST http://apiserver/pledgeselections/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgeselections/7", {});

EXAMPLE RESPONSE
204 No Content

```

Reruns a pledge selection.

##### Arguments

* id (required) - The id of the pledge selection to be rerun.

##### Returns

Returns a `204 No Content` response on success. If the pledge selection does not exist, this call returns an error.

#### Retrieve a pledge selection

```
DEFINITION
GET http://apiserver/pledgeselections/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgeselections/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "runDate": "2015-10-26",
    "description": "Active Not Checked Out",
    "quantity": 74,
    "active": "Y",
    "sponsored": "A",
    "checkedOut": "N",
    "criteria": [
        {
            "id": "5",
            "runId": "7",
            "criteriaType": "PLEDGETYPE",
            "comparisonType": "EQ",
            "comparisonValue": "CHILD"
        }
    ],
    "sqlFrom": "SELECT distinct L19.RunId,\r\n                L01.PledgeCode  FROM dbo.L01_PledgeMaster as L01 WITH (NOLOCK),\n               dbo.L19_PledgeSelectionRunCriteria as L19 WITH (NOLOCK) ",
    "sqlWhere": "WHERE (L01.Active = 1 and L19.CriteriaType = 'PLEDGETYPE' and L01.PledgeType = L19.ComparisonValue  and L19.Runid = 7 and\r\n   \r\n\t     NOT EXISTS (SELECT PledgeCode \r\n\t\t\tFROM dbo.L01gCheckoutHistory WITH (NOLOCK)\r\n\t\t\t  WHERE RecordId = (select max(RecordId)\r\n\t\t\t\tFROM dbo.L01gCheckoutHistory WITH (NOLOCK)\n\t\t\t\t  WHERE PledgeCode =  L01.PledgeCode) and Status = 'O' ))"
}

```

Retrieves the details of an existing pledge selection. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge selection to be retrieved.

#### Delete a pledge selection

```
DEFINITION
DELETE http://apiserver/pledgeselections/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgeselections/7", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge selection. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge selection to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge selection does not exist, this call returns an error.

#### List all pledge selections

```
DEFINITION
GET http://apiserver/pledgeselections

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgeselections?description=Active");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "runDate": "2015-10-26",
            "description": "Active Not Checked Out",
            "quantity": 74,
            "active": "Y",
            "sponsored": "A",
            "checkedOut": "N"
        },
        {...},
    ]
}

```

Returns a list of all pledge selections.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* description (optional) - Filters the list by partial match on description.
* groupId (optional) - Filters the list by exact match on pledge selection id.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge selections, starting at index offset. Each entry in the array is a separate pledge selection object. If no more pledge selections are available, the resulting array will be empty. This request should never return an error.

### Pledge Selection Details

#### Retrieve a pledge selection detail

```
DEFINITION
GET http://apiserver/pledgeselections/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgeselections/7/details/100009");

EXAMPLE RESPONSE
{
    "id": "100009",
    "pledgeDescription": "Bob Builder"
}

```

Retrieves the details of an existing pledge selection detail. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge selection detail to be retrieved.

#### List all pledge selection details

```
DEFINITION
GET http://apiserver/pledgeselections/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgeselections/7/details?getPageContainingId=100009");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "100009",
            "pledgeDescription": "Bob Builder"
        },
        {...},
    ]
}

```

Returns a list of all pledge selection details.

##### Arguments

* getPageContainingId (optional) - Will return the page of pledge selections that contains the pledge selection detail with this id.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge selection details, starting at index offset. Each entry in the array is a separate pledge selection detail object. If no more pledge selection details are available, the resulting array will be empty. This request should never return an error.

### Pledge Sponsorship Communications

#### Create a Pledge Sponsorship Communication

```

DEFINITION
POST http://apiserver/pledgesponsorshipcommunications

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgesponsorshipcommunications", {
    "accountNumber":"42820",
    "pledgeCode":"220102",
    "type":"D",
    "sourceCode":"0_A_B_C_M",
    "contactMethod":"WEB",
    "communication":"Test Test",
    "status":"T",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":null,
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797"
});

EXAMPLE RESPONSE
{
    "id":"6",
    "accountNumber":"42820",
    "formattedName": "Robert Jameson",
    "pledgeCode":"220102",
    "pledgeCodeDescription": "Sanjay in India",
    "type":"D",
    "typeDescription":"Donor To Child",
    "sourceCode":"0_A_B_C_M",
    "sourceCodeDescription":"Zero",
    "contactMethod":"WEB",
    "contactMethodDescription":"Website",
    "communication":"Test Test",
    "status":"T",
    "statusDescription":"Translated",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":null,
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797",
    "accessorName":"Nathan Johnson - Internal User"
}

```

Creates a new sponsorship communication.

##### Arguments

* accountNumber (required) - The account number for the account sponsorship communication
* pledgeCode (required) - The pledge code for the account sponsorship communication
* type (required) - Type of communication
* sourceCode (optional) - Source code for the pledge
* contactMethod (optional) - Contact method for the account
* status (required) - Status of communication
* communication (optional) - Communication data
* dateCreated (required) - Communication created date
* dateApproved (optional) - Communication approved date
* dateTranslated (optional) - Communication translated date
* dateSent (optional) - Communication sent date
* dateDelivered (optional) - Communication delivered date
* dateCanceled (optional) - Communication canceled date
* assignedToAccessorId (optional) - Assigned accessor id

##### Returns

Returns a communication object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Pledge Sponsorship Communication

```
DEFINITION
GET http://apiserver/pledgesponsorshipcommunications/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgesponsorshipcommunications/6");

EXAMPLE RESPONSE
{
    "id":"6",
    "accountNumber":"42820",
    "formattedName": "Robert Jameson",
    "pledgeCode":"220102",
    "pledgeCodeDescription": "Sanjay in India",
    "type":"D",
    "typeDescription":"Donor To Child",
    "sourceCode":"0_A_B_C_M",
    "sourceCodeDescription":"Zero",
    "contactMethod":"WEB",
    "contactMethodDescription":"Website",
    "communication":"Test Test",
    "status":"T",
    "statusDescription":"Translated",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":null,
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797",
    "accessorName":"Nathan Johnson - Internal User"
}

```

Retrieves the details of an existing sponsorship communication. You need only supply the id.

##### Arguments

* id (required) - Id of the sponsorship communication to retrieve

#### Update a Pledge Sponsorship Communication

```
DEFINITION
POST http://apiserver/pledgesponsorshipcommunications/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgesponsorshipcommunications/6", {
    "dateTranslated": "2018-10-31"
});

EXAMPLE RESPONSE
{
    "id":"6",
    "accountNumber":"42820",
    "formattedName": "Robert Jameson",
    "pledgeCode":"220102",
    "pledgeCodeDescription": "Sanjay in India",
    "type":"D",
    "typeDescription":"Donor To Child",
    "sourceCode":"0_A_B_C_M",
    "sourceCodeDescription":"Zero",
    "contactMethod":"WEB",
    "contactMethodDescription":"Website",
    "communication":"Test Test",
    "status":"T",
    "statusDescription":"Translated",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":"2018-10-31",
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797",
    "accessorName":"Nathan Johnson - Internal User"
}


```

Updates the specified sponsorship communication by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* accountNumber (optional) - The account number for the account sponsorship communication
* pledgeCode (optional) - The pledge code for the account sponsorship communication
* type (optional) - Type of communication
* sourceCode (optional) - Source code for the pledge
* contactMethod (optional) - Contact method for the account
* status (optional) - Status of communication
* communication (optional) - Communication data
* dateCreated (optional) - Communication created date
* dateApproved (optional) - Communication approved date
* dateTranslated (optional) - Communication translated date
* dateSent (optional) - Communication sent date
* dateDelivered (optional) - Communication delivered date
* dateCanceled (optional) - Communication canceled date
* assignedToAccessorId (optional) - Assigned accessor id

##### Returns

Returns the communication object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Pledge Sponsorship Communication

```
DEFINITION
DELETE http://apiserver/pledgesponsorshipcommunications/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgesponsorshipcommunications/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a communication. It cannot be undone.

##### Arguments

* id (required) - The id of the communication to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the communication does not exist, this call returns an error.

#### List all Pledge Sponsorship Communications

```

DEFINITION
GET http://apiserver/pledgesponsorshipcommunications

EXAMPLE REQUEST
$.get("http://localhost:8000/api/pledgesponsorshipcommunications?offset=0&limit=5", {});

EXAMPLE RESPONSE
{
    "paging":    {
                    "limit":5,
                    "offset":0,
                    "total":13
                },
    "items":    [
                    {
                        "id":"6",
                        "accountNumber":"42820",
                        "formattedName": "Robert Jameson",
                        "pledgeCode":"220102",
                        "pledgeCodeDescription": "Sanjay in India",
                        "type":"D",
                        "typeDescription":"Donor To Child",
                        "sourceCode":"0_A_B_C_M",
                        "sourceCodeDescription":"Zero",
                        "contactMethod":"WEB",
                        "contactMethodDescription":"Website",
                        "communication":"Test Test",
                        "status":"T",
                        "statusDescription":"Translated",
                        "dateCreated":"2018-10-25",
                        "dateApproved":"2018-10-25",
                        "dateTranslated":null,
                        "dateSent":null,
                        "dateDelivered":null,
                        "dateCanceled":null,
                        "assignedToAccessorId":"11797",
                        "accessorName":"Nathan Johnson - Internal User"
                    },
                    {...},
                ]
}

```

Gets a list of all sponsorship communications.

##### ARGUMENTS

* recordId - Filters list by matching the record id
* accountNumber - Filters list by matching the account number
* pledgeCode - Filter list by partial matching the pledge code
* type - Filter list by matching the type of communication
* sourceCode - Filter list by partial matching the source code for the pledge
* contactMethod - Filter list by partial matching the contact method for the account
* communication - Filter list by partial matching communication data
* status - Filter list by matching the status of communication
* dateCreated - Filter list by matching communication created date
* dateApproved - Filter list by matching communication approved date
* dateTranslated - Filter list by matching communication translated date
* dateSent - Filter list by matching communication sent date
* dateDelivered - Filter list by matching communication delivered date
* dateCanceled - Filter list by matching communication canceled date
* assignedToAccessorId - Filter list by matching the assigned accessor id

##### Returns

A dictionary with an items property that contains an array of up to limit communications, starting at index offset. Each entry in the array is a separate communication object. If no more communications are available, the resulting array will be empty. This request should never return an error.

#### List all Sponsorship Communications for a pledge

```

DEFINITION
GET http://apiserver/pledges/:pledgeId/sponsorshipcommunications

EXAMPLE REQUEST
$.get("http://localhost:8000/api/pledges/220102/sponsorshipcommunications?offset=0&limit=5", {});

EXAMPLE RESPONSE
{
    "paging":    {
                    "limit":5,
                    "offset":0,
                    "total":13
                },
    "items":    [
                    {
                        "id":"6",
                        "accountNumber":"42820",
                        "formattedName": "Robert Jameson",
                        "pledgeCode":"220102",
                        "pledgeCodeDescription": "Sanjay in India",
                        "type":"D",
                        "typeDescription":"Donor To Child",
                        "sourceCode":"0_A_B_C_M",
                        "sourceCodeDescription":"Zero",
                        "contactMethod":"WEB",
                        "contactMethodDescription":"Website",
                        "communication":"Test Test",
                        "status":"T",
                        "statusDescription":"Translated",
                        "dateCreated":"2018-10-25",
                        "dateApproved":"2018-10-25",
                        "dateTranslated":null,
                        "dateSent":null,
                        "dateDelivered":null,
                        "dateCanceled":null,
                        "assignedToAccessorId":"11797",
                        "accessorName":"Nathan Johnson - Internal User"
                    },
                    {...},
                ]
}

```

Gets a list of all sponsorship communications for a given pledge.

##### Arguments

* pledgeId - Filter list by matching the pledge code

##### Returns

A dictionary with an items property that contains an array of up to limit communications, starting at index offset. Each entry in the array is a separate communication object. If no more communications are available, the resulting array will be empty. This request should never return an error.

### Pledge StudioOnline Publish Data

#### Retrieve the pledge StudioOnline publish data

```
DEFINITION
GET http://apiserver/pledges/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/7399/studioonlinepublishdata");

EXAMPLE RESPONSE
{
    "id": "6440",
    "description": "Pledge Test",
    "summary": "Summary Test",
    "extendedDescription": "Description Test",
    "associatedProject": "100101",
    "isExtendedDescriptionLocked": true,
    "iconImage": "iconImage.png",
    "mediumImage": "mediumImage.jpg",
    "largeImage": "largeImage.jpg",
    "keywords": "Test Keywords",
    "pageLayout": "PLDGPACK2"
}

```

Retrieves the details of the existing pledge StudioOnline publish data. You need only supply the pledge id.

##### Returns

Returns a pledge StudioOnline publish data object if a valid id was provided.

#### Update and publish the pledge StudioOnline publish data

```
DEFINITION
POST http://apiserver/pledges/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/7399/studioonlinepublishdata", {
    "pageLayout": "PLDGPACK3",
});

EXAMPLE RESPONSE
{
    "id": "6440",
    "description": "Pledge Test",
    "summary": "Summary Test",
    "extendedDescription": "Description Test",
    "isExtendedDescriptionLocked": true,
    "associatedProject": "100101",
    "updateImages": true,
    "iconImage": "iconImage.png",
    "mediumImage": "mediumImage.jpg",
    "largeImage": "largeImage.jpg",
    "keywords": "Test Keywords",
    "pageLayout": "PLDGPACK3"
}


```

Updates and publishes the specified pledge StudioOnline publish dat by setting the values of the parameters passed. Any parameters not provided will be left unchanged. Any categories must already have been updated through the Pledge Codes resources.

##### Arguments

* description (optional) - The description for the pledge on StudioOnline.
* summary (optional) - The summary for the pledge on StudioOnline.
* extendedDescription (optional) - The extended description for the pledge on StudioOnline.
* updateImages (optional) - Whether or not to update the icon and medium images. If this is selected and the icon or medium image are not provided, they will be deleted.
* associatedProject (optional) - The project that is associated with the pledge.
* iconImage (optional) - The icon image for the pledge on StudioOnline.
* mediumImage (optional) - The medium image for the pledge on StudioOnline.
* largeImage (optional) - The large image for the pledge on StudioOnline.
* keywords (optional) - The keywords for the pledge on StudioOnline.
* pageLayout (optional) - The page layout (XML Package) for the pledge on StudioOnline.

##### Returns

Returns the pledge StudioOnline publish data object if the update and publish succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined page layout code).

#### Unpublish the pledge StudioOnline publish data

```
DEFINITION
DELETE http://apiserver/pledges/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/7399/studioonlinepublishdata", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Unpublishes the pledge StudioOnline publish data. The actual data will not be deleted.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the pledge StudioOnline publish data cannot be unpublished, this call returns an error.

### Pledge Advanced StudioOnline Configuration

#### Create a pledge Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/pledges/:id/storeconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/110160/storeconfigurations", {
    "store": "19",
    "useInStudioOnline": true,
    "title": "Billy & Stacey Brand",
    "urlOverride": "billy-stacey-brand",
    "description": "Help support Billy & Stacey Brand as they reach the indigenous peoples of Australia with the gospel."
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "pledge": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": null,
    "endDate": null,
    "hideFromSearch": false,
    "title": "Billy & Stacey Brand",
    "urlOverride": "billy-stacey-brand",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Help support Billy & Stacey Brand as they reach the indigenous peoples of Australia with the gospel.",
    "keywords": null,
    "layoutOverride": null,
    "amountOverride": null,
    "frequencyOverride": null
}

```

Creates a new pledge Advanced StudioOnline configuration.

##### Arguments

* store (required) - The unique id of the store this configuration is for. Must be a valid store Id.
* title (required) - The online title for the pledge when used in the specified store.
* description (optional) - The online description for the pledge when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the pledge title.
* useInStudioOnline (optional) - Whether the pledge should be used in the specified store.
* startDate (optional) - The date the pledge will become visible in the specified store.
* endDate (optional) - The date the pledge will be removed from the specified store.
* hideFromSearch (optional) - Whether the pledge should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the pledgewhen used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default pledge layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate pledge that should be shown in StudioOnline if someone tries to navigate to this pledge.
* amountOverride (optional) - The amount used to override the Default Pledge Amount in Advanced Studio Online. NOTES: If 'frequencyOverride' is provided, this field is required. Only available for 'CHILD' and 'OTHER' pledge types.
* frequencyOverride (optional) - The 'DDCPLDGFRQ' frequency used to override the Default Pledge Frequency in Advanced Studio Online. NOTES: If 'amountOverride' is provided, this field is required. Only available for 'CHILD' and 'OTHER' pledge types.

##### Returns

Returns a pledge Advanced StudioOnline configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge Advanced StudioOnline configuration

```
DEFINITION
GET http://apiserver/pledges/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/110160/storeconfigurations/10033");

EXAMPLE RESPONSE
{
    "id": "10033",
    "pledge": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": null,
    "endDate": null,
    "hideFromSearch": false,
    "title": "Billy & Stacey Brand",
    "urlOverride": "billy-stacey-brand",
    "url": "https://www.myministry.com/pledge/billy-stacey-brand",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Help support Billy & Stacey Brand as they reach the indigenous peoples of Australia with the gospel.",
    "keywords": null,
    "layoutOverride": null,
    "amountOverride": null,
    "frequencyOverride": null
}

```

Retrieves the details of a pledge Advanced StudioOnline configuration. You need only supply the pledge id and configuration id.

##### Returns

Returns a pledge Advanced StudioOnline configuration object if valid ids were provided.

#### Update a pledge Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/pledges/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledges/110160/storeconfigurations/10033", {
    "startDate": "2017-09-01",
    "endDate": "2018-10-25"
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "pledge": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2017-09-01",
    "endDate": "2018-10-25",
    "hideFromSearch": false,
    "title": "Billy & Stacey Brand",
    "urlOverride": "billy-stacey-brand",
    "url": "https://www.myministry.com/pledge/billy-stacey-brand",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Help support Billy & Stacey Brand as they reach the indigenous peoples of Australia with the gospel.",
    "keywords": null,
    "layoutOverride": null,
    "amountOverride": null,
    "frequencyOverride": null
}


```

Updates the specified pledge Advanced StudioOnline configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title (optional) - The online title for the pledge when used in the specified store.
* description (optional) - The online description for the pledge when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the pledge title.
* useInStudioOnline (optional) - Whether the pledge should be used in the specified store.
* startDate (optional) - The date the pledge will become visible in the specified store.
* endDate (optional) - The date the pledge will be removed from the specified store.
* hideFromSearch (optional) - Whether the pledge should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the pledgewhen used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default pledge layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate pledge that should be shown in StudioOnline if someone tries to navigate to this pledge.
* amountOverride (optional) - The amount used to override the Default Pledge Amount in Advanced Studio Online. NOTES: If 'frequencyOverride' is provided, this field is required. Only available for 'CHILD' and 'OTHER' pledge types.
* frequencyOverride (optional) - The 'DDCPLDGFRQ' frequency used to override the Default Pledge Frequency in Advanced Studio Online. NOTES: If 'amountOverride' is provided, this field is required. Only available for 'CHILD' and 'OTHER' pledge types.

##### Returns

Returns a pledge Advanced StudioOnline configuration object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid permanentRedirect).

#### Delete a pledge Advanced StudioOnline configuration

```
DEFINITION
DELETE http://apiserver/pledges/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledges/110160/storeconfigurations/10033", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge Advanced StudioOnline configuration. It cannot be undone.

##### Arguments

* id (required) - The pledge Advanced StudioOnline configuration id of the configuration to be deleted.

##### Returns

Returns a 204 No Content response on success. If the pledge Advanced StudioOnline configuration does not exist, this call returns an error.

#### List all pledge Advanced StudioOnline configurations

```
DEFINITION
GET http://apiserver/pledges/:id/storeconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/pledges/110160/storeconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10033",
            "pledge": "110160",
            "store": "19",
            "storeDescription": "ASO US-English",
            "useInStudioOnline": true,
            "startDate": "2017-09-01",
            "endDate": "2018-10-25",
            "hideFromSearch": false,
            "title": "Billy & Stacey Brand",
            "urlOverride": "billy-stacey-brand",
            "url": "https://www.myministry.com/pledge/billy-stacey-brand",
            "permanentRedirect": null,
            "permanentRedirectDescription": null,
            "description": "Help support Billy & Stacey Brand as they reach the indigenous peoples of Australia with the gospel.",
            "keywords": null,
            "layoutOverride": null
        }
        {...},
        {...}
    ]
}

```

Returns a list of all pledge Advanced StudioOnline configurations matching the provided filter criteria.

##### Arguments

* id () - Filter list by an exact match on configuration id
* store () - Filter list by an exact match on store id
* pledge () - Filter list by an exact match in pledge code

##### Returns

A dictionary with an items property that contains an array of up to limit pledge Advanced StudioOnline configurations, starting at index offset. Each entry in the array is a separate pledge Advanced StudioOnline configuration object. If no more pledge Advanced StudioOnline configurations are available, the resulting array will be empty. This request should never return an error.

### Pledge Quick Picks

#### Create a pledge quick pick

```
DEFINITION
POST http://apiserver/pledgequickpicks

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgequickpicks", {
    "pledgeCode": "PLEDGECODE"
});

EXAMPLE RESPONSE
{
    "id": "49",
    "pledgeCode": "PLEDGECODE",
    "pledgeCodeDescription": "Pledge code description",
    "startDate": "2023-01-05",
    "endDate": "2050-02-17",
    "sequenceNumber": 10,
    "type": "QuickPick"
}

```

Creates a new pledge quick pick.

##### Arguments

* pledgeCode (required) - The pledge code. Must be a defined pledge code.
* startDate (optional) - The start date for the pledge quick pick.
* endDate (optional) - The end date for the pledge quick pick. Must be later than the start date.
* sequenceNumber (optional) - The sequence number for the pledge quick pick.

##### Returns

Returns a pledge quick pick object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a pledge quick pick

```
DEFINITION
GET http://apiserver/pledgequickpicks/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgequickpicks/49");

EXAMPLE RESPONSE
{
    "id": "49",
    "pledgeCode": "PLEDGECODE",
    "pledgeCodeDescription": "Pledge code description",
    "startDate": "2023-01-05",
    "endDate": "2050-02-17",
    "sequenceNumber": 10,
    "type": "QuickPick"
}

```

Retrieves the details of an existing pledge quick pick. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge quick pick to be retrieved.

#### Update a pledge quick pick

```
DEFINITION
POST http://apiserver/pledgequickpicks/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgequickpicks/49", {
    "startDate": "2023-11-01"
});

EXAMPLE RESPONSE
{
    "id": "49",
    "pledgeCode": "PLEDGECODE",
    "pledgeCodeDescription": "Pledge code description",
    "startDate": "2023-11-01",
    "endDate": "2050-02-17",
    "sequenceNumber": 10,
    "type": "QuickPick"
}


```

Updates the specified pledge quick pick by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* pledgeCode (optional) - The pledge code. Must be a defined pledge code.
* startDate (optional) - The start date for the quick pick.
* endDate (optional) - The end date for the quick pick. Must be later than the start date.
* sequenceNumber (optional) - The sequence number used to sort the pledge quick pick.

##### Returns

Returns the pledge quick pick object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a pledge quick pick

```
DEFINITION
DELETE http://apiserver/pledgequickpicks/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgequickpicks/49");

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge quick pick. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge quick pick to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge quick pick does not exist, this call returns an error.

#### List all pledge quick picks

```
DEFINITION
GET http://apiserver/pledgequickpicks

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgequickpicks");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "49",
            "pledgeCode": "PLEDGECODE",
            "pledgeCodeDescription": "Pledge code description",
            "startDate": "2023-01-05",
            "endDate": "2050-02-17",
            "sequenceNumber": 10,
            "type": "QuickPick"
        },
        {...},
    ]
}

```

Returns a list of all pledge quick picks.

##### Arguments

* pledgeCode (optional) - The pledge code the quick pick is associated with.
* date (optional) - The date in which the pledge quick pick must be active.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge quick picks, starting at index offset. Each entry in the array is a separate pledge quick pick object. If no more pledge quick picks are available, the resulting array will be empty. This request should never return an error.

### Programs

#### Create a program

```
DEFINITION
POST http://apiserver/programs

EXAMPLE REQUEST
$.post("http://localhost:49195/programs", {
    "id": "SAVCHLD",
    "description": "A Program for saving children.",
    "campaignCode": "MINGENRL",
    "start": "2015-02-01",
    "end": "2015-05-31"
});

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "A Program for saving children.",
    "campaignCode": "MINGENRL",
    "campaignCodeDescription": "Miniture Gaurdians Enroll",
    "start": "2015-02-01",
    "end": "2015-05-31"
}

```

Creates a new program.

##### Arguments

* id (required) - The unique code for the new program.
* description (optional) - The description of the program.
* campaignCode (optional) - The campaign of the program.
* start (optional) - The start date of the program.
* end (optional) - The end date of the program.

##### Returns

Returns a program object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve a program

```
DEFINITION
GET http://apiserver/programs/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/SAVCHLD");

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "A Program for saving children.",
    "campaignCode": "MINGENRL",
    "start": "2015-02-01",
    "end": "2015-05-31"
}

```

Retrieves the details of an existing program. You need only supply the program code.

##### Arguments

* id (required) - The program code of the program to retrieve.

##### Returns

Returns a program object if a valid id was provided.

#### Update a program

```
DEFINITION
POST http://apiserver/programs/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/SAVCHLD", {
    "end": "2015-06-21"
});

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "A Program for saving children.",
    "campaignCode": "MINGENRL",
    "campaignCodeDescription": "Miniture Gaurdians Enroll",
    "start": "2015-02-01",
    "end": "2015-06-21"
}

```

Updates the specified program by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the program.
* campaignCode (optional) - The campaign of the program.
* start (optional) - The start date of the program.
* end (optional) - The end date of the program.

##### Returns

Returns the program object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid default project, subscription, or event code).

#### Delete a program

```
DEFINITION
DELETE http://apiserver/programs/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/programs/SAVCHLD", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a program. It cannot be undone.

##### Arguments

* id (required) - The program code of the program to be deleted.

##### Returns

Returns a 204 No Content response on success. If the program does not exist, this call returns an error.

#### List all programs

```
DEFINITION
GET http://apiserver/programs

EXAMPLE REQUEST
$.get("http://localhost:49195/programs");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 242
    }
    "items": [
        {
            "id": "SAVCHLD",
            "description": "A Program for saving children.",
            "campaignCode": "MINGENRL",
            "campaignCodeDescription": "Miniture Gaurdians Enroll",
            "start": "2015-02-01",
            "end": "2015-06-21"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all programs matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in program code
* description () - Filter list by partial match in program description
* campaignCode () - The campaign of the program.
* status () - Filter list by status

##### Returns

A dictionary with an items property that contains an array of up to limit programs, starting at index offset. Each entry in the array is a separate program object. If no more programs are available, the resulting array will be empty. This request should never return an error.

### Program Attachments

#### Create a program attachment

```
DEFINITION
POST http://apiserver/programs/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new program attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a program attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a program attachment

```
DEFINITION
GET http://apiserver/programs/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/attachments/49");

EXAMPLE RESPONSE
{
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing program attachment. You need only supply the program id and program attachment id.

##### Arguments

* id (required) - The id of the account attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a program attachment object if a valid id was provided.

#### Update a program attachment

```
DEFINITION
POST http://apiserver/programs/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/attachments/49", {
    "type": "LOGO",
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Updates the specified program attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the program attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a program attachment

```
DEFINITION
DELETE http://apiserver/programs/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/programs/10EVT/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a program attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the program attachment id does not exist, this call returns an error.

#### List all program attachments

```
DEFINITION
GET http://apiserver/programs/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all program attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit program attachments, starting at index offset. Each entry in the array is a separate program attachment object. If no more program attachments are available, the resulting array will be empty. This request should never return an error.

### Program Codes

#### Create a program code

```
DEFINITION
POST http://apiserver/programs/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/codes", {
    "type": "PGTYPE",
    "value": "DM"
});

EXAMPLE RESPONSE
{
    "id": "24",
    "type": "PGTYPE",
    "typeDescription": null,
    "value": "DM",
    "valueDescription": "Direct Mail",
    "isActive": true
}

```

Creates a new program code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a program code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a program code

```
DEFINITION
GET http://apiserver/programs/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/codes/24");

EXAMPLE RESPONSE
{
    "id": "24",
    "type": "PGTYPE",
    "typeDescription": null,
    "value": "DM",
    "valueDescription": "Direct Mail",
    "isActive": true
}

```

Retrieves the details of an existing program code. You need only supply the program id and program code id.

##### Returns

Returns a program code object if a valid id was provided.

#### Update a program code

```
DEFINITION
POST http://apiserver/programs/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/codes/24", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "24",
    "type": "PGTYPE",
    "typeDescription": null,
    "value": "DM",
    "valueDescription": "Direct Mail",
    "isActive": false
}

```

Updates the specified program code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the program code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a program code

```
DEFINITION
DELETE http://apiserver/programs/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/programs/10EVT/codes/24", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a program code. It cannot be undone.

##### Arguments

* id (required) - The id of the account code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the program code id does not exist, this call returns an error.

#### List all program codes

```
DEFINITION
GET http://apiserver/programs/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "24",
            "type": "PGTYPE",
            "typeDescription": null,
            "value": "DM",
            "valueDescription": "Direct Mail",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all program codes.

##### Returns

A dictionary with an items property that contains an array of up to limit program codes, starting at index offset. Each entry in the array is a separate program code object. If no more program codes are available, the resulting array will be empty. This request should never return an error.

### Program Dates

#### Create a program date

```
DEFINITION
POST http://apiserver/programs/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/dates", {
    "type": "PROGDATS",
    "value": "2013-04-14"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGDATS",
    "typeDescription": "Program Dates Single",
    "value": "2013-04-14",
    "isActive": true
}

```

Creates a new program date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a program date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a program date

```
DEFINITION
GET http://apiserver/programs/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/dates/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGDATS",
    "typeDescription": "Program Dates Single",
    "value": "2013-04-14",
    "isActive": true
}

```

Retrieves the details of an existing program date. You need only supply the program id and program date id.

##### Returns

Returns a program date object if a valid id was provided.

#### Update a program date

```
DEFINITION
POST http://apiserver/programs/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/dates/5", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGDATS",
    "typeDescription": "Program Dates Single",
    "value": "2013-04-14",
    "isActive": false
}

```

Updates the specified program date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the program date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a program date

```
DEFINITION
DELETE http://apiserver/programs/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/programs/10EVT/dates/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a program date. It cannot be undone.

##### Arguments

* id (required) - The id of the account date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the program date id does not exist, this call returns an error.

#### List all program dates

```
DEFINITION
GET http://apiserver/programs/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/dates");

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
            "type": "PROGDATS",
            "typeDescription": "Program Dates Single",
            "value": "2013-04-14",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all program dates.

##### Returns

A dictionary with an items property that contains an array of up to limit program dates, starting at index offset. Each entry in the array is a separate program date object. If no more program dates are available, the resulting array will be empty. This request should never return an error.

### Program Notes

#### Create a program note

```
DEFINITION
POST http://apiserver/programs/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/notes", {
    "type": "PROGNOTE",
    "shortComment": "Notes about the program"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGNOTE",
    "typeDescription": "Program Note",
    "shortComment": "Notes about the program",
    "longComment": null
}

```

Creates a new program note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a program note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Retrieve a program note

```
DEFINITION
GET http://apiserver/programs/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/notes/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGNOTE",
    "typeDescription": "Program Note",
    "shortComment": "Notes about the program",
    "longComment": null
}

```

Retrieves the details of an existing program note. You need only supply the program id and program note id.

##### Returns

Returns a program note object if a valid id was provided.

#### Update a program note

```
DEFINITION
POST http://apiserver/programs/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/notes/5", {
    "longComment": "now we have a\nlong comment"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGNOTE",
    "typeDescription": "Program Note",
    "shortComment": "Notes about the program",
    "longComment": "now we have a\nlong comment"
}

```

Updates the specified program note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the program note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a program note

```
DEFINITION
DELETE http://apiserver/programs/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/programs/10EVT/notes/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a program note. It cannot be undone.

##### Arguments

* id (required) - The id of the account note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the program note id does not exist, this call returns an error.

#### List all program notes

```
DEFINITION
GET http://apiserver/programs/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/notes");

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
            "type": "PROGNOTE",
            "typeDescription": "Program Note",
            "shortComment": "Notes about the program",
            "longComment": "now we have a\nlong comment"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all program notes.

##### Returns

A dictionary with an items property that contains an array of up to limit program notes, starting at index offset. Each entry in the array is a separate program note object. If no more program notes are available, the resulting array will be empty. This request should never return an error.

### Program Numbers

#### Create a program number

```
DEFINITION
POST http://apiserver/programs/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/numbers", {
    "type": "PROGNUMS",
    "value": 3
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGNUMS",
    "typeDescription": null,
    "value": 3,
    "isActive": true
}

```

Creates a new program number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be a defined value of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a program number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Retrieve a program number

```
DEFINITION
GET http://apiserver/programs/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/numbers/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGNUMS",
    "typeDescription": null,
    "value": 3,
    "isActive": true
}

```

Retrieves the details of an existing program number. You need only supply the program id and program number id.

##### Returns

Returns a program number object if a valid id was provided.

#### Update a program number

```
DEFINITION
POST http://apiserver/programs/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/programs/10EVT/numbers/5", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "PROGNUMS",
    "typeDescription": null,
    "value": 3,
    "isActive": false
}

```

Updates the specified program number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be a defined value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the program number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a program number

```
DEFINITION
DELETE http://apiserver/programs/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/programs/10EVT/numbers/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a program number. It cannot be undone.

##### Arguments

* id (required) - The id of the account number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the program number id does not exist, this call returns an error.

#### List all program numbers

```
DEFINITION
GET http://apiserver/programs/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/programs/10EVT/numbers");

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
            "type": "PROGNUMS",
            "typeDescription": null,
            "value": 3,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all program numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit program numbers, starting at index offset. Each entry in the array is a separate program number object. If no more program numbers are available, the resulting array will be empty. This request should never return an error.

### Segmentation Criteria Types

#### Create a segmentation criteria type

```
DEFINITION
POST http://apiserver/segmentationcriteriatypes

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationcriteriatypes", {
    "id": "ACCTITLE",
    "description": "Account Title",
    "category": "ACCOUNTS",
    "dataType": "STRING",
    "tableId": "A01",
    "field": "Title",
    "isActive": true,
    "isAdvancedFindType": true
});

EXAMPLE RESPONSE
{
    "id": "ACCTITLE",
    "description": "Account Title",
    "category": "ACCOUNTS",
    "dataType": "STRING",
    "tableId": "A01",
    "field": "Title",
    "codeType": null,
    "isActive": true,
    "isAdvancedFindType": true
}

```

##### Arguments

* id (required) - The segmentation criteria type.
* description (required) - The description of the segmentation criteria type.
* category (required) - The category of the segmentation criteria type.
* dataType (required) - The data type of the segmentation criteria type. (Some possible values are "DATE", "AMOUNT", "STRING", "ACCESSOR".)
* tableId (required) - The database table id of the segmentation criteria type.
* field (optional) - The database field or column of the segmentation criteria type.
* codeType (optional) - The code type of the segmentation criteria type.
* isActive (optional) - Whether the segmentation criteria type is active. (If not provided, isActive will be defaulted to 'true'.)
* isAdvancedFindType (optional) - Whether the segmentation criteria type is used in Advanced Find for accounts. Defaults to false.

##### Returns

Returns a segmentation criteria type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a segmentation criteria type

```
DEFINITION
GET http://apiserver/segmentationcriteriatypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationcriteriatypes/acctitle");

EXAMPLE RESPONSE
{
    "id": "ACCTITLE",
    "description": "Account Title",
    "category": "ACCOUNTS",
    "dataType": "STRING",
    "tableId": "A01",
    "field": "Title",
    "codeType": null,
    "isActive": true,
    "isAdvancedFindType": true
}

```

Retrieves the details of an existing segmentation criteria type. You need only supply the segmentation criteria type id.

##### Returns

Returns segmentation criteria type object if a valid id was provided.

#### Update a segmentation criteria type

```
DEFINITION
POST http://apiserver/segmentationcriteriatypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationcriteriatypes/acctitle", {
        "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "ACCTITLE",
    "description": "Account Title",
    "category": "ACCOUNTS",
    "dataType": "STRING",
    "tableId": "A01",
    "field": "Title",
    "codeType": null,
    "isActive": false,
    "isAdvancedFindType": true
}

```

##### Arguments

* description (optional) - The description of the segmentation criteria type.
* category (optional) - The category of the segmentation criteria type.
* dataType (optional) - The data type of the segmentation criteria type. (Some possible values are "DATE", "AMOUNT", "STRING", "ACCESSOR".)
* tableId (optional) - The database table id of the segmentation criteria type.
* field (optional) - The database field or column of the segmentation criteria type.
* codeType (optional) - The code type of the segmentation criteria type.
* isActive (optional) - Whether the segmentation criteria type is active. (If not provided, isActive will be defaulted to 'true'.)
* isAdvancedFindType (optional) - Whether the segmentation criteria type is used in Advanced Find for accounts. Defaults to false.

##### Returns

Returns segmentation criteria type object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a segmentation criteria type

```
DEFINITION
DELETE http://apiserver/segmentationcriteriatypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/segmentationcriteriatypes/acctitle", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes segmentation criteria type. It cannot be undone.

##### Arguments

* id (required) - The id of the segmentation criteria type to be deleted.

##### Returns

Returns a 204 No Content response on success. If the segmentation criteria type id does not exist, this call returns an error.

#### List all segmentation criteria types

```
DEFINITION
GET http://apiserver/segmentationcriteriatypes

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationcriteriatypes?isActive=false");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "ACCTITLE",
            "description": "Account Title",
            "category": "ACCOUNTS",
            "dataType": "STRING",
            "tableId": "A01",
            "field": "Title",
            "codeType": null,
            "isActive": false,
            "isAdvancedFindType": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation criteria types.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (required) - The id of the segmentation criteria types to retrieve.
* description (required) - The description of the segmentation criteria types to retrieve.
* category (required) - The category of the segmentation criteria types to retrieve.
* dataType (required) - The data type of the segmentation criteria types to retrieve.
* tableId (required) - The database table id of the segmentation criteria types to retrieve.
* isActive (optional) - Whether to return active segmentation criteria types.
* isAdvancedFindType (optional) - Whether the segmentation criteria type is used in Advanced Find for accounts.

##### Returns

A dictionary with an items property that contains an array of up to limit segmentation criteria types, starting at index offset. Each entry in the array is a separate segmentation criteria type object. If no more segmentation criteria types are available, the resulting array will be empty. This request should never return an error.

### Segmentation Jobs

#### Create a segmentation job

```
DEFINITION
POST http://apiserver/segmentationjobs

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs", {
    "description": "Family Pledges",
    "category": "MAIL"
});

EXAMPLE RESPONSE
{
    "id": "541",
    "description": "Family Pledges",
    "category": "MAIL",
    "categoryDescription": "Direct Mail",
    "lastUsedDate": "2014-08-14T08:31:01.11",
    "elementReportingGroup": null,
    "elementReportingGroupDescription": null,
    "inputJobNumber": null,
    "inputJobNumberDescription": null,
    "inputSegmentNumber": null,
    "inputSegmentNumberDescription": null
}

```

##### Arguments

* description (optional) - The description of the segmentation job.
* category (optional) - The segmentation category of the segmentation job. Must be a valid code value for the code type `DDCSEGCAT`.
* elementReportingGroup (optional) - The element reporting group of the segmentation job. Must be a valid code value for the code type `DDCELEMENT`.
* inputJobNumber (optional) - The input job number of the segmentation job. Must be a valid code value for the code type `DDCJOBNMBR`.
* inputSegmentNumber (optional) - The input segment number of the segmentation job. Must be a valid code value for the code type `DDCSEGNMBR`.

##### Returns

Returns a segmentation job object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a segmentation job

```
DEFINITION
GET http://apiserver/segmentationjobs/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/541");

EXAMPLE RESPONSE
{
    "id": "541",
    "description": "Family Pledges",
    "category": "MAIL",
    "categoryDescription": "Direct Mail",
    "lastUsedDate": "2014-08-14T08:31:01.11",
    "elementReportingGroup": null,
    "elementReportingGroupDescription": null,
    "inputJobNumber": null,
    "inputJobNumberDescription": null,
    "inputSegmentNumber": null,
    "inputSegmentNumberDescription": null
}

```

Retrieves the details of an existing segmentation job. You need only supply the segmentation job id.

##### Returns

Returns segmentation job object if a valid id was provided.

#### Update a segmentation job

```
DEFINITION
POST http://apiserver/segmentationjobs/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541", {
        "category": "REPORT",
});

EXAMPLE RESPONSE
{
    "id": "541",
    "description": "Family Pledges",
    "category": "REPORT",
    "categoryDescription": "Reports/Numbers",
    "lastUsedDate": "2014-08-14T08:31:01.11",
    "elementReportingGroup": null,
    "elementReportingGroupDescription": null,
    "inputJobNumber": null,
    "inputJobNumberDescription": null,
    "inputSegmentNumber": null,
    "inputSegmentNumberDescription": null
}

```

##### Arguments

* description (optional) - The description of the segmentation job.
* category (optional) - The segmentation category of the segmentation job. Must be a valid code value for the code type `DDCSEGCAT`.
* elementReportingGroup (optional) - The element reporting group of the segmentation job. Must be a valid code value for the code type `DDCELEMENT`.
* inputJobNumber (optional) - The input job number of the segmentation job. Must be a valid code value for the code type `DDCJOBNMBR`.
* inputSegmentNumber (optional) - The input segment number of the segmentation job. Must be a valid code value for the code type `DDCSEGNMBR`.

##### Returns

Returns segmentation job object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a segmentation job

```
DEFINITION
DELETE http://apiserver/segmentationjobs/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/segmentationjobs/541", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes segmentation job. It cannot be undone.

##### Arguments

* id (required) - The id of the segmentation job to be deleted.

##### Returns

Returns a 204 No Content response on success. If the segmentation job id does not exist, this call returns an error.

#### List all segmentation jobs

```
DEFINITION
GET http://apiserver/segmentationjobs

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs?category=report");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "541",
            "description": "Family Pledges",
            "category": "REPORT",
            "categoryDescription": "Reports/Numbers",
            "lastUsedDate": "2014-08-14T08:31:01.11",
            "elementReportingGroup": null,
            "elementReportingGroupDescription": null,
            "inputJobNumber": null,
            "inputJobNumberDescription": null,
            "inputSegmentNumber": null,
            "inputSegmentNumberDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation jobs.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - The id (job number) of the segmentation jobs to retrieve.
* description (optional) - The description of the segmentation jobs to retrieve.
* category (optional) - The segmentation category of the segmentation jobs to retrieve.
* elementReportingGroup (optional) - The element reporting group of the segmentation jobs to retrieve.

##### Returns

A dictionary with an items property that contains an array of up to limit segmentation jobs, starting at index offset. Each entry in the array is a separate job specification object. If no more segmentation jobs are available, the resulting array will be empty. This request should never return an error.

### Segmentation Job Accounts

#### Create a segmentation job account

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accounts

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accounts", {
    "id":"16638",
    "segmentNumber":1
});

EXAMPLE RESPONSE
{
    "id": "5",
    "account": "16638",
    "segmentNumber": 1,
    "segmentNumberDescription": "Family Pledge",
    "accountName": "Frank Smith",
    "sourceCode": null,
    "accountType": "I",
    "allowTransactions": true,
    "isFamilyConsolidated": true,
    "familyId": 16633,
    "familyMemberType": "CN",
    "firstName": "Frank",
    "lastName": "Smith",
    "middleName": null,
    "organizationName": "DonorDirect",
    "status": "A",
    "suffix": null,
    "title": null,
    "primaryEmail": "frank@donordirect.com",
    "salutation": "Frank",
    "addressLine1": "2435 N. Central Expressway",
    "addressLine2": "Ste. 950",
    "addressLine3": null,
    "addressLine4": null,
    "city": "Richardson",
    "state": "TX",
    "zipPostal": "75080",
    "country": "USA",
    "addressType": "MAIL"
}

```

##### Arguments

* id (required) - Account number for the segmentation job account.
* segmentNumber (required) - The segment number of the job for the segmentation job account.

##### Returns

Returns a segmentation job account object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a segmentation job account

```
DEFINITION
GET http://apiserver/segmentationjobs/:id/accounts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/541/accounts/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "account": "16638",
    "segmentNumber": 1,
    "segmentNumberDescription": "Family Pledge",
    "accountName": "Frank Smith"
    "sourceCode": null,
    "accountType": "I",
    "allowTransactions": true,
    "isFamilyConsolidated": true,
    "familyId": 16633,
    "familyMemberType": "CN",
    "firstName": "Frank",
    "lastName": "Smith",
    "middleName": null,
    "organizationName": "DonorDirect",
    "status": "A",
    "suffix": null,
    "title": null,
    "primaryEmail": "frank@donordirect.com",
    "salutation": "Frank",
    "addressLine1": "2435 N. Central Expressway",
    "addressLine2": "Ste. 950",
    "addressLine3": null,
    "addressLine4": null,
    "city": "Richardson",
    "state": "TX",
    "zipPostal": "75080",
    "country": "USA",
    "addressType": "MAIL"
}

```

Retrieves the details of an existing segmentation job account. You need only supply the segmentation job account id.

##### Returns

Returns segmentation job account object if a valid id was provided.

#### Update a segmentation job account

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accounts/5", {
    "segmentNumber": "Individual Pledge"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "account": "16638",
    "segmentNumber": 1,
    "segmentNumberDescription": "Individual Pledge",
    "accountName": "Frank Smith"
    "sourceCode": null,
    "accountType": "I",
    "allowTransactions": true,
    "isFamilyConsolidated": true,
    "familyId": 16633,
    "familyMemberType": "CN",
    "firstName": "Frank",
    "lastName": "Smith",
    "middleName": null,
    "organizationName": "DonorDirect",
    "status": "A",
    "suffix": null,
    "title": null,
    "primaryEmail": "frank@donordirect.com",
    "salutation": "Frank",
    "addressLine1": "2435 N. Central Expressway",
    "addressLine2": "Ste. 950",
    "addressLine3": null,
    "addressLine4": null,
    "city": "Richardson",
    "state": "TX",
    "zipPostal": "75080",
    "country": "USA",
    "addressType": "MAIL"
}

```

##### Arguments

* segmentNumber (required) - The segment number of the job for the segmentation job account.

##### Returns

Returns segmentation job account object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a segmentation job account

```
DEFINITION
DELETE http://apiserver/segmentationjobs/:id/accounts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/segmentationjobs/541/accounts/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes segmentation job account. It cannot be undone.

##### Arguments

* id (required) - The id of the segmentation job account to be deleted.

##### Returns

Returns a 204 No Content response on success. If the segmentation job account id does not exist, this call returns an error.

#### List all segmentation job accounts

```
DEFINITION
GET http://apiserver/segmentationjobs/:id/accounts

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/541/accounts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "5",
            "account": "16638",
            "segmentNumber": 1,
            "segmentNumberDescription": "Individual Pledge",
            "accountName": "Frank Smith"
            "sourceCode": null,
            "accountType": "I",
            "allowTransactions": true,
            "isFamilyConsolidated": true,
            "familyId": 16633,
            "familyMemberType": "CN",
            "firstName": "Frank",
            "lastName": "Smith",
            "middleName": null,
            "organizationName": "DonorDirect",
            "status": "A",
            "suffix": null,
            "title": null,
            "primaryEmail": "frank@donordirect.com",
            "salutation": "Frank",
            "addressLine1": "2435 N. Central Expressway",
            "addressLine2": "Ste. 950",
            "addressLine3": null,
            "addressLine4": null,
            "city": "Richardson",
            "state": "TX",
            "zipPostal": "75080",
            "country": "USA",
            "addressType": "MAIL"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation job accounts.

##### Arguments

* account (optional) - The account number of the account to retrieve.
* segmentNumber (optional) - The segment number of the accounts to retrieve.

##### Returns

A dictionary with an items property that contains an array of up to limit segmentation job accounts, starting at index offset. Each entry in the array is a separate job account specification object. If no more segmentation job accounts are available, the resulting array will be empty. This request should never return an error.

#### Segmentation Job Account Codes Update

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accountcodesupdate

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accountcodesupdate", {
        "segmentNumber":600,
        "codeAction":"UPDATE",
        "codeType":"DONORLEVEL",
        "codeValue":"CATEGORY3",
        "codeNewValue":"CATEGORY4"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (optional) - The segment number used in the segmentation job account codes update process. (If not provided or null, the output will be run over all segments.)
* codeAction (optional) - The action to perform on account codes in the segmentation job account codes update process. (Must be one of the following: `ADD`, `UPDATE`, `DELETE`, `INACTIVE`, `NONE`. Instead of passing `NONE`, you can just leave this field `null` or not include it.)
* codeType (optional) - The account code type to perform the codeAction on in the segmentation job account codes update process. (Must be a valid and active code type in the `ACCOUNT` category. Required if codeAction is `ADD`, `UPDATE`, `DELETE`, `INACTIVE`.)
* codeValue (optional) - The value of the codeType to perform the codeAction on in the segmentation job account codes update process. (Must be a valid code value for the codeType. Required if codeAction is `ADD`, `UPDATE`, `DELETE`, `INACTIVE`.)
* codeNewValue (optional) - The new value of the codeType to `UPDATE` in the segmentation job account codes update process. (Must be a valid code value for the codeType. Rquired if codeAction is `UPDATE`.)
* mediaCodeAction (optional) - The action to perform on media codes in the segmentation job account codes update process. (Must be one of the following: `ADD`, `UPDATE`, `DELETE`, `INACTIVE`, `NONE`. Instead of passing `NONE`, you can just leave this field `null` or not include it.)
* mediaCodeValue (optional) - The value of the media code to perform the mediaCodeAction on in the segmentation job account codes update process. (Must be a valid code value for the code type `DDCMEDIA`. Required if mediaCodeAction is `ADD`, `UPDATE`, `DELETE`, `INACTIVE`.)
* mediaCodeNewValue (optional) - The new value of the media code to `UPDATE` in the segmentation job account codes update process. (Must be a valid code value for the code type `DDCMEDIA`. Rquired if mediaCodeAction is `UPDATE`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job account codes update process has an error, a 400 or 500 will be returned.

#### Segmentation Job Account Marketing Attributes Update

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accountmarketingattributesupdate

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accountmarketingattributesupdate", {
        "segmentNumber":600,
        "attributeAction":"SET",
        "attributeType":"DONTRACK",
        "attributeValue":"5"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (optional) - The segment number used in the segmentation job account marketing attributes update process. (If not provided or null, the output will be run over all segments.)
* attributeAction (optional) - The action to perform on account marketing codes in the segmentation job account marketing attributes update process. (Must be one of the following: `SET`, `DELETE`.)
* attributeType (optional) - The account marketing code type to perform the attributeAction on in the segmentation job account marketing attributes update process. (Must be a valid and active code type in the `ACCTMKATTR` category. Required if attributeAction is `SET`, `DELETE`.)
* attributeValue (optional) - The value of the attributeType to perform the attributeAction on in the segmentation job account marketing attributes update process. (Must be a valid code value for the attributeType. Required if attributeAction is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job account marketing attributes update process has an error, a 400 or 500 will be returned.

#### Segmentation Job Account Marketing Dates Update

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accountmarketingdatesupdate

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accountmarketingdatesupdate", {
        "segmentNumber":600,
        "dateAction":"SET",
        "dateType":"LSTCONTACT",
        "dateValue":"2016-06-01"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (optional) - The segment number used in the segmentation job account marketing dates update process. (If not provided or null, the output will be run over all segments.)
* dateAction (optional) - The action to perform on account marketing dates in the segmentation job account marketing dates update process. (Must be one of the following: `SET`, `DELETE`.)
* dateType (optional) - The account marketing date type to perform the dateAction on in the segmentation job account marketing dates update process. (Must be a valid and active date type in the `ACCTMKATTR` category. Required if dateAction is `SET`, `DELETE`.)
* dateValue (optional) - The value of the dateType to perform the dateAction on in the segmentation job account marketing dates update process. (Must be a valid date value for the dateType. Required if dateAction is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job account marketing dates update process has an error, a 400 or 500 will be returned.

#### Segmentation Job Account Marketing Notes Update

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accountmarketingnotesupdate

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accountmarketingnotesupdate", {
        "segmentNumber":600,
        "noteAction":"SET",
        "noteType":"MKTNOTE",
        "noteValue":"He enjoys attending basketball games with his family."
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (optional) - The segment number used in the segmentation job account marketing notes update process. (If not provided or null, the output will be run over all segments.)
* noteAction (optional) - The action to perform on account marketing notes in the segmentation job account marketing notes update process. (Must be one of the following: `SET`, `DELETE`.)
* noteType (optional) - The account marketing note type to perform the noteAction on in the segmentation job account marketing notes update process. (Must be a valid and active note type in the `ACCTMKATTR` category. Required if noteAction is `SET`, `DELETE`.)
* noteValue (optional) - The value of the noteType to perform the noteAction on in the segmentation job account marketing notes update process. (Required if noteAction is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job account marketing notes update process has an error, a 400 or 500 will be returned.

#### Segmentation Job Account Marketing Numbers Update

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accountmarketingnumbersupdate

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accountmarketingnumbersupdate", {
        "segmentNumber":600,
        "numberAction":"SET",
        "numberType":"LSTGIFTAMT",
        "numberValue":175
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (optional) - The segment number used in the segmentation job account marketing numbers update process. (If not provided or null, the output will be run over all segments.)
* numberAction (optional) - The action to perform on account marketing numbers in the segmentation job account marketing numbers update process. (Must be one of the following: `SET`, `DELETE`.)
* numberType (optional) - The account marketing number type to perform the numberAction on in the segmentation job account marketing numbers update process. (Must be a valid and active number type in the `ACCTMKATTR` category. Required if numberAction is `SET`, `DELETE`.)
* numberValue (optional) - The value of the numberType to perform the numberAction on in the segmentation job account marketing numbers update process. (Must be a valid number value for the numberType. Required if numberAction is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job account marketing numbers update process has an error, a 400 or 500 will be returned.

#### Segmentation Job Account Pledge Update

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/accountpledgeupdate

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/accountpledgeupdate", {
        "segmentNumber": 600,
        "pledge":"4RELIEF",
        "action":"CONTINUE"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* action (required) - The action to perform on account pledge in the segmentation job account pledge update process. (Must be one of the following: `CONTINUE`, `CANCELADD`, `UPDATE`, `ACTIVATE`, `CANCEL`.)
* pledge (required) - The pledge code filter used in the segmentation job account pledge update process. (Must be a valid code value for the code type `DDCPLDGCD`.)
* segmentNumber (optional) - The segment number used in the segmentation job account pledge update process. (If not provided or null, the output will be run over all segments.)
* newPledge (optional) - The new pledge code used in the segmentation job account pledge update process. (Only used if the action is `CONTINUE` or `CANCELADD`.)
* increaseAmount (optional) - The increase amount used in the segmentation job account pledge update process. (Only used if the action is `CONTINUE` or `CANCELADD`. Can be a negative value; however, this could result in a $0 pledge.)
* cancelReason (optional) - The cancel reason used in the segmentation job account pledge update process. (Only used if the action is `CONTINUE`, `CANCELADD`, or `CANCEL`. Required if the action is `CANCELADD` or `CANCEL`.)
* adjustedMonths (optional) - The number of adjusted months used in the segmentation job account pledge update process. (Only used if the action is `UPDATE`.)
* pledgeStatus (optional) - The pledge status filter used in the segmentation job account pledge update process. (Required if the action is `ACTIVATE` or `CANCEL`. If the action is `ACTIVATE`, must be one of the following: `INACTIVE`, `PENDING`, or `ANY`. If the action is `CANCEL`, must be one of the following: `ACTIVE`, `PENDING`, or `ANY`.)
* cancelRecurring (optional) - Whether or not to cancel the recurring as well in the segmentation job account pledge update process. (Required and only used if the action is `CANCEL`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job account pledge update process has an error, a 500 will be returned.

#### Segmentation Job Build Communications

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/buildcommunications

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/buildcommunications", {
        "segmentNumber": 600,
        "type": "PHONE",
        "date": "2015-07-14",
        "shortComment": "Communication for Segment 600",
        "isInbound": true,
        "buildQueues": false
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* type (required) - The communication type used in the segmentation job build communications process. (Must be a valid code value for the code type `DDCCOMTYPE`.)
* date (required) - The communication type used in the segmentation job build communications process.
* isInbound (required) - Whether inbound or outbound is used for the communication in the segmentation job build communications process.
* shortComment (required) - The short comment used in the segmentation job build communications process. (For communications of type `EMAIL`, this is the email subject.)
* buildQueues (required) - Whether or not account queues should also be build during the segmentation job build communications process.
* segmentNumber (optional) - The segment number used in the segmentation job build communications process. (If not provided or null, the output will be run over all segments.)
* longComment (optional) - The long comment used in the segmentation job build communications process. (Required if the communication type is `EMAIL`. For communications of type "EMAIL", this is the email message body.)
* source (optional) - The communication souce used in the segmentation job build communications process. (If not provided or null, the source will be taken from the segment.)
* letterPrintStatus (optional) - The letter print status used in the segmentation job build communications process. (Required and only used if the communication type is `LETTER`. Must be one of the following: `Y` (Ready), `N` (Never), `P` (Printed), `R` (Profiled), `H` (Hold).)
* letterCode (optional) - The letter code used in the segmentation job build communications process. (Required and only used if the communication type is `LETTER`.)
* letterCompletionText (optional) - The letter completion text used in the segmentation job build communications process. (Only used if the communication type is `LETTER`.)
* queueCategory (optional) - The queue category used when building account queues in the segmentation job build communications process. (Only used if buildQueues is `true`.)
* queueDescription (optional) - The queue description used when building account queues in the segmentation job build communications process. (Only used if buildQueues is `true`.)
* queueAssignTo (optional) - The queue assign To user id used when building account queues in the segmentation job build communications process. (Only used if buildQueues is `true`.)
* queueScript (optional) - The queue script code used when building account queues in the segmentation job build communications process. (Must be a valid code value for the code type `DDCSCRIPTS`. Only used if buildQueues is `true`.)
* queueInstruction (optional) - The queue instruction code used when building account queues in the segmentation job build communications process. (Must be a valid code value for the code type `DDCINSTRUC`. Only used if buildQueues is `true`.)
* maxQueueSize (optional) - The maximum entries in each queue when building account queues for the segmentation job build communications process. (Only used if buildQueues is `true`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job build communciations process has an error, a 400 or 500 will be returned.

#### Segmentation Job Build Event Invitation List

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/buildeventinvitationlist

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/buildeventinvitationlist", {
        "segmentNumber": 10,
        "eventCode": "10DAL1",
        "registrationType": "REGTYPE",
        "functionalCategory": "FUNCTIONCATEGORY",
        "status": "N"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (optional) - The segment number used in the segmentation job build event invitation list process. (Must be a valid segment number)
* eventCode (required) - A valid event code for the invitation list that the accounts will be added to. (Valid code types for `DDCEVENTCD`)
* registrationType (optional) - A valid registration type to use when building the invitation list (Valid code types for `EVTREGTYPE`)
* functionalCategory (optional) - If not included, the accounts primary email address will be used, otherwise the email address with this functional category will be selected from the account. (Valid functional categories for `DDCFUNCCAT`)
* status (required) - A valid status code that will be added to each invitation added to the list. StudioEnterpise UI defaults to 'N' (Not Invited Yet). (Valid code types for `EINVSTATUS`)

##### Returns

Returns a 204 No Content response on success. If the segmentation job build event invitation list process has an error, a 400 or 500 will be returned.

#### Segmentation Job Build Orders

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/buildorders

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/buildorders", {
        "segmentNumber": 600,
        "company": "1",
        "warehouse": "10",
        "source": "0700",
        "product1": "10-0-003",
        "productQuantity1": 2,
        "shippingMethod": "2DAY"

});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (required) - The segment number used in the segmentation job build orders process.
* batch (optional) - The batch number used in the segmentation job build orders process. The transaction will be created with this batch. Either `batch` or `company` is required. (Must be an open and standard batch.)
* company (optional) - The company used in the segmentation job build orders process. Either `batch` or `company` is required. (Must be a valid code value for the code type `DDCCOMPANY`.)
* warehouse (required) - The warehouse used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCWHS`.)
* source (required) - The source code used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCSRCCODE`.)
* shippingMethod (required) - The shipping method used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCSHIPMET`.)
* product1 (required) - The first product code used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCPROD`.)
* productQuantity1 (required) - The quantity for the first product code used in the segmentation job build orders process. (Must be an integer greater than 0.)
* product2 (optional) - The second product code used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCPROD`.)
* productQuantity2 (optional) - The quantity for the second product code used in the segmentation job build orders process. (Required if product2 is provided. Must be an integer greater than 0.)
* product3 (optional) - The third product code used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCPROD`.)
* productQuantity3 (optional) - The quantity for the third product code used in the segmentation job build orders process. (Required if product3 is provided. Must be an integer greater than 0.)
* product4 (optional) - The fourth product code used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCPROD`.)
* productQuantity4 (optional) - The quantity for the fourth product code used in the segmentation job build orders process. (Required if product4 is provided. Must be an integer greater than 0.)
* product5 (optional) - The fifth product code used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCPROD`.)
* productQuantity5 (optional) - The quantity for the fifth product code used in the segmentation job build orders process. (Required if product5 is provided. Must be an integer greater than 0.)
* letterCode (optional) - The letter code used in the segmentation job build orders process. (Must be a valid code value for the code type `DDCLTRCODE`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job build communciations process has an error, a 500 will be returned.

#### Segmentation Job Build Queues

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/buildqueues

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/buildqueues", {
        "segmentNumber": 600
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (required) - The segment number used in the segmentation job build account queues process.
* category (optional) - The queue category used in the segmentation job build account queues process.
* description (optional) - The queue description used in the segmentation job build account queues process.
* processingType (optional) - The queue processing type used in the segmentation job build account queues process. (Must be a valid code value for the code type `DDCACCQPR`.)
* assignTo (optional) - The queue assign To user id used in the segmentation job build account queues process.
* batch (optional) - The queue batch number used in the segmentation job build account queues process. (Must be a valid code value for the code type `DDCBATCH`.)
* script (optional) - The queue script code used in the segmentation job build account queues process. (Must be a valid code value for the code type `DDCSCRIPTS`.)
* instruction (optional) - The queue instruction code used in the segmentation job build account queues process. (Must be a valid code value for the code type `DDCINSTRUC`.)
* maxQueueSize (optional) - The maximum entries in each queue for the segmentation job build account queues process.

##### Returns

Returns a 204 No Content response on success. If the segmentation job build account queue process has an error, a 500 will be returned.

#### Segmentation Job Build Subscriptions

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/buildsubscriptions

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/buildsubscriptions", {
        "segmentNumber": 600,
        "company": "10",
        "source": "14GDC001",
        "subscription": "EXPLORERS",
        "price": "1YR",
        "numberOfIssues": 12
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (required) - The segment number used in the segmentation job build subscriptions process.
* company (required) - The company used in the segmentation job build subscriptions process.
* source (required) - The source code used in the segmentation job build subscriptions process.
* subscription (required) - The subscription code used in the segmentation job build subscriptions process.
* price (required) - The price code used in the segmentation job build subscriptions process.
* numberOfIssues (required) - The number of issues used in the segmentation job build subscriptions process.
* autoRenew (optional) - The auto renew status used in the segmentation job build subscriptions process. NOTE: Only applies to membership type subscriptions.
* renewalPrice (optional) - The renewal price code used in the segmentation job build subscriptions process. (required if autoRenew is true) NOTE: Only applies to membership type subscriptions.
* startDate (optional) - The start date used in the segmentation job build subscriptions process.
* letterCode (optional) - The letter code used in the segmentation job build subscriptions process.

##### Returns

Returns a 204 No Content response on success. If the segmentation job build subscriptions process has an error, a 500 will be returned.

#### Segmentation Job Copy

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/copy

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/output", {
        "useSameElementGroup": false,
        "createNewElementGroup": true,
        "jobDescription": "Copy of Job",
        "elementGroup": "TST",
        "elementGroupDescription": "New Element Group Description",
        "campaignProgram": "CAMPAIGN",
        "startDate": "2015-07-01",
        "endDate": "2015-07-31",
        "defaultProject": "PROJ",
        "defaultSubscription": "SUBSC",
        "defaultEvent": "EVENT"
});

EXAMPLE RESPONSE
{
    "newJob": {
        "id": "579",
        "description": "Copy of Job",
        "category": "CHILD",
        "categoryDescription": "Child",
        "lastUsedDate": null,
        "elementReportingGroup": "TST",
        "elementReportingGroupDescription": "New Element Group Description",
        "inputJobNumber": null,
        "inputJobNumberDescription": null,
        "inputSegmentNumber": null,
        "inputSegmentNumberDescription": null
    },
    "skippedSegments": [
        {
            "id": "7",
            "message": "Does not have the same prefix as the element group."
        },
        {...}
    ],
    "skippedSourceCodes": [
        {
            "id": "EK123456",
            "message": "Does not have the same prefix as the element group."
        },
        {...}
    ]
}

```

##### Arguments

* useSameElementGroup (required) - Whether you want to use the same element group as the source segmentation job.
* createNewElementGroup (optional) - Whether you want to create a new element group or use an existing on the copied segmentation job. (Required if useSameElementGroup is false.)
* jobDescription (optional) - The description of the copied segmentation job.
* elementGroup (optional) - The element group of the copied segmentation job. (Required if useSameElementGroup is false and createNewElementGroup is true. If createNewElementGroup is false, must be a valid code value for the code type `DDCELEMENT`.)
* elementGroupDescription (optional) - The element group description for the new element group of the copied segmentation job. (Only used if useSameElementGroup is false and createNewElementGroup is true.)
* campaignProgram (optional) - The campaign program for the new element group of the copied segmentation job. (Only used if useSameElementGroup is false and createNewElementGroup is true. Must be a valid code value for the code type `DDCPROGRAM`.)
* startDate (optional) - The start date for the new element group of the copied segmentation job. (Only used if useSameElementGroup is false and createNewElementGroup is true.)
* endDate (optional) - The end date for the new element group of the copied segmentation job. (Only used if useSameElementGroup is false and createNewElementGroup is true.)
* defaultProject (optional) - The default project for the new element group of the copied segmentation job. (Only used if useSameElementGroup is false and createNewElementGroup is true. Required if createNewElementGroup is true. Must be a valid code value for the code type `DDCPROJ`.)
* defaultSubscription (optional) - The default subscription for the new element group of the copied segmentation job. (Only used if useSameElementGroup is false and createNewElementGroup is true. Must be a valid code value for the code type `DDCSBSCRCD`.)
* defaultEvent (optional) - The default event for the new element group of the copied segmentation job. (Only used if useSameElementGroup is false and createNewElementGroup is true. Must be a valid code value for the code type `DDCEVENTTP`.)

##### Returns

Returns a the new segmentation job object and a list of skipped segments and skipped source codes, if there were any. The skipped segments and source codes will contain an id to identify the skipped ones and a message why they were skipped. If the segmentation job copy has an error, a 400 or 500 will be returned along with a message in the response payload describing the issue.

#### Segmentation Job Output

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/output

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/output", {
        "segmentNumber": 1,
        "outputSpecification": "5",
        "addCommunication": true,
        "contactType": "ASP"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* outputSpecification (required) - The output specification to use when generating job output in the segmentation job run
* contactType (required) - The organization contact type for the segmentation job run. (Must be a valid code value for the code type `DDCORGCNTP`.)
* addCommunication (required) - Whether to auto add a communication record in the segmentation job run.
* numberOfGroups (required) - The number of groups for the segmentation job output. (The numberOfGroups must be between 1 and 10, inclusive.)
* segmentNumber (optional) - The segment number to run the segmentation job output. (If not provided or null, the output will be run over all segments.)
* everyNth (optional) - Every nth number for the segmentation job output.
* maximumPerGroup (optional) - The maximum quantity per group for the segmentation job output.
* captureRemainder (optional) - Whether to capture the remainder for the segmentation job output.
* communicationShortComment (optional) - The communication short comment for the segmentation job run.
* overrideEmailSubscriptionType (optional) - The override email subscription to use in the segmentation job run. (Must be a valid code value for the code type `DDCESUBTP`.)
* overridePreferredCategory (optional) - The override preferred category for Email and Phone to use in segmentation job run. (If overrideEmailSubscription is provided, this field will only apply to phone. Must be a valid code value for the code type `DDCASNFUNC`.)
* overrideAddressType (optional) - The override address type for the segmentation job run. (Must be a valid code value for the code type `DDCADDRTYP`.)
* overrideSalutationType (optional) - The override salutation type for the segmentation job run. (Must be a valid code value for the code type `DDCSALUTYP`.)
* overrideEmailType (optional) - The override email type for the segmentation job run. (Only used if overrideEmailSubscriptionType and overridePreferredCategory are not provided. Must be a valid code value for the code type `DDCMAILTYP`.)
* overridePhoneType (optional) - The override phone type for the segmentation job run. (Only used if overridePreferredCategory is not provided. Must be a valid code value for the code type `DDCPHONTYP`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job output has an error, a 400 or 500 will be returned. In the case where addCommunication is true and any of the segmentation job segments do not have a source, the response will be a 200 with a warning message. Segments must exist on the job or an error message 400 response will be returned.

#### Segmentation Job Output Results

##### List all segmentation job output results

```
DEFINITION
GET http://apiserver/segmentationjobs/:id/outputresults

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/541/outputresults");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    }
    "items": [
        {
            "id": "1000000006",
            "tableName": "NJ541_SEGMENT_2_OUTSPEC_3_B",
            "createdDate": "2019-02-22T10:00:23 AM",
            "outputSpecificationId": 2,
            "outputSpecificationDescription": "Output Specification Number Two",
            "segmentNumber": 2,
            "segmentDescription": "Segment Number Two",
            "groupName": "B",
            "rowCount": 432
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation job output results.

###### Returns

A dictionary with an items property that contains an array of up to limit segmentation job output results, starting at index offset. Each entry in the array is a separate segmentation job output result object. If no more segmentation job output results are available, the resulting array will be empty. This request should never return an error.

##### Retrieve raw data for a segmentation job output result

```
DEFINITION
GET http://apiserver/segmentationjobs/:id/outputresults/:id/raw

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/541/outputresults/1839283/raw");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    }
    "items": [
        {
            "RecordId": 1839283,
            "JobNumber": 541,
            "SegmentNumber": 1,
            "AccountNumber": 235342,
            "SourceCode": "MYSOURCE",
            "Title": "Dr.",
            "FirstName": "Thomas",
            "MiddleName": "William",
            ...
        },
        {...},
        {...}
    ]
}

```

Returns a list of segmentation job output result raw data records.

###### Returns

A dictionary with an items property that contains an array of up to limit segmentation job output result raw data records, starting at index offset. Each entry in the array is a separate segmentation job output result raw data record. If no more segmentation job output results raw data records are available, the resulting array will be empty. This request should never return an error.

#### Segmentation Job Project Account Relationship Update

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/projectaccountrelationshipupdate

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/projectaccountrelationshipupdate", {
        "action":"ADD",
        "filterBy":"PROJECT",
        "project":"101011"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* action (required) - The action to perform on project account relationship in the segmentation job project account relationship update process. (Must be one of the following: `ADD` or `DELETE`.)
* filterBy (required) - The method to filter project account relationships by in the segmentation job project account relationship update process. (Must be one of the following: `PROJECT` or `CODE`.)
* segmentNumber (optional) - The segment number used in the segmentation job project account relationship update process. (If not provided or null, the output will be run over all segments.)
* project (optional) - The project to perform the action on in the segmentation job project account relationship update process. (Must be a valid code value for the code type `DDCPROJ`. Required if filterBy is `PROJECT`.)
* codeType (optional) - The project code type to perform the action on in the segmentation job project account relationship update process. (Must be a valid and active code type in the `PROJECT` category. Required if filterBy is `CODE`.)
* codeValue (optional) - The value of the codeType to perform the action on in the segmentation job project account relationship update process. (Must be a valid code value for the codeType. Required if filterBy is `PROJECT`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job project account relationship update process has an error, a 500 will be returned.

#### Segmentation Job Run

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/run

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/run", {
        "isStandardRun": true,
        "useFamilies": true,
        "generateJobOutput": true,
        "outputSpecification": "5",
        "addCommunication": true,
        "contactType": "ASP"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* isStandardRun (required) - Is the segmentation job run a standard one or just generate SQL only.
* useFamilies (required) - Whether to use families in the segmentation job run.
* generateJobOutput (optional) - Whether to generate segmentation job output in the job run. (Required if isStandardRun is true. Not used if isStandardRun is false.)
* outputSpecification (optional) - The output specification to use when generating job output in the segmentation job run (Required if isStandardRun and generateJobOutput are both true. Not used if isStandardRun and generateJobOutput are both false.)
* contactType (optional) - The organization contact type for the segmentation job run. (Required if isStandardRun and generateJobOutput are both true. Not used if both isStandardRun and generateJobOutput are both false. Must be a valid code value for the code type `DDCORGCNTP`.)
* addCommunication (optional) - Whether to auto add a communication record in the segmentation job run. (Required if isStandardRun and generateJobOutput are both true. Not used if both isStandardRun and generateJobOutput are both false.)
* communicationShortComment (optional) - The communication short comment for the segmentation job run. (Only used if isStandardRun, generateJobOutput, and addCommunication are all true.)
* overrideEmailSubscriptionType (optional) - The override email subscription to use in the segmentation job run. (Only used if isStandardRun and generateJobOutput are both true. Must be a valid code value for the code type `DDCESUBTP`.)
* overridePreferredCategory (optional) - The override preferred category for Email and Phone to use in segmentation job run. (Only used if isStandardRun and generateJobOutput are both true. If overrideEmailSubscription is provided, this field will only apply to phone. Must be a valid code value for the code type `DDCASNFUNC`.)
* overrideAddressType (optional) - The override address type for the segmentation job run. (Only used if isStandardRun and generateJobOutput are both true. Must be a valid code value for the code type `DDCADDRTYP`.)
* overrideSalutationType (optional) - The override salutation type for the segmentation job run. (Only used if isStandardRun and generateJobOutput are both true. Must be a valid code value for the code type `DDCSALUTYP`.)
* overrideEmailType (optional) - The override email type for the segmentation job run. (Only used if isStandardRun and generateJobOutput are both true and overrideEmailSubscriptionType and overridePreferredCategory are not provided. Must be a valid code value for the code type `DDCMAILTYP`.)
* overridePhoneType (optional) - The override phone type for the segmentation job run. (Only used if isStandardRun and generateJobOutput are both true and overridePreferredCategory is not provided. Must be a valid code value for the code type `DDCPHONTYP`.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job run has an error, a 400 or 500 will be returned. In the case where addCommunication is true and any of the segmentation job segments do not have a source, the response will be a 200 with a warning message.

#### Segmentation Job Send To Email

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/sendtoemail

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/sendtoemail", {
        "emailService": "CONSTCNTCT",
        "emailListName": "Donors",
        "emailListType": "ANNUAL",
        "addCommunication": false
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* emailService (required) - The email service to use when running the segmentation job sent to email process. (Must be a valid code value for the code type `DDCEMLSRV`.)
* emailListName (required) - The email list name to use when running the segmentation job sent to email process.
* emailListType (optional) - The email list type to use when running the segmentation job sent to email process. (Must be a valid code value for the code type `DDCEMLLIST`.) (Required when the emailService is not Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP`.)
* addCommunication (required) - Whether to auto add a communication record during the segmentation job send to email process.
* segmentNumber (optional) - The segment number used in the segmentation job send to email process. (If not provided or null, the output will be run over all segments.)
* communicationShortComment (optional) - The communication short comment for the segmentation job send to email process. (Only used if addCommunication is true.)
* overrideEmailSubscriptionType (optional) - An email subscription type used to limit or narrow the email addresses that are sent.
* overrideFunctionalCategory (optional) - A function category used to limit or narrow the email addresses that are sent.
* overrideEmailType (optional) - An email type used to limit or narrow the email addresses that are sent.
* action (optional) - The operation that should be done. Possible options: `LIST` - Syncing account data and adding accounts to a contact list; `SYNC` - Only syncing account data; `OPTOUT` - Posting opted-out or inactive email addresses to the emailService. (Only used and required with the Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP` emailService.)
* onlySendPrimaryEmail (optional) - Whether or not to only send an accounts' primary email addresses. (Only used and required with the Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP` emailService.)
* overwriteEmailListName (optional) - Set this to true when you want to overwrite an email list if it already exists. (SilverPop does not allow the list to be overwritten; this field is ignored if the emailService is non-Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP`.)
* emailDatabaseName (optional) - The email database name to use when running the segmentation job send to email process. (Only used and required with the `MAILCHIMP` emailService.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job sent to email process has an error, a 400 or 500 will be returned. The segmentation job must have been run first and accounts must exist on the job or an error message 400 response will be returned.

#### Segmentation Job StudioOnline Publish

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/studioonlinepublish

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/studioonlinepublish");

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

##### Returns

Returns a 204 No Content response on success. The segmentation job must have been run first or an error message 400 response will be returned. If the segmentation job StudioOnline publish process has an error, a 500 will be returned.

#### Segmentation Job Update Source Counts

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/updatesourcecounts

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/updatesourcecounts", {
        "segmentNumber":600
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentNumber (optional) - The segment number used in the segmentation job update source counts process. (If not provided or null, the output will be run over all segments.)

##### Returns

Returns a 204 No Content response on success. If the segmentation job update source counts process has an error, a 500 will be returned.

#### Segmentation Job Manage Assignments

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/bulkmanageassignments

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/bulkmanageassignments", {
        "action": "delete"
        "accessor": 532
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segment (optional) - The segment number used in the segmentation job manage assignments process.
* action (required) - The action (add, update, delete) used in the segmentation job manage assignments process.
* accessor (optional) - The accessor id used in the segmentation job manage assignments process. (required when action is add)
* notAccessor (optional) - Flag used for filtering accessors used in the segmentation job manage assignments process.
* functionalCategory (optional) - The functional category filter used in the segmentation job manage assignments process. (required when action is add)
* type (optional) - The assignment type filter used in the segmentation job manage assignments process.
* isPrimary (optional) - The primary flag used in the segmentation job manage assignments process. (required when action is add)
* isActive (optional) - The active flag used in the segmentation job manage assignments process. (required when action is add)
* start (optional) - The start date used in the segmentation job manage assignments process. (required when action is add)
* end (optional) - The end date used in the segmentation job manage assignments process.
* newAccessor (optional) - The new accessor id used in the segmentation job manage assignments process.
* newFunctionalCategory (optional) - The new functional category used in the segmentation job manage assignments process.
* newType (optional) - The new assignment type used in the segmentation job manage assignments process.
* newIsPrimary (optional) - The new primary flag used in the segmentation job manage assignments process.
* newIsActive (optional) - The new active flag used in the segmentation job manage assignments process.
* newStart (optional) - The new start date used in the segmentation job manage assignments process.
* newEnd (optional) - The new end date used in the segmentation job manage assignments process.

##### Returns

Returns a 204 No Content response on success. If the segmentation job manage assignment process has an error, a 500 will be returned.

### Segmentation Job Segments

#### Create a segmentation job segment

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/segments

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/segments", {
    "id": "12548"
    "segmentNumber": "10",
    "description": "Actives",
    "processingSequence": 10,
    "estimatedQuantity": 0,
    "source": "14GDC001",
    "isActive": true,
    "includeInJobOutput": true
});

EXAMPLE RESPONSE
{
    "id": "12548"
    "segmentNumber": "10",
    "description": "Actives",
    "processingSequence": 10,
    "actualQuantity": 0,
    "estimatedQuantity": 0,
    "source": "14GDC001",
    "sourceDescription": "Active Majors",
    "isActive": true,
    "includeInJobOutput": true
}

```

##### Arguments

* segmentNumber (required) - The segment number of the segmentation job segment. (Must be greater than 0 and not already exist.)
* description (required) - The description of the segmentation job segment.
* processingSequence (required) - The processing sequence of the segmentation job segment.
* estimatedQuantity (optional) - The estimated quantity of the segmentation job segment.
* source (optional) - The source fo the segmentation job segment.
* isActive (optional) - Whether or not the segmentation job segment is active. If not specified, will default to true.
* includeInJobOutput (optional) - Whether or not the segmentation job segment should be included in the job output. If not specified, will default to true.

##### Returns

Returns a segmentation job segment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a segmentation job segment

```
DEFINITION
GET http://apiserver/segmentationjobs/:id/segments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/541/segments/12548");

EXAMPLE RESPONSE
{
    "id": "12548"
    "segmentNumber": "10",
    "description": "Actives",
    "processingSequence": 10,
    "actualQuantity": 0,
    "estimatedQuantity": 0,
    "source": "14GDC001",
    "sourceDescription": "Active Majors",
    "isActive": true,
    "includeInJobOutput": true
}

```

Retrieves the details of an existing segmentation job segment. You need only supply the segmentation job segment id.

##### Returns

Returns segmentation job segment object if a valid id was provided.

#### Update a segmentation job segment

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/segments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/segments/12548", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "12548"
    "segmentNumber": "10",
    "description": "Active Majors",
    "processingSequence": 10,
    "actualQuantity": 0,
    "estimatedQuantity": 0,
    "source": "14GDC001",
    "sourceDescription": "Active Majors",
    "isActive": false,
    "includeInJobOutput": true
}

```

##### Arguments

* segmentNumber (optional) - The segment number of the segmentation job segment. (Must be greater than 0 and not already exist.)
* description (optional) - The description of the segmentation job segment.
* processingSequence (optional) - The processing sequence of the segmentation job segment.
* estimatedQuantity (optional) - The estimated quantity of the segmentation job segment.
* source (optional) - The source fo the segmentation job segment.
* isActive (optional) - Whether or not the segmentation job segment is active. If not specified, will default to true.
* includeInJobOutput (optional) - Whether or not the segmentation job segment should be included in the job output. If not specified, will default to true.

##### Returns

Returns segmentation job segment object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a segmentation job segment

```
DEFINITION
DELETE http://apiserver/segmentationjobs/:id/segments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/segmentationjobs/541/segments/12548", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes segmentation job segment. It cannot be undone.

##### Arguments

* id (required) - The id of the segmentation job segment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the segmentation job segment id does not exist, this call returns an error.

#### List all segmentation job segments

```
DEFINITION
GET http://apiserver/segmentationjobs/:id/segments

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/541/segments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "12548"
            "segmentNumber": "10",
            "description": "Active Majors",
            "processingSequence": 10,
            "actualQuantity": 0,
            "estimatedQuantity": 0,
            "source": "14GDC001",
            "sourceDescription": "Active Majors",
            "isActive": false,
            "includeInJobOutput": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation job segments.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit segmentation job segments, starting at index offset. Each entry in the array is a separate job segment specification object. If no more segmentation job segments are available, the resulting array will be empty. This request should never return an error.

#### Bulk update status for segmentation job segments

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/segments/bulkupdatestatus

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/541/segments/bulkupdatestatus", {
    "segmentIds": {
        1,
        2
    },
    "isActive": true
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* segmentIds (required) - The list of segmentation job segments ids to update
* isActive (require) - Whether or not the segmentation job segments are active.

##### Returns

Returns a 204 No Content response on success.

#### Copy segmentation job segment

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/segments/:id/copy

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/568/segments/1/copy", {
    "jobId": 572,
    "segmentId": 3
});

EXAMPLE RESPONSE
{
    id: "22889",
    segmentNumber: 3,
    description: "Major Donor Accounts",
    processingSequence: 1,
    actualQuantity: null,
    estimatedQuantity: 0,
    source: "00711",
    sourceDescription: null,
    isActive: true,
    includeInJobOutput: true
}

```

##### Arguments

* jobId (required) - The destination segmentation job segment job id/number.
* segmentId (required) - The destination segmentation job segment id/number.

##### Returns

Returns the created Segmentation Job Segment object.

#### Retrieve a segmentation job segment criteria

```
DEFINITION
GET http://apiserver/segmentationjobs/:id/segments/:id/criteria

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationjobs/568/segments/1/criteria");

EXAMPLE RESPONSE
{
    "details": [
        {
            "id": 47390,
            "groupId": 1000000991,
            "criteriaType": "LASTNAME",
            "processingSequence": 0,
            "comparisonType": "EQ",
            "comparisonValue": "White",
            "isActive": true
        },
        {
            "id": 47391,
            "groupId": 1000000991,
            "criteriaType": "ZIP",
            "processingSequence": 1,
            "comparisonType": "EQ",
            "comparisonValue": "75002",
            "isActive": true
        },
        {
            "id": 47392,
            "groupId": 1000000991,
            "criteriaType": "FAMMEMTYPE",
            "processingSequence": 2,
            "comparisonType": "NEQ",
            "comparisonValue": "F",
            "isActive": true
        }
    ],
    "sql": {
        "sqlFrom": "INSERT INTO NJ558 (JobNumber, SegmentNumber, AccountNumber)\r\n\t\t\t\tSELECT distinct\r\n\t\t\t\t\t558,\r\n\t\t\t\t\t100,\r\n\t\t\t\t\t(case a01.FamilyId when 0 then A01.AccountNumber else a01.FamilyId end )  FROM dbo.A01_AccountMaster as A01 WITH (NOLOCK) , dbo.A02_AccountAddresses as a02 WITH (NOLOCK), dbo.A03_AddressMaster as a03 WITH (NOLOCK)",
        "sqlWhere": " WHERE ((case a01.FamilyId when 0 then A01.AccountNumber else a01.FamilyId end ) NOT IN (SELECT AccountNumber FROM NJ558)) and ( A01.LastName = 'White' AND  A01.FamilyMemberType != 'F' AND A01.Status ='A') and ( A01.AccountNumber = a02.AccountNumber and a02.addressId = a03.AddressId and a02.UseAsPrimary = 1  and  (case a03.Country when 'USA' then substring(A03.ZipPostal,1,5)  \r\n\t\t\t\t\t\t\t\t\t\t\t\t\twhen 'US' then substring(A03.ZipPostal,1,5) \r\n\t\t\t\t\t\t\t\t\t\t\t\t\telse A03.ZipPostal end )  = '75002')",
        "additionalSqlFrom": null,
        "additionalSqlWhere": null
    }
}

```

Retrieves the details of an existing segmentation job segement criteria. You need only supply the segmentation job id and the segmentation job segement id.

##### Returns

Returns segmentation job segment criteria object if valid ids were provided. Both the set of detail criteria and 4 possible SQL queries are returned.

#### Update a segmentation job segment criteria

```
DEFINITION
POST http://apiserver/segmentationjobs/:id/segments/:id/criteria

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationjobs/568/segments/1/criteria", {
    "deletedCriteriaDetails": [47392],
    "details": [
        {
            "id": 47390,
            "comparisonValue": "Smith",
        }
    ]
    "sql" : {
        "additionalSqlWhere": "--test"
    }
});

EXAMPLE RESPONSE
{
    "details": [
        {
            "id": 47390,
            "groupId": 1000000991,
            "criteriaType": "LASTNAME",
            "processingSequence": 0,
            "comparisonType": "EQ",
            "comparisonValue": "Smith",
            "isActive": true
        },
        {
            "id": 47391,
            "groupId": 1000000991,
            "criteriaType": "ZIP",
            "processingSequence": 1,
            "comparisonType": "EQ",
            "comparisonValue": "75002",
            "isActive": true
        }
    ],
    "sql": {
        "sqlFrom": "INSERT INTO NJ558 (JobNumber, SegmentNumber, AccountNumber)\r\n\t\t\t\tSELECT distinct\r\n\t\t\t\t\t558,\r\n\t\t\t\t\t100,\r\n\t\t\t\t\t(case a01.FamilyId when 0 then A01.AccountNumber else a01.FamilyId end )  FROM dbo.A01_AccountMaster as A01 WITH (NOLOCK) , dbo.A02_AccountAddresses as a02 WITH (NOLOCK), dbo.A03_AddressMaster as a03 WITH (NOLOCK)",
        "sqlWhere": " WHERE ((case a01.FamilyId when 0 then A01.AccountNumber else a01.FamilyId end ) NOT IN (SELECT AccountNumber FROM NJ558)) and ( A01.LastName = 'White' AND  A01.FamilyMemberType != 'F' AND A01.Status ='A') and ( A01.AccountNumber = a02.AccountNumber and a02.addressId = a03.AddressId and a02.UseAsPrimary = 1  and  (case a03.Country when 'USA' then substring(A03.ZipPostal,1,5)  \r\n\t\t\t\t\t\t\t\t\t\t\t\t\twhen 'US' then substring(A03.ZipPostal,1,5) \r\n\t\t\t\t\t\t\t\t\t\t\t\t\telse A03.ZipPostal end )  = '75002')",
        "additionalSqlFrom": null,
        "additionalSqlWhere": "--test"
    }
}

```

##### Arguments

* deletedCriteriaDetails (optional) - This is a list of ids that should be deleted from the segmentation job segment criteria details. This list cannot contain duplicates.
* details (optional) - This list contains any changes you would like to make to any of the segmentation job segment criteria details.
  + id (optional) - The unique identifier for the criteria detail. Required if updating. Do not specify if creating the detail.
  + criteriaType (optional) - The criteria type for the criteria detail.
  + processingSequence (optional) - The processing sequence for the criteria detail.
  + comparisonType (optional) - The comparison type for the criteria detail.
  + comparisonValue (optional) - The comparison value for the criteria detail.
  + isActive (optional) - Whether the criteria detail should be active or not
* sql (optional) - This object contains any changes you would like to make to the sql of the segmentation job segment criteria
  + additionalSqlFrom (optional) - The additional FROM SQL clause to change.
  + additionalSqlWhere (optional) - The additional WHERE SQL clause to change.

##### Returns

Returns segmentation job segment criteria object if valid ids were provided. Both the set of detail criteria and 4 possible SQL queries are returned. Any parameters not provided will be left unchanged.

### Segmentation Output Specifications

#### Create a segmentation output specification

```
DEFINITION
POST http://apiserver/segmentationoutputspecifications

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationoutputspecifications", {
    "description": "Basic Contact Information",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "1",
    "description": "Basic Contact Information",
    "isActive": true
}

```

##### Arguments

* id (required) - The segmentation output data specification.
* description (required) - The description of the segmentation output specification.
* isActive (optional) - Whether the segmentation output specification is active. (If not provided, isActive will be defaulted to 'true'.)

##### Returns

Returns a segmentation output specification object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a segmentation output specification

```
DEFINITION
GET http://apiserver/segmentationoutputspecifications/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationoutputspecifications/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "description": "Basic Contact Information",
    "isActive": true
}

```

Retrieves the details of an existing segmentation output specification. You need only supply the segmentation output specification id.

##### Returns

Returns segmentation output specification object if a valid id was provided.

#### Update a segmentation output specification

```
DEFINITION
POST http://apiserver/segmentationoutputspecifications/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationoutputspecifications/1", {
        "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1",
    "description": "Basic Contact Information",
    "isActive": false
}

```

##### Arguments

* description (optional) - The description of the segmentation output specification.
* isActive (optional) - Whether the segmentation output specification is active.

##### Returns

Returns segmentation output specification object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a segmentation output specification

```
DEFINITION
DELETE http://apiserver/segmentationoutputspecifications/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/segmentationoutputspecifications/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes segmentation output specification. It cannot be undone.

##### Arguments

* id (required) - The id of the segmentation output specification to be deleted.

##### Returns

Returns a 204 No Content response on success. If the segmentation output specification id does not exist, this call returns an error.

#### List all segmentation output specifications

```
DEFINITION
GET http://apiserver/segmentationoutputspecifications

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationoutputspecifications?isActive=false");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "1",
            "description": "Basic Contact Information",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation output specifications.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - The id of the segmentation output specifications to retrieve.
* description (optional) - The description of the segmentation output specifications to retrieve.
* isActive (optional) - Whether to return active segmentation output specifications.

##### Returns

A dictionary with an items property that contains an array of up to limit segmentation output specifications, starting at index offset. Each entry in the array is a separate segmentation output specification object. If no more segmentation output specifications are available, the resulting array will be empty. This request should never return an error.

### Segmentation Output Specification Details

#### Create a segmentation output specification detail

```
DEFINITION
POST http://apiserver/segmentationoutputspecifications/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationoutputspecifications/1/details", {
    "id": "BDATE",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "BDATE",
    "isActive": true
}

```

##### Arguments

* id (required) - The segmentation output data specification detail output data type.
* isActive (optional) - Whether the segmentation output specification detail is active. (If not provided, isActive will be defaulted to 'true'.)

##### Returns

Returns a segmentation output specification detail object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a segmentation output specification detail

```
DEFINITION
GET http://apiserver/segmentationoutputspecifications/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationoutputspecifications/1/details/BDATE");

EXAMPLE RESPONSE
{
    "id": "BDATE",
    "isActive": true
}

```

Retrieves the details of an existing segmentation output specification detail. You need only supply the segmentation output specification detail id.

##### Returns

Returns segmentation output specification detail object if a valid id was provided.

#### Update a segmentation output specification detail

```
DEFINITION
POST http://apiserver/segmentationoutputspecifications/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationoutputspecifications/1/details/BDATE", {
        "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "BDATE",
    "isActive": false
}

```

##### Arguments

* isActive (optional) - Whether the segmentation output specification detail is active.

##### Returns

Returns segmentation output specification detail object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a segmentation output specification detail

```
DEFINITION
DELETE http://apiserver/segmentationoutputspecifications/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/segmentationoutputspecifications/1/details/BDATE", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes segmentation output specification detail. It cannot be undone.

##### Arguments

* id (required) - The id of the segmentation output specification detail to be deleted.

##### Returns

Returns a 204 No Content response on success. If the segmentation output specification detail id does not exist, this call returns an error.

#### List all segmentation output specification details

```
DEFINITION
GET http://apiserver/segmentationoutputspecifications/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationoutputspecifications/1/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "BDATE",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation output specification details.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit segmentation output specification details, starting at index offset. Each entry in the array is a separate segmentation output specification detail object. If no more segmentation output specification details are available, the resulting array will be empty. This request should never return an error.

### Segmentation Output Types

#### Create a segmentation output type

```
DEFINITION
POST http://apiserver/segmentationoutputtypes

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationoutputtypes", {
    "id": "ADDRESS",
    "description": "Mailing address",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "ADDRESS",
    "description": "Mailing address",
    "isActive": true
}

```

##### Arguments

* id (required) - The segmentation output data type.
* description (required) - The description of the segmentation output type.
* isActive (optional) - Whether the segmentation output type is active. (If not provided, isActive will be defaulted to 'true'.)

##### Returns

Returns a segmentation output type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a segmentation output type

```
DEFINITION
GET http://apiserver/segmentationoutputtypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationoutputtypes/address");

EXAMPLE RESPONSE
{
    "id": "ADDRESS",
    "description": "Mailing address",
    "isActive": true
}

```

Retrieves the details of an existing segmentation output type. You need only supply the segmentation output type id.

##### Returns

Returns segmentation output type object if a valid id was provided.

#### Update a segmentation output type

```
DEFINITION
POST http://apiserver/segmentationoutputtypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/segmentationoutputtypes/address", {
        "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "ADDRESS",
    "description": "Mailing address",
    "isActive": false
}

```

##### Arguments

* description (optional) - The description of the segmentation output type.
* isActive (optional) - Whether the segmentation output type is active.

##### Returns

Returns segmentation output type object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a segmentation output type

```
DEFINITION
DELETE http://apiserver/segmentationoutputtypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/segmentationoutputtypes/address", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes segmentation output type. It cannot be undone.

##### Arguments

* id (required) - The id of the segmentation output type to be deleted.

##### Returns

Returns a 204 No Content response on success. If the segmentation output type id does not exist, this call returns an error.

#### List all segmentation output types

```
DEFINITION
GET http://apiserver/segmentationoutputtypes

EXAMPLE REQUEST
$.get("http://localhost:49195/segmentationoutputtypes?isActive=false");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "ADDRESS",
            "description": "Mailing address",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all segmentation output types.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - The id of the segmentation output types to retrieve.
* description (optional) - The description of the segmentation output types to retrieve.
* isActive (optional) - Whether to return active segmentation output types.

##### Returns

A dictionary with an items property that contains an array of up to limit segmentation output types, starting at index offset. Each entry in the array is a separate segmentation output type object. If no more segmentation output types are available, the resulting array will be empty. This request should never return an error.

### Sources

#### Create a source

```
DEFINITION
POST http://apiserver/sources

EXAMPLE REQUEST
$.post("http://localhost:49195/sources", {
    "isActive": true,
    "id": "SAVCHLD",
    "description": "Source saving children",
    "elementGroup": "D10D",
    "start": "2015-03-18",
    "defaultProject": "101010",
    "defaultSubscription": "DECISION",
    "defaultEvent": "DTDD",
    "end": "2015-04-29"
});

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "Source saving children",
    "elementGroup": "D10D",
    "start": "2015-03-18",
    "end": "2015-04-29",
    "isActive": true,
    "defaultProject": "101010",
    "defaultSubscription": "DECISION",
    "defaultEvent": "DTDD",
    "company": null
}

```

Creates a new source.

##### Arguments

* id (required) - The unique code for the new source.
* defaultProject (required) - The default project for each donation with this source.
* description (optional) - The description of the source.
* elementGroup (optional) - The element group of the source.
* start (optional) - The start date of the source.
* end (optional) - The end date of the source.
* isActive (optional) - Whether the source is active or not.
* defaultSubscription (optional) - The default subscription for the source.
* defaultEvent (optional) - The default event for the source.

##### Returns

Returns a source object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve a source

```
DEFINITION
GET http://apiserver/sources/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/11DRA100");

EXAMPLE RESPONSE
{
    "id": "11DRA100",
    "description": "DM 2010 Apr Major Donors",
    "elementGroup": "11DRA",
    "start": "2010-05-05",
    "end": null,
    "isActive": true,
    "defaultProject": "110500",
    "defaultSubscription": null,
    "defaultEvent": null,
    "company": "10"
}

```

Retrieves the details of an existing source. You need only supply the source code.

##### Arguments

* id (required) - The source code of the source to retrieve.

##### Returns

Returns a source object if a valid id was provided.

#### Update a source

```
DEFINITION
POST http://apiserver/sources/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD", {
    "elementGroup": "WTR10"
});

EXAMPLE RESPONSE
{
    "id": "SAVCHLD",
    "description": "Source saving children",
    "elementGroup": "WTR10",
    "start": "2015-03-18",
    "end": "2015-04-29",
    "isActive": true,
    "defaultProject": "101010",
    "defaultSubscription": "DECISION",
    "defaultEvent": "DTDD",
    "company": null
}

```

Updates the specified source by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* defaultProject (optional) - The default project for each donation with this source.
* description (optional) - The description of the source.
* elementGroup (optional) - The element group of the source.
* start (optional) - The start date of the source.
* end (optional) - The end date of the source.
* isActive (optional) - Whether the source is active or not.
* defaultSubscription (optional) - The default subscription for the source.
* defaultEvent (optional) - The default event for the source.

##### Returns

Returns the source object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid default project, subscription, or event code).

#### Delete a source

```
DEFINITION
DELETE http://apiserver/sources/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sources/SAVCHLD", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source. It cannot be undone.

##### Arguments

* id (required) - The source code of the source to be deleted.

##### Returns

Returns a 204 No Content response on success. If the source does not exist, this call returns an error.

#### List all sources

```
DEFINITION
GET http://apiserver/sources

EXAMPLE REQUEST
$.get("http://localhost:49195/sources");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 242
    }
    "items": [
        {
            "id": "11DRA100",
            "description": "DM 2010 Apr Major Donors"
            "elementGroup": "11DRA",
            "start": "2010-05-05",
            "end": null,
            "isActive": true,
            "defaultProject": "110500",
            "defaultSubscription": null,
            "defaultEvent": null,
            "company": "10"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all sources matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in source code
* description () - Filter list by partial match in source description
* start () - Filter list by start date on or after the specified value
* end () - Filter list by end date on or before the specified value
* isActive () - Filter list by whether active or not

##### Returns

A dictionary with an items property that contains an array of up to limit sources, starting at index offset. Each entry in the array is a separate source object. If no more sources are available, the resulting array will be empty. This request should never return an error.

### Source Actual

#### Retrieve a source actual

```
DEFINITION
GET http://apiserver/sources/:id/actual

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/1111A0FC/actual");

EXAMPLE RESPONSE
{
    "numberContacted": 200,
    "actualCost": 15.79,
    "numberOfResponses": 141,
    "giftIncome": 10481.74,
    "numberOfGifts": 62,
    "salesIncome": 3487.22,
    "numberOfSales": 86,
    "subscriptionIncome": 26.22,
    "numberOfSubscriptions": 3,
    "registrationIncome": 8400,
    "numberRegistered": 1,
    "nonCashGiftIncome": 0,
    "numberOfNonCashGifts": 0,
    "numberOfNoMoneyResponses": 0,
    "newAccounts": 51,
    "percentResponse": 70.5
}

```

Retrieves the source actual. You need only supply the source code.

##### Arguments

* id (required) - The source code.

##### Returns

Returns a source actual object if a valid id was provided.

#### Update a source actual

```
DEFINITION
POST http://apiserver/sources/:id/actual

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/1111A0FC/actual", {
    "numberContacted": 201,
    "actualCost": 15.95
});

EXAMPLE RESPONSE
{
    "numberContacted": 201,
    "actualCost": 15.95,
    "numberOfResponses": 141,
    "giftIncome": 10481.74,
    "numberOfGifts": 62,
    "salesIncome": 3487.22,
    "numberOfSales": 86,
    "subscriptionIncome": 26.22,
    "numberOfSubscriptions": 3,
    "registrationIncome": 8400,
    "numberRegistered": 1,
    "nonCashGiftIncome": 0,
    "numberOfNonCashGifts": 0,
    "numberOfNoMoneyResponses": 0,
    "newAccounts": 51,
    "percentResponse": 70.5
}

```

Updates the specified source actual by setting the values of the parameters passed. Any parameters not provided will be left unchanged. The only properties that allow modification are `numberContacted` and `actualCost`. The other properties are calculated fields and are read-only. If values are provided for the read-only properties, the values will be ignored.

##### Arguments

* numberContacted (optional) - The number of accounts contacted.
* actualCost (optional) - The actual cost.

##### Returns

Returns the source actual object if the update succeeded. Returns an error if parameters are invalid.

### Source Attachments

#### Create a source attachment

```
DEFINITION
POST http://apiserver/sources/:id/attachments

EXAMPLE REQUEST
{
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new source attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a source attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a source attachment

```
DEFINITION
GET http://apiserver/sources/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing source attachment. You need only supply the source id and source attachment id.

##### Returns

Returns a source attachment object if a valid id was provided.

##### Arguments

* id (required) - The id of the account attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

#### Update a source attachment

```
DEFINITION
POST http://apiserver/sources/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/attachments/49", {
    "type": "LOGO",
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified source attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the source attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a source attachment

```
DEFINITION
DELETE http://apiserver/sources/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sources/SAVCHLD/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the source attachment id does not exist, this call returns an error.

#### List all source attachments

```
DEFINITION
GET http://apiserver/sources/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all source attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit source attachments, starting at index offset. Each entry in the array is a separate source attachment object. If no more source attachments are available, the resulting array will be empty. This request should never return an error.

### Source Codes

#### Create a source code

```
DEFINITION
POST http://apiserver/sources/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/codes", {
    "type": "DDCSRCWHS",
    "value": "01"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCSRCWHS",
    "typeDescription": "Warehouse",
    "value": "01",
    "valueDescription": "Amazing Facts",
    "isActive": true
}

```

Creates a new source code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a source code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a source code

```
DEFINITION
GET http://apiserver/sources/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/codes/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCSRCWHS",
    "typeDescription": "Warehouse",
    "value": "01",
    "valueDescription": "Amazing Facts",
    "isActive": true
}

```

Retrieves the details of an existing source code. You need only supply the source id and source code id.

##### Returns

Returns a source code object if a valid id was provided.

#### Update a source code

```
DEFINITION
POST http://apiserver/sources/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/codes/16", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCSRCWHS",
    "typeDescription": "Warehouse",
    "value": "01",
    "valueDescription": "Amazing Facts",
    "isActive": false
}


```

Updates the specified source code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the source code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a source code

```
DEFINITION
DELETE http://apiserver/sources/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sources/SAVCHLD/codes/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source code. It cannot be undone.

##### Arguments

* id (required) - The id of the account code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the source code id does not exist, this call returns an error.

#### List all source codes

```
DEFINITION
GET http://apiserver/sources/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "16",
            "type": "DDCSRCWHS",
            "typeDescription": "Warehouse",
            "value": "01",
            "valueDescription": "Amazing Facts",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all source codes.

##### Returns

A dictionary with an items property that contains an array of up to limit source codes, starting at index offset. Each entry in the array is a separate source code object. If no more source codes are available, the resulting array will be empty. This request should never return an error.

### Source Dates

#### Create a source date

```
DEFINITION
POST http://apiserver/sources/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/dates", {
    "type": "MAILDATE",
    "value": "2015-03-18"
});

EXAMPLE RESPONSE
{
    "id": "22",
    "type": "MAILDATE",
    "typeDescription": "Mailing Date",
    "value": "2015-03-18",
    "isActive": true
}

```

Creates a new source date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a source date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a source date

```
DEFINITION
GET http://apiserver/sources/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/dates/22");

EXAMPLE RESPONSE
{
    "id": "22",
    "type": "MAILDATE",
    "typeDescription": "Mailing Date",
    "value": "2015-03-18",
    "isActive": true
}

```

Retrieves the details of an existing source date. You need only supply the source id and source date id.

##### Returns

Returns a source date object if a valid id was provided.

#### Update a source date

```
DEFINITION
POST http://apiserver/sources/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/dates/22", {
    "value": "2015-03-11",
});

EXAMPLE RESPONSE
{
    "id": "22",
    "type": "MAILDATE",
    "typeDescription": "Mailing Date",
    "value": "2015-03-11",
    "isActive": false
}


```

Updates the specified source date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the source date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a source date

```
DEFINITION
DELETE http://apiserver/sources/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sources/SAVCHLD/dates/22", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source date. It cannot be undone.

##### Arguments

* id (required) - The id of the account date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the source date id does not exist, this call returns an error.

#### List all source dates

```
DEFINITION
GET http://apiserver/sources/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "22",
            "type": "MAILDATE",
            "typeDescription": "Mailing Date",
            "value": "2015-03-11",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all source dates.

##### Returns

A dictionary with an items property that contains an array of up to limit source dates, starting at index offset. Each entry in the array is a separate source date object. If no more source dates are available, the resulting array will be empty. This request should never return an error.

### Source Notes

#### Create a source note

```
DEFINITION
POST http://apiserver/sources/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/notes", {
    "type": "SOPRJTITLE",
    "shortComment": "example",
    "longComment":"This is an example comment.\nMultiple lines are supported."
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SOPRJTITLE",
    "description": "SO Project Title",
    "shortComment": "example",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Creates a new source note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a source note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a source note

```
DEFINITION
GET http://apiserver/sources/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/notes/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SOPRJTITLE",
    "description": "SO Project Title",
    "shortComment": "example",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Retrieves the details of an existing source note. You need only supply the source id and source note id.

##### Returns

Returns a source note object if a valid id was provided.

#### Update a source note

```
DEFINITION
POST http://apiserver/sources/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/notes/9", {
    "shortComment": "time for an edit"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SOPRJTITLE",
    "description": "SO Project Title",
    "shortComment": "time for an edit",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}


```

Updates the specified source note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the source note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type).

#### Delete a source note

```
DEFINITION
DELETE http://apiserver/sources/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sources/SAVCHLD/notes/11", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source note. It cannot be undone.

##### Arguments

* id (required) - The id of the account note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the source note id does not exist, this call returns an error.

#### List all source notes

```
DEFINITION
GET http://apiserver/sources/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "9",
            "type": "SOPRJTITLE",
            "description": "SO Project Title",
            "shortComment": "time for an edit",
            "longComment": "This is an example comment.\nMultiple lines are supported."
        },
        {...},
        {...}
    ]
}

```

Returns a list of all source notes.

##### Returns

A dictionary with an items property that contains an array of up to limit source notes, starting at index offset. Each entry in the array is a separate source note object. If no more source notes are available, the resulting array will be empty. This request should never return an error.

### Source Numbers

#### Create a source number

```
DEFINITION
POST http://apiserver/sources/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/numbers", {
    "type": "SOURCENUMS",
    "value": "700"
});

EXAMPLE RESPONSE
{
    "id": "10",
    "type": "SOURCENUMS",
    "typeDescription": "Source Numbers Single",
    "value": 700,
    "isActive": true
}

```

Creates a new source number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a source number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a source number

```
DEFINITION
GET http://apiserver/sources/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/numbers/10");

EXAMPLE RESPONSE
{
    "id": "10",
    "type": "SOURCENUMS",
    "typeDescription": "Source Numbers Single",
    "value": 700,
    "isActive": true
}

```

Retrieves the details of an existing source number. You need only supply the source id and source number id.

##### Returns

Returns a source number object if a valid id was provided.

#### Update a source number

```
DEFINITION
POST http://apiserver/sources/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/SAVCHLD/numbers/10", {
    "value": 800
});

EXAMPLE RESPONSE
{
    "id": "10",
    "type": "SOURCENUMS",
    "typeDescription": "Source Numbers Single",
    "value": 800,
    "isActive": true
}


```

Updates the specified source number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the source number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Delete a source number

```
DEFINITION
DELETE http://apiserver/sources/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sources/SAVCHLD/numbers/10", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source number. It cannot be undone.

##### Arguments

* id (required) - The id of the account number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the source number id does not exist, this call returns an error.

#### List all source numbers

```
DEFINITION
GET http://apiserver/sources/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/SAVCHLD/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10",
            "type": "SOURCENUMS",
            "typeDescription": "Source Numbers Single",
            "value": 800,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all source numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit source numbers, starting at index offset. Each entry in the array is a separate source number object. If no more source numbers are available, the resulting array will be empty. This request should never return an error.

### Source Offerings

#### Create a source offering

```
DEFINITION
POST http://apiserver/sources/:id/offerings

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/0700A/offerings", {
    "product": "BK1001",
    "price": "RP",
    "amount": 32,
    "isPrimaryOffering": true
});

EXAMPLE RESPONSE
{
    "id": "10475",
    "product": "BK1001",
    "productDescription": "From the Cross to Pentecost",
    "price": "RP",
    "priceDescription": "Retail Price",
    "amount": 32,
    "isPrimaryOffering": true
}

```

Creates a new source offering.

##### Arguments

* product (required) - The product code. Must be a defined product.
* price (required) - The price code. Must be a defined price code.
* amount (required) - The amount.
* isPrimaryOffering (optional) - Whether or not the offering is a primary offering.

#### Retrieve a source offering

```
DEFINITION
GET http://apiserver/sources/:id/offerings/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/0700/offerings/10475");

EXAMPLE RESPONSE
{
    "id": "10475",
    "product": "BK1001",
    "productDescription": "From the Cross to Pentecost",
    "price": "RP",
    "priceDescription": "Retail Price",
    "amount": 32,
    "isPrimaryOffering": true
}

```

Retrieves the details of an existing source offering. You need only supply the id of the source offering.

##### Arguments

* id (required) - The id of the source offering to retrieve

##### Returns

Returns a source offering if a valid id was provided.

#### Update a source offering

```
DEFINITION
POST http://apiserver/sources/:id/offerings/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/0700/offerings/10475", {
    "isPrimaryOffering": false
});

EXAMPLE RESPONSE
{
    "id": "10475",
    "product": "BK1001",
    "productDescription": "From the Cross to Pentecost",
    "price": "RP",
    "priceDescription": "Retail Price",
    "amount": 32,
    "isPrimaryOffering": false
}

```

Updates the specified source offering by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* product (optional) - The product code. Must be a defined product.
* price (optional) - The price code. Must be a defined price code.
* amount (optional) - The amount.
* isPrimaryOffering (optional) - Whether or not the offering is a primary offering.

##### Returns

Returns the source offering object if the update succeeded. Returns an error if parameters are invalid.

#### Delete a source offering

```
DEFINITION
DELETE http://apiserver/sources/:id/offerings/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sources/0700/offerings/10475", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source offering. It cannot be undone.

##### Arguments

* id (required) - The id of the source offering to be deleted.

##### Returns

Returns a 204 No Content response on success. If the source offering id does not exist, this call returns an error.

#### List all source offerings

```
DEFINITION
GET http://apiserver/sources/:id/offerings

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/0700/offerings");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 2
    },
    "items": [
        {
            "id": "10476",
            "product": "1025",
            "productDescription": "Book Series",
            "price": "RP",
            "priceDescription": "Retail Price",
            "amount": 1.59,
            "isPrimaryOffering": true
        },
        { ... }
    ]
}

```

Returns a list of offerings for a source.

##### Returns

A dictionary with an items property that contains an array of up to limit source offerings, starting at index offset. Each entry in the array is a separate source offering object. If no more source offerings are available, the resulting array will be empty. This request should never return an error.

### Source Projection

#### Retrieve a source projection

```
DEFINITION
GET http://apiserver/sources/:id/projection

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/1111A0FC/projection");

EXAMPLE RESPONSE
{
    "contactResponses": 3000,
    "cost": 200,
    "giftIncome": 15000,
    "salesIncome": 0,
    "subscriptionIncome": 0,
    "registrationIncome": 0,
    "nonCashGiftIncome": 0
}

```

Retrieves the source projection. You need only supply the source code.

##### Arguments

* id (required) - The source code.

##### Returns

Returns a source projection object if a valid id was provided.

#### Update a source projection

```
DEFINITION
POST http://apiserver/sources/:id/projection

EXAMPLE REQUEST
$.post("http://localhost:49195/sources/1111A0FC/projection", {
    "cost": 250,
    "giftIncome": 16000
});

EXAMPLE RESPONSE
{
    "contactResponses": 3000,
    "cost": 250,
    "giftIncome": 16000,
    "salesIncome": 0,
    "subscriptionIncome": 0,
    "registrationIncome": 0,
    "nonCashGiftIncome": 0
}

```

Updates the specified source projection by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* contactResponses (optional) - The projected number of contact responses
* cost (optional) - The projected cost
* giftIncome (optional) - The projected donation income
* salesIncome (optional) - The projected order income
* subscriptionIncome (optional) - The projected subscription income
* registrationIncome (optional) - The projected registration income
* nonCashGiftIncome (optional) - The projected non-cash gift income

##### Returns

Returns the source projection object if the update succeeded. Returns an error if parameters are invalid.

### Source Summaries

#### List all source summaries

```
DEFINITION
GET http://apiserver/sources/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sources/11DRA100");

EXAMPLE RESPONSE
{
    "id": "11DRA100",
    "description": "DM 2010 Apr Major Donors",
    "elementGroup": "11DRA",
    "start": "2010-05-05",
    "end": null,
    "isActive": true,
    "defaultProject": "110500",
    "defaultSubscription": null,
    "defaultEvent": null,
    "company": "10"
}

```

Retrieves the details of an existing source. You need only supply the source code.

##### Arguments

* id (required) - The source code of the source to retrieve.

##### Returns

Returns a source object if a valid id was provided.

#### List all sources

```
DEFINITION
GET http://apiserver/sources

EXAMPLE REQUEST
$.get("http://localhost:49195/sources");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 242
    }
    "items": [
        {
            "id": "11DRA100",
            "description": "DM 2010 Apr Major Donors"
            "elementGroup": "11DRA",
            "start": "2010-05-05",
            "end": null,
            "isActive": true,
            "defaultProject": "110500",
            "defaultSubscription": null,
            "defaultEvent": null,
            "company": "10"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all sources matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in source code
* description () - Filter list by partial match in source description
* start () - Filter list by start date on or after the specified value
* end () - Filter list by end date on or before the specified value
* isActive () - Filter list by whether active or not

##### Returns

A dictionary with an items property that contains an array of up to limit sources, starting at index offset. Each entry in the array is a separate source object. If no more sources are available, the resulting array will be empty. This request should never return an error.

### Source Quick Picks

#### Create a source quick pick

```
DEFINITION
POST http://apiserver/sourceQuickPicks

EXAMPLE REQUEST
$.post("http://localhost:49195/sourceQuickPicks", {
    "source": "072711"
});

EXAMPLE RESPONSE
{
    "id": "26",
    "source": "072711",
    "description": "New Accounts",
    "start": null,
    "end": null
}

```

Creates a new source quick pick.

##### Arguments

* source (required) - Valid source code
* start (optional) - Start date
* end (optional) - End date

##### Returns

Returns a source quick pick object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a source quick pick

```
DEFINITION
GET http://apiserver/sourceQuickPicks/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/sourceQuickPicks/26");

EXAMPLE RESPONSE
{
    "id": "26",
    "source": "072711",
    "description": "New Accounts",
    "start": null,
    "end": null
}

```

Retrieves the details of an existing source quick pick. You need only supply the id.

##### Arguments

* id (required) - The id of the source quick pick to retrieve.

##### Returns

Returns a source quick pick object if a valid id was provided.

#### Update a source quick pick

```
DEFINITION
POST http://apiserver/sourceQuickPicks/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sourceQuickPicks/26", {
    "start": "2015-01-01",
    "end": "2016-01-01"
});

EXAMPLE RESPONSE
{
    "id": "26",
    "source": "072711",
    "description": "New Accounts",
    "start": "2015-01-01",
    "end": "2016-01-01"
}

```

Updates the specified source quick pick by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* source (optional) - Source code
* start (optional) - Start date
* end (optional) - End date

##### Returns

Returns the source quick pick object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a source quick pick

```
DEFINITION
DELETE http://apiserver/sourceQuickPicks/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sourceQuickPicks/26", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a source quick pick. It cannot be undone.

##### Arguments

* id (required) - The id of the source quick pick

##### Returns

Returns a 204 No Content response on success. If the source quick pick does not exist, this call returns an error.

#### List all source quick picks

```
DEFINITION
GET http://apiserver/sourceQuickPicks

EXAMPLE REQUEST
$.get("http://localhost:49195/sourceQuickPicks?date=2015-07-04");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 242
    }
    "items": [
        {
            "id": "26",
            "source": "072711",
            "description": "New Accounts",
            "start": "2015-01-01",
            "end": "2016-01-01"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all source quick picks matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* source - Filters by partial match on source code
* date - Filters where `date` is within the `start` and `end` date range

##### Returns

A dictionary with an items property that contains an array of up to limit source quick picks, starting at index offset. Each entry in the array is a separate source quick pick object. If no more source quick picks are available, the resulting array will be empty. This request should never return an error.

### Subscription Management

#### Create a subscription

```
DEFINITION
POST http://apiserver/subscriptions

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions", {
    "id": "EXPLORERS",
    "description": "Little Explorers",
    "type": "M",
    "frequency": "M",
    "expireProcess": "N",
    "fulfillmentMethod": "MAIL",
    "isActive": true,
    "useInStudioOnline": false,
    "autoRenewDefault": false
    "functionalCategory": null,
    "segmentationJobNumber": 550,
    "segmentationEmails": 1,
    "segmentationLetters": 2,
    "autoRenewDaysBefore": 14,
    "autoReneEmailTemplateId": 1142,
    "autoRenewLetterCode": "EXPUPCRNWL",
    "autoRenewSourceCode": "EXPAUTORNW",
    "declineEmailTemplateId": null,
    "delineLetterCode": null,
    "declineSourceCode": null
});

EXAMPLE RESPONSE
{
    "id": "EXPLORERS",
    "description": "Little Explorers",
    "type": "M",
    "frequency": "M",
    "expireProcess": "N",
    "fulfillmentMethod": "MAIL",
    "isActive": true,
    "useInStudioOnline": false,
    "autoRenewDefault": false,
    "functionalCategory": null,
    "segmentationJobNumber": 550,
    "segmentationEmails": 1,
    "segmentationLetters": 2,
    "autoRenewDaysBefore": 14,
    "autoReneEmailTemplateId": 1142,
    "autoRenewLetterCode": "EXPUPCRNWL",
    "autoRenewSourceCode": "EXPAUTORNW",
    "declineEmailTemplateId": null,
    "delineLetterCode": null,
    "declineSourceCode": null
}

```

Creates a new subscription.

##### Arguments

* id (required) - the subscription code to use for the new subscription
* type (required) - the subscription type to use for the new subscription
* description (optional) - the description to use for the new subscription
* frequency (required) - the frequency to use for the new subscription
* fulfillmentMethod (see description) - the fulfillment method to use for the new subscription. If not a membership type (B), field is not required.
* expireProcess (see description) - the expire process to use for the new subscription. If not a membership type (B), field is not required.
* isActive (optional: defaults to true) - is the new subscription active
* useInStudioOnline (required: defaults to false) - should the subscription be used in StudioOnline

##### Returns

Returns a subscription object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription

```
DEFINITION
GET http://apiserver/subscriptions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS");

EXAMPLE RESPONSE
{
    "id": "EXPLORERS",
    "description": "Little Explorers",
    "type": "M",
    "typeDescription": "Magazine",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "expireProcess": "N",
    "expireProcessDescription": "Never Expire",
    "fulfillmentMethod": "MAIL",
    "fulfillmentDescription": "Mail to Subscriber ",
    "isActive": true,
    "useInStudioOnline": false,
    "autoRenewDefault": false,
    "functionalCategory": null,
    "functionalCategoryDescription": null,
    "segmentationJobNumber": 550,
    "segmentationJobNumberDescription": "Subscription Upcoming Auto-Renewal Delivery Method",
    "segmentationEmails": 1,
    "segmentationEmailsDescription": "Accounts to Send Emails For",
    "segmentationLetters": 2,
    "segmentationLettersDescription": "Accounts to Send Letters For",
    "autoRenewDaysBefore": 14,
    "autoRenewEmailTemplateId": 1142,
    "autoRenewEmailTemplateDescription": "Upcoming Auto-Renewal for Little Explorers Magazine",
    "autoRenewLetterCode": "EXPUPCRNWL",
    "autoRenewLetterCodeDescription": "Upcoming Auto-Renewal for EXPLORERS",
    "autoRenewSourceCode": "EXPAUTORNW",
    "autoRenewSourceCodeDescription": "Upcoming Auto-Renewal for EXPLORERS",
    "declineEmailTemplateId": null,
    "declineEmailTemplateDescription": null,
    "declineSourceCode": null,
    "declineSourceCodeDescription": null
}

```

Retrieves the details of an existing subscription. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription to be retrieved.

#### Update a subscription

```
DEFINITION
POST http://apiserver/subscriptions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS", {
    "frequency": "Q"
});

EXAMPLE RESPONSE
{
    "id": "EXPLORERS",
    "description": "Little Explorers",
    "type": "M",
    "frequency": "Q",
    "expireProcess": "N",
    "fulfillmentMethod": "MAIL",
    "isActive": true,
    "useInStudioOnline": false,
    "autoRenewDefault": false,
    "functionalCategory": null,
    "segmentationJobNumber": 550,
    "segmentationEmails": 1,
    "segmentationLetters": 2,
    "autoRenewDaysBefore": 14,
    "autoReneEmailTemplateId": 1142,
    "autoRenewLetterCode": "EXPUPCRNWL",
    "autoRenewSourceCode": "EXPAUTORNW",
    "declineEmailTemplateId": null,
    "delineLetterCode": null,
    "declineSourceCode": null
}

```

Updates the specified subscription by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the subscription type to update the subscription with
* description (optional) - the description to update the subscription with
* frequency (optional) - the frequency to update the subscription with
* fulfillmentMethod (optional) - the fulfillment method to update the subscription with
* expireProcess (optional) - the expire process to update the subscription with
* isActive (optional) - is the new subscription active
* useInStudioOnline (optional) - should the subscription be used in StudioOnline

##### Returns

Returns the subscription object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription

```
DEFINITION
DELETE http://apiserver/subscriptions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription does not exist, this call returns an error.

#### List all subscriptions

```
DEFINITION
GET http://apiserver/subscriptions

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions?type=P");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "EXPLORERS",
            "description": "Little Explorers",
            "type": "P",
            "typeDescription": "Product",
            "frequency": "M",
            "frequencyDescription": "Monthly",
            "expireProcess": "N",
            "expireProcessDescription": "Never Expire",
            "fulfillmentMethod": "MAIL",
            "fulfillmentDescription": "Mail to Subscriber ",
            "isActive": true,
            "useInStudioOnline": false,
            "autoRenewDefault": false,
            "functionalCategory": null,
            "functionalCategoryDescription": null,
            "segmentationJobNumber": 550,
            "segmentationJobNumberDescription": "Subscription Upcoming Auto-Renewal Delivery Method",
            "segmentationEmails": 1,
            "segmentationEmailsDescription": "Accounts to Send Emails For",
            "segmentationLetters": 2,
            "segmentationLettersDescription": "Accounts to Send Letters For",
            "autoRenewDaysBefore": 14,
            "autoRenewEmailTemplateId": 1142,
            "autoRenewEmailTemplateDescription": "Upcoming Auto-Renewal for Little Explorers Magazine",
            "autoRenewLetterCode": "EXPUPCRNWL",
            "autoRenewLetterCodeDescription": "Upcoming Auto-Renewal for EXPLORERS",
            "autoRenewSourceCode": "EXPAUTORNW",
            "autoRenewSourceCodeDescription": "Upcoming Auto-Renewal for EXPLORERS",
            "declineEmailTemplateId": null,
            "declineEmailTemplateDescription": null,
            "declineSourceCode": null,
            "declineSourceCodeDescription": null
        },
        {...},
    ]
}

```

Returns a list of all subscriptions.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* type (optional) - the subscription type to filter results on
* description (optional) - the description to filter results on
* frequency (optional) - the frequency to filter results on
* fulfillmentMethod (optional) - the fulfillment method to filter results on
* expireProcess (optional) - the expire process to filter results on
* isActive (optional) - the active status to filter results on
* forSubscriptionEntry (optional) - if provided, the subscriptions returned will have price information included. This is used for subscription entry.

##### Returns

A dictionary with an items property that contains an array of up to limit subscriptions, starting at index offset. Each entry in the array is a separate subscription object. If no more subscriptions are available, the resulting array will be empty. This request should never return an error.

#### Run membership processing

```
DEFINITION
POST http://apiserver/subscriptions/processmemberships

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/processmemberships", {
    "company": "4",
    "paymentGatewayCode": "CCONNECT",
    "runAsDate": "2016-12-28"
    "runId": 45
});

EXAMPLE RESPONSE
204 No Content

```

Performs membership subscription processing for all membership subscriptions that meet processing criteria.

##### Arguments

* companyCode (required) - the company code to perform membership processing for.
* paymentGatewayCode (optional) - The company payment gateway code to perform membership processing for. If not provided, membership processing will run on all payment gateways of the company.
* runAsDate (optional) - if provided, runs membership processing for that day for any membership subscriptions that have not yet been processed for the month.
* runId (optional) - if provided, runs membership processing with the criteria provided, but will only process membership subscriptions that had errors in the specified run.

#### Run subscription auto-renewal processing

```
DEFINITION
POST http://apiserver/subscriptions/processautorenew

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/processautorenew", {
    "company": "4",
    "paymentGatewayCode": "CCONNECT",
    "runAsDate": "2016-12-28"
    "runId": 45
});

EXAMPLE RESPONSE
204 No Content

```

Performs subscription auto-renewal processing for all subscriptions that meet processing criteria.

##### Arguments

* companyCode (required) - the company code to perform subscription auto-renewal processing for.
* paymentGatewayCode (optional) - The company payment gateway code to perform subscription auto-renewal processing for. If not provided, subscription auto-renewal processing will run on all payment gateways of the company.
* runAsDate (optional) - if provided, runs subscription auto-renewal processing for that day for any auto-renewing subscriptions that have reached the auto-renewal date.
* runId (optional) - if provided, runs subscription auto-renewal processing with the criteria provided, but will only process subscriptions that had errors in the specified run.

### Subscription Advanced StudioOnline Configuration

#### Create a subscription Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/subscriptions/:id/storeconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/2019DAL/storeconfigurations", {
    "store": "19",
    "useInStudioOnline": true,
    "title": "Member Magazine",
    "urlOverride": "member-magazine",
    "description": "Monthly Member Magazine",
    "startDate": "2019-01-01",
    "endDate": "2019-10-05"
});

EXAMPLE RESPONSE
{
    "id": "10004",
    "subscription": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2019-01-01",
    "endDate": "2019-10-05",
    "hideFromSearch": false,
    "title": "Member Magazine",
    "urlOverride": "member-magazine",
    "url": "https://store.aso.com/subscribe/member-magazine",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Monthly Member Magazine",
    "keywords": null,
    "layoutOverride": null
}

```

Creates a new subscription Advanced StudioOnline configuration.

##### Arguments

* store (required) - The unique id of the store this configuration is for. Must be a valid store Id.
* title (required) - The online title for the subscription when used in the specified store.
* description (optional) - The online description for the subscription when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the subscription title.
* useInStudioOnline (optional) - Whether the subscription should be used in the specified store.
* startDate (optional) - The date the subscription will become visible in the specified store.
* endDate (optional) - The date the subscription will be removed from the specified store.
* hideFromSearch (optional) - Whether the subscription should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the subscription when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default subscription layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate subscription that should be shown in StudioOnline if someone tries to navigate to this subscription.

##### Returns

Returns a subscription Advanced StudioOnline configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription Advanced StudioOnline configuration

```
DEFINITION
GET http://apiserver/subscriptions/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/2019DAL/storeconfigurations/10004");

EXAMPLE RESPONSE
{
    "id": "10004",
    "subscription": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2019-01-01",
    "endDate": "2019-10-05",
    "hideFromSearch": false,
    "title": "Member Magazine",
    "urlOverride": "member-magazine",
    "url": "https://store.aso.com/subscribe/member-magazine",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Monthly Member Magazine",
    "keywords": null,
    "layoutOverride": null
}

```

Retrieves the details of a subscription Advanced StudioOnline configuration. You need only supply the subscription id and configuration id.

##### Returns

Returns a subscription Advanced StudioOnline configuration object if valid ids were provided.

#### Update a subscription Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/subscriptions/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/2019DAL/storeconfigurations/10004", {
    "startDate": "2018-12-15",
    "endDate": "2019-10-15"
});

EXAMPLE RESPONSE
{
    "id": "10004",
    "subscription": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2018-12-15",
    "endDate": "2019-10-15",
    "hideFromSearch": false,
    "title": "Member Magazine",
    "urlOverride": "member-magazine",
    "url": "https://store.aso.com/subscribe/member-magazine",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Monthly Member Magazine",
    "keywords": null,
    "layoutOverride": null
}


```

Updates the specified subscription Advanced StudioOnline configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title (optional) - The online title for the subscription when used in the specified store.
* description (optional) - The online description for the subscription when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the subscription title.
* useInStudioOnline (optional) - Whether the subscription should be used in the specified store.
* startDate (optional) - The date the subscription will become visible in the specified store.
* endDate (optional) - The date the subscription will be removed from the specified store.
* hideFromSearch (optional) - Whether the subscription should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the subscription when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default subscription layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate subscription that should be shown in StudioOnline if someone tries to navigate to this subscription.

##### Returns

Returns a subscription Advanced StudioOnline configuration object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid permanentRedirect).

#### Delete a subscription Advanced StudioOnline configuration

```
DEFINITION
DELETE http://apiserver/subscriptions/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/2019DAL/storeconfigurations/10004", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription Advanced StudioOnline configuration. It cannot be undone.

##### Arguments

* id (required) - The subscription Advanced StudioOnline configuration id of the configuration to be deleted.

##### Returns

Returns a 204 No Content response on success. If the subscription Advanced StudioOnline configuration does not exist, this call returns an error.

#### List all subscription Advanced StudioOnline configurations

```
DEFINITION
GET http://apiserver/subscriptions/:id/storeconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/2019DAL/storeconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10004",
            "subscription": "110160",
            "store": "19",
            "storeDescription": "ASO US-English",
            "useInStudioOnline": true,
            "startDate": "2018-12-15",
            "endDate": "2019-10-15",
            "hideFromSearch": false,
            "title": "Member Magazine",
            "urlOverride": "member-magazine",
            "url": "https://store.aso.com/subscribe/member-magazine",
            "permanentRedirect": null,
            "permanentRedirectDescription": null,
            "description": "Monthly Member Magazine",
            "keywords": null,
            "layoutOverride": null
        }
        {...},
        {...}
    ]
}

```

Returns a list of all subscription Advanced StudioOnline configurations matching the provided filter criteria.

##### Arguments

* subscription (required) - Filter list by an exact match in subscription code

##### Returns

A dictionary with an items property that contains an array of up to limit subscription Advanced StudioOnline configurations, starting at index offset. Each entry in the array is a separate subscription Advanced StudioOnline configuration object. If no more subscription Advanced StudioOnline configurations are available, the resulting array will be empty. This request should never return an error.

#### Generate subscription Advanced StudioOnline Url

```
DEFINITION
GET http://apiserver/subscriptions/:id/stores/:id/generateurl

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/2019DAL/stores/19/generateurl", {
    "urlOverride": "member-magazine"
});

EXAMPLE RESPONSE
{
    "url": "https://store.aso.com/subscribe/member-magazine"
}

```

##### Arguments

* urlOverride (required) - The properly formatted Advanced StudioOnline urlOverride for the subscription. If the urlOverride is not properly formatted, it will be properly formatted first.

##### Returns

Returns the url that is used in Advanced StudioOnline to view the subscription. Returns an error if urlOverride is empty.

### Subscription Categories

#### Create a subscription category

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/storeconfigurations/1/categories", {
    "categoryId": 20
});

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Creates a new subscription category for the given StudioOnline store configuration.

##### Arguments

* categoryId (required) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns a subscription category object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription category

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/storeconfigurations/1/categories/14");

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Retrieves the details of an existing subscription category for the given StudioOnline store configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription category to be retrieved.

#### Update a subscription category

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/storeconfigurations/1/categories/14", {
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": true,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}


```

Updates the specified subscription category for the given StudioOnline store configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* categoryId (optional) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns the subscription category object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription category

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/storeconfigurations/1/categories/14", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription category from the given StudioOnline store configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription category to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription category does not exist, this call returns an error.

#### List all subscription categories

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/storeconfigurations/1/categories");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "14",
            "categoryId": "20",
            "categoryName": "Best Sellers",
            "isPrimary": true,
            "isActive": true,
            "breadcrumb": "best-sellers",
            "parentCategoryId": null,
            "parentCategoryName": null
        },
        {...},
    ]
}

```

Returns a list of all subscription categories for the given StudioOnline store configuration.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription categories, starting at index offset. Each entry in the array is a separate subscription category object. If no more subscription categories are available, the resulting array will be empty. This request should never return an error.

### Subscription Codes

#### Create a subscription code

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/codes", {
    "type": "DDCSUBCD2",
    "value": "MFS",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "13",
    "type": "DDCSUBCD2",
    "typeDescription": "Subscription Code - Publishing House",
    "value": "MFS",
    "valueDescription": "Magazine Fulfillment Services",
    "isActive": true
}

```

Creates a new subscription code.

##### Arguments

* type (required) - the code type to create the subscription code with
* value (required) - the code value to create the subscription code with
* isActive (optional: defaults to true) - is the code active

##### Returns

Returns a subscription code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription code

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/codes/13");

EXAMPLE RESPONSE
{
    "id": "13",
    "type": "DDCSUBCD2",
    "typeDescription": "Subscription Code - Publishing House",
    "value": "MFS",
    "valueDescription": "Magazine Fulfillment Services",
    "isActive": true
}

```

Retrieves the details of an existing subscription code. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription code to be retrieved.

#### Update a subscription code

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/:subscriptionCode/codes/13", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "13",
    "type": "DDCSUBCD2",
    "typeDescription": "Subscription Code - Publishing House",
    "value": "MFS",
    "valueDescription": "Magazine Fulfillment Services",
    "isActive": false
}

```

Updates the specified subscription code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the code type to update the subscription code with
* value (optional) - the code value to update the subscription code with
* isActive (optional) - is the code active

##### Returns

Returns the subscription code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription code

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/codes/13", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription code. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription code does not exist, this call returns an error.

#### List all subscription codes

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "13",
            "type": "DDCSUBCD2",
            "typeDescription": "Subscription Code - Publishing House",
            "value": "MFS",
            "valueDescription": "Magazine Fulfillment Services",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all subscription codes.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription codes, starting at index offset. Each entry in the array is a separate subscription code object. If no more subscription codes are available, the resulting array will be empty. This request should never return an error.