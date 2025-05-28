# System Administration

### Accessor Activities

#### Retrieve an accessor activity

```
DEFINITION
GET http://apiserver/accessors/:id/activities/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/activities/237548");

EXAMPLE RESPONSE
{
    "id": "237548",
    "type": "PHONE",
    "date": "2015-07-31",
    "isInbound": false,
    "shortComment": "Thank You Phone Call",
    "longComment": "Personally thank the donor for their generous donation.",
    "url": null,
    "source": "1109A328",
    "sourceDescription": "Donor Mail 2yr Over $10,000",
    "elementGroup": "G12BSCA",
    "elementGroupDescription": "Science and Christianity can Coexist",
    "assignedToAccessor": "1234",
    "assignedToAccessorDescription": "John Doe - Internal User",
    "status": "C",
    "response": null,
    "account": "16335",
    "accountName": "John D. Smith",
    "lastContactDate": "2015-07-25",
    "lastContactType": "EMAIL",
    "lastContactUser": "Jane Doe - Internal User",
    "lastDonationAmount": "100.00"
}

```

Retrieves the details of an existing accessor activity. You need only supply the activity id.

##### Arguments

* id (required) - The id of the accessor activity to be retrieved.
* ignoreAdditionalInformation (optional) - If true, then in the API Response, the following properties will be null on the returned accessor activity object: response, elementGroup and elementGroupDescription
* includeLastContact (optional) - If true, information about the most recent communication for the account will be included in the response.
* includeLastDonation (optional) - If true, the account's most recent donation amount will be included in the response.

#### Update an accessor activity

```
DEFINITION
POST http://apiserver/accessors/:id/activities/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/activities/237548", {
    "status": "O",
});

EXAMPLE RESPONSE
{
    "id": "237548",
    "type": "PHONE",
    "date": "2015-07-31",
    "isInbound": false,
    "shortComment": "Thank You Phone Call",
    "longComment": "Personally thank the donor for their generous donation.",
    "url": null,
    "source": "1109A328",
    "sourceDescription": "Donor Mail 2yr Over $10,000",
    "elementGroup": "G12BSCA",
    "elementGroupDescription": "Science and Christianity can Coexist",
    "assignedToAccessor": "1234",
    "assignedToAccessorDescription": "John Doe - Internal User",
    "status": "O",
    "response": null,
    "account": "16335",
    "accountName": "John D. Smith"
}

```

Updates the specified accessor activity by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The communication type code of the accessor activity. Must be a defined communication type code.
* source (optional) - The source code of the accessor activity. Must be a defind source code.
* date (optional) - The date of the accessor activity.
* isInbound (optional) - Whether or not the accessor activity is inbound.
* shortComment (optional) - The short comment of the accessor activity.
* longComment (optional) - The long comment of the accessor activity.
* url (optional) - The url where the accessor activity is located.
* response (optional) - The accessor activity response object if type is "LETTER"
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.
* status (optional) - the accessor activity status

##### Returns

Returns the accessor activity object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined accessor activity type code).

#### List all accessor activities

```
DEFINITION
GET http://apiserver/accessors/:id/activities

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/activities");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "237548",
            "type": "PHONE",
            "date": "2015-07-31",
            "isInbound": false,
            "shortComment": "Thank You Phone Call",
            "longComment": "Personally thank the donor for their generous donation.",
            "url": null,
            "source": "1109A328",
            "sourceDescription": "Donor Mail 2yr Over $10,000",
            "elementGroup": "G12BSCA",
            "elementGroupDescription": "Science and Christianity can Coexist",
            "assignedToAccessor": "1234",
            "assignedToAccessorDescription": "John Doe - Internal User",
            "status": "C",
            "response": null,
            "account": "16335",
            "accountName": "John D. Smith",
            "lastContactDate": "2015-07-25",
            "lastContactType": "EMAIL",
            "lastContactUser": "Jane Doe - Internal User",
            "lastDonationAmount": "100.00"
        },
        ...
    ]
}

```

Returns a list of all activities for the accessor, matching the provided filter criteria.

##### Arguments

* account () - The account associatied with the activity
* communicationType () - The activity's communication type
* status () - The activity's status
* shortComment () - The activity's short comment.
* longComment () - The activity's long comment.
* includeGroups () - should the results include activities assigned to your group?
* groupMemberAccessorId () - if the accessor in the route is the group leader, retreive activities of the members in their group by the member's accessor Id
* ignoreAdditionalInformation () - If true, then in the API Response, the following properties will be null for every accessor activity object in the items array: response, elementGroup and elementGroupDescription
* includeLastContact () - If true, information about the most recent communication for the account will be included in the response.
* includeLastDonation () - If true, the account's most recent donation amount will be included in the response.

##### Returns

A dictionary with an items property that contains an array of up to limit accessor activity entries, starting at index offset. Each entry in the array is a separate accessor activity entry object. If no more accessor activity entries are available, the resulting array will be empty. This request will return a 404 if accessor is not found.

### Accessor Dashboard Views

#### Create an accessor dashboard view

```
DEFINITION
POST http://apiserver/accessors/:id/dashboardviews

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/dashboardviews", {
    "view": "10015",
    "isChart": false,
    "displaySequence": 0,
    "gridPageSize": 5
});

EXAMPLE RESPONSE
{
    "id": "20030",
    "accessor": "1234",
    "accessorName": "John Doe",
    "view": "10015",
    "viewDescription": "Accounts Assigned to Me",
    "isChart": false,
    "displaySequence": 0,
    "gridPageSize": 5
}

```

Creates a new accessor dashboard view.

##### Arguments

* view (required) - The id of the view to create the dashboard view for
* isChart (required) - Specifies if the dashboard is a chart or grid
* displaySequence (required) - The sequence of the dashboard relative to other dashboards
* gridPageSize (required) - Specifies the number of rows per grid page when the dashboard is rendered as a grid

##### Returns

Returns an accessor dashboard view object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accessor dashboard view

```
DEFINITION
GET http://apiserver/accessors/:id/dashboardviews/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/dashboardviews/20030");

EXAMPLE RESPONSE
{
    "id": "20030",
    "accessor": "1234",
    "accessorName": "John Doe",
    "view": "10015",
    "viewDescription": "Accounts Assigned to Me",
    "isChart": false,
    "displaySequence": 0,
    "gridPageSize": 5
}

```

Retrieves the details of an existing accessor dashboard view. You need only supply the id.

##### Arguments

* id (required) - The id of the accessor dashboard view to be retrieved.

#### Update an accessor dashboard view

```
DEFINITION
POST http://apiserver/accessors/:id/dashboardviews/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/dashboardviews/20030", {
    "displaySequence": 10
});

EXAMPLE RESPONSE
{
    "id": "20030",
    "accessor": "1234",
    "accessorName": "John Doe",
    "view": "10015",
    "viewDescription": "Accounts Assigned to Me",
    "isChart": false,
    "displaySequence": 10,
    "gridPageSize": 5
}


```

Updates the specified accessor dashboard view by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* view - The id of the view for the dashboard
* isChart - Specifies if the dashboard is a chart or grid
* displaySequence - The sequence of the dashboard relative to other dashboards
* gridPageSize - Specifies the number of rows per grid page when the dashboard is rendered as a grid

##### Returns

Returns the accessor dashboard view object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an accessor dashboard view

```
DEFINITION
DELETE http://apiserver/accessors/:id/dashboardviews/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accessors/1234/dashboardviews/20300", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a accessor dashboard view. It cannot be undone.

##### Arguments

* id (required) - The id of the accessor dashboard view to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the accessor dashboard view does not exist, this call returns an error.

#### List all accessor dashboard views

```
DEFINITION
GET http://apiserver/accessor/:id/dashboardviews

EXAMPLE REQUEST
$.get("http://localhost:49195/accessor/1234/dashboardviews?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20030",
            "accessor": "1234",
            "accessorName": "John Doe",
            "view": "10015",
            "viewDescription": "Accounts Assigned to Me",
            "isChart": false,
            "displaySequence": 10,
            "gridPageSize": 5
        },
        {...},
    ]
}

```

Returns a list of all accessor dashboard views.

##### Arguments

* id (required) - The unique id of the accessor to list the dashboard views for.

##### Returns

A dictionary with an items property that contains an array of up to limit accessor dashboard views, starting at index offset. Each entry in the array is a separate accessor dashboard view object. If no more accessor dashboard views are available, the resulting array will be empty. This request should never return an error.

### Accessor Dashboard View Details

#### List all accessor dashboard view details

```
DEFINITION
GET http://apiserver/accessors/:id/dashboardviews/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/dashboardviews/20300/details?");

EXAMPLE RESPONSE
{
    "metadata": [
        {
            "tableId": "A01",
            "entityId": "133",
            "entityDescription": "Account Master",
            "entityIdField": "Id",
            "module": "AT",
            "field": "Id",
            "title": "AccountNumber",
            "fieldType": "ACCOUNT",
            "sequence": "0",
            "width": "10em",
            "attributeType": null
        }
        {...},
    ],
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "uniqueId": "1",
            "Id": "16234",
            "FamilyId": "28339",
            "AccountType": "I",
            "AccountTypeDescription": "Individual",
            "FamilyMemberType": "SP",
            "FamilyMemberTypeDescription": "Spouse",
            "Title": "Mrs.",
            "FirstName": "Jane",
            "LastName": "Smith",
            "FormattedName": "Mrs. Jane Smith",
            "Status": "A",
            "StatusDescription": "Active",
            "A07EmailAddress": "",
            "A04Phone": "(555) 555-5555",
            "A02Active": true,
            "A02UseAsPrimary": true,
            "A03AddressLine1": "12345 North Lights Way",
            "A03AddressLine2": "Apt. 1111",
            "A03City": "Dallas",
            "A03State": "TX",
            "A03StateDescription": "Texas",
            "A03Country": "USA",
            "A03CountryDescription": "United States of America",
            "A03ZipPostal": "76706",
            "A02AddressId": "1000028388"
        },
        {...},
    ]
}

```

Returns a list of all accessor dashboard view details.

##### Arguments

* id (required) - The unique id of the accessor to list the dashboard views for.
* dashboardViewId (required) - The unique id of the accessor's dashboard to list the details for.

##### Returns

A dictionary with an items property that contains an array of up to limit accessor dashboard view details, starting at index offset. Each entry in the array is a separate accessor dashboard view detail object. If no more accessor dashboard view details are available, the resulting array will be empty. This request should never return an error.

### Accessor Notifications

#### Forward an accessor notification

```
DEFINITION
POST http://apiserver/accessors/:id/notifications/:id/forward

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/notifications/1/forward", {
    "recipient": "4321",
    "recipientType": "ACCESSOR"
});

EXAMPLE RESPONSE
204 No Content

```

Creates a copy of the notification and sends it to the specified recipient.

##### Arguments

* recipient (required) - The recipient id of the entity receiving the notification. Must be a valid id for the given recipientType.
* recipientType (required) - a valid recipient type

##### Returns

Returns a 204 No Content response on success. If the notification does not exist, this call returns an error.

#### Retrieve an accessor notification

```
DEFINITION
GET http://apiserver/accessors/:id/notifications/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/notifications/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "DNRASSIGN",
    "typeDescription": "Donor Assignment",
    "deliveryMethod": "SYSTEM",
    "recipient": "1234",
    "recipientType": "ACCESSOR",
    "workflow": "90",
    "workflowDescription": "DELETE AT01S - AT01V01 MONITORED",
    "date": "2015-06-19",
    "status": "U",
    "fromEmailAddress": "test@test.edu",
    "subject": "New Account",
    "body": "A new account has been assigned to you."
}

```

Retrieves the details of an existing accessor notification. You need only supply the notification id.

##### Arguments

* id (required) - The id of the accessor notification to be retrieved.

#### Update an accessor notification

```
DEFINITION
POST http://apiserver/accessors/:id/notifications/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/notifications/1", {
    "status": "R"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "DNRASSIGN",
    "typeDescription": "Donor Assignment",
    "deliveryMethod": "SYSTEM",
    "recipient": "1234",
    "recipientType": "ACCESSOR",
    "workflow": "90",
    "workflowDescription": "DELETE AT01S - AT01V01 MONITORED",
    "date": "2015-06-19",
    "status": "R",
    "fromEmailAddress": "test2@test.edu",
    "subject": "New Account",
    "body": "A new account has been assigned to you."
}

```

Only updates the status of the specified accessor notification by setting the value of the status parameter passed. All other parameters will be left unchanged.

##### Arguments

* status (required) - The status to set on the accessor notification. If not provided, the existing status will be used.

##### Returns

Returns the accessor notification object if the update succeeded. Returns an error if update parameters are invalid.

#### List all accessor notifications

```
DEFINITION
GET http://apiserver/accessors/:id/notifications

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/notifications");

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
            "type": "DNRASSIGN",
            "typeDescription": "Donor Assignment",
            "deliveryMethod": "SYSTEM",
            "recipient": "1234",
            "recipientType": "ACCESSOR",
            "workflow": "90",
            "workflowDescription": "DELETE AT01S - AT01V01 MONITORED",
            "date": "2015-06-19",
            "status": "U",
            "fromEmailAddress": "test@test.edu",
            "subject": "New Account",
            "body": "A new account has been assigned to you."
        },
        ...
    ]
}

```

Returns a list of all notifications for the accessor, matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* type () - The notification type
* deliveryMethod () - The notification delivery method
* recipient () - must be the same as the accessorId in the route
* recipientType () - The notification recipient type
* workflow () - The workflow unique id which caused the notification to be created
* date () - The date when the notification was sent
* status () - The status of the notification
* subject () - The subject of the notification
* body () - The body of the notification

##### Returns

A dictionary with an items property that contains an array of up to limit accessor notification entries, starting at index offset. Each entry in the array is a separate accessor notification entry object. If no more accessor notification entries are available, the resulting array will be empty. This request will return a 404 if accessorId/recipient is not found.

### Accessor Notification Settings

#### Create an accessor notification setting

```
DEFINITION
POST http://apiserver/accessors/:id/notificationsettings

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/notificationsettings", {
    "notificationType": "OTHER",
    "deliveryMethod": "TEXT",
    "isSuppressed": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "recipient": "1234",
    "recipientType": "ACCESSOR",
    "notificationType": "OTHER",
    "notificationTypeDescription": "Other Notification Type",
    "deliveryMethod": "TEXT",
    "isSuppressed": false
}

```

Creates a new accesssor notification setting.

##### Arguments

* id (required) - The unique id of the accessor to create the notification setting for.

##### Returns

Returns an accessor notification setting object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve an accessor notification setting

```
DEFINITION
GET http://apiserver/accessors/:id/notificationsettings/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/notificationsettings/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "recipient": "1234",
    "recipientType": "ACCESSOR",
    "notificationType": "OTHER",
    "notificationTypeDescription": "Other Notification Type",
    "deliveryMethod": "SYSTEM",
    "isSuppressed": false
}

```

Retrieves the details of an accessor notification setting.

##### Arguments

* id (required) - The id of the accessor notification setting

#### Update an accessor notification setting

```
DEFINITION
POST http://apiserver/accessors/:id/notificationsettings/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/notificationsettings/3", {
    "deliveryMethod": null,
    "isSuppressed": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "recipient": "1234",
    "recipientType": "ACCESSOR",
    "notificationType": "OTHER",
    "notificationTypeDescription": "Other Notification Type",
    "deliveryMethod": null,
    "isSuppressed": true
}

```

Updates an accessor's notification settting.

##### Arguments

* notificationType () - The notification type which this setting applies
* deliveryMethod () - The accessor's desired deliveryMethod for the notification type
* isSuppressed () - Is this notificaiton type suppressed (accessor will not get notifications of this type). If true, deliveryMethod must be null.

##### Returns

Returns an accessor notification setting object if the update succeeded. Returns an error if update parameters are invalid.

#### List all accessor notification settings

```
DEFINITION
GET http://apiserver/accessors/:id/notificationsettings

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/notificationsettings");

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
            "recipient": "1234",
            "recipientType": "ACCESSOR",
            "notificationType": "OTHER",
            "notificationTypeDescription": "Other Notification Type",
            "deliveryMethod": "SYSTEM",
            "isSuppressed": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all accessor notification settings matching the provided filter criteria.

##### Arguments

* notificationType () - Filter list by exact match in notificationType.
* deliveryMethod () - Filter list by exactMatch in deliveryMethod
* isSuppressed () - Filter list by whether the notification type is suppressed

##### Returns

A dictionary with an items property that contains an array of up to limit accessor notification setting objects, starting at index offset. Each entry in the array is a separate accessor notification setting object. If no more accessor notification settings are available, the resulting array will be empty. This request should never return an error.

### Accessor Pledges

#### Create an accessor pledge

```
DEFINITION
POST http://apiserver/accessors/:accessorId/pledges

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6631/pledges", {
    "pledgeCode": "100002"
});

EXAMPLE RESPONSE
{
    "id": "20015",
    "pledgeCode": "100002",
    "pledgeDescription": "Harriet Acen"
}

```

Creates a new accessor pledge.

##### Arguments

* pledgeCode (required) - The pledge code to associate with the specified accessor.

##### Returns

Returns an accessor pledge object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accessor pledge

```
DEFINITION
GET http://apiserver/accessors/:accessorId/pledges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/6631/pledges/20015");

EXAMPLE RESPONSE
{
    "id": "20015",
    "pledgeCode": "100002",
    "pledgeDescription": "Harriet Acen"
}

```

Retrieves the details of an existing accessor pledge. You need only supply the id.

##### Arguments

* id (required) - The id of the accessor pledge to be retrieved.

#### Update an accessor pledge

```
DEFINITION
POST http://apiserver/accessors/:accessorId/pledges/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6631/pledges/20015", {
    "pledgeCode": "100003"
});

EXAMPLE RESPONSE
{
    "id": "20015",
    "pledgeCode": "100003",
    "pledgeDescription": "Martha Kyomya"
}


```

Updates the specified accessor pledge by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* pledgeCode (optional) - The pledge code to update the accessor pledge association with.

##### Returns

Returns the accessor pledge object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an accessor pledge

```
DEFINITION
DELETE http://apiserver/accessors/:accessorId/pledges/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accessors/6631/pledges/20015", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an accessor pledge. It cannot be undone.

##### Arguments

* id (required) - The id of the accessor pledge to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the accessor pledge does not exist, this call returns an error.

#### List all accessor pledges

```
DEFINITION
GET http://apiserver/accessors/:accessorId/pledges

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/6631/pledges");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20015",
            "pledgeCode": "100003",
            "pledgeDescription": "Martha Kyomya"
        },
        {...},
    ]
}

```

Returns a list of all accessor pledges.

##### Returns

A dictionary with an items property that contains an array of up to limit accessor pledges, starting at index offset. Each entry in the array is a separate accessor pledge object. If no more accessor pledges are available, the resulting array will be empty. This request should never return an error.

### Accessor Projects

#### Create an accessor project

```
DEFINITION
POST http://apiserver/accessors/:accessorId/projects

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6631/projects", {
    "projectCode": "110"
});

EXAMPLE RESPONSE
{
    "id": "19",
    "projectCode": "110",
    "projectDescription": "General Project Match"
}

```

Creates a new accessor project.

##### Arguments

* projectCode (required) - The project code to associate with the specified accessor.

##### Returns

Returns an accessor project object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accessor project

```
DEFINITION
GET http://apiserver/accessors/:accessorId/projects/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/6631/projects/19");

EXAMPLE RESPONSE
{
    "id": "19",
    "projectCode": "110",
    "projectDescription": "General Project Match"
}

```

Retrieves the details of an existing accessor project. You need only supply the id.

##### Arguments

* id (required) - The id of the accessor project to be retrieved.

#### Update an accessor project

```
DEFINITION
POST http://apiserver/accessors/:accessorId/projects/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6631/projects/19", {
    "projectCode": "101010"
});

EXAMPLE RESPONSE
{
    "id": "19",
    "projectCode": "101010",
    "projectDescription": "Billy Key"
}

```

Updates the specified accessor project by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* projectCode (optional) - The project code to update the accessor association with.

##### Returns

Returns the accessor project object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an accessor project

```
DEFINITION
DELETE http://apiserver/accessors/:accessorId/projects/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accessors/6631/projects/19", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an accessor project. It cannot be undone.

##### Arguments

* id (required) - The id of the accessor project to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the accessor project does not exist, this call returns an error.

#### List all accessor projects

```
DEFINITION
GET http://apiserver/accessors/:accessorId/projects

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/6631/projects");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "19",
            "projectCode": "101010",
            "projectDescription": "Billy Key"
        },
        {...},
    ]
}

```

Returns a list of all accessor projects.

##### Returns

A dictionary with an items property that contains an array of up to limit accessor projects, starting at index offset. Each entry in the array is a separate accessor project object. If no more accessor projects are available, the resulting array will be empty. This request should never return an error.

### Accessor User Settings

#### Retrieve accessor user settings

```
DEFINITION
GET http://apiserver/accessors/:id/usersettings

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/usersettings");

EXAMPLE RESPONSE
{
    "accessor": "1234",
    "username": "yourcompany\\jdoe",
    "telephoneExtension": "463",
    "description": "John Doe",
    "emailAddress": "john.doe@yourcompany.com",
    "phone": {
        "areaCode": "555",
        "phoneNumber": "123-4567",
        "carrier": "ATT"
    },
    "signatureBlock": "John Doe"
}

```

Retrieves the details the accessor's user settings.

##### Arguments

* id (required) - The id of the accessor for retrieving user settings

#### Update accessor user settings

```
DEFINITION
POST http://apiserver/accessors/:id/usersettings

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/usersettings", {
    "telephoneExtension": "463",
    "emailAddress": "john.doe@yourcompany.com",
    "phone": {
        "areaCode": "555",
        "phoneNumber": "123-4567",
        "carrier": "VERIZON"
    }
});

EXAMPLE RESPONSE
{
    "accessor": "1234",
    "username": "yourcompany\\jdoe",
    "telephoneExtension": "463",
    "description": "John Doe",
    "emailAddress": "john.doe@yourcompany.com",
    "phone": {
        "areaCode": "555",
        "phoneNumber": "123-4567",
        "carrier": "VERIZON"
    },
    "signatureBlock": "John Doe"
}

```

Updates user setttings like internal phone extension, email address, and mobile phone for receiving text notifications. Does not allow updating of user information like accessor, username, etc.

##### Arguments

* telephoneExtension () - The user's internal phone extension for call pop.
* emailAddress () - The user's email address for receiving email notifications
* phone () - area code, phone number, and mobile carrier code for receiving text notifications
* signatureBlock () - The user's email signature block for sending emails from StudioEnterprise Web

##### Returns

Returns the accessor user settings object if the update succeeded. Returns an error if update parameters are invalid.

### Account Access Audit

#### List all account access audit information

```
DEFINITION
GET http://apiserver/accountaccessaudit

EXAMPLE REQUEST
$.get("http://localhost:49195/accountaccessaudit?account=9318");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "account": "9318",
            "accessor": "11631",
            "accessorSource": "I",
            "session": 859491,
            "dateTime": "2016-10-31T11:34:37 AM",
            "source": "bperkins"
        },
        ...
    ]
}

```

Returns a list of all account access audit information matching the provided filter criteria.

##### Arguments

* account - The account number to audit
* accessor - The accessor of the user that accessed the account

##### Returns

A dictionary with an items property that contains an array of up to limit account access audit information entries, starting at index offset. Each entry in the array is a separate account access audit information entry object. If no more audit information entries are available, the resulting array will be empty.

### Actions

#### Create an action

```
DEFINITION
POST http://apiserver/actions

EXAMPLE REQUEST
$.post("http://localhost:49195/actions", {
    "name": "Create a Prayer Request",
    "buttonLabel": "Prayer Request",
    "isSelectedEntityRequired": false,
    "category": "ACCOUNT",
    "sawId": "S0000001",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "5",
    "name": "Create a Prayer Request",
    "buttonLabel": "Prayer Request",
    "isSelectedEntityRequired": false,
    "category": "ACCOUNT",
    "sawId": "S0000001",
    "sawIdDescription": "Generic SAW",
    "isActive": true
}

```

Creates a new action.

##### Arguments

* name (required) - name of action
* buttonLabel (required) - text for the button label
* category (optional) - category of the action
* isSelectedEntityRequired (defaults to `false`)- Determines whether a selected entity record is required to invoke the action
* sawId (required) - SAW Id
* isActive (defaults to `false`) - Determines whether the action is acive

##### Returns

Returns an action object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an action

```
DEFINITION
GET http://apiserver/actions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/actions/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "name": "Create a Prayer Request",
    "buttonLabel": "Prayer Request",
    "isSelectedEntityRequired": false,
    "category": "ACCOUNT",
    "sawId": "S0000001",
    "sawIdDescription": "Generic SAW",
    "isActive": true
}

```

Retrieves the details of an existing action. You need only supply the id.

##### Arguments

* id (required) - The id of the action to be retrieved.

#### Update an action

```
DEFINITION
POST http://apiserver/actions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/actions/5", {{
    "isSelectedEntityRequired": true,
});

EXAMPLE RESPONSE
{
    "id": "5",
    "name": "Create a Prayer Request",
    "buttonLabel": "Prayer Request",
    "isSelectedEntityRequired": true,
    "category": "ACCOUNT",
    "sawId": "S0000001",
    "sawIdDescription": "Generic SAW",
    "isActive": true
}


```

Updates the specified action by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name - name of action
* buttonLabel - text for the button label
* category - category of the action
* isSelectedEntityRequired - Determines whether a selected entity record is required to invoke the action
* sawId - SAW Id
* isActive - Determines whether the action is acive

##### Returns

Returns the action object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an action

```
DEFINITION
DELETE http://apiserver/actions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/actions/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a action. It cannot be undone.

##### Arguments

* id (required) - The id of the action to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the action does not exist, this call returns an error.

#### List all actions

```
DEFINITION
GET http://apiserver/actions

EXAMPLE REQUEST
$.get("http://localhost:49195/actions?");

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
            "name": "Create a Prayer Request",
            "buttonLabel": "Prayer Request",
            "isSelectedEntityRequired": true,
            "category": "ACCOUNT",
            "sawId": "S0000001",
            "sawIdDescription": "Generic SAW",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all actions.

##### Arguments

* name - name of action
* buttonLabel - text for the button label
* category - category of the action
* isActive - Determines whether the action is acive

##### Returns

A dictionary with an items property that contains an array of up to limit actions, starting at index offset. Each entry in the array is a separate action object. If no more actions are available, the resulting array will be empty. This request should never return an error.

### Action Locations

#### Create an action location

```
DEFINITION
POST http://apiserver/action/:id/locations

EXAMPLE REQUEST
$.post("http://localhost:49195/action/6/locations", {
    "interfaceId": "accountCommunications",
    "key": "accountCommunications",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "10011",
    "action": "6",
    "actionName": "Prayer Request",
    "interfaceId": "accountCommunications",
    "key": "accountCommunications",
    "activityTitleShort": "Communications",
    "activityTitleLong": "Account Communications",
    "componentTitleShort": "Account Processing",
    "isActive": true
}

```

Creates a new action location.

##### Arguments

* interfaceId (required) - The interfaceId of the activity in which the action should be located
* key (required) - The location key which is provided throughout the action process to the custom logic which may be used by the custom logic to determine the source of the action.
* isActive (required) - Specifies if action location is active

##### Returns

Returns an action location object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an action location

```
DEFINITION
GET http://apiserver/actions/:id/locations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/actions/6/locations/10011");

EXAMPLE RESPONSE
{
    "id": "10011",
    "action": "6",
    "actionName": "Prayer Request",
    "interfaceId": "accountCommunications",
    "key": "accountCommunications",
    "activityTitleShort": "Communications",
    "activityTitleLong": "Account Communications",
    "componentTitleShort": "Account Processing",
    "isActive": true
}

```

Retrieves the details of an existing action location. You need only supply the id.

##### Arguments

* id (required) - The id of the action location to be retrieved.

#### Update an action location

```
DEFINITION
POST http://apiserver/actions/:id/locations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/actions/6/locations/10011", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "10011",
    "action": "6",
    "actionName": "Prayer Request",
    "interfaceId": "accountCommunications",
    "key": "accountCommunications",
    "activityTitleShort": "Communications",
    "activityTitleLong": "Account Communications",
    "componentTitleShort": "Account Processing",
    "isActive": false
}


```

Updates the specified action location by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* interfaceId - The interfaceId of the activity in which the action should be located
* key - The location key which is provided throughout the action process to the custom logic which may be used by the custom logic to determine the source of the action.
* isActive - Specifies if action location is active

##### Returns

Returns the action location object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an action location

```
DEFINITION
DELETE http://apiserver/actions/:id/locations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/actions/6/locations/10011", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a action location. It cannot be undone.

##### Arguments

* id (required) - The id of the action location to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the action location does not exist, this call returns an error.

#### List all action locations

```
DEFINITION
GET http://apiserver/actions/:id/locations

EXAMPLE REQUEST
$.get("http://localhost:49195/actions/6/locations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10011",
            "action": "6",
            "actionName": "Prayer Request",
            "interfaceId": "accountCommunications",
            "key": "accountCommunications",
            "activityTitleShort": "Communications",
            "activityTitleLong": "Account Communications",
            "componentTitleShort": "Account Processing",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all action locations.

##### Arguments

* interfaceId - The interfaceId of the activity in which the action should be located
* key - The location key which is provided throughout the action process to the custom logic which may be used by the custom logic to determine the source of the action.
* isActive - Specifies if action location is active

##### Returns

A dictionary with an items property that contains an array of up to limit action locations, starting at index offset. Each entry in the array is a separate action location object. If no more action locations are available, the resulting array will be empty. This request should never return an error.

### Action Steps

#### Create an action step

```
DEFINITION
POST http://apiserver/actions/:id/steps

EXAMPLE REQUEST
$.post("http://localhost:49195/actions/6/steps", {
    "name": "Prompt",
    "type": "FORM",
    "isCancelEnabled": true,
    "isBackEnabled": true,
    "sequence": 1,
    "onLoad": null,
    "onSubmit": "ActionStepFormSubmit",
    "actionDetails": {  }
});

EXAMPLE RESPONSE
{
    "id": "20021",
    "type": "FORM",
    "action": "1",
    "actionName": "Prayer Request",
    "name": "Prompt",
    "sequence": 1,
    "isCancelEnabled": true,
    "isBackEnabled": true,
    "onLoad": null,
    "onSubmit": "ActionStepFormSubmit",
    "actionDetails": {  }
}

```

Creates a new action step.

##### Arguments

* name (required) - name of the step
* type (required) - type of the step.
* isCancelEnabled (required) - specifies whether the Cancel button on the step should be visible
* isBackEnabled (required) - specifies whether the Back button on the step should be visible
* onLoad - the stored procedure name to execute prior to the step
* onSubmit - the stored procedure name to execute after the step
* actionDetails (required) - the properties within the `actionDetails` will vary based on the action step `type`
* sequence (required) - sequence of the step

##### Returns

Returns an action step object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an action step

```
DEFINITION
GET http://apiserver/actions/:id/steps/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/actions/6/steps/20021");

EXAMPLE RESPONSE
{
    "id": "20021",
    "type": "FORM",
    "action": "1",
    "actionName": "Prayer Request",
    "name": "Prompt",
    "sequence": 1,
    "isCancelEnabled": true,
    "isBackEnabled": true,
    "onLoad": null,
    "onSubmit": "ActionStepFormSubmit",
    "actionDetails": {  }
}

```

Retrieves the details of an existing action step. You need only supply the id.

##### Arguments

* id (required) - The id of the action step to be retrieved.

#### Update an action step

```
DEFINITION
POST http://apiserver/actions/:id/steps/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/actions/6/steps/20021", {
    "onLoad": "ActionStepFormLoad"
});

EXAMPLE RESPONSE
{
    "id": "20021",
    "type": "FORM",
    "action": "1",
    "actionName": "Prayer Request",
    "name": "Prompt",
    "sequence": 1,
    "isCancelEnabled": true,
    "isBackEnabled": true,
    "onLoad": "ActionStepFormLoad",
    "onSubmit": "ActionStepFormSubmit",
    "actionDetails": {  }
}


```

Updates the specified action step by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name - name of the step
* type - type of the step.
* isCancelEnabled - specifies whether the Cancel button on the step should be visible
* isBackEnabled - specifies whether the Back button on the step should be visible
* onLoad - the stored procedure name to execute prior to the step
* onSubmit - the stored procedure name to execute after the step
* actionDetails - the properties within the `actionDetails` will vary based on the action step `type`
* sequence - sequence of the step

##### Returns

Returns the action step object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an action step

```
DEFINITION
DELETE http://apiserver/actions/:id/step/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/actions/:id/step/20021", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a action step. It cannot be undone.

##### Arguments

* id (required) - The id of the action step to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the action step does not exist, this call returns an error.

#### List all action steps

```
DEFINITION
GET http://apiserver/actions/:id/steps

EXAMPLE REQUEST
$.get("http://localhost:49195/actions/6/steps");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20021",
            "type": "FORM",
            "action": "1",
            "actionName": "Prayer Request",
            "name": "Prompt",
            "sequence": 1,
            "isCancelEnabled": true,
            "isBackEnabled": true,
            "onLoad": "ActionStepFormLoad",
            "onSubmit": "ActionStepFormSubmit",
            "actionDetails": {  }
        },
        {...},
    ]
}

```

Returns a list of all action steps.

##### Returns

A dictionary with an items property that contains an array of up to limit action steps, starting at index offset. Each entry in the array is a separate action step object. If no more action steps are available, the resulting array will be empty. This request should never return an error.

### Action Step Fields

#### Create an action step field

```
DEFINITION
POST http://apiserver/actions/:id/steps/:id/fields

EXAMPLE REQUEST
$.post("http://localhost:49195/actions/5/steps/20/fields", {
    "name": "postalCode",
    "fieldType": "TEXT",
    "dataType": null,
    "actionLinkId": null,
    "prompt": "Postal Code",
    "isRequired": false,
    "sequence": 5
});

EXAMPLE RESPONSE
{
    "id": "300",
    "actionStep": "20",
    "name": "postalCode",
    "fieldType": "TEXT",
    "dataType": null,
    "dataTypeDescription": null,
    "actionLinkId": null,
    "actionLinkDescription": null,
    "prompt": "Postal Code",
    "isRequired": false,
    "sequence": 5
}

```

Creates a new action step field.

##### Arguments

* name (required) - field name
* fieldType (required) - must be a valid field type defined as a `DDCACFLTYP` code value
* dataType (required when `fieldType="CODE"`) - specifies the data type for a code field.
* actionLinkId (required when `fieldType="LINK"`) - specifies the Activity InterfaceId to link to for a link field.
* prompt (required) - The label for the field
* tip (optional) - tool tip for the field; currently not used by SE Web
* isRequired (required) - Specifies if the field should be a required field
* sequence (required) - Specifies the sequence to present the field when rendered on a form.

##### Returns

Returns an action step field object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an action step field

```
DEFINITION
GET http://apiserver/actions/:id/steps/:id/fields/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/actions/5/steps/20/fields/300");

EXAMPLE RESPONSE
{
    "id": "300",
    "actionStep": "20",
    "name": "postalCode",
    "fieldType": "TEXT",
    "dataType": null,
    "dataTypeDescription": null,
    "actionLinkId": null,
    "actionLinkDescription": null,
    "prompt": "Postal Code",
    "isRequired": false,
    "sequence": 5
}

```

Retrieves the details of an existing action step field. You need only supply the id.

##### Arguments

* id (required) - The id of the action step field to be retrieved.

#### Update an action step field

```
DEFINITION
POST http://apiserver/actions/:id/steps/:id/fields/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/actions/5/steps/20/fields/300", {
    "isRequired": true
});

EXAMPLE RESPONSE
{
    "id": "300",
    "actionStep": "20",
    "name": "postalCode",
    "fieldType": "TEXT",
    "dataType": null,
    "dataTypeDescription": null,
    "actionLinkId": null,
    "actionLinkDescription": null,
    "prompt": "Postal Code",
    "isRequired": true,
    "sequence": 5
}


```

Updates the specified action step field by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name - field name
* fieldType - must be a valid field type defined as a `DDCACFLTYP` code value
* dataType (required when `fieldType="CODE"`) - specifies the data type for a code field.
* actionLinkId (required when `fieldType="LINK"`) - specifies the Activity InterfaceId to link to for a link field.
* prompt - The label for the field
* tip - tool tip for the field; currently not used by SE Web
* isRequired - Specifies if the field should be a required field
* sequence - Specifies the sequence to present the field when rendered on a form.

##### Returns

Returns the action step field object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an action step field

```
DEFINITION
DELETE http://apiserver/actions/:id/steps/:id/fields/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/actions/5/steps/20/fields/300", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a action step field. It cannot be undone.

##### Arguments

* id (required) - The id of the action step field to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the action step field does not exist, this call returns an error.

#### List all action step fields

```
DEFINITION
GET http://apiserver/actions/:id/step/:id/fields

EXAMPLE REQUEST
$.get("http://localhost:49195/actions/5/step/20/fields");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "300",
            "actionStep": "20",
            "name": "postalCode",
            "fieldType": "TEXT",
            "dataType": null,
            "dataTypeDescription": null,
            "actionLinkId": null,
            "actionLinkDescription": null,
            "prompt": "Postal Code",
            "isRequired": true,
            "sequence": 5
        },
        {...},
    ]
}

```

Returns a list of all action step fields.

##### Returns

A dictionary with an items property that contains an array of up to limit action step fields, starting at index offset. Each entry in the array is a separate action step field object. If no more action step fields are available, the resulting array will be empty. This request should never return an error.

### Api Extension Endpoints

#### Create an api extension endpoint

```
DEFINITION
POST http://apiserver/apiextensionendpoints

EXAMPLE REQUEST
$.post("http://localhost:49195/apiextensionendpoints", {
    "name": "NAME",
    "description": "DESCRIPTION",
    "storedProcedureName": "STOREDPROCEDURENAME",
    "urlSlug": "URLSLUG",
    "sawId": "SAWID",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "123",
    "name": "NAME",
    "description": "DESCRIPTION",
    "storedProcedureName": "STOREDPROCEDURENAME",
    "urlSlug": "URLSLUG",
    "sawId": "SAWID",
    "isActive": true
}

```

Creates a new api extension endpoint.

##### Arguments

* name (optional) - name of the endpoint | MaxLength(100)
* description (optional) - description of the endpoint | MaxLength(900)
* storedProcedureName (required) - name of the stored procedure that will be called in SQL | MaxLength(128)
* urlSlug (required) - url slug called to access the endpoint | MaxLength(100), Alpha characters and dashes only
* sawId (optional) - SAWId required to access the api endpoint
* isActive (required) - specifies if the endpoint is active

##### Returns

Returns an api extension endpoint object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an api extension endpoint

```
DEFINITION
GET http://apiserver/apiextensionendpoints/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/apiextensionendpoints/123");

EXAMPLE RESPONSE
{
    "id": "123",
    "name": "NAME",
    "description": "DESCRIPTION",
    "storedProcedureName": "STOREDPROCEDURENAME",
    "urlSlug": "URLSLUG",
    "sawId": "SAWID",
    "isActive": true
}

```

Retrieves the details of an existing api extension endpoint. You need only supply the id.

##### Arguments

* id (required) - The id of the api extension endpoint to be retrieved.

#### Update an api extension endpoint

```
DEFINITION
POST http://apiserver/apiextensionendpoints/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/apiextensionendpoints/123", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "123",
    "name": "NAME",
    "description": "DESCRIPTION",
    "storedProcedureName": "STOREDPROCEDURENAME",
    "urlSlug": "URLSLUG",
    "sawId": "SAWID",
    "isActive": false
}


```

Updates the specified api extension endpoint by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name - name of the endpoint | MaxLength(100)
* description - description of the endpoint | MaxLength(900)
* storedProcedureName - name of the stored procedure that will be called in SQL | MaxLength(128)
* urlSlug - url slug called to access the endpoint | MaxLength(100), Alpha characters and dashes only
* sawId - SAWId required to access the api endpoint
* isActive - specifies if the endpoint is active

##### Returns

Returns the api extension endpoint object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an api extension endpoint

```
DEFINITION
DELETE http://apiserver/apiextensionendpoints/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/apiextensionendpoints/123", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an api extension endpoint. It cannot be undone.

##### Arguments

* id (required) - The id of the api extension endpoint to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the api extension endpoint does not exist, this call returns an error.

#### List all api extension endpoints

```
DEFINITION
GET http://apiserver/apiextensionendpoints

EXAMPLE REQUEST
$.get("http://localhost:49195/apiextensionendpoints");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "123",
            "name": "NAME",
            "description": "DESCRIPTION",
            "storedProcedureName": "STOREDPROCEDURENAME",
            "urlSlug": "URLSLUG",
            "sawId": "SAWID",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all api extension endpoints.

##### Returns

A dictionary with an items property that contains an array of up to limit api extension endpoints, starting at index offset. Each entry in the array is a separate api extension endpoint object. If no more api extension endpoints are available, the resulting array will be empty. This request should never return an error.

#### Execute an api extension endpoint

```
DEFINITION
GET http://apiserver/extensions/:urlSlug

EXAMPLE REQUEST
$.get("http://localhost:49195/extensions/paymentsbyaccount?accountNumber=3040&offset=10&limit=10");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        See Description
    ]
}

```

Returns whatever data is returned by the stored procedure which is linked to the specified urlSlug

##### Arguments

* urlSlug (required) - The urlSlug that is part of the same Api Extension Endpoint record as the desired stored procedure

##### Query Parameters

* Which query parameters are accepted is determined by the stored procedure that is called. Any passed in parameters that are not used will be ignored.

##### Description

This endpoint is different from all other endpoints in that it can be customized by a user. This endpoint is linked to a stored procedure in the Api Extension Endpoints resource. This endpoint will return whatever the linked stored procedure returns.

### Audit Information

#### List all audit information

```
DEFINITION
GET http://apiserver/auditinfo

EXAMPLE REQUEST
$.get("http://localhost:49195/auditinfo?interfaceId=AccountCodes&id=1761507");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "action": "INSERT",
            "dateTime": "2014-03-06T14:18:22",
            "username": "bperkins"
        },
        ...
    ]
}

```

Returns a list of all audit information matching the provided filter criteria.

##### Arguments

* interfaceId (required) - The interfaceId of the entity to audit
* id (required) - The id of the entity to audit

##### Returns

A dictionary with an items property that contains an array of up to limit audit information entries, starting at index offset. Each entry in the array is a separate audit information entry object. If no more audit information entries are available, the resulting array will be empty. This request will return a 404 if either the specified interfaceId or id are not found.

### Calendar Sync

#### Create a calendar sync

```
DEFINITION
POST http://apiserver/accessors/:accessorid/calendars

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/calendars", {
    "folderName": "Calendar"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "accessor": "1234",
    "user": "ddc\\jdoe",
    "emailAddress": "johndoe@donordirect.com",
    "folderName": "Calendar",
    "lastSyncVersion": "1111",
    "lastSyncDate": "2016-01-01"
}

```

Creates a new calendar sync for tracking.

##### Arguments

* accessorid (required) - The unique id of the accessor to create the calendar sync for.
* folderName (required) - The name of the calendar.

##### Returns

Returns a calendar sync object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve a calendar sync

```
DEFINITION
GET http://apiserver/accessors/:accessorid/calendars/:calendarid

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/calendars/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "accessor": "1234",
    "user": "ddc\\jdoe",
    "emailAddress": "johndoe@donordirect.com",
    "folderName": "Calendar",
    "lastSyncVersion": "1111",
    "lastSyncDate": "2016-01-01"
}

```

Retrieves the details of a calendar sync.

##### Arguments

* accessorid (required) - The unique id of the accessor that owns the calendar.
* calendarid (required) - The id of the calendar sync

#### Update a calendar sync

```
DEFINITION
POST http://apiserver/accessors/:accessorid/calendars/:calendarid

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/calendars/8", {
    "folderName": "Calendar"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "accessor": "1234",
    "user": "ddc\\jdoe",
    "emailAddress": "johndoe@donordirect.com",
    "folderName": "Calendar",
    "lastSyncVersion": "1111",
    "lastSyncDate": "2016-01-01"
}

```

Updates a calendar sync.

##### Arguments

* accessorid (required) - The unique id of the accessor that owns the calendar.
* calendarid (required) - The id of the calendar sync
* folderName - The name of the calendar.

##### Returns

Returns a calendar sync object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a calendar sync

```
DEFINITION
DELETE http://apiserver/accessors/:accessorid/calendars/:calendarid

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/calendars/8");

EXAMPLE RESPONSE
204 No Content

```

Deletes a calendar sync.

##### Arguments

* accessorid (required) - The unique id of the accessor that owns the calendar.
* calendarid (required) - The id of the calendar sync

##### Returns

Returns a 204 No Content response on success. If the calendar does not exist, this call returns an error.

#### List all calendar syncs

```
DEFINITION
GET http://apiserver/accessors/:accessorid/calendars

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/calendars"), {
    "user": "ddc\\jdoe",
    "isExactMatch": true
});

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
            "accessor": "1234",
            "user": "ddc\\jdoe",
            "emailAddress": "johndoe@donordirect.com",
            "folderName": "Calendar",
            "lastSyncVersion": "1111",
            "lastSyncDate": "2016-01-01"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all calendar sync matching the provided filter criteria.

##### Arguments

* accessorid (required) - Filter list by match on accessor
* user - Filter list by partial match on user
* emailAddress - Filter list by match on email address
* folderName - Filter list by match on folder name
* isExactMatch - Determines if the fields should be an exact match or fuzzy match

##### Returns

A dictionary with an items property that contains an array of up to limit calendar sync objects, starting at index offset. Each entry in the array is a separate calendar sync object. If no more calendar sync are available, the resulting array will be empty. This request should never return an error.

### Call Pop

#### Retrieve a call pop

```
DEFINITION
GET http://apiserver/callpop

EXAMPLE REQUEST
$.get("http://localhost:49195/callpop");

EXAMPLE RESPONSE
{
    "telephoneExtension": "2222",
    "broadcastAreaCode": null,
    "broadcastTelephoneNumber": null,
    "accountAreaCode": "972",
    "accountTelephoneNumber": "867-5309",
    "source": "072711"
}

```

##### Arguments

* telephoneExtension (optional) - The telephone extension for which to receive the call pop. If not provided, the telephone extension for the current user will be used.

### Call Pop Configuration

#### Retrieve a call pop configuration

```
DEFINITION
GET http://apiserver/callpop/config

EXAMPLE REQUEST
$.get("http://localhost:49195/callpop/config");

EXAMPLE RESPONSE
{
    "username": "corp\\ssmith",
    "telephoneExtension": "23"
}

```

##### Returns

Returns a call pop configuration object. If none exists, then a default configuration object is returned.

#### Update a call pop configuration

```
DEFINITION
POST http://apiserver/callpop/config

EXAMPLE REQUEST
$.post("http://localhost:49195/callpop/config", {
    "telephoneExtension": "107"
});

EXAMPLE RESPONSE
{
    "username": "corp\\ssmith",
    "telephoneExtension": "107"
}

```

Updates the specified call pop configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* telephoneExtension (optional) - The telephone extension for which to receive the call pop. If not provided, the telephone extension for the current user will be used.

##### Returns

Returns the call pop configuration object if the update succeeded. Returns an error if update parameters are invalid.

### Code Types

#### Create a code type

```
DEFINITION
POST http://apiserver/codetypes

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes", {
    "securityRequired": true,
    "id": "ACCICECRM",
    "description": "Favorite Ice Cream",
    "displaySequence": 50,
    "isMultiValue": false,
    "labelDescription": "Favorite Ice",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "isFamilyCode": false,
    "requiredForAccountType": null,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "securityRequired": true,
    "id": "ACCICECRM",
    "description": "Favorite Ice Cream",
    "displaySequence": 50,
    "isMultiValue": false,
    "labelDescription": "Favorite Ice",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "isFamilyCode": false,
    "requiredForAccountType": null,
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Creates a new code type.

##### Arguments

* id (required) - The unique id for the new code type.

##### Returns

Returns a code type object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve a code type

```

DEFINITION
GET http://apiserver/codetypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/MAILCODE");

EXAMPLE RESPONSE
{
    "id": "MAILCODE",
    "description": "MAILCODE",
    "displaySequence": 0,
    "isMultiValue": true,
    "labelDescription": "MAILCODE",
    "isUserDefined": true,
    "category": "ACCOUNT",
    "isFamilyCode": false,
    "requiredForAccountType": null,
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Retrieves the details of an existing code type. You need only supply the code type.

##### Arguments

* id (required) - The code type of the code type object to be retrieved.

##### Returns

Returns a code type object if a valid id was provided.

#### Update a code type

```
DEFINITION
POST http://apiserver/codetypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM", {
    "displaySequence": 40,
});

EXAMPLE RESPONSE
{
    "securityRequired": true,
    "id": "ACCICECRM",
    "description": "Favorite Ice Cream",
    "displaySequence": 40,
    "isMultiValue": false,
    "labelDescription": "Favorite Ice",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "isFamilyCode": false,
    "requiredForAccountType": null,
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Updates the specified code type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* securityRequired (optional) - The security required property of the code type.
* description (optional) - The description of the code type.
* displaySequence (optional) - The display sequence of the code type.
* isMultiValue (optional) - Indicates code type is single/multi value.
* labelDescription (optional) - The label description of the code type.
* isUserDefined (optional) - Indicates code type is user defined.
* category (optional) - The category of the code type.
* isFamilyCode (optional) - Indicates code type is a family code.
* requiredForAccountType (optional) - Indicates code type is required for account type.
* isActive (optional) - Indicates code type is active/inactive.
* isDisplayableInStudioOnline (optional) - Indicates whether the date type is able to be displayed in StudioOnline.
* isSearchableInStudioOnline (optional) - Indicates whether the date type is able to be searched in StudioOnline.

##### Returns

Returns the code type object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid category).

#### Delete a code type

```
DEFINITION
DELETE http://apiserver/codetypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/codetypes/ACCICECRM", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a code type. It cannot be undone.

##### Arguments

* id (required) - The code type id of the code type to be deleted.

##### Returns

Returns a 204 No Content response on success. If the code type does not exist, this call returns an error.

#### List all code types

```
DEFINITION
GET http://apiserver/codetypes

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes?isActive=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 581
    },
    "items": [
        {
            "id": "MAILCODE",
            "description": "MAILCODE",
            "displaySequence": 0,
            "isMultiValue": true,
            "labelDescription": "MAILCODE",
            "isUserDefined": true,
            "category": "ACCOUNT",
            "isFamilyCode": false,
            "requiredForAccountType": null,
            "isActive": true,
            "isDisplayableInStudioOnline": false,
            "isSearchableInStudioOnline": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all code types matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in code type
* description () - Filter list by partial match in description
* category () - Filter list by partial match in category
* requiredForAccountType () - Filter list by exact match in requiredForAccountType.
* isActive () - Filter list by whether active or not
* isFamilyCode () - Filter list by whether family code or not
* isMultiValue () - Filter list be whether multi-value or not
* isDisplayableInStudioOnline () - Filter list by whether marked as displayable in StudioOnline or not
* isSearchableInStudioOnline () - Filter list by whether marked as searchable in StudioOnline or not

##### Returns

A dictionary with an items property that contains an array of up to limit code types, starting at index offset. Each entry in the array is a separate code type object. If no more code types are available, the resulting array will be empty. This request should never return an error.

### Code Type Values

#### Create a code type value

```
DEFINITION
POST http://apiserver/codetypes/:id/values

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values", {
    "id": "STRAWBERRY",
    "description": "Strawberry",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "STRAWBERRY",
    "description": "Strawberry",
    "isActive": true
}

```

Creates a new code type value object

##### Arguments

* id (required) - The value of code type value.
* description (optional) - The description limit.
* isActive (optional) - Indicates if code type value is active/inactive.

##### Returns

Returns a code type value object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid id).

#### Retrieve a code type value

```
DEFINITION
GET http://apiserver/codetypes/:id/values/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/ACCICECRM/values/STRAWBERRY");

EXAMPLE RESPONSE
{
    "id": "STRAWBERRY",
    "description": "Strawberry",
    "isActive": true
}

```

Retrieves the details of an existing code type value. You need only supply the codetype id and code type value id.

##### Returns

Returns a code type value object if a valid id was provided.

#### Update a code type value

```
DEFINITION
POST http://apiserver/codetypes/:id/values/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values/Strawberry", {
    "description": "Strawberry ice cream"
});

EXAMPLE RESPONSE
{
    "id": "STRAWBERRY",
    "description": "Strawberry ice cream",
    "isActive": true
}

```

Updates the specified code type value by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - The value of code type value.
* description (optional) - The description limit.
* isActive (optional) - Indicates if code type value is active/inactive.

##### Returns

Returns the code type value object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined codetype or invalid code type value id).

#### Delete a code type value

```
DEFINITION
DELETE http://apiserver/codetypes/:id/values/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/codetypes/ACCICECRM/values/RROAD", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a code type value. It cannot be undone.

##### Arguments

* id (required) - The id of the code type value to be deleted.

##### Returns

Returns a 204 No Content response on success. If the code type value id does not exist, this call returns an error.

#### List all code type values

```
DEFINITION
GET http://apiserver/codetypes/:id/values

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/MAILCODE/values?isActive=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 37
    },
    "items": [
        {
            "id": "0",
            "description": "Default Mail",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all code type values matching the provided filter criteria.

##### Arguments

* id () - Filter list by partial match in code type value
* description () - Filter list by partial match in description
* isActive () - Filter list by whether active or not

##### Returns

A dictionary with an items property that contains an array of up to limit code type values, starting at index offset. Each entry in the array is a separate code type value object. If no more code type values are available, the resulting array will be empty. This request should never return an error.

### Code Type Attributes

#### Create a code type attribute

```
DEFINITION
POST http://apiserver/codetypes/:id/attributes

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/age/attributes", {
    "type": "NUMBER",
    "value": "INTEGER",
    "description": null
});

EXAMPLE RESPONSE
{
    "id": "240",
    "type": "NUMBER",
    "value": "INTEGER",
    "description": null
}

```

Creates a new code type attribute object

##### Arguments

* type (required) - The type of the code type attribute.
* value (optional) - The value of the code type attribute.
* description (optional) - The description of the code type attribute.

##### Returns

Returns a code type attribute object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined codetype or invalid attribute type).

#### Retrieve a code type attribute

```
DEFINITION
GET http://apiserver/codetypes/:id/attributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/age/attributes/240");

EXAMPLE RESPONSE
{
    "id": "240",
    "type": "NUMBER",
    "value": "INTEGER",
    "description": null
}

```

Retrieves the details of an existing code type attribute. You need only supply the codetype id and code type attribute id.

##### Returns

Returns a code type attribute object if a valid id was provided.

#### Update a code type attribute

```
DEFINITION
POST http://apiserver/codetypes/:id/attributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/age/attributes/240", {
    "description": "Represents age"
});

EXAMPLE RESPONSE
{
    "id": "240",
    "type": "NUMBER",
    "value": "INTEGER",
    "description": "Represents age"
}

```

Updates the specified code type attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of the code type attribute.
  + value (optional) - The value of the code type attribute.
  + description (optional) - The description of the code type attribute.

##### Returns

Returns the code type attribute object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined codetype or invalid attribute type).

#### Delete a code type attribute

```
DEFINITION
DELETE http://apiserver/codetypes/:id/attributes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/codetypes/age/attributes/240", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a code type attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the code type attribute to be deleted.

##### Returns

Returns a 204 No Content response on success. If the code type attribute id does not exist, this call returns an error.

#### List all code type attributes

```
DEFINITION
GET http://apiserver/codetypes/:id/attributes

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/age/attributes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "240",
            "type": "NUMBER",
            "value": "INTEGER",
            "description": "Represents age"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all code type attributes.

##### Returns

A dictionary with an items property that contains an array of up to limit code type attributes, starting at index offset. Each entry in the array is a separate code type attribute object. If no more code type attributes are available, the resulting array will be empty. This request should never return an error.

### Code Type Dependencies

#### Create a code type dependency

```
DEFINITION
POST http://apiserver/codetypes/:id/dependencies

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/item-id/dependencies", {
    "code": "ADVOCATE-2",
    "description": "Ministry Advocate-2"
});

EXAMPLE RESPONSE
{
    "id": "29",
    "code": "ADVOCATE-2",
    "description": "Ministry Advocate-2"
}

```

Creates a new code type dependency object

##### Arguments

* code (required) - The dependency code.
* description (optional) - The description of the dependency code.

##### Returns

Returns a code type dependency object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or invalid code).

#### Retrieve a code type dependency

```
DEFINITION
GET http://apiserver/codetypes/:id/dependencies/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/item-id/dependencies/29");

EXAMPLE RESPONSE
{
    "id": "29",
    "code": "ADVOCATE-2",
    "description": "Ministry Advocate-2"
}

```

Retrieves the details of an existing code type dependency. You need only supply the componentname id and code type dependency id.

##### Returns

Returns a code type dependency object if a valid id was provided.

#### Update a code type dependency

```
DEFINITION
POST http://apiserver/codetypes/:id/dependencies/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/item-id/dependencies/29", {
    "description": "Ministry Advocate-2"
});

EXAMPLE RESPONSE
{
    "id": "29",
    "code": "ADVOCATE-2",
    "description": "Ministry Advocate-2"
}

```

Updates the specified code type dependency by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* code (optional) - The dependency code.
* description (optional) - The description of the dependency code.

##### Returns

Returns the code type dependency object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or invalid dependency code).

#### Delete a code type dependency

```
DEFINITION
DELETE http://apiserver/codetypes/:id/dependencies/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/codetypes/item-id/dependencies/29", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a code type dependency. It cannot be undone.

##### Arguments

* id (required) - The id of the code type dependency to be deleted.

##### Returns

Returns a 204 No Content response on success. If the code type dependency id does not exist, this call returns an error.

#### List all code type dependencies

```
DEFINITION
GET http://apiserver/codetypes/:id/dependencies

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/item-id/dependencies");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "71",
            "code": "APLD100",
            "description": "Account Pledge - Current Donor"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all code type attributes.

##### Returns

A dictionary with an items property that contains an array of up to limit code type dependencies, starting at index offset. Each entry in the array is a separate code type dependency object. If no more code type dependencies are available, the resulting array will be empty. This request should never return an error.

### Code Type Value Attributes

#### Create a code type value attribute

```
DEFINITION
POST http://apiserver/codetypes/:id/values/:id/attributes

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values/choc/attributes", {
    "type": "TASTE",
    "value": "TASTE VALUE",
    "description": "Taste of ice cream"
});

EXAMPLE RESPONSE
{
    "id": "20610",
    "type": "TASTE",
    "value": "TASTE VALUE",
    "description": "Taste of ice cream"
}

```

Creates a new code type value attribute object

##### Arguments

* type (required) - The type of the code type value attribute.
* value (required) - The value of the code type value attribute.
* description (optional) - The description of the code type value attribute.

##### Returns

Returns a code type value attribute object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type attribute value).

#### Retrieve a code type value attribute

```
DEFINITION
GET http://apiserver/codetypes/:id/values/:id/attributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/ACCICECRM/values/choc/attributes/20610");

EXAMPLE RESPONSE
{
    "id": "20610",
    "type": "TASTE",
    "value": "TASTE VALUE",
    "description": "Taste of ice cream"
}

```

Retrieves the details of an existing code type value attribute. You need only supply the codetype id, code type value id, code type value attribute id.

##### Returns

Returns a code type value attribute object if a valid id was provided.

#### Update a code type value attribute

```
DEFINITION
POST http://apiserver/codetypes/:id/values/:id/attributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values/choc/attributes/20610", {
    "description": "Taste of the chocolate ice cream"
});

EXAMPLE RESPONSE
{
    "id": "20610",
    "type": "TASTE",
    "value": "TASTE VALUE",
    "description": "Taste of ice cream"
}

```

Updates the specified code type value attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (required) - The type of the code type value attribute.
* value (required) - The value of the code type value attribute.
* description (optional) - The description of the code type value attribute.

##### Returns

Returns the code type value attribute object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type, code type value, or code type value attribute).

#### Delete a code type value attribute

```
DEFINITION
DELETE http://apiserver/codetypes/:id/values/:id/attributes:/id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/codetypes/ACCICECRM/values/choc/attributes/20610", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a code type value attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the code type value attribute to be deleted.

##### Returns

Returns a 204 No Content response on success. If the code type value attribute id does not exist, this call returns an error.

#### List all code type value attributes

```
DEFINITION
GET http://apiserver/codetypes/:id/values/:id/attributes

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/DDCCOMPANY/values/QUICK/attributes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "10540",
            "type": "SUGGDONEN",
            "value": "FALSE",
            "description": "Suggested Donation Default"
        }
    ]
}

```

Returns a list of all attributes for the specified code type value.

##### Returns

A dictionary with an items property that contains an array of up to limit code type value attributes, starting at index offset. Each entry in the array is a separate code type value attribute object. If no more code type value attributes are available, the resulting array will be empty. This request should never return an error.

### Code Type Value Dependent Values

#### Create a code type value dependent value

```
DEFINITION
POST http://apiserver/codetypes/:id/values/:id/dependentvalues

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values/choc/dependentvalues", {
    "type": "APLD100",
    "value": "YES"
});

EXAMPLE RESPONSE
{
    "id": "10691",
    "type": "APLD100",
    "typeDescription": "Account Pledge - Current Donor",
    "value": "YES",
    "valueDescription": "Yes"
}

```

Creates a new code type value dependent value object

##### Arguments

* type (required) - The type of the code type value dependent value.
* value (required) - The value of the code type value dependent value.

##### Returns

Returns a code type value dependent value object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type value dependent value).

#### Retrieve a code type value dependent value

```
DEFINITION
GET http://apiserver/codetypes/:id/values/:id/dependentvalues/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/ACCICECRM/values/choc/dependentvalues/10691");

EXAMPLE RESPONSE
{
    "id": "10691",
    "type": "APLD100",
    "typeDescription": "Account Pledge - Current Donor",
    "value": "YES",
    "valueDescription": "Yes"
}

```

Retrieves the details of an existing code type value dependent value. You need only supply the codetype id, code type value id, code type value dependent value id.

##### Returns

Returns a code type value dependent value object if a valid id was provided.

#### Update a code type value dependent value

```
DEFINITION
POST http://apiserver/codetypes/:id/values/:id/dependentvalues/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values/choc/dependentvalues/10691", {
    "value": "YES"
});

EXAMPLE RESPONSE
{
    "id": "10691",
    "type": "APLD100",
    "typeDescription": "Account Pledge - Current Donor",
    "value": "YES",
    "valueDescription": "Yes"
}

```

Updates the specified code type value dependent value by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (required) - The type of the code type value dependent value.
* value (required) - The value of the code type value dependent value.

##### Returns

Returns the code type value dependent value object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type, code type value, or code type value dependent value).

#### Delete a code type value dependent value

```
DEFINITION
DELETE http://apiserver/codetypes/:id/values/:id/dependentvalues:/id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/codetypes/ACCICECRM/values/choc/dependentvalues/20610", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a code type value dependent value. It cannot be undone.

##### Arguments

* id (required) - The id of the code type value dependent value to be deleted.

##### Returns

Returns a 204 No Content response on success. If the code type value dependent value id does not exist, this call returns an error.

#### List all code type value dependent values

```
DEFINITION
GET http://apiserver/codetypes/:id/values/dependentvalues/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/ACCICECRM/values/choc/dependentvalues");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20610",
            "type": "TASTE",
            "typeDescription": "Taste Type"
            "value": "TASTE VALUE",
            "valueDescription": "Taste of ice cream"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all code type value dependent values.

##### Returns

A dictionary with an items property that contains an array of up to limit code type value dependent values, starting at index offset. Each entry in the array is a separate code type value dependent value object. If no more code type value dependent values are available, the resulting array will be empty. This request should never return an error.

### Code Type Value Notes

#### Create a code type value note

```
DEFINITION
POST http://apiserver/codetypes/:id/values/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values/choc/notes", {
    "type": "ADDRSTDNOT",
    "shortComment": "Address",
    "longComment": "Address"
});

EXAMPLE RESPONSE
{
    "id": "20610",
    "type": "ADDRSTDNOT",
    "typeDescription": "Address Note",
    "shortComment": "Address",
    "longComment": "Address"
}

```

Creates a new code type value note object

##### Arguments

* type (required) - The type of the code type value note.
* shortComment (optional) - The short comment of the code type value note.
* longComment (optional) - The long comment of the code type value note.

##### Returns

Returns a code type value note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type note value).

#### Retrieve a code type value note

```
DEFINITION
GET http://apiserver/codetypes/:id/values/:id/notes:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/ACCICECRM/values/choc/notes/20610");

EXAMPLE RESPONSE
{
    "id": "20610",
    "type": "ADDRSTDNOT",
    "typeDescription": "Address Note",
    "shortComment": "Address",
    "longComment": "Address"
}

```

Retrieves the details of an existing code type value note. You need only supply the codetype id, code type value id, code type value note id.

##### Returns

Returns a code type value note object if a valid id was provided.

#### Update a code type value note

```
DEFINITION
POST http://apiserver/codetypes/:id/values/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/codetypes/ACCICECRM/values/choc/notes/20610", {
    "longComment": "The address note"
});

EXAMPLE RESPONSE
{
    "id": "20610",
    "type": "ADDRSTDNOT",
    "typeDescription": "Address Note",
    "shortComment": "Address",
    "longComment": "The address note"
}

```

Updates the specified code type value note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - The id of the code type value note.
* type (optional) - The type of the code type value note.
* shortComment (optional) - The short comment of the code type value note.
* longComment (optional) - The long comment of the code type value note.

##### Returns

Returns the code type value note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type, code type value, or code type value note).

#### Delete a code type value note

```
DEFINITION
DELETE http://apiserver/codetypes/:id/values/:id/notes:/id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/codetypes/ACCICECRM/values/choc/notes/20610", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a code type value note. It cannot be undone.

##### Arguments

* id (required) - The id of the code type value note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the code type value note id does not exist, this call returns an error.

#### List all code type value notes

```
DEFINITION
GET http://apiserver/codetypes/:id/values/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/codetypes/ACCICECRM/values/choc/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20610",
            "type": "ADDRSTDNOT",
            "typeDescription": "Address Note",
            "shortComment": "Address",
            "longComment": "The address note"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all code type value notes.

##### Returns

A dictionary with an items property that contains an array of up to limit code type value notes, starting at index offset. Each entry in the array is a separate code type value note object. If no more code type value notes are available, the resulting array will be empty. This request should never return an error.

### Control Records

#### Create a Control Record

```
DEFINITION
POST http://apiserver/controlrecords

EXAMPLE REQUEST
$.post("http://localhost:49195/controlrecords", {
    "id": "ACTSRCEDIT",
    "description": "Account Source Edit",
    "value": "Y",
    "comment": "Account Source Edit (Y/N)"
});

EXAMPLE RESPONSE
{
    "id": "ACTSRCEDIT",
    "description": "Account Source Edit",
    "value": "Y",
    "comment": "Account Source Edit (Y/N)"
}

```

Creates a new Control Record.

##### Arguments

* id (required) - The type.
* description (required) - The description.
* value (required) - The value.
* comment () - The comment.

##### Returns

Returns a Control Record object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a control record

```
DEFINITION
GET http://apiserver/controlrecords/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/controlrecords/ACTSRCEDIT");

EXAMPLE RESPONSE
{
    "id": "ACTSRCEDIT",
    "description": "Account Source Edit",
    "value": "Y",
    "comment": "Account Source Edit (Y/N)"
}

```

Retrieves the details of an existing control record. You need only supply the control type.

##### Arguments

* id (required) - The control type of the control record object to be retrieved.

##### Returns

Returns a control record object if a valid control type was provided.

#### Update a Control Record

```
DEFINITION
POST http://apiserver/controlrecords/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/controlrecords/ACTSRCEDIT", {
    "id": "ACTSRCEDIT",
    "description": "Account Source Edit",
    "value": "Y",
    "comment": "Account Source Edit (Y/N)"
});

EXAMPLE RESPONSE
{
    "id": "ACTSRCEDIT",
    "description": "Account Source Edit",
    "value": "Y",
    "comment": "Account Source Edit (Y/N)"
}


```

Updates the specified Control Record by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id () - The type.
* description () - The description.
* value () - The value.
* comment () - The comment.

##### Returns

Returns the Control Record object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Control Record

```
DEFINITION
DELETE http://apiserver/controlrecords/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/controlrecords/3PPTEST", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Control Record. It cannot be undone.

##### Arguments

* id (required) - The id of the Control Record to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Control Record does not exist, this call returns an error.

#### List all control records

```
DEFINITION
GET http://apiserver/controlrecords

EXAMPLE REQUEST
$.get("http://localhost:49195/controlrecords?value=Y");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 43
    },
    "items": [
        {
            "id": "ACTSRCEDIT",
            "description": "Account Source Edit",
            "value": "Y",
            "comment": "Account Source Edit (Y/N)"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all control record matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in control type
* description () - Filter list by partial match in description
* value () - Filter list by partial match in value

##### Returns

A dictionary with an items property that contains an array of up to limit control records, starting at index offset. Each entry in the array is a separate control record object. If no more controle records are available, the resulting array will be empty. This request should never return an error.

### Countries

#### Retrieve a country

```
DEFINITION
GET http://apiserver/countries/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/countries/CA");

EXAMPLE RESPONSE
{
    "id": "CA",
    "description": "Canada",
    "isActive": true
}

```

Retrieves the details of an existing country. You need only supply the country code.

##### Arguments

* id (required) - The country code of the country object to be retrieved.

##### Returns

Returns a country object if a valid country code was provided.

#### List all countries

```
DEFINITION
GET http://apiserver/countries

EXAMPLE REQUEST
$.get("http://localhost:49195/countries?id=CA");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "CA",
            "description": "Canada",
            "isActive": true
        }
    ]
}

```

Returns a list of all countries matching the provided filter criteria.

##### Arguments

* id () - Filter list by partial match in country code
* description () - Filter list by partial match in description
* isActive () - Filter list by whether active or not

##### Returns

A dictionary with an items property that contains an array of up to limit countries, starting at index offset. Each entry in the array is a separate country object. If no more countries are available, the resulting array will be empty. This request should never return an error.

### Country States

#### Retrieve a certain country state

```
DEFINITION
GET http://apiserver/countries/:country/states/:state

EXAMPLE REQUEST
$.get("http://localhost:49195/countries/USA/states/TX");

EXAMPLE RESPONSE
{
    "description": "Texas"
    "id": "TX"
}

```

Retrieves the state of an existing country.

##### Arguments

* country (required) - The country code for the country that the state belongs to.
* state (required) - The two-digit state code for the state to retrieve.

##### Returns

Returns a state object if a valid id was provided.

#### List all countries states

```
DEFINITION
GET http://apiserver/countries/:id/states

EXAMPLE REQUEST
$.get("http://localhost:49195/countries/CA/states?id=N");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 5
    },
    "items": [
        {
            "id": "NB",
            "description": "New Brunswick"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all country states matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in state code
* description () - Filter list by partial match in description

##### Returns

A dictionary with an items property that contains an array of up to limit country states, starting at index offset. Each entry in the array is a separate country state object. If no more country states are available, the resulting array will be empty. This request should never return an error.

#### Create a Country State

```
DEFINITION
POST http://apiserver/countrystates

EXAMPLE REQUEST
$.post("http://localhost:49195/countrystates", {
    "country": "USA",
    "state": "TX",
    "description": "Texas"
});

EXAMPLE RESPONSE
{
    "id": "10250",
    "country": "USA",
    "countryDescription": "United States of America",
    "state": "TX",
    "description": "Texas"
}

```

Creates a new Country State.

##### Arguments

* country (required) - The country code for the country that the state belongs to.
* state (required) - The two-digit state code for the state to retrieve.
* description (required) - The description

##### Returns

Returns a Country State object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Country State

```
DEFINITION
GET http://apiserver/countrystates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/countrystates/10250");

EXAMPLE RESPONSE
{
    "id": "10250",
    "country": "USA",
    "countryDescription": "United States of America",
    "state": "TX",
    "description": "Texas"
}

```

Retrieves the details of an existing Country State. You need only supply the id.

##### Arguments

* id (required) - The id of the Country State to be retrieved.

#### Update a Country State

```
DEFINITION
POST http://apiserver/countrystates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/countrystates/10250", {
    "country": "USA",
    "state": "TX",
    "description": "Texas"

});

EXAMPLE RESPONSE
{
    "id": "10250",
    "country": "USA",
    "countryDescription": "United States of America",
    "state": "TX",
    "description": "Texas"
}


```

Updates the specified Country State by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* country () - The country code for the country that the state belongs to.
* state () - The two-digit state code for the state to retrieve.
* description () - The description

##### Returns

Returns the Country State object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Country State

```
DEFINITION
DELETE http://apiserver/countrystates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/countrystates/10250", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a CountryState. It cannot be undone.

##### Arguments

* id (required) - The id of the CountryState to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the CountryState does not exist, this call returns an error.

#### List all Country States

```
DEFINITION
GET http://apiserver/countrystates

EXAMPLE REQUEST
$.get("http://localhost:49195/countrystates?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10250",
            "country": "USA",
            "countryDescription": "United States of America",
            "state": "TX",
            "description": "Texas"
        },
        {...},
    ]
}

```

Returns a list of all Country States.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* country () - The country code for the country that the state belongs to.
* state () - The two-digit state code for the state to retrieve.
* description () - The description

##### Returns

A dictionary with an items property that contains an array of up to limit Country States, starting at index offset. Each entry in the array is a separate country state object. If no more Country States are available, the resulting array will be empty. This request should never return an error.

### Country Postal Code Media Outlet

#### Retrieve a country postal code media outlet

```
DEFINITION
GET http://apiserver/countries/:id/postalcodes/:id/mediaoutlet

EXAMPLE REQUEST
$.get("http://localhost:49195/countries/USA/postalcodes/53/mediaoutlet");

EXAMPLE RESPONSE
{
    "id": "WMBI-FM"
}

```

Retrieves the id of an existing country postal code media outlet. You need only supply the country postal code id.

##### Arguments

* id (required) - The id of the country postal code to retrieve the media outlet for.

##### Returns

Returns a country postal code media outlet object if a valid id was provided.

### Country Postal Codes

#### Retrieve a country postal code

```
DEFINITION
GET http://apiserver/countries/:id/postalcodes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/countries/CA/postalcodes/43343");

EXAMPLE RESPONSE
{
    "id": "43343",
    "start": "E2E 2V2",
    "end": "E2E 2V2",
    "defaultCity": "Quispamisis",
    "defaultState": "NB"
}

```

Retrieves the details of an existing country postal code. You need only supply the country postal code id.

##### Arguments

* id (required) - The id of the country postal code to be retrieved.

##### Returns

Returns a country postal code object if a valid id was provided.

#### Verify a country postal code

```
DEFINITION
GET http://apiserver/countries/:id/postalcode

EXAMPLE REQUEST
$.get("http://localhost:49195/countries/CA/postalcode?postalCode=E2E%202V2");

EXAMPLE RESPONSE
{
    "id": "43343",
    "start": "E2E 2V2",
    "end": "E2E 2V2",
    "defaultCity": "Quispamisis",
    "defaultState": "NB"
}

```

Verifies whether a postal code range is found for the specified postal code. You need only supply the postal code.

This resource exist as an alternative to /countries/:id/postalcodes which does a partial match on postal code and /countries/:id/postalcodes/:id which requires the postal code id.

##### Arguments

* postalCode (required) - The postal code to be verified.

##### Returns

Returns a country postal code object if the specified postal code is found. If not found, returns a 404.

#### List all country postal codes

```
DEFINITION
GET http://apiserver/countries/:id/postalcodes

EXAMPLE REQUEST
$.get("http://localhost:49195/countries/CA/postalcodes?defaultState=NB");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 5
    },
    "items": [
        {
            "id": "43343",
            "start": "E2E 2V2",
            "end": "E2E 2V2",
            "defaultCity": "Quispamisis",
            "defaultState": "NB"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all country postal codes matching the provided filter criteria.

##### Arguments

* postalCode () - Filter list by matching provided code between start and end of postal code ranges on each postal code object in the list
* defaultCity () - Filter list by partial match in defaultCity
* defaultState () - Filter list by partial match in defaultState
* isCountryExactMatch (optional; defaults to 'false') - When set to true, only postal codes with an *exact* match on country code will be returned; otherwise, a partial match will be performed.

##### Returns

A dictionary with an items property that contains an array of up to limit country postal codes, starting at index offset. Each entry in the array is a separate country postal code object. If no more country postal codes are available, the resulting array will be empty. This request should never return an error.

### Credit Card Processings

#### Create a Credit Card Processing

```
DEFINITION
POST http://apiserver/creditcardprocessing

EXAMPLE REQUEST
$.post("http://localhost:49195/creditcardprocessing", {
    "id": "1",
    "accountingIntegrationConfigurationCode": null,
    "accountingDatabseServer": null,
    "accountingDatabseName": null,
    "accountingDatabseOwner": null,
    "inventoryDatabseServer": null,
    "inventoryDatabseName": null,
    "inventoryDatabseOwner": null,
    "baseCurrency": null,
    "giftCardAssemblyName": null,
    "giftCardClassName": null
});

EXAMPLE RESPONSE
{
    "id": "1",
    "companyDescription": "SON Media",
    "accountingIntegrationConfigurationCode": null,
    "accountingDatabseServer": null,
    "accountingDatabseName": null,
    "accountingDatabseOwner": null,
    "inventoryDatabseServer": null,
    "inventoryDatabseName": null,
    "inventoryDatabseOwner": null,
    "baseCurrency": null,
    "giftCardAssemblyName": null,
    "giftCardClassName": null,
    "payPalRestApiBaseUrl": null,
    "payPalRestApiClientId": null,
}

```

Creates a new Credit Card Processing.

##### Arguments

* id (required) - The company code.
* accountingIntegrationConfigurationCode (optional) - The Integration Configuration code for an Accounting integration.
* accountingDatabaseServer () - The accounting database server.
* accountingDatabaseName () - The accounting database name.
* accountingDatabaseOwner () - The accounting database owner.
* inventoryDatabaseServer () - The inventory database server.
* inventoryDatabaseName () - The inventory database name.
* inventoryDatabaseOwner () - The inventory database owner.
* baseCurrency () - The base currency.
* giftCardAssemblyName () - The gift card assmebly name.
* giftCardClassName () - The gift card class name.
* payPalRestApiBaseUrl (optional) - The base URL to use when making PayPal REST API calls.
* payPalRestApiClientId (optional) - The client ID to use when making PayPal REST API calls.

##### Returns

Returns a Credit Card Processing object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Credit Card Processing

```
DEFINITION
GET http://apiserver/creditcardprocessing/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/creditcardprocessing/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "companyDescription": "SON Media",
    "accountingIntegrationConfigurationCode": null,
    "accountingDatabseServer": null,
    "accountingDatabseName": null,
    "accountingDatabseOwner": null,
    "inventoryDatabseServer": null,
    "inventoryDatabseName": null,
    "inventoryDatabseOwner": null,
    "baseCurrency": null,
    "giftCardAssemblyName": null,
    "giftCardClassName": null,
    "payPalRestApiBaseUrl": null,
    "payPalRestApiClientId": null,
}

```

Retrieves the details of an existing Credit Card Processing. You need only supply the id.

##### Arguments

* id (required) - The id of the Credit Card Processing to be retrieved.

#### Update a Credit Card Processing

```
DEFINITION
POST http://apiserver/creditcardprocessing/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/creditcardprocessing/1", {
    "accountingIntegrationConfigurationCode": null,
    "accountingDatabseServer": null,
    "accountingDatabseName": null,
    "accountingDatabseOwner": null,
    "inventoryDatabseServer": null,
    "inventoryDatabseName": null,
    "inventoryDatabseOwner": null,
    "baseCurrency": null,
    "giftCardAssemblyName": null,
    "giftCardClassName": null
});

EXAMPLE RESPONSE
{
    "id": "1",
    "companyDescription": "SON Media",
    "accountingIntegrationConfigurationCode": null,
    "accountingDatabseServer": null,
    "accountingDatabseName": null,
    "accountingDatabseOwner": null,
    "inventoryDatabseServer": null,
    "inventoryDatabseName": null,
    "inventoryDatabseOwner": null,
    "baseCurrency": null,
    "giftCardAssemblyName": null,
    "giftCardClassName": null,
    "payPalRestApiBaseUrl": null,
    "payPalRestApiClientId": null,
}


```

Updates the specified Credit Card Processing by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The company code.
* accountingIntegrationConfigurationCode (optional) - The Integration Configuration code for an Accounting integration.
* accountingDatabaseServer () - The accounting database server.
* accountingDatabaseName () - The accounting database name.
* accountingDatabaseOwner () - The accounting database owner.
* inventoryDatabaseServer () - The inventory database server.
* inventoryDatabaseName () - The inventory database name.
* inventoryDatabaseOwner () - The inventory database owner.
* baseCurrency () - The base currency.
* giftCardAssemblyName () - The gift card assmebly name.
* giftCardClassName () - The gift card class name.
* payPalRestApiBaseUrl (optional) - The base URL to use when making PayPal REST API calls.
* payPalRestApiClientId (optional) - The client ID to use when making PayPal REST API calls.

##### Returns

Returns the Credit Card Processing object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Credit Card Processing

```
DEFINITION
DELETE http://apiserver/creditcardprocessing/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/creditcardprocessing/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Credit Card Processing. It cannot be undone.

##### Arguments

* id (required) - The id of the Credit Card Processing to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Credit Card Processing does not exist, this call returns an error.

#### List all Credit Card Processings

```
DEFINITION
GET http://apiserver/creditcardprocessing

EXAMPLE REQUEST
$.get("http://localhost:49195/creditcardprocessing?");

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
            "companyDescription": "SON Media",
            "accountingIntegrationConfigurationCode": null,
            "accountingDatabseServer": null,
            "accountingDatabseName": null,
            "accountingDatabseOwner": null,
            "inventoryDatabseServer": null,
            "inventoryDatabseName": null,
            "inventoryDatabseOwner": null,
            "baseCurrency": null,
            "giftCardAssemblyName": null,
            "giftCardClassName": null,
            "payPalRestApiBaseUrl": null,
            "payPalRestApiClientId": null,
        },
        {...},
    ]
}

```

Returns a list of all Credit Card Processings.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - The company code.
* provider () - The credit card processing provider.

##### Returns

A dictionary with an items property that contains an array of up to limit Credit Card Processings, starting at index offset. Each entry in the array is a separate credit card processing object. If no more Credit Card Processings are available, the resulting array will be empty. This request should never return an error.

#### Retrieve Credit Card Info For Transaction Processing

NOTE: THIS ROUTE IS DEPRECATED. You should use [Retrieve payment gateway configuration for transaction processing](#retrieve-payment-gateway-configuration-for-transaction-processing) instead.

```
DEFINITION
GET http://apiserver/creditcardinfofortransactionprocessing/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/creditcardinfofortransactionprocessing/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "companyDescription": "SON Media",
    "provider": "TRUSTCOMM",
    "providerDescription": "TrustCommerce",
    "useEncrptedCC": true,
    "supportsUpdateExpDateOnly": false,
    "tokenizeEFT": true,
    "additionalParameters": null
}

```

Retrieves the details of an existing Credit Card Info For Transaction Processing. You need only supply the id.

##### Arguments

* id (required) - The id of the Credit Card Info For Transaction Processing to be retrieved.

#### List all Credit Card Info For Transaction Processing

NOTE: THIS ROUTE IS DEPRECATED. You should use [Retrieve payment gateway configuration for transaction processing](#retrieve-payment-gateway-configuration-for-transaction-processing) instead.

```
DEFINITION
GET http://apiserver/creditcardinfofortransactionprocessing

EXAMPLE REQUEST
$.get("http://localhost:49195/creditcardinfofortransactionprocessing?");

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
            "companyDescription": "SON Media",
            "provider": "TRUSTCOMM",
            "providerDescription": "TrustCommerce",
            "useEncrptedCC": true,
            "supportsUpdateExpDateOnly": false,
            "tokenizeEFT": true,
            "additionalParameters": null
        },
        {...},
    ]
}

```

Returns a list of all Credit Card Infos For Transaction Processing.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - The company code.
* provider () - The credit card processing provider.

##### Returns

A dictionary with an items property that contains an array of up to limit Credit Card Infos For Transaction Processing, starting at index offset. Each entry in the array is a separate credit card info for transaction processing object. If no more credit card infos for transaction processing are available, the resulting array will be empty. This request should never return an error.

### Company Payment Gateways

#### Create a company payment gateway

```
DEFINITION
POST http://apiserver/companies/:companyCode/paymentgateways

EXAMPLE REQUEST
$.post("http://localhost:49195/companies/1/paymentgateways", {
    "id": "CCONNECT",
    "description": "Clover Connect",
    "integrationConfigurationCode": "CCONNECT",
    "isDefaultForCreditCard": true,
    "isDefaultForEft": true,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "CCONNECT",
    "companyCode": "4",
    "description": "Clover Connect",
    "integrationConfigurationCode": "CCONNECT",
    "integrationConfigurationDescription": "Clover Connect Configuration",
    "isDefaultForCreditCard": true,
    "isDefaultForEft": true,
    "isActive": true
}

```

Creates a new company payment gateway.

##### Arguments

* id (required) - The payment gateway code for the company payment gateway. A duplicate 10 character, UPPERCASE payment gateway code cannot exist under the same company.
* integrationConfigurationCode (required) - The integration configuration code for the integration configuration that contains the payment gateway configuration.
* description (optional) - The description for the company payment gatway.
* isDefaultForCreditCard (optional) - Whether the payment gateway should be used as the default for credit cards payment types. Defaults to `false`.
* isDefaultForEft (optional) - Whether the payment gateway should be used as the default for EFT payment types. Defaults to `false`.
* isActive (optional) - Whether the payment gateway is active and can be used for new transactions, recurrings, saved payments, etc. Defaults to `false`.

##### Returns

Returns a company payment gateway object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a company payment gateway

```
DEFINITION
GET http://apiserver/companies/:companyCode/paymentgateways/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/companies/1/paymentgateways/CCONNECT");

EXAMPLE RESPONSE
{
    "id": "CCONNECT",
    "companyCode": "4",
    "description": "Clover Connect",
    "integrationConfigurationCode": "CCONNECT",
    "integrationConfigurationDescription": "Clover Connect Configuration",
    "isDefaultForCreditCard": true,
    "isDefaultForEft": true,
    "isActive": true
}

```

Retrieves the details of an existing company payment gateway.

##### Arguments

* companyCode (required) - The parent company code of the company payment gateway to be retrieved.
* id (required) - The id of the company payment gateway to be retrieved.

#### Update a company payment gateway

```
DEFINITION
POST http://apiserver/companies/:companyCode/paymentgateways/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/companies/1/paymentgateways/CCONNECT", {
    "description": "Clover Connect Payment Gateway",
    "isDefaultForEft": false
});

EXAMPLE RESPONSE
{
    "id": "CCONNECT",
    "companyCode": "4",
    "description": "Clover Connect Payment Gateway",
    "integrationConfigurationCode": "CCONNECT",
    "integrationConfigurationDescription": "CloverConnect Configuration",
    "isDefaultForCreditCard": true,
    "isDefaultForEft": false,
    "isActive": true


```

Updates the specified company payment gateway by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* companyCode (required) - The parent company code of the company payment gateway to be updated.
* id (required) - The id of the company payment gateway to be updated.
* integrationConfigurationCode (optional) - The integration configuration code for the integration configuration that contains the payment gateway configuration.
* description (optional) - The description for the company payment gatway.
* isDefaultForCreditCard (optional) - Whether the payment gateway should be used as the default for credit cards payment types.
* isDefaultForEft (optional) - Whether the payment gateway should be used as the default for EFT payment types.
* isActive (optional) - Whether the payment gateway is active and can be used for new transactions, recurrings, saved payments, etc.

##### Returns

Returns the company payment gateway object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a company payment gateway

```
DEFINITION
DELETE http://apiserver/companies/:companyCode/paymentgateways/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/companies/1/paymentgateways/CCONNECT", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a company payment gateway. It cannot be undone.

##### Arguments

* companyCode (required) - The parent company code of the company payment gateway to be deleted.
* id (required) - The id of the company payment gateway to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the company payment gateway does not exist, this call returns an error.

#### List all company payment gateways

```
DEFINITION
GET http://apiserver/companies/:companyCode/paymentgateways

EXAMPLE REQUEST
$.get("http://localhost:49195/companies/1/paymentgateways");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "CCONNECT",
            "companyCode": "4",
            "description": "Clover Connect Payment Gateway",
            "integrationConfigurationCode": "CCONNECT",
            "integrationConfigurationDescription": "CardConnect Configuration",
            "isDefaultForCreditCard": true,
            "isDefaultForEft": false,
            "isActive": true
        },
        {...}
    ]
}

```

Returns a list of all company payment gateways.

##### Arguments

* companyCode (required) - The parent company code of all company payment gateways to be retrieved.
* isActive (optional) - Whether to return active (`true`) or inactive (`false`) company payment gateways. Do not include to return all for the companyCode.

##### Returns

A dictionary with an items property that contains an array of up to limit company payment gateways, starting at index offset. Each entry in the array is a separate company payment gateway object. If no more company payment gateways are available, the resulting array will be empty. This request should never return an error.

### CRM Roles

#### Retrieve a CRM Role

```
DEFINITON
GET http://apiserver/crmroles/:id

EXAMPLE REQUEST
$.get("http://localhost:49194/crmroles/CRM2013");

EXAMPLE RESPONSE
{
    "id": "CRM2013",
    "description": "Donor Development CRM",
    "baseUri": "https://devcrm.company.com",
    "database": "DEVCRM",
    "server": "DEVCRMAPPSQL",
    "majorVersion": 5,
    "ifdMode": false,
    "organization": "DEVCRM"
}

```

Retrieves the details of an existing CRM Role. You need only supply the CRM Role id.

##### Arguments

* id (required) - The id of the CRM Role to be retrieved.

##### Returns

Returns a CRM Role object if a valid id was provided.

#### List all CRM Roles

```
DEFINITON
GET http://apiserver/crmroles

EXAMPLE REQUEST
$.get("http://localhost:49194/crmroles");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "CRM2013",
            "description": "Donor Development CRM",
            "baseUri": "https://devcrm.company.com",
            "database": "DEVCRM",
            "server": "DEVCRMAPPSQL",
            "majorVersion": 5,
            "ifdMode": false,
            "organization": "DEVCRM"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all CRM Roles \ Environments.

##### Arguments

* id () - Filter list by partial match in role id
* description () - Filter list by partial match in description

##### Returns

A dictionary with an items property that contains an array of up to limit CRM Roles, starting at index offset. Each entry in the array is a separate CRM Role object. If no more CRM Roles are available, the resulting array will be empty. This request should never return an error.

### CRM Role Owners

#### Retrieve a CRM Role Owner

```
DEFINITON
GET http://apiserver/crmroles/:id/owners/:id

EXAMPLE REQUEST
$.get("http://localhost:49194/crmroles/CRM2013/owners/DDTeam");

EXAMPLE RESPONSE
{
    "id": "DDTeam",
    "description": "Donor Development Team"
}

```

Retrieves the details of an existing CRM Role Owner. You need only supply the CRM Role Owner id.

##### Arguments

* id (required) - The id of the CRM Role Owner to be retrieved.

##### Returns

Returns a CRM Role Owner object if a valid id was provided.

#### List all CRM Role Owners

```
DEFINITON
GET http://apiserver/crmroles/:id/owners

EXAMPLE REQUEST
$.get("http://localhost:49194/crmroles/CRM2013/owners");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "myDomain\jDoe",
            "description": "John Doe"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all CRM Role Owners.

##### Arguments

* id () - Filter list by partial match in owner id
* description () - Filter list by partial match in owner description

##### Returns

A dictionary with an items property that contains an array of up to limit CRM Role Owners, starting at index offset. Each entry in the array is a separate CRM Role Owner object. If no more CRM Role Owners are available, the resulting array will be empty. This request should never return an error.

### Custom Entities

#### Create a custom entity

```
DEFINITION
POST http://apiserver/customentities

EXAMPLE REQUEST
$.post("http://localhost:49195/customentities", {
    "name": "A01Codes",
    "description": "Cars Codes",
    "tableId": "A01c",
    "tableName": "A01cCarsCodes",
    "isEditInGrid": true
});

EXAMPLE RESPONSE
{
    "id": "115",
    "name": "A01Codes",
    "description": "Cars Codes",
    "tableId": "A01c",
    "tableName": "A01cCarsCodes",
    "isEditInGrid": true,
    "highlightBasedOnField": null
}

```

Creates a new custom entity.

##### Arguments

* name (required) - The name of the new custom entity.
* description (optional) - The description of the new custom entity.
* tableId (required) - The TableId of the new custom entity.
* tableName (required) - The SQL table name.
* isEditInGrid (optional; defaults to `true`) - Specifies if the UI should use grid entry or a form entry.

##### Returns

Returns a custom entity object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve a custom entity

```
DEFINITION
GET http://apiserver/customentities/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/customentities/115");

EXAMPLE RESPONSE
{
    "id": "115",
    "name": "A01Codes",
    "description": "Cars Codes",
    "tableId": "A01c",
    "tableName": "A01cCarsCodes",
    "isEditInGrid": true,
    "highlightBasedOnField": null
}

```

Retrieves the details of an existing custom entity. You need only supply the custom entity id.

##### Arguments

* id (required) - The id of the custom entity to retrieve.

##### Returns

Returns a custom entity object if a valid id was provided.

#### Update a custom entity

```
DEFINITION
POST http://apiserver/customentities/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/customentities/115", {
    "description": "Account Car Codes",
});

EXAMPLE RESPONSE
{
    "id": "115",
    "name": "A01Codes",
    "description": "Account Car Codes",
    "tableId": "A01c",
    "tableName": "A01cCarsCodes",
    "isEditInGrid": true,
    "highlightBasedOnField": null
}

```

Updates the specified custom entity by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name (optional) - The security required property of the custom entity.
* description (optional) - The description of the custom entity.
* tableId (optional) - The table id of the custom entity.
* tableName (optional) - The table name of the custom entity.
* isEditInGrid (optional) - Specifies if the UI should use grid entry or a form entry.
* highlightBasedOnField (optional) - If row highlightig is configured, determine which higlighting configuration to used based on the value of this field.

##### Returns

Returns the custom entity object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid name).

#### Delete a custom entity

```
DEFINITION
DELETE http://apiserver/customentities/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/customentities/115", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a custom entity. It cannot be undone.

##### Arguments

* id (required) - The custom entity id of the custom entity to be deleted.

##### Returns

Returns a 204 No Content response on success. If the custom entity does not exist, this call returns an error.

#### List all custom entities

```
DEFINITON
GET http://apiserver/customentities

EXAMPLE REQUEST
$.get("http://localhost:49194/customentities");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "103",
            "name": "PETS",
            "description": "Family Pets",
            "parentTableId": "A01",
            "isEditInGrid": true,
            "highlightBasedOnField": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all custom entities.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* name - Filter list by partial match in name
* description - Filter list by partial match in description
* parentTableId - Filter list by exact match in parent table id

##### Returns

A dictionary with an items property that contains an array of up to limit custom entities, starting at index offset. Each entry in the array is a separate custom entity object. If no more custom entities are available, the resulting array will be empty. This request should never return an error.

### Custom Entity Fields

#### Create a custom entity field

```
DEFINITION
POST http://apiserver/customentities/:id/fields

EXAMPLE REQUEST
$.post("http://localhost:49195/customentities/353/fields", {
    "fieldType": "DATETYPE",
    "dataType": "CAACERTDT",
    "title": "Cert Date",
    "columnName": "CAACERTDT",
    "displaySequence": 5
});

EXAMPLE RESPONSE
{
    "id": "793",
    "customEntityId": "353",
    "fieldType": "DATETYPE",
    "fieldTypeDescription": "Date types",
    "dataType": "CAACERTDT",
    "dataTypeDescription": "Certifcate date",
    "title": "Cert Date",
    "columnName": "CAACERTDT",
    "isRequired": false,
    "isForeignKey": false,
    "foreignKeyTableId": null,
    "displaySequence": 5,
    "isCalculatedField": false,
    "calculatedFieldSQL": null
}

```

Creates a new custom entity field.

##### Arguments

* fieldType - The field type; valid values are `GET /datatypes/DDCCEFIELD/values`
* dataType - The data type; valid values are `GET /datatypes/{fieldType}/values?category=CE` where the values cascade from the value of `fieldType`
* title (required) - The display title
* columnName (required) - The column name of the field that will be created in the database table for the custom entity
* isRequired (optional; default `false`) - Specifies if the field should be a required field
* displaySequence (required) - Specifies the sequence of the field in the UI in relation to other fields
* isCalculatedField (optional; default `false`) - Specifies if the field is a calculated field.
* calculatedFieldSQL (required when `isCalculatedField` is `true`) - SQL to calculate the value of the field. It is validated to prevent dangerous sql syntax.

##### Returns

Returns a custom entity field object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a custom entity field

```
DEFINITION
GET http://apiserver/customentities/:id/fields/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/customentities/353/fields/793");

EXAMPLE RESPONSE
{
    "id": "793",
    "customEntityId": "353",
    "fieldType": "DATETYPE",
    "fieldTypeDescription": "Date types",
    "dataType": "CAACERTDT",
    "dataTypeDescription": "Certifcate date",
    "title": "Cert Date",
    "columnName": "CAACERTDT",
    "isRequired": false,
    "isForeignKey": false,
    "foreignKeyTableId": null,
    "displaySequence": 5,
    "isCalculatedField": false,
    "calculatedFieldSQL": null
}

```

Retrieves the details of an existing custom entity field. You need only supply the id.

##### Arguments

* id (required) - The id of the custom entity field to be retrieved.

#### Update a custom entity field

```
DEFINITION
POST http://apiserver/customentities/:id/fields/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/customentities/353/fields/793", {
    "displaySequence": 20
});

EXAMPLE RESPONSE
{
    "id": "793",
    "customEntityId": "353",
    "fieldType": "DATETYPE",
    "fieldTypeDescription": "Date types",
    "dataType": "CAACERTDT",
    "dataTypeDescription": "Certifcate date",
    "title": "Cert Date",
    "columnName": "CAACERTDT",
    "isRequired": false,
    "isForeignKey": false,
    "foreignKeyTableId": null,
    "displaySequence": 20,
    "isCalculatedField": false,
    "calculatedFieldSQL": null
}


```

Updates the specified custom entity field by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title (optional) - The display title
* displaySequence (optional) - Specifies the sequence of the field in the UI in relation to other fields
* columnName (optional) - The column name of the field that will be created in the database table for the custom entity
* isRequired (optional) - Specifies if the field should be a required field
* isCalculatedField (optional) - Specifies if the field is a calculated field.
* calculatedFieldSQL (required when `isCalculatedField` is `true`) - SQL to calculate the value of the field. It is validated to prevent dangerous sql syntax.

##### Returns

Returns the custom entity field if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a custom entity field

```
DEFINITION
DELETE http://apiserver/customentities/:id/fields/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/customentities/353/fields/793", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a custom entity field. It cannot be undone.

##### Arguments

* id (required) - The id of the custom entity field to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the custom entity field does not exist, this call returns an error.

#### List all custom entity fields

```
DEFINITION
GET http://apiserver/customentities/:id/fields

EXAMPLE REQUEST
$.get("http://localhost:49195/customentities/353/fields");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "793",
            "customEntityId": "353",
            "fieldType": "DATETYPE",
            "fieldTypeDescription": "Date types",
            "dataType": "CAACERTDT",
            "dataTypeDescription": "Certifcate date",
            "title": "Cert Date",
            "columnName": "CAACERTDT",
            "isRequired": false,
            "isForeignKey": false,
            "foreignKeyTableId": null,
            "displaySequence": 20,
            "isCalculatedField": false,
            "calculatedFieldSQL": null
        },
        {...},
    ]
}

```

Returns a list of all custom entity fields.

##### Arguments

None

##### Returns

A dictionary with an items property that contains an array of up to limit custom entity fields, starting at index offset. Each entry in the array is a separate custom entity field. If no more custom entity fields are available, the resulting array will be empty. This request should never return an error.

#### Retrieve custom entity field metadata

```
DEFINITION
GET http://apiserver/customentities/:id/fieldmetadata

EXAMPLE REQUEST
$.get("http://localhost:49195/customentities/2228/fieldmetadata");

EXAMPLE RESPONSE
{[
    {
        "field": "Name",
        "title": "Pet's Name",
        "fieldType": "TXDSCTYPE",
        "isRequired": false,
        "sequence": 1,
        "width": "15em",
        "isForeignKey": false,
        "foreignKeyTableId": null,
        "foreignKeyEntityId": 0
    },
    {...}
]}

```

Retrieves the metadata details of an existing custom entity field. You need only supply the id.

##### Arguments

* id (required) - The id of the custom entity field metadata to be retrieved.

### Custom Entity Parent Values

#### Retrieve a custom entity parent value

```
DEFINITION
GET http://apiserver/customentityparents/:tableId/values/:recordId

EXAMPLE REQUEST
$.get("http://localhost:49195/customentityparents/CT/values/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "description": "Chloe"
}

```

Retrieves the details of an existing custom entity parent value. You need only supply the table id and record id.

##### Arguments

* tableId (required) - The tableId of the custom entity parent value to be retrieved.
* id (required) - The id of the custom entity parent value to be retrieved.

#### List all custom entity parent values

```
DEFINITION
GET http://apiserver/customentityparents/:tableId/values

EXAMPLE REQUEST
$.get("http://localhost:49195/customentityparents/CT/values");

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
            "description": "Chloe"
        },
        {...},
    ]
}

```

Returns a list of all custom entity parent values.

##### Arguments

* tableId (required) - the tableId of the custom entity parent value to be retrieved.
* recordId (optional) - the recordId with which to filter the list.
* description (optional) - the partial description with which to filter the list.

##### Returns

A dictionary with an items property that contains an array of up to limit custom entity parent values, starting at index offset. Each entry in the array is a separate custom entity parent value object. If no more custom entity parents are available, the resulting array will be empty. This request should never return an error.

### Custom Entity Parent Relationships

#### Create a custom entity parent relationship

```
DEFINITION
POST http://apiserver/customentities/:id/parentrelationships

EXAMPLE REQUEST
$.post("http://localhost:49195/customentities/354/parentrelationships", {
    "table": "B01",
    "sawId": "A0000001",
    "title": "Batch",
    "description": "Batch"
});

EXAMPLE RESPONSE
{
    "id": "355",
    "entity": "354",
    "table": "B01",
    "tableDescription": "Batches",
    "sawId": "A0000001",
    "sawIdDescription": "Account lookup module",
    "title": "Batch",
    "description": "Batch"
}

```

Creates a new custom entity parent relationship.

##### Arguments

* table (required) - parent table of the relationship
* sawId (required) - SAW Id specifies permission for the activity under the parent entity
* title (required) - Title of the activity under the parent entity
* description (required) - Description of the activity under the parent entity

##### Returns

Returns a custom entity parent relationship object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a custom entity parent relationship

```
DEFINITION
GET http://apiserver/customentities/:id/parentrelationships/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/customentities/354/parentrelationships/355");

EXAMPLE RESPONSE
{
    "id": "355",
    "entity": "354",
    "table": "B01",
    "tableDescription": "Batches",
    "sawId": "A0000001",
    "sawIdDescription": "Account lookup module",
    "title": "Batch",
    "description": "Batch"
}

```

Retrieves the details of an existing custom entity parent relationship. You need only supply the id.

##### Arguments

* id (required) - The id of the custom entity parent relationship to be retrieved.

#### Update a custom entity parent relationship

```
DEFINITION
POST http://apiserver/customentities/:id/parentrelationships/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/customentities/354/parentrelationships/355", {
    "sawId": "A0000002"
});

EXAMPLE RESPONSE
{
    "id": "355",
    "entity": "354",
    "table": "B01",
    "tableDescription": "Batches",
    "sawId": "A0000002",
    "sawIdDescription": "Batch processing module",
    "title": "Batch",
    "description": "Batch"
}


```

Updates the specified custom entity parent relationship by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* table (optional) - parent table of the relationship
* sawId (optional) - SAW Id specifies permission for the activity under the parent entity
* title (optional) - Title of the activity under the parent entity
* description (optional) - Description of the activity under the parent entity

##### Returns

Returns the custom entity parent relationship object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a custom entity parent relationship

```
DEFINITION
DELETE http://apiserver/customentities/:id/parentrelationships/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/customentities/354/parentrelationships/355", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a custom entity parent relationship. It cannot be undone.

##### Arguments

* id (required) - The id of the custom entity parent relationship to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the custom entity parent relationship does not exist, this call returns an error.

#### List all custom entity parent relationships

```
DEFINITION
GET http://apiserver/customentities/:id/parentrelationships

EXAMPLE REQUEST
$.get("http://localhost:49195/customentities/354/parentrelationships");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "355",
            "entity": "354",
            "table": "B01",
            "tableDescription": "Batches",
            "sawId": "A0000002",
            "sawIdDescription": "Batch processing module",
            "title": "Batch",
            "description": "Batch"
        },
        {...},
    ]
}

```

Returns a list of all custom entity parent relationships.

##### Arguments

no arguments available

##### Returns

A dictionary with an items property that contains an array of up to limit custom entity parent relationships, starting at index offset. Each entry in the array is a separate custom entity parent relationship object. If no more custom entity parent relationships are available, the resulting array will be empty. This request should never return an error.

#### List all custom entity row highlighting configurations

```
DEFINITION
GET http://apiserver/customentities/highlightingconfiguration

EXAMPLE REQUEST
$.get("http://localhost:49195/customentities/highlightingconfiguration");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "entity": 1662,
            "table": "AD",
            "field": "FollowUpDevice",
            "value": "PREM",
            "foregroundColor": "red",
            "backgroundColor": "blue"
        },
        {...},
    ]
}

```

Returns a list of all custom entity row highlighting configurations.

##### Returns

A dictionary with an items property that contains an array of up to limit custom entity row highlighting configurations, starting at index offset. Each entry in the array is a separate custom entity row highlighting configuration object. If no more custom entity row highlighting configurations are available, the resulting array will be empty. This request should never return an error.

### Data Types

#### Retrieve a data type

```
DEFINITION
GET http://apiserver/datatypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/datatypes/PRODAUTH");

EXAMPLE RESPONSE
{
    "id": "PRODAUTH",
    "description": "Product Author",
    "displaySequence": null,
    "isMultiValue": true,
    "labelDescription": "Product Author",
    "isUserDefined": true,
    "category": "INVENTORY",
    "isActive": true,
    "isDisplayableInStudioOnline": true,
    "isSearchableInStudioOnline": true,
    "dataType": "NOTE"
}

```

Retrieves the details of an existing data type. You need only supply the id.

##### Arguments

* id (required) - The id of the data type to be retrieved.

#### List all data types

```
DEFINITION
GET http://apiserver/datatypes

EXAMPLE REQUEST
$.get("http://localhost:49195/datatypes?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "PRODAUTH",
            "description": "Product Author",
            "displaySequence": null,
            "isMultiValue": true,
            "labelDescription": "Product Author",
            "isUserDefined": true,
            "category": "INVENTORY",
            "isActive": true,
            "isDisplayableInStudioOnline": true,
            "isSearchableInStudioOnline": true,
            "dataType": "NOTE"
        },
        {...},
    ]
}

```

Returns a list of all data types.

##### Arguments

* id () - Filter list by partial match in date type
* category () - Filter list by partial match in category
* dataType () - Filter list by partial match in dataType
* description () - Filter list by partial match in description
* isActive () - Filter list by whether active or not
* isMultiValue () - Filter list be whether multi-value or not
* isDisplayableInStudioOnline () - Filter list by whether marked as displayable in StudioOnline or not
* isSearchableInStudioOnline () - Filter list by whether marked as searchable in StudioOnline or not. Not currently used in datetypes or numbertypes, included because of common inheritance with codetypes and notetypes.

##### Returns

A dictionary with an items property that contains an array of up to limit data types, starting at index offset. Each entry in the array is a separate data type object. If no more data types are available, the resulting array will be empty. This request should never return an error.

### Date Types

#### Create a date type

```
DEFINITION
POST http://apiserver/datetypes

EXAMPLE REQUEST
$.post("http://localhost:49195/datetypes", {
    "id": "DDCINCEPT"
    "description": "Account Inception Date",
    "displaySequence": 184,
    "isMultiValue": false,
    "labelDescription": "Inception Date",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "DDCINCEPT",
    "description": "Account Inception Date",
    "displaySequence": 184,
    "isMultiValue": false,
    "labelDescription": "Inception Date",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "start": null,
    "end": null,
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Creates a new date type.

##### Arguments

* id (required) - The id of the date type.
* isMultiValue (required) - Whether the date type is a multi value date or not.
* isUserDefined (required) - Whether the date type is user defined or not.
* isActive (required) - Whether the date type is active or not.
* description (optional) - The description for the date type.
* displaySequence (optional) - The display sequence of the date type.
* labelDescription (optional) - The label description for the date type.
* category (optional) - The category of the date type.
* isDisplayableInStudioOnline (optional) - Indicates whether the date type is able to be displayed in StudioOnline.
* isSearchableInStudioOnline (optional) - Not currently used in datetypes, included because of common inheritance with codetypes and notetypes.

##### Returns

Returns a date type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a date type

```
DEFINITION
GET http://apiserver/datetypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/datetypes/DDCINCEPT");

EXAMPLE RESPONSE
{
    "id": "DDCINCEPT",
    "description": "Account Inception Date",
    "displaySequence": 184,
    "isMultiValue": false,
    "labelDescription": "Inception Date",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "start": null,
    "end": null,
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Retrieves the details of an existing date type. You need only supply the date type.

##### Arguments

* id (required) - The date type of the date type object to be retrieved.

##### Returns

Returns a date type object if a valid date type was provided.

#### Update a date type

```
DEFINITION
POST http://apiserver/datetypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/datetypes/DDCINCEPT", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "DDCINCEPT",
    "description": "Account Inception Date",
    "displaySequence": 184,
    "isMultiValue": false,
    "labelDescription": "Inception Date",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "start": null,
    "end": null,
    "isActive": false,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}


```

Updates the specified date type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* isMultiValue () - Whether the date type is a multi value date or not.
* isUserDefined () - Whether the date type is user defined or not.
* isActive () - Whether the date type is active or not.
* description () - The description for the date type.
* displaySequence () - The display sequence of the date type.
* labelDescription () - The label description for the date type.
* category () - The category of the date type.
* isDisplayableInStudioOnline () - Indicates whether the date type is able to be displayed in StudioOnline.
* isSearchableInStudioOnline () - Not currently used in datetypes, included because of common inheritance with codetypes and notetypes.

##### Returns

Returns the date type object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a date type

```
DEFINITION
DELETE http://apiserver/datetypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/datetypes/DDCINCEPT", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a date type. It cannot be undone.

##### Arguments

* id (required) - The id of the date type to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the date type does not exist, this call returns an error.

#### List all date types

```
DEFINITION
GET http://apiserver/datetypes

EXAMPLE REQUEST
$.get("http://localhost:49195/datetypes?isActive=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 155
    },
    "items": [
        {
            "id": "DDCINCEPT",
            "description": "Account Inception Date",
            "displaySequence": 184,
            "isMultiValue": false,
            "labelDescription": "Inception Date",
            "isUserDefined": false,
            "category": "ACCOUNT",
            "start": null,
            "end": null,
            "isActive": false,
            "isDisplayableInStudioOnline": false,
            "isSearchableInStudioOnline": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all date types matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in date type
* description () - Filter list by partial match in description
* category () - Filter list by partial match in category
* isActive () - Filter list by whether active or not
* isMultiValue () - Filter list be whether multi-value or not
* isDisplayableInStudioOnline () - Filter list by whether marked as displayable in StudioOnline or not
* isSearchableInStudioOnline () - Not currently used in datetypes, included because of common inheritance with codetypes and notetypes.

##### Returns

A dictionary with an items property that contains an array of up to limit date types, starting at index offset. Each entry in the array is a separate date type object. If no more date types are available, the resulting array will be empty. This request should never return an error.

### Date Type Attributes

#### Create a date type attribute

```
DEFINITION
POST http://apiserver/datetypes/:id/attributes

EXAMPLE REQUEST
$.post("http://localhost:49195/datetypes/age/attributes", {
    "type": "NUMBER",
    "value": "INTEGER",
    "description": null
});

EXAMPLE RESPONSE
{
    "id": "240",
    "type": "NUMBER",
    "value": "INTEGER",
    "description": null
}

```

Creates a new date type attribute object

##### Arguments

* type (required) - The type of the date type attribute.
* value (optional) - The value of the date type attribute.
* description (optional) - The description of the date type attribute.

##### Returns

Returns a date type attribute object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined datetype or invalid attribute type).

#### Retrieve a date type attribute

```
DEFINITION
GET http://apiserver/datetypes/:id/attributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/datetypes/age/attributes/240");

EXAMPLE RESPONSE
{
    "id": "240",
    "type": "NUMBER",
    "value": "INTEGER",
    "description": null
}

```

Retrieves the details of an existing date type attribute. You need only supply the datetype id and date type attribute id.

##### Returns

Returns a date type attribute object if a valid id was provided.

#### Update a date type attribute

```
DEFINITION
POST http://apiserver/datetypes/:id/attributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/datetypes/age/attributes/240", {
    "description": "Represents age"
});

EXAMPLE RESPONSE
{
    "id": "240",
    "type": "NUMBER",
    "value": "INTEGER",
    "description": "Represents age"
}

```

Updates the specified date type attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of the date type attribute.
* value (optional) - The value of the date type attribute.
* description (optional) - The description of the date type attribute.

##### Returns

Returns the date type attribute object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined datetype or invalid attribute type).

#### Delete a date type attribute

```
DEFINITION
DELETE http://apiserver/datetypes/:id/attributes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/datetypes/age/attributes/240", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a date type attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the date type attribute to be deleted.

##### Returns

Returns a 204 No Content response on success. If the date type attribute id does not exist, this call returns an error.

#### List all date type attributes

```
DEFINITION
GET http://apiserver/datetypes/:id/attributes

EXAMPLE REQUEST
$.get("http://localhost:49195/datetypes/age/attributes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "240",
            "type": "NUMBER",
            "value": "INTEGER",
            "description": "Represents age"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all date type attributes.

##### Returns

A dictionary with an items property that contains an array of up to limit date type attributes, starting at index offset. Each entry in the array is a separate date type attribute object. If no more date type attributes are available, the resulting array will be empty. This request should never return an error.

### Date Type Range Limits

#### Create a date type range limit

```
DEFINITION
POST http://apiserver/datetypes/:id/rangelimits

EXAMPLE REQUEST
$.post("http://localhost:49195/datetypes/ANNIV/rangelimits", {
    "dateLow": "1900-01-01",
    "dateHigh": "2020-12-31
});

EXAMPLE RESPONSE
{
    "id":"43",
    "dateLow":"1900-01-01",
    "dateHigh":"2020-12-31"
}

```

Creates a new date type range limit object

##### Arguments

* dateLow (required) - The low date of the date type range limit.
* dateHigh (required) - The high date of the date type range limit.

##### Returns

Returns a date type range limit object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined datetype or invalid range limit type).

#### Retrieve a date type range limit

```
DEFINITION
GET http://apiserver/datetypes/:id/rangelimits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/datetypes/ANNIV/rangelimits/43");

EXAMPLE RESPONSE
{
    "id":"43",
    "dateLow":"1900-01-01",
    "dateHigh":"2020-12-31"
}

```

Retrieves the details of an existing date type range limit. You need only supply the datetype id and date type range limit id.

##### Returns

Returns a date type range limit object if a valid id was provided.

#### Update a date type range limit

```
DEFINITION
POST http://apiserver/datetypes/:id/rangelimits/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/datetypes/ANNIV/rangelimits/43", {
    "dateHigh": "2050-12-31"
});

EXAMPLE RESPONSE
{
    "id":"43",
    "dateLow":"1900-01-01",
    "dateHigh":"2050-12-31"
}

```

Updates the specified date type range limit by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* dateLow () - The low date of the date type range limit.
* dateHigh () - The high date of the date type range limit.

##### Returns

Returns the date type range limit object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined datetype or invalid range limit type).

#### Delete a date type range limit

```
DEFINITION
DELETE http://apiserver/datetypes/:id/rangelimits/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/datetypes/ANNIV/rangelimits/43", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a date type range limit. It cannot be undone.

##### Arguments

* id (required) - The id of the date type range limit to be deleted.

##### Returns

Returns a 204 No Content response on success. If the date type range limit id does not exist, this call returns an error.

#### List all date type range limits

```
DEFINITION
GET http://apiserver/datetypes/:id/rangelimits

EXAMPLE REQUEST
$.get("http://localhost:49195/datetypes/ANNIV/rangelimits");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id":"43",
            "dateLow":"1900-01-01",
            "dateHigh":"2050-12-31"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all date type range limit.

##### Returns

A dictionary with an items property that contains an array of up to limit date type range limits, starting at index offset. Each entry in the array is a separate date type range limit object. If no more date type range limits are available, the resulting array will be empty. This request should never return an error.

### Demographics

#### Create a demographic

```
DEFINITION
POST http://apiserver/demographics

EXAMPLE REQUEST
$.post("http://localhost:49195/demographics", {
    "sectionCode": "CHURCH",
    "type": "DDCGENDER",
    "soLabel": "Gender:",
    "soControlType": "DROPDOWN",
    "displaySequence": 10,
    "isRequired": false,
    "ecStoreId": null,
    "isActive": true,
    "soDefaultValue": "U"
});

EXAMPLE RESPONSE
{
    "id": "10018",
    "sectionCode": "CHURCH",
    "dataType": "X04",
    "dataTypeDescription": "CODE",
    "type": "DDCGENDER",
    "typeDescription": "Gender",
    "soLabel": "Gender:",
    "soControlType": "DROPDOWN",
    "displaySequence": 10,
    "isRequired": false,
    "ecStoreId": null,
    "isActive": true,
    "demographicCode": "DM7582EA32",
    "soDefaultValue": "U"
}

```

Creates a new demographic.

##### Arguments

* sectionCode (required) - Section Code
* type (required) - Type
* soLabel (requried) - Studio Online Label
* soControlType (required) - Studio Online Control Type
* displaySequence (required) - Display Sequence
* isRequired (required) - Required Indicator
* ecStoreId () - Specific Studio Online Store Id
* isActive (required) - Active Indicator
* soDefaultValue (conditional) - Studio Online Default Value

##### Returns

Returns a demographic object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a demographic

```
DEFINITION
GET http://apiserver/demographics/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/demographics/10018");

EXAMPLE RESPONSE
{
    "id": "10018",
    "sectionCode": "CHURCH",
    "dataType": "X04",
    "dataTypeDescription": "CODE",
    "type": "DDCGENDER",
    "typeDescription": "Gender",
    "soLabel": "Gender:",
    "soControlType": "DROPDOWN",
    "displaySequence": 10,
    "isRequired": false,
    "ecStoreId": null,
    "isActive": true,
    "demographicCode": "DM7582EA32",
    "soDefaultValue": "U"
}

```

Retrieves the details of an existing demographic. You need only supply the id.

##### Arguments

* id (required) - The id of the demographic to be retrieved.

#### Update a demographic

```
DEFINITION
POST http://apiserver/demographics/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/demographics/10018", {
    "sectionCode": "CHURCH",
    "type": "DDCGENDER",
    "soLabel": "Gender:",
    "soControlType": "DROPDOWN",
    "displaySequence": 10,
    "isRequired": false,
    "ecStoreId": null,
    "isActive": true,
    "soDefaultValue": "U"
});

EXAMPLE RESPONSE
{
    "id": "10018",
    "sectionCode": "CHURCH",
    "dataType": "X04",
    "dataTypeDescription": "CODE",
    "type": "DDCGENDER",
    "typeDescription": "Gender",
    "soLabel": "Gender:",
    "soControlType": "DROPDOWN",
    "displaySequence": 10,
    "isRequired": false,
    "ecStoreId": null,
    "isActive": true,
    "demographicCode": "DM7582EA32",
    "soDefaultValue": "U"
}


```

Updates the specified demographic by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sectionCode () - Section Code
* type () - Type
* soLabel () - Studio Online Label
* soControlType () - Studio Online Control Type
* displaySequence () - Display Sequence
* isRequired () - Required Indicator
* ecStoreId () - Specific Studio Online Store Id
* isActive () - Active Indicator
* soDefaultValue () - Studio Online Default Value

##### Returns

Returns the demographic object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a demographic

```
DEFINITION
DELETE http://apiserver/demographics/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/demographics/10018", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a demographic. It cannot be undone.

##### Arguments

* id (required) - The id of the demographic to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the demographic does not exist, this call returns an error.

#### List all demographics

```
DEFINITION
GET http://apiserver/demographics

EXAMPLE REQUEST
$.get("http://localhost:49195/demographics?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10018",
            "sectionCode": "CHURCH",
            "dataType": "X04",
            "dataTypeDescription": "CODE",
            "type": "DDCGENDER",
            "typeDescription": "Gender",
            "soLabel": "Gender:",
            "soControlType": "DROPDOWN",
            "displaySequence": 10,
            "isRequired": false,
            "ecStoreId": null,
            "isActive": true,
            "demographicCode": "DM7582EA32",
            "soDefaultValue": "U"
        },
        {...},
    ]
}

```

Returns a list of all demographics.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Record Id
* demographicCode () - Demographic Code
* sectionCode () - Section Code
* type () - Type
* soLabel (requried) - Studio Online Label
* soControlType () - Studio Online Control Type
* ecStoreId () - Specific Studio Online Store Id
* isActive () - Active Indicator

##### Returns

A dictionary with an items property that contains an array of up to limit demographics, starting at index offset. Each entry in the array is a separate demographic object. If no more demographics are available, the resulting array will be empty. This request should never return an error.

### Demographic Notes

#### Create a demographic note

```
DEFINITION
POST http://apiserver/demographics/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/demographics/3/notes", {
    "type": "ADDRSTDMSG",
    "shortComment": "Use Standard Address",
    "longComment": "Our records indicate that there is a closer match for your address in the USPS database. Would you like to use it?"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "ADDRSTDMSG",
    "typeDescription": "Address Standardization Response Msg",
    "shortComment": "Use Standard Address",
    "longComment": "Our records indicate that there is a closer match for your address in the USPS database. Would you like to use it?"
}

```

Creates a new demographic note.

##### Arguments

* type (required) - Note Type
* shortComment () - Short Comment
* longComment () - Long Comment

##### Returns

Returns a demographic note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a demographic note

```
DEFINITION
GET http://apiserver/demographics/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/demographics/3/notes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "ADDRSTDMSG",
    "typeDescription": "Address Standardization Response Msg",
    "shortComment": "Use Standard Address",
    "longComment": "Our records indicate that there is a closer match for your address in the USPS database. Would you like to use it?"
}

```

Retrieves the details of an existing demographic note. You need only supply the id.

##### Arguments

* id (required) - The id of the demographic note to be retrieved.

#### Update a demographic note

```
DEFINITION
POST http://apiserver/demographics/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/demographics/3/notes/1", {
    "type": "ADDRSTDMSG",
    "shortComment": "Use Standard Address",
    "longComment": "Our records indicate that there is a closer match for your address in the USPS database. Would you like to use it?"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "ADDRSTDMSG",
    "typeDescription": "Address Standardization Response Msg",
    "shortComment": "Use Standard Address",
    "longComment": "Our records indicate that there is a closer match for your address in the USPS database. Would you like to use it?"
}


```

Updates the specified demographic note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type () - Note Type
* shortComment () - Short Comment
* longComment () - Long Comment

##### Returns

Returns the demographic note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a demographic note

```
DEFINITION
DELETE http://apiserver/demographics/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/demographics/3/notes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a demographic note. It cannot be undone.

##### Arguments

* id (required) - The id of the demographic note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the demographic note does not exist, this call returns an error.

#### List all demographic notes

```
DEFINITION
GET http://apiserver/demographics/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/demographics/3/notes?");

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
            "type": "ADDRSTDMSG",
            "typeDescription": "Address Standardization Response Msg",
            "shortComment": "Use Standard Address",
            "longComment": "Our records indicate that there is a closer match for your address in the USPS database. Would you like to use it?"
        },
        {...},
    ]
}

```

Returns a list of all demographic notes.

##### Arguments

* demographicId (required) - Id for the Demographic

##### Returns

A dictionary with an items property that contains an array of up to limit demographic notes, starting at index offset. Each entry in the array is a separate demographic note object. If no more demographic notes are available, the resulting array will be empty. This request should never return an error.

### Letter codes

#### Create a letter code

```
DEFINITION
POST http://apiserver/lettercodes

EXAMPLE REQUEST
$.post("http://localhost:49195/lettercodes", {
    "id": "0613APPL",
    "description": "June 13 Appeal",
    "canCombine": true,
    "instructions": null,
    "completionTextProcessing": "NONE",
    "completionText": null,
    "department": null,
    "author": null,
    "topic": null,
    "category": null,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "0613APPL",
    "description": "June 13 Appeal",
    "canCombine": true,
    "instructions": null,
    "completionTextProcessing": "NONE",
    "completionText": null,
    "department": null,
    "author": null,
    "topic": null,
    "category": null,
    "isActive": true
}

```

Creates a new letter code.

##### Arguments

* id (required) - letter code
* description (required)
* canCombine (optional)
* instructions (optional)
* completionTextProcessing (optional)
* completionText (optional)
* department (optional)
* author (optional)
* topic (optional)
* category (optional)
* isActive (optional)

##### Returns

Returns a letter code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a letter code

```
DEFINITION
GET http://apiserver/lettercodes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/lettercodes/0613APPL");

EXAMPLE RESPONSE
{
    "id": "0613APPL",
    "description": "June 13 Appeal",
    "canCombine": true,
    "instructions": null,
    "completionTextProcessing": "NONE",
    "completionText": null,
    "department": null,
    "author": null,
    "topic": null,
    "category": null,
    "isActive": true
}

```

Retrieves the details of an existing letter code. You need only supply the id.

##### Arguments

* id (required) - The id of the letter code to be retrieved.

#### Update a letter code

```
DEFINITION
POST http://apiserver/lettercodes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/lettercodes/0613APPL", {
    "canCombine": false
});

EXAMPLE RESPONSE
{
    "id": "0613APPL",
    "description": "June 13 Appeal",
    "canCombine": false,
    "instructions": null,
    "completionTextProcessing": "NONE",
    "completionText": null,
    "department": null,
    "author": null,
    "topic": null,
    "category": null,
    "isActive": true
}


```

Updates the specified letter code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional)
* description (optional)
* canCombine (optional)
* instructions (optional)
* completionTextProcessing (optional)
* completionText (optional)
* department (optional)
* author (optional)
* topic (optional)
* category (optional)
* isActive (optional)

##### Returns

Returns the letter code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a letter code

```
DEFINITION
DELETE http://apiserver/lettercodes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/lettercodes/0613APPL", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a letter code. It cannot be undone.

##### Arguments

* id (required) - The id of the letter code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the letter code does not exist, this call returns an error.

#### List all letter codes

```
DEFINITION
GET http://apiserver/lettercodes

EXAMPLE REQUEST
$.get("http://localhost:49195/lettercodes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 58
    },
    "items": [
        {
            "id": "DEF",
            "description": "Defective Products Letter",
            "canCombine": false,
            "instructions": null,
            "completionTextProcessing": "FILL",
            "completionText": "List the product(s) that were defective and returned.",
            "department": "DS",
            "author": null,
            "topic": null,
            "category": null,
            "isActive": true,
            "formType": "LETTER"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all letter codes matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in letter code
* category () - Filter list by partial match in category
* completionText () - Filter list by partial match in completion text
* description () - Filter list by partial match in description
* isActive () - Filter list by whether active or not
* topic () - Filter list by partial match in topic
* formType () - Filter list by partial match in form type.

##### Returns

A dictionary with an items property that contains an array of up to limit letter codes, starting at index offset. Each entry in the array is a separate letter code object. If no more letter codes are available, the resulting array will be empty. This request should never return an error.

### Letter Code Attributes

#### Create a letter code attribute

```
DEFINITION
POST http://apiserver/lettercodes/:id/attributes

EXAMPLE REQUEST
$.post("http://localhost:49195/lettercodes/DRTY01/attributes", {
    "type": "NONCASH",
    "value": "NONCASHFRM"
});

EXAMPLE RESPONSE
{
    "id": "97",
    "letterCode": "DRTY01",
    "type": "NONCASH",
    "typeDescription": "Override Form Communication Type",
    "value": "NONCASHFRM",
    "valueDescription": "Non Cash Gift"
}

```

Creates a new letter code attribute.

##### Arguments

* type (required) - The attribute type
* value (required) - The attribute value

##### Returns

Returns a letter code attribute object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a letter code attribute

```
DEFINITION
GET http://apiserver/lettercodes/:id/attributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/lettercodes/DRTY01/attributes/97");

EXAMPLE RESPONSE
{
    "id": "97",
    "letterCode": "DRTY01",
    "type": "NONCASH",
    "typeDescription": "Override Form Communication Type",
    "value": "NONCASHFRM",
    "valueDescription": "Non Cash Gift"
}

```

Retrieves the details of an existing letter code attribute. You need only supply the id.

##### Arguments

* id (required) - The id of the letter code attribute to be retrieved.

#### Update a letter code attribute

```
DEFINITION
POST http://apiserver/lettercodes/:id/attributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/lettercodes/DRTY01/attributes/97", {
    "value": "FRMTYPNCGF"
});

EXAMPLE RESPONSE
{
    "id": "97",
    "letterCode": "DRTY01",
    "type": "NONCASH",
    "typeDescription": "Override Form Communication Type",
    "value": "FRMTYPNCGF",
    "valueDescription": "Non Cash Gift"
}


```

Updates the specified letter code attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional)
* value (optional)

##### Returns

Returns the letter code attribute object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a letter code attribute

```
DEFINITION
DELETE http://apiserver/lettercodes/:id/attribute/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/lettercodes/DRTY01/attributes/97", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a letter code attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the letter code attribute to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the letter code attribute does not exist, this call returns an error.

#### List all letter code attributes

```
DEFINITION
GET http://apiserver/lettercodes/:id/attributes

EXAMPLE REQUEST
$.get("http://localhost:49195/lettercodes/DRTY01/attributes");

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
            "letterCode": "DRTY01",
            "type": "NONCASH",
            "typeDescription": "Override Form Communication Type",
            "value": "NONCASHFRM",
            "valueDescription": "Non Cash Gift"
        },
        { ... }
    ]
}

```

Returns a list of all letter code attributes.

##### Arguments

No arguments available

##### Returns

A dictionary with an items property that contains an array of up to limit letter code attributes, starting at index offset. Each entry in the array is a separate letter code attribute object. If no more letter code attributes are available, the resulting array will be empty. This request should never return an error.

### Documents

#### Create a document

```
DEFINITION
POST http://apiserver/documents

EXAMPLE REQUEST
$.post("http://localhost:49195/documents", {
    "documentCode": "GENDOC",
    "type": "GENERAL",
    "name": "General Document",
    "url": "P://Documents/Shared/GeneralDocument.txt"
    "sequence": 5
});

EXAMPLE RESPONSE
{
    "id": "5",
    "documentCode": "GENDOC",
    "type": "GENERAL",
    "name": "General Document",
    "summary": null,
    "description": null,
    "sequence": 5,
    "url": "P://Documents/Shared/GeneralDocument.txt",
    "isActive": true,
    "useInStudioOnline": false
}

```

Creates a new document.

##### Arguments

* documentCode (required) - The document code for the new document.
* type (required) - The document type code value for the new document.
* name (required) - The document name to be used for the new document.
* summary (optional) - The document summary to be used for the new document.
* description (optional) - The description to be used for the new document.
* sequence (required) - The display sequence to be used for the new document.
* url (required) - The URL or external document address to be used for the new document.
* isActive (optional: defaults to true) - Should the new document be marked as active.
* useInStudioOnline (optional: defaults to false) - Should the new document be used in StudioOnline.

##### Returns

Returns a document object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a document

```
DEFINITION
GET http://apiserver/documents/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/documents/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "documentCode": "GENDOC",
    "type": "GENERAL",
    "name": "General Document",
    "summary": null,
    "description": null,
    "sequence": 5,
    "url": "P://Documents/Shared/GeneralDocument.txt",
    "isActive": true,
    "useInStudioOnline": false
}

```

Retrieves the details of an existing document. You need only supply the id.

##### Arguments

* id (required) - The id of the document to be retrieved.

#### Update a document

```
DEFINITION
POST http://apiserver/documents/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/documents/5", {
    "summary": "A general document."
});

EXAMPLE RESPONSE
{
    "id": "5",
    "documentCode": "GENDOC",
    "type": "GENERAL",
    "name": "General Document",
    "summary": "A general document.",
    "description": null,
    "sequence": 5,
    "url": "P://Documents/Shared/GeneralDocument.txt",
    "isActive": true,
    "useInStudioOnline": false
}

```

Updates the specified document by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* documentCode (optional) - The document code value to update the document with.
* type (optional) - The document type code value to update the document with.
* name (optional) - The document name to be used to update the document with.
* summary (optional) - The document summary to be used to update the document with.
* description (optional) - The description to be used to update the document with.
* sequence (optional) - The display sequence to be used to update the document with.
* url (optional) - The URL or external document address to be used to update the document with.
* isActive (optional) - Should the document be marked as active.
* useInStudioOnline (optional) - Should the ocument be used in StudioOnline.

##### Returns

Returns the document object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a document

```
DEFINITION
DELETE http://apiserver/documents/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/documents/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a document. It cannot be undone.

##### Arguments

* id (required) - The id of the document to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the document does not exist, this call returns an 404 Not Found error. If the document has dependent Advanced Studio Online configurations, this call returns a 409 Conflict error.

#### List all documents

```
DEFINITION
GET http://apiserver/documents

EXAMPLE REQUEST
$.get("http://localhost:49195/documents?type=GENERAL");

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
            "documentCode": "GENDOC",
            "type": "GENERAL",
            "name": "General Document",
            "summary": null,
            "description": null,
            "sequence": 5,
            "url": "P://Documents/Shared/GeneralDocument.txt",
            "isActive": true,
            "useInStudioOnline": false
        },
        {...},
    ]
}

```

Returns a list of all documents.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* documentCode (optional) - The document code to filter results on.
* type (optional) - The document type code value to filter results on.
* name (optional) - The document name to be used to filter results on.
* summary (optional) - The document summary to be used to filter results on.
* description (optional) - The description to be used to filter results on.
* url (optional) - The URL or external document address to be used to filter results on.
* isActive (optional) - Should the document be marked as active.
* useInStudioOnline (optional) - Should the ocument be used in StudioOnline.

##### Returns

A dictionary with an items property that contains an array of up to limit documents, starting at index offset. Each entry in the array is a separate document object. If no more documents are available, the resulting array will be empty. This request should never return an error.

### Document Advanced StudioOnline Configuration

#### Create a document Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/documents/:id/storeconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/documents/5/storeconfigurations", {
    "storeRecordId": "19",
    "isPublished": true,
    "startDate": "2019-01-01",
    "endDate": "2019-10-05"
    "title": "General Document",
    "description": "General Document",
    "summary": "General Document"
});

EXAMPLE RESPONSE
{
    "id": "15132",
    "documentCode": "5",
    "storeRecordId": "19",
    "storeDescription": "ASO US-English",
    "isPublished": true,
    "startDate": "2019-01-01",
    "endDate": "2019-10-05",
    "title": "General Document",
    "description": "General Document",
    "summary": "General Document"
}

```

Creates a new document Advanced StudioOnline configuration.

##### Arguments

* store (required) - The unique id of the store this configuration is for. Must be a valid store Id.
* isPublished (optional)- Whether the document should be used in the specified store.
* startDate (optional) - The date the document will become visible in the specified store.
* endDate (optional) - The date the document will be removed from the specified store.
* title (required) - The online title for the document when used in the specified store. {Max Length (900)}
* description (optional) - The online description for the document when used in the specified store.
* summary (optional) - The online summary for the document when used in the specified store. {Max Length (70)}

##### Returns

Returns a document Advanced StudioOnline configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a document Advanced StudioOnline configuration

```
DEFINITION
GET http://apiserver/documents/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/documents/5/storeconfigurations/15132");

EXAMPLE RESPONSE
{
    "id": "15132",
    "documentCode": "5",
    "storeRecordId": "19",
    "storeDescription": "ASO US-English",
    "isPublished": true,
    "startDate": "2019-01-01",
    "endDate": "2019-10-05",
    "title": "General Document",
    "description": "General Document",
    "summary": "General Document"
}

```

Retrieves the details of a document Advanced StudioOnline configuration. You need only supply the document id and configuration id.

##### Returns

Returns a document Advanced StudioOnline configuration object if valid ids were provided.

#### Update a document Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/documents/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/documents/5/storeconfigurations/15132", {
    "startDate": "2018-12-15",
    "endDate": "2019-10-15"
});

EXAMPLE RESPONSE
{
    "id": "15132",
    "documentCode": "5",
    "storeRecordId": "19",
    "storeDescription": "ASO US-English",
    "isPublished": true,
    "startDate": "2018-12-15",
    "endDate": "2019-10-15",
    "title": "General Document",
    "description": "General Document",
    "summary": "General Document"
}


```

Updates the specified document Advanced StudioOnline configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* store (optional) - The unique id of the store this configuration is for. Must be a valid store Id.
* isPublished (optional)- Whether the document should be used in the specified store.
* startDate (optional) - The date the document will become visible in the specified store.
* endDate (optional) - The date the document will be removed from the specified store.
* title (optional) - The online title for the document when used in the specified store. {Max Length (900)}
* description (optional) - The online description for the document when used in the specified store.
* summary (optional) - The online summary for the document when used in the specified store. {Max Length (70)}

##### Returns

Returns a document Advanced StudioOnline configuration object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid permanentRedirect).

#### Delete a document Advanced StudioOnline configuration

```
DEFINITION
DELETE http://apiserver/documents/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/documents/5/storeconfigurations/15132", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a document Advanced StudioOnline configuration. It cannot be undone.

##### Arguments

* id (required) - The document Advanced StudioOnline configuration id of the configuration to be deleted.

##### Returns

Returns a 204 No Content response on success. If the document Advanced StudioOnline configuration does not exist, this call returns an error.

#### List all document Advanced StudioOnline configurations

```
DEFINITION
GET http://apiserver/documents/:id/storeconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/documents/5/storeconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "15132",
            "documentCode": "5",
            "storeRecordId": "19",
            "storeDescription": "ASO US-English",
            "isPublished": true,
            "startDate": "2018-12-15",
            "endDate": "2019-10-15",
            "title": "General Document",
            "description": "General Document",
            "summary": "General Document"
        }
        {...},
        {...}
    ]
}

```

Returns a list of all document Advanced StudioOnline configurations matching the provided filter criteria.

##### Arguments

* document () - Filter list by an exact match in document code

##### Returns

A dictionary with an items property that contains an array of up to limit document Advanced StudioOnline configurations, starting at index offset. Each entry in the array is a separate document Advanced StudioOnline configuration object. If no more document Advanced StudioOnline configurations are available, the resulting array will be empty. This request should never return an error.

### Document Attributes

#### Create a document attribute

```
DEFINITION
POST http://apiserver/documents/:documentId/attributes

EXAMPLE REQUEST
$.post("http://localhost:49195/documents/5/attributes", {
    "type": "DDCROLE",
    "value": "CHURCH"
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "DDCROLE",
    "value": "CHURCH",
    "isActive": true,
    "comment": null,
    "description": null
}

```

Creates a new document attribute.

##### Arguments

* type (required) - The type to create the document attribute with.
* value (required) - The value to create the document attribute with.
* isActive (optional: defaults to true) - Should the new document attribute be active.
* comment (optional) - The comment to create the document attribute with.
* description (optional) - The description to create the document attribute with.

##### Returns

Returns a document attribute object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a document attribute

```
DEFINITION
GET http://apiserver/documents/:documentId/attributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/documents/5/attributes/4");

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "DDCROLE",
    "value": "CHURCH",
    "isActive": true,
    "comment": null,
    "description": null
}

```

Retrieves the details of an existing document attribute. You need only supply the id.

##### Arguments

* id (required) - The id of the document attribute to be retrieved.

#### Update a document attribute

```
DEFINITION
POST http://apiserver/documents/:documentId/attributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/documents/5/attributes/4", {
    "type": "DDCORG"
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "DDCORG",
    "value": "CHURCH",
    "isActive": true,
    "comment": null,
    "description": null
}

```

Updates the specified document attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type to update the document attribute with.
* value (optional) - The value to update the document attribute with.
* isActive (optional) - Should the document attribute be active.
* comment (optional) - The comment to update the document attribute with
* description (optional) - The description to update the document attribute with

##### Returns

Returns the document attribute object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a document attribute

```
DEFINITION
DELETE http://apiserver/documents/:documentId/attributes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/documents/5/attributes/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a document attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the document attribute to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the document attribute does not exist, this call returns an error.

#### List all document attributes

```
DEFINITION
GET http://apiserver/documents/:documentId/attributes

EXAMPLE REQUEST
$.get("http://localhost:49195/documents/5/attributes");

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
            "type": "DDCROLE",
            "value": "CHURCH",
            "isActive": true,
            "comment": null,
            "description": null
        },
        {...},
    ]
}

```

Returns a list of all document attributes.

##### Returns

A dictionary with an items property that contains an array of up to limit document attributes, starting at index offset. Each entry in the array is a separate document attribute object. If no more document attributes are available, the resulting array will be empty. This request should never return an error.

### Email Folder Sync

#### Create an email folder sync

```
DEFINITION
POST http://apiserver/accessors/:id/emailfolders

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/emailfolders", {
    "folderName": "INBOX",
    "processType": "READ",
    "trackingLevel": "CATEGORY",
    "createEmailOnlyAccounts": false
});

EXAMPLE RESPONSE
{
    "id": "8",
    "accessor": "1234",
    "user": "ddc\\jdoe",
    "emailAddress": "johndoe@donordirect.com",
    "folderName": "INBOX",
    "processType": "READ",
    "trackingLevel": "CATEGORY",
    "createEmailOnlyAccounts": false,
    "lastSyncVersion": "1111",
    "lastSyncDate": "2016-01-01"
}

```

Creates a new email folder sync for email tracking.

##### Arguments

* id (required) - The unique id of the accessor to create the folder sync for.
* folderName (required) - The name of the email folder.
* processType - Determines if the sync should track ANY email or only READ emails.
* trackingLevel - Determines if the sync should track ALL accounts, accounts ASSIGNED to accessor, accounts assigned to access in same functional CATEGORY.
* createEmailOnlyAccounts - If the sync tracks an email for an email address that is not currently on any account, should it create a new account. (This is only respected for inbound emails.)

##### Returns

Returns an email folder sync object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined id).

#### Retrieve an email folder sync

```
DEFINITION
GET http://apiserver/accessors/:id/emailsfolders/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/emailfolders/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "accessor": "1234",
    "user": "ddc\\jdoe",
    "emailAddress": "johndoe@donordirect.com",
    "folderName": "INBOX",
    "processType": "READ",
    "trackingLevel": "CATEGORY",
    "createEmailOnlyAccounts": false,
    "lastSyncVersion": "1111",
    "lastSyncDate": "2016-01-01"
}

```

Retrieves the details of an email folder sync.

##### Arguments

* id (required) - The id of the email folder sync

#### Update an email folder sync

```
DEFINITION
POST http://apiserver/accessors/:id/emailfolders/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/emailfolders/8", {
    "processType": "ANY",
});

EXAMPLE RESPONSE
{
    "id": "8",
    "accessor": "1234",
    "user": "ddc\\jdoe",
    "emailAddress": "johndoe@donordirect.com",
    "folderName": "INBOX",
    "processType": "ANY",
    "trackingLevel": "CATEGORY",
    "createEmailOnlyAccounts": false,
    "lastSyncVersion": "1111",
    "lastSyncDate": "2016-01-01"
}

```

Updates an email folder sync.

##### Arguments

* folderName - The name of the email folder.
* processType - Determines if the sync should track ANY email or only READ emails.
* trackingLevel - Determines if the sync should track ALL accounts, accounts ASSIGNED to accessor, accounts assigned to access in same functional CATEGORY.
* createEmailOnlyAccounts - If the sync tracks an email for an email address that is not currently on any account, should it create a new account.

##### Returns

Returns an email folder sync object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an email folder sync

```
DEFINITION
DELETE http://apiserver/accessors/:accessorid/emailfolders/:emailfolderid

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/1234/emailfolders/8");

EXAMPLE RESPONSE
204 No Content

```

Deletes an email folder sync.

##### Arguments

* accessorid (required) - The unique id of the accessor that owns the email folder.
* emailfolderid (required) - The id of the email folder sync

##### Returns

Returns a 204 No Content response on success. If the email folder does not exist, this call returns an error.

#### List all email folder syncs

```
DEFINITION
GET http://apiserver/accessors/:id/emailfolders

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234/emailfolders", {
    "user": "ddc\\jdoe",
    "isExactMatch": true
});

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
            "accessor": "1234",
            "user": "ddc\\jdoe",
            "emailAddress": "johndoe@donordirect.com",
            "folderName": "INBOX",
            "processType": "READ",
            "trackingLevel": "CATEGORY",
            "createEmailOnlyAccounts": false,
            "lastSyncVersion": "1111",
            "lastSyncDate": "2016-01-01"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all email folder sync matching the provided filter criteria.

##### Arguments

* accessorid (required) - Filter list by match on accessor
* user - Filter list by partial match on user
* emailAddress - Filter list by match on email address
* folderName - Filter list by match on folder name
* processType - Filter list by exact match on process type
* trackingLevel - Filter list by exact match on tracking level
* createEmailOnlyAccounts - Filter list by whether the folder sync should create email only accounts
* isExactMatch - Determines if the user, email address, folder name fields should be an exact match or fuzzy match

##### Returns

A dictionary with an items property that contains an array of up to limit email folder sync objects, starting at index offset. Each entry in the array is a separate email folder sync object. If no more email folder sync are available, the resulting array will be empty. This request should never return an error.

### Email Templates

#### Create an email template

```
DEFINITION
POST http://apiserver/emailtemplates

EXAMPLE REQUEST
$.post("http://localhost:49195/emailtemplates", {
    "entity": "A01",
    "description": "New Account Thank You Email",
    "functionalCategory": "DM",
    "selectionCriteria": [],
    "emailSubject": "Thank you for your kind donation",
    "emailBody": "{FirstName},\n\nThank you for your donation.",
    "topic": "THANKYOU",
    "category": "DONATION",
    "formType": null
});

EXAMPLE RESPONSE
{
    "id": "5",
    "entity": "A01",
    "entityDescription": "Account Master",
    "description": "New Account Thank You Email",
    "isSystemTemplate": true,
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Donor Ministries",
    "sawId": "AAT23EMA",
    "sawIdDescription": "Account Emails Activity",
    "accessor": null,
    "accessorName": null,
    "selectionCriteria": null,
    "emailSubject": "Thank you for your kind donation",
    "emailBody": "{FirstName},\n\nThank you for your donation.",
    "topic": "THANKYOU",
    "topicDescription": "A thank you email for the donor",
    "category": "DONATION",
    "categoryDescription": "Donation templates",
    "formType": null,
    "formTypeDescription": null
}

```

Creates a new email template.

##### Arguments

* entity (required): base entity associated with the email template
* description (): description of the email template
* isSystemTemplate (required): true if creating a system email template, false if creating a user/accessor email template
* functionalCategory (): Functional category associated with this email template
* sawId (conditionally required): if isSystemTemplate is true, the sawId needed to use this email template is required (accessor is ignored)
* accessor (conditionally required): if isSystemTemplate is false, the accessor who owns the email template is required (sawId is ignored)
* emailSubject (required): email template subject
* emailBody (required): email template body
* selectionCriteria: an array of entities joined to 'entity' which are reqired for any merge text contained in the template
* topic (optional): a topic code for the email template
* category (optional): a category code for the email template
* formType (conditionally required): if type is `RECEIPTS`, the Form Type from which to retrieve merge fields

##### Returns

Returns a email template object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an email template

```
DEFINITION
GET http://apiserver/emailtemplates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/emailtemplates/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "entity": "A01",
    "entityDescription": "Account Master",
    "description": "New Account Thank You Email",
    "isSystemTemplate": true,
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Donor Ministries",
    "sawId": "AAT23EMA",
    "sawIdDescription": "Account Emails Activity",
    "accessor": null,
    "accessorName": null,
    "selectionCriteria": null,
    "emailSubject": "Thank you for your kind donation",
    "emailBody": "{FirstName},\n\nThank you for your donation.",
    "topic": "THANKYOU",
    "topicDescription": "A thank you email for the donor",
    "category": "DONATION",
    "categoryDescription": "Donation templates",
    "formType": null,
    "formTypeDescription": null
}

```

Retrieves the details of an existing email template. You need only supply the id.

##### Arguments

* id (required) - The id of the email template to be retrieved.

#### Update an email template

```
DEFINITION
POST http://apiserver/emailtemplates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/emailtemplates/5", {
    "functionalCategory": "CV"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "entity": "A01",
    "entityDescription": "Account Master",
    "description": "New Account Thank You Email",
    "isSystemTemplate": true,
    "functionalCategory": "CV",
    "functionalCategoryDescription": "Church Volunteers",
    "sawId": "AAT23EMA",
    "sawIdDescription": "Account Emails Activity",
    "accessor": null,
    "accessorName": null,
    "selectionCriteria": null,
    "emailSubject": "Thank you for your kind donation",
    "emailBody": "{FirstName},\n\nThank you for your donation.",
    "topic": "THANKYOU",
    "category": "DONATION",
    "formType": null,
    "formTypeDescription": null
}


```

Updates the specified email template by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* entity (): base entity associated with the email template
* description (): description of the email template
* isSystemTemplate (): true if createing a system email template, false if creating a user/accessor email template
* functionalCategory (): Functional category associated with this email template
* sawId (): if isSystemTemplate is true, the sawId needed to use this email template is required (accessor is ignored)
* accessor (): if isSystemTemplate is false, the accessor who owns the email template is required (sawId is ignored)
* emailSubject (): email template subject
* emailBody (): email template body
* selectionCriteria: an array of entities joined to 'entity' which are reqired for any merge text contained in the template
* topic (optional): a topic code for the email template
* category (optional): a category code for the email template
* formType (optional): if type is `RECEIPTS`, the Form Type from which to retrieve merge fields

##### Returns

Returns the email template object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an email template

```
DEFINITION
DELETE http://apiserver/emailtemplates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/emailtemplates/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a email template. It cannot be undone.

##### Arguments

* id (required) - The id of the email template to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the email template does not exist, this call returns an error.

#### List all email templates

```
DEFINITION
GET http://apiserver/emailtemplates

EXAMPLE REQUEST
$.get("http://localhost:49195/emailtemplates?");

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
            "entity": "A01",
            "entityDescription": "Account Master",
            "description": "New Account Thank You Email",
            "isSystemTemplate": true,
            "functionalCategory": "DM",
            "functionalCategoryDescription": "Donor Ministries",
            "sawId": "AAT23EMA",
            "sawIdDescription": "Account Emails Activity",
            "accessor": "0",
            "accessorName": null,
            "selectionCriteria": [],
            "topic": "THANKYOU",
            "topicDescription": "A thank you email for the donor",
            "category": "DONATION",
            "categoryDescription": "Donation templates",
            "formType": null,
            "formTypeDescription": null
        },
        {...},
    ]
}

```

Returns a list of all email templates.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* entity (): base entity associated with the email template
* description (): description of the email template
* isSystemTemplate (): true if createing a system email template, false if creating a user/accessor email template
* functionalCategory (): Functional category associated with this email template
* sawId (): if isSystemTemplate is true, the sawId needed to use this email template is required (accessor is ignored)
* accessor (): if isSystemTemplate is false, the accessor who owns the email template is required (sawId is ignored)
* topic (optional): a topic code for the email template
* category (optional): a category code for the email template
* formType (optional): the Form Type from which to retrieve merge fields

##### Returns

A dictionary with an items property that contains an array of up to limit email templates, starting at index offset. Each entry in the array is a separate email template object. If no more email templates are available, the resulting array will be empty. This request should never return an error.

#### Preview an email template merge

```
DEFINITION
POST http://apiserver/emailtemplates/:id/preview

EXAMPLE REQUEST
$.post("http://localhost:49195/emailtemplates/5/preview", {
    "shouldSendEmail": true,
    "emailAddresses": ["jbrown@test.com", "lstone@test.com"]
});

EXAMPLE RESPONSE
{
    "subject": "Thank you for your kind donation, Dale Smith",
    "body": "Mr. Dale Smith,\n\nThank you for your recent donation of $15.15.",
    "errorMessage": null
}


```

Preview the merge of an existing email template. You need only supply the id. To preview, the email template must have a type of "RECEIPTS" and a valid Form Type. The Document Filter Query on the Form Type must also return at least one record.

##### Arguments

* shouldSendEmail (optional) - Whether or not to send the merged subject and body as an email to the specified `emailAddresses`
* emailAddresses (optional; required if `shouldSendEmail` is `true`) - If `shouldSendEmail` is `true`, the list of email addresses to which to send the merged subject and body as an email

##### Returns

Returns the merged `subject` and `body` if the preview merge was successful and an `errorMessage` otherwise.

### Email Assignments

#### Create an email assignment

```
DEFINITION
POST http://apiserver/emailassignments

EXAMPLE REQUEST
$.post("http://localhost:49195/emailassignments", {
    "emailAddress": "user@website.com",
    "statusForReplies": "O"
});

EXAMPLE RESPONSE
{
    "emailAddress": "user@website.com"
    "id": "10"
    "statusDescription": "Open"
    "statusForReplies": "O"
}

```

Creates a new email assignment.

##### Arguments

* emailAddress (required): email address to use for assignment logic
* statusForReplies (required): the status that will be stamped on the communication when the inbound email is a reply

##### Returns

Returns a email assignment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an email assignment

```
DEFINITION
GET http://apiserver/emailassignments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/emailassignments/5");

EXAMPLE RESPONSE
{
    "emailAddress": "user@website.com"
    "id": "10"
    "statusDescription": "Open"
    "statusForReplies": "O"
}

```

Retrieves the details of an existing email assignment. You need only supply the id.

##### Arguments

* id (required) - The id of the email assignment to be retrieved.

#### Update an email assignment

```
DEFINITION
POST http://apiserver/emailassignments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/emailassignments/5", {
    "emailAddress": "otherUser@website.com"
});

EXAMPLE RESPONSE
{
    "emailAddress": "otherUser@website.com"
    "id": "10"
    "statusDescription": "Open"
    "statusForReplies": "O"
}


```

Updates the specified email assignment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* emailAddress (): email address to use for assignment logic
* statusForReplies (): the status that will be stamped on the communication when the inbound email is a reply

##### Returns

Returns the email assignment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an email assignment

```
DEFINITION
DELETE http://apiserver/emailassignments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/emailassignments/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a email assignment. It cannot be undone.

##### Arguments

* id (required) - The id of the email assignment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the email assignment does not exist, this call returns an error.

#### List all email assignments

```
DEFINITION
GET http://apiserver/emailassignments

EXAMPLE REQUEST
$.get("http://localhost:49195/emailassignments?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "emailAddress": "user@website.com"
            "id": "10"
            "statusDescription": "Open"
            "statusForReplies": "O"
        },
        {...},
    ]
}

```

Returns a list of all email assignments.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* emailAddress (): email address to use for assignment logic
* statusForReplies (): the status that will be stamped on the communication when the inbound email is a reply

##### Returns

A dictionary with an items property that contains an array of up to limit email assignments, starting at index offset. Each entry in the array is a separate email assignment object. If no more email assignments are available, the resulting array will be empty. This request should never return an error.

### Email Assignment Rules

#### Create an email assignment rule

```
DEFINITION
POST http://apiserver/emailassignments/:id/rules

EXAMPLE REQUEST
$.post("http://localhost:49195/emailassignments/5/rules", {
    "isActive": true,
    "searchInSubject": true,
    "searchInBody": false,
    "sequence": 1,
    "keywords": "words",
    "assignToAccessor": "1234",
    "source": "G12GENERAL",
    "status": "O"
});

EXAMPLE RESPONSE
{
    "id": "18",
    "emailAssignmentId": 10,
    "sequence": 1,
    "keywords": "words",
    "searchInSubject": true,
    "searchInBody": false,
    "assignToAccessor": "1234",
    "isActive": true,
    "source": "G12GENERAL",
    "status": "O",
    "accessorName": "Accessor Person - Internal User",
    "sourceDescription": "General Source Code",
    "statusDescription": "Open"
}

```

Creates a new email assignment.

##### Arguments

* sequence (required): the sequence number that the assignment rule will be applied
* keywords (): comma separated list of words to look for
* searchInSubject (required): flag to indicate if the subject should be searched for the keywords or not
* searchInBody (required): flag to indicate if the body should be searched for the keywords or not
* assignToAccessor (required): the id of the accessor to assign the communication record to
* isActive (required): indicates if the rule is active or inactive
* source (): a source code to be stamped on the communication record when the rule is applied
* status (required): the status that will be stamped on the communication record when the rule is applied

##### Returns

Returns a email assignment rule object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an email assignment rule

```
DEFINITION
GET http://apiserver/emailassignments/:id/rules/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/emailassignments/5/rules/12");

EXAMPLE RESPONSE
{
    "id": "18",
    "emailAssignmentId": 10,
    "sequence": 1,
    "keywords": "words",
    "searchInSubject": true,
    "searchInBody": false,
    "assignToAccessor": "1234",
    "isActive": true,
    "source": "G12GENERAL",
    "status": "O",
    "accessorName": "Accessor Person - Internal User",
    "sourceDescription": "General Source Code",
    "statusDescription": "Open"
}

```

Retrieves the details of an existing email assignment rule. You need to supply the email assignment id as well as the assignment rule the id.

##### Arguments

* id (required) - The id of the email assignment rule to be retrieved.

#### Update an email assignment rule

```
DEFINITION
POST http://apiserver/emailassignments/:id/rules/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/emailassignments/5/rules/12", {
    "keywords": "more,key,words"
});

EXAMPLE RESPONSE
{
    "id": "18",
    "emailAssignmentId": 10,
    "sequence": 1,
    "keywords": "more,key,words",
    "searchInSubject": true,
    "searchInBody": false,
    "assignToAccessor": "1234",
    "isActive": true,
    "source": "G12GENERAL",
    "status": "O",
    "accessorName": "Accessor Person - Internal User",
    "sourceDescription": "General Source Code",
    "statusDescription": "Open"
}


```

Updates the specified email assignment rule by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sequence (): the sequence number that the assignment rule will be applied
* keywords (): comma separated list of words to look for
* searchInSubject (): flag to indicate if the subject should be searched for the keywords or not
* searchInBody (): flag to indicate if the body should be searched for the keywords or not
* assignToAccessor (): the id of the accessor to assign the communication record to
* isActive (): indicates if the rule is active or inactive
* source (): a source code to be stamped on the communication record when the rule is applied
* status (): the status that will be stamped on the communication record when the rule is applied

##### Returns

Returns the email assignment rule object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an email assignment rule

```
DEFINITION
DELETE http://apiserver/emailassignments/:id/rules/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/emailassignments/5/rules/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a email assignment rule. It cannot be undone.

##### Arguments

* id (required) - The id of the email assignment rule to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the email assignment rule does not exist, this call returns an error.

#### List all email assignment rules

```
DEFINITION
GET http://apiserver/emailassignments/:id/rules

EXAMPLE REQUEST
$.get("http://localhost:49195/emailassignments/5/rules?");

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
            "emailAssignmentId": 10,
            "sequence": 1,
            "keywords": "words",
            "searchInSubject": true,
            "searchInBody": false,
            "assignToAccessor": "1234",
            "isActive": true,
            "source": "G12GENERAL",
            "status": "O",
            "accessorName": "Accessor Person - Internal User",
            "sourceDescription": "General Source Code",
            "statusDescription": "Open"
        },
        {...},
    ]
}

```

Returns a list of all email assignment rules.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* sequence (): the sequence number that the assignment rule will be applied
* keywords (): comma separated list of words to look for
* searchInSubject (): flag to indicate if the subject should be searched for the keywords or not
* searchInBody (): flag to indicate if the body should be searched for the keywords or not
* assignToAccessor (): the id of the accessor to assign the communication record to
* isActive (): indicates if the rule is active or inactive
* source (): a source code to be stamped on the communication record when the rule is applied
* status (): the status that will be stamped on the communication record when the rule is applied

##### Returns

A dictionary with an items property that contains an array of up to limit email assignment rules, starting at index offset. Each entry in the array is a separate email assignment rules object. If no more email assignment rules are available, the resulting array will be empty. This request should never return an error.

### File Export Configurations

#### Create a file export configuration

```
DEFINITION
POST http://apiserver/fileexportconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/fileexportconfigurations", {
    "isActive":true,
    "processType":"JRNALSHIP",
    "sequence":1,
    "storedProcedure":"StoredProcedureName",
    "fileOutputLocation":"C:\output",
    "useFtp":true,
    "ftpAppConfigKeyPrefix":"ExportFTP",
    "shouldIncludeHeader":true,
    "escapeString":true,
    "delimiter":","
});

EXAMPLE RESPONSE
{
    "id":"3",
    "processType":"JRNALSHIP",
    "sequence":1,
    "storedProcedure":"StoredProcedureName",
    "fileOutputLocation":"C:\output",
    "useFtp":true,
    "isSftp":false,
    "ftpAppConfigKeyPrefix":"ExportFTP",
    "isActive":true,
    "shouldIncludeHeader":true,
    "escapeString":true,
    "delimiter":","
}

```

Creates a new file export configuration.

##### Arguments

* processType (required): the process type that the export will run after
* sequence (required): the sequence that the exports of the same type will be run in
* storedProcedure (required): the name of the stored procedure that will get the data for the export
* fileOutputLocation (required): the location that the exported file is put
* useFtp: (required) indicates if the export will transfer the file over an FTP
* isSftp: (required) indicates if the export will transfer the file over SFTP
* ftpAppConfigKeyPrefix: the prefix for app config keys with with FTP or SFTP credentials
* isActive: (required) indicates if the file export configuration is active or inactive
* shouldIncludeHeader: (required) indicates whether a header row should be added to the file
* escapeString: (required) indicates whether strings should be escaped by adding quotations around them
* delimiter: (required) the delimiter to be used between file columns

##### Returns

Returns a file export configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a file export configuration

```
DEFINITION
GET http://apiserver/fileexportconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/fileexportconfigurations/3");

EXAMPLE RESPONSE
{
    "id":"3",
    "processType":"JRNALSHIP",
    "sequence":1,
    "storedProcedure":"StoredProcedureName",
    "fileOutputLocation":"C:\output",
    "useFtp":true,
    "isSftp":false,
    "ftpAppConfigKeyPrefix":"ExportFTP",
    "isActive":true,
    "shouldIncludeHeader":true,
    "escapeString":true,
    "delimiter":","
}

```

Retrieves the details of an existing file export configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the file export configuration to be retrieved.

#### Update a file export configuration

```
DEFINITION
POST http://apiserver/fileexportconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/fileexportconfigurations/3", {
    "useFtp": false
});

EXAMPLE RESPONSE
{
    "id":"3",
    "processType":"JRNALSHIP",
    "sequence":1,
    "storedProcedure":"StoredProcedureName",
    "fileOutputLocation":"C:\output",
    "useFtp":false,
    "isSftp":false,
    "ftpAppConfigKeyPrefix":"ExportFTP",
    "isActive":true,
    "shouldIncludeHeader":true,
    "escapeString":true,
    "delimiter":","
}


```

Updates the specified file export configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* processType (optional): the process type that the export will run after
* sequence (optional): the sequence that the exports of the same type will be run in
* storedProcedure (optional): the name of the stored procedure that will get the data for the export
* fileOutputLocation (optional): the location that the exported file is put
* useFtp (optional): indicates if the export will transfer the file over an FTP
* isSftp (optional): indicates if the export will transfer the file over SFTP
* ftpAppConfigKeyPrefix (optional): the prefix for app config keys with with FTP or SFTP credentials
* isActive (optional): indicates if the file export configuration is active or inactive
* shouldIncludeHeader: (optional) indicates whether a header row should be added to the file
* escapeString: (optional) indicates whether strings should be escaped by adding quotations around them
* delimiter: (optional) the delimiter to be used between file columns

##### Returns

Returns the file export configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a file export configuration

```
DEFINITION
DELETE http://apiserver/fileexportconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/fileexportconfigurations/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a file export configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the file export configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the file export configuration does not exist, this call returns an error.

#### List all file export configurations

```
DEFINITION
GET http://apiserver/fileexportconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/fileexportconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id":"3",
            "processType":"JRNALSHIP",
            "sequence":1,
            "storedProcedure":"StoredProcedureName",
            "fileOutputLocation":"C:\output",
            "useFtp":false,
            "isSftp":false,
            "ftpAppConfigKeyPrefix":"ExportFTP",
            "isActive":true,
            "shouldIncludeHeader":true,
            "escapeString":true,
            "delimiter":","
        },
        {...},
    ]
}

```

Returns a list of all file export configurations.

##### Arguments

* processType (optional): the process type that the export will run after
* sequence (optional): the sequence that the exports of the same type will be run in
* storedProcedure (optional): the name of the stored procedure that will get the data for the export
* fileOutputLocation (optional): the location that the exported file is put
* useFtp (optional): indicates if the export will transfer the file over an FTP
* isSftp (optional): indicates if the export will transfer the file over SFTP
* ftpAppConfigKeyPrefix (optional): the prefix for app config keys with with FTP or SFTP credentials
* isActive (optional): indicates if the file export configuration is active or inactive
* shouldIncludeHeader: (optional) indicates whether a header row should be added to the file
* escapeString: (optional) indicates whether strings should be escaped by adding quotations around them
* delimiter: (optional) the delimiter to be used between file columns

##### Returns

A dictionary with an items property that contains an array of up to limit file export configurations, starting at index offset. Each entry in the array is a separate file export configuration object. If no more file export configurations are available, the resulting array will be empty. This request should never return an error.

### Form Types

#### Create a form type

```
DEFINITION
POST http://apiserver/formtypeconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/formtypeconfigurations", {
    "formType": "ELETTER",
    "description": "Email Letter",
    "communicationType": "LETTER",
    "deliveryMethod": "EMAIL",
    "isDocumentMergedOnServer": true,
    "maxMergedDocumentRecordCount": 1000,
    "dataSource": null,
    "documentFilterQuery": "SELECT * FROM \"D09_ProductionPrintGroupLetters\" WHERE  PrintGroupId = {PrintGroupId}",
    "isActive": true,
    "fromEmailAddress": null,
    "emailSubject": "Thank You!",
    "isTemplateHtml": null,
    "isAutomaticPrintingAllowed": true
});

EXAMPLE RESPONSE
{
    "id": "49",
    "formType": "ELETTER",
    "description": "Email Letter",
    "communicationType": "LETTER",
    "communicationTypeDescription": "Communication Letters",
    "deliveryMethod": "EMAIL",
    "deliveryMethodDescription": "EMAIL",
    "isDocumentMergedOnServer": true,
    "maxMergedDocumentRecordCount": 1000,
    "dataSource": null,
    "documentFilterQuery": "SELECT * FROM \"D09_ProductionPrintGroupLetters\" WHERE  PrintGroupId = {PrintGroupId}",
    "isActive": true,
    "fromEmailAddress": null,
    "emailSubject": "Thank You!",
    "isTemplateHtml": null,
    "isAutomaticPrintingAllowed": true
}

```

Creates a new form type.

##### Arguments

* formType (required) - The type of the form type.
* description (required) - The description of the form type.
* communicationType (required) - The communication type of the form type.
* deliveryMethod (required) - The delivery method of the form type.
* isDocumentMergedOnServer (conditional; required if `deliveryMethod` is `EMAIL` or `NOTEMAIL`; must be empty otherwise; *must* be `true` if the `communicationType` is `PERIODIC` and the `deliveryMethod` is `EMAIL` or `NOTEMAIL`) - Whether or not documents will be merged on the server (as opposed to on the client using ActiveX)
* maxMergedDocumentRecordCount (optional) - The maximum number of records allowed in a single merged document. Must be null if `isDocumentMergedOnServer` is `false` or `deliveryMethod` is not `NOTEMAIL`.
* dataSource (conditional; required if `deliveryMethod` is `EMAIL` or `NOTEMAIL` and `isDocumentMergedOnServer` is `false`; must be empty otherwise) - The location on a disc where the form is located.
* documentFilterQuery (conditional; required if `deliveryMethod` is `EMAIL` or `NOTEMAIL`) - The query to filter the document.
* isActive (required) - Whether or not this form type is active.
* fromEmailAddress (conditional; required if `deliveryMethod` is `EMAIL`, must be `null` otherwise) - The email address from which to send merged emails. Defaults to the configured from address if not provided.
* emailSubject (conditional; required if `deliveryMethod` is `EMAIL` and `isTemplateHtml` is `false`, must be `null` otherwise) - The subject of the email to send.
* isTemplateHtml (conditional; must be `null` if `deliveryMethod` is not `EMAIL` or `isDocumentMergedOnServer` is `false` or `communicationType` is not `RECEIPT`) - Whether or not the documents under this Form Type will use an HTML Template.
* isAutomaticPrintingAllowed (conditional; must be `false` if `isDocumentMergedOnServer` is `false`) - Whether automatic printing is allowed as part of the Production Run Process.

##### Returns

Returns a form type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a form type

```
DEFINITION
GET http://apiserver/formtypeconfigurations/:id - id is the RecordId

EXAMPLE REQUEST
$.get("http://localhost:49195/formtypeconfigurations/49");

EXAMPLE RESPONSE
{
    "id": "49",
    "formType": "ELETTER",
    "description": "Email Letter",
    "communicationType": "LETTER",
    "communicationTypeDescription": "Communication Letters",
    "deliveryMethod": "EMAIL",
    "deliveryMethodDescription": "EMAIL",
    "isDocumentMergedOnServer": true,
    "maxMergedDocumentRecordCount": 1000,
    "dataSource": null,
    "documentFilterQuery": "SELECT * FROM \"D09_ProductionPrintGroupLetters\" WHERE  PrintGroupId = {PrintGroupId}",
    "isActive": true,
    "fromEmailAddress": null,
    "emailSubject": "Thank You!",
    "isTemplateHtml": null,
    "isAutomaticPrintingAllowed": true
}

```

Retrieves the details of an existing form type object. You need only supply the form type id.

##### Arguments

* id (required) - The id of the form type object to be retrieved.

##### Returns

Returns a form type object if a valid form type id was provided.

#### Retrieve a form type legacy

```
DEFINITION
GET http://apiserver/formtypes/:id - id is the formType

EXAMPLE REQUEST
$.get("http://localhost:49195/formtypes/LTR");

EXAMPLE RESPONSE
{
    "id": "LTR",
    "formType": "LTR",
    "description": "BP-PledgeStatement-Print_Report",
    "communicationType": "PLDGACK",
    "communicationTypeDescription": "Pledge Acknowledgements",
    "deliveryMethod": "REPORT",
    "deliveryMethodDescription": "Report",
    "isDocumentMergedOnServer": null,
    "maxMergedDocumentRecordCount": null,
    "dataSource": null,
    "documentFilterQuery": null,
    "isActive": true,
    "fromEmailAddress": null,
    "emailSubject": null,
    "isTemplateHtml": null,
    "isAutomaticPrintingAllowed": false,
    "documents": [
        null,
        null
    ],
    "documentCollection": [
        {
            "id": "20117",
            "sequenceNumber": 1,
            "documentAddress": null,
            "reportId": "176",
            "reportDescription": "Pledge Statement"
        },
        {
            "id": "20118",
            "sequenceNumber": 2,
            "documentAddress": null,
            "reportId": "177",
            "reportDescription": "New Report"
        }
    ]
}

```

Retrieves the details of an existing form type. You need only supply the form type.

##### Arguments

* id (required) - The form type of the form type object to be retrieved.

##### Returns

Returns a form type object if a valid form type was provided.
The `documents` property is only returned if the /formtypes/:id URL is used.

#### Update a form type

```
DEFINITION
POST http://apiserver/formtypeconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/formtypeconfigurations/49", {
    "formType": "ELETTER",
    "description": "Email Letter",
    "communicationType": "LETTER",
    "deliveryMethod": "EMAIL",
    "isDocumentMergedOnServer": false,
    "maxMergedDocumentRecordCount": null,
    "dataSource": "P:\DonorStudio\DataSources\SE_5_0\SQL01 SE_5_0 D09_ProductionPrintGroupLetters.odc",
    "documentFilterQuery": "SELECT * FROM \"D09_ProductionPrintGroupLetters\" WHERE  PrintGroupId = {PrintGroupId}",
    "isActive": true,
    "fromEmailAddress": "test@test.edu",
    "emailSubject": "Thank You!",
    "isTemplateHtml": null,
    "isAutomaticPrintingAllowed": false
});

EXAMPLE RESPONSE
{
    "id": "49",
    "formType": "ELETTER",
    "description": "Email Letter",
    "communicationType": "LETTER",
    "communicationTypeDescription": "Communication Letters",
    "deliveryMethod": "EMAIL",
    "deliveryMethodDescription": "EMAIL",
    "isDocumentMergedOnServer": false,
    "maxMergedDocumentRecordCount": null,
    "dataSource": "P:\DonorStudio\DataSources\SE_5_0\SQL01 SE_5_0 D09_ProductionPrintGroupLetters.odc",
    "documentFilterQuery": "SELECT * FROM \"D09_ProductionPrintGroupLetters\" WHERE  PrintGroupId = {PrintGroupId}",
    "isActive": true,
    "fromEmailAddress": "test@test.edu",
    "emailSubject": "Thank You!",
    "isTemplateHtml": null,
    "isAutomaticPrintingAllowed": false
}


```

Updates the specified form type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* formType () - The type of the form type.
* description () - The description of the form type.
* communicationType() - The communication type of the form type.
* deliveryMethod () - The delivery method of the form type.
* isDocumentMergedOnServer () - Whether or not documents will be merged on the server (as opposed to on the client using ActiveX).
* maxMergedDocumentRecordCount () - The maximum number of records allowed in a single merged document. Must be null if `isDocumentMergedOnServer` is `false` or `deliveryMethod` is not `NOTEMAIL`.
* dataSource () - The location on a disc where the form is located.
* documentFilterQuery () - The query to filter the document.
* isActive () - Whether or not this form type is active.
* fromEmailAddress (conditional; required if `deliveryMethod` is `EMAIL`, must be `null` otherwise) - The email address from which to send merged emails. Defaults to the configured from address if not provided.
* emailSubject (conditional; required if `deliveryMethod` is `EMAIL` and `isTemplateHtml` is `false`, must be `null` otherwise) - The subject of the email to send.
* isTemplateHtml (conditional; must be `null` if `deliveryMethod` is not `EMAIL` or `isDocumentMergedOnServer` is `false` or `communicationType` is not `RECEIPT`) - Whether or not the documents under this Form Type will use an HTML Template.
* isAutomaticPrintingAllowed (conditional; must be `false` if `isDocumentMergedOnServer` is `false`) - Whether automatic printing is allowed as part of the Production Run Process.

##### Returns

Returns the form type object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a form type

```
DEFINITION
DELETE http://apiserver/formtypeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/formtypeconfigurations/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a form type. It cannot be undone.

##### Arguments

* id (required) - The id of the form type to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the form type does not exist, this call returns an error.

#### List all form types

```
DEFINITION
GET http://apiserver/formtypes
GET http://apiserver/formtypeconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/formtypeconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 581
    },
    "items": [
        {
            "id": "49",
            "formType": "ELETTER",
            "description": "Email Letter",
            "communicationType": "LETTER",
            "communicationTypeDescription": "Communication Letters",
            "deliveryMethod": "EMAIL",
            "deliveryMethodDescription": "EMAIL",
            "isDocumentMergedOnServer": false,
            "maxMergedDocumentRecordCount": null,
            "dataSource": "P:\DonorStudio\DataSources\SE_5_0\SQL01 SE_5_0 D09_ProductionPrintGroupLetters.odc",
            "documentFilterQuery": "SELECT * FROM \"D09_ProductionPrintGroupLetters\" WHERE  PrintGroupId = {PrintGroupId}",
            "isActive": true,
            "fromEmailAddress": "test@test.edu",
            "emailSubject": "Thank You!",
            "isTemplateHtml" null,
            "isAutomaticPrintingAllowed": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all form types matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in form type
* description () - Filter list by partial match in description
* communicationType () - Filter list by partial match in communication type
* isActive () - Filter list by whether active or not

##### Returns

A dictionary with an items property that contains an array of up to limit form types, starting at index offset. Each entry in the array is a separate form type object. If no more form types are available, the resulting array will be empty. This request should never return an error.

#### Retrieve all form type merge fields

```
DEFINITION
GET http://apiserver/formtypeconfigurations/:id/mergefields

EXAMPLE REQUEST
$.get("http://localhost:49195/formtypeconfigurations/49/mergefields");

EXAMPLE RESPONSE
[
    {
        "field": "RecordId",
        "title": "RecordId"
    },
    {
        "field": "ResponseId",
        "title": "ResponseId"
    },
    {...},
    {...}
]

```

Returns a list of all form type merge fields based on the response from the form type DocumentFilterQuery.

##### Arguments

* id (required) - The id of the form type for which to retrieve merge fields.

##### Returns

An array of form type merge fields. Each entry in the array is a separate form type merge field object. If no form type merge fields are available, the resulting array will be empty. This request will return an error if the DocumentFilterQuery on the form type could not be executed.

### Form Type Documents

#### Create a form type document

```
DEFINITION
POST http://apiserver/formtypeconfigurations/:id/documents

EXAMPLE REQUEST
$.post("http://localhost:49195/formtypeconfigurations/57/documents", {
    "seqenceNumber": 5,
    "reportId": "176"
});

EXAMPLE RESPONSE
{
    "id": "20084",
    "seqenceNumber": 5,
    "documentAddress": null,
    "fileName": null,
    "fileMimeType": null,
    "groupSize": null,
    "reportId": "176",
    "reportDescription": "Pledge Statement",
    "emailTemplateRecordId": null,
    "emailTemplateDescription": null
}

```

Creates a new form type document. If the parent form type's `isDocumentMergedOnServer` flag is `true` and its `isTemplateHtml` flag is `false`, either `documentAddress` or `fileName`/`file` must be provided, but not both.

##### Arguments

* sequenceNumber (required) - The sequence number of the form type document.
* documentAddress (conditional; required if the parent form type's `isDocumentMergedOnServer` flag is `false` or if `fileName`/`file` are empty; must be empty when `reportId` is present or the parent form type's `isTemplateHtml` flag is `true`) - The address where the document is located. If the parent form type's `isDocumentMergedOnServer` flag is `true`, it must be a path accessible by the server. If the flag is `false`, it must be a path accessible by the client.
* fileName (conditional; required if the parent form type's `isDocumentMergedOnServer` flag is `true` and its `isTemplateHtml` flag is `false` and `documentAddress` is empty; must be empty otherwise) - The name of the `file` uploaded for this document.
* file (conditional; required if the parent form type's `isDocumentMergedOnServer` flag is `true` and its `isTemplateHtml` flag is `false` and `documentAddress` is empty; must be empty otherwise) - A Base64-encoded string containing the bytes of the uploaded file for this document.
* groupSize (conditional; optional if the parent form type's `isDocumentMergedOnServer` flag is `true` and its `isTemplateHtml` flag is `false`; must be empty otherwise) - The number of records per group to process when this document is merged. Must be between 1 and the `SSMRGMAXGP` control record value, if provided.
* reportId (conditional; required if the parent form type's `deliveryType` is equal to `REPORT`; must be empty otherwise) - The report that is associated with this form type document.
* emailTemplateRecordId (conditional; required if the parent form type's `isTemplateHtml` flag is `true`; must be null otherwise) - The id of the email template that is associated with this form type document.

##### Returns

Returns a form type document object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a form type document

```
DEFINITION
GET http://apiserver/formtypeconfigurations/:id/documents/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/formtypeconfigurations/57/documents/20084");

EXAMPLE RESPONSE
{
    "id": "20084",
    "seqenceNumber": 5,
    "documentAddress": null,
    "fileName": null,
    "fileMimeType": null,
    "groupSize": null,
    "reportId": "176",
    "reportDescription": "Pledge Statement",
    "emailTemplateRecordId": null,
    "emailTemplateDescription": null
}

```

Retrieves the details of an existing form type document. You need only supply the id.

##### Arguments

* id (required) - The id of the form type document to be retrieved.
* download (optional) - A `true` value will force the `file` to be retrieved as a Base64 string. Otherwise, `file` will be `null`.

#### Update a form type document

```
DEFINITION
POST http://apiserver/formtypeconfigurations/:id/documents/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/formtypeconfigurations/57/documents/20084", {
    "documentAddress": "C:\sample\path\template.docx",
    "reportId": null
});

EXAMPLE RESPONSE
{
    "id": "20084",
    "seqenceNumber": 5,
    "documentAddress": "C:\sample\path\template.docx",
    "fileName": null,
    "fileMimeType": null,
    "groupSize": null,
    "reportId": null,
    "reportDescription": null,
    "emailTemplateRecordId": null,
    "emailTemplateDescription": null
}


```

Updates the specified form type document by setting the values of the parameters passed. Any parameters not provided will be left unchanged. The final properties of the form type document must correspond with the argument rules outlined in the [Create a form type document](#create-a-form-type-document) section.

##### Arguments

* sequenceNumber (optional) - The sequence number of the form type document.
* documentAddress (optional) - The address where the document is located. If the parent form type's `isDocumentMergedOnServer` flag is `true` and its `isTemplateHtml` flag is `false`, it must be a path accessible by the server. If the flag is `false` and its `isTemplateHtml` flag is `false`, it must be a path accessible by the client. It must be null otherwise.
* fileName (optional) - The name of the `file` uploaded for this document.
* groupSize (optional) - The number of records per group to process when this document is merged. Must be between 1 and the `SSMRGMAXGP` control record value, if provided.
* reportId (optional) - The report that is associated with this form type.
* emailTemplateRecordId (optional) - The id of the email template that is associated with this form type document.

##### Returns

Returns the form type document object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a form type document

```
DEFINITION
DELETE http://apiserver/formtypeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/formtypeconfigurations/20084", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a form type document. It cannot be undone.

##### Arguments

* id (required) - The id of the form type document to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the form type document does not exist, this call returns an error.

#### List all form type documents

```
DEFINITION
GET http://apiserver/formtypeconfigurations/:id/documents

EXAMPLE REQUEST
$.get("http://localhost:49195/formtypeconfigurations/57/documents?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20084",
            "seqenceNumber": 5,
            "documentAddress": "C:\sample\path\template.docx",
            "fileName": null,
            "fileMimeType": null,
            "groupSize": null,
            "reportId": null,
            "reportDescription": null,
            "emailTemplateRecordId": null,
            "emailTemplateDescription": null
        },
        {...}
    ]
}

```

Returns a list of all form type documents.

##### Arguments

* formType (required) - The type of form to retrieve documents for.

##### Returns

A dictionary with an items property that contains an array of up to limit form type documents, starting at index offset. Each entry in the array is a separate form type document object. If no more form type documents are available, the resulting array will be empty. This request should never return an error.

#### Preview a form type document merge

```
DEFINITION
POST http://apiserver/formtypeconfigurations/:id/documents/:id/preview

EXAMPLE REQUEST
$.post("http://localhost:49195/formtypeconfigurations/57/documents/20085/preview");

EXAMPLE RESPONSE
{
    "formType": "ARSTMTTST",
    "formTypeDeliveryMethod": "NOTEMAIL",
    "document": {
        "id": "20085",
        "seqenceNumber": 5,
        "documentAddress": "test\\path\\document.docx",
        "fileName": null,
        "fileMimeType": null,
        "reportId": null,
        "reportDescription": null
    },
    "mergedDocument": {
        "fileName": "document.docx",
        "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
        "file": "UEsDBBQAAgAIAKyDe1AemujtOQEAAHcCAAARAAAAZG9jUHJvcHMvY29yZS54bWyVUstOwzAQ/JXI98S..."
    },
    "errorMessage": null
}

```

Preview the document merge of an existing form type document. You need only supply the id.

##### Arguments

* id (required) - The id of the form type document to be previewed.

##### Returns

Returns the form type document object along with the previewed document (if the FormType DeliveryMethod is "NOTEMAIL"). If the FormType DeliveryMethod is "EMAIL", this method will add a notification record to be processed by the Notification service, which will send the email to the logged-in user. Returns an error if validate parameters are invalid.

### Missionary Summaries

#### Retrieve a missionary summary

```
DEFINITION
GET http://apiserver/missionarysummaries/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/missionarysummaries/MISSPROJ1");

EXAMPLE RESPONSE
{
    "id": "MISSPROJ1",
    "projectCode": "MISSPROJ1",
    "projectDescription": "My First Missionary Project",
    "firstName": "John",
    "lastName": "Smithington",
    "currentBudgetAmount": 25500.50,
    "fiscalYearStartDate": "2020-01-01",
    "fiscalYearEndDate": "2020-12-31",
    "currentYearToDateDonationAmount": 21355.78,
    "previousYearToDateDonationAmount": 23845.21,
    "previousYearTotalDonationAmount": 28062.15
}

```

Retrieves the details of an existing missionary summary. You need only supply the id.

##### Arguments

* id (required) - The project code of the missionary summary to be retrieved.

##### Returns

Returns a missionary summary object if a valid id was provided.

#### List all missionary summaries

```
DEFINITION
GET http://apiserver/missionarysummaries

EXAMPLE REQUEST
$.get("http://localhost:49195/missionarysummaries");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 10
    },
     "items": [
        {
            "id": "MISSPROJ1",
            "projectCode": "MISSPROJ1",
            "projectDescription": "My First Missionary Project",
            "firstName": "John",
            "lastName": "Smithington",
            "currentBudgetAmount": 25500.50,
            "fiscalYearStartDate": "2020-01-01",
            "fiscalYearEndDate": "2020-12-31",
            "currentYearToDateDonationAmount": 21355.78,
            "previousYearToDateDonationAmount": 23845.21,
            "previousYearTotalDonationAmount": 28062.15
        },
        {...},
    ]
}

```

Returns a list of missionary summaries to which the logged in user has access.

May be sorted by providing column criteria. Please see the [Paged Response](#paged-response) section above for more details about sorting.

##### Returns

A dictionary with an items property that contains an array of up to limit missionary summaries, starting at index offset. Each entry in the array is a separate missionary summary object. If no more missionary summaries are available, the resulting array will be empty. This request should never return an error.

#### Retrieve a missionary pledge summary

```
DEFINITION
GET http://apiserver/missionarysummaries/:id/pledgesummary

EXAMPLE REQUEST
$.get("http://localhost:49195/missionarysummaries/MISSPROJ1/pledgesummary");

EXAMPLE RESPONSE
{
    "activePledges": 10,
    "totalPledged": 12345.67,
    "currentYearToDateDonationAmount": 21355.78,
    "previousYearToDateDonationAmount": 23845.21,
    "previousYearTotalDonationAmount": 28062.15
}

```

Retrieves the details of an existing missionary pledge summary. You need only supply the project code.

##### Arguments

* id (required) - The project code of the missionary pledge summary to be retrieved.

##### Returns

Returns a missionary pledge summary object if a valid project code was provided.

### Note Types

#### Retrieve a note type

```
DEFINITION
GET http://apiserver/notetypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/notetypes/DDCACALERT");

EXAMPLE RESPONSE
{
    "id": "DDCACALERT",
    "description": "Account Alert",
    "displaySequence": 35,
    "labelDescription": "Account Alert",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Retrieves the details of an existing note type. You need only supply the note type.

##### Arguments

* id (required) - The note type of the note type object to be retrieved.

##### Returns

Returns a note type object if a valid note type was provided.

#### List all note types

```
DEFINITION
GET http://apiserver/notetypes

EXAMPLE REQUEST
$.get("http://localhost:49195/notetypes?isActive=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 581
    },
    "items": [
        {
            "id": "DDCACALERT",
            "description": "Account Alert",
            "displaySequence": 35,
            "labelDescription": "Account Alert",
            "isUserDefined": false,
            "category": "ACCOUNT",
            "isActive": true,
            "isDisplayableInStudioOnline": false,
            "isSearchableInStudioOnline": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all note types matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in note type
* description () - Filter list by partial match in description
* category () - Filter list by partial match in category
* isActive () - Filter list by whether active or not
* isDisplayableInStudioOnline () - Filter list by whether marked as displayable in StudioOnline or not
* isSearchableInStudioOnline () - Filter list by whether marked as searchable in StudioOnline or not

##### Returns

A dictionary with an items property that contains an array of up to limit note types, starting at index offset. Each entry in the array is a separate note type object. If no more note types are available, the resulting array will be empty. This request should never return an error.

### Number Types

#### Create a number type

```
DEFINITION
POST http://apiserver/numbertypes

EXAMPLE REQUEST
$.post("http://localhost:49195/numbertypes", {
    "id": "DDCDONYEAR"
    "description": "Number of Donations in a Year",
    "displaySequence": 258,
    "isMultiValue": false,
    "labelDescription": "Number of Donations in a Year",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "DDCDONYEAR",
    "description": "Number of Donations in a Year",
    "displaySequence": 258,
    "isMultiValue": false,
    "labelDescription": "Number of Donations in a Year",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "start": null,
    "end": null,
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Creates a new number type.

##### Arguments

* id (required) - The id of the number type.
* isMultiValue (required) - Whether the number type is a multi value number or not.
* isUserDefined (required) - Whether the number type is user defined or not.
* isActive (required) - Whether the number type is active or not.
* description (optional) - The description for the number type.
* displaySequence (optional) - The display sequence of the number type.
* labelDescription (optional) - The label description for the number type.
* category (optional) - The category of the number type.
* isDisplayableInStudioOnline (optional) - Indicates whether the date type is able to be displayed in StudioOnline.
* isSearchableInStudioOnline (optional) - Not currently used in datetypes, included because of common inheritance with codetypes and notetypes.

##### Returns

Returns a number type object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a number type

```
DEFINITION
GET http://apiserver/numbertypes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/numbertypes/DDCDONYEAR");

EXAMPLE RESPONSE
{
    "id": "DDCDONYEAR",
    "description": "Number of Donations in a Year",
    "displaySequence": 258,
    "isMultiValue": false,
    "labelDescription": "Number of Donations in a Year",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "start": 0,
    "end": 100,
    "isActive": true,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}

```

Retrieves the details of an existing number type. You need only supply the number type.

##### Arguments

* id (required) - The number type of the number type object to be retrieved.

##### Returns

Returns a number type object if a valid number type was provided.

#### Update a number type

```
DEFINITION
POST http://apiserver/numbertypes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/numbertypes/DDCDONYEAR", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "DDCDONYEAR",
    "description": "Number of Donations in a Year",
    "displaySequence": 258,
    "isMultiValue": false,
    "labelDescription": "Number of Donations in a Year",
    "isUserDefined": false,
    "category": "ACCOUNT",
    "start": 0,
    "end": 100,
    "isActive": false,
    "isDisplayableInStudioOnline": false,
    "isSearchableInStudioOnline": false
}


```

Updates the specified number type by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* isMultiValue () - Whether the number type is a multi value number or not.
* isUserDefined () - Whether the number type is user defined or not.
* isActive () - Whether the number type is active or not.
* description () - The description for the number type.
* displaySequence () - The display sequence of the danumberte type.
* labelDescription () - The label description for the number type.
* category () - The category of the number type.
* isDisplayableInStudioOnline () - Indicates whether the date type is able to be displayed in StudioOnline.
* isSearchableInStudioOnline () - Not currently used in datetypes, included because of common inheritance with codetypes and notetypes.

##### Returns

Returns the number type object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a number type

```
DEFINITION
DELETE http://apiserver/numbertypes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/numbertypes/DDCDONYEAR", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a number type. It cannot be undone.

##### Arguments

* id (required) - The id of the number type to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the number type does not exist, this call returns an error.

#### List all number types

```
DEFINITION
GET http://apiserver/numbertypes

EXAMPLE REQUEST
$.get("http://localhost:49195/numbertypes?isActive=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 155
    },
    "items": [
        {
            "id": "DDCDONYEAR",
            "description": "Number of Donations in a Year",
            "displaySequence": 258,
            "isMultiValue": false,
            "labelDescription": "Number of Donations in a Year",
            "isUserDefined": false,
            "category": "ACCOUNT",
            "start": 0,
            "end": 100,
            "isActive": false,
            "isDisplayableInStudioOnline": false,
            "isSearchableInStudioOnline": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all number types matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in number type
* description () - Filter list by partial match in description
* category () - Filter list by partial match in category
* isActive () - Filter list by whether active or not
* isMultiValue () - Filter list be whether multi-value or not
* isDisplayableInStudioOnline () - Filter list by whether marked as displayable in StudioOnline or not
* isSearchableInStudioOnline () - Filter list by whether marked as searchable in StudioOnline or not

##### Returns

A dictionary with an items property that contains an array of up to limit number types, starting at index offset. Each entry in the array is a separate number type object. If no more number types are available, the resulting array will be empty. This request should never return an error.

### Number Type Range Limits

#### Create a number type range limit

```
DEFINITION
POST http://apiserver/numbers/:id/rangelimits

EXAMPLE REQUEST
$.post("http://localhost:49195/numbers/CSS/rangelimits", {
    "numberLow": 1,
    "numberHigh": 10000
});

EXAMPLE RESPONSE
{
    "id": "50",
    "numberLow": 1,
    "numberHigh": 10000
}

```

Creates a new number type range limit object

##### Arguments

* numberLow (required) - The minimum range limit.
* numberHigh (required) - The maximum range limit.

##### Returns

Returns a number type range limit object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or number type url).

#### Retrieve a number type range limit

```
DEFINITION
GET http://apiserver/numbers/:id/rangelimits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/numbers/CCS/rangelimits/50");

EXAMPLE RESPONSE
{
    "id": "50",
    "numberLow": 1,
    "numberHigh": 10000
}

```

Retrieves the details of an existing number type range limit. You need only supply the number type id and number type range limit id.

##### Returns

Returns a number type range limit object if a valid id was provided.

#### Update a number type range limit

```
DEFINITION
POST http://apiserver/numbers/:id/rangelimits/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/numbers/CSS/rangelimits/50", {
    "numberLow": 10
});

EXAMPLE RESPONSE
{
    "id": "50",
    "numberLow": 10,
    "numberHigh": 10000
}

```

Updates the specified number type range limit by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* numberLow (optional) - The minimum range limit.
* numberHigh (optional) - The maximum range limit.

##### Returns

Returns the number type range limit object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type url).

#### Delete a number type range limit

```
DEFINITION
DELETE http://apiserver/numbers/:id/rangelimits/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/numbers/G15/rangelimits/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a number type range limit. It cannot be undone.

##### Arguments

* id (required) - The id of the number type range limit to be deleted.

##### Returns

Returns a 204 No Content response on success. If the number type range limit id does not exist, this call returns an error.

#### List all number type range limits

```
DEFINITION
GET http://apiserver/numbers/:id/rangelimits

EXAMPLE REQUEST
$.get("http://localhost:49195/numbers/G15/rangelimits");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "50",
            "numberLow": 10,
            "numberHigh": 10000
        },
        {...},
        {...}
    ]
}

```

Returns a list of all number type range limits.

##### Returns

A dictionary with an items property that contains an array of up to limit number type range limits, starting at index offset. Each entry in the array is a separate number type range limit object. If no more number type range limits are available, the resulting array will be empty. This request should never return an error.

### Number Type Attributes

#### Create a number type attribute

```
DEFINITION
POST http://apiserver/numbertypes/:id/attributes

EXAMPLE REQUEST
$.post("http://localhost:49195/numbertypes/CCS/attributes", {
    "type": "CHURCHATTR",
    "value": "ATTRVALUE",
    "description": "TESTDESC"
});

EXAMPLE RESPONSE
{
    "id": "238",
    "type": "CHURCHATTR",
    "value": "ATTRVALUE",
    "description": "TESTDESC"
}

```

Creates a new number type attribute object

##### Arguments

* type (required) - The type of the attribute.
* value (optional) - The value of the attribute.
* description (optional) - The description of the attribute.

##### Returns

Returns a number type attribute object if the call succeeded. Returns an error if create parameters are invalid (e.g. not providing a type).

#### Retrieve a number type attribute

```
DEFINITION
GET http://apiserver/numbertypes/:id/attributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/numbertypes/CCS/attributes/238");

EXAMPLE RESPONSE
{
    "id": "238",
    "type": "CHURCHATTR",
    "value": "ATTRVALUE",
    "description": "TESTDESC"
}

```

Retrieves the details of an existing number type attribute. You need only supply the number type id and number type attribute id.

##### Returns

Returns a number type attribute object if a valid id was provided.

#### Update a number type attribute

```
DEFINITION
POST http://apiserver/numbertypes/:id/attributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/numbertypes/CCS/attributes/238", {
    "value": "NewValue"
});

EXAMPLE RESPONSE
{
    "id": "238",
    "type": "CHURCHATTR",
    "value": "NewValue",
    "description": "TESTDESC"
}

```

Updates the specified number type attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of the attribute.
* value (optional) - The value of the attribute.
* description (optional) - The description of the attribute.

##### Returns

Returns the number type attribute object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type url).

#### Delete a number type attribute

```
DEFINITION
DELETE http://apiserver/numbertypes/:id/attributes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/numbertypes/CCS/attributes/238", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a number type attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the number type attribute to be deleted.

##### Returns

Returns a 204 No Content response on success. If the number type attribute id does not exist, this call returns an error.

#### List all number type attributes

```
DEFINITION
GET http://apiserver/numbertypes/:id/attributes

EXAMPLE REQUEST
$.get("http://localhost:49195/numbertypes/CCS/attributes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "238",
            "type": "CHURCHATTR",
            "value": "NewValue",
            "description": "TESTDESC"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all number type attributes.

##### Returns

A dictionary with an items property that contains an array of up to limit number type attributes, starting at index offset. Each entry in the array is a separate number type attribute object. If no more number type attributes are available, the resulting array will be empty. This request should never return an error.

### Integration Configurations

#### Create an integration configuration

```
DEFINITION
POST http://apiserver/integrationconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/integrationconfigurations", {
    "code": "CCNCT123",
    "description": "CardConnect Configuration",
    "type": "CCONNECT",
    "typeCategory": "PAYGATEWAY",
    "configuration": "{\"username\":\"username123\"}"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "code": "CCNCT123",
    "description": "CardConnect Configuration",
    "type": "CCONNECT",
    "typeDescription": "CardConnect Integration",
    "typeCategory": "PAYGATEWAY",
    "typeCategoryDescription": "Payment Gateway",
    "configuration": "{\"username\":\"username123\"}",
    "prototype": {
        "id": "CCONNECT",
        "configuration": "{\"username\":\"Default Username\"}"
    }
}

```

Creates a new integration configuration.

##### Arguments

* code (required) - The unique code of integration configuration.
* description (required) - The description of the integration configuration.
* type (required) - The type of integration configuration. Must be a valid 'INTCFGTYP' code. Must have a valid Code Value Code Attribute of the type category for this record.
* typeCategory (required) - The type category for the integration configuration. Must be a valid 'INTCFGCAT' code.
* configuration (required) - JSON object containing all configuration fields required for a specific integration.

##### Returns

Returns an integration configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an integration configuration

```
DEFINITION
GET http://apiserver/integrationconfigurations/7

EXAMPLE REQUEST
$.get("http://localhost:49195/integrationconfigurations/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "code": "CYBTKNVLT",
    "description": "CyberSource Configuration",
    "type": "CYB_SOURCE",
    "typeDescription": "CyberSource Integration",
    "typeCategory": "PAYGATEWAY",
    "typeCategoryDescription": "Payment Gateway",
    "configuration": "{\"TokenVaultCode\":\"TOKENEX\"}",
    "prototype": {
        "id": "CYB_SOURCE",
        "configuration": "{\"TokenVaultCode\":\"Default TokenVaultCode\"}"
    }
}

```

Retrieves the details of an existing integration configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the integration configuration to be retrieved.

#### Update an integration configuration

```
DEFINITION
POST http://apiserver/integrationconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/integrationconfigurations/2", {
    "configuration": "{\"TokenVaultCode\":\"TOXENEX\"}"
});

EXAMPLE RESPONSE
{
    "id": "2",
    "code": "CYBTKNVLT",
    "description": "CyberSource Configuration",
    "type": "CYB_SOURCE",
    "typeDescription": "CyberSource Integration",
    "typeCategory": "PAYGATEWAY",
    "typeCategoryDescription": "Payment Gateway",
    "configuration": "{\"TokenVaultCode\":\"TOXENEX\"}",
    "prototype": {
        "id": "CYB_SOURCE",
        "configuration": "{\"TokenVaultCode\":\"Default TokenVaultCode\"}"
    }
}


```

Updates the specified integration configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of integration configuration. Must be a valid 'INTCFGTYP' code. Must have a valid Code Value Code Attribute of the type category for this record.
* description (optional) - The description of the integration configuration.
* configuration (optional) - JSON object containing all configuration fields required for a specific integration.

##### Returns

Returns the integration configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an integration configuration

```
DEFINITION
DELETE http://apiserver/integrationconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/integrationconfigurations/13", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an integration configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the integration configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the integration configuration does not exist, this call returns an error. If the integration configuration cannot be deleted, this call will return an error with a message indicating the problem.

#### List all integration configurations

```
DEFINITION
GET http://apiserver/integrationconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/integrationconfigurations");

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
            "code": "TOKENEX",
            "description": "TokenEx Configuration",
            "type": "TOKENEX",
            "typeDescription": "TokenEx Integration",
            "typeCategory": "TOKENVAULT",
            "typeCategoryDescription": "Token Vault",
            "configuration": "{\"Id\":\"12345\",\"ApiKey\":\"abc123\",\"Url\":\"https://test-api.tokenex.com\",\"EncryptionProfile\":\"test_data\"}",
            "prototype": {
                "id": "TOKENEX",
                "configuration": "{\"ApiKey\":\"Default ApiKey\"}"
            }
        },
        {...},
    ]
}

```

Returns a list of all integration configurations.

##### Returns

A dictionary with an items property that contains an array of up to limit integration configurations, starting at index offset. Each entry in the array is a separate integration configuration object. If no more integration configurations are available, the resulting array will be empty. This request should never return an error.

### Integration Configuration Prototypes

#### Retrieve an integration configuration prototype

```
DEFINITION
GET http://apiserver/integrationconfigurationprototypes/{id}

EXAMPLE REQUEST
$.get("http://localhost:49195/integrationconfigurationprototypes/CYB_SOURCE");

EXAMPLE RESPONSE
{
    "id": "CYB_SOURCE",
    "configuration": "{\"TokenVaultCode\":\"Default TokenVaultCode\"}"
}

```

Retrieves the details of an existing integration configuration prototype. You need only supply the id.

##### Arguments

* id (required) - The id of the integration configuration to be retrieved.

### Insert Code Rules

#### Create a Insert Code Rule

```
DEFINITION
POST http://apiserver/insertcoderules

EXAMPLE REQUEST
$.post("http://localhost:49195/insertcoderules", {
    "type": "P",
    "sequence": 10,
    "description": "Son Minstry Info - Insert",
    "sqlStatement": "SELECT * FROM  dbo.T01_TransactionMaster T01 WITH (NOLOCK) JOIN \r\n              dbo.T03_OrderDetails t03 WITH (NOLOCK) ON T01.DocumentNumber = t03.DocumentNumber\r\n WHERE T01.DocumentNumber = #DOCUMENT_NUMBER# and \r\n t03.ProductCode = 'SONINFO'",
    "insertCode": "INFO",
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "P",
    "sequence": 10,
    "description": "Son Minstry Info - Insert",
    "sqlStatement": "SELECT * FROM  dbo.T01_TransactionMaster T01 WITH (NOLOCK) JOIN \r\n              dbo.T03_OrderDetails t03 WITH (NOLOCK) ON T01.DocumentNumber = t03.DocumentNumber\r\n WHERE T01.DocumentNumber = #DOCUMENT_NUMBER# and \r\n t03.ProductCode = 'SONINFO'",
    "insertCode": "INFO",
    "insertCodeDescription": "Son Ministry - Info Insert"
}

```

Creates a new Insert Code Rule.

##### Arguments

* type (required) - The Primary or Second Party Indicator. Can be P or 2.
* sequence (required) - The sequence of the Insert Code.
* description (required) - The description of the Letter Code Priority.
* sqlStatement (optional) - SQL to run to help assign Letter Codes automatically.
* insertCode (required) - The Insert Code that this Rule is associated with.

##### Returns

Returns a Insert Code Rule object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Insert Code Rule

```
DEFINITION
GET http://apiserver/insertcoderules/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/insertcoderules/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "P",
    "sequence": 10,
    "description": "Son Minstry Info - Insert",
    "sqlStatement": "SELECT * FROM  dbo.T01_TransactionMaster T01 WITH (NOLOCK) JOIN \r\n              dbo.T03_OrderDetails t03 WITH (NOLOCK) ON T01.DocumentNumber = t03.DocumentNumber\r\n WHERE T01.DocumentNumber = #DOCUMENT_NUMBER# and \r\n t03.ProductCode = 'SONINFO'",
    "insertCode": "INFO",
    "insertCodeDescription": "Son Ministry - Info Insert"
}

```

Retrieves the details of an existing Insert Code Rule. You need only supply the id.

##### Arguments

* id (required) - The id of the Insert Code Rule to be retrieved.

#### Update a Insert Code Rule

```
DEFINITION
POST http://apiserver/insertcoderules/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/insertcoderules/1", {
    "type": "P",
    "sequence": 10,
    "description": "Son Minstry Info - Insert",
    "sqlStatement": "SELECT * FROM  dbo.T01_TransactionMaster T01 WITH (NOLOCK) JOIN \r\n              dbo.T03_OrderDetails t03 WITH (NOLOCK) ON T01.DocumentNumber = t03.DocumentNumber\r\n WHERE T01.DocumentNumber = #DOCUMENT_NUMBER# and \r\n t03.ProductCode = 'SONINFO'",
    "insertCode": "INFO",
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "P",
    "sequence": 10,
    "description": "Son Minstry Info - Insert",
    "sqlStatement": "SELECT * FROM  dbo.T01_TransactionMaster T01 WITH (NOLOCK) JOIN \r\n              dbo.T03_OrderDetails t03 WITH (NOLOCK) ON T01.DocumentNumber = t03.DocumentNumber\r\n WHERE T01.DocumentNumber = #DOCUMENT_NUMBER# and \r\n t03.ProductCode = 'SONINFO'",
    "insertCode": "INFO",
    "insertCodeDescription": "Son Ministry - Info Insert"
}


```

Updates the specified Insert Code Rule setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type () - The Primary or Second Party Indicator. Can be P or 2.
* sequence () - The sequence of the Insert Code.
* description () - The description of the Letter Code Priority.
* sqlStatement () - SQL to run to help assign Letter Codes automatically.
* insertCode () - The Insert Code that this Rule is associated with.

##### Returns

Returns the Insert Code Rule if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Insert Code Rule

```
DEFINITION
DELETE http://apiserver/insertcoderules/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/insertcoderules/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Insert Code Rule. It cannot be undone.

##### Arguments

* id (required) - The id of the Insert Code Rule to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Insert Code Rule does not exist, this call returns an error.

#### List all Insert Code Rules

```
DEFINITION
GET http://apiserver/insertcoderules

EXAMPLE REQUEST
$.get("http://localhost:49195/insertcoderules?");

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
            "type": "P",
            "sequence": 10,
            "description": "Son Minstry Info - Insert",
            "sqlStatement": "SELECT * FROM  dbo.T01_TransactionMaster T01 WITH (NOLOCK) JOIN \r\n              dbo.T03_OrderDetails t03 WITH (NOLOCK) ON T01.DocumentNumber = t03.DocumentNumber\r\n WHERE T01.DocumentNumber = #DOCUMENT_NUMBER# and \r\n t03.ProductCode = 'SONINFO'",
            "insertCode": "INFO",
            "insertCodeDescription": "Son Ministry - Info Insert"
        },
        {...},
    ]
}

```

Returns a list of all Insert Code Rules.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* description (optional) - The description of the Letter Code Priority.
* type (optional) - The Primary or Second Party Indicator. Can be P or 2.

##### Returns

A dictionary with an items property that contains an array of up to limit Insert Code Rules, starting at index offset. Each entry in the array is a separate Insert Code Rule object. If no more Insert Code Rules are available, the resulting array will be empty. This request should never return an error.

### Letter Code Priorities

#### Create a Letter Code Priority

```
DEFINITION
POST http://apiserver/lettercodepriorities

EXAMPLE REQUEST
$.post("http://localhost:49195/lettercodepriorities", {
    "type": "2",
    "priority": 10,
    "table": "X01,
    "description": "LARGEBB > $5000",
    "sqlStatement": "SELECT t01.DocumentNumber FROM dbo.T01_TransactionMaster t01 WITH (NOLOCK)
JOIN dbo.T04_GiftDetails t04 WITH (NOLOCK) ON t01.DocumentNumber = t04.DocumentNumber
WHERE  t04.TotalAmount >= 5000 and t01.DocumentNumber = #DOCUMENT_NUMBER#",
    "letterCode": "NORECPT",
    "letterCodeAlt1": "NORECPT",
    "letterCodeAlt2": null,
    "letterCodeAlt3": null,
    "letterCodeAlt4": null,
});

EXAMPLE RESPONSE
{
    "id": "94",
    "type": "2",
    "priority": 10,
    "table": "X01,
    "description": "LARGEBB > $5000",
    "sqlStatement": "SELECT t01.DocumentNumber FROM dbo.T01_TransactionMaster t01 WITH (NOLOCK)
JOIN dbo.T04_GiftDetails t04 WITH (NOLOCK) ON t01.DocumentNumber = t04.DocumentNumber
WHERE  t04.TotalAmount >= 5000 and t01.DocumentNumber = #DOCUMENT_NUMBER#",
    "letterCode": "NORECPT",
    "letterCodeAlt1": "NORECPT",
    "letterCodeAlt1Description": "No Receipt (Do Not Print)",
    "letterCodeAlt2": null,
    "letterCodeAlt2Description": null,
    "letterCodeAlt3": null,
    "letterCodeAlt3Description": null,
    "letterCodeAlt4": null,
    "letterCodeAlt4Description": null
}

```

Creates a new Letter Code Priority.

##### Arguments

* type (required) - The Primary or Second Party Indicator. Can be P or 2.
* priority (required) - The priority of the Letter Code.
* table (required) - The table that the Second Party points to. Has to be null for P and populated for 2.
* description (required) - The description of the Letter Code Priority.
* sqlStatement (optional) - SQL to run to help assign Letter Codes automatically.
* letterCode (required) - The Letter Code that this Priority is associated with.
* letterCodeAlt1 (optional) - The 1st Letter Code Alternate that this Priority is associated with.
* letterCodeAlt2 (optional) - The 2nd Letter Code Alternate that this Priority is associated with.
* letterCodeAlt3 (optional) - The 3rd Letter Code Alternate that this Priority is associated with.
* letterCodeAlt4 (optional) - The 4th Letter Code Alternate that this Priority is associated with.

##### Returns

Returns a Letter Code Priority object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Letter Code Priority

```
DEFINITION
GET http://apiserver/lettercodepriorities/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/lettercodepriorities/94");

EXAMPLE RESPONSE
{
    "id": "94",
    "type": "2",
    "priority": 10,
    "table": "X01,
    "description": "LARGEBB > $5000",
    "sqlStatement": "SELECT t01.DocumentNumber FROM dbo.T01_TransactionMaster t01 WITH (NOLOCK)
JOIN dbo.T04_GiftDetails t04 WITH (NOLOCK) ON t01.DocumentNumber = t04.DocumentNumber
WHERE  t04.TotalAmount >= 5000 and t01.DocumentNumber = #DOCUMENT_NUMBER#",
    "letterCode": "NORECPT",
    "letterCodeAlt1": "NORECPT",
    "letterCodeAlt1Description": "No Receipt (Do Not Print)",
    "letterCodeAlt2": null,
    "letterCodeAlt2Description": null,
    "letterCodeAlt3": null,
    "letterCodeAlt3Description": null,
    "letterCodeAlt4": null,
    "letterCodeAlt4Description": null
}

```

Retrieves the details of an existing Letter Code Priority. You need only supply the id.

##### Arguments

* id (required) - The id of the Letter Code Priority to be retrieved.

#### Update a Letter Code Priority

```
DEFINITION
POST http://apiserver/lettercodepriorities/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/lettercodepriorities/94", {
    "id": "94",
    "type": "2",
    "priority": 10,
    "table": "X01,
    "description": "LARGEBB > $5000",
    "sqlStatement": "SELECT t01.DocumentNumber FROM dbo.T01_TransactionMaster t01 WITH (NOLOCK)
JOIN dbo.T04_GiftDetails t04 WITH (NOLOCK) ON t01.DocumentNumber = t04.DocumentNumber
WHERE  t04.TotalAmount >= 5000 and t01.DocumentNumber = #DOCUMENT_NUMBER#",
    "letterCode": "NORECPT",
    "letterCodeAlt1": "NORECPT",
    "letterCodeAlt1Description": "No Receipt (Do Not Print)",
    "letterCodeAlt2": null,
    "letterCodeAlt2Description": null,
    "letterCodeAlt3": null,
    "letterCodeAlt3Description": null,
    "letterCodeAlt4": null,
    "letterCodeAlt4Description": null
});

EXAMPLE RESPONSE
{
    "id": "94",
    "type": "2",
    "priority": 10,
    "table": "X01,
    "description": "LARGEBB > $5000",
    "sqlStatement": "SELECT t01.DocumentNumber FROM dbo.T01_TransactionMaster t01 WITH (NOLOCK)
JOIN dbo.T04_GiftDetails t04 WITH (NOLOCK) ON t01.DocumentNumber = t04.DocumentNumber
WHERE  t04.TotalAmount >= 5000 and t01.DocumentNumber = #DOCUMENT_NUMBER#",
    "letterCode": "NORECPT",
    "letterCodeAlt1": "NORECPT",
    "letterCodeAlt1Description": "No Receipt (Do Not Print)",
    "letterCodeAlt2": null,
    "letterCodeAlt2Description": null,
    "letterCodeAlt3": null,
    "letterCodeAlt3Description": null,
    "letterCodeAlt4": null,
    "letterCodeAlt4Description": null
}


```

Updates the specified Letter Code Priority by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The id of the Letter Code Priority to be retrieved.
* type (required) - The Primary or Second Party Indicator. Can be P or 2.
* priority (required) - The priority of the Letter Code.
* table (required) - The table that the Second Party points to. Has to be null for P and populated for 2.
* description (required) - The description of the Letter Code Priority.
* sqlStatement (optional) - SQL to run to help assign Letter Codes automatically.
* letterCode (required) - The Letter Code that this Priority is associated with.
* letterCodeAlt1 (optional) - The 1st Letter Code Alternate that this Priority is associated with.
* letterCodeAlt2 (optional) - The 2nd Letter Code Alternate that this Priority is associated with.
* letterCodeAlt3 (optional) - The 3rd Letter Code Alternate that this Priority is associated with.
* letterCodeAlt4 (optional) - The 4th Letter Code Alternate that this Priority is associated with.

##### Returns

Returns the Letter Code Priority object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Letter Code Priority

```
DEFINITION
DELETE http://apiserver/lettercodepriorities/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/lettercodepriorities/94", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Letter Code Priority. It cannot be undone.

##### Arguments

* id (required) - The id of the Letter Code Priority to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Letter Code Priority does not exist, this call returns an error.

#### List all Letter Code Priorities

```
DEFINITION
GET http://apiserver/lettercodepriorities

EXAMPLE REQUEST
$.get("http://localhost:49195/lettercodepriorities?description='Happy'&type='2'");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "94",
            "type": "2",
            "priority": 10,
            "table": "X01,
            "description": "LARGEBB > $5000",
            "sqlStatement": "SELECT t01.DocumentNumber FROM dbo.T01_TransactionMaster t01 WITH (NOLOCK)
        JOIN dbo.T04_GiftDetails t04 WITH (NOLOCK) ON t01.DocumentNumber = t04.DocumentNumber
        WHERE  t04.TotalAmount >= 5000 and t01.DocumentNumber = #DOCUMENT_NUMBER#",
            "letterCode": "NORECPT",
            "letterCodeAlt1": "NORECPT",
            "letterCodeAlt1Description": "No Receipt (Do Not Print)",
            "letterCodeAlt2": null,
            "letterCodeAlt2Description": null,
            "letterCodeAlt3": null,
            "letterCodeAlt3Description": null,
            "letterCodeAlt4": null,
            "letterCodeAlt4Description": null
        },
        {...},
    ]
}

```

Returns a list of all Letter Code Priorities.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* description (optional) - The description of the Letter Code Priority.
* type (optional) - The Primary or Second Party Indicator. Can be P or 2.

##### Returns

A dictionary with an items property that contains an array of up to limit Letter Code Priorities, starting at index offset. Each entry in the array is a separate Letter Code Priority object. If no more Letter Code Priorities are available, the resulting array will be empty. This request should never return an error.

### Paragraph Codes

#### Create a Paragraph Code

```
DEFINITION
POST http://apiserver/paragraphcodes

EXAMPLE REQUEST
$.post("http://localhost:49195/paragraphcodes", {
    "id": "A01",
    "description": "Need Birth Dates and Names",
    "instructions": null,
    "completionTextProcessing": "NONE",
    "completionText": null,
    "topic": null,
    "category": null,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "A01",
    "description": "Need Birth Dates and Names",
    "instructions": null,
    "completionTextProcessing": "NONE",
    "completionText": null,
    "topic": null,
    "category": null,
    "isActive": true
}

```

Creates a new paragraph code.

##### Arguments

* paragraphCode (required) - paragraph code
* completionTextProcessing (required; default `NONE`) - completion text processing
* description (optional) - description
* instructions (optional) - instructions
* completionText (optional) - completion text
* topic (optional) - topic
* category (optional) - paragraph code category
* isActive (optional; default `true`) - specifies if paragraph code is active

##### Returns

Returns a paragraph code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Paragraph Code

```
DEFINITION
GET http://apiserver/paragraphcode/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/paragraphcode/A01");

EXAMPLE RESPONSE
{
    "id": "A01",
    "description": "Need Birth Dates and Names",
    "instructions": null,
    "completionTextProcessing": "NONE",
    "completionText": null,
    "topic": null,
    "category": null,
    "isActive": true
}

```

Retrieves the details of an existing Paragraph Code. You need only supply the id.

##### Arguments

* id (required) - The id of the Paragraph Code to be retrieved.

#### Update a Paragraph Code

```
DEFINITION
POST http://apiserver/paragraphcodes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/paragraphcodes/A01", {
            "id": "A01",
            "description": "Need Birth Dates and Names",
            "instructions": null,
            "completionTextProcessing": "NONE",
            "completionText": null,
            "topic": null,
            "category": null,
            "isActive": true});

EXAMPLE RESPONSE
{
            "id": "A01",
            "description": "Need Birth Dates and Names",
            "instructions": null,
            "completionTextProcessing": "NONE",
            "completionText": null,
            "topic": null,
            "category": null,
            "isActive": true
}

```

Updates the specified Paragraph Code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* paragraphCode (required) - paragraph code
* description (required) - description
* instructions (optional) - instructions
* completionTextProcessing (required) - completion text processing
* category (optional) - category
* topic (optional) - topic
* isActive (optional; default `true`) - specifies if user is active

##### Returns

Returns the Paragraph Code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Paragraph Code

```
DEFINITION
DELETE http://apiserver/paragraphcodes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/paragraphcodes/A01", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Paragraph Code. It cannot be undone.

##### Arguments

* id (required) - The id of the Paragraph Code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Paragraph Code does not exist, this call returns an error.

#### List all Paragraph Codes

```
DEFINITION
GET http://apiserver/pargraphcodes

EXAMPLE REQUEST
$.get("http://localhost:49195/pargraphcodes?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "A01",
            "description": "Need Birth Dates and Names",
            "instructions": null,
            "completionTextProcessing": "NONE",
            "completionText": null,
            "topic": null,
            "category": null,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all Paragraph Codes.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in paragraph code
* category () - Filter list by partial match in category
* completionText () - Filter list by partial match in completion text
* description () - Filter list by partial match in description
* isActive () - Filter list by whether active or not
* topic () - Filter list by partial match in topic

##### Returns

A dictionary with an items property that contains an array of up to limit paragraph codes, starting at index offset. Each entry in the array is a separate paragraph code object. If no more paragraph codes are available, the resulting array will be empty. This request should never return an error.

### Payment Gateway Configuration

#### Retrieve Transaction Payment Gateway Configuration

```
DEFINITION
GET http://apiserver/transaction/paymentgatewayconfiguration

EXAMPLE REQUEST
$.get("http://localhost:49195/transaction/paymentgatewayconfiguration?companyCode=1&paymentGatewayCode=CARDCONNCT");

EXAMPLE RESPONSE
{
    "companyCode": "1",
    "creditCardProvider": "CCONNECT",
    "creditCardPaymentGatewayCode": "CARDCONNCT",
    "eftProvider": "CCONNECT",
    "eftPaymentGatewayCode": "CARDCONNCT",
    "shouldUseEncryptedCreditCard": true,
    "supportsUpdateCreditCardExpirationDateOnly": false,
    "shouldTokenizeEft": true
}

```

Retrieves the details of a Transaction Payment Gateway Configuration.

##### Arguments

* company (required) - The id of the Company of Transaction Payment Gateway Configuration to be retrieved.
* paymentGatewayCode (optional) - The code of the company payment gateway for which to retrieve both the credit card and EFT configuration. If this is not provided the configuration for the default credit card and default eft payment gateways for the company will returned.
* creditCardPaymentGatewayCode (optional) - The code of the company payment gateway for which to retrieve credit card configuration. For credit card configuration, this will overwrite the paymentGatewayCode parameter.
* eftPaymentGatewayCode (optional) - The code of the company payment gateway for which to retrieve EFT configuration. For EFT configuration, this will overwrite the paymentGatewayCode parameter.

### Postal Codes

#### Create a postal code

```
DEFINITION
POST http://apiserver/postalcodes

EXAMPLE REQUEST
$.post("http://localhost:49195/postalcodes", {
    "country": "required",
    "postalCodeLow": "78628",
    "postalCodeHigh": "78628-9999",
    "city": "Georgetown",
    "state": "TX",
    "county": "",
    "latitude": 30.8431,
    "longitude": 97.7954
});

EXAMPLE RESPONSE
{
    "id": "35471",
    "country": "USA",
    "postalCodeLow": "78628",
    "postalCodeHigh": "78628-9999",
    "city": "Georgetown",
    "state": "TX",
    "county": "",
    "latitude": 30.8431,
    "longitude": 97.7954
}

```

Creates a new postal code.

##### Arguments

* country (required)
* postalCodeLow (required)
* postalCodeHigh (required)
* city (optional)
* state (optional)
* county (optional)
* latitude (optional)
* longitude (optional)

##### Returns

Returns a postal code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a postal code

```
DEFINITION
GET http://apiserver/postalcodes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/postalcodes/35471");

EXAMPLE RESPONSE
{
    "id": "35471",
    "country": "USA",
    "postalCodeLow": "78628",
    "postalCodeHigh": "78628-9999",
    "city": "Georgetown",
    "state": "TX",
    "county": "",
    "latitude": 30.8431,
    "longitude": 97.7954
}

```

Retrieves the details of an existing postal code. You need only supply the id.

##### Arguments

* id (required) - The id of the postal code to be retrieved.

##### Returns

Returns a postal code object if a valid id was provided.

#### Update a postal code

```
DEFINITION
POST http://apiserver/postalcodes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/postalcodes/35471", {
    "county": "Williamson"
});

EXAMPLE RESPONSE
{
    "id": "35471",
    "country": "USA",
    "postalCodeLow": "78628",
    "postalCodeHigh": "78628-9999",
    "city": "Georgetown",
    "state": "TX",
    "county": "Williamson",
    "latitude": 30.8431,
    "longitude": 97.7954
}


```

Updates the specified postal code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* country (optional)
* postalCodeLow (optional)
* postalCodeHigh (optional)
* city (optional)
* state (optional)
* county (optional)
* latitude (optional)
* longitude (optional)

##### Returns

Returns the postal code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a postal code

```
DEFINITION
DELETE http://apiserver/postalcodes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/postalcodes/35471", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a postal code. It cannot be undone.

##### Arguments

* id (required) - The id of the postal code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the postal code does not exist, this call returns an error.

#### List all postal codes

```
DEFINITION
GET http://apiserver/postalcodes

EXAMPLE REQUEST
$.get("http://localhost:49195/postalcodes?country=USA&city=Georgetown");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "35469",
            "country": "USA",
            "postalCodeLow": "78626",
            "postalCodeHigh": "78626-9999",
            "city": "Georgetown",
            "state": "TX",
            "county": "",
            "latitude": 30.6337,
            "longitude": 97.679
        },
        {...},
    ]
}

```

Returns a list of all postal codes.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Returns

A dictionary with an items property that contains an array of up to limit postal codes, starting at index offset. Each entry in the array is a separate postal code object. If no more postal codes are available, the resulting array will be empty. This request should never return an error.

### Postal Code Media Assignment

#### Create a postal code media assignment

```
DEFINITION
POST http://apiserver/postalcodes/:id/mediaassignments

EXAMPLE REQUEST
$.post("http://localhost:49195/postalcodes/33617/mediaassignments", {
    "id": "KBDE",
    "distributionPercent": 33
});

EXAMPLE RESPONSE
{
    "id": "KBDE",
    "distributionPercent": 33,
    "description": "KBDE 88.4 Stockton, CA"
}

```

Creates a new postal code media assignment.

##### Arguments

* id (required) - the media outlet
* distributionPercent (optional; defaults to `0`) - the distribution percentage

##### Returns

Returns a postal code media assignment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a postal code media assignment

```
DEFINITION
GET http://apiserver/postalcodes/:id/mediaassignments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/postalcodes/33617/mediaassignments/KBDE");

EXAMPLE RESPONSE
{
    "id": "KBDE",
    "distributionPercent": 33,
    "description": "KBDE 88.4 Stockton, CA"
}

```

Retrieves the details of an existing postal code media assignment. You need only supply the id.

##### Arguments

* id (required) - The id of the postal code media assignment to be retrieved.

#### Update a postal code media assignment

```
DEFINITION
POST http://apiserver/postalcodes/:id/mediaassignments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/postalcodes/33617/mediaassignments/KBDE", {
    "distributionPercent": 50
});

EXAMPLE RESPONSE
{
    "id": "KBDE",
    "distributionPercent": 50,
    "description": "KBDE 88.4 Stockton, CA"
}


```

Updates the specified postal code media assignment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - the media outlet
* distributionPercent (optional) - the distribution percent

##### Returns

Returns the postal code media assignment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a postal code media assignment

```
DEFINITION
DELETE http://apiserver/postalcodes/:id/mediaassignments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/postalcodes/33617/mediaassignments/KBDE", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a postal code media assignment. It cannot be undone.

##### Arguments

* id (required) - The id of the postal code media assignment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the postal code media assignment does not exist, this call returns an error.

#### List all postal code media assignments

```
DEFINITION
GET http://apiserver/postalcodes/:id/mediaassignments

EXAMPLE REQUEST
$.get("http://localhost:49195/postalcodes/33617/mediaassignments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "KBDE",
            "distributionPercent": 33,
            "description": "KBDE 88.4 Stockton, CA"
        },
        {...},
    ]
}

```

Returns a list of all postal code media assignments.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit postal code media assignments, starting at index offset. Each entry in the array is a separate postal code media assignment object. If no more postal code media assignments are available, the resulting array will be empty. This request should never return an error.

### Postal Code Media Search

#### List all postal code media

```
DEFINITION
GET http://apiserver/postalcodemedia/

EXAMPLE REQUEST
$.get("http://localhost:49195/postalcodemedia?state=CA");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "KBDE",
            "description": "KBDE 88.4 Stockton, CA",
            "mediaFrequency": "88.4"
        },
        {...},
    ]
}

```

Returns a list of all postal code media assignments.

##### Arguments

* postalCode (optional) - Filter list by postal code. Must be exact postal code. Does a between search between X08.PostalCodeLow and X08.PostalCodeHigh.
* city (optional) - Filter list by partial match of city.
* state (optional) - Filter list by partial match of state.
* country (optional) - Filter list by match of country. Must be exact country code.
* description (optional) - Filter list by partial match of description.
* mediaFrequency (optional) - Filter list by partial match of media frequency.
* alias (optional) - Filter list by partial match of media alias. Searches the M02.Description.
* currentMedia (optional) - Will return media with id of currentMedia regardless of the filter criteria. The filtered results will be returned as well.

##### Returns

A dictionary with an items property that contains an array of up to limit postal code medias, starting at index offset. Each entry in the array is a separate postal code media object. If no more postal code medias are available, the resulting array will be empty. This request should never return an error.

### Postal Codes Update Codes For A Range

#### Update Codes For a Postal Code Range

```
DEFINITION
POST http://apiserver/postalcodes/updatecodesforrange

EXAMPLE REQUEST
$.post("http://localhost:49195/postalcodes/updatecodesforrange", {
    country: "USA"
    postalCodeLow: "78626"
    postalCodeHigh: "78628"
    action: "ADD"
    codeType: "CAHDIST"
    codeValue: "0001"
    autoAdd: true
});

EXAMPLE RESPONSE
204 NO CONTENT

```

Provides the ability to manage codes in bulk for a range of postal codes.

##### Arguments

* country (required)
* postalCodeLow (required)
* postalCodeHigh (required)
* action (required) - allowed values are `ADD`, `UPDATE`, `DELETE`
* codeType (required)
* codeValue (required)
* originalCodeType (required when `action=UPDATE`)
* originalCodeValue (required when `action=UPDATE`)
* autoAdd (optional)

##### Returns

Returns a `204 NO CONTENT` if the call succeeded. Returns an error if create parameters are invalid.

### Postal Codes Update Media For A Range

#### Update Media For a Postal Code Range

```
DEFINITION
POST http://apiserver/postalcodes/updatemediaforrange

EXAMPLE REQUEST
$.post("http://localhost:49195/postalcodes/updatemediaforrange", {
    "country": "USA",
    "postalCodeLow": "78626",
    "postalCodeHigh": "78628",
    "action": "UPDATE",
    "mediaCode": "KAMY",
    "distributionPercent": "80"
});

EXAMPLE RESPONSE
204 NO CONTENT

```

Provides the ability to manage media codes in bulk for a range of postal codes.

##### Arguments

* country (required)
* postalCodeLow (required)
* postalCodeHigh (required)
* action (required) - allowed values are `ADD`, `UPDATE`, `DELETE`
* mediaCode (required)
* distributionPercent (required)

##### Returns

Returns a `204 NO CONTENT` if the call succeeded. Returns an error if create parameters are invalid.

### Profiles

#### Create a profile

```
DEFINITION
POST http://apiserver/profiles

EXAMPLE REQUEST
$.post("http://localhost:49195/profiles", {
    "importVersion": "PROD",
    "description": "Production",
    "wsiUrl": "http://localhost:12345/index.asmx",
    "wsiUsername": "user@website.com",
    "wsiPassword": "password",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "1",
    "importVersion": "PROD",
    "description": "Production",
    "wsiUrl": "http://localhost:12345/index.asmx",
    "wsiUsername": "user@website.com",
    "wsiPassword": "password",
    "isActive": true
}

```

Creates a new profile.

##### Arguments

* importVersion () - Import Version
* description () - Description
* wsiUrl () - Wsi Url
* wsiUsername () - Wsi Username
* wsiPassword () - Wsi Password
* isActive (required) - Active Indicator

##### Returns

Returns a profile object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a profile

```
DEFINITION
GET http://apiserver/profiles/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/profiles/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "importVersion": "PROD",
    "description": "Production",
    "wsiUrl": "http://localhost:12345/index.asmx",
    "wsiUsername": "user@website.com",
    "wsiPassword": "password",
    "isActive": true
}

```

Retrieves the details of an existing profile. You need only supply the id.

##### Arguments

* id (required) - The id of the profile to be retrieved.

#### Update a profile

```
DEFINITION
POST http://apiserver/profiles/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/profiles/1", {
    "importVersion": "PROD",
    "description": "Production",
    "wsiUrl": "http://localhost:12345/index.asmx",
    "wsiUsername": "user@website.com",
    "wsiPassword": "password",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "1",
    "importVersion": "PROD",
    "description": "Production",
    "wsiUrl": "http://localhost:12345/index.asmx",
    "wsiUsername": "user@website.com",
    "wsiPassword": "password",
    "isActive": true
}


```

Updates the specified profile by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* importVersion () - Import Version
* description () - Description
* wsiUrl () - Wsi Url
* wsiUsername () - Wsi Username
* wsiPassword () - Wsi Password
* isActive () - Active Indicator

##### Returns

Returns the profile object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a profile

```
DEFINITION
DELETE http://apiserver/profiles/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/profiles/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a profile. It cannot be undone.

##### Arguments

* id (required) - The id of the profile to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the profile does not exist, this call returns an error.

#### List all profiles

```
DEFINITION
GET http://apiserver/profiles

EXAMPLE REQUEST
$.get("http://localhost:49195/profiles?");

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
            "importVersion": "PROD",
            "description": "Production",
            "wsiUrl": "http://localhost:12345/index.asmx",
            "wsiUsername": "user@website.com",
            "wsiPassword": "password",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all profiles.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* importVersion () - Import Version
* description () - Description
* isActive () - Active Indicator

##### Returns

A dictionary with an items property that contains an array of up to limit profiles, starting at index offset. Each entry in the array is a separate profile object. If no more profiles are available, the resulting array will be empty. This request should never return an error.

### Profile Stores

#### Create a profile store

```
DEFINITION
POST http://apiserver/profiles/:id/stores

EXAMPLE REQUEST
$.post("http://localhost:49195/profiles/1/stores", {
    "store": "7"
});

EXAMPLE RESPONSE
{
    "id": "10",
    "store": "7"
}

```

Creates a new profile store.

##### Arguments

* store () - Store Id

##### Returns

Returns a profile store object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a profile store

```
DEFINITION
GET http://apiserver/profiles/:id/stores/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/profiles/1/stores/10");

EXAMPLE RESPONSE
{
    "id": "10",
    "store": "7"
}

```

Retrieves the details of an existing profile store. You need only supply the id.

##### Arguments

* id (required) - The id of the profile store to be retrieved.

#### Update a profile store

```
DEFINITION
POST http://apiserver/profiles/:id/stores/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/profiles/1/stores/10", {
    "store": "7"
});

EXAMPLE RESPONSE
{
    "id": "10",
    "store": "7"
}


```

Updates the specified profile store by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* store () - Store Id

##### Returns

Returns the profile store object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a profile store

```
DEFINITION
DELETE http://apiserver/profiles/:id/stores/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/profiles/1/stores/10", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a profile store. It cannot be undone.

##### Arguments

* id (required) - The id of the profile store to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the profile store does not exist, this call returns an error.

#### List all profile stores

```
DEFINITION
GET http://apiserver/profiles/:id/stores

EXAMPLE REQUEST
$.get("http://localhost:49195/profiles/1/stores?");

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
            "store": "7"
        },
        {...},
    ]
}

```

Returns a list of all profile stores.

##### Returns

A dictionary with an items property that contains an array of up to limit profile stores, starting at index offset. Each entry in the array is a separate profile store object. If no more profile stores are available, the resulting array will be empty. This request should never return an error.

### Profile Store Attributes

#### Create a profile store attribute

```
DEFINITION
POST http://apiserver/profiles/:id/stores/:id/attributes

EXAMPLE REQUEST
$.post("http://localhost:49195/profiles/1/stores/10/attributes", {
    "attributeType": "PLGAMOUNTS",
    "attributeValue": "SEECOMMENT",
    "description": "Default Pledge Amount Options",
    "comment": "25.00,50.00,100.00"
});

EXAMPLE RESPONSE
{
    "id": "27",
    "attributeType": "PLGAMOUNTS",
    "attributeTypeDescription": "Pledge Default Amounts",
    "attributeValue": "SEECOMMENT",
    "description": "Default Pledge Amount Options",
    "comment": "25.00,50.00,100.00"
}

```

Creates a new profile store attribute.

##### Arguments

* attributeType (required) - Attribute Type
* attributeValue (required) - Attribute Value
* description (required) - Description
* comment () - Comment

##### Returns

Returns a profile store attribute object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a profile store attribute

```
DEFINITION
GET http://apiserver/profiles/:id/stores/:id/attributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/profiles/1/stores/10/attributes/27");

EXAMPLE RESPONSE
{
    "id": "27",
    "attributeType": "PLGAMOUNTS",
    "attributeTypeDescription": "Pledge Default Amounts",
    "attributeValue": "SEECOMMENT",
    "description": "Default Pledge Amount Options",
    "comment": "25.00,50.00,100.00"
}

```

Retrieves the details of an existing profile store attribute. You need only supply the id.

##### Arguments

* id (required) - The id of the profile store attribute to be retrieved.

#### Update a profile store attribute

```
DEFINITION
POST http://apiserver/profiles/:id/stores/:id/attributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/profiles/1/stores/10/attributes/27", {
    "attributeType": "PLGAMOUNTS",
    "attributeValue": "SEECOMMENT",
    "description": "Default Pledge Amount Options",
    "comment": "25.00,50.00,100.00"
});

EXAMPLE RESPONSE
{
    "id": "27",
    "attributeType": "PLGAMOUNTS",
    "attributeTypeDescription": "Pledge Default Amounts",
    "attributeValue": "SEECOMMENT",
    "description": "Default Pledge Amount Options",
    "comment": "25.00,50.00,100.00"
}


```

Updates the specified profile store attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* attributeType () - Attribute Type
* attributeValue () - Attribute Value
* description () - Description
* comment () - Comment

##### Returns

Returns the profile store attribute object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a profile store attribute

```
DEFINITION
DELETE http://apiserver/profiles/:id/stores/:id/attributes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/profiles/1/stores/10/attributes/27", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a profile store attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the profile store attribute to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the profile store attribute does not exist, this call returns an error.

#### List all profile store attributes

```
DEFINITION
GET http://apiserver/profiles/:id/stores/:id/attributes

EXAMPLE REQUEST
$.get("http://localhost:49195/profiles/1/stores/10/attributes?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "27",
            "attributeType": "PLGAMOUNTS",
            "attributeTypeDescription": "Pledge Default Amounts",
            "attributeValue": "SEECOMMENT",
            "description": "Default Pledge Amount Options",
            "comment": "25.00,50.00,100.00"
        },
        {...},
    ]
}

```

Returns a list of all profile store attributes.

##### Returns

A dictionary with an items property that contains an array of up to limit profile store attributes, starting at index offset. Each entry in the array is a separate profile store attribute object. If no more profile store attributes are available, the resulting array will be empty. This request should never return an error.

### Studio Online Bulk Publishings

#### Retrieve a studio online bulk publishing

```
DEFINITION
GET http://apiserver/studioonlinebulkpublishing/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinebulkpublishing/Project|050098");

EXAMPLE RESPONSE
{
    "id": "Pledge|050098",
    "entityType": "Pledge",
    "entityCode": "050098",
    "description": "Mark McLemore Outreach 2012",
    "type": "CHILD",
    "updated": false,
    "useInStudioOnline": false,
    "publishable": false,
    "autoGenerateDescription": false,
    "missingData": "Project"
}

```

Retrieves the details of an existing studio online bulk publishing. You need only supply the id.

##### Arguments

* id (required) - The id of the studio online bulk publishing to be retrieved.

#### List all studio online bulk publishings

```
DEFINITION
GET http://apiserver/studioonlinebulkpublishing

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinebulkpublishing?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "Pledge|050098",
            "entityType": "Pledge",
            "entityCode": "050098",
            "description": "Mark McLemore Outreach 2012",
            "type": "CHILD",
            "updated": false,
            "useInStudioOnline": false,
            "publishable": false,
            "autoGenerateDescription": false,
            "missingData": "Project"
        },
        {...},
    ]
}

```

Returns a list of all studio online bulk publishings.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* entityType () - Entity Type
* entityCodeRange.Low () - Entity Code Lower Limit
* entityCodeRange.High () - Entity Code Upper Limit
* type () - Type
* description () - Description
* updated () - Updated Indicator
* useInStudioOnline () - Use in Studio Online Indicator
* autoGenerateDescription () - Auto Generate Description Indicator
* publishable () - Publishable Indicator

##### Returns

A dictionary with an items property that contains an array of up to limit studio online bulk publishings, starting at index offset. Each entry in the array is a separate studio online bulk publishing object. If no more studio online bulk publishings are available, the resulting array will be empty. This request should never return an error.

#### Process studio online bulk publishings

```
DEFINITION
POST http://apiserver/studioonlinebulkpublishing/process

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinebulkpublishing/process", {
    "publish": true,
    "rebuildDescriptions": true,
    "category": "RFFOBH",
    "associatedProject": "OS4OLAH",
    "overrideAssociatedProject": true,
    "criteria": {
            "entityType": "Pledge",
            "entityCodeLow": "OS4OLAA",
            "entityCodeHigh": "OS4OLAZ",
            "type": "CHILD",
            "updated": true,
            "useInStudioOnline": true,
            "publishable": true,
            "autoGenerateDescription": true,
            "missingData": "Project"
    }
});

EXAMPLE RESPONSE
204 No Content

```

Peforms actions based on the provided criteria to the entities they result in.

##### Arguments

* publish () - Publish Action Indicator
* rebuildDescriptions () - Rebuild Descriptions Action Indicator
* category () - Category to associate to all entities
* associatedProject () - Project to associate to all pledge entities
* overrideAssociatedProject () - Overrired project provided to all pledge entities
* criteria.entityType () - Entity Type
* criteria.entityCodeLow () - Entity Code Lower Limit
* criteria.entityCodeHigh () - Entity Code Upper Limit
* criteria.type () - Type
* criteria.description () - Description
* criteria.updated () - Updated Indicator
* criteria.useInStudioOnline () - Use in Studio Online Indicator
* criteria.autoGenerateDescription () - Auto Generate Description Indicator
* criteria.publishable () - Publishable Indicator

##### Returns

Returns a `204 No Content` response on success. If the process fails, this call returns an error.

### Sales Tax

#### Calculate Sales Tax

```
DEFINITION
GET http://apiserver/salestax

EXAMPLE REQUEST
$.get("http://localhost:49195/salestax?product=BK1005&postalCode=75082&country=USA&extendedAmount=5.59&shippingAmount=1.13");

EXAMPLE RESPONSE
{
    "taxRate1Amount": 1.02,
    "taxRate2Amount": 0.10,
    "taxRate3Amount": 0.01,
    "taxRate4Amount": 0,
    "taxRate5Amount": 0,
    "totalTax": 1.13,
    "taxArea": "TX"
}

```

```
DEFINITION
POST http://apiserver/salestax

EXAMPLE REQUEST
$.POST("http://localhost:49195/salestax", {salesTaxCriteria: [{
    product: "BK1005",
    postalCode: "75082",
    country: "USA",
    extendedAmount: 5.59,
    shippingAmount: 1.13
}, {...}]});

EXAMPLE RESPONSE
{
    "taxRate1Amount": 1.02,
    "taxRate2Amount": 0.10,
    "taxRate3Amount": 0.01,
    "taxRate4Amount": 0,
    "taxRate5Amount": 0,
    "totalTax": 1.13,
    "taxArea": "TX"
}

```

Note: This method has been deprecated. Instead use the taxquote resource.

##### Returns

Returns the sales tax amounts for each tax rate as well as the total tax amount.

##### Arguments

* product (optional) - The product for which to calculate the sales tax. Must be a valid product code.
* postalCode (optional) - The postal code of the shipping address. (Required if `addressId` is not provided.)
* country (optional) - The country of the shipping address. Must be a valid country code. (Required if `addressId` is not provided.)
* extendedAmount (required) - The extended amount of the order detail ((price \* quantity) - discount)
* shippingAmount (required) - The portion of shipping for the order detail.
* addressId (optional) - Used instead of the separate address components

### Scheduled Activities

#### Create a scheduled activity

```
DEFINITION
POST http://apiserver/scheduledactivities

EXAMPLE REQUEST
$.post("http://localhost:49195/scheduledactivities", {
    "activityType":5,
    "name":"Recurring Transaction Post Process",
    "schedule":{
        "cron":"0 0 1 9 *",
        "isRecurring":true,
        "isActive":true
    },
    "options":{
        "currency":"USD",
        "company":"4",
        "product":"10-0-003",
        "warehouse":"50"
    }
});

EXAMPLE RESPONSE
{
    "id": "73",
    "runId": "101",
    "activityType": 5,
    "name": "Recurring Transaction Post Process",
    "notifyUser": null,
    "schedule": {
        "id": "63",
        "description": "Recurring Transaction Post Process",
        "cron": "0 0 1 9 *",
        "cronDescription": "At 00:00 AM, on day 1 of the month, only in September",
        "startDate": null,
        "endDate": null,
        "startTime": null,
        "endTime": null,
        "isRecurring": true,
        "isActive": true
    },
    "options": {
        "paymentType": null,
        "currency": "USD",
        "frequency": null,
        "dayFrom": 1,
        "dayTo": 31,
        "category": null,
        "company": "4",
        "isDonation": true,
        "batchDate": null,
        "isPrintReceipt": true,
        "containsProduct": true,
        "product": "10-0-003",
        "warehouse": "50",
        "quantity": 0,
        "shipMethod": null
    }
}

```

Creates a new scheduled activity.

##### Arguments

* activityType (required) - The type of scheduled activity to create. The valid options are `1` for Account Import, `2` for Production, `3` for Shipping Groups, `4` for Segmentation Job Run, `5` for Recurring Transaction Post, `7` for Release Backorder, and `19` for Email Service Import.
* name (required) - The name for the activity.
* options (required) - The options for the specified activity. The value of activityType will determine what type of object options is. Please see [Activity Options](#activity-options) below.
* schedule.cron (required) - The cron string for when to run the activity.
* schedule.startDate (optional) - The start date for if recurring is used.
* schedule.endDate (optional) - The end date for if recurring is used.
* schedule.startTime (optional) - The start time for if recurring and the frequency is to run at an interval instead of 1 time per day.
* schedule.endTime (optional) - The end time for if recurring and the frequency is to run at an interval instead of 1 time per day.
* schedule.isRecurring (optional) - Whether the schedule is recurring or not.
* schedule.isActive (optional) - Whether the schedule is active or not.
* notifyUser (optional) - The user to notify when the job is run.

##### Activity Options

Below are the possible properties to include in the options object. To find more information about them, see the section of the API Docs that mention running the process manually.

###### activityType=1 ([Account Import](#account-imports-process))

* importType
* externalSystem
* batchProcessType
* dataSource
* id
* batchType
* batchNumber
* company
* acquisitionImport
* acquisitionDeduped
* useBulkImport

###### activityType=2 ([Production](#process-a-new-production-run))

* includeOrders
* includeReceipts
* includeLetters
* includeSubscriptions
* includeEvents
* includePledges
* includeNonCashGifts
* combo
* company
* letterCode
* department
* dateFrom
* dateTo
* warehouse
* productCode

###### activityType=3 ([Shipping Groups](#shipping-groups-process))

* company

###### activityType=4 ([Segmentation Job Run](#segmentation-job-run))

* job
* isStandardRun
* useFamilies
* generateJobOutput
* outputSpecification
* contactType
* overridePreferredCategory
* overrideEmailSubscriptionType
* overrideAddressType
* overrideSalutationType
* overrideEmailType
* overridePhoneType
* addCommunication
* communicationShortComment
* sendToEmail
* emailService (See [Segmentation Job Send To Email](#segmentation-job-send-to-email) for more details.)
* emailListName (See [Segmentation Job Send To Email](#segmentation-job-send-to-email) for more details.)
* emailListType (See [Segmentation Job Send To Email](#segmentation-job-send-to-email) for more details.)
* action (See [Segmentation Job Send To Email](#segmentation-job-send-to-email) for more details.)
* onlySendPrimaryEmail (See [Segmentation Job Send To Email](#segmentation-job-send-to-email) for more details.)
* sendToEmailSegmentNumber (See [Segmentation Job Send To Email](#segmentation-job-send-to-email) for more details.)
* emailDatabaseName (See [Segmentation Job Send To Email](#segmentation-job-send-to-email) for more details.)

###### activityType=5 ([Recurring Transaction Post](#recurring-transactions-post))

* paymentType
* currency
* frequency
* dayFrom
* dayTo
* category
* company
* isDonation
* batchDate
* isPrintReceipt
* containsProduct
* product
* warehouse
* quantity
* shipMethod

###### activityType=7 ([Release Backorder](#product-release-backorder))

* startDocumentNumber
* endDocumentNumber
* warehouse
* product

###### activityType=17 ([Exchange Email Sync Process](#exchange-email-sync-process))

* inboundPageSize
* inboundDelayInMinutes
* inboundReachInDays
* outboundPageSize
* outboundDelayInMinutes
* outboundReachInDays
* bodyType
* historyLevel
* errorThreshold

###### activityType=17 ([Gmail Sync Process](#gmail-sync-process))

* bodyType
* historyLevel
* errorThreshold

###### activityType=18 ([Exchange Calendar Sync Process](#exchange-calendar-sync-process))

* reachBackInDays
* reachForwardInDays
* pageSize
* bodyType
* historyLevel
* errorThreshold

###### activityType=18 ([Google Calendar Sync Process](#google-calendar-sync-process))

* historyLevel
* errorThreshold

###### activityType=19 ([Email Service Import Process](#email-service-import-process))

* emailService
* syncFromDate
* action
* listName
* databaseName

###### activityType=20 ([Custom File Processing](#custom-file-processing))

* directoryType
* ftpAppConfigKeyPrefix
* directory
* storedProcedure
* postProcessAction
* processedDirectory
* errorDirectory
* historyLevel

##### Returns

Returns a scheduled activity object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a scheduled activity

```
DEFINITION
GET http://apiserver/scheduledactivities/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/scheduledactivities/73");

EXAMPLE RESPONSE
{
    "id": "73",
    "runId": "101",
    "activityType": 5,
    "name": "Recurring Transaction Post Process",
    "notifyUser": null,
    "schedule": {
        "id": "63",
        "description": "Recurring Transaction Post Process",
        "cron": "0 0 1 9 *",
        "cronDescription": "At 00:00 AM, on day 1 of the month, only in September",
        "startDate": null,
        "endDate": null,
        "startTime": null,
        "endTime": null,
        "isRecurring": true,
        "isActive": true
    },
    "options": {
        "paymentType": null,
        "currency": "USD",
        "frequency": null,
        "dayFrom": 1,
        "dayTo": 31,
        "category": null,
        "company": "4",
        "isDonation": true,
        "batchDate": null,
        "isPrintReceipt": true,
        "containsProduct": true,
        "product": "10-0-003",
        "warehouse": "50",
        "quantity": 0,
        "shipMethod": null
    }
}

```

Retrieves the details of an existing scheduled activity. You need only supply the scheduled activity id.

##### Returns

Returns a scheduled activity object if a valid id was provided.

#### Update a scheduled activity

```
DEFINITION
POST http://apiserver/scheduledactivities/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/scheduledactivities/73", {
    schedule: {
        isActive: false
    }
});

EXAMPLE RESPONSE
{
    "id": "73",
    "runId": "101",
    "activityType": 5,
    "name": "Recurring Transaction Post Process",
    "notifyUser": null,
    "schedule": {
        "id": "63",
        "description": "Recurring Transaction Post Process",
        "cron": "0 0 1 9 *",
        "cronDescription": "At 00:00 AM, on day 1 of the month, only in September",
        "startDate": null,
        "endDate": null,
        "startTime": null,
        "endTime": null,
        "isRecurring": true,
        "isActive": false
    },
    "options": {
        "paymentType": null,
        "currency": "USD",
        "frequency": null,
        "dayFrom": 1,
        "dayTo": 31,
        "category": null,
        "company": "4",
        "isDonation": true,
        "batchDate": null,
        "isPrintReceipt": true,
        "containsProduct": true,
        "product": "10-0-003",
        "warehouse": "50",
        "quantity": 0,
        "shipMethod": null
    }
}


```

Updates the specified scheduled activity by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* activityType () - The type of scheduled activity to create. The valid options are `1` for Account Import, `2` for Production, `3` for Shipping Groups, `4` for Segmentation Job Run, `5` for Recurring Transaction Post, and `7` for Release Backorder.
* name () - The name for the activity.
* options () - The options for the specified activity. The value of activityType will determine what type of object options is. Please see [Activity Options](#activity-options).
* schedule.cron () - The cron string for when to run the activity.
* schedule.startDate () - The start date for if recurring is used.
* schedule.endDate () - The end date for if recurring is used.
* schedule.startTime () - The start time for if recurring and the frequency is to run at an interval instead of 1 time per day.
* schedule.endTime () - The end time for if recurring and the frequency is to run at an interval instead of 1 time per day.
* schedule.isRecurring () - Whether the schedule is recurring or not.
* schedule.isActive () - Whether the schedule is active or not.
* notifyUser () - The user to notify when the job is run.

##### Returns

Returns the scheduled activity object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a scheduled activity

```
DEFINITION
DELETE http://apiserver/scheduledactivities/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/scheduledactivities/73", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a scheduled activity. It cannot be undone.

##### Arguments

* id (required) - The id of the scheduled activity to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the scheduled activity does not exist, this call returns an error.

#### List all scheduled activities

```
DEFINITION
GET http://apiserver/scheduledactivities

EXAMPLE REQUEST
$.get("http://localhost:49195/scheduledactivities?name=*Transaction*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "73",
            "runId": "101",
            "activityType": 5,
            "name": "Recurring Transaction Post Process",
            "notifyUser": null,
            "schedule": {
                "id": "63",
                "description": "Recurring Transaction Post Process",
                "cron": "0 0 1 9 *",
                "cronDescription": "At 00:00 AM, on day 1 of the month, only in September",
                "startDate": null,
                "endDate": null,
                "startTime": null,
                "endTime": null,
                "isRecurring": true,
                "isActive": false
            },
            "options": {
                "paymentType": null,
                "currency": "USD",
                "frequency": null,
                "dayFrom": 1,
                "dayTo": 31,
                "category": null,
                "company": "4",
                "isDonation": true,
                "batchDate": null,
                "isPrintReceipt": true,
                "containsProduct": true,
                "product": "10-0-003",
                "warehouse": "50",
                "quantity": 0,
                "shipMethod": null
            }
        },
        {...},
    ]
}

```

Returns a list of all scheduled activities.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by id
* runId (optional) - Filter list by runId
* activityType (optional) - Filter list by the activity type.
* scheduleId (optional) - Filter list by the schedule id.
* name (optional) - Filter list by partial match of activity name
* notifyUser (optional) - Filter list by partial match of the notify user
* isRecurring (optional) - Filter list by whether the scheduled activity is recurring or not.
* isActive (optional) - Filter list by whether the scheduled activity is active or not.

##### Returns

A dictionary with an items property that contains an array of up to limit scheduled activities, starting at index offset. Each entry in the array is a separate scheduled activity object. If no more scheduled activity are available, the resulting array will be empty. This request should never return an error.

### Scheduled Activity History

#### Retrieve a scheduled activity history

```
DEFINITION
GET http://apiserver/scheduledactivities/:id/history/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/scheduledactivities/5/history/2464");

EXAMPLE RESPONSE
{
    "id": "2464",
    "runDate": "2015-02-16T05:00:02 PM",
    "status": "P",
    "message": "Import process complete. No imports to run.",
    "extId": null
}

```

Retrieves the details of a scheduled activity history. You need only supply the scheduled activity id and the scheduled activity history id.

##### Arguments

##### Returns

Returns a scheduled activity history object if a valid id was provided.

#### List all scheduled activity histories

```
DEFINITION
GET http://apiserver/scheduledactivities/:id/history

EXAMPLE REQUEST
$.get("http://localhost:49195/scheduledactivities/5/history");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "2464",
            "runDate": "2015-02-16T05:00:02 PM",
            "status": "P",
            "message": "Import process complete. No imports to run.",
            "extId": null
        },
        {...},
    ]
}

```

Returns a list of all scheduled activity histories.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit scheduled activity histories, starting at index offset. Each entry in the array is a separate scheduled activity history object. If no more scheduled activity history are available, the resulting array will be empty. This request should never return an error.

### Shipping Methods

#### Create a shipping method

```
DEFINITION
POST http://apiserver/shippingmethods

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods", {
    "id": "2DAY",
    "description": "2nd Day Air",
    "canDeliverOnSaturday": true,
    "canDeliverOnSunday": true,
    "canDeliverInternational": true,
    "canDeliverOnHolidays": true,
    "useInStudioOnline": true,
    "shippingControl": "RUSH",
    "shippingProviderIntegrationConfigurationCode": "UPS",
    "canDeliverCanada": true,
    "canDeliverUS": true,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "2DAY",
    "description": "2nd Day Air",
    "numberofDays": 2,
    "preference": "2",
    "isZoneBased": false,
    "canDeliverOnSaturday": true,
    "canDeliverOnSunday": true,
    "canDeliverInternational": true,
    "canDeliverOnHolidays": true,
    "cutoffTime": null,
    "shippingControl": "RUSH",
    "shippingProviderIntegrationConfigurationCode": "UPS",
    "realTimeShippingProvider": null,
    "realTimeService": null,
    "useInStudioOnline": true,
    "excludeFreeProducts": false,
    "excludeIfFree": false,
    "canDeliverCanada": true,
    "canDeliverUS": true,
    "isActive": true
}

```

Creates a new shipping method.

##### Arguments

* id (required)
* description (optional)
* numberofDays (optional)
* preference (optional)
* isZoneBased (optional)
* canDeliverOnSaturday (optional)
* canDeliverOnSunday (optional)
* canDeliverInternational (optional)
* canDeliverOnHolidays (optional)
* cutoffTime (optional)
* shippingControl (required)
* shippingProviderIntegrationConfigurationCode (optional) - Must be a valid shipping provider integration configuration code.
* realTimeShippingProvider (optional)
* realTimeService (optional)
* useInStudioOnline (optional)
* excludeFreeProducts (optional)
* excludeIfFree (optional)
* canDeliverCanada (optional)
* canDeliverUS (optional)
* isActive (optional)

##### Returns

Returns a shipping method object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a shipping method

```
DEFINITION
GET http://apiserver/shippingmethods/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY");

EXAMPLE RESPONSE
{
    "id": "2DAY",
    "description": "2nd Day Air",
    "numberofDays": 2,
    "preference": "2",
    "isZoneBased": false,
    "canDeliverOnSaturday": true,
    "canDeliverOnSunday": true,
    "canDeliverInternational": true,
    "canDeliverOnHolidays": true,
    "cutoffTime": null,
    "shippingControl": "RUSH",
    "shippingProviderIntegrationConfigurationCode": "UPS",
    "realTimeShippingProvider": null,
    "realTimeService": null,
    "useInStudioOnline": true,
    "excludeFreeProducts": false,
    "excludeIfFree": false,
    "canDeliverCanada": true,
    "canDeliverUS": true,
    "isActive": true
}

```

Retrieves the details of an existing shipping method. You need only supply the id.

#### Update a shipping method

```
DEFINITION
POST http://apiserver/shippingmethods/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY", {
    "isZoneBased": true
});

EXAMPLE RESPONSE
{
    "id": "2DAY",
    "description": "2nd Day Air",
    "numberofDays": 2,
    "preference": "2",
    "isZoneBased": true,
    "canDeliverOnSaturday": true,
    "canDeliverOnSunday": true,
    "canDeliverInternational": true,
    "canDeliverOnHolidays": true,
    "cutoffTime": null,
    "shippingControl": "RUSH",
    "shippingProviderIntegrationConfigurationCode": "UPS",
    "realTimeShippingProvider": null,
    "realTimeService": null,
    "useInStudioOnline": true,
    "excludeFreeProducts": false,
    "excludeIfFree": false,
    "canDeliverCanada": true,
    "canDeliverUS": true,
    "isActive": true
}


```

Updates the specified shipping method by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional)
* numberofDays (optional)
* preference (optional)
* isZoneBased (optional)
* canDeliverOnSaturday (optional)
* canDeliverOnSunday (optional)
* canDeliverInternational (optional)
* canDeliverOnHolidays (optional)
* cutoffTime (optional)
* shippingControl (optional)
* shippingProviderIntegrationConfigurationCode (optional) - Must be a valid shipping provider integration configuration code.
* realTimeShippingProvider (optional)
* realTimeService (optional)
* useInStudioOnline (optional)
* excludeFreeProducts (optional)
* excludeIfFree (optional)
* canDeliverCanada (optional)
* canDeliverUS (optional)
* isActive (optional)

##### Returns

Returns the shipping method object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a shipping method

```
DEFINITION
DELETE http://apiserver/shippingmethods/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/shippingmethods/2DAY", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a shipping method. It cannot be undone.

##### Arguments

* id (required) - The id of the shipping method to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the shipping method does not exist, this call returns an error.

#### List all shipping methods

```
DEFINITION
GET http://apiserver/shippingmethods

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "2DAY",
            "description": "2nd Day Air",
            "numberofDays": 2,
            "preference": "2",
            "isZoneBased": true,
            "canDeliverOnSaturday": true,
            "canDeliverOnSunday": true,
            "canDeliverInternational": true,
            "canDeliverOnHolidays": true,
            "cutoffTime": null,
            "shippingControl": "RUSH",
            "shippingProviderIntegrationConfigurationCode": "UPS",
            "realTimeShippingProvider": null,
            "realTimeService": null,
            "useInStudioOnline": true,
            "excludeFreeProducts": false,
            "excludeIfFree": false,
            "canDeliverCanada": true,
            "canDeliverUS": true,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all shipping methods.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id
* description
* numberofDays
* preference
* isZoneBased
* canDeliverOnSaturday
* canDeliverOnSunday
* canDeliverInternational
* canDeliverOnHolidays
* cutoffTime
* shippingControl
* realTimeShippingProvider
* realTimeService
* useInStudioOnline
* excludeFreeProducts
* excludeIfFree
* canDeliverCanada
* canDeliverUS
* isActive

##### Returns

A dictionary with an items property that contains an array of up to limit shipping methods, starting at index offset. Each entry in the array is a separate shipping method object. If no more shipping methods are available, the resulting array will be empty. This request should never return an error.

### Scripts and Instructions

#### Create a Script or Instruction

```
DEFINITION
POST http://apiserver/scriptandinstructions

EXAMPLE REQUEST
$.post("http://localhost:49195/scriptandinstructions", {
    "code": "S2",
    "description": "Donor Thankyou Phone Script1",
    "type": "SCRIPT",
    "startDate": "2010-01-01",
    "endDate": "2013-12-31",
    "isActive": true,
    "usage": "P",
    "topic": "DONEMS",
    "category": "QUESTION",
    "notify": false,
    "userId": null,
    "emailAddress": "laura.vance@donordirect.com"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "code": "S2",
    "description": "Donor Thankyou Phone Script1",
    "type": "SCRIPT",
    "startDate": "2010-01-01",
    "endDate": "2013-12-31",
    "isActive": true,
    "usage": "P",
    "topic": "DONEMS",
    "topicDescription": "Donation Entry Mistake",
    "category": "QUESTION",
    "categoryDescription": "Question About Business Policies",
    "notify": false,
    "userId": null,
    "emailAddress": "laura.vance@donordirect.com"
}

```

Creates a new Script or Instruction.

##### Arguments

* code (required) - The code associated with this script or instruction.
* description (required) - The description of what this script or instruction is for.
* type (required) - The type of this object whether it is a script or instruciton.
* startDate () - The date when this script or instruction is "valid."
* endDate () - The date when this script or instruciton is no longer "valid."
* isActive () - Whether or not this script or instruction is active.
* topic () - The topic which this script or instruction pertains to.
* category () - The category which this script or instruction belongs in.
* notify () - Whether or not to notify?
* userId () - The user id.
* emailAddress () - The email address to notify.

##### Returns

Returns a Script or Instruction object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a script or instruction

```
DEFINITION
GET http://apiserver/scriptandinstructions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/scriptandinstructions/S2");

EXAMPLE RESPONSE
{
    "id": "5",
    "code": "S2",
    "description": "Donor Thankyou Phone Script1",
    "type": "SCRIPT",
    "startDate": "2010-01-01",
    "endDate": "2013-12-31",
    "isActive": true,
    "usage": "P",
    "topic": "DONEMS",
    "topicDescription": "Donation Entry Mistake",
    "category": "QUESTION",
    "categoryDescription": "Question About Business Policies",
    "notify": false,
    "userId": null,
    "emailAddress": "laura.vance@donordirect.com"
}

```

Retrieves the details of an existing script or instruction. You need only supply the ###.

##### Arguments

* id (required) - The id of the script or instruction to retrieve.

##### Returns

Returns a script or instruction object if a valid id was provided.

#### Update a Script or Instruction

```
DEFINITION
POST http://apiserver/scriptandinstructions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/scriptandinstructions/1", {
    "code": "S2",
    "description": "Donor Thankyou Phone Script1",
    "type": "SCRIPT",
    "startDate": "2010-01-01",
    "endDate": "2013-12-31",
    "isActive": true,
    "usage": "P",
    "topic": "DONEMS",
    "category": "QUESTION",
    "notify": false,
    "userId": null,
    "emailAddress": "laura.vance@donordirect.com"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "code": "S2",
    "description": "Donor Thankyou Phone Script1",
    "type": "SCRIPT",
    "startDate": "2010-01-01",
    "endDate": "2013-12-31",
    "isActive": true,
    "usage": "P",
    "topic": "DONEMS",
    "topicDescription": "Donation Entry Mistake",
    "category": "QUESTION",
    "categoryDescription": "Question About Business Policies",
    "notify": false,
    "userId": null,
    "emailAddress": "laura.vance@donordirect.com"
}


```

Updates the specified Script or Instruction by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* code () - The code associated with this script or instruction.
* description () - The description of what this script or instruction is for.
* type () - The type of this object whether it is a script or instruciton.
* startDate () - The date when this script or instruction is "valid."
* endDate () - The date when this script or instruciton is no longer "valid."
* isActive () - Whether or not this script or instruction is active.
* topic () - The topic which this script or instruction pertains to.
* category () - The category which this script or instruction belongs in.
* notify () - Whether or not to notify?
* userId () - The user id.
* emailAddress () - The email address to notify.

##### Returns

Returns the Script or Instruction object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Script or Instruction

```
DEFINITION
DELETE http://apiserver/scriptandinstructions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/scriptandinstructions/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Script or Instruction. It cannot be undone.

##### Arguments

* id (required) - The id of the Script or Instruction to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Script or Instruction does not exist, this call returns an error.

#### List all scripts and instructions

```
DEFINITION
GET http://apiserver/scriptandinstructions", {

});

EXAMPLE REQUEST
$.get("http://localhost:49195/scriptandinstructions", {

});

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
            "code": "S2",
            "description": "Donor Thankyou Phone Script1",
            "type": "SCRIPT",
            "startDate": "2010-01-01",
            "endDate": "2013-12-31",
            "isActive": true,
            "usage": "P",
            "topic": "DONEMS",
            "topicDescription": "Donation Entry Mistake",
            "category": "QUESTION",
            "categoryDescription": "Question About Business Policies",
            "notify": false,
            "userId": null,
            "emailAddress": "laura.vance@donordirect.com"
        },
        {...},
        {...}
    ]
}

```

Returns a list of scripts and instructions for the specified criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match in script/instruction Id.
* description (optional) - Filter list by partial match in description.
* type (optional) - The script/instruction type. Valid values are (SCRIPT|INSTRUCTION).
* isActive (optional) - Whether or not the script/instruction is active.

##### Returns

A dictionary with an items property that contains an array of up to limit scripts and instructions, starting at index offset. Each entry in the array is a separate script/instruction. If no more scripts/instructions are available, the resulting array will be empty. This request should never return an error.

### Script and Instruction Details

#### Create a Script or Instruction Detail

```
DEFINITION
POST http://apiserver/scriptandinstructions/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/scriptandinstructions/1/details", {
    "scriptOrInstructionId": "4",
    "detailHeading": "PLEDGE OFFER",
    "detailText": "As a part of becoming a SON Ministry pledge partner, we have a special promotional product that we offer our special friends.  This product is sent to you or someone else of your choosing upon receipt of your first full payment to the pledge.  Can we count on your continued support?",
    "sequenceNumber": 10,
    "isButtonVisible": true,
    "buttonTitle": "Pledges",
    "detailActivityId": "965",
});

EXAMPLE RESPONSE
{
    "id": "2",
    "scriptOrInstructionId": "4",
    "detailHeading": "PLEDGE OFFER",
    "detailText": "As a part of becoming a SON Ministry pledge partner, we have a special promotional product that we offer our special friends.  This product is sent to you or someone else of your choosing upon receipt of your first full payment to the pledge.  Can we count on your continued support?",
    "sequenceNumber": 10,
    "isButtonVisible": true,
    "buttonTitle": "Pledges",
    "detailActivityId": "965",
    "interfaceId": "AccountPledges"
}

```

Creates a new Script or Instruction Detail.

##### Arguments

* detailHeading (required) - The heading of this detail.
* detailText (required) - The text body of this detial.
* sequenceNumber (required) - The order of priority for this detail.
* isButtonVisible (required) - Whether or not the button is visible.
* buttonTitle () - The title if the button is visible.
* detailActivityId () - The activity that this detail is associated with.

##### Returns

Returns a Script or Instruction Detail object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Script or Instruction Detail

```
DEFINITION
GET http://apiserver/scriptandinstructions/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/scriptandinstructions/1/details/2");

EXAMPLE RESPONSE
{
    "id": "2",
    "scriptOrInstructionId": "4",
    "detailHeading": "PLEDGE OFFER",
    "detailText": "As a part of becoming a SON Ministry pledge partner, we have a special promotional product that we offer our special friends.  This product is sent to you or someone else of your choosing upon receipt of your first full payment to the pledge.  Can we count on your continued support?",
    "sequenceNumber": 10,
    "isButtonVisible": true,
    "buttonTitle": "Pledges",
    "detailActivityId": "965",
    "interfaceId": "AccountPledges"
}

```

Retrieves the details of an existing Script or Instruction Detail. You need only supply the id.

##### Arguments

* id (required) - The id of the Script or Instruction to be retrieved.

#### Update a Script or Instruction Detail

```
DEFINITION
POST http://apiserver/scriptandinstructions/:id/detail/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/scriptandinstructions/1/detail/2", {
    "detailHeading": "PLEDGE OFFER",
    "detailText": "As a part of becoming a SON Ministry pledge partner, we have a special promotional product that we offer our special friends.  This product is sent to you or someone else of your choosing upon receipt of your first full payment to the pledge.  Can we count on your continued support?",
    "sequenceNumber": 10,
    "isButtonVisible": true,
    "buttonTitle": "Pledges",
    "detailActivityId": "965",
});

EXAMPLE RESPONSE
{
    "id": "2",
    "scriptOrInstructionId": "4",
    "detailHeading": "PLEDGE OFFER",
    "detailText": "As a part of becoming a SON Ministry pledge partner, we have a special promotional product that we offer our special friends.  This product is sent to you or someone else of your choosing upon receipt of your first full payment to the pledge.  Can we count on your continued support?",
    "sequenceNumber": 10,
    "isButtonVisible": true,
    "buttonTitle": "Pledges",
    "detailActivityId": "965",
    "interfaceId": "AccountPledges"
}


```

Updates the specified Script or Instruction Detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* detailHeading () - The heading of this detail.
* detailText () - The text body of this detial.
* sequenceNumber () - The order of priority for this detail.
* isButtonVisible () - Whether or not the button is visible.
* buttonTitle () - The title if the button is visible.
* detailActivityId () - The activity that this detail is associated with.

##### Returns

Returns the Script or Instruction Detail object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Script or Instruction Detail

```
DEFINITION
DELETE http://apiserver/scriptandinstructions/:id/detail/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/scriptandinstructions/1/detail/2", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Script or Instruction Detail. It cannot be undone.

##### Arguments

* id (required) - The id of the Script or Instruction Detail to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Script or Instruction Detail does not exist, this call returns an error.

#### List all Script and Instruction Details

```
DEFINITION
GET http://apiserver/scriptandinstructions/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/scriptandinstructions/1/details?");

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
            "scriptOrInstructionId": "4",
            "detailHeading": "PLEDGE OFFER",
            "detailText": "As a part of becoming a SON Ministry pledge partner, we have a special promotional product that we offer our special friends.  This product is sent to you or someone else of your choosing upon receipt of your first full payment to the pledge.  Can we count on your continued support?",
            "sequenceNumber": 10,
            "isButtonVisible": true,
            "buttonTitle": "Pledges",
            "detailActivityId": "965",
            "interfaceId": "AccountPledges"
        },
        {...},
    ]
}

```

Returns a list of all Script and Instruction Details.

##### Arguments

* detailHeading () - The heading of this detail.
* detailText () - The text body of this detial.
* sequenceNumber () - The order of priority for this detail.
* isButtonVisible () - Whether or not the button is visible.
* buttonTitle () - The title if the button is visible.
* detailActivityId () - The activity that this detail is associated with.

##### Returns

A dictionary with an items property that contains an array of up to limit Script and Instruction Details, starting at index offset. Each entry in the array is a separate script or instruction detail object. If no more Script and Instruction Details are available, the resulting array will be empty. This request should never return an error.

### Next Numbers

#### Create a Next Number

```
DEFINITION
POST http://apiserver/nextnumbers

EXAMPLE REQUEST
$.post("http://localhost:49195/nextnumbers", {
    "id": "ACCLKPGRID",
    "number": "1000001265"
});

EXAMPLE RESPONSE
{
    "id": "ACCLKPGRID",
    "number": "1000001265"
}

```

Creates a new Next Number.

##### Arguments

* id (required) - The type.
* number (required) - The number.

##### Returns

Returns a Next Number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a Next Number

```
DEFINITION
GET http://apiserver/nextnumbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/nextnumbers/ACCLKPGRID");

EXAMPLE RESPONSE
{
    "id": "ACCLKPGRID",
    "number": "1000001265"
}

```

Retrieves the details of an existing Next Number. You need only supply the id.

##### Arguments

* id (required) - The id of the Next Number to be retrieved.

#### Update a Next Number

```
DEFINITION
POST http://apiserver/nextnumbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/nextnumbers/ACCLKPGRID", {
    "number": "1000001265"
});

EXAMPLE RESPONSE
{
    "id": "ACCLKPGRID",
    "number": "1000001265"
}


```

Updates the specified Next Number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The type.
* number (required) - The number.

##### Returns

Returns the Next Number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a Next Number

```
DEFINITION
DELETE http://apiserver/nextnumbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/nextnumbers/ACCLKPGRID", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Next Number. It cannot be undone.

##### Arguments

* id (required) - The id of the Next Number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the Next Number does not exist, this call returns an error.

#### List all Next Numbers

```
DEFINITION
GET http://apiserver/nextnumbers

EXAMPLE REQUEST
$.get("http://localhost:49195/nextnumbers?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "ACCLKPGRID",
            "number": "1000001265"
        },
        {...},
    ]
}

```

Returns a list of all Next Numbers.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - The Type to search for.

##### Returns

A dictionary with an items property that contains an array of up to limit Next Numbers, starting at index offset. Each entry in the array is a separate Next Number object. If no more Next Numbers are available, the resulting array will be empty. This request should never return an error.

### Shipping Method Attachments

#### Create a shipping method attachment

```
DEFINITION
POST http://apiserver/shippingmethods/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAD1ZJREFUeNrMW8uLZkcVr1P39owihPaFy8zSZbvwBUanQdGdihsXgpO1SJiNghJnxiwCgowu4irgzEJwl/wBkR7BTQhKL9WFtAsXimCTlTPfrTrWeVWduo/uL5Nkxg+q697v3u/eOr8673MawuzzoVe+clima2Wc62yf85XvznTu7vvbX8/p+6Owxwdi+TPoHKGMcgyB5wBB/oD7AdqMckxTLnOmuZwkPcbV15194pdvnXXvd4TTgu+Wcb2MB2X8voxb7t617+7o3N1XAKDvTy4lHpT4QYgXEHRVdA5L+o12JpzmjA4EDGgApM3XEgA3CxCvB32dEX+ixD+RT0f8ADrTeTkeIUS9FvW8jnoe5J5y3H4v1+tz1z/Era/984VPf6MCoDt/+NSIj23xc6JDIZQG6MzHDii53z+HxElFKV64jF/Tn1Flfq+dh5Xv8HEQWCVeFm5iACoKJgZ0ACrY6GQfQGQkQmF//gHymsrdgb/BTX1wWLjg+niZsqIHm2hGlUdwhKvo6QyXAgLuYQviByV+MEXY9EDdAgyNKDqgr0CBUNLpItp99Mxpez3j5oXyaxKnUbiJjyP0nIAd8UUBl7dOeAkLxeVOV+LVGoBxhu38DHUmrryQiMYGwp2P/PjN2++UGRcADOWBRPQV0S1BdQwTP7Q1VbZKlXgZ0yWyXwlzQHRgeLGoYgAOAEVciZdrfOHWf17+3C0si8CJrIBahElmXF/Y8eg3h3b9oLz0oJxcjUL8qIRHBWKLA5h4Hdvy1Ij3IFS2V6KrJo+eE/SFKN8RgQwCS75j+0zPo2NgLkF6PnPLui4YjaCDQvyVKDtPMwFgHFC5wMwGNFb0HHARAJWNTa7rrDtv3KHExwF6gLz/k5uPJBuBAgwTLEBBFt1gihRhXWOPkS0NMsFE+AdmHHDgRQDci3GFA/IFIuCVWafdGzABmk4IJg6D6oFoLBdU06ue5+8ITOTfNMuAFYDu3XMArpjMK/FXFYAPGgcoEBeKgHEAXCwCEPoFmWxDBaQHwcRCuEVR55etsXy4V4C4D2oGqwIlkJqemH9OR5b50Ii/6sTAiKdZAMCFGUwFZgNgKOgPeAkHwDoYDQhwekKIN3GoW0rbzLtNnIHiBodwo1y6MX+m57qwFIPj8Yqy+YFq/qtC/OHVITxL7z2I1SQeDjE8G/rnPJsL9Mb+sSx4yHs4UwDr5x6M0HSDiQOzNyrBJttOyYhKbOj252v0swgIkVfcKOdHZdePWDyUE8r7j8pmHAF0CulG3X3apHIyAexhfbGuSvwZrE5OHaGfmWhl+xoFziIkfAz3dBydsjtQdmdAyCQOTQSIC2J0VsApQRKDSTUzIF5OuidwTqxqdETnZgZxg9kCpBYGc/Q3fwZuALLhEo9j6Ikfje3teBDilQvEG/RmkFgfTTeALFryBg8WlGPvzYXQ3FqQ747K7w9BtTlfTCLzwgFKSEJ3XgG5V47v4/xdGDaDAVaCg2r3avNjI9iODZChKJxoGlsVMsl9zB2Nhy8898zhwxTuPCxK6r/FUaCxw3D61o03zi/ijrd/8fmT8vDrRKC8Qr2X6B0hAYeSHzJrIiSHGySSlgxBdCKzLRbHHQDRHQsgDYiDot4HxwXMgWT3s1lkeh8WSwRH5fJJdMpc13+84IoV+WBizByqnWdtbwrPJUCqu4vy7rDkisb6G0wwRmiRnhxjO1aCaeeHaKKBFYBUNSJyJJiimMH6ezeGPRQTVjDRBT1q6rpskO5+alkgHjU1NgNkO0XGXB/izPRCBaPnCiJ+HORY5FZ87uwIJUckskly4TPsp5EljeVAMCcnL3VJef9ZIf6sigO6vGB2RHtuWH7Oxzh3Smbhd/CAKBAkDjmLAwTVgZGFw0ryhMGI+wJgixb31mx+F80IQffv/PY7r7/LTNbZiDMLBCvpnplIseznMAf24mQI7mObcxNhyOhYMjTB6JXb3XeZxzweK5dgizU6zjGOyiLztJAMQizZfosFsj4j49L65D0BMBtPco81sMHqI1VF+di5uBUdkB3Rnggf5MSyoClYTN00Ml2f0gyIAO0Zjvi8nw64X268TnLPQHDSIyz9WHzvAIieUPPqUs3wADs6ic0dhF0h9pGOnY6Jr4snyM/ILTvkn7sPAB+98+a9sut3cgrnnNWhbA5ndCzL03/ngr423ikHTCpqyaW1mGgI6t6CpRzY1JmmD3qeLQ+gIFlSxMDLel7m030W9LGfcl7v9r9/8tnrCN6CYO8vFAU2DPAlgGW+Gi17nGXlF4nfaHk8WziHtOzdoTMMwA9N0UwbhDDPBSgX1OEyROX03h+fv9gLXAHiwWX3/OiLz7fkSqdsQfVa8xYzrgPBHACq0CYxu+zaclyesSoxAmVAM3chNKdMdnpSTtjxAJ7Ld2fluwfl8Ob7UWAZime25mNU4imoYpcZRbFmMt/YqY/xkZ4NSnj0GZ8oxodMRYqWEgPvlvPLfvOt30F4Cp9hdABAi9B8HJArAMj6iZKYOTduGHfqaDBr52UhlrR6YlcWq3cYZimxp/XhWL4WRebyj9WfMACAgizi4MKyOSGvfdypXeXdjxqrO4ckaUTKesFpWu8rPK3PsAKAgbAEIMvaE/0kytYWOseHWVxun+hEDeuJ8FEBqL7+zCbnpwwAzCpHGJzyQ2wApODSynQUubBSlKAWF7JzdRWAyaXFB+hrg/83IhChqxFYaJwNAGJ1Io4Ti1mLD7nSOlpm92HQHykAxPoU/u60Qj0HAJ0leGoccOA4YGYBSKQzV4QKqxcNDkFBINYosT1ibgD49HZWe0+7T/rBKkOmAGdJ0fdVBO587dXbhc2/Hod4VJyeUOYwlEFp8qjpcgMAND4JKv+0mSz3TLyvZSvxg0AyzoO/R+zBIQMwrw0+SQ64/dVXb0OEW1QgEWKFeAaCOkiKxo56zUBApwBZ6+eoXmuW9JoRT+Zdg4zV8rhxw46UROjLYnMdQOOTL/3hEChlHqCW0FsYjeow4elfXnxub2+wPO+7TCBAJTQq8cIFBQwDIMLCAiQ1e0w86zkhHvR+oKAOL+gPEDQhPLI+BGgRP9ScvtToPh6B6gUn7CRBl79kk0JiRSAUoO5Rg9KfX/zC+SW7XwCFa7yz0QEQbeeFExgIIwi8AlT7XVk+tJ3XkbWeOO6VqnI+9lrTDGvj4MpaoaYKxeBkiSUKEDeyKI3nL9l9KcC4He6AMOI9CIpAdjtvLB+N6Oh1hjx/fC/kldjRHJJFYIJSsjabHAH360eCZt7agntQBqcXQDO1uSA81WxyZhHKs2dI18k74IBLAZhxAIDP3NhikB2PMq7tQ3yrEYJbMLikreoH4oJRuIABT+TVZtnt2nugv7XYFloilACgOP34XbW9DbEvb0Or9pitBDAA9jCc0APRJ1ihAzoqGMQJOaPKtsVG0LLSviTvhHkc/v5D2pFby14hCFfKQw8GmW1Etcdsg4lwMRGH4OSrS1ywCGh2N4VLm/f6ZCwuiqCS4EDn9orvQjF5DYOrznLHs/oguhaZ1T5BYzEyNTZibWxyg+VPbbJzSoLKYVatnAFb78o+9NcKMKoYYUveOm2fVOFlpwMo0lu7X+FwlaINHWBFjSEqe+kwswRaNoIBqkmqjomypKWikhKfyiJTCGGvrJ3tYmi7VvVIxprY4ExMsEStWQEDIatIzMCoZXb5blxvjrTdBHcsqETwHNBM0aBaOTq3VHzy4lWm5oomjPvQf1rGcVsoajEW7xZLcpQq8eLb59hEDxUA4oxEYuEAwwUYWxywUtszGbekAOhum3iMQ+OEWj4nFoXa2SRltHL6mVf+dIK0uCnzInOZH5X5oc6/KvPDhKFPXoWbL/3jX+eZgxuN6dW5geiyVBoKJxUFen5KDQQeMw7orIB4zM1sGAeEbufZ87trjonsfnNOTNNWNkX1vKIkW8vpdfSt8OC1e29J3OeQd34K6t4Gfqc9t/VRitdZRYDC4Zw7bkDHDdYrfLJhiTZrfcGJiPfUzDOrqSkUD4zByqAVZdCihwwhHl05HVYLbZnBjLLTQ66y762PxQJLEHBxTrWFeFFHF/i+vtl1HxFCpyDFMYoKhPX6ds1asNI6t4W2D9KMpac2CiHHaUphKsfTrsw7ZvmbieYJ231Tvkm/n4MQL2xWwFk9LmydN2XFSojZLavywi53OO9YwbDWJ7RRO51UuysIROz373/7ARNdxjTZ9+lUZF/kn+6fJjxl6zDjhHGL+Owdj+p8YLWnoAhZpBdVwUBoCiYvtG9r17Bjan7KAV1xFjeTrSzHTqQsDE5T7vqW0LvfubE/F3csI6yKcdUVzm5LEGv7k2SP5cJR2em7OYZqdxPxPjsgkm0N5gQlic1TtjxdqA1O6Cq9nYdnYK0BoEoPY1O2tPPzThMMPQCmBI144dKwVILVvaSbo3aBZmmRCfpAjrXBPLzCXik2zRybgmDE9eUCgLCepa2sjJxnFekNX/EayTS51VTlyeqTVA6YO1HKAeYI0T38OtMDVhdYd0SMtZH/CULcWWAQpIlJ082gO888U/wAckpyqC2c9pyUsBcHJd4qNPYu/94VEbhGOgDNHScQHAeAzwhZHJCby5wnBSI1K7GZEmsNkFIRSjoozESQ6gmqJ5aDmib1yCL0ANQFqNlh5WiurHNMmFOwccOqFZg0pUUb4EQg7dLiP0q60hiGyvKL2uA2ACo7AOzNJe4Xlq5r+j8i7l/SrEtCtcnZkg/QRWWy6+qIpDayEj1lAzlUTlj7FE1elB/WZAasiEAfP/RcsPUPE6v5gOwWk2teD6V5o/jj1J8jD2ye3rxI0TUrGvurCSJAOPusI5myyrhpDbM2R0L/rzLF7KGvjfZ6AC/pD9Bw+GTJBSgNEjV8JQ+MdjoWvz9zVpU7uTDq//xIWxvCWkvbzAV1xO+SByJLbL9PftLdl1Je+jD7ZrPe/tmXz0L7H+BZerztEC2OorpdmXepNydZAxobrY3FXUtt8HP0WclxQMqPV2zt4/69n3H28ze/98B0ADUwvLYKgjo3wmKi7VELDQPKkG5OTUHBzLGzNlat1zHBKCBOjgtozk+u1kxp+W8G82sKF7yuqerzNZabdNd3WXaNQlY/piR+t+22uaHZfHa6r1znkJd/b89qxCd8YsRT682nyu6fdlaggEBFi3vP/OCNo3n3Jao4UMEx+b4hVUKo/7paU9kzZSrVIdR2Ou8ZNj9jH5YtY6szdK7ETze++3AhvNvk/wkwAHX7faDFX68AAAAAAElFTkSuQmCC",
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

Creates a new shipping method attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a shipping method attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a shipping method attachment

```
DEFINITION
GET http://apiserver/shippingmethods/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/attachments/49");

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

Retrieves the details of an existing shipping method attachment. You need only supply the shipping method id and shipping method attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a shipping method attachment object if a valid id was provided.

#### Update a shipping method attachment

```
DEFINITION
POST http://apiserver/shippingmethods/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/attachments/49", {
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

Updates the specified shipping method attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type. Must be a defined attachment type.
* url (optional) - The url of the attachment type.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the shipping method attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a shipping method attachment

```
DEFINITION
DELETE http://apiserver/shippingmethods/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/shippingmethods/2DAY/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a shipping method attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the shipping method attachment id does not exist, this call returns an error.

#### List all shipping method attachments

```
DEFINITION
GET http://apiserver/shippingmethods/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/attachments");

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

Returns a list of all shipping method attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit shipping method attachments, starting at index offset. Each entry in the array is a separate shipping method attachment object. If no more shipping method attachments are available, the resulting array will be empty. This request should never return an error.

### Shipping Method Codes

#### Create a shipping method code

```
DEFINITION
POST http://apiserver/shippingmethods/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/codes", {
    "type": "SHPCD1",
    "value": "V1"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "SHPCD1",
    "typeDescription": "Shipping Method Code 1",
    "value": "V1",
    "valueDescription": "Code Value 1",
    "isActive": true
}

```

Creates a new shipping method code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a shipping method code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a shipping method code

```
DEFINITION
GET http://apiserver/shippingmethods/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/codes/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "SHPCD1",
    "typeDescription": "Shipping Method Code 1",
    "value": "V1",
    "valueDescription": "Code Value 1",
    "isActive": true
}

```

Retrieves the details of an existing shipping method code. You need only supply the shipping method id and shipping method code id.

##### Returns

Returns a shipping method code object if a valid id was provided.

#### Update a shipping method code

```
DEFINITION
POST http://apiserver/shippingmethods/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/codes/16", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "SHPCD1",
    "typeDescription": "Shipping Method Code 1",
    "value": "V1",
    "valueDescription": "Code Value 1",
    "isActive": false
}


```

Updates the specified shipping method code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the shipping method code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a shipping method code

```
DEFINITION
DELETE http://apiserver/shippingmethods/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/shippingmethods/2DAY/codes/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a shipping method code. It cannot be undone.

##### Arguments

* id (required) - The id of the account code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the shipping method code id does not exist, this call returns an error.

#### List all shipping method codes

```
DEFINITION
GET http://apiserver/shippingmethods/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/codes");

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
            "type": "SHPCD1",
            "typeDescription": "Shipping Method Code 1",
            "value": "V1",
            "valueDescription": "Code Value 1",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all shipping method codes.

##### Returns

A dictionary with an items property that contains an array of up to limit shipping method codes, starting at index offset. Each entry in the array is a separate shipping method code object. If no more shipping method codes are available, the resulting array will be empty. This request should never return an error.

### Shipping Method Dates

#### Create a shipping method date

```
DEFINITION
POST http://apiserver/shippingmethods/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/dates", {
    "type": "SHPDT",
    "value": "2015-02-11"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "SHPDT",
    "typeDescription": "Shipping Method Date Attr",
    "value": "2015-02-11",
    "isActive": true
}

```

Creates a new shipping method date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a shipping method date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a shipping method date

```
DEFINITION
GET http://apiserver/shippingmethods/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/dates/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "SHPDT",
    "typeDescription": "Shipping Method Date Attr",
    "value": "2015-02-11",
    "isActive": true
}

```

Retrieves the details of an existing shipping method date. You need only supply the shipping method id and shipping method date id.

##### Returns

Returns a shipping method date object if a valid id was provided.

#### Update a shipping method date

```
DEFINITION
POST http://apiserver/shippingmethods/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/dates/16", {
    "value": "2015-03-11",
});cmd

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "SHPDT",
    "typeDescription": "Shipping Method Date Attr",
    "value": "2015-03-11",
    "isActive": false
}


```

Updates the specified shipping method date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the shipping method date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a shipping method date

```
DEFINITION
DELETE http://apiserver/shippingmethods/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/shippingmethods/2DAY/dates/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a shipping method date. It cannot be undone.

##### Arguments

* id (required) - The id of the account date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the shipping method date id does not exist, this call returns an error.

#### List all shipping method dates

```
DEFINITION
GET http://apiserver/shippingmethods/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/dates");

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
            "type": "SHPDT",
            "typeDescription": "Shipping Method Date Attr",
            "value": "2015-03-11",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all shipping method dates.

##### Returns

A dictionary with an items property that contains an array of up to limit shipping method dates, starting at index offset. Each entry in the array is a separate shipping method date object. If no more shipping method dates are available, the resulting array will be empty. This request should never return an error.

### Shipping Method Notes

#### Create a shipping method note

```
DEFINITION
POST http://apiserver/shippingmethods/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/notes", {
    "type": "SHPNT",
    "shortComment": "Example1",
    "longComment": "This is an example comment.\nMultiple lines are supported."
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SHPNT",
    "description": "Shipping Method Note",
    "shortComment": "Example1",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Creates a new shipping method note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a shipping method note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a shipping method note

```
DEFINITION
GET http://apiserver/shippingmethods/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/notes/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SHPNT",
    "description": "Shipping Method Note Type",
    "shortComment": "Example1",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Retrieves the details of an existing shipping method note. You need only supply the shipping method id and shipping method note id.

##### Returns

Returns a shipping method note object if a valid id was provided.

#### Update a shipping method note

```
DEFINITION
POST http://apiserver/shippingmethods/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/notes/9", {
    "shortComment": "Example2"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SHPNT",
    "description": "Shipping Method Note Type",
    "shortComment": "Example2",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}


```

Updates the specified shipping method note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the shipping method note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type).

#### Delete a shipping method note

```
DEFINITION
DELETE http://apiserver/shippingmethods/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/shippingmethods/2DAY/notes/11", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a shipping method note. It cannot be undone.

##### Arguments

* id (required) - The id of the account note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the shipping method note id does not exist, this call returns an error.

#### List all shipping method notes

```
DEFINITION
GET http://apiserver/shippingmethods/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/notes");

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
            "type": "SHPNT",
            "description": "Shipping Method Note Type",
            "shortComment": "Example1",
            "longComment": "This is an example comment.\nMultiple lines are supported."
        },
        {...},
        {...}
    ]
}

```

Returns a list of all shipping method notes.

##### Returns

A dictionary with an items property that contains an array of up to limit shipping method notes, starting at index offset. Each entry in the array is a separate shipping method note object. If no more shipping method notes are available, the resulting array will be empty. This request should never return an error.

### Shipping Method Numbers

#### Create a shipping method number

```
DEFINITION
POST http://apiserver/shippingmethods/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/numbers", {
    "type": "SHPNBR",
    "value": 141
});

EXAMPLE RESPONSE
{
    "id": "10",
    "isMultiValue": true,
    "type": "SHPNBR",
    "typeDescription": "Shipping Method Number Attr",
    "value": 141
    "isActive": true,
}

```

Creates a new shipping method number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a shipping method number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a shipping method number

```
DEFINITION
GET http://apiserver/shippingmethods/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/numbers/10");

EXAMPLE RESPONSE
{
    "id": "10",
    "isMultiValue": true,
    "type": "SHPNBR",
    "typeDescription": "Shipping Method Number Attr",
    "value": 141
    "isActive": true,
}

```

Retrieves the details of an existing shipping method number. You need only supply the shipping method id and shipping method number id.

##### Returns

Returns a shipping method number object if a valid id was provided.

#### Update a shipping method number

```
DEFINITION
POST http://apiserver/shippingmethods/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/numbers/10", {
    "value": 78
});

EXAMPLE RESPONSE
{
    "id": "10",
    "isMultiValue": true,
    "type": "SHPNBR",
    "typeDescription": "Shipping Method Number Attr",
    "value": 78
    "isActive": true,
}


```

Updates the specified shipping method number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the shipping method number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Delete a shipping method number

```
DEFINITION
DELETE http://apiserver/shippingmethods/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/shippingmethods/2DAY/numbers/10", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a shipping method number. It cannot be undone.

##### Arguments

* id (required) - The id of the account number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the shipping method number id does not exist, this call returns an error.

#### List all shipping method numbers

```
DEFINITION
GET http://apiserver/shippingmethods/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/numbers");

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
            "isMultiValue": true,
            "type": "SHPNBR",
            "typeDescription": "Shipping Method Number Attr",
            "value": 78
            "isActive": true,
        },
        {...},
        {...}
    ]
}

```

Returns a list of all shipping method numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit shipping method numbers, starting at index offset. Each entry in the array is a separate shipping method number object. If no more shipping method numbers are available, the resulting array will be empty. This request should never return an error.

### Shipping Method Rates

#### Create a shipping method rate

```
DEFINITION
POST http://apiserver/shippingmethods/:id/rates

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/:id/rates", {
    amount: 4.99
    baseAmount: 4.99
    calculationType: "I"
    capAmount: 9.99
    distributionPercent: 100
});

EXAMPLE RESPONSE
{
    "id" : "12085",
    "zone" : null,
    "zoneDescription" : null,
    "calculationType" : "I",
    "calculationTypeDescription" : "Item Based"
    "amount" : 4.99
    "baseAmount" : 4.99
    "capAmount" : 9.99
    "distributionPercent" : 100.0
    "calculationValue" : 0.0
}

```

Creates a new shipping method rate.

##### Arguments

* calculationType (required)
* amount (optional)
* baseAmount (optional)
* capAmount (optional)
* distributionPercent (optional)
* calculationValue (optional)
* zone (optional)

##### Returns

Returns a shipping method rate object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a shipping method rate

```
DEFINITION
GET http://apiserver/shippingmethods/:id/rates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/rates/12085");

EXAMPLE RESPONSE
{
    "id" : "12085",
    "zone" : null,
    "zoneDescription" : null,
    "calculationType" : "I",
    "calculationTypeDescription" : "Item Based"
    "amount" : 4.99
    "baseAmount" : 4.99
    "capAmount" : 9.99
    "distributionPercent" : 100.0
    "calculationValue" : 0.0
}

```

Retrieves the details of an existing shipping method. You need only supply the id.

##### Arguments

* id (required) - The id of the shipping method to be retrieved.

#### Update a shipping method rate

```
DEFINITION
POST http://apiserver/shippingmethods/:id/rate/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingmethods/2DAY/rate/12085", {
    "amount" : 5.99
});

EXAMPLE RESPONSE
{
    "id" : "12085",
    "zone" : null,
    "zoneDescription" : null,
    "calculationType" : "I",
    "calculationTypeDescription" : "Item Based"
    "amount" : 5.99
    "baseAmount" : 4.99
    "capAmount" : 9.99
    "distributionPercent" : 100.0
    "calculationValue" : 0.0
}


```

Updates the specified shipping method rate by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* calculationType (optional)
* amount (optional)
* baseAmount (optional)
* capAmount (optional)
* distributionPercent (optional)
* calculationValue (optional)
* zone (optional)

##### Returns

Returns the shipping method rate object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a shipping method rate

```
DEFINITION
DELETE http://apiserver/shippingmethods/:id/rates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/shippingmethods/2DAY/rates/12085", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a shipping method. It cannot be undone.

##### Arguments

* id (required) - The id of the shipping method to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the shipping method does not exist, this call returns an error.

#### List all shipping method rates

```
DEFINITION
GET http://apiserver/shippingmethods/:id/rates

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingmethods/2DAY/rates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id" : "12085",
            "zone" : null,
            "zoneDescription" : null,
            "calculationType" : "I",
            "calculationTypeDescription" : "Item Based"
            "amount" : 5.99
            "baseAmount" : 4.99
            "capAmount" : 9.99
            "distributionPercent" : 100.0
            "calculationValue" : 0.0
        },
        {...},
    ]
}

```

Returns a list of all shipping method rates.

##### Arguments

* zone

##### Returns

A dictionary with an items property that contains an array of up to limit shipping method rates, starting at index offset. Each entry in the array is a separate shipping method rate object. If no more shipping method rates are available, the resulting array will be empty. This request should never return an error.

### Shipping Quotes

#### Retrieve a shipping quote

```
Note: The GET method has been deprecated.  Use the POST method instead.

DEFINITION
GET http://apiserver/shippingquote

EXAMPLE REQUEST
$.get("http://localhost:49195/shippingquote?warehouse=UKWH&country=US&postalCode=75474&amount=200&weight=2&quantity=3&useInStudioOnline=true");

EXAMPLE RESPONSE
[
    {
        "id": "2DAY",
        "description": "UPS Next Day Air",
        "amount": 4.99,
        "isError": false,
        "errorMessage": null
    },
    {...},
    {...},
    ...
]

```

```
DEFINITION
POST http://apiserver/shippingquote

EXAMPLE REQUEST
$.post("http://localhost:49195/shippingquote", {
    "warehouse": "UKWH",
    "country": "US",
    "postalCode": "75474",
    "amount": 200,
    "weight": 2,
    "quantity": 3,
    "useInStudioOnline": true
});

EXAMPLE RESPONSE
[
    {
        "id": "2DAY",
        "description": "UPS Next Day Air",
        "amount": 4.99,
        "isError": false,
        "errorMessage": null
    },
    {...},
    {...},
    ...
]

```

Retrieves a shipping quote based on the specified criteria.

##### Arguments

* warehouse (required) - The warehouse code of the shipment.
* shippingMethod (optional) - Limits the results to only the specified shipping method.
* address (optional) - Line 1 of the destination address. (Required if `addressId` is not provided.)
* city (optional) - The city of the destination address. (Required if `addressId` is not provided.)
* state (optional) - The state of the destination address. Must be a defined state code. (Required if `addressId` is not provided.)
* country (optional) - The country code of the destination address. Must be a defined country code. (Required if `addressId` is not provided.)
* postalCode (optional) - The postal code of the destination address. Must be a defined postal code of the specified country. (Required if `addressId` is not provided.)
* amount (optional) - The amount of the order. (Required if `inventoryItems` is not provided.)
* weight (optional) - The weight of the shipment. (Required if `inventoryItems` is not provided.)
* quantity (optional) - The quantity of the shipment. (Required if `inventoryItems` is not provided.)
* useInStudioOnline (optional) - Whether or not the shipping method is published to StudioOnline.
* freeProductsWeight (optional) - The weight of free products in the shipment.
* freeProductsQuantity (optional) - The quantity of free products in the shipment.
* includeErrors (optional) - Set as `true` if you want to receive all shipping rates, even if there was an error in calculating the rate.
* inventoryItems (optional) - Can be set instead of using `amount`, `weight`, and `quantity`.
  + productCode (required) - The product code of the item to ship.
  + quantity (required) - The quantity of the product to ship.
  + price (required) - The price of the product to ship.
  + discountAmount (optional) - The overall discount amount of the product to ship. (This is the discount amount over the whole quantity.)
* company (optional) - Used if `inventoryItems` is included and `weight` is not populated.
* addressId (optional) - Used instead of the separate address components

##### Returns

Returns an array of shipping quote option objects.

### SmartyStreets Configuration

#### Retrieve SmartyStreets configuration

```
DEFINITION
GET http://apiserver/smartystreets/configuration

EXAMPLE REQUEST
$.get("http://localhost:49195/smartystreets/configuration);

EXAMPLE RESPONSE
{
    "BackButtonText": null,
    "ContinueButtonText": "Save",
    "ClarifyAddressMessage": null,
    "ConfirmAddressAdjustmentMessage": null,
    "VerifyAddressMessage": "Verify this"
}

```

Retrieves the current SmartyStreets configuration.

##### Arguments

* No arguments are taken.

##### Returns

Returns one Integration Configuration object for the only "SMARTST" type and "ADDRSTDSVC" type-category record in the database. All credentials are removed from the object before it is returned.

### StudioOnline PayPal REST API Payments

#### Create a PayPal REST API Payment

```
DEFINITION
POST http://apiserver/studioonline/paypal/payments/create

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonline/paypal/payments/create", {
    "store": "10023",
    "transactionData": "{
        \"account\": {},
        \"contactMethod\": \"MAIL\",
        \"shippingMethod\": \"2DAY\",
        \"tangibleCode\": \"100BKLET\",
        \"cartItems\": {
            \"orders\": [{
                \"orderDetails\": [{
                    \"productCode\": \"100BKLET\",
                    \"isShippable\": true,
                    \"quantity\": 1,
                    \"price\": 1.5000,
                    \"sourceCode\": null,
                    \"productPriceType\": \"Retail\",
                    \"suggestedDonation\": false
                }],
                \"addressId\": null,
                \"recipientAccountNumber\": null,
                \"shipMethod\": null,
                \"warehouse\": \"30\"
            }]
        },
        \"tangibleType\": \"Product\"
    }",
    "userToken": "AA28CF39-54D7-4373-8549-B686951632A6"
});

EXAMPLE RESPONSE
{
    "paymentId": "PAY-8RU15504000896635LNB4QMY"
}

```

Makes a server-side call to the PayPal API to authorize a payment for the StudioOnline cart.

##### Arguments

* store (required) - The StudioOnline store that the OPCO/belongs to.
* company (required) - The company that the StudioOnline store is configured for.
* userToken (required) - The user token of the user completing the cart/OPCO.
* transactionData (required) - The shopping cart data that is passed into the typical cart checkout, in a JSON string form.

##### Returns

Returns an object that contains a payment id if the call succeeded. Returns an error if create parameters are invalid.

### StudioOnline Stores

#### Create a store

```
DEFINITION
POST http://apiserver/store

EXAMPLE REQUEST
$.post("http://localhost:49195/stores", {
    "databaseServer": "SQLServerInstance",
    "databaseName": "ASODatabase",
    "description": "Advanced StudioOnline"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "description": "Advanced StudioOnline",
    "databaseServer": "SQLServerInstance",
    "databaseName": "ASODatabase",
    "url": null,
    "company": null,
    "companyDescription": null,
    "paymentGatewayCode": null,
    "paymentGatewayDescription": null,
    "defaultWarehouse": null,
    "defaultWarehouseDescription": null,
    "currency": null,
    "currencyDescription": null,
    "passwordRequireUppercase": false,
    "passwordRequireLowercase": false,
    "passwordRequireSpecialCharacter": false,
    "passwordRequireNumber": false,
    "passwordMinimumLength": null,
    "passwordMaximumFailedAttempts": null,
    "passwordLockoutLengthInMinutes": null,
    "defaultSource": null,
    "defaultSourceDescription": null,
    "defaultRecurringCategory": null,
    "defaultRecurringCategoryDescription": null,
    "defaultRecurringSource": null,
    "defaultRecurringSourceDescription": null,
    "defaultShippingMethod": null,
    "defaultShippingMethodDescription": null,
    "freeShippingMethod": null,
    "freeShippingMethodDescription": null,
    "downloadShippingMethod": null,
    "downloadShippingMethodDescription": null,
    "retailPriceCode": null,
    "retailPriceCodeDescription": null,
    "salePriceCode": null,
    "salePriceCodeDescription": null,
    "suggestedDonationPriceCode": null,
    "suggestedDonationPriceCodeDescription": null,
    "premiumPriceCode": null,
    "premiumPriceCodeDescription": null,
    "defaultFailedTransactionContactMethod": null,
    "defaultFailedTransactionContactMethodDescription": null,
    "defaultFailedTransactionMediaCode": null,
    "defaultFailedTransactionMediaCodeDescription": null,
    "defaultFailedTransactionSource": null,
    "defaultFailedTransactionSourceDescription": null,
    "defaultFailedDonationProject": null,
    "defaultFailedDonationProjectDescription": null,
    "defaultFailedDonationSource": null,
    "defaultFailedDonationSourceDescription": null,
    "defaultFailedDonationSubaccount": null,
    "defaultFailedDonationSubaccountDescription": null,
    "defaultFailedDonationRecurringFrequency": null,
    "defaultFailedDonationRecurringFrequencyDescription": null,
    "defaultFailedDonationRecurringUseOnDay": null,
    "defaultFailedDonationRecurringUseOnDayDescription": null,
    "defaultFailedDonationRecurringCategory": null,
    "defaultFailedDonationRecurringCategoryDescription": null,
    "constituentEmailFromAddress: null,
    "passwordResetEmailTemplateId": null,
    "passwordResetEmailTemplateDescription": null,
    "checkoutConfirmationEmailTemplateId": null,
    "checkoutConfirmationEmailTemplateDescription": null,
    "eventSessionPriceCode": null,
    "eventSessionPriceCodeDescription": null,
    "defaultMediaCode": null,
    "defaultMediaCodeDescription": null
}

```

Creates a new store.

##### Arguments

* databaseServer (required) - The server name of store database.
* databaseName (required) - The database name of store database.
* description (optional) - The description of store.
* url (optional) - The base Url of the store.
* company (optional) - The company code of the store.
* paymentGatewayCode (optional) - The company payment gateway code of the store.
* defaultWarehouse (optional) - The default warehouse of the store.
* currency (optional) - The currency code of the store.
* passwordRequireUppercase (optional) - Whether an uppercase character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordRequireLowercase (optional) - Whether a lowercase character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordRequireSpecialCharacter (optional) - Whether a special character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordRequireNumber (optional) - Whether a numberic character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordMinimumLength (optional) - The minimum length required for a StudioOnline account password.
* passwordMaximumFailedAttempts (optional) - The maximum number of failed login attempts before the StudioOnline account is locked.
* passwordLockoutLengthInMinutes (optional) - The number of minutes the StudioOnline is locked when reaching the maximum number of failed attempts.
* defaultSource (optional) - The default source code for the store.
* defaultRecurringCategory (optional) - The default recurring category for the store.
* defaultRecurringSource (optional) - The default recurring source code for the store.
* defaultShippingMethod (optional) - The default shipping method for the store.
* freeShippingMethod (optional) - The free shipping method for the store.
* downloadShippingMethod (optional) - The download shipping method for the store.
* retailPriceCode (optional) - The retail price code for the store.
* salePriceCode (optional) - The sales price code for the store.
* suggestedDonationPriceCode (optional) - The suggested donation price code for the store.
* premiumPriceCode (optional) - The premium price code for the store.
* defaultFailedTransactionContactMethod (optional) - The default contact method if the contact method of the transaction is invalid.
* defaultFailedTransactionMediaCode (optional) - The default media code if the media code of the transaction is invalid.
* defaultFailedTransactionSource (optional) - The default source code if the source code of the transaction is invalid.
* defaultFailedDonationProject (optional) - The default project code if the project code of the transaction donation is invalid.
* defaultFailedDonationSource (optional) - The default source code if the source code of the transaction donation is invalid.
* defaultFailedDonationSubaccount (optional) - The default subaccount if the subaccount of the transaction donation is invalid.
* defaultFailedDonationRecurringFrequency (optional) - The default recurring frequency if the recurring frequency of the recurring is invalid.
* defaultFailedDonationRecurringUseOnDay (optional) - The default recurring use on day if the recurring use on day of the recurring is invalid.
* defaultFailedDonationRecurringCategory (optional) - The recurring category set to the recurring if transaction validation has failed.
* constituentEmailFromAddress (optional) - The email address that all constituent emails sent from this store are from.
* passwordResetEmailTemplateId (optional) - The email template to use when sending a password reset email from this store.
* checkoutConfirmationEmailTemplateId (optional) - The email template to use when sending a checkout confirmation email from this store.
* eventSessionPriceCode (optional) - The event session price code for the store.
* defaultMediaCode (optional) - The default media code used for the store.

##### Returns

Returns a store object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a store

```
DEFINITION
GET http://apiserver/stores/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "description": "Advanced StudioOnline",
    "databaseServer": "SQLServerInstance",
    "databaseName": "ASODatabase",
    "url": null,
    "company": null,
    "companyDescription": null,
    "paymentGatewayCode": null,
    "paymentGatewayDescription": null,
    "defaultWarehouse": null,
    "defaultWarehouseDescription": null,
    "currency": null,
    "currencyDescription": null,
    "passwordRequireUppercase": false,
    "passwordRequireLowercase": false,
    "passwordRequireSpecialCharacter": false,
    "passwordRequireNumber": false,
    "passwordMinimumLength": null,
    "passwordMaximumFailedAttempts": null,
    "passwordLockoutLengthInMinutes": null,
    "defaultSource": null,
    "defaultSourceDescription": null,
    "defaultRecurringCategory": null,
    "defaultRecurringCategoryDescription": null,
    "defaultRecurringSource": null,
    "defaultRecurringSourceDescription": null,
    "defaultShippingMethod": null,
    "defaultShippingMethodDescription": null,
    "freeShippingMethod": null,
    "freeShippingMethodDescription": null,
    "downloadShippingMethod": null,
    "downloadShippingMethodDescription": null,
    "retailPriceCode": null,
    "retailPriceCodeDescription": null,
    "salePriceCode": null,
    "salePriceCodeDescription": null,
    "suggestedDonationPriceCode": null,
    "suggestedDonationPriceCodeDescription": null,
    "premiumPriceCode": null,
    "premiumPriceCodeDescription": null,
    "defaultFailedTransactionContactMethod": null,
    "defaultFailedTransactionContactMethodDescription": null,
    "defaultFailedTransactionMediaCode": null,
    "defaultFailedTransactionMediaCodeDescription": null,
    "defaultFailedTransactionSource": null,
    "defaultFailedTransactionSourceDescription": null,
    "defaultFailedDonationProject": null,
    "defaultFailedDonationProjectDescription": null,
    "defaultFailedDonationSource": null,
    "defaultFailedDonationSourceDescription": null,
    "defaultFailedDonationSubaccount": null,
    "defaultFailedDonationSubaccountDescription": null,
    "defaultFailedDonationRecurringFrequency": null,
    "defaultFailedDonationRecurringFrequencyDescription": null,
    "defaultFailedDonationRecurringUseOnDay": null,
    "defaultFailedDonationRecurringUseOnDayDescription": null,
    "defaultFailedDonationRecurringCategory": null,
    "defaultFailedDonationRecurringCategoryDescription": null,
    "constituentEmailFromAddress: null,
    "passwordResetEmailTemplateId": null,
    "passwordResetEmailTemplateDescription": null,
    "checkoutConfirmationEmailTemplateId": null,
    "checkoutConfirmationEmailTemplateDescription": null,
    "eventSessionPriceCode": null,
    "eventSessionPriceCodeDescription": null,
    "defaultMediaCode": null,
    "defaultMediaCodeDescription": null
}

```

Retrieves the details of an existing store. You need only supply the id.

##### Arguments

* id (required) - The id of the store to be retrieved.

#### Update a store

```
DEFINITION
POST http://apiserver/stores/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/1", {
    "url": "https://www.ministry.com"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "description": "Advanced StudioOnline",
    "databaseServer": "SQLServerInstance",
    "databaseName": "ASODatabase",
    "url": "https://www.ministry.com",
    "company": null,
    "companyDescription": null,
    "paymentGatewayCode": null,
    "paymentGatewayDescription": null,
    "defaultWarehouse": null,
    "defaultWarehouseDescription": null,
    "currency": null,
    "currencyDescription": null,
    "passwordRequireUppercase": false,
    "passwordRequireLowercase": false,
    "passwordRequireSpecialCharacter": false,
    "passwordRequireNumber": false,
    "passwordMinimumLength": null,
    "passwordMaximumFailedAttempts": null,
    "passwordLockoutLengthInMinutes": null,
    "defaultSource": null,
    "defaultSourceDescription": null,
    "defaultRecurringCategory": null,
    "defaultRecurringCategoryDescription": null,
    "defaultRecurringSource": null,
    "defaultRecurringSourceDescription": null,
    "defaultShippingMethod": null,
    "defaultShippingMethodDescription": null,
    "freeShippingMethod": null,
    "freeShippingMethodDescription": null,
    "downloadShippingMethod": null,
    "downloadShippingMethodDescription": null,
    "retailPriceCode": null,
    "retailPriceCodeDescription": null,
    "salePriceCode": null,
    "salePriceCodeDescription": null,
    "suggestedDonationPriceCode": null,
    "suggestedDonationPriceCodeDescription": null,
    "premiumPriceCode": null,
    "premiumPriceCodeDescription": null,
    "defaultFailedTransactionContactMethod": null,
    "defaultFailedTransactionContactMethodDescription": null,
    "defaultFailedTransactionMediaCode": null,
    "defaultFailedTransactionMediaCodeDescription": null,
    "defaultFailedTransactionSource": null,
    "defaultFailedTransactionSourceDescription": null,
    "defaultFailedDonationProject": null,
    "defaultFailedDonationProjectDescription": null,
    "defaultFailedDonationSource": null,
    "defaultFailedDonationSourceDescription": null,
    "defaultFailedDonationSubaccount": null,
    "defaultFailedDonationSubaccountDescription": null,
    "defaultFailedDonationRecurringFrequency": null,
    "defaultFailedDonationRecurringFrequencyDescription": null,
    "defaultFailedDonationRecurringUseOnDay": null,
    "defaultFailedDonationRecurringUseOnDayDescription": null,
    "defaultFailedDonationRecurringCategory": null,
    "defaultFailedDonationRecurringCategoryDescription": null,
    "constituentEmailFromAddress: null,
    "passwordResetEmailTemplateId": null,
    "passwordResetEmailTemplateDescription": null,
    "checkoutConfirmationEmailTemplateId": null,
    "checkoutConfirmationEmailTemplateDescription": null,
    "eventSessionPriceCode": null,
    "eventSessionPriceCodeDescription": null,
    "defaultMediaCode": null,
    "defaultMediaCodeDescription": null
}


```

Updates the specified store by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* databaseServer (optional) - The server name of store database.
* databaseName (optional) - The database name of store database.
* description (optional) - The description of store.
* url (optional) - The base Url of the store.
* company (optional) - The company code of the store.
* paymentGatewayCode (optional) - The company payment gateway code of the store.
* defaultWarehouse (optional) - The default warehouse of the store.
* currency (optional) - The currency code of the store.
* passwordRequireUppercase (optional) - Whether an uppercase character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordRequireLowercase (optional) - Whether a lowercase character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordRequireSpecialCharacter (optional) - Whether a special character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordRequireNumber (optional) - Whether a numberic character is required for a StudioOnline account password. (Defaults to `false`.)
* passwordMinimumLength (optional) - The minimum length required for a StudioOnline account password.
* passwordMaximumFailedAttempts (optional) - The maximum number of failed login attempts before the StudioOnline account is locked.
* passwordLockoutLengthInMinutes (optional) - The number of minutes the StudioOnline is locked when reaching the maximum number of failed attempts.
* defaultSource (optional) - The default source code for the store.
* defaultRecurringCategory (optional) - The default recurring category for the store.
* defaultRecurringSource (optional) - The default recurring source code for the store.
* defaultShippingMethod (optional) - The default shipping method for the store.
* freeShippingMethod (optional) - The free shipping method for the store.
* downloadShippingMethod (optional) - The download shipping method for the store.
* retailPriceCode (optional) - The retail price code for the store.
* salePriceCode (optional) - The sales price code for the store.
* suggestedDonationPriceCode (optional) - The suggested donation price code for the store.
* premiumPriceCode (optional) - The premium price code for the store.
* defaultFailedTransactionContactMethod (optional) - The default contact method if the contact method of the transaction is invalid.
* defaultFailedTransactionMediaCode (optional) - The default media code if the media code of the transaction is invalid.
* defaultFailedTransactionSource (optional) - The default source code if the source code of the transaction is invalid.
* defaultFailedDonationProject (optional) - The default project code if the project code of the transaction donation is invalid.
* defaultFailedDonationSource (optional) - The default source code if the source code of the transaction donation is invalid.
* defaultFailedDonationSubaccount (optional) - The default subaccount if the subaccount of the transaction donation is invalid.
* defaultFailedDonationRecurringFrequency (optional) - The default recurring frequency if the recurring frequency of the recurring is invalid.
* defaultFailedDonationRecurringUseOnDay (optional) - The default recurring use on day if the recurring use on day of the recurring is invalid.
* defaultFailedDonationRecurringCategory (optional) - The recurring category set to the recurring if transaction validation has failed.
* constituentEmailFromAddress (optional) - The email address that all constituent emails sent from this store are from.
* passwordResetEmailTemplateId (optional) - The email template to use when sending a password reset email from this store.
* checkoutConfirmationEmailTemplateId (optional) - The email template to use when sending a checkout confirmation email from this store.
* eventSessionPriceCode (optional) - The event session price code for the store.
* defaultMediaCode (optional) - The default media code used for the store.

##### Returns

Returns the store object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a store

```
DEFINITION
DELETE http://apiserver/stores/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/stores/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a store. It cannot be undone.

##### Arguments

* id (required) - The id of the store to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the store does not exist, this call returns an error.

#### List all stores

```
DEFINITION
GET http://apiserver/stores

EXAMPLE REQUEST
$.get("http://localhost:49195/stores?description=*Studio*");

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
            "description": "Advanced StudioOnline",
            "databaseServer": "SQLServerInstance",
            "databaseName": "ASODatabase",
            "url": "https://www.ministry.com",
            "company": null,
            "companyDescription": null,
            "paymentGatewayCode": null,
            "paymentGatewayDescription": null,
            "defaultWarehouse": null,
            "defaultWarehouseDescription": null,
            "currency": null,
            "currencyDescription": null,
            "passwordRequireUppercase": false,
            "passwordRequireLowercase": false,
            "passwordRequireSpecialCharacter": false,
            "passwordRequireNumber": false,
            "passwordMinimumLength": null,
            "passwordMaximumFailedAttempts": null,
            "passwordLockoutLengthInMinutes": null,
            "defaultSource": null,
            "defaultSourceDescription": null,
            "defaultRecurringCategory": null,
            "defaultRecurringCategoryDescription": null,
            "defaultRecurringSource": null,
            "defaultRecurringSourceDescription": null,
            "defaultShippingMethod": null,
            "defaultShippingMethodDescription": null,
            "freeShippingMethod": null,
            "freeShippingMethodDescription": null,
            "downloadShippingMethod": null,
            "downloadShippingMethodDescription": null,
            "retailPriceCode": null,
            "retailPriceCodeDescription": null,
            "salePriceCode": null,
            "salePriceCodeDescription": null,
            "suggestedDonationPriceCode": null,
            "suggestedDonationPriceCodeDescription": null,
            "premiumPriceCode": null,
            "premiumPriceCodeDescription": null,
            "defaultFailedTransactionContactMethod": null,
            "defaultFailedTransactionContactMethodDescription": null,
            "defaultFailedTransactionMediaCode": null,
            "defaultFailedTransactionMediaCodeDescription": null,
            "defaultFailedTransactionSource": null,
            "defaultFailedTransactionSourceDescription": null,
            "defaultFailedDonationProject": null,
            "defaultFailedDonationProjectDescription": null,
            "defaultFailedDonationSource": null,
            "defaultFailedDonationSourceDescription": null,
            "defaultFailedDonationSubaccount": null,
            "defaultFailedDonationSubaccountDescription": null,
            "defaultFailedDonationRecurringFrequency": null,
            "defaultFailedDonationRecurringFrequencyDescription": null,
            "defaultFailedDonationRecurringUseOnDay": null,
            "defaultFailedDonationRecurringUseOnDayDescription": null,
            "defaultFailedDonationRecurringCategory": null,
            "defaultFailedDonationRecurringCategoryDescription": null,
            "constituentEmailFromAddress: null,
            "passwordResetEmailTemplateId": null,
            "passwordResetEmailTemplateDescription": null,
            "checkoutConfirmationEmailTemplateId": null,
            "checkoutConfirmationEmailTemplateDescription": null,
            "eventSessionPriceCode": null,
            "eventSessionPriceCodeDescription": null,
            "defaultMediaCode": null,
            "defaultMediaCodeDescription": null
        },
        {...},
    ]
}

```

Returns a list of all stores.

##### Arguments

* id (optional) - Filter list the id of the store.
* description (optional) - Filter list by partial match on the description of the store.
* databaseServer (optional) - Filter list by partial match on the database server of the store.
* databaseName (optional) - Filter list by partial match on the database name of the store.
* url (optional) - Filter list by partial match on the url of the store.
* company (optional) - Filter list by partial match on the company of the store.
* currency (optional) - Filter list by partial match on the currency of the store.

##### Returns

A dictionary with an items property that contains an array of up to limit stores, starting at index offset. Each entry in the array is a separate store object. If no more stores are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Store Apple Pay Payment Sessions

#### Create an Apple Pay payment session

```
DEFINITION
POST http://apiserver/stores/:storeId/applepay/paymentsessions

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/:storeId/applepay/paymentsessions", {
    "integrationConfigurationCode": "APPLEPAY",
    "validationUrl": "https://apple-pay-gateway.apple.com/paymentservices/paymentSession"
});

EXAMPLE RESPONSE
{
    "paymentSession": {
        ... Opaque Apple Pay Payment Session object ...
    }
}

```

Creates an Apple Pay payment session.

##### Arguments

* integrationConfigurationCode (required) - The code of the Apple Pay integration configuration used by the StudioOnline store.
* validationUrl (required) - The fully qualified validation URL received in the call to Apple Pay's onvalidatemerchant method. The URL's domain must be one of the whitelisted Apple Pay domains.

##### Returns

Returns an opaque Apple Pay session object for Apple Pay on the web and for Apple Pay in Apple Messages for Business. Returns an error if create parameters are invalid.

### StudioOnline Store Categories

#### Create a store category

```
DEFINITION
POST http://apiserver/stores/:id/categories

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/categories", {
    "name": "Projects",
    "weight": 0,
    "isActive": true,
    "includeAsSearchFilter": true,
    "description": "Project category",
    "layoutOverride": null,
    "sequence": 1
});

EXAMPLE RESPONSE
{
    "id": "1",
    "name": "Projects",
    "breadcrumb": "projects",
    "parentCategoryId": null,
    "parentCategoryName": null,
    "description": "Project category",
    "weight": 0,
    "layoutOverride": null,
    "isActive": true,
    "includeAsSearchFilter": true,
    "isRelatedTangiblesCategory": false,
    "priceCodeRestriction": null,
    "categoryType": null,
    "categoryTypeDescription": null,
    "maxItemsInCategory": 0,
    "maxNumberOfDays": 0,
    "minPurchasedTogetherOccurences": 0,
    "sequence": 1
}

```

Creates a new store category.

##### Arguments

* name (required) - The name of the store category, this is also used for the URL.
* weight (required : 0-99) - Weight modifier applied to tangibles in this store category.
* isActive (required) - Indicates whether the store category is active. A value of true will cascade up parent store categories.
* includeAsSearchFilter (required) - Indicates whether the store category should be included as a filter in StudioOnline when searching. A value of true will cascade up parent store categories.
* description (optional) - Description of the store category.
* layoutOverride (optional) - Id of StudioOnline layout to use for this store category on the Category Page.
* parentCategoryId (optional) - Sets the parent store category. Must be a valid store category. Must not cause a cycle (e.g. Category A has parent Category B which has parent Category A).
* isRelatedTangiblesCategory (optional) - Indicates whether the store category should be used a the related store category.
* categoryType (optional) - The category type for this category. Must either be null (standard category) or a valid X04 for the code type `SOCATTYPE`.
* priceCodeRestriction (optional) - Indicates that only products that contain an active price with this price code will appear in the store category. (No other tangible types will appear in the store category.)
* sequence (optional) - The sequence number of the store category.

##### Returns

Returns a store category object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a store category

```
DEFINITION
GET http://apiserver/stores/:id/categories/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "name": "Projects",
    "breadcrumb": "projects",
    "parentCategoryId": null,
    "parentCategoryName": null,
    "description": "Project category",
    "weight": 0,
    "layoutOverride": null,
    "isActive": true,
    "includeAsSearchFilter": true,
    "isRelatedTangiblesCategory": false,
    "priceCodeRestriction": null,
    "categoryType": null,
    "categoryTypeDescription": null,
    "maxItemsInCategory": 0,
    "maxNumberOfDays": 0,
    "minPurchasedTogetherOccurences": 0,
    "sequence": 1
}

```

Retrieves the details of an existing store category. You need only supply the id.

##### Arguments

* id (required) - The id of the store category to be retrieved.

#### Update a store category

```
DEFINITION
POST http://apiserver/stores/:id/categories/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/categories/1", {
    "description": "Project Category"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "name": "Projects",
    "breadcrumb": "projects",
    "parentCategoryId": null,
    "parentCategoryName": null,
    "description": "Project Category",
    "weight": 0,
    "layoutOverride": null,
    "isActive": true,
    "includeAsSearchFilter": true,
    "isRelatedTangiblesCategory": false,
    "priceCodeRestriction": null,
    "categoryType": null,
    "categoryTypeDescription": null,
    "maxItemsInCategory": 0,
    "maxNumberOfDays": 0,
    "minPurchasedTogetherOccurences": 0,
    "sequence": 1
}


```

Updates the specified store category by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name (optional) - The name of the store category, this is also used for the URL.
* weight (optional : 0-99) - Weight modifier applied to tangibles in this store category.
* isActive (optional) - Indicates whether the store category is active. A value of true will cascade up parent store categories. A value of false will cascade down children store categories.
* includeAsSearchFilter (optional) - Indicates whether the store category should be included as a filter in StudioOnline when searching. A value of true will cascade up parent categories. A value of false will cascade down children store categories.
* description (optional) - Description of the store category.
* layoutOverride (optional) - Id of StudioOnline layout to use for this store category on the Category Page.
* parentCategoryId (optional) - Sets the parent store category. Must be a valid store category. Must not cause a cycle (e.g. Category A has parent Category B which has parent Category A).
* isRelatedTangiblesCategory (optional) - Indicates whether the store category should be used a the related store category.
* priceCodeRestriction (optional) - Indicates that only products that contain an active price with this price code will appear in the store category. (No other tangible types will appear in the store category.)
* sequence (optional) - The sequence number of the store category.

##### Returns

Returns the store category object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a store category

```
DEFINITION
DELETE http://apiserver/stores/:id/categories/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/stores/19/categories/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a store category. It cannot be undone. Deleting a store category with children will set their parentCategoryId to null.

##### Arguments

* id (required) - The id of the store category to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the store category does not exist, this call returns an error.

#### List all store categories

```
DEFINITION
GET http://apiserver/stores/:id/categories

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories?breadcrumb=*water*");

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
            "name": "Africa",
            "breadcrumb": "projects/water-wells/africa",
            "parentCategoryId": 2,
            "parentCategoryName": "Water Wells",
            "description": "African water wells",
            "weight": 0,
            "layoutOverride": null,
            "isActive": true,
            "includeAsSearchFilter": true,
            "isRelatedTangiblesCategory": false,
            "priceCodeRestriction": null,
            "categoryType": null,
            "categoryTypeDescription": null,
            "maxItemsInCategory": 0,
            "maxNumberOfDays": 0,
            "minPurchasedTogetherOccurences": 0,
            "sequence": 1
        },
        {...},
    ]
}

```

Returns a list of all store categories.

##### Arguments

* name (optional) - Filter list by partial match on the name of the store category.
* breadcrumb (optional) - Filter list by partial match on the breadcrumb of the store category.
* parentCategoryId (optional) - Filters the list by store categories with matching category parent Ids.
* active (optional) - Filter list by whether the store category is active (true for active, false for inactive, omit for all).
* relatedTangiblesCategory (optional) - If true, filters list by whether category is marked as a related tangibles category.
* filterAutoPopulatedCategories (optional) - If true, filters list by category type, removing best sellers and also bought categories.
* preventCyclesWith (optional) - Filters the list to store categories that do not cause cycles with the passed parameter.

##### Returns

A dictionary with an items property that contains an array of up to limit store categories, starting at index offset. Each entry in the array is a separate store category object. If no more store categories are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Store Category Images

#### Create a store category image

```
DEFINITION
POST http://apiserver/stores/:id/categories/:categoryId/images

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/categories/1/images", {
    "imageType": "IMAGEXS",
    "description": "Extra Small Category Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image",
    "title": "Image Title",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "2",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Category Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image",
    "title": "Image Title",
    "isActive": true
}

```

Creates a new store category image.

##### Arguments

* imageType (required) - the ImageType code value for the store category image.
* description (optional) - the description for the store category image.
* imageUrl (required) - the image URL for the store category image.
* alternateText (optional) - the alternate text for the store category image.
* title (optional) - the image title for the store category image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns a store category image object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a store category image

```
DEFINITION
GET http://apiserver/stores/:id/categories/:categoryId/images/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1/images/2");

EXAMPLE RESPONSE
{
    "id": "2",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Category Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image",
    "title": "Image Title",
    "isActive": true
}

```

Retrieves the details of an existing store category image. You need only supply the id.

##### Arguments

* id (required) - The id of the store category image to be retrieved.

#### Update a store category image

```
DEFINITION
POST http://apiserver/stores/:id/categories/:categoryId/images/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/categories/1/images/2", {
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png"
});

EXAMPLE RESPONSE
{
    "id": "2",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Category Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image",
    "title": "Image Title",
    "isActive": true
}


```

Updates the specified store category image by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* imageType (optional) - the ImageType code value to update for the store category image.
* description (optional) - the description to update for the store category image.
* imageUrl (optional) - the image URL to update for the store category image.
* alternateText (optional) - the alternate text to update for the store category image.
* title (optional) - the image title to update for the store category image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns the store category image object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a store category image

```
DEFINITION
DELETE http://apiserver/stores/:id/categories/:categoryId/images/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/stores/19/categories/1/images/2", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a store category image. It cannot be undone.

##### Arguments

* id (required) - The id of the store category image to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the store category image does not exist, this call returns an error.

#### List all store category images

```
DEFINITION
GET http://apiserver/stores/:id/categories/:categoryId/images

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1/images");

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
            "imageType": "IMAGEXS",
            "imageTypeDescription": "Extra Small Image",
            "description": "Extra Small Category Img",
            "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
            "alternateText": "Image",
            "title": "Image Title",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all store category images.

##### Returns

A dictionary with an items property that contains an array of up to limit store category images, starting at index offset. Each entry in the array is a separate store category image object. If no more store category images are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Store Category Notes

#### Create a store category note

```
DEFINITION
POST http://apiserver/stores/:id/categories/:categoryId/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/categories/1/notes", {
    "type": "SOCATNOTE",
    "shortComment": "Test",
    "longComment": "notey note"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "SOCATNOTE",
    "typeDescription": "SO Category note",
    "shortComment": "Test",
    "longComment": "notey note"
}

```

Creates a new store category note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a store category note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a store category note

```
DEFINITION
GET http://apiserver/stores/:id/categories/:categoryId/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1/notes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "SOCATNOTE",
    "typeDescription": "SO Category note",
    "shortComment": "Test",
    "longComment": "notey note"
}

```

Retrieves the details of an existing store category note. You need only supply the id.

##### Arguments

* id (required) - The id of the store category note to be retrieved.

#### Update a store category note

```
DEFINITION
POST http://apiserver/stores/:id/categories/:categoryId/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/categories/1/notes/1", {
    "shortComment": "fun"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "SOCATNOTE",
    "typeDescription": "SO Category note",
    "shortComment": "fun",
    "longComment": "notey note"
}


```

Updates the specified store category note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the store category note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a store category note

```
DEFINITION
DELETE http://apiserver/stores/:id/categories/:categoryId/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/stores/19/categories/1/notes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a store category note. It cannot be undone.

##### Arguments

* id (required) - The id of the store category note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the store category note does not exist, this call returns an error.

#### List all store category notes

```
DEFINITION
GET http://apiserver/stores/:id/categories/:categoryId/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1/notes");

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
            "type": "SOCATNOTE",
            "typeDescription": "SO Category note",
            "shortComment": "fun",
            "longComment": "notey note"
        },
        {...},
    ]
}

```

Returns a list of all store category notes.

##### Returns

A dictionary with an items property that contains an array of up to limit store category notes, starting at index offset. Each entry in the array is a separate store category note object. If no more store category notes are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Store Category SubCategories

#### List all store category subcategories

```
DEFINITION
GET http://apiserver/stores/:id/categories/:categoryId/subcategories

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1/subcategories");

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
            "name": "Water Wells",
            "breadcrumb": "projects/water-wells",
            "parentCategoryId": 1,
            "parentCategoryName": "Projects",
            "description": "Water Wells category",
            "weight": 0,
            "layoutOverride": null,
            "isActive": true,
            "includeAsSearchFilter": true,
            "isRelatedTangiblesCategory": false,
            "priceCodeRestriction": null,
            "categoryType": null,
            "categoryTypeDescription": null,
            "maxItemsInCategory": 0,
            "maxNumberOfDays": 0,
            "minPurchasedTogetherOccurences": 0,
            "sequence": 10
        },
        {...},
    ]
}

```

Returns a list of all store category subcategories.

##### Returns

Returns a list of all store category subcategories.

### StudioOnline Store Category Tangibles

#### Retrieve a store category tangible

```
DEFINITION
GET http://apiserver/stores/:id/categories/:id/tangibles/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1/tangibles/2");

EXAMPLE RESPONSE
{
    "id": "2",
    "tangibleType": "Project",
    "TangibleCode": "PROJECT10",
    "sequence": 10,
    "title": "Project 10",
    "isPublished": true,
    "startDate": "2024-03-25",
    "endDate": "2030-12-31
}

```

Retrieves the details of an existing store category tangible. You need only supply the id.

##### Arguments

* id (required) - The id of the store category tangible to be retrieved.

##### Returns

Returns the store category tangible object if the call succeeded. Returns an error if create parameters are invalid.

#### Update a store category tangible

```
DEFINITION
POST http://apiserver/stores/:id/categories/:id/tangibles/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/categories/1/tangibles/2", {
    "sequence": 20
});

EXAMPLE RESPONSE
{
    "id": "2",
    "tangibleType": "Project",
    "TangibleCode": "PROJECT10",
    "sequence": 20,
    "title": "Project 10",
    "isPublished": true,
    "startDate": "2024-03-25",
    "endDate": "2030-12-31
}

```

Updates the specified store category tangible by setting the value of the sequence. All other properties will be left unchanged.

##### Arguments

* sequence (optional) - The sequence of the store category tangible.

##### Returns

Returns the store category tangible object if the update succeeded. Returns an error if update parameters are invalid.

#### List all store category tangibles

```
DEFINITION
GET http://apiserver/stores/:id/categories/:id/tangibles

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/categories/1/tangibles");

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
            "tangibleType": "Project",
            "TangibleCode": "PROJECT10",
            "sequence": 10,
            "title": "Project 10",
            "isPublished": true,
            "startDate": "2024-03-25",
            "endDate": "2030-12-31
        },
        {...},
    ]
}

```

Returns a list of all store category tangibles.

##### Returns

Returns a list of all store category tangibles.

### StudioOnline Store Giving Array Overrides

#### Create a store giving array override

```
DEFINITION
POST http://apiserver/stores/:id/givingarrayoverrides

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/givingarrayoverrides", {
    "marketingCodeType": "DONTRACK",
    "marketingCodeValue": "2",
    "project": null,
    "showOther": true,
    "customSql": "SELECT DISTINCT TOP 5 [T04].[TotalAmount] FROM [dbo].[T04_GiftDetails] T04\n\tJOIN [dbo].[T01_TransactionMaster] T01 ON [T01].[DocumentNumber] = [T04].[DocumentNumber]\n\tWHERE t01.[AccountNumber] IN (SELECT AccountNumber FROM [dbo].[GetAllFamilyAccountNumbersByAccountNumber](#ACCOUNT#))\n\tORDER BY [T04].[TotalAmount] DESC",
    "givingAmounts": "10,20,30,40,50,60,70,WHAT,80,90,100,102,102.51"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "marketingCodeType": "DONTRACK",
    "marketingCodeTypeDescription": "Donor Track",
    "marketingCodeValue": "2",
    "marketingCodeValueDescription": "Track 2",
    "project": null,
    "projectDescription": null,
    "showOther": true,
    "customSql": "SELECT DISTINCT TOP 5 [T04].[TotalAmount] FROM [dbo].[T04_GiftDetails] T04\n\tJOIN [dbo].[T01_TransactionMaster] T01 ON [T01].[DocumentNumber] = [T04].[DocumentNumber]\n\tWHERE t01.[AccountNumber] IN (SELECT AccountNumber FROM [dbo].[GetAllFamilyAccountNumbersByAccountNumber](#ACCOUNT#))\n\tORDER BY [T04].[TotalAmount] DESC",
    "givingAmounts": "10,20,30,40,50,60,70,WHAT,80,90,100,102,102.51"
}

```

Creates a new store giving array override.

##### Arguments

* marketingCodeType (required) - The account marketing attribute code type to use for the this store giving array override.
* marketingCodeValue (required) - The account marketing attribute code type value to use for the this store giving array override.
* project (optional) - The project to use for this store giving array override.
* showOther (required) - Whether the Other gift amount option would appear for the giving array.
* customSql (optional) - Custom SQL to use to retrieve the giving amounts for this giving array override. (The following parameters can be used: `#MARKETING_TYPE#`, `#MARKETING_VALUE#`, `#TANGIBLE_TYPE#`, `#TANGIBLE_CODE#`, and `#ACCOUNT#`. The Custom Sql should return either a table with single-columned rows of data that can be automatically converted to a VARCHAR or a single row with a single VARCHAR column of comma delimited amounts. Either customSql or givingAmounts is required.)
* givingAmounts (optional) - Comma delimited list of giving amounts for this giving array override. (Either customSql or givingAmounts is required.)

##### Returns

Returns a store giving array override object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a store giving array override

```
DEFINITION
GET http://apiserver/stores/:id/givingarrayoverrides/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/givingarrayoverrides/1");

EXAMPLE RESPONSE
{
    "id": "3",
    "marketingCodeType": "DONTRACK",
    "marketingCodeTypeDescription": "Donor Track",
    "marketingCodeValue": "2",
    "marketingCodeValueDescription": "Track 2",
    "project": null,
    "projectDescription": null,
    "showOther": true,
    "customSql": "SELECT DISTINCT TOP 5 [T04].[TotalAmount] FROM [dbo].[T04_GiftDetails] T04\n\tJOIN [dbo].[T01_TransactionMaster] T01 ON [T01].[DocumentNumber] = [T04].[DocumentNumber]\n\tWHERE t01.[AccountNumber] IN (SELECT AccountNumber FROM [dbo].[GetAllFamilyAccountNumbersByAccountNumber](#ACCOUNT#))\n\tORDER BY [T04].[TotalAmount] DESC",
    "givingAmounts": "10,20,30,40,50,60,70,WHAT,80,90,100,102,102.51"
}

```

Retrieves the details of an existing store giving array override. You need only supply the id.

##### Arguments

* id (required) - The id of the store giving array override to be retrieved.

#### Update a store giving array override

```
DEFINITION
POST http://apiserver/stores/:id/givingarrayoverrides/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/stores/19/givingarrayoverrides/1", {
    "givingAmounts": "10,20,30,40,50,60,70"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "marketingCodeType": "DONTRACK",
    "marketingCodeTypeDescription": "Donor Track",
    "marketingCodeValue": "2",
    "marketingCodeValueDescription": "Track 2",
    "project": null,
    "projectDescription": null,
    "showOther": true,
    "customSql": "SELECT DISTINCT TOP 5 [T04].[TotalAmount] FROM [dbo].[T04_GiftDetails] T04\n\tJOIN [dbo].[T01_TransactionMaster] T01 ON [T01].[DocumentNumber] = [T04].[DocumentNumber]\n\tWHERE t01.[AccountNumber] IN (SELECT AccountNumber FROM [dbo].[GetAllFamilyAccountNumbersByAccountNumber](#ACCOUNT#))\n\tORDER BY [T04].[TotalAmount] DESC",
    "givingAmounts": "10,20,30,40,50,60,70"
}


```

Updates the specified store giving array override by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* marketingCodeType (optional) - The account marketing attribute code type to use for the this store giving array override.
* marketingCodeValue (optional) - The account marketing attribute code type value to use for the this store giving array override.
* project (optional) - The project to use for this store giving array override.
* showOther (optional) - Whether the Other gift amount option would appear for the giving array.
* customSql (optional) - Custom SQL to use to retrieve the giving amounts for this giving array override. (The following parameters can be used: `#MARKETING_TYPE#`, `#MARKETING_VALUE#`, `#TANGIBLE_TYPE#`, `#TANGIBLE_CODE#`, and `#ACCOUNT#`. The Custom Sql should return either a table with single-columned rows of data that can be automatically converted to a VARCHAR or a single row with a single VARCHAR column of comma delimited amounts. Either customSql or givingAmounts is required to be populated.)
* givingAmounts (optional) - Comma delimited list of giving amounts for this giving array override. (Either customSql or givingAmounts is required to be populated.)

##### Returns

Returns the store giving array override object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a store giving array override

```
DEFINITION
DELETE http://apiserver/stores/:id/givingarrayoverrides/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/stores/19/givingarrayoverrides/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a store giving array override. It cannot be undone.

##### Arguments

* id (required) - The id of the store giving array override to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the store giving array override does not exist, this call returns an error.

#### List all store giving array overrides

```
DEFINITION
GET http://apiserver/stores/:id/givingarrayoverrides

EXAMPLE REQUEST
$.get("http://localhost:49195/stores/19/givingarrayoverrides?marketingCodeType=DONTRACK");

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
            "marketingCodeType": "DONTRACK",
            "marketingCodeTypeDescription": "Donor Track",
            "marketingCodeValue": "2",
            "marketingCodeValueDescription": "Track 2",
            "project": null,
            "projectDescription": null,
            "showOther": true,
            "customSql": "SELECT DISTINCT TOP 5 [T04].[TotalAmount] FROM [dbo].[T04_GiftDetails] T04\n\tJOIN [dbo].[T01_TransactionMaster] T01 ON [T01].[DocumentNumber] = [T04].[DocumentNumber]\n\tWHERE t01.[AccountNumber] IN (SELECT AccountNumber FROM [dbo].[GetAllFamilyAccountNumbersByAccountNumber](#ACCOUNT#))\n\tORDER BY [T04].[TotalAmount] DESC",
            "givingAmounts": "10,20,30,40,50,60,70"
        },
        {...},
    ]
}

```

Returns a list of all store giving array overrides.

##### Arguments

* marketingCodeType (optional) - Filter list by partial match on the marketing code type of the store giving array override.
* marketingCodeValue (optional) - Filter list by partial match on the marketing code value of the store giving array override.
* project (optional) - Filter list by partial match on the project of the store giving array override.

##### Returns

A dictionary with an items property that contains an array of up to limit store giving array overrides, starting at index offset. Each entry in the array is a separate store giving array override object. If no more store giving array overrides are available, the resulting array will be empty. This request should never return an error.

### Templates

#### Create a template

```
DEFINITION
POST http://apiserver/templates

EXAMPLE REQUEST
$.post("http://localhost:49195/templates", {
    "entityType": "Pledge",
    "templateType": "CHILD LETTER",
    "content": "<Sentence requires=\"DOCCHLOGND,CHLDCHORE>\n\tAt home, {DDCCHLDGNO:subjective:lowercase} is required to {CHLIOCHORE1:lowercase}.\n</Sentence>\n<Sentence requires=\"CHLONMFRST,DOCCHLDGNO,DOCCHLOBD\">\n\tHelp {CHLDNMFRST} celebrate {DDCCHLDGND:possessive:lowercase} {DOCCHLDBD:nextage:ordinal:word:lowercase) birthday.\n</Sentence> "
});

EXAMPLE RESPONSE
{
    "id": "1",
    "entityType": "Pledge",
    "templateType": "CHILD LETTER",
    "content": "<Sentence requires=\"DOCCHLOGND,CHLDCHORE>\n\tAt home, {DDCCHLDGNO:subjective:lowercase} is required to {CHLIOCHORE1:lowercase}.\n</Sentence>\n<Sentence requires=\"CHLONMFRST,DOCCHLDGNO,DOCCHLOBD\">\n\tHelp {CHLDNMFRST} celebrate {DDCCHLDGND:possessive:lowercase} {DOCCHLDBD:nextage:ordinal:word:lowercase) birthday.\n</Sentence> "
}

```

Creates a new template.

##### Arguments

* entityType (required) - Entity Type
* templateType (required) - Template Type
* content (required) - Content

##### Returns

Returns a template object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a template

```
DEFINITION
GET http://apiserver/templates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/templates/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "entityType": "Pledge",
    "templateType": "CHILD LETTER",
    "content": "<Sentence requires=\"DOCCHLOGND,CHLDCHORE>\n\tAt home, {DDCCHLDGNO:subjective:lowercase} is required to {CHLIOCHORE1:lowercase}.\n</Sentence>\n<Sentence requires=\"CHLONMFRST,DOCCHLDGNO,DOCCHLOBD\">\n\tHelp {CHLDNMFRST} celebrate {DDCCHLDGND:possessive:lowercase} {DOCCHLDBD:nextage:ordinal:word:lowercase) birthday.\n</Sentence> "
}

```

Retrieves the details of an existing template. You need only supply the id.

##### Arguments

* id (required) - The id of the template to be retrieved.

#### Update a template

```
DEFINITION
POST http://apiserver/templates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/templates/1", {
    "entityType": "Pledge",
    "templateType": "CHILD LETTER",
    "content": "<Sentence requires=\"DOCCHLOGND,CHLDCHORE>\n\tAt home, {DDCCHLDGNO:subjective:lowercase} is required to {CHLIOCHORE1:lowercase}.\n</Sentence>\n<Sentence requires=\"CHLONMFRST,DOCCHLDGNO,DOCCHLOBD\">\n\tHelp {CHLDNMFRST} celebrate {DDCCHLDGND:possessive:lowercase} {DOCCHLDBD:nextage:ordinal:word:lowercase) birthday.\n</Sentence> "
});

EXAMPLE RESPONSE
{
    "id": "1",
    "entityType": "Pledge",
    "templateType": "CHILD LETTER",
    "content": "<Sentence requires=\"DOCCHLOGND,CHLDCHORE>\n\tAt home, {DDCCHLDGNO:subjective:lowercase} is required to {CHLIOCHORE1:lowercase}.\n</Sentence>\n<Sentence requires=\"CHLONMFRST,DOCCHLDGNO,DOCCHLOBD\">\n\tHelp {CHLDNMFRST} celebrate {DDCCHLDGND:possessive:lowercase} {DOCCHLDBD:nextage:ordinal:word:lowercase) birthday.\n</Sentence> "
}


```

Updates the specified template by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* entityType () - Entity Type
* templateType () - Template Type
* content () - Content

##### Returns

Returns the template object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a template

```
DEFINITION
DELETE http://apiserver/templates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/templates/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a template. It cannot be undone.

##### Arguments

* id (required) - The id of the template to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the template does not exist, this call returns an error.

#### List all templates

```
DEFINITION
GET http://apiserver/templates

EXAMPLE REQUEST
$.get("http://localhost:49195/templates?");

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
            "entityType": "Pledge",
            "templateType": "CHILD LETTER",
            "content": "<Sentence requires=\"DOCCHLOGND,CHLDCHORE>\n\tAt home, {DDCCHLDGNO:subjective:lowercase} is required to {CHLIOCHORE1:lowercase}.\n</Sentence>\n<Sentence requires=\"CHLONMFRST,DOCCHLDGNO,DOCCHLOBD\">\n\tHelp {CHLDNMFRST} celebrate {DDCCHLDGND:possessive:lowercase} {DOCCHLDBD:nextage:ordinal:word:lowercase) birthday.\n</Sentence> "
        },
        {...},
    ]
}

```

Returns a list of all templates.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* entityType () - Entity Type
* templateType () - Template Type
* content () - Content

##### Returns

A dictionary with an items property that contains an array of up to limit templates, starting at index offset. Each entry in the array is a separate template object. If no more templates are available, the resulting array will be empty. This request should never return an error.

#### Generate a template preview

```
DEFINITION
POST http://apiserver/templates/preview?entityCode=:entityCode

EXAMPLE REQUEST
$.post("http://localhost:49195/templates/preview?entityCode=CHILD200", {
    "entityType": "Pledge",
    "content": "<Sentence requires=\"DOCCHLOGND,CHLDCHORE>\n\tAt home, {DDCCHLDGNO:subjective:lowercase} is required to {CHLIOCHORE1:lowercase}.\n</Sentence>\n<Sentence requires=\"CHLONMFRST,DOCCHLDGNO,DOCCHLOBD\">\n\tHelp {CHLDNMFRST} celebrate {DDCCHLDGND:possessive:lowercase} {DOCCHLDBD:nextage:ordinal:word:lowercase) birthday.\n</Sentence> "
});

EXAMPLE RESPONSE
{
    "preview": "At home, John he is required to sew.
    Help John celebrate his fourth birthday"
}

```

Generates a preview for the given entity type, code, and content.

##### Arguments

* entityCode (required) - Entity Code
* entityType (required) - Entity Type
* content (required) - Content

#### Retrieve template completions

```
DEFINITION
GET http://apiserver/template/completions?entityType=:entityType

EXAMPLE REQUEST
$.get("http://localhost:49195/template/completions?entityType=Pledge");

EXAMPLE RESPONSE
[
    {
        "dataType": "NOTE",
        "isGender": false,
        "id": "DDCPLGNT",
        "description": "Pledge Note Type",
        "displaySequence": null,
        "isMultiValue": false,
        "labelDescription": "Pldg Note Type",
        "isUserDefined": false,
        "category": "PLEDGE",
        "isFamilyCode": false,
        "securityRequired": false,
        "requiredForAccountType": null,
        "isActive": true
    },
    {...},
]

```

Returns a list of all template completions.

##### Arguments

* entityType (required) - Entity Type

##### Returns

An array of template completions. Each entry in the array is a separate template completion object.

### Titles

#### Create a title

```
DEFINITION
POST http://apiserver/titles

EXAMPLE REQUEST
$.post("http://localhost:49195/titles", {
    "id": "PASTOR"
});

EXAMPLE RESPONSE
{
    "id": "PASTOR"
}

```

##### Arguments

* id (required) - The title

##### Returns

Returns a title object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a title

```
DEFINITION
GET http://apiserver/titles/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/titles/PASTOR");

EXAMPLE RESPONSE
{
    "id": "PASTOR"
}

```

#### Delete a title

```
DEFINITION
DELETE http://apiserver/titles/:id

EXAMPLE REQUEST
$.delete("http://localhost:49195/titles/PASTOR");

EXAMPLE RESPONSE
204 NO CONTENT

```

#### List all titles

```
DEFINITION
GET http://apiserver/titles

EXAMPLE REQUEST
$.get("http://localhost:49195/titles");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 38
    },
    "items": [
        {
            "id": "Admiral"
        },
        {
            "id": "Bishop"
        },
        {...}
}

```

Returns a list of valid titles.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Returns

A dictionary with an items property that contains an array of up to limit titles, starting at index offset. Each entry in the array is a valid title. This request should never return an error.

### User Telephone Extension

#### Retrieve a user telephone extension

```
DEFINITION
GET http://apiserver/usertelephoneextension

EXAMPLE REQUEST
$.get("http://localhost:49195/usertelephoneextension");

EXAMPLE RESPONSE
{
    "telephoneExtension": "456"
}

```

##### Returns

Returns the telephone extension for the current user session.

#### Update a user telephone extension

```
DEFINITION
POST http://apiserver/usertelephoneextension

EXAMPLE REQUEST
$.post("http://localhost:49195/usertelephoneextension", {
    "telephoneExtension": "489"
});

EXAMPLE RESPONSE
{
    "telephoneExtension": "489"
}

```

##### ARGUMENTS

* telephoneExtension (required) - The user telephone extension for the user of the current session

### Workflow Actions

#### Create a workflow action

```
DEFINITION
POST http://apiserver/workflows/:id/actions

EXAMPLE REQUEST
$.post("http://localhost:49195/workflows/10036/actions", {
    "action":"SETMKATTR",
    "actionData":{
        "attributeType":"DONTRACK",
        "attributeValue":"4"
    },
    "description":"Add Marketing Attribute",
    "sequence":0
});

EXAMPLE RESPONSE
{
    "id": "10057",
    "description": "Add Marketing Attribute",
    "action": "SETMKATTR",
    "actionDescription": null,
    "actionData": {
        "advancedFind": null,
        "action": null,
        "attributeType": "DONTRACK",
        "attributeValue": "4"
    },
    "sequence": 0,
    "notificationType": null,
    "notificationTypeDescription": null
}

```

Creates a new workflow action.

##### Arguments

* action (optional) - The action to perform in the workflow action process.
* actionData (optional) - The action data to use in the workflow action process.
* description (optional) - The description of the workflow action.
* sequence (optional) - If multiple actions exist, the order of processing.

##### Returns

Returns a workflow action object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a workflow action

```
DEFINITION
GET http://apiserver/workflows/:id/actions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/workflows/10036/actions/10057");

EXAMPLE RESPONSE
{
    "id": "10057",
    "description": "Add Marketing Attribute",
    "action": "SETMKATTR",
    "actionDescription": "Set marketing attribute workflow action",
    "actionData": {
        "advancedFind": null,
        "action": null,
        "attributeType": "DONTRACK",
        "attributeValue": "4"
    },
    "sequence": 0,
    "notificationType": null,
    "notificationTypeDescription": null
}

```

Retrieves the details of an existing workflow action. You need only supply the id.

##### Arguments

* id (required) - The id of the workflow action to be retrieved.

#### Update a workflow action

```
DEFINITION
POST http://apiserver/workflows/:id/actions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/workflows/10036/actions/10057", {
    "actionData":{
        "attributeType":"DONTRACK",
        "attributeValue":"5"
    }
});

EXAMPLE RESPONSE
{
    "id": "10057",
    "description": "Add Marketing Attribute",
    "action": "SETMKATTR",
    "actionDescription": "Set marketing attribute workflow action",
    "actionData": {
        "advancedFind": null,
        "action": "set",
        "attributeType": "DONTRACK",
        "attributeValue": "5"
    },
    "sequence": 0,
    "notificationType": null,
    "notificationTypeDescription": null
}


```

Updates the specified workflow action by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* action (optional) - The action to perform in the workflow action process.
* actionData (optional) - The action data to use in the workflow action process.
* description (optional) - The description of the workflow action.
* sequence (optional) - If multiple actions exist, the order of processing.

##### Returns

Returns the workflow action object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a workflow action

```
DEFINITION
DELETE http://apiserver/workflows/:id/actions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/workflows/10036/actions/10057", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a workflow action. It cannot be undone.

##### Arguments

* id (required) - The id of the workflow action to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the workflow action does not exist, this call returns an error.

#### List all workflow actions

```
DEFINITION
GET http://apiserver/workflows/:id/actions

EXAMPLE REQUEST
$.get("http://localhost:49195/workflows/10036/actions?action=SETMKATTR");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10057",
            "description": "Add Marketing Attribute",
            "action": "SETMKATTR",
            "actionDescription": "Set marketing attribute workflow action",
            "actionData": {
                "advancedFind": null,
                "action": null,
                "attributeType": "DONTRACK",
                "attributeValue": "5"
            },
            "sequence": 0,
            "notificationType": null,
            "notificationTypeDescription": null
        },
        {...},
    ]
}

```

Returns a list of all workflow actions.

##### Arguments

* action (optional) - filters results on partial match

##### Returns

A dictionary with an items property that contains an array of up to limit workflow actions, starting at index offset. Each entry in the array is a separate workflow action object. If no more account workflow actions are available, the resulting array will be empty. This request should never return an error.

### Workflow Action Types

This section details specific `action` and `actionData` arguments of the [Workflow Actions](#workflow-actions).

#### Marketing attribute action type

```
EXAMPLE ARGUMENT
{
    "action":"SETMKATTR",
    "actionData":{
        "attributeType":"DONTRACK",
        "attributeValue":"4"
    },
    ...
};

```

##### Arguments

* action (optional) - The action to perform in the workflow action process. (Must be one of the following: `SETMKATTR`, `DELMKATTR`.)
* actionData (optional) - The action data to use in the workflow action process.
  + attributeType (optional) - The account marketing code type to perform the action on in the workflow action process. (Must be a valid and active code type in the `ACCTMKATTR` category.)
  + attributeValue (optional) - The value of the attributeType to perform the action on in the workflow action process. (Must be a valid code value for the attributeType.)

#### Marketing date action type

```
EXAMPLE ARGUMENT
{
    "action":"SETMKATTR",
    "actionData":{
        "dateType":"LSTCONTACT",
        "dateValue":"2016-06-01"
    },
    ...
};

```

##### Arguments

* action (optional) - The action to perform in the workflow action process. (Must be one of the following: `SETMKATTR`, `DELMKATTR`.)
* actionData (optional) - The action data to use in the workflow action process.
  + dateType (optional) - The account marketing date type to perform the action on in the workflow action process. (Must be a valid and active date type in the `ACCTMKATTR` category.)
  + dateValue (optional) - The value of the dateType to perform the action on in the workflow action process. (Must be a valid date value for the dateType.)

#### Marketing note action type

```
EXAMPLE ARGUMENT
{
    "action":"SETMKATTR",
    "actionData":{
        "noteType":"MKTNOTE",
        "noteValue":"He enjoys attending hockey games with his family."
    },
    ...
};

```

##### Arguments

* action (optional) - The action to perform in the workflow action process. (Must be one of the following: `SETMKATTR`, `DELMKATTR`.)
* actionData (optional) - The action data to use in the workflow action process.
  + noteType (optional) - The account marketing note type to perform the action on in the workflow action process. (Must be a valid and active note type in the `ACCTMKATTR` category.)
  + noteValue (optional) - The value of the noteType to perform the action on in the workflow action process.

#### Marketing number action type

```
EXAMPLE ARGUMENT
{
    "action":"SETMKATTR",
    "actionData":{
        "numberType":"LSTGIFTAMT",
        "numberValue":"256"
    },
    ...
};

```

##### Arguments

* action (optional) - The action to perform in the workflow action process. (Must be one of the following: `SETMKATTR`, `DELMKATTR`.)
* actionData (optional) - The action data to use in the workflow action process.
  + numberType (optional) - The account marketing number type to perform the action on in the workflow action process. (Must be a valid and active number type in the `ACCTMKATTR` category.)
  + numberValue (optional) - The value of the numberType to perform the action on in the workflow action process. (Must be a valid number value for the numberType.)