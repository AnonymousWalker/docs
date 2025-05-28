# Security and Setup

### Accessor Environments

#### Create an accessor environment

```
DEFINITION
POST http://apiserver/accessors/:id/environments

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6637/environments", {
    "environmentId": "PROD",
    "roleId": "STAFF"
});

EXAMPLE RESPONSE
{
    "id": "50556",
    "environmentId": "PROD",
    "environmentDescription": "Production Environment",
    "roleId": "STAFF",
    "roleDescription": "Staff",
    "isActive": true,
    "useAsDefault": false
}

```

Creates a new accessor environment.

##### Arguments

* environmentId (required) - The environment / databaseId
* roleId (required) - The role
* isActive (optional; defaults `true`) - Specifies if it is active or not
* useAsDefault (optional; defaults `false`) - Specifies if it should be the default

##### Returns

Returns an accessor environment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accessor environment

```
DEFINITION
GET http://apiserver/accessors/:id/environments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/6637/environments/50556");

EXAMPLE RESPONSE
{
    "id": "50556",
    "environmentId": "PROD",
    "environmentDescription": "Production Environment",
    "roleId": "STAFF",
    "roleDescription": "Staff",
    "isActive": true,
    "useAsDefault": false
}

```

Retrieves the details of an existing accessor environment. You need only supply the id.

##### Arguments

* id (required) - The id of the accessor environment to be retrieved.

#### Update an accessor environment

```
DEFINITION
POST http://apiserver/accessors/:id/environments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6637/environments/50556", {
    "useAsDefault": true
});

EXAMPLE RESPONSE
{
    "id": "50556",
    "environmentId": "PROD",
    "environmentDescription": "Production Environment",
    "roleId": "STAFF",
    "roleDescription": "Staff",
    "isActive": true,
    "useAsDefault": true
}


```

Updates the specified accessor environment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* environmentId (optional) - The environment / databaseId
* roleId (optional) - The role
* isActive (optional) - Specifies if it is active or not
* useAsDefault (optional) - Specifies if it should be the default

##### Returns

Returns the accessor environment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an accessor environment

```
DEFINITION
DELETE http://apiserver/accessors/:id/environments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accessors/6637/environments/50556", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a accessor environment. It cannot be undone.

##### Arguments

* id (required) - The id of the accessor environment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the accessor environment does not exist, this call returns an error.

#### List all accessor environments

```
DEFINITION
GET http://apiserver/accessors/:id/environments

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/:id/environments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "50556",
            "environmentId": "PROD",
            "environmentDescription": "Production Environment",
            "roleId": "STAFF",
            "roleDescription": "Staff",
            "isActive": true,
            "useAsDefault": true
        },
        {...},
    ]
}

```

Returns a list of all accessor environments.

##### Arguments

None

##### Returns

A dictionary with an items property that contains an array of up to limit accessor environments, starting at index offset. Each entry in the array is a separate accessor environment object. If no more accessor environments are available, the resulting array will be empty. This request should never return an error.

### Accessor Environment Account Lookup Restrictions

#### Create an accessor environment account lookup restriction

```
DEFINITION
POST http://apiserver/accessors/:id/environments/:id/accountlookuprestrictions

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6637/environments/50556/accountlookuprestrictions", {
    "type": "ACRESTRICT",
    "valueLow": "A1",
    "valueHigh": "A99"
});

EXAMPLE RESPONSE
{
    "id": "23"
    "type": "ACRESTRICT",
    "valueLow": "A1",
    "valueHigh": "A99"
}

```

Creates a new accessor environment account lookup restriction.

##### Arguments

* type (required) - A code type
* valueLow (required) - A valid code value of the specified `type`
* valueHigh (required) - A valid code value of the specified `type`

##### Returns

Returns an accessor environment account lookup restriction object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accessor environment account lookup restriction

```
DEFINITION
GET http://apiserver/accessors/:id/environments/:id/accountlookuprestrictions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/6637/environments/50556/accountlookuprestrictions/23");

EXAMPLE RESPONSE
{
    "id": "23"
    "type": "ACRESTRICT",
    "valueLow": "A1",
    "valueHigh": "A99"
}

```

Retrieves the details of an existing accessor environment account lookup restriction. You need only supply the id.

##### Arguments

* id (required) - The id of the accessor environment account lookup restriction to be retrieved.

#### Update an accessor environment account lookup restriction

```
DEFINITION
POST http://apiserver/accessors/:id/environments/:id/accountlookuprestrictions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessors/6637/environments/50556/accountlookuprestrictions/23", {
    "valueHigh": "B9"
});

EXAMPLE RESPONSE
{
    "id": "23"
    "type": "ACRESTRICT",
    "valueLow": "A1",
    "valueHigh": "B9"
}


```

Updates the specified accessor environment account lookup restriction by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type - A code type
* valueLow - A valid code value of the specified `type`
* valueHigh - A valid code value of the specified `type`

##### Returns

Returns the accessor environment account lookup restriction object if the update succeeded. Returns an error if update parameters are invalid.

#### List all accessor environment account lookup restrictions

```
DEFINITION
GET http://apiserver/accessors/:id/environments/:id/accountlookuprestrictions

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/6637/environments/50556/accountlookuprestrictions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "23"
            "type": "ACRESTRICT",
            "valueLow": "A1",
            "valueHigh": "B9"
        },
        {...},
    ]
}

```

Returns a list of all accessor environment account lookup restrictions.

##### Arguments

None

##### Returns

A dictionary with an items property that contains an array of up to limit accessor environment account lookup restrictions, starting at index offset. Each entry in the array is a separate accessor environment account lookup restriction object. If no more accessor environment account lookup restrictions are available, the resulting array will be empty. This request should never return an error.

#### Delete an accessor environment account lookup restriction

```
DEFINITION
DELETE http://apiserver/accessors/:id/environments/:id/accountlookuprestrictions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accessors/6637/environments/50556/accountlookuprestrictions/23", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an accessor environment account lookup restriction. It cannot be undone.

##### Arguments

* id (required) - The id of the accessor environment account lookup restriction to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the accessor environment account lookup restriction does not exist, this call returns an error.

### Accessor Override Audit Information

#### Create an accessor override audit information record

```
DEFINITION
POST http://apiserver/accessoroverrideaudits

EXAMPLE REQUEST
$.post("http://localhost:49195/accessoroverrideaudits", {
    "accountNumber": "56135",
    "actionCode": "PCIPALOFF",
    "reasonCode": "DRIVING"
});

EXAMPLE RESPONSE
{
    "id": "13456",
    "accessorId": "45613",
    "accessorName": "John Smith - Internal",
    "accountNumber": "56135",
    "accountName": "Timothy Moore III",
    "actionCode": "PCIPALOFF",
    "actionDescription": "Disable PCI Pal",
    "reasonCode": "DRIVING",
    "reasonDescription": "Constituent is driving",
    "actionDateTime": "2019-01-27T09:45:21 AM",
    "documentNumber": null,
    "shortComment": null,
    "longComment": null
}

```

Creates a new accessor override audit information record. Note that accessorId does not need to be provided and will be taken from the logged-in user.

##### Arguments

* accountNumber (required) - The account number of the account on which the override is occurring; must be a valid account number.
* actionCode (required) - The action code of the accessor override audit; must be a valid accessor override audit information action code (ACOVRAUACT).
* reasonCode (required) - The reason code of the accessor override audit; must be a valid code attribute of type "REASON" on the accessor override audit information action code value.
* documentNumber (optional) - The document number of the transaction on which the override is occurring; must be a valid transaction document number.

##### Returns

Returns an accessor override audit information record object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accessor override audit information record

```
DEFINITION
GET http://apiserver/accessoroverrideaudits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessoroverrideaudits/13456");

EXAMPLE RESPONSE
{
    "id": "13456",
    "accessorId": "45613",
    "accessorName": "John Smith - Internal",
    "accountNumber": "56135",
    "accountName": "Timothy Moore III",
    "actionCode": "PCIPALOFF",
    "actionDescription": "Disable PCI Pal",
    "reasonCode": "DRIVING",
    "reasonDescription": "Constituent is driving",
    "actionDateTime": "2019-01-27T09:45:21 AM",
    "documentNumber": "56134897",
    "shortComment": null,
    "longComment": null
}

```

Retrieves the details of an existing accessor override audit information record. You need only supply the id.

##### Arguments

* id (required) - The id of the accessor override audit information record to be retrieved.

#### Update an accessor override audit information record

```
DEFINITION
POST http://apiserver/accessoroverrideaudits/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accessoroverrideaudits/13456", {
    "shortComment": "A short comment."
});

EXAMPLE RESPONSE
{
    "id": "13456",
    "accessorId": "45613",
    "accessorName": "John Smith - Internal",
    "accountNumber": "56135",
    "accountName": "Timothy Moore III",
    "actionCode": "PCIPALOFF",
    "actionDescription": "Disable PCI Pal",
    "reasonCode": "DRIVING",
    "reasonDescription": "Constituent is driving",
    "actionDateTime": "2019-01-27T09:45:21 AM",
    "documentNumber": "56134897",
    "shortComment": "A short comment.",
    "longComment": null
}


```

Updates the specified accessor override audit information record by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* shortComment (optional) - A short comment on the accessor override audit information record.
* longComment (optional) - A longer comment on the accessor override audit information record.

##### Returns

Returns the accessor override audit information record object if the update succeeded. Returns an error if update parameters are invalid.

#### List all accessor override audit information records

```
DEFINITION
GET http://apiserver/accessoroverrideaudits

EXAMPLE REQUEST
$.get("http://localhost:49195/accessoroverrideaudits");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "13456",
            "accessorId": "45613",
            "accessorName": "John Smith - Internal",
            "accountNumber": "56135",
            "accountName": "Timothy Moore III",
            "actionCode": "PCIPALOFF",
            "actionDescription": "Disable PCI Pal",
            "reasonCode": "DRIVING",
            "reasonDescription": "Constituent is driving",
            "actionDateTime": "2019-01-27T09:45:21 AM",
            "documentNumber": "56134897",
            "shortComment": null,
            "longComment": null
        },
        { ... },
        { ... }
    ]
}

```

Returns a list of all accessor override audit information records.

##### Returns

A dictionary with an items property that contains an array of up to limit accessor override audit information records, starting at index offset. Each entry in the array is a separate accessor override audit information record object. If no more accessor override audit information records are available, the resulting array will be empty. This request should never return an error.

### Activities

#### List all activities

```
DEFINITION
GET http://apiserver/activities

EXAMPLE REQUEST
$.get("http://localhost:49195/activities");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 674
    },
    "items": [
        {
            "id": "AccountCodes",
            "parentId": null,
            "title": "Codes",
            "titleLong": "Account Codes",
            "component": "AccountProcessing",
            "componentTitleShort": "Account Processing",
            "displaySequence": 41,
            "SAW": "AAT21COD",
            "scriptCode": null,
            "instructionCode": null,
            "minimumGridPageSize": 5,
            "defaultGridPageSize": 5
        },
        {...}
    ]
}

```

Returns a list of all the activities.

##### Arguments

* interfaceIdList (optional) - The list of Activity Interface IDs to return Activities for. If null or not provided, all Activities will be returned.

##### Returns

A dictionary with an items property that contains an array of activity objects. Each entry in the array is an activity object. This request should never return an error.

### Activity Configurations

#### Create a activity configuration

```
DEFINITION
POST http://apiserver/activityconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/activityconfigurations", {
    "sawId": "AST10ELK",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "scriptCode": null,
    "instructionCode": null,
    "category": null,
    "interfaceId": null,
    "minimumGridPageSize": 5,
    "defaultGridPageSize": 5
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "detailActivityId": 2001867,
    "sawId": "AST10ELK",
    "sawDescription": "Environment Lookup Activity",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "scriptCode": null,
    "instructionCode": null,
    "category": null,
    "interfaceId": null,
    "minimumGridPageSize": 5,
    "defaultGridPageSize": 5
}

```

Creates a new activity configuration.

##### Arguments

* sawId (required) - The SAW Id associated with this Detail Activity.
* title (required) - The Short Title of the Detail Activity.
* description (required) - The Long Title of the Detail Activity.
* scriptCode () - The Script Code that is associated with this Detail Activity.
* instructionCode () - The Instruction Code that is associated with this Detail Activity.
* category () - The string category to place on this Detail Activity.
* interfaceId () - The Interface Id for this Detail Activity.
* minimumGridPageSize (required) - The activity grid page size to use when in tablet mode.
* defaultGridPageSize (required) - The activity grid page size to use when in desktop mode.

##### Returns

Returns a activity configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a activity configuration

```
DEFINITION
GET http://apiserver/activityconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/activityconfigurations/91507");

EXAMPLE RESPONSE
{
    "id": "91507",
    "detailActivityId": 2001867,
    "sawId": "AST10ELK",
    "sawDescription": "Environment Lookup Activity",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "scriptCode": null,
    "instructionCode": null,
    "category": null,
    "interfaceId": null,
    "minimumGridPageSize": 5,
    "defaultGridPageSize": 5
}

```

Retrieves the details of an existing activity configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the activity configuration to be retrieved.

#### Update a activity configuration

```
DEFINITION
POST http://apiserver/activityconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/activityconfigurations/91507", {
    "sawId": "AST10ELK",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "scriptCode": null,
    "instructionCode": null,
    "category": null,
    "interfaceId": null,
    "minimumGridPageSize": 5,
    "defaultGridPageSize": 5
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "detailActivityId": 2001867,
    "sawId": "AST10ELK",
    "sawDescription": "Environment Lookup Activity",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "scriptCode": null,
    "instructionCode": null,
    "category": null,
    "interfaceId": null,
    "minimumGridPageSize": 5,
    "defaultGridPageSize": 5
}


```

Updates the specified activity configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sawId - The SAW Id associated with this Detail Activity.
* title - The Short Title of the Detail Activity.
* description - The Long Title of the Detail Activity.
* scriptCode - The Script Code that is associated with this Detail Activity.
* instructionCode - The Instruction Code that is associated with this Detail Activity.
* category - The string category to place on this Detail Activity.
* interfaceId - The Interface Id for this Detail Activity.
* minimumGridPageSize - The activity grid page size to use when in tablet mode.
* defaultGridPageSize - The activity grid page size to use when in desktop mode.

##### Returns

Returns the activity configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a activity configuration

```
DEFINITION
DELETE http://apiserver/activityconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/activityconfigurations/91507", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a activity configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the activity configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the activity configuration does not exist, this call returns an error.

#### List all activity configurations

```
DEFINITION
GET http://apiserver/activityconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/activityconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "91507",
            "detailActivityId": 2001867,
            "sawId": "AST10ELK",
            "sawDescription": "Environment Lookup Activity",
            "title": "Environment Lookup",
            "description": "Environment Lookup",
            "scriptCode": null,
            "instructionCode": null,
            "category": null,
            "interfaceId": null,
            "minimumGridPageSize": 5,
            "defaultGridPageSize": 5
        },
        {...},
    ]
}

```

Returns a list of all activity configurations.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* sawId () - The SAW Id associated with this Detail Activity.
* title () - The Short Title of the Detail Activity.
* description () - The Long Title of the Detail Activity.

##### Returns

A dictionary with an items property that contains an array of up to limit activity configurations, starting at index offset. Each entry in the array is a separate activity configuration object. If no more activity configurations are available, the resulting array will be empty. This request should never return an error.

### Accessors

#### Retrieve an accessor

```
DEFINITION
GET http://apiserver/accessors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accessors/1234");

EXAMPLE RESPONSE
{
    "id": "1234",
    "description": null,
    "source": "I",
    "sourceDescription": "Internal User",
    "databaseId": "PROD",
    "databaseDescription": "SE Production",
    "isDefaultDatabase": "True",
    "roleId": "DDCSTAFF",
    "roleDescription": "DonorDirect Staff/Training",
    "emailAddress ": "johndoe@donordirect.com"
}

```

Retrieves the details of an existing accessor. You need only supply the accessor id.

##### Arguments

* id (required) - The id of the accessor to be retrieved.

##### Returns

Returns an accessor object.

### Assignment Accessors

#### Retrieve an assignment accessor

```
DEFINITION
GET http://apiserver/assignmentAccessors/:id/

EXAMPLE REQUEST
$.get("http://localhost:49195/assignmentAccessors/6630/");

EXAMPLE RESPONSE
{
    "id": "6630",
    "description": "Webber Bradley",
    "type": "Internal User",
    "source": "I",
    "databaseId": "PROD",
    "databaseDescription": "SE 7.0 Production",
    "isDefaultDatabase": false,
    "roleId": "DDCSTAFF",
    "roleDescription": "DonorDirect Staff/Training",
    "assignmentType": "VOLUNTEER",
    "restrictViewsBasedOnAssignment": false,
    "functionalCategory": "OCC",
    "isAssigned": true,
    "isPrimary": true
}

```

Retrieves the details of an existing assignment accessor.

##### Arguments

* id (required) - The id of the assignment accessor to retrieve.

##### Returns

Returns an assignment accessor object if a valid id was provided.

#### List all assignment accessors

```
DEFINITION
GET http://apiserver/assignmentAccessors/:databaseId/:id/

EXAMPLE REQUEST
$.get("http://localhost:49195/assignmentAccessors/PROD/6635/");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "6630",
            "description": "Webber Bradley",
            "type": "Internal User",
            "source": "I",
            "databaseId": "PROD",
            "databaseDescription": "SE 7.0 Production",
            "isDefaultDatabase": false,
            "roleId": "DDCSTAFF",
            "roleDescription": "DonorDirect Staff/Training",
            "assignmentType": "VOLUNTEER",
            "restrictViewsBasedOnAssignment": false,
            "functionalCategory": "OCC",
            "isAssigned": true,
            "isPrimary": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all assignment accessors

##### Returns

A dictionary with an items property that contains an array of up to limit assignment accessors, starting at index offset. Each entry in the array is a separate assignment accessor object. If no more assignment accessors are available, the resulting array will be empty. This request should never return an error.

### Assignment Groups

#### Bulk Email Folder Setting Management

##### Add Folder Settings

```
DEFINITION
POST http://apiserver/assignmentgroups/:id/manageemailfoldersettings

EXAMPLE REQUEST
$.post("http://localhost:49195/assignmentgroups/Donor Management/manageemailfoldersettings", {
    "action": "add",
    "folder": "TRACK",
    "processType": "READ",
    "trackingLevel":"CATEGORY",
    "createEmailOnlyAccounts": true
});

EXAMPLE RESPONSE
204 No Content

```

##### Delete Folder Settings

```
DEFINITION
POST http://apiserver/assignmentgroups/:id/manageemailfoldersettings

EXAMPLE REQUEST
$.post("http://localhost:49195/assignmentgroups/Donor Management/manageemailfoldersettings", {
    "action": "delete",
    "folder": "TRACK"
});

EXAMPLE RESPONSE
204 No Content

```

##### Update Folder Settings

```
DEFINITION
POST http://apiserver/assignmentgroups/:id/manageemailfoldersettings

EXAMPLE REQUEST
$.post("http://localhost:49195/assignmentgroups/Donor Management/manageemailfoldersettings", {
    "action": "update",
    "folder": "TRACK",
    "processType": "ALL",
    "trackingLevel":"ASSIGNED",
    "createEmailOnlyAccounts": false
});

EXAMPLE RESPONSE
204 No Content

```

#### Create an assignment group

```
DEFINITION
POST http://apiserver/assignmentgroups

EXAMPLE REQUEST
$.post("http://localhost:49195/assignmentgroups", {
    "name": "Operations",
    "description": "Operations Group",
    "functionalCategory": "CR"
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "name": "Operations",
    "description": "Operations Group",
    "functionalCategory": "CR"
    "isActive": true
}

```

Creates a new assignment group.

##### Arguments

* name (required) - The assignment group name
* description (required) - The assignment group description
* functionalCategory (required) - The group's associated functional category
* isActive (optional) - Is the group active. Defaults to true.

##### Returns

Returns an assignment group object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a assignment group

```
DEFINITION
GET http://apiserver/assignmentgroups/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/assignmentgroups/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "name": "Operations",
    "description": "Operations Group",
    "functionalCategory": "CR"
    "isActive": true
}

```

Retrieves the details of an existing assignment group. You need only supply the id.

##### Arguments

* id (required) - The id of the assignment group to be retrieved.

#### Update an assignment group

```
DEFINITION
POST http://apiserver/assignmentgroups/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/assignmentgroups/3", {
    "name": "Ops"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "name": "Ops",
    "description": "Operations Group",
    "functionalCategory": "CR"
    "isActive": true
}

```

Updates the specified assignment group by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name - The assignment group name
* description - The assignment group description
* functionalCategory - The group's associated functional category
* isActive - Is the group active

##### Returns

Returns the assignment group object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an assignment group

```
DEFINITION
DELETE http://apiserver/assignmentgroups/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/assignmentgroups/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a assignment group. It cannot be undone.

##### Arguments

* id (required) - The id of the assignment group to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the assignment group does not exist, this call returns an error.

#### List all assignment groups

```
DEFINITION
GET http://apiserver/assignmentgroups

EXAMPLE REQUEST
$.get("http://localhost:49195/assignmentgroups?functionalCategory=CR");

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
            "name": "Ops",
            "description": "Operations Group",
            "functionalCategory": "CR"
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all assignment groups.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* name - The assignment group name
* description - The assignment group description
* functionalCategory - The group's associated functional category
* isActive - Is the group active

##### Returns

A dictionary with an items property that contains an array of up to limit assignment groups, starting at index offset. Each entry in the array is a separate assignment group object. If no more assignment groups are available, the resulting array will be empty. This request should never return an error.

### Assignment Group Members

#### Create an assignment group member

```
DEFINITION
POST http://apiserver/assignmentgroups/:groupId/members

EXAMPLE REQUEST
$.post("http://localhost:49195/assignmentgroups/OPERATIONS/members", {
    "accessorId": "6631",
    "isLeader": true,
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "8",
    "groupCode": "OPERATIONS",
    "accessorId": "6631",
    "accessorName": "ddc\\mmeza",
    "isLeader": true,
    "isActive": true
}

```

Creates a new assignment group member.

##### Arguments

* accessorId (required) - The id of the accessor to be added.
* isLeader (optional) - Is this member a group leader. Defaults to false.
* isActive (optional) - Is this member active. Defaults to true.

##### Returns

Returns an assignment group member object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an assignment group member

```
DEFINITION
GET http://apiserver/assignmentGroup/:groupId/members/:memberId

EXAMPLE REQUEST
$.get("http://localhost:49195/assignmentGroup/OPERATIONS/members/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "groupCode": "OPERATIONS",
    "accessorId": "6631",
    "accessorName": "ddc\\mmeza",
    "isLeader": true,
    "isActive": true
}

```

Retrieves the details of an existing assignment group member. You need only supply the id.

##### Arguments

* groupId (required) - The group that the group member is a part of.
* memberId (required) - The id of the assignment group member to be retrieved.

#### Update an assignment group member

```
DEFINITION
POST http://apiserver/assignmentgroups/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/assignmentgroups/:groupId/members/:memberId", {
    isLeader: false
});

EXAMPLE RESPONSE
{
    "id": "8",
    "groupCode": "OPERATIONS",
    "accessorId": "6631",
    "accessorName": "ddc\\mmeza",
    "isLeader": false,
    "isActive": true
}

```

Updates the specified assignment group member by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* accessorId (required) - The id of the accessor to be updated.
* isLeader (optional) - Is this member a group leader.
* isActive (optional) - Is this member active.

##### Returns

Returns the assignment group member object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a assignment group member

```
DEFINITION
DELETE http://apiserver/assignmentgroups/:groupId/members/:memberId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/assignmentgroups/OPERATIONS/members/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an assignment group member. It cannot be undone.

##### Arguments

* id (required) - The id of the assignment group member to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the assignment group member does not exist, this call returns an error.

#### List all assignment group members

```
DEFINITION
GET http://apiserver/assignmentgroups/:groupId/members

EXAMPLE REQUEST
$.get("http://localhost:49195/assignmentgroups/OPERATIONS/members?isActive=true");

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
            "groupCode": "OPERATIONS",
            "accessorId": "6631",
            "accessorName": "ddc\\mmeza",
            "isLeader": false,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all assignment group members.

##### Arguments

* groupCode (optional) - The group to look up members for.
* accessorId (optional) - The id of the accessor to be looked up.
* isLeader (optional) - Filter members by isLeader.
* isActive (optional) - Filter by active members.

##### Returns

A dictionary with an items property that contains an array of up to limit assignment group members, starting at index offset. Each entry in the array is a separate assignment group member object. If no more assignment group members are available, the resulting array will be empty. This request should never return an error.

### Authorized Accounts

#### Create an authorized account

```
DEFINITION
POST http://apiserver/authorizedaccounts

EXAMPLE REQUEST
$.post("http://localhost:49195/authorizedaccounts", {
    "environment": "PROD",
    "account": "1",
    "role": "VOLUNTEER",
    "isActive": true,
    "email": "volunteer@domain.com"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "environment": "PROD",
    "environmentDescription": "Production Environment",
    "account": "1",
    "accountName": "Mr. John Doe",
    "role": "VOLUNTEER",
    "roleDescription": "Volunteer",
    "accessorId": "6631",
    "isActive": true,
    "email": "volunteer@domain.com",
    "twoStepVerificationEnabled": true,
    "lockoutEndDateUtc": "2016-10-20T20:03:55.7697376+00:00",
    "lockoutEnabled": true,
    "accessFailedCount": 0,
    "lastPasswordChangedDateUtc": "0001-01-01T00:00:00+00:00",
    "lastSessionStartDateTime": "0001-01-01T00:00:00"
}

```

Creates a new authorized account.

##### Arguments

* environment (required) - The environment / databaseId
* account (required) - An account number which exists in the specified `environment`
* role (required) - The user role
* isActive (optional; default `true`) - Specifies if the authorized account is active
* email (optional) - The login email address.

##### Returns

Returns an authorized account object if the call succeeded. Returns an error if create parameters are invalid.

#### Authorize authorized accounts

```
DEFINITION
POST http://apiserver/authorizedaccounts/authorizeaccounts

EXAMPLE REQUEST
$.post("http://localhost:49195/authorizedaccounts/authorizeaccounts", {
    "environment": "PROD",
    "segmentNumber": "1",
    "jobNumber": "1",
    "role": "VOLUNTEER",
    "sendEmail": true
});

EXAMPLE RESPONSE
204 No Content

```

Authorizes all accounts with email addresses on a job segment.

##### Arguments

* environment (required) - The environment / databaseId
* segmentNumber (required) - An segment number
* jobNumber (required) - An job number
* role (required) - The user role
* sendEmail (required) - Specifies if the reset password email should be sent

##### Returns

Returns a `204 No Content` response on success.

#### Retrieve an authorized account

```
DEFINITION
GET http://apiserver/authorizedaccounts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/authorizedaccounts/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "environment": "PROD",
    "environmentDescription": "Production Environment",
    "account": "1",
    "accountName": "Mr. John Doe",
    "role": "VOLUNTEER",
    "roleDescription": "Volunteer",
    "accessorId": "6631",
    "isActive": true,
    "email": "volunteer@domain.com",
    "twoStepVerificationEnabled": true,
    "lockoutEndDateUtc": "2016-10-20T20:03:55.7697376+00:00",
    "lockoutEnabled": true,
    "accessFailedCount": 0,
    "lastPasswordChangedDateUtc": "0001-01-01T00:00:00+00:00",
    "lastSessionStartDateTime": "0001-01-01T00:00:00"
}

```

Retrieves the details of an existing authorized account. You need only supply the id.

##### Arguments

* id (required) - The id of the authorized account to be retrieved.

#### Update an authorized account

```
DEFINITION
POST http://apiserver/authorizedaccounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/authorizedaccounts/1", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1",
    "environment": "PROD",
    "environmentDescription": "Production Environment",
    "account": "1",
    "accountName": "Mr. John Doe",
    "role": "VOLUNTEER",
    "roleDescription": "Volunteer",
    "accessorId": "6631",
    "isActive": true,
    "email": "volunteer@domain.com",
    "twoStepVerificationEnabled": true,
    "lockoutEndDateUtc": "2016-10-20T20:03:55.7697376+00:00",
    "lockoutEnabled": true,
    "accessFailedCount": 0,
    "lastPasswordChangedDateUtc": "0001-01-01T00:00:00+00:00",
    "lastSessionStartDateTime": "0001-01-01T00:00:00"
}


```

Updates the specified authorized account by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* environment (optional) - The environment / databaseId
* account (optional) - An account number which exists in the specified `environment`
* role (optional) - The user role
* isActive (optional) - Specifies if the authorized account is active
* email (optional) - The login email address.
* twoStepVerificationEnabled (optional) - Specifies if the authorized account requires Two Step Verification

##### Returns

Returns the authorized account object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an authorized account

```
DEFINITION
DELETE http://apiserver/authorizedaccounts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/authorizedaccounts/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an authorized account. It cannot be undone.

##### Arguments

* id (required) - The id of the authorized account to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the authorized account does not exist, this call returns an error.

#### List all authorized accounts

```
DEFINITION
GET http://authorizedaccounts

EXAMPLE REQUEST
$.get("http://localhost:49195/authorizedaccounts/?environment=PROD");

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
            "environment": "PROD",
            "environmentDescription": "Production Environment",
            "account": "1",
            "accountName": "Mr. John Doe",
            "role": "VOLUNTEER",
            "roleDescription": "Volunteer",
            "accessorId": "6631",
            "isActive": true,
            "email": "volunteer@domain.com",
            "twoStepVerificationEnabled": true,
            "lockoutEndDateUtc": "2016-10-20T20:03:55.7697376+00:00",
            "lockoutEnabled": true,
            "accessFailedCount": 0,
            "lastPasswordChangedDateUtc": "0001-01-01T00:00:00+00:00",
            "lastSessionStartDateTime": "0001-01-01T00:00:00"
        },
        {...},
    ]
}

```

Returns a list of all authorized accounts.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* environment - The environment / databaseId
* account - An account number which exists in the specified `environment`
* isActive - Specifies if the authorized account is active

##### Returns

A dictionary with an items property that contains an array of up to limit authorized accounts, starting at index offset. Each entry in the array is a separate authorized account object. If no more authorized accounts are available, the resulting array will be empty. This request should never return an error.

#### Reset password of an authorized account

```
DEFINITION
GET http://apiserver/authorizedaccounts/:id/resetpassword

EXAMPLE REQUEST
$.get("http://localhost:49195/authorizedaccounts/23/resetpassword");

EXAMPLE RESPONSE
204 No Content

```

Sends a reset password email containing a URL to follow to change the password of the authorized account.

##### Arguments

* id (required) - The id of the authorized account to send a reset email to.

##### Returns

Returns a `204 No Content` response on success. If the authorized account does not exist, this call returns an error.

#### Change password of an authorized account

```
DEFINITION
GET http://apiserver/authorizedaccounts/:id/changepassword

EXAMPLE REQUEST
$.post("http://localhost:49195/authorizedaccounts/23/changepassword", {
    newPassword: "Password"
});

EXAMPLE RESPONSE
204 No Content

```

Changes the password of the authorized account.

##### Arguments

* id (required) - The id of the authorized account.
* newPassword (required) - The new password to change to.

##### Returns

Returns a `204 No Content` response on success. If the authorized account does not exist, this call returns an error.

### Call Pop Calls

#### Create a call pop call

```
DEFINITION
POST http://apiserver/callpopcalls

EXAMPLE REQUEST
$.post("http://localhost:49195/callpopcalls", {
    "telephoneExtension": "463",
    "broadcastAreaCode": "210",
    "broadcastTelephoneNumber": "2102102100",
    "accountAreaCode": "979",
    "accountTelephoneNumber": "3244244233",
    "sourceCode": "SCODE"
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "telephoneExtension": "463",
    "broadcastAreaCode": "210",
    "broadcastTelephoneNumber": "2102102100",
    "accountAreaCode": "979",
    "accountTelephoneNumber": "3244244233",
    "sourceCode": "SCODE"
}

```

Creates a new call pop call configuration.

##### Arguments

* telephoneExtension (required) - The user's internal phone extension for call pop
* broadcastAreaCode () - The area code of the broadcast number.
* broadcastTelephoneNumber () - The number of the broadcast.
* accountAreaCode () - The area code of the account.
* accountTelephoneNumber () - The number for the account.
* sourceCode () - The source code for the call information.

##### Returns

Returns a call pop call object. Returns an error if create parameters are invalid.

#### Retrieve a call pop call

```
DEFINITION
GET http://apiserver/callpopcalls/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/callpopcalls/91507");

EXAMPLE RESPONSE
{
    "id": "91507",
    "telephoneExtension": "463",
    "broadcastAreaCode": "210",
    "broadcastTelephoneNumber": "2102102100",
    "accountAreaCode": "979",
    "accountTelephoneNumber": "3244244233",
    "sourceCode": "SCODE"
}

```

Retrieves the details of an existing call pop call. You need only supply the id.

##### Arguments

* id (required) - The id of the call pop call to be retrieved.

#### Update a call pop call

```
DEFINITION
POST http://apiserver/callpopcalls/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/callpopcalls/91507", {
    "telephoneExtension": "464",
    "broadcastAreaCode": "210",
    "broadcastTelephoneNumber": "2102102100",
    "accountAreaCode": "979",
    "accountTelephoneNumber": "3244244233",
    "sourceCode": "SCODE2"
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "telephoneExtension": "464",
    "broadcastAreaCode": "210",
    "broadcastTelephoneNumber": "2102102100",
    "accountAreaCode": "979",
    "accountTelephoneNumber": "3244244233",
    "sourceCode": "SCODE2"
}


```

Updates the specified call pop call by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* telephoneExtension () - The user's internal phone extension for call pop
* broadcastAreaCode () - The area code of the broadcast number.
* broadcastTelephoneNumber () - The number of the broadcast.
* accountAreaCode () - The area code of the account.
* accountTelephoneNumber () - The number for the account.
* sourceCode () - The source code for the call information.

##### Returns

Returns the call pop call object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a call pop call

```
DEFINITION
DELETE http://apiserver/callpopcalls/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/callpopcalls/91507", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a call pop call. It cannot be undone.

##### Arguments

* id (required) - The id of the component configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the call pop call does not exist, this call returns an error.

#### List all call pop calls

```
DEFINITION
GET http://apiserver/callpopcalls

EXAMPLE REQUEST
$.get("http://localhost:49195/callpopcalls?sourceCode=SCODE2");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "91507",
            "telephoneExtension": "464",
            "broadcastAreaCode": "210",
            "broadcastTelephoneNumber": "2102102100",
            "accountAreaCode": "979",
            "accountTelephoneNumber": "3244244233",
            "sourceCode": "SCODE2"
        },
        {...},
    ]
}

```

Returns a list of all call pop calls.

##### Arguments

* telephoneExtension () - The user's internal phone extension for call pop
* broadcastAreaCode () - The area code of the broadcast number.
* broadcastTelephoneNumber () - The number of the broadcast.
* accountAreaCode () - The area code of the account.
* accountTelephoneNumber () - The number for the account.
* sourceCode () - The source code for the call information.

##### Returns

A dictionary with an items property that contains an array of up to limit call pop calls, starting at index offset. Each entry in the array is a separate call pop call object. If no more call pop calls are available, the resulting array will be empty. This request should never return an error.

### Call Pop Users

#### Create a call pop user

```
DEFINITION
POST http://apiserver/callpopusers

EXAMPLE REQUEST
$.post("http://localhost:49195/callpopusers", {
    "userId": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "telephoneExtension": "463"
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "userId": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "telephoneExtension": "463"
}

```

Creates a new call pop user configuration.

##### Arguments

* userId (required) - The user id.
* telephoneExtension (required) - The user's internal phone extension for call pop

##### Returns

Returns a call pop user object. Returns an error if create parameters are invalid.

#### Retrieve a call pop user

```
DEFINITION
GET http://apiserver/callpopusers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/callpopusers/91507");

EXAMPLE RESPONSE
{
    "id": "91507",
    "userId": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "telephoneExtension": "463"
}

```

Retrieves the details of an existing call pop user. You need only supply the id.

##### Arguments

* id (required) - The id of the call pop user to be retrieved.

#### Update a call pop user

```
DEFINITION
POST http://apiserver/callpopusers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/callpopusers/91507", {
    "userId": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "telephoneExtension": "464"
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "userId": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "telephoneExtension": "464"
}


```

Updates the specified call pop user by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* userId () - The user id.
* telephoneExtension () - The user's internal phone extension for call pop

##### Returns

Returns the call pop user object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a call pop user

```
DEFINITION
DELETE http://apiserver/callpopusers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/callpopusers/91507", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a call pop user. It cannot be undone.

##### Arguments

* id (required) - The id of the component configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the call pop user does not exist, this call returns an error.

#### List all call pop users

```
DEFINITION
GET http://apiserver/callpopusers

EXAMPLE REQUEST
$.get("http://localhost:49195/callpopusers?userId=01199F6A-F669-4AFB-BE78-87E4E8C1E4FF");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "91507",
            "userId": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
            "telephoneExtension": "464"
        },
        {...},
    ]
}

```

Returns a list of all call pop users.

##### Arguments

* userId () - The user id.
* telephoneExtension () - The user's internal phone extension for call pop

##### Returns

A dictionary with an items property that contains an array of up to limit call pop users, starting at index offset. Each entry in the array is a separate call pop user object. If no more call pop users are available, the resulting array will be empty. This request should never return an error.

### Components

#### List all components

```
DEFINITION
GET http://apiserver/components

EXAMPLE REQUEST
$.get("http://localhost:49195/components");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 57
    },
    "items": [
        {
            "id": "AccountProcessing",
            "title": "Account Processing",
            "module": "AccountsAndTransactions",
            "isDefault": true,
            "isGroup": false,
            "groupComponentId", null,
            "displaySequence": 0,
            "SAW": "CAT10ACC",
            "minimumGridPageSize": null,
            "defaultGridPageSize": null
        },
        {...}
    ]
}

```

Returns a list of all the components.

##### Returns

A dictionary with an items property that contains an array of component objects. Each entry in the array is a component object. This request should never return an error.

### Component Configurations

#### Create a component configuration

```
DEFINITION
POST http://apiserver/componentconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/componentconfigurations", {
    "sawId": "AST10ELK",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "isGroup": false,
    "interfaceId": null
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "componentId": 2001867,
    "sawId": "AST10ELK",
    "sawDescription": "Environment Lookup Component",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "isGroup": false,
    "interfaceId": null,
    "minimumGridPageSize": null,
    "defaultGridPageSize": null
}

```

Creates a new component configuration.

##### Arguments

* sawId (required) - The SAW Id associated with this Component.
* title (required) - The Short Title of the Component.
* description () - The Long Title of the Component.
* isGroup (required) - The group indicator.
* interfaceId () - The Interface Id for this Component.
* minimumGridPageSize () - The minimum grid page size for the component search results.
* defaultGridPageSize () - The default grid page size for the component search results.

##### Returns

Returns a component configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a component configuration

```
DEFINITION
GET http://apiserver/componentconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/componentconfigurations/91507");

EXAMPLE RESPONSE
{
    "id": "91507",
    "componentId": 2001867,
    "sawId": "AST10ELK",
    "sawDescription": "Environment Lookup Component",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "isGroup": false,
    "interfaceId": null,
    "minimumGridPageSize": null,
    "defaultGridPageSize": null
}

```

Retrieves the details of an existing component configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the component configuration to be retrieved.

#### Update a component configuration

```
DEFINITION
POST http://apiserver/componentconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/componentconfigurations/91507", {
    "sawId": "AST10ELK",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "isGroup": false,
    "interfaceId": null
});

EXAMPLE RESPONSE
{
    "id": "91507",
    "componentId": 2001867,
    "sawId": "AST10ELK",
    "sawDescription": "Environment Lookup Component",
    "title": "Environment Lookup",
    "description": "Environment Lookup",
    "isGroup": false,
    "interfaceId": null,
    "minimumGridPageSize": null,
    "defaultGridPageSize": null
}


```

Updates the specified component configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sawId () - The SAW Id associated with this Component.
* title () - The Short Title of the Component.
* description () - The Long Title of the Component.
* isGroup () - The group indicator.
* interfaceId () - The Interface Id for this Component.
* minimumGridPageSize () - The minimum grid page size for the component search results.
* defaultGridPageSize () - The default grid page size for the component search results.

##### Returns

Returns the component configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a component configuration

```
DEFINITION
DELETE http://apiserver/componentconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/componentconfigurations/91507", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a component configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the component configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the component configuration does not exist, this call returns an error.

#### List all component configurations

```
DEFINITION
GET http://apiserver/componentconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/componentconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "91507",
            "componentId": 2001867,
            "sawId": "AST10ELK",
            "sawDescription": "Environment Lookup Component",
            "title": "Environment Lookup",
            "description": "Environment Lookup",
            "isGroup": false,
            "interfaceId": null,
            "minimumGridPageSize": null,
            "defaultGridPageSize": null
        },
        {...},
    ]
}

```

Returns a list of all component configurations.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* sawId () - The SAW Id associated with this Component.
* title () - The Short Title of the Component.
* description () - The Long Title of the Component.

##### Returns

A dictionary with an items property that contains an array of up to limit component configurations, starting at index offset. Each entry in the array is a separate component configuration object. If no more component configurations are available, the resulting array will be empty. This request should never return an error.

### Component Configuration Activity Configurations

#### Create a component configuration activity configuration

```
DEFINITION
POST http://apiserver/componentconfigurations/:id/activityconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/componentconfigurations/22/activityconfigurations", {
    "activityId": 2001112,
    "description": "Account Alerts",
    "sequence": 0,
    "interfaceId": null
});

EXAMPLE RESPONSE
{
    "id": "21299",
    "componentId": 22,
    "activityId": 2001112,
    "activityIdDescription": "Account Alerts",
    "description": "Account Alerts",
    "sequence": 0,
    "interfaceId": null,
    "activityInterfaceId": "AccountAlerts"
}

```

Creates a new component configuration activity configuration.

##### Arguments

* activityId (required) - The activity id associated with this component configuration
* description () - A description for this entity
* sequence (required) - The sequnce number of this activity configuration.
* interfaceId () - The interface id for this activity configuration.

##### Returns

Returns a component configuration activity configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a component configuration activity configuration

```
DEFINITION
GET http://apiserver/componentconfigurations/:id/activityconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/componentconfigurations/22/activityconfigurations/21299");

EXAMPLE RESPONSE
{
    "id": "21299",
    "componentId": 22,
    "activityId": 2001112,
    "activityIdDescription": "Account Alerts",
    "description": "Account Alerts",
    "sequence": 0,
    "interfaceId": null,
    "activityInterfaceId": "AccountAlerts"
}

```

Retrieves the details of an existing component configuration activity configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the component configuration activity configuration to be retrieved.

#### Update a component configuration activity configuration

```
DEFINITION
POST http://apiserver/componentconfigurations/:id/activityconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/componentconfigurations/22/activityconfigurations/21299", {
    "activityId": 2001112,
    "description": "Account Alerts",
    "sequence": 0,
    "interfaceId": null,
    "activityInterfaceId": "AccountAlerts"
});

EXAMPLE RESPONSE
{
    "id": "21299",
    "componentId": 22,
    "activityId": 2001112,
    "activityIdDescription": "Account Alerts",
    "description": "Account Alerts",
    "sequence": 0,
    "interfaceId": null
}


```

Updates the specified component configuration activity configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* activityId () - The detail activity id associated with this component configuration
* description () - A description for this entity
* sequence () - The sequnce number of this activity configuration.
* interfaceId () - The interface id for this activity configuration.

##### Returns

Returns the component configuration activity configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a component configuration activity configuration

```
DEFINITION
DELETE http://apiserver/componentconfigurations/:id/activityconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/componentconfigurations/22/activityconfigurations/21299", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a component configuration activity configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the component configuration activity configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the component configuration activity configuration does not exist, this call returns an error.

#### List all component configuration activity configurations

```
DEFINITION
GET http://apiserver/componentconfigurations/:id/activityconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/componentconfigurations/22/activityconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "21299",
            "componentId": 22,
            "activityId": 2001112,
            "activityIdDescription": "Account Alerts",
            "description": "Account Alerts",
            "sequence": 0,
            "interfaceId": null,
            "activityInterfaceId": "AccountAlerts"
        },
        {...},
    ]
}

```

Returns a list of all component configuration activity configurations.

##### Arguments

* componentConfigurationId (required) - The id of the component configuration to retreive activities from.

##### Returns

A dictionary with an items property that contains an array of up to limit component configuration activity configurations, starting at index offset. Each entry in the array is a separate component configuration activity configuration object. If no more component configuration activity configurations are available, the resulting array will be empty. This request should never return an error.

### Data Security Tables

#### Create a data security table

```
DEFINITION
POST http://apiserver/datasecuritytables

EXAMPLE REQUEST
$.post("http://localhost:49195/datasecuritytables", {
    "databaseId": "DEV",
    "tableId": "A01C"
});

EXAMPLE RESPONSE
{
    "id": "10016",
    "databaseId": "DEV",
    "databaseDescription": "StudioEnterprise DEV",
    "tableId": "A01C"
}

```

Creates a new data security table.

##### Arguments

* databaseId (required) - The id of the database environment.
* tableId (required) - The id of the table.

##### Returns

Returns a data security table object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a data security table

```
DEFINITION
GET http://apiserver/datasecuritytables/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/datasecuritytables/10016");

EXAMPLE RESPONSE
{
    "id": "10016",
    "databaseId": "DEV",
    "databaseDescription": "StudioEnterprise DEV",
    "tableId": "A01C"
}

```

Retrieves the details of an existing data security table. You need only supply the id.

##### Arguments

* id (required) - The id of the data security table to be retrieved.

#### Update a data security table

```
DEFINITION
POST http://apiserver/datasecuritytable/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/datasecuritytable/10016", {
    "databaseId": "DEV",
    "databaseDescription": "StudioEnterprise DEV",
});

EXAMPLE RESPONSE
{
    "id": "10016",
    "databaseId": "DEV",
    "databaseDescription": "StudioEnterprise DEV",
    "tableId": "A01C"
}


```

Updates the specified data security table by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* databaseId () - The id of the database environment.
* tableId () - The id of the table.

##### Returns

Returns the data security table object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a data security table

```
DEFINITION
DELETE http://apiserver/datasecuritytables/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/datasecuritytables/10016", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a data security table. It cannot be undone.

##### Arguments

* id (required) - The id of the data security table to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the data security table does not exist, this call returns an error.

#### List all data security tables

```
DEFINITION
GET http://apiserver/datasecuritytables

EXAMPLE REQUEST
$.get("http://localhost:49195/datasecuritytables?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10016",
            "databaseId": "DEV",
            "databaseDescription": "StudioEnterprise DEV",
            "tableId": "A01C"
        },
        {...},
    ]
}

```

Returns a list of all data security tables.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* databaseId () - The id of the database environment.
* tableId () - The id of the table.

##### Returns

A dictionary with an items property that contains an array of up to limit data security tables, starting at index offset. Each entry in the array is a separate data security table object. If no more data security tables are available, the resulting array will be empty. This request should never return an error.

### Data Security Table Columns

#### Create a data security table column

```
DEFINITION
POST http://apiserver/datasecuritytables/:id/columns

EXAMPLE REQUEST
$.post("http://localhost:49195/datasecuritytables/10019/columns", {
    "columnName": "DataSource"
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "parentRecordId": "10019",
    "columnName": "DataSource"
}

```

Creates a new data security table column.

##### Arguments

* columnName (required) - The column name in the table.

##### Returns

Returns a data security table column object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a data security table column

```
DEFINITION
GET http://apiserver/datasecuritytables/:id/columns/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/datasecuritytables/10019/columns/10033");

EXAMPLE RESPONSE
{
    "id": "10033",
    "parentRecordId": "10019",
    "columnName": "DataSource"
}

```

Retrieves the details of an existing data security table column. You need only supply the id.

##### Arguments

* id (required) - The id of the data security table column to be retrieved.

#### Update a data security table column

```
DEFINITION
POST http://apiserver/datasecuritytables/:id/columns/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/datasecuritytables/10019/columns/10033", {
    "columnName": "DataSource"
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "parentRecordId": "10019",
    "columnName": "DataSource"
}


```

Updates the specified data security table column by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* columnName () - The name of the column in the table

##### Returns

Returns the data security table column object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a data security table column

```
DEFINITION
DELETE http://apiserver/datasecuritytables/:id/columns/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/datasecuritytables/10019/columns/10033", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a data security table column. It cannot be undone.

##### Arguments

* id (required) - The id of the data security table column to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the data security table column does not exist, this call returns an error.

#### List all data security table columns

```
DEFINITION
GET http://apiserver/datasecuritytables/:id/columns

EXAMPLE REQUEST
$.get("http://localhost:49195/datasecuritytables/10019/columns?");

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
            "parentRecordId": "10019",
            "columnName": "DataSource"
        },
        {...},
    ]
}

```

Returns a list of all data security table columns.

##### Arguments

* columnName () - The name of the column in the table

##### Returns

A dictionary with an items property that contains an array of up to limit data security table columns, starting at index offset. Each entry in the array is a separate data security table column object. If no more data security table columns are available, the resulting array will be empty. This request should never return an error.

### Data Security Table Column Values

#### Create a data security table column value

```
DEFINITION
POST http://apiserver/datasecuritytables/:id/columns/:id/values

EXAMPLE REQUEST
$.post("http://localhost:49195/datasecuritytables/10019/columns/10033/values", {
    "valueHigh": "312",
    "valueLow": "1123",
    "sawId": "A0000001"
});

EXAMPLE RESPONSE
{
    "id": "31",
    "parentRecordId": "10033",
    "valueHigh": "312",
    "valueLow": "1123",
    "sawId": "A0000001"
}

```

Creates a new data security table column value.

##### Arguments

* valueHigh (required) - The upper limit of values
* valueLow (required) - The lower limit of values
* sawId (required) - The authorized SAW id.

##### Returns

Returns a data security table column value object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a data security table column value

```
DEFINITION
GET http://apiserver/datasecuritytables/:id/columns/:id/value/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/datasecuritytables/10019/columns/10033/value/31");

EXAMPLE RESPONSE
{
    "id": "31",
    "parentRecordId": "10033",
    "valueHigh": "312",
    "valueLow": "1123",
    "sawId": "A0000001"
}

```

Retrieves the details of an existing data security table column value. You need only supply the id.

##### Arguments

* id (required) - The id of the data security table column value to be retrieved.

#### Update a data security table column value

```
DEFINITION
POST http://apiserver/datasecuritytables/:id/columns/:id/vaules/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/datasecuritytables/10019/columns/10033/vaules/31", {
    "valueHigh": "312",
    "valueLow": "1123",
    "sawId": "A0000001"
});

EXAMPLE RESPONSE
{
    "id": "31",
    "parentRecordId": "10033",
    "valueHigh": "312",
    "valueLow": "1123",
    "sawId": "A0000001"
}


```

Updates the specified data security table column value by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* valueHigh () - The upper limit of values
* valueLow () - The lower limit of values
* sawId () - The authorized SAW id.

##### Returns

Returns the data security table column value object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a data security table column value

```
DEFINITION
DELETE http://apiserver/datasecuritytables/:id/columns/:id/values/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/datasecuritytables/10019/columns/10033/values/31", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a data security table column value. It cannot be undone.

##### Arguments

* id (required) - The id of the data security table column value to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the data security table column value does not exist, this call returns an error.

#### List all data security table column values

```
DEFINITION
GET http://apiserver/datasecuritytables/:id/columns/:id/values

EXAMPLE REQUEST
$.get("http://localhost:49195/datasecuritytables/10019/columns/10013/values?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "31",
            "parentRecordId": "10033",
            "valueHigh": "312",
            "valueLow": "1123",
            "sawId": "A0000001"
        },
        {...},
    ]
}

```

Returns a list of all data security table column values.

##### Arguments

* valueHigh () - The upper limit of values
* valueLow () - The lower limit of values
* sawId () - The authorized SAW id.

##### Returns

A dictionary with an items property that contains an array of up to limit data security table column values, starting at index offset. Each entry in the array is a separate data security table column value object. If no more data security table column values are available, the resulting array will be empty. This request should never return an error.

### Environments

#### List all environments

```
DEFINITION
GET http://apiserver/environments

EXAMPLE REQUEST
$.get("http://localhost:49195/environments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 2
    },
    "items": [
        {
            "id": "USPROD",
            "description": "Dev local Environment",
            "isDefault": false
        },
        {...}
    ]
}

```

Returns a list of environments available to the current user.

##### Returns

A dictionary with an items property that contains an array of environment objects. Each entry in the array is an environment object. If the current user does not have any available environments, the items array will be empty. This request should never return an error.

### Environment Configurations

#### Create an environment configuration

```
DEFINITION
POST http://apiserver/environmentconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations", {
    "database": "6_0_1_GfP",
    "description": "StudioEnterprise 6.0.1 w/ GP",
    "connectionString": "Data Source=DB_SERVER_NAME;Initial Catalog=DB_NAME;Integrated Security=True;",
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "64",
    "database": "6_0_1_GfP",
    "description": "StudioEnterprise 6.0.1 w/ GP",
    "connectionString": "Data Source=DB_SERVER_NAME;Initial Catalog=DB_NAME;Integrated Security=True;",
    "activeComponentColor": null,
    "activeFontColor": null,
    "inactiveComponentColor": null,
    "inactiveFontColor": null,
    "isActive": false
}

```

Creates a new environment configuration.

##### Arguments

* database (required) - Database Id
* description (required) - Description
* connectionString () - Connection String
* activeComponentColor () - The background color of the active component in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in a supported format: 000, #000, 000000, #000000
* activeFontColor () - The font color of the active component in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in the a supported format: 000, #000, 000000, #000000
* inactiveComponentColor () - The background color of all inactive components in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in a supported format: 000, #000, 000000, #000000
* inactiveFontColor () - The font color of all inactive components in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in a supported format: 000, #000, 000000, #000000
* isActive (required) - Active Indicator

##### Returns

Returns an environment configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an environment configuration

```
DEFINITION
GET http://apiserver/environmentconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations/64");

EXAMPLE RESPONSE
{
    "id": "64",
    "database": "6_0_1_GfP",
    "description": "StudioEnterprise 6.0.1 w/ GP",
    "connectionString": "Data Source=DB_SERVER_NAME;Initial Catalog=DB_NAME;Integrated Security=True;",
    "activeComponentColor": null,
    "activeFontColor": null,
    "inactiveComponentColor": null,
    "inactiveFontColor": null,
    "isActive": false
}

```

Retrieves the details of an existing environment configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the environment configuration to be retrieved.

#### Update an environment configuration

```
DEFINITION
POST http://apiserver/environmentconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations/64", {
    "database": "6_0_1_GfP",
    "description": "StudioEnterprise 6.0.1 w/ GP",
    "connectionString": "Data Source=DB_SERVER_NAME;Initial Catalog=DB_NAME;Integrated Security=True;",
    "activeComponentColor": "#990000",
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "64",
    "database": "6_0_1_GfP",
    "description": "StudioEnterprise 6.0.1 w/ GP",
    "connectionString": "Data Source=DB_SERVER_NAME;Initial Catalog=DB_NAME;Integrated Security=True;",
    "activeComponentColor": "#990000",
    "activeFontColor": null,
    "inactiveComponentColor": null,
    "inactiveFontColor": null,
    "isActive": false
}


```

Updates the specified environment configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* database () - Database Id
* description () - Description
* connectionString () - Connection String
* activeComponentColor () - The background color of the active component in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in a supported format: 000, #000, 000000, #000000
* activeFontColor () - The font color of the active component in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in the a supported format: 000, #000, 000000, #000000
* inactiveComponentColor () - The background color of all inactive components in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in a supported format: 000, #000, 000000, #000000
* inactiveFontColor () - The font color of all inactive components in the StudioEnterprise Component menu for this environment. The value must be a valid 3 or 6 digit hexadecimal color value in a supported format: 000, #000, 000000, #000000
* isActive () - Active Indicator

##### Returns

Returns the environment configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an environment configuration

```
DEFINITION
DELETE http://apiserver/environmentconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/environmentconfigurations/64", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an environment configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the environment configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the environment configuration does not exist, this call returns an error.

#### List all environment configurations

```
DEFINITION
GET http://apiserver/environmentconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "64",
            "database": "6_0_1_GfP",
            "description": "StudioEnterprise 6.0.1 w/ GP",
            "connectionString": "Data Source=DB_SERVER_NAME;Initial Catalog=DB_NAME;Integrated Security=True;",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all environment configurations.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* database () - Database Id
* description () - Description
* isActive () - Active Indicator

##### Returns

A dictionary with an items property that contains an array of up to limit environment configurations, starting at index offset. Each entry in the array is a separate environment configuration object. If no more environment configurations are available, the resulting array will be empty. This request should never return an error.

### Environment Configuration Endpoints

#### Create an environment configuration endpoint

```
DEFINITION
POST http://apiserver/environmentconfigurations/:id/endpoints

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations/60/endpoints", {
    "service": "AT",
    "address": "http://DEVSESOAPP:8081/Api/AccountApiService",
    "type": "External",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "5004",
    "service": "AT",
    "address": "http://DEVSESOAPP:8081/Api/AccountApiService",
    "type": "External",
    "isActive": true
}

```

Creates a new environment configuration endpoint.

##### Arguments

* service (required) - Service Id
* address (required) - Web Address of the Service
* type (required) - Internal or External Service Type
* isActive (required) - Active Indicator

##### Returns

Returns an environment configuration endpoint object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an environment configuration endpoint

```
DEFINITION
GET http://apiserver/environmentconfigurations/:id/endpoints/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations/60/endpoints/5004");

EXAMPLE RESPONSE
{
    "id": "5004",
    "service": "AT",
    "address": "http://DEVSESOAPP:8081/Api/AccountApiService",
    "type": "External",
    "isActive": true
}

```

Retrieves the details of an existing environment configuration endpoint. You need only supply the id.

##### Arguments

* id (required) - The id of the environment configuration endpoint to be retrieved.

#### Update an environment configuration endpoint

```
DEFINITION
POST http://apiserver/environmentconfigurations/:id/endpoints/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations/60/endpoints/5004", {
    "service": "AT",
    "address": "http://DEVSESOAPP:8081/Api/AccountApiService",
    "type": "External",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "5004",
    "service": "AT",
    "address": "http://DEVSESOAPP:8081/Api/AccountApiService",
    "type": "External",
    "isActive": true
}


```

Updates the specified environment configuration endpoint by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* service () - Service Id
* address () - Web Address of the Service
* type () - Internal or External Service Type
* isActive () - Active Indicator

##### Returns

Returns the environment configuration endpoint object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an environment configuration endpoint

```
DEFINITION
DELETE http://apiserver/environmentconfigurations/:id/endpoints/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/environmentconfigurations/60/endpoints/5004", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an environment configuration endpoint. It cannot be undone.

##### Arguments

* id (required) - The id of the environment configuration endpoint to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the environment configuration endpoint does not exist, this call returns an error.

#### List all environment configuration endpoints

```
DEFINITION
GET http://apiserver/environmentconfigurations/:id/endpoints

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations/60/endpoints?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5004",
            "service": "AT",
            "address": "http://DEVSESOAPP:8081/Api/AccountApiService",
            "type": "External",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all environment configuration endpoints.

##### Arguments

* databasId (required) - Database Record Id

##### Returns

A dictionary with an items property that contains an array of up to limit environment configuration endpoints, starting at index offset. Each entry in the array is a separate environment configuration endpoint object. If no more environment configuration endpoints are available, the resulting array will be empty. This request should never return an error.

### Environment Configuration Next Numbers

#### Create an environment configuration next number

```
DEFINITION
POST http://apiserver/environmentconfigurations/:id/nextnumbers

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations/60/nextnumbers", {
    "id": "ACCESSID",
    "number": 777
});

EXAMPLE RESPONSE
{
    "id": "ACCESSID",
    "number": 777
}

```

Creates a new environment configuration next number.

##### Arguments

* id (required) - Next Number Type
* number (required) - Next Number

##### Returns

Returns an environment configuration next number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an environment configuration next number

```
DEFINITION
GET http://apiserver/environmentconfigurations/:id/nextnumbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations/60/nextnumbers/ACCESSID");

EXAMPLE RESPONSE
{
    "id": "ACCESSID",
    "number": 777
}

```

Retrieves the details of an existing environment configuration next number. You need only supply the id.

##### Arguments

* id (required) - The id of the environment configuration next number to be retrieved.

#### Update an environment configuration next number

```
DEFINITION
POST http://apiserver/environmentconfigurations/:id/nextnumbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations/60/nextnumbers/ACCESSID", {
    "number": 777
});

EXAMPLE RESPONSE
{
    "id": "ACCESSID",
    "number": 777
}


```

Updates the specified environment configuration next number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* number () - Next Number

##### Returns

Returns the environment configuration next number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an environment configuration next number

```
DEFINITION
DELETE http://apiserver/environmentconfigurations/:id/nextnumbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/environmentconfigurations/60/nextnumbers/ACCESSID", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an environment configuration next number. It cannot be undone.

##### Arguments

* id (required) - The id of the environment configuration next number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the environment configuration next number does not exist, this call returns an error.

#### List all environment configuration next numbers

```
DEFINITION
GET http://apiserver/environmentconfigurations/:id/nextnumbers

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations/60/nextnumbers?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "ACCESSID",
            "number": 777
        },
        {...},
    ]
}

```

Returns a list of all environment configuration next numbers.

##### Arguments

* database (required) - Database Id

##### Returns

A dictionary with an items property that contains an array of up to limit environment configuration next numbers, starting at index offset. Each entry in the array is a separate environment configuration next number object. If no more environment configuration next numbers are available, the resulting array will be empty. This request should never return an error.

### Environment Field Defaults

#### Create an environment field default

```
DEFINITION
POST http://apiserver/environmentconfigurations/:id/fielddefaults

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations/50/fielddefaults", {
    "fieldName": "phoneType",
    "value": "HOME",
    "description": "Default phone type"
});

EXAMPLE RESPONSE
{
    "id": "21",
    "interfaceIdOverride": null,
    "fieldName": "phoneType",
    "value": "HOME",
    "description": "Default phone type",
    "accessorOverride": null,
    "accessorName": null
}

```

Creates a new environment field default.

##### Arguments

* fieldName (required) - The field name
* value (optional) - The value to use when defaulting the field
* interfaceIdOverride (optional) - Set to `null` if the default should be a global default throughout the application. Otherwise, specify the interfaceId for the screen that the default applies to. When used in cunjunction with the interfaceIdOverride, the default will only apply for the accessor on the given screen.
* description (optional) - A description of the field default.
* accessorOverride (optional) - Set to `null` if the default should be a global default throughout the application. Otherwise, specify the accessor that the default applies to. When used in cunjunction with the interfaceIdOverride, the default will only apply for the accessor on the given screen.

##### Returns

Returns an environment field default object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an environment field default

```
DEFINITION
GET http://apiserver/environmentconfigurations/:id/fielddefaults/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations/60/fielddefaults/21");

EXAMPLE RESPONSE
{
    "id": "21",
    "interfaceIdOverride": null,
    "fieldName": "phoneType",
    "value": "HOME",
    "description": "Default phone type",
    "accessorOverride": null,
    "accessorName": null
}

```

Retrieves the details of an existing environment field default. You need only supply the id.

##### Arguments

* id (required) - The id of the environment field default to be retrieved.

#### Update an environment field default

```
DEFINITION
POST http://apiserver/environmentconfigurations/:id/fielddefaults/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/environmentconfigurations/60/fielddefaults/21", {
    "value": "WORK"
});

EXAMPLE RESPONSE
{
    "id": "21",
    "interfaceIdOverride": null,
    "fieldName": "phoneType",
    "value": "WORK",
    "description": "Default phone type",
    "accessorOverride": null,
    "accessorName": null
}

```

Updates the specified environment field default by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* fieldName - The field name
* value - The value to use when defaulting the field
* interfaceIdOverride - Set to `null` if the default should be a global default throughout the application. Otherwise, specify the interfaceId for the screen that the default applies to. When used in cunjunction with the interfaceIdOverride, the default will only apply for the accessor on the given screen.
* description - A description of the field default.
* accessorOverride - Set to `null` if the default should be a global default throughout the application. Otherwise, specify the accessor that the default applies to. When used in cunjunction with the interfaceIdOverride, the default will only apply for the accessor on the given screen.

##### Returns

Returns the environment field default object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an environment field default

```
DEFINITION
DELETE http://apiserver/environmentconfigurations/:id/fielddefaults/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/environmentconfigurations/60/fielddefaults/21", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an environment field default. It cannot be undone.

##### Arguments

* id (required) - The id of the environment field default to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the environment field default does not exist, this call returns an error.

#### List all environment field defaults

```
DEFINITION
GET http://apiserver/environmentconfigurations/:id/fielddefaults
GET http://apiserver/environments/:id/fielddefaults

EXAMPLE REQUEST
$.get("http://localhost:49195/environmentconfigurations/60/fielddefaults?");
$.get("http://localhost:49195/environments/USPROD/fielddefaults?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "21",
            "interfaceIdOverride": null,
            "fieldName": "phoneType",
            "value": "WORK",
            "description": "Default phone type",
            "accessorOverride": null,
            "accessorName": null
        },
        {...},
    ]
}

```

Returns a list of all environment field defaults.

##### Arguments

* fieldName
* interfaceIdOverride
* description

##### Returns

A dictionary with an items property that contains an array of up to limit environment field defaults, starting at index offset. Each entry in the array is a separate environment field default object. If no more environment field defaults are available, the resulting array will be empty. This request should never return an error.

### Grids

#### List all grids

```
DEFINITION
GET http://apiserver/grids

EXAMPLE REQUEST
$.get("http://localhost:49195/grids");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 100
    },
    "items": [
        {
            "id": "accountCodes",
            "description": "Account Codes",
            "columns": [
                {
                    "field": "type",
                    "title": "Code Type",
                    "sequence": 1,
                    "width": "10em",
                    "isCurrency": false,
                    "sortSequence": null,
                    "sortDirection": null
                },
                {...}
            ]
        },
        {...}
    ]
}

```

##### Returns

A dictionary with an items property that contains an array of grids. Each entry in the array is a separate grid object.

This request should never return an error.

Grid columns can be configured at three levels: default, role and accessor. The role and accessor levels override the default configuration. A request to `GET /grids` with no query parameters will flatten the three-level configuration into a consolidated list of grids and columns for the current user. To manage and configure grid columns and grid column overrides see [Grid Configurations](#grid-configurations).

### Grid Configurations

#### Create a grid configuration

```
DEFINITION
POST http://apiserver/gridconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations", {
    "name": "accountAttachments",
    "description": "Attachments"
});

EXAMPLE RESPONSE
{
    "id": "225283",
    "name": "accountAttachments",
    "description": "Attachments"
}

```

Creates a new grid configuration.

##### Arguments

* name
* description

##### Returns

Returns a grid configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a grid configuration

```
DEFINITION
GET http://apiserver/gridconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations/225283");

EXAMPLE RESPONSE
{
    "id": "225283",
    "name": "accountAttachments",
    "description": "Attachments"
}

```

Retrieves the details of an existing grid configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the grid configuration to be retrieved.

#### Update a grid configuration

```
DEFINITION
POST http://apiserver/gridconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225283", {
    "description": "Account Attachments"
});

EXAMPLE RESPONSE
{
    "id": "225283",
    "name": "accountAttachments",
    "description": "Account Attachments"
}

```

Updates the specified grid configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name
* description

##### Returns

Returns the grid configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a grid configuration

```
DEFINITION
DELETE http://apiserver/gridconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/gridconfigurations/225283", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a grid configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the grid configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the grid configuration does not exist, this call returns an error.

#### List all grid configurations

```
DEFINITION
GET http://apiserver/gridconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "225283",
            "name": "accountAttachments",
            "description": "Account Attachments"
        },
        {...},
    ]
}

```

Returns a list of all grid configurations.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* name - partial match on name
* description - partial match on description

##### Returns

A dictionary with an items property that contains an array of up to limit grid configurations, starting at index offset. Each entry in the array is a separate grid configuration object. If no more grid configurations are available, the resulting array will be empty. This request should never return an error.

### Grid Configuration Columns

#### Create a grid configuration column

```
DEFINITION
POST http://apiserver/gridconfigurations/:id/columns

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/columns", {
    "field": "fullName",
    "title": "Name",
    "sequence": 5,
    "width": "12em",
    "fieldType": "TEXT"
    "sortSequence": null
    "sortDirection": null
});

EXAMPLE RESPONSE
{
    "id": "200560",
    "field": "fullName",
    "title": "Name",
    "sequence": 5,
    "width": "12em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}

```

Creates a new grid configuration column.

##### Arguments

* field (required) - Represents the property on the data model. Most of the time this is the same as the property name on the API resource.
* title (required) - Display label for the grid column header
* sequence (required) - Sequence in relation to other grid columns
* width (required) - Width must be a unit of em's.
* fieldType (required) - Must be a valid value for code type `DDCGDCLTYP`
* sortSequence - Default sort sequence. Must be a number. This field is only supported for Component Grids
* sortDirection - Default sort direction. Must be a char 'A' or 'D'. This field is only supported for Component Grids

##### Returns

Returns a grid configuration column object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a grid configuration column

```
DEFINITION
GET http://apiserver/gridconfigurations/:id/columns/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations/225273/columns/200560");

EXAMPLE RESPONSE
{
    "id": "200560",
    "field": "fullName",
    "title": "Name",
    "sequence": 5,
    "width": "12em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}

```

Retrieves the details of an existing grid configuration column. You need only supply the id.

##### Arguments

* id (required) - The id of the grid configuration column to be retrieved.

#### Update a grid configuration column

```
DEFINITION
POST http://apiserver/gridconfigurations/:id/columns/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/columns/200560", {
    "sequence": 20,
});

EXAMPLE RESPONSE
{
    "id": "200560",
    "field": "fullName",
    "title": "Name",
    "sequence": 20,
    "width": "12em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}


```

Updates the specified grid configuration column by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* field - Represents the property on the data model. Most of the time this is the same as the property name on the API resource.
* title - Display label for the grid column header
* sequence - Sequence in relation to other grid columns
* width - Width must be a unit of em's.
* fieldType - Must be a valid value for code type `DDCGDCLTYP`
* sortSequence - Default sort sequence. Must be a number. This field is only supported for Component Grids
* sortDirection - Default sort direction. Must be a char 'A' or 'D'. This field is only supported for Component Grids

##### Returns

Returns the grid configuration column object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a grid configuration column

```
DEFINITION
DELETE http://apiserver/gridconfigurations/:id/columns/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/gridconfigurations/225273/columns/200560", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a grid configuration column. It cannot be undone.

##### Arguments

* id (required) - The id of the grid configuration column to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the grid configuration column does not exist, this call returns an error.

#### List all grid configuration columns

```
DEFINITION
GET http://apiserver/gridconfigurations/:id/columns

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations/225273/columns");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "200560",
            "field": "fullName",
            "title": "Name",
            "sequence": 20,
            "width": "12em",
            "fieldType": "TEXT",
            "sortSequence": null,
            "sortDirection": null
        },
        {...},
    ]
}

```

Returns a list of all grid configuration columns.

##### Returns

A dictionary with an items property that contains an array of up to limit grid configuration columns, starting at index offset. Each entry in the array is a separate grid configuration column object. If no more grid configuration columns are available, the resulting array will be empty. This request should never return an error.

### Grid Configuration Columns Copy

#### Copy grid configuration columns to overrides

```
DEFINITION
POST http://apiserver/gridconfigurations/:id/copycolumns

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/copycolumns", {
    "role": "DEO"
});

EXAMPLE RESPONSE
204 NO CONTENT


EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/copycolumns", {
    "accessor": "6630"
});

EXAMPLE RESPONSE
204 NO CONTENT

```

Copies grid columns to grid overrides.

##### Arguments

* role (optional) - Copies grid columns to grid overrides by role for the specfied role.
* accessor (optional) - Copies grid columns to grid overrides by accessor for the specfied accessor.

##### Returns

Returns `204 NO CONTENT` if successful. Returns an error if parameters are invalid or if there are already existing overrides that conflict with the columns being copied.

### Grid Configuration Overrides By Accessor

#### Create a grid configuration override by accessor

```
DEFINITION
POST http://apiserver/gridconfigurations/:id/overridesbyaccessor

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/overridesbyaccessor", {
    "accessor": "6636",
    "accessorName": "ddc\\jdoe",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "8em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
});

EXAMPLE RESPONSE
{
    "id": "201"
    "accessor": "6636",
    "accessorName": "ddc\\jdoe",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "8em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}

```

Creates a new grid configuration override by accessor.

##### Arguments

* accessor (required) - Accessor for which to override the grid column.
* field (required) - Represents the property on the data model. Most of the time this is the same as the property name on the API resource.
* title (required) - Display label for the grid column header
* sequence (required) - Sequence in relation to other grid columns
* width (required) - Width must be a unit of em's.
* fieldType (required) - Must be a valid value for code type `DDCGDCLTYP`
* sortSequence - Default sort sequence. Must be a number. This field is only supported for Component Grids
* sortDirection - Default sort direction. Must be a char 'A' or 'D'. This field is only supported for Component Grids

##### Returns

Returns a grid configuration override by accessor object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a grid configuration override by accessor

```
DEFINITION
GET http://apiserver/gridconfigurations/:id/overridesbyaccessor/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations/225273/overridesbyaccessor/201");

EXAMPLE RESPONSE
{
    "id": "201"
    "accessor": "6636",
    "accessorName": "ddc\\jdoe",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "8em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}

```

Retrieves the details of an existing grid configuration override by accessor. You need only supply the id.

##### Arguments

* id (required) - The id of the grid configuration override by accessor to be retrieved.

#### Update a grid configuration override by accessor

```
DEFINITION
POST http://apiserver/gridconfigurations/:id/overridesbyaccessor/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/overridesbyaccessor/201", {
    "width": "10em"
});

EXAMPLE RESPONSE
{
    "id": "201"
    "accessor": "6636",
    "accessorName": "ddc\\jdoe",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "10em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}


```

Updates the specified grid configuration override by accessor by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* accessor - Accessor for which to override the grid column.
* field - Represents the property on the data model. Most of the time this is the same as the property name on the API resource.
* title - Display label for the grid column header
* sequence - Sequence in relation to other grid columns
* width - Width must be a unit of em's.
* fieldType - Must be a valid value for code type `DDCGDCLTYP`
* sortSequence - Default sort sequence. Must be a number. This field is only supported for Component Grids
* sortDirection - Default sort direction. Must be a char 'A' or 'D'. This field is only supported for Component Grids

##### Returns

Returns the grid configuration override by accessor object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a grid configuration override by accessor

```
DEFINITION
DELETE http://apiserver/gridconfigurations/:id/overridesbyaccessor/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/gridconfigurations/225273/overridesbyaccessor/201", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a grid configuration override by accessor. It cannot be undone.

##### Arguments

* id (required) - The id of the grid configuration override by accessor to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the grid configuration override by accessor does not exist, this call returns an error.

#### List all grid configuration overrides by accessor

```
DEFINITION
GET http://apiserver/gridconfigurations/:id/overridesbyaccessor

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations/225273/overridesbyaccessor");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "201"
            "accessor": "6636",
            "accessorName": "ddc\\jdoe",
            "field": "firstName",
            "title": "First Name",
            "sequence": 3,
            "width": "10em",
            "fieldType": "TEXT",
            "sortSequence": null,
            "sortDirection": null
        },
        {...},
    ]
}

```

Returns a list of all grid configuration overrides by accessor.

##### Returns

A dictionary with an items property that contains an array of up to limit grid configuration overrides by accessor, starting at index offset. Each entry in the array is a separate grid configuration override by accessor object. If no more grid configuration overrides by accessor are available, the resulting array will be empty. This request should never return an error.

### Grid Configuration Overrides By Role

#### Create a grid configuration override by role

```
DEFINITION
POST http://apiserver/gridconfigurations/:id/overridesbyrole

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/overridesbyrole", {
    "role": "DEO",
    "roleDescription": "Data Entry Operator",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "8em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
});

EXAMPLE RESPONSE
{
    "id": "109"
    "role": "DEO",
    "roleDescription": "Data Entry Operator",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "8em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}

```

Creates a new grid configuration override by role.

##### Arguments

* role (required) - Role for which to override the grid column.
* field (required) - Represents the property on the data model. Most of the time this is the same as the property name on the API resource.
* title (required) - Display label for the grid column header
* sequence (required) - Sequence in relation to other grid columns
* width (required) - Width must be a unit of em's.
* fieldType (required) - Must be a valid value for code type `DDCGDCLTYP`
* sortSequence - Default sort sequence. Must be a number. This field is only supported for Component Grids
* sortDirection - Default sort direction. Must be a char 'A' or 'D'. This field is only supported for Component Grids

##### Returns

Returns a grid configuration override by role object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a grid configuration override by role

```
DEFINITION
GET http://apiserver/gridconfigurations/:id/overridesbyrole/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations/225273/overridesbyrole/109");

EXAMPLE RESPONSE
{
    "id": "109"
    "role": "DEO",
    "roleDescription": "Data Entry Operator",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "8em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}

```

Retrieves the details of an existing grid configuration override by role. You need only supply the id.

##### Arguments

* id (required) - The id of the grid configuration override by role to be retrieved.

#### Update a grid configuration override by role

```
DEFINITION
POST http://apiserver/gridconfigurations/:id/overridesbyrole/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/gridconfigurations/225273/overridesbyrole/109", {
    "width": "10em"
});

EXAMPLE RESPONSE
{
    "id": "109"
    "role": "DEO",
    "roleDescription": "Data Entry Operator",
    "field": "firstName",
    "title": "First Name",
    "sequence": 3,
    "width": "10em",
    "fieldType": "TEXT",
    "sortSequence": null,
    "sortDirection": null
}


```

Updates the specified grid configuration override by role by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* role - Role for which to override the grid column. Must be a valid data type `DDCROLEID`.
* field - Represents the property on the data model. Most of the time this is the same as the property name on the API resource.
* title - Display label for the grid column header
* sequence - Sequence in relation to other grid columns
* width - Width must be a unit of em's.
* fieldType - Must be a valid value for code type `DDCGDCLTYP`
* sortSequence - Default sort sequence. Must be a number. This field is only supported for Component Grids
* sortDirection - Default sort direction. Must be a char 'A' or 'D'. This field is only supported for Component Grids

##### Returns

Returns the grid configuration override by role object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a grid configuration override by role

```
DEFINITION
DELETE http://apiserver/gridconfigurations/:id/overridesbyrole/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/gridconfigurations/225273/overridesbyrole/109", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a grid configuration override by role. It cannot be undone.

##### Arguments

* id (required) - The id of the grid configuration override by role to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the grid configuration override by role does not exist, this call returns an error.

#### List all grid configuration overrides by role

```
DEFINITION
GET http://apiserver/gridconfigurations/:id/overridesbyrole

EXAMPLE REQUEST
$.get("http://localhost:49195/gridconfigurations/225273/overridesbyrole");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "109"
            "role": "DEO",
            "roleDescription": "Data Entry Operator",
            "field": "firstName",
            "title": "First Name",
            "sequence": 3,
            "width": "10em",
            "fieldType": "TEXT",
            "sortSequence": null,
            "sortDirection": null
        },
        {...},
    ]
}

```

Returns a list of all grid configuration overrides by role.

##### Returns

A dictionary with an items property that contains an array of up to limit grid configuration overrides by role, starting at index offset. Each entry in the array is a separate grid configuration override by role object. If no more grid configuration overrides by role are available, the resulting array will be empty. This request should never return an error.

### Grid Page Size Overrides

#### Create a grid page size override

```
DEFINITION
POST http://apiserver/gridpagesizeoverrides/:interfaceId

EXAMPLE REQUEST
$.post("http://localhost:49195/gridpagesizeoverrides/Camps", {
    "roleId": "DEC",
    "defaultGridPageSize": 2,
    "minimumGridPageSize": 2,
    "interfaceId":"Camps"
});

EXAMPLE RESPONSE
{
    "id": "18",
    "roleId": "DEC",
    "roleDescription": "Data Entry Clerk",
    "interfaceId": "Camps",
    "minimumGridPageSize": 2,
    "defaultGridPageSize": 2
}

```

Creates a new grid page size override.

##### Arguments

* roleId
* interfaceId
* minimumGridPageSize
* defaultGridPageSize

##### Returns

Returns a grid page size override object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a grid page size override

```
DEFINITION
GET http://apiserver/gridpagesizeoverrides/:interfaceId/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/gridpagesizeoverrides/Camps/19");

EXAMPLE RESPONSE
{
    "id": "19",
    "roleId": "VOL",
    "roleDescription": "Volunteer",
    "interfaceId": "Camps",
    "minimumGridPageSize": 4,
    "defaultGridPageSize": 5
}

```

Retrieves the details of an existing grid page size override. You need only supply the interface id and the id.

##### Arguments

* id (required) - The id of the grid page size override to be retrieved.
* interfaceId - The interfaceId of the interface the override is under.

#### Update a grid page size override

```
DEFINITION
POST http://apiserver/gridpagesizeoverrides/:interfaceId/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/gridpagesizeoverrides/Camps/19", {
    "defaultGridPageSize": 2
});

EXAMPLE RESPONSE
{
    "id": "19",
    "roleId": "VOL",
    "roleDescription": "Volunteer",
    "interfaceId": "Camps",
    "minimumGridPageSize": 4,
    "defaultGridPageSize": 2
}

```

Updates the specified grid page size override by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The id of the grid page size override to be retrieved.
* interfaceId - The interfaceId of the interface the override is under.

##### Returns

Returns the grid page size override object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a grid page size override

```
DEFINITION
DELETE http://apiserver/gridpagesizeoverrides/:interfaceId/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/gridpagesizeoverrides/AccountProcessing/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a grid page size override. It cannot be undone.

##### Arguments

* id (required) - The id of the grid page size override to be retrieved.
* interfaceId - The interfaceId of the interface the override is under.

##### Returns

Returns a `204 No Content` response on success. If the grid page size override does not exist, this call returns an error.

#### List all grid page size overrides for an interface

```
DEFINITION
GET http://apiserver/gridpagesizeoverrides/:interfaceId

EXAMPLE REQUEST
$.get("http://localhost:49195/gridpagesizeoverrides/Camps");

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
            "roleId": "VOL",
            "roleDescription": "Volunteer",
            "interfaceId": "Camps",
            "minimumGridPageSize": 4,
            "defaultGridPageSize": 2
        },
        {...},
    ]
}

```

Returns a list of all grid page size overrides for an interface.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* interfaceId - The interfaceId of the interface the override is under.

##### Returns

A dictionary with an items property that contains an array of up to limit grid page size overrides, starting at index offset. Each entry in the array is a separate grid page size override object. If no more grid page size overrides are available, the resulting array will be empty. This request should never return an error.

### Interface Permissions

#### Create an interface permission

```
DEFINITION
POST http://apiserver/interfacepermissions

EXAMPLE REQUEST
$.post("http://localhost:49195/interfacepermissions", {
    "interface": "AccountsEdit",
    "database": "PROD",
    "action": "ADD",
    "SAW": "S0000001",
    "comment": "Restricts the Add Account Button",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "2"
    "interface": "AccountsEdit",
    "database": "PROD",
    "databaseDescription": "Production Environment",
    "action": "ADD",
    "SAW": "S0000001",
    "sawDescription": "General Programming SAW",
    "comment": "Restricts the Add Account Button",
    "isActive": true
}

```

Creates a new interface permission.

##### Arguments

* interface (required) - The activity interface for the interface permission.
* database (required) - The environment database for the interface permission.
* action (required) - The action secure for the interface permission.
* SAW (required) - The SAW with which to secure for the interface permission.
* isActive (required) - Whether the interface permission is active or not.
* comment (optional) - A comment for the interface permission.

##### Returns

Returns an interface permission object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an interface permission

```
DEFINITION
GET http://apiserver/interfacepermissions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/interfacepermissions/2");

EXAMPLE RESPONSE
{
    "id": "2"
    "interface": "AccountsEdit",
    "database": "PROD",
    "databaseDescription": "Production Environment",
    "action": "ADD",
    "SAW": "S0000001",
    "sawDescription": "General Programming SAW",
    "comment": "Restricts the Add Account Button",
    "isActive": true
}

```

Retrieves the details of an existing interface permission. You need only supply the id.

##### Arguments

* id (required) - The id of the interface permission to be retrieved.

#### Update an interface permission

```
DEFINITION
POST http://apiserver/interfacepermissions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/interfacepermissions/2", {
    "isActive": "false"
});

EXAMPLE RESPONSE
{
    "id": "2"
    "interface": "AccountsEdit",
    "database": "PROD",
    "databaseDescription": "Production Environment",
    "action": "ADD",
    "SAW": "S0000001",
    "sawDescription": "General Programming SAW",
    "comment": "Restricts the Add Account Button",
    "isActive": false
}


```

Updates the specified interface permission by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* interface - The activity interface for the interface permission.
* database - The environment database for the interface permission.
* action - The action secure for the interface permission.
* SAW - The SAW with which to secure for the interface permission.
* isActive - Whether the interface permission is active or not.
* comment - A comment for the interface permission.

##### Returns

Returns the interface permission object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an interface permission

```
DEFINITION
DELETE http://apiserver/interfacepermissions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/interfacepermissions/2", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an interface permission. It cannot be undone.

##### Arguments

* id (required) - The id of the interface permission to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the interface permission does not exist, this call returns an error.

#### List all Interface Permissions

```
DEFINITION
GET http://apiserver/interfacePermissions/

EXAMPLE REQUEST
$.get("http://localhost:49195/interfacePermissions?interface=AccountsEdit");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 57
    },
    "items": [
        {
            "id": "2"
            "interface": "AccountsEdit",
            "database": "PROD",
            "databaseDescription": "Production Environment",
            "action": "ADD",
            "SAW": "S0000001",
            "sawDescription": "General Programming SAW",
            "comment": "Restricts the Add Account Button",
            "isActive": false
        },
        {...}
    ]
}

```

##### Arguments

* interface - Filter results by exact match on interface
* database - Filter results by exact match on database
* action - Filter results by exact match on action
* id - Filter results by the interface permission id
* forCurrentEnvironment - `forCurrentEnvironment=true` filters results to only Interface Permissions relating to the current environment/database

##### Returns

A dictionary with an items property that contains an array of Interface Permissions. Each entry in the array is a separate Interface Permission object.

This request should never return an error.

### Logs

#### Retrieve a log

```
DEFINITION
GET http://apiserver/log/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/log/2015-10-09");

EXAMPLE RESPONSE
{
    "filename": "ServerRetrievedLog_2015-10-09.txt",
    "log": "2015-10-09 07:15:53.6207 [Error] :: (635799717536207001) WARNING: BaseWebUrl is set to localhost in the app.config\r\n2...",
    "date": "2015-10-09T00:00:00"
}

```

Retrieves the details of an existing log. You need only supply the id.

##### Arguments

* id (required) - The date of the log to be retrieved.

### Login

#### Create a token

```
DEFINITION
POST https://apiserver/login

EXAMPLE REQUEST

function createBasicAuth(user, pass) {
    var token = user + ":" + pass;
    var hash = btoa(token);
    return "Basic " + hash;
}
var username = "domain\jdoe";
var password = "somePassword123";

$.ajax({
    type: "POST",
    url: "https://apiserver/login",
    beforeSend: function(xhr) {
        xhr.setRequestHeader("Authorization", createBasicAuth(username, password));
    },
    success: function(data) {
        // save JWT for future API requests
        sessionStorage.setItem("id_token", data.token);
        sessionStorage.setItem("environments", data.environments);
    },
    fail: function(error) {
        // Possible Errors include RequiresVerification, PasswordExpired, or Unauthorized
        alert(error);
    }
});

EXAMPLE RESPONSE
{
    "status": "Success"
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJVc2VyTmFtZSI6ImRkY1xcY3JhaW5leSIsIkV4cGlyZXMiOiJcL0RhdGUoMTQxNTQwMDkxODI3NSlcLOElZYFp5ZSkyNmIkQzVtPzog1BTUF9FKFx1MDAzZTVARkNTO2gvbUM9NF0rUVRtQi53Y1B4LnE0dWxwUkMzVXVQeUFsXXFZKFljVmcoL3g2MUkjSjZBRlx1MDAyNyk7JD8oXYm17ZGBPIEMuXHUwMDI3KTtVSDdHW0AjaDU2JHduJFx1MDAzZWI6K2NeW1g2aTQwYX1zTChxMyNoKnxTbjo6IXpkXzhBIThtNy8yWV5vcipLOiFDU082Zi1vYT9QXHUwMDNjdHZgfS1AdkwtQE1CJXo2UDE7LV8lXHUwMDI2K3pSAwMjZ0Sj1qaXVMMnM5U3MpYn03MEgrWjg7QDdDJTIxKiIsIklzc3VlciI6IkRPTk9SRElSRUNUIn0.JPI11jy4B7cs_qiOy-UWodF-V5ZfTQqTgQRdHSo0pB5YDCxQEryAgGLmyf5kJ3F6o4fZ6QyWc64848SLV4s3iQ",
    "expirationPeriod": "01:00:00",
    "environments": [{id: "DEV", description: "StudioEnterprise DEV", isDefault: false}, {id: "DEV_LOCAL", description: "Local Environment", isDefault: true}]
}

```

#### Refresh a token

```
DEFINITION
POST https://apiserver/login/refresh

EXAMPLE REQUEST
$.ajaxSetup({
    'beforeSend': function(xhr) {
        if (sessionStorage.getItem("id_token")) {
            xhr.setRequestHeader("Authorization",
                'Bearer ' + sessionStorage.getItem("id_token"));
        }
    }
});

$.ajax({
    type: "POST",
    url: "https://apiserver/login/refresh",
    success: function(data) {
        // save JWT for future API requests
        sessionStorage.setItem("id_token", data.token);
    },
});

EXAMPLE RESPONSE
{
    "status": "Success",
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJVc2VyTmFtZSI6ImRkY1xcY3JhaW5leSIsIkV4cGlyZXMiOiJcL0RhdGUoMTQxNTQwMjExMjE1MSlcLyIsIkF1dGhLZXkiOiJrJVszOElZYFp5ZMDAzZTVARkNTO2gvbUM9NF0rUVRtQi53Y1B4LnE0dWxwUkMzVXXFZKFljVmcoL3g2MUkjSjZBRlx1MDAyNyk725-Mjg7LntucyRMQ0RcdTAwMjY6ey47XHUwMDNjelx1MDAzY3NcdTAwM2M5YHVtWn1rO1tKY1I9YENze0orL2ZZLnJFQi1fYm17ZGBPIEMuXHUwMDI3KTtVSDdHW0AjaDU2JHduJFx1MDAzZWI6K2NeW1g2aTQwYX1zTChxMyNoKnxTbjo6IXpkXzhBITh0ZhLnxnQS1cdTAwMjZ0Sj1qaXVMMnM5U3MpYn03MEgrWjg7QDdDJTIxKiIsIklzc3VlciI6IkRPTk9SRElSRUNUIn0.tfXghjaKhJ-_vboDnou70ykn3EQkQkGR4ECmezciZiNuWIkAcZFXIw1BHdKMMiKrPO9G9uWsWJHPrdUcxy8jog",
    "expirationPeriod": "01:00:00",
    "environments": [{id: "DEV", description: "StudioEnterprise DEV", isDefault: false}, {id: "DEV_LOCAL", description: "Local Environment", isDefault: true}]
}


```

### Logos

#### Retrieve a logo

```
DEFINITION
GET http://apiserver/logos/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/logos/PROD");

EXAMPLE RESPONSE
{
    "image", "JhbGciOiJIUzUxMiJ9yJVc2VyTmFtZSI6ImRkY1xcY3JhaW5leSIsIkV4cGlyZXMiOiJcL0RhdGUoMTQxNTQwMjExMjE1MSlcLyIsIkF1dGhLZXkiOiJr..."
}

```

Retrieves the details of an existing logo. You need only supply the id.

##### Arguments

* id (required) - The environment id of the logo to be retrieved.

### Modules

#### List all modules

```
DEFINITION
GET http://apiserver/modules

EXAMPLE REQUEST
$.get("http://localhost:49195/modules");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 57
    },
    "items": [
        {
            "id": "AccountsAndTransactions",
            "title": "Accounts and Transactions",
            "isDefault": true,
            "displaySequence": 0,
            "SAW": "M10AT000"
        },
        {...}
    ]
}

```

Returns a list of all modules the current user has access to, through the user's role.

##### Returns

A dictionary with an items property that contains an array of module objects. Each entry in the array is a module object. This request should never return an error.

### Module Configurations

#### Create a module configuration

```
DEFINITION
POST http://apiserver/moduleconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/moduleconfigurations", {
    "title": "Accounts and Transactions",
    "sawId": "M10AT000",
    "interfaceId": "AccountsAndTransactions"
});

EXAMPLE RESPONSE
{
    "id": "2001900",
    "title": "Accounts and Transactions",
    "sawId": "M10AT000",
    "sawDescription": "Accounts and Transactions Module",
    "interfaceId": "AccountsAndTransactions"
}

```

Creates a new module configuration.

##### Arguments

* title (required) - The Module Configuration Title.
* sawID (required) - The associated SAW Id.
* interfaceId () - The associated Interface Id.

##### Returns

Returns a module configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a module configuration

```
DEFINITION
GET http://apiserver/moduleconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/moduleconfigurations/2001899");

EXAMPLE RESPONSE
{
    "id": "2001900",
    "title": "Accounts and Transactions",
    "sawId": "M10AT000",
    "sawDescription": "Accounts and Transactions Module",
    "interfaceId": "AccountsAndTransactions"
}

```

Retrieves the details of an existing module configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the module configuration to be retrieved.

#### Update a module configuration

```
DEFINITION
POST http://apiserver/moduleconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/moduleconfigurations/2001899", {
    "title": "Accounts and Transactions",
    "sawId": "M10AT000",
    "interfaceId": "AccountsAndTransactions"
});

EXAMPLE RESPONSE
{
    "id": "2001900",
    "title": "Accounts and Transactions",
    "sawId": "M10AT000",
    "sawDescription": "Accounts and Transactions Module",
    "interfaceId": "AccountsAndTransactions"
}


```

Updates the specified module configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title () - The Module Configuration Title.
* sawID () - The associated SAW Id.
* interfaceId () - The associated Interface Id.

##### Returns

Returns the module configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a module configuration

```
DEFINITION
DELETE http://apiserver/moduleconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/moduleconfigurations/2001899", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a module configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the module configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the module configuration does not exist, this call returns an error.

#### List all module configurations

```
DEFINITION
GET http://apiserver/moduleconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/moduleconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "2001900",
            "title": "Accounts and Transactions",
            "sawId": "M10AT000",
            "sawDescription": "Accounts and Transactions Module",
            "interfaceId": "AccountsAndTransactions"
        },
        {...},
    ]
}

```

Returns a list of all module configurations.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* title () - The Module Configuration Title.
* sawID () - The associated SAW Id.

##### Returns

A dictionary with an items property that contains an array of up to limit module configurations, starting at index offset. Each entry in the array is a separate module configuration object. If no more module configurations are available, the resulting array will be empty. This request should never return an error.

### Module Configuration Component Configurations

#### Create a module configuration component configuration

```
DEFINITION
POST http://apiserver/moduleconfigurations/:id/componentconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/moduleconfigurations/6/componentconfigurations", {
    "componentId": "23",
    "groupComponentId": null,
    "sequenceNumber": 1,
    "isDefault": true
});

EXAMPLE RESPONSE
{
    "id": "60348",
    "moduleId": 6,
    "componentId": "23",
    "description": "Gift Studio",
    "groupComponentId": null,
    "groupComponentIdDescription": null,
    "sequenceNumber": 1,
    "isDefault": true
}

```

Creates a new module configuration component configuration.

##### Arguments

* componentId (required) - The component id to associate to this module.
* groupComponentId () - The optional group component id to be in.
* sequenceNumber (required) - The sequence number to show this component in.
* isDefault () - Whether or not this is the default component for this module.

##### Returns

Returns a module configuration component configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a module configuration component configuration

```
DEFINITION
GET http://apiserver/moduleconfigurations/:id/componentconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/moduleconfigurations/6/componentconfigurations/60348");

EXAMPLE RESPONSE
{
    "id": "60348",
    "moduleId": 6,
    "componentId": "23",
    "description": "Gift Studio",
    "groupComponentId": null,
    "groupComponentIdDescription": null,
    "sequenceNumber": 1,
    "isDefault": true
}

```

Retrieves the details of an existing module configuration component configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the module configuration component configuration to be retrieved.

#### Update a module configuration component configuration

```
DEFINITION
POST http://apiserver/moduleconfigurations/:id/componentconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/moduleconfigurations/6/componentconfigurations/60348", {
    "componentId": "23",
    "groupComponentId": null,
    "sequenceNumber": 1,
    "isDefault": true
});

EXAMPLE RESPONSE
{
    "id": "60348",
    "moduleId": 6,
    "componentId": "23",
    "description": "Gift Studio",
    "groupComponentId": null,
    "groupComponentIdDescription": null,
    "sequenceNumber": 1,
    "isDefault": true
}


```

Updates the specified module configuration component configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* componentId () - The component id to associate to this module.
* groupComponentId () - The optional group component id to be in.
* sequenceNumber () - The sequence number to show this component in.
* isDefault () - Whether or not this is the default component for this module.

##### Returns

Returns the module configuration component configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a module configuration component configuration

```
DEFINITION
DELETE http://apiserver/moduleconfigurations/:id/componentconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/moduleconfigurations/6/componentconfigurations/60348", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a module configuration component configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the module configuration component configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the module configuration component configuration does not exist, this call returns an error.

#### List all module configuration component configurations

```
DEFINITION
GET http://apiserver/moduleconfigurations/6/componentconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/moduleconfigurations/:id/componentconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "60348",
            "moduleId": 6,
            "componentId": "23",
            "description": "Gift Studio",
            "groupComponentId": null,
            "groupComponentIdDescription": null,
            "sequenceNumber": 1,
            "isDefault": true
        },
        {...},
    ]
}

```

Returns a list of all module configuration component configurations.

##### Arguments

none

##### Returns

A dictionary with an items property that contains an array of up to limit module configuration component configurations, starting at index offset. Each entry in the array is a separate module configuration component configuration object. If no more module configuration component configurations are available, the resulting array will be empty. This request should never return an error.

### Quick Actions

#### List all quick actions

```
DEFINITION
GET http://apiserver/quickactions

EXAMPLE REQUEST
$.get("http://localhost:49195/quickactions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "quickActionComponentActivityId": "8",
            "componentActivityId": "120",
            "componentInterfaceId": "AccountProcessing",
            "componentShortTitle": "Account Processing",
            "componentLongTitle": "Account Processing",
            "activityInterfaceId": "AccountCommunications",
            "activityShortTitle": "Communications",
            "activityLongTitle": "Account Communications",
            "actionId": "ADD",
            "actionItemId": "EMAIL",
            "displayName": "Create Email",
            "sequenceNumber": 40
        },
        {...},
    ]
}

```

Returns a list of all quick actions for the logged-in user.

##### Returns

A dictionary with an items property that contains an array of up to limit quick actions, starting at index offset. Each entry in the array is a separate quick action object. If no more quick actions are available, the resulting array will be empty. This request should never return an error.

### Quick Action Component Activities

#### Retrieve a quick action component activity

```
DEFINITION
GET http://apiserver/quickactioncomponentactivities/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/quickactioncomponentactivities/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "quickActionComponentActivityId": null,
    "componentActivityId": "120",
    "componentInterfaceId": "AccountProcessing",
    "componentShortTitle": "Account Processing",
    "componentLongTitle": "Account Processing",
    "activityInterfaceId": "AccountCommunications",
    "activityShortTitle": "Communications",
    "activityLongTitle": "Account Communications",
    "actionId": "ADD",
    "actionItemId": "APPOINTMENT",
    "displayName": null,
    "sequenceNumber": null
}

```

Retrieves the details of an existing quick action component activity. You need only supply the id.

##### Arguments

* id (required) - The id of the quick action component activity to be retrieved.

#### List all quick action component activities

```
DEFINITION
GET http://apiserver/quickactioncomponentactivities

EXAMPLE REQUEST
$.get("http://localhost:49195/quickactioncomponentactivities");

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
            "quickActionComponentActivityId": null,
            "componentActivityId": "120",
            "componentInterfaceId": "AccountProcessing",
            "componentShortTitle": "Account Processing",
            "componentLongTitle": "Account Processing",
            "activityInterfaceId": "AccountCommunications",
            "activityShortTitle": "Communications",
            "activityLongTitle": "Account Communications",
            "actionId": "ADD",
            "actionItemId": "APPOINTMENT",
            "displayName": null,
            "sequenceNumber": null
        },
        {...},
    ]
}

```

Returns a list of all quick action component activities.

##### Returns

A dictionary with an items property that contains an array of up to limit quick action component activities, starting at index offset. Each entry in the array is a separate quick action component activity object. If no more quick action component activities are available, the resulting array will be empty. This request should never return an error.

### Quick Action Configurations

#### Create a quick action configuration

```
DEFINITION
POST http://apiserver/quickactionconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/quickactionconfigurations", {
    "quickActionComponentActivityId": "28927",
    "displayName": "Order",
    "sequenceNumber": 15
});

EXAMPLE RESPONSE
{
    "id": "456135",
    "quickActionComponentActivityId": "28927",
    "componentActivityId": "9156",
    "componentInterfaceId": "AccountProcessing",
    "componentShortTitle": "Account Processing",
    "componentLongTitle": "Account Processing",
    "activityInterfaceId": "TransactionOrders",
    "activityShortTitle": "Orders (F3)",
    "activityLongTitle": "Account Order Entry",
    "actionId": null,
    "actionItemId": null,
    "displayName": "Order",
    "sequenceNumber": 15
}

```

Creates a new quick action configuration.

##### Arguments

* quickActionComponentActivityId (required) - The id of the related quick action/component/activity grouping (the SEC51\_QuickActionComponentActivities RecordId).
* displayName (required) - The display name of the quick action configuration.
* sequenceNumber (required) - The sequence number of the quick action configuration.

##### Returns

Returns a quick action configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a quick action configuration

```
DEFINITION
GET http://apiserver/quickactionconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/quickactionconfigurations/456135");

EXAMPLE RESPONSE
{
    "id": "456135",
    "quickActionComponentActivityId": "28927",
    "componentActivityId": "9156",
    "componentInterfaceId": "AccountProcessing",
    "componentShortTitle": "Account Processing",
    "componentLongTitle": "Account Processing",
    "activityInterfaceId": "TransactionOrders",
    "activityShortTitle": "Orders (F3)",
    "activityLongTitle": "Account Order Entry",
    "actionId": null,
    "actionItemId": null,
    "displayName": "Order",
    "sequenceNumber": 15
}

```

Retrieves the details of an existing quick action configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the quick action configuration to be retrieved.

#### Update a quick action configuration

```
DEFINITION
POST http://apiserver/quickactionconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/quickactionconfigurations/456135", {
    "displayName": "Create Order",
    "sequenceNumber": 25
});

EXAMPLE RESPONSE
{
    "id": "456135",
    "quickActionComponentActivityId": "28927",
    "componentActivityId": "9156",
    "componentInterfaceId": "AccountProcessing",
    "componentShortTitle": "Account Processing",
    "componentLongTitle": "Account Processing",
    "activityInterfaceId": "TransactionOrders",
    "activityShortTitle": "Orders (F3)",
    "activityLongTitle": "Account Order Entry",
    "actionId": null,
    "actionItemId": null,
    "displayName": "Create Order",
    "sequenceNumber": 25
}

```

Updates the specified quick action configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* quickActionComponentActivityId (optional) - The id of the related quick action/component/activity grouping (the SEC51\_QuickActionComponentActivities RecordId).
* displayName (optional) - The display name of the quick action configuration.
* sequenceNumber (optional) - The sequence number of the quick action configuration.

##### Returns

Returns the quick action configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a quick action configuration

```
DEFINITION
DELETE http://apiserver/quickactionconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/quickactionconfigurations/456135", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a quick action configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the quick action configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the quick action configuration does not exist, this call returns an error.

#### List all quick action configurations

```
DEFINITION
GET http://apiserver/quickactionconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/quickactionconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "456135",
            "quickActionComponentActivityId": "28927",
            "componentActivityId": "9156",
            "componentInterfaceId": "AccountProcessing",
            "componentShortTitle": "Account Processing",
            "componentLongTitle": "Account Processing",
            "activityInterfaceId": "TransactionOrders",
            "activityShortTitle": "Orders (F3)",
            "activityLongTitle": "Account Order Entry",
            "actionId": null,
            "actionItemId": null,
            "displayName": "Create Order",
            "sequenceNumber": 25
        },
        {...},
    ]
}

```

Returns a list of all quick action configurations.

##### Arguments

* quickActionComponentActivityId (optional) - The id of the related quick action/component/activity grouping (the SEC51\_QuickActionComponentActivities RecordId).
* componentActivityId (optional) - The id of the related component/activity pairing (the SEC20\_ComponentConfigurationsDAs RecordId).
* componentInterfaceId (optional) - The interface id of the related component.
* componentShortTitle (optional) - The short title of the related component.
* componentLongTitle (optional) - The long title of the related component.
* activityInterfaceId (optional) - The interface id of the related activity.
* activityShortTitle (optional) - The short title of the related activity.
* activityLongTitle (optional) - The long title of the related activity.
* actionId (optional) - The action id of the quick action/component/activity grouping. (Ex. ADD)
* actionItemId (optional) - The action item id of the quick action/component/activity grouping. (Ex. LETTER)
* displayName (optional) - The display name of the quick action configuration.
* sequenceNumber (optional) - The sequence number of the quick action configuration.

##### Returns

A dictionary with an items property that contains an array of up to limit quick action configurations, starting at index offset. Each entry in the array is a separate quick action configuration object. If no more quick action configurations are available, the resulting array will be empty. This request should never return an error.

### Quick Action Configuration Overrides

#### Create a quick action configuration override

```
DEFINITION
POST http://apiserver/quickactionconfigurations/overrides

EXAMPLE REQUEST
$.post("http://localhost:49195/quickactionconfigurations/overrides", {
    "roleId": "DDCSTAFF",
    "quickActionComponentActivityId": "28927",
    "displayName": "Order",
    "sequenceNumber": 15
});

EXAMPLE RESPONSE
{
    "id": "4984135",
    "roleId": "DDCSTAFF",
    "roleDescription": "DonorDirect Staff/Training",
    "quickActionComponentActivityId": "28927",
    "componentActivityId": "9156",
    "componentInterfaceId": "AccountProcessing",
    "componentShortTitle": "Account Processing",
    "componentLongTitle": "Account Processing",
    "activityInterfaceId": "TransactionOrders",
    "activityShortTitle": "Orders (F3)",
    "activityLongTitle": "Account Order Entry",
    "actionId": null,
    "actionItemId": null,
    "displayName": "Order",
    "sequenceNumber": 15
}

```

Creates a new quick action configuration override.

##### Arguments

* roleId (conditionally required) - The Role for which to override the quick action. Required if `accessorId` is not provided, otherwise must be `null`.
* accessorId (conditionally required) - The Accessor for which to override the quick action. Required if `roleId` is not provided, otherwise must be `null`.
* quickActionComponentActivityId (required) - The id of the related quick action/component/activity grouping (the SEC51\_QuickActionComponentActivities RecordId).
* displayName (required) - The display name of the quick action configuration override.
* sequenceNumber (required) - The sequence number of the quick action configuration override.

##### Returns

Returns a quick action configuration override object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a quick action configuration override

```
DEFINITION
GET http://apiserver/quickactionconfigurations/overrides/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/quickactionconfigurations/overrides/4984135");

EXAMPLE RESPONSE
{
    "id": "4984135",
    "roleId": "DDCSTAFF",
    "roleDescription": "DonorDirect Staff/Training",
    "quickActionComponentActivityId": "28927",
    "componentActivityId": "9156",
    "componentInterfaceId": "AccountProcessing",
    "componentShortTitle": "Account Processing",
    "componentLongTitle": "Account Processing",
    "activityInterfaceId": "TransactionOrders",
    "activityShortTitle": "Orders (F3)",
    "activityLongTitle": "Account Order Entry",
    "actionId": null,
    "actionItemId": null,
    "displayName": "Order",
    "sequenceNumber": 15
}

```

Retrieves the details of an existing quick action configuration override. You need only supply the id.

##### Arguments

* id (required) - The id of the quick action configuration override to be retrieved.

#### Update a quick action configuration override

```
DEFINITION
POST http://apiserver/quickactionconfigurations/overrides/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/quickactionconfigurations/overrides/4984135", {
    "roleId": null,
    "accessorId": "238927"
});

EXAMPLE RESPONSE
{
    "id": "4984135",
    "accessorId": "238927",
    "accessorName": "John Johnson",
    "quickActionComponentActivityId": "28927",
    "componentActivityId": "9156",
    "componentInterfaceId": "AccountProcessing",
    "componentShortTitle": "Account Processing",
    "componentLongTitle": "Account Processing",
    "activityInterfaceId": "TransactionOrders",
    "activityShortTitle": "Orders (F3)",
    "activityLongTitle": "Account Order Entry",
    "actionId": null,
    "actionItemId": null,
    "displayName": "Order",
    "sequenceNumber": 15
}


```

Updates the specified quick action configuration override by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* roleId (optional) - The Role for which to override the quick action.
* accessorId (optional) - The Accessor for which to override the quick action.
* quickActionComponentActivityId (optional) - The id of the related quick action/component/activity grouping (the SEC51\_QuickActionComponentActivities RecordId).
* displayName (optional) - The display name of the quick action configuration override.
* sequenceNumber (optional) - The sequence number of the quick action configuration override.

##### Returns

Returns the quick action configuration override object if the update succeeded. Returns an error if update parameters are invalid.

#### Copy quick action configurations to overrides

```
DEFINITION
GET http://apiserver/quickactionconfigurations/overrides/copyquickactions

EXAMPLE REQUEST
$.post("http://localhost:49195/quickactionconfigurations/overrides/copyquickactions", {
    "roleId": "DDCSTAFF"
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
            "id": "4984135",
            "accessorId": "238927",
            "accessorName": "John Johnson",
            "quickActionComponentActivityId": "28927",
            "componentActivityId": "9156",
            "componentInterfaceId": "AccountProcessing",
            "componentShortTitle": "Account Processing",
            "componentLongTitle": "Account Processing",
            "activityInterfaceId": "TransactionOrders",
            "activityShortTitle": "Orders (F3)",
            "activityLongTitle": "Account Order Entry",
            "actionId": null,
            "actionItemId": null,
            "displayName": "Order",
            "sequenceNumber": 15
        },
        {...},
    ]
}

```

Creates a quick action configuration override with the specified `roleId` or `accessorId` for each quick action configuration.

##### Arguments

* roleId (optional) - The Role of the copied quick action configuration overrides. Required if `accessorId` is not provided, otherwise must be `null`.
* accessorId (optional) - The Accessor of the copied quick action configuration overrides. Required if `roleId` is not provided, otherwise must be `null`.

##### Returns

Returns the copied quick action configuration override objects if the copy succeeded. Returns an error if copy parameters were invalid.

#### Delete a quick action configuration override

```
DEFINITION
DELETE http://apiserver/quickactionconfigurations/overrides/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/quickactionconfigurations/overrides/4984135", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a quick action configuration override. It cannot be undone.

##### Arguments

* id (required) - The id of the quick action configuration override to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the quick action configuration override does not exist, this call returns an error.

#### List all quick action configuration overrides

```
DEFINITION
GET http://apiserver/quickactionconfigurations/overrides

EXAMPLE REQUEST
$.get("http://localhost:49195/quickactionconfigurations/overrides");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4984135",
            "accessorId": "238927",
            "accessorName": "John Johnson",
            "quickActionComponentActivityId": "28927",
            "componentActivityId": "9156",
            "componentInterfaceId": "AccountProcessing",
            "componentShortTitle": "Account Processing",
            "componentLongTitle": "Account Processing",
            "activityInterfaceId": "TransactionOrders",
            "activityShortTitle": "Orders (F3)",
            "activityLongTitle": "Account Order Entry",
            "actionId": null,
            "actionItemId": null,
            "displayName": "Order",
            "sequenceNumber": 15
        },
        {...},
    ]
}

```

Returns a list of all quick action configuration overrides.

##### Returns

A dictionary with an items property that contains an array of up to limit quick action configuration overrides, starting at index offset. Each entry in the array is a separate quick action configuration override object. If no more quick action configuration overrides are available, the resulting array will be empty. This request should never return an error.

### Report Configurations

#### Create a report configuration

```
DEFINITION
POST http://apiserver/reportconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/reportconfigurations", {
    "name": "Account Annual Summary",
    "description": "Yearly Donation Revenue from Specified Start Date",
    "category": "ACCOUNT",
    "saw": "RSR0001",
    "subCategory": "LISTING",
    "origin": "DonorStudio",
    "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
    "image": ""
});

EXAMPLE RESPONSE
{
    "id": "184",
    "name": "Account Annual Summary",
    "description": "Yearly Donation Revenue from Specified Start Date",
    "category": "ACCOUNT",
    "saw": "RSR0001",
    "sawDescription": "Account Annual Summary",
    "subCategory": "LISTING",
    "origin": "DonorStudio",
    "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
    "image": ""
}

```

Creates a new report configuration.

##### Arguments

* name (required) - The name
* description () - The description
* category (required) - The category
* saw (required) - The SAW
* subCategory () - The sub category
* origin () - The origin
* comment () - The comment
* image () - The image

##### Returns

Returns a report configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a report configuration

```
DEFINITION
GET http://apiserver/reportconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/reportconfigurations/1");

EXAMPLE RESPONSE
{
    "id": "184",
    "name": "Account Annual Summary",
    "description": "Yearly Donation Revenue from Specified Start Date",
    "category": "ACCOUNT",
    "saw": "RSR0001",
    "sawDescription": "Account Annual Summary",
    "subCategory": "LISTING",
    "origin": "DonorStudio",
    "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
    "image": ""
}

```

Retrieves the details of an existing report configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the report configuration to be retrieved.

#### Update a report configuration

```
DEFINITION
POST http://apiserver/reportconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/reportconfigurations/1", {
    "id": "184",
    "name": "Account Annual Summary",
    "description": "Yearly Donation Revenue from Specified Start Date",
    "category": "ACCOUNT",
    "saw": "RSR0001",
    "sawDescription": "Account Annual Summary",
    "subCategory": "LISTING",
    "origin": "DonorStudio",
    "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
    "image": ""
});

EXAMPLE RESPONSE
{
    "id": "184",
    "name": "Account Annual Summary",
    "description": "Yearly Donation Revenue from Specified Start Date",
    "category": "ACCOUNT",
    "saw": "RSR0001",
    "sawDescription": "Account Annual Summary",
    "subCategory": "LISTING",
    "origin": "DonorStudio",
    "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
    "image": ""
}


```

Updates the specified report configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* name () - The name
* description () - The description
* category () - The category
* saw () - The SAW
* subCategory () - The sub category
* origin () - The origin
* comment () - The comment
* image () - The image

##### Returns

Returns the report configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a report configuration

```
DEFINITION
DELETE http://apiserver/reportconfiguraions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/reportconfiguraions/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a report configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the report configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the report configuration does not exist, this call returns an error.

#### List all report configurations

```
DEFINITION
GET http://apiserver/reportconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/reportconfigurations?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "184",
            "name": "Account Annual Summary",
            "description": "Yearly Donation Revenue from Specified Start Date",
            "category": "ACCOUNT",
            "saw": "RSR0001",
            "sawDescription": "Account Annual Summary",
            "subCategory": "LISTING",
            "origin": "DonorStudio",
            "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
            "image": ""
        },
        {...},
    ]
}

```

Returns a list of all report configurations.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by id.
* name (optional) - Filter list by the partial match of report name.
* description (optional) - Filter list by partial match of report description.
* category (optional) - Filter list by partial match of report category.
* subCategory (optional) - Filter list by partial match of report sub category.
* origin (optional) - Filter list by partial match of report origin.

##### Returns

A dictionary with an items property that contains an array of up to limit report configurations, starting at index offset. Each entry in the array is a separate repot configuration object. If no more report configurations are available, the resulting array will be empty. This request should never return an error.

### Report Configuration Databases

#### Create a report configuration database

```
DEFINITION
POST http://apiserver/reportconfigurations/:id/databases

EXAMPLE REQUEST
$.post("http://localhost:49195/reportconfigurations/183/databases", {
    "databaseId": "DEV",
    "reportUrl": "http://www.google.com"
}
});

EXAMPLE RESPONSE
{
    "id": "26700",
    "reportId": "183",
    "databaseId": "DEV",
    "databaseDescription": "StudioEnterprise DEV",
    "reportUrl": "http://www.google.com"
}

```

Creates a new report configuration database.

##### Arguments

* databaseId (required) - The Database Id
* url (required) - The URL

##### Returns

Returns a report configuration database object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a report configuration database

```
DEFINITION
GET http://apiserver/reportconfigurations/:id/databases/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/reportconfigurations/183/databases/26700");

EXAMPLE RESPONSE
{
    "id": "26700",
    "reportId": "183",
    "databaseId": "DEV",
    "databaseDescription": "StudioEnterprise DEV",
    "reportUrl": "http://www.google.com"
}

```

Retrieves the details of an existing report configuration database. You need only supply the id.

##### Arguments

* id (required) - The id of the report configuration database to be retrieved.

#### Update a report configuration database

```
DEFINITION
POST http://apiserver/reportconfigurations/:id/databases/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/reportconfigurations/183/databases/26700", {
    "databaseId": "DEV",
    "reportUrl": "http://www.google.com"
});

EXAMPLE RESPONSE
{
    "id": "26700",
    "reportId": "183",
    "databaseId": "DEV",
    "databaseDescription": "StudioEnterprise DEV",
    "reportUrl": "http://www.google.com"
}


```

Updates the specified report configuration database by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* databaseId () - The Database Id
* url () - The URL

##### Returns

Returns the report configuration database object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a report configuration database

```
DEFINITION
DELETE http://apiserver/reportconfigurations/:id/databses/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/reportconfigurations/183/databses/26700", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a report configuration database. It cannot be undone.

##### Arguments

* id (required) - The id of the report configuration database to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the report configuration database does not exist, this call returns an error.

#### List all report configuration databases

```
DEFINITION
GET http://apiserver/reportconfigurations/:id/databases

EXAMPLE REQUEST
$.get("http://localhost:49195/reportconfigurations/183/databases?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "26700",
            "reportId": "183",
            "databaseId": "DEV",
            "databaseDescription": "StudioEnterprise DEV",
            "reportUrl": "http://www.google.com"
        },
        {...},
    ]
}

```

Returns a list of all report configuration databases.

##### Arguments

* reportId (required) - The Report Id.

##### Returns

A dictionary with an items property that contains an array of up to limit report configuration databases, starting at index offset. Each entry in the array is a separate report configuration database object. If no more report configuration databases are available, the resulting array will be empty. This request should never return an error.

### SAWs

#### Create a saw

```
DEFINITION
POST http://apiserver/saws

EXAMPLE REQUEST
$.post("http://localhost:49195/saws", {
    "sawId": "A0000001A",
    "description": "Account lookup modules",
    "category": "DStudio",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "74816",
    "sawId": "A0000001A",
    "description": "Account lookup modules",
    "category": "DStudio",
    "isActive": true
}

```

Creates a new saw.

##### Arguments

* sawId (required) - The SAW id.
* description (required) - The description of the SAW.
* category (required) - The category of the SAW.
* isActive (required) - Whether or not this SAW is active.

##### Returns

Returns a saw object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a saw

```
DEFINITION
GET http://apiserver/saws/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/saws/74816");

EXAMPLE RESPONSE
{
    "id": "74816",
    "sawId": "A0000001A",
    "description": "Account lookup modules",
    "category": "DStudio",
    "isActive": true
}

```

Retrieves the details of an existing saw. You need only supply the id.

##### Arguments

* id (required) - The id of the saw to be retrieved.

#### Update a saw

```
DEFINITION
POST http://apiserver/saw/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/saw/74816", {
    "sawId": "A0000001A",
    "description": "Account lookup modules",
    "category": "DStudio",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "74816",
    "sawId": "A0000001A",
    "description": "Account lookup modules",
    "category": "DStudio",
    "isActive": true
}


```

Updates the specified saw by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sawId () - The SAW id.
* description () - The description of the SAW.
* category () - The category of the SAW.
* isActive () - Whether or not this SAW is active.

##### Returns

Returns the saw object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a saw

```
DEFINITION
DELETE http://apiserver/saws/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/saws/74816", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a saw. It cannot be undone.

##### Arguments

* id (required) - The id of the saw to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the saw does not exist, this call returns an error.

#### List all saws

```
DEFINITION
GET http://apiserver/saws

EXAMPLE REQUEST
$.get("http://localhost:49195/saws?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "74816",
            "sawId": "A0000001A",
            "description": "Account lookup modules",
            "category": "DStudio",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all saws.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* sawId () - The SAW id.
* description () - The description of the SAW.
* category () - The category of the SAW.
* isActive () - Whether or not this SAW is active.

##### Returns

A dictionary with an items property that contains an array of up to limit saws, starting at index offset. Each entry in the array is a separate saw object. If no more saws are available, the resulting array will be empty. This request should never return an error.

### Security Functions

#### Create a security function

```
DEFINITION
POST http://apiserver/securityfunctions

EXAMPLE REQUEST
$.post("http://localhost:49195/securityfunctions", {
    "functionId": "DEO",
    "description": "Data Entry Operator",
    "category": "TS",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "127",
    "functionId": "DEO",
    "description": "Data Entry Operator",
    "category": "TS",
    "isActive": true
}

```

Creates a new security function.

##### Arguments

* functionId (required) - The function id of the security function.
* description (required) - The description of the security function.
* category (required) - The category of the security function.
* isActive (required) - Whether or not this model is active.

##### Returns

Returns a security function object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a security function

```
DEFINITION
GET http://apiserver/securityfunctions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/securityfunctions/127");

EXAMPLE RESPONSE
{
    "id": "127",
    "functionId": "DEO",
    "description": "Data Entry Operator",
    "category": "TS",
    "isActive": true
}

```

Retrieves the details of an existing security function. You need only supply the id.

##### Arguments

* id (required) - The id of the security function to be retrieved.

#### Update a security function

```
DEFINITION
POST http://apiserver/securityfunctions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/securityfunctions/127", {
    "functionId": "DEO",
    "description": "Data Entry Operator",
    "category": "TS",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "127",
    "functionId": "DEO",
    "description": "Data Entry Operator",
    "category": "TS",
    "isActive": true
}


```

Updates the specified security function by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* functionId () - The function id of the security function.
* description () - The description of the security function.
* category () - The category of the security function.
* isActive () - Whether or not this model is active.

##### Returns

Returns the security function object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a security function

```
DEFINITION
DELETE http://apiserver/securityfunctions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/securityfunctions/127", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a security function. It cannot be undone.

##### Arguments

* id (required) - The id of the security function to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the security function does not exist, this call returns an error.

#### List all security functions

```
DEFINITION
GET http://apiserver/securityfunctions

EXAMPLE REQUEST
$.get("http://localhost:49195/securityfunctions?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "127",
            "functionId": "DEO",
            "description": "Data Entry Operator",
            "category": "TS",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all security functions.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* functionId () - The function id of the security function.
* description () - The description of the security function.
* category () - The category of the security function.
* isActive () - Whether or not this model is active.

##### Returns

A dictionary with an items property that contains an array of up to limit security functions, starting at index offset. Each entry in the array is a separate security function object. If no more security functions are available, the resulting array will be empty. This request should never return an error.

### Security Function SAWs

#### Create a security function saw

```
DEFINITION
POST http://apiserver/securityfunctions/:id/saws

EXAMPLE REQUEST
$.post("http://localhost:49195/securityfunctions/127/saws", {
    "sawId": "AAT10ALK",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "97496",
    "functionId": "DEO",
    "sawId": "AAT10ALK",
    "description": "Account Lookup Activity",
    "category": "DStudio",
    "isActive": true
}

```

Creates a new security function saw.

##### Arguments

* sawId (required) - The SAW Id to associate to this security function.
* isActive (required) - Whether or not this security function is active.

##### Returns

Returns a security function saw object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a security function saw

```
DEFINITION
GET http://apiserver/securityfunction/:id/saws/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/securityfunction/127/saws/97496");

EXAMPLE RESPONSE
{
    "id": "97496",
    "functionId": "DEO",
    "sawId": "AAT10ALK",
    "description": "Account Lookup Activity",
    "category": "DStudio",
    "isActive": true
}

```

Retrieves the details of an existing security function saw. You need only supply the id.

##### Arguments

* id (required) - The id of the security function saw to be retrieved.

#### Update a security function saw

```
DEFINITION
POST http://apiserver/securityfunctions/:id/saws/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/securityfunctions/127/saws/97496", {
    "sawId": "AAT10ALK",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "97496",
    "functionId": "DEO",
    "sawId": "AAT10ALK",
    "description": "Account Lookup Activity",
    "category": "DStudio",
    "isActive": true
}


```

Updates the specified security function saw by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* sawId () - The SAW Id to associate to this security function.
* isActive () - Whether or not this security function is active.

##### Returns

Returns the security function saw object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a security function saw

```
DEFINITION
DELETE http://apiserver/securityfunctions/:id/saws/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/securityfunctions/:id/saws/97496", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a security function saw. It cannot be undone.

##### Arguments

* id (required) - The id of the security function saw to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the security function saw does not exist, this call returns an error.

#### List all security function saws

```
DEFINITION
GET http://apiserver/securityfunctions/:id/saws

EXAMPLE REQUEST
$.get("http://localhost:49195/securityfunctions/127/saws");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "97496",
            "functionId": "DEO",
            "sawId": "AAT10ALK",
            "description": "Account Lookup Activity",
            "category": "DStudio",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all security function saws.

##### Returns

A dictionary with an items property that contains an array of up to limit security function saws, starting at index offset. Each entry in the array is a separate security function saw object. If no more security function saws are available, the resulting array will be empty. This request should never return an error.

#### Copy all security function saws

```
DEFINITION
GET http://apiserver/securityfunctions/:id/saws/copy

EXAMPLE REQUEST
$.get("http://localhost:49195/securityfunctions/127/saws/copy");

EXAMPLE RESPONSE
204 No Content

```

Returns a list of all security function saws.

##### Arguments

* functionId (required) - The id of the security function saw to copy SAWs from.

##### Returns

Returns a `204 No Content` response on success. If the security function does not exist, this call returns an error.

### Security Roles

#### Create a security role

```
DEFINITION
POST http://apiserver/securityroles

EXAMPLE REQUEST
$.post("http://localhost:49195/securityroles", {
    "roleId": "DEO",
    "description": "Data Entry Operator",
    "functionalCategory": null,
    "isActive": true,
    "sendEmailsOnBehalfOfOtherAccessors": false,
    "twoStepVerificationEnabled": false,
    "restrictViewsBasedOnAssignment": false,
    "restrictFinancialInformation": false,
    "restrictCommunications": false,
    "restrictEventViewsBasedOnAssignment": false,
    "autoAddAccountAssignment": false,
    "autoAddAccountAssignmentsByProjectAndPledgeAccess": false,
    "autoAddEventAssignment": false,
    "defaultAccountSearchStatuses": {
        "active": true,
        "inactive": true,
        "acquired": true,
        "duplicate": false,
        "merged": true
    }
});

EXAMPLE RESPONSE
{
    "id": "62",
    "roleId": "DEO",
    "description": "Data Entry Operator",
    "functionalCategory": null,
    "functionalCategoryDescription": null,
    "isActive": true,
    "sendEmailsOnBehalfOfOtherAccessors": false,
    "twoStepVerificationEnabled": false,
    "restrictViewsBasedOnAssignment": false,
    "restrictFinancialInformation": false,
    "restrictCommunications": false,
    "restrictEventViewsBasedOnAssignment": false,
    "autoAddAccountAssignment": false,
    "autoAddAccountAssignmentsByProjectAndPledgeAccess": false,
    "autoAddEventAssignment": false,
    "defaultAccountSearchStatuses": {
        "active": true,
        "inactive": true,
        "acquired": true,
        "duplicate": false,
        "merged": true
    }
}

```

Creates a new security role.

##### Arguments

* roleId (required) - The Role Id
* description (required) - The Description
* functionalCategory (required when `autoAddAccountAssignment`, `autoAddAccountAssignmentsByProjectAndPledgeAccess`, or `autoAddEventAssignment` is `true`) - Functional Category
* isActive (required) - Specifies whether the role is active
* sendEmailsOnBehalfOfOtherAccessors (required) - Whether accessors with this role be allowed to send email on behalf of other accessors
* twoStepVerificationEnabled (required) - Specifies whether two step verification is enabled
* restrictViewsBasedOnAssignment (required) - Toggle for Views based on assignment
* restrictFinancialInformation (required) - Specifies whether the role should be restricted to the financial information (i.e. projects and pledges) configured for the accessor
* restrictCommunications (required) - Specifies whether the role should be restricted to the communications assigned to the accessor
* restrictEventViewsBasedOnAssignment (required) - Toggle for Event/Event Type Views based on assignment
* autoAddAccountAssignment (required; value required to be `true` when `restrictViewsBasedOnAssignment` is `true`) - Specifies that new accounts should be automatically assigned based on the functional category of the user
* autoAddAccountAssignmentsByProjectAndPledgeAccess (required) - Specifies that accounts should be automatically assigned when a project, pledge, or recurring donation is added or updated based on the functional category of the user
* autoAddEventAssignment (required; value required to be `true` when `restrictEventViewsBasedOnAssignment` is `true`) - Specifies that new events and event types should be automatically assigned based on the functional category of the user
* defaultAccountSearchStatuses (optional) - Default Account Search Statuses object that contains the default statuses to be used when searching for accounts. Valid statuses are `active`, `inactive`, `acquired`, `duplicate`, and `merged`.

##### Returns

Returns a security role object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a security role

```
DEFINITION
GET http://apiserver/securityroles/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/securityroles/62");

EXAMPLE RESPONSE
{
    "id": "62",
    "roleId": "DEO",
    "description": "Data Entry Operator",
    "functionalCategory": null,
    "functionalCategoryDescription": null,
    "isActive": true,
    "sendEmailsOnBehalfOfOtherAccessors": false,
    "twoStepVerificationEnabled": false,
    "restrictViewsBasedOnAssignment": false,
    "restrictFinancialInformation": false,
    "restrictCommunications": false,
    "restrictEventViewsBasedOnAssignment": false,
    "autoAddAccountAssignment": false,
    "autoAddAccountAssignmentsByProjectAndPledgeAccess": false,
    "autoAddEventAssignment": false,
    "defaultAccountSearchStatuses": {
        "active": true,
        "inactive": true,
        "acquired": true,
        "duplicate": false,
        "merged": true
    }
}

```

Retrieves the details of an existing security role. You need only supply the id.

##### Arguments

* id (required) - The id of the security role to be retrieved.

#### Update a security role

```
DEFINITION
POST http://apiserver/securityroles/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/securityroles/62", {
    "roleId": "DEO",
    "description": "Data Entry Operator",
    "isActive": true,
    "restrictViewsBasedOnAssignment": false,
    "functionalCategory": null,
    "sendEmailsOnBehalfOfOtherAccessors": false,
    "restrictFinancialInformation": false,
    "restrictCommunications": false,
    "autoAddAccountAssignment": false,
    "defaultAccountSearchStatuses": {
        "active": true,
        "inactive": true,
        "acquired": false,
        "duplicate": false,
        "merged": true
    }
});

EXAMPLE RESPONSE
{
    "id": "62",
    "roleId": "DEO",
    "description": "Data Entry Operator",
    "functionalCategory": null,
    "functionalCategoryDescription": null,
    "isActive": true,
    "sendEmailsOnBehalfOfOtherAccessors": false,
    "twoStepVerificationEnabled": false,
    "restrictViewsBasedOnAssignment": false,
    "restrictFinancialInformation": false,
    "restrictCommunications": false,
    "restrictEventViewsBasedOnAssignment": false,
    "autoAddAccountAssignment": false,
    "autoAddAccountAssignmentsByProjectAndPledgeAccess": false,
    "autoAddEventAssignment": false,
    "defaultAccountSearchStatuses": {
        "active": true,
        "inactive": true,
        "acquired": false,
        "duplicate": false,
        "merged": true
    }
}


```

Updates the specified security role by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* roleId (optional) - The Role Id
* description (optional) - The Description
* functionalCategory (conditional; required when `autoAddAccountAssignment`, `autoAddAccountAssignmentsByProjectAndPledgeAccess`, or `autoAddEventAssignment` is `true`) - Functional Category
* isActive (optional) - Specifies whether the role is active
* sendEmailsOnBehalfOfOtherAccessors (optional) - Whether accessors with this role be allowed to send email on behalf of other accessors
* twoStepVerificationEnabled (optional) - Specifies whether two step verification is enabled
* restrictViewsBasedOnAssignment (optional) - Toggle for Views based on assignment
* restrictFinancialInformation (optional) - Specifies whether the role should be restricted to the financial information (i.e. projects and pledges) configured for the accessor
* restrictCommunications (optional) - Specifies whether the role should be restricted to the communications assigned to the accessor
* restrictEventViewsBasedOnAssignment (optional) - Toggle for Event/Event Type Views based on assignment
* autoAddAccountAssignment (conditional; required to be `true` when `restrictViewsBasedOnAssignment` is `true`) - Specifies that new accounts should be automatically assigned based on the functional category of the user
* autoAddAccountAssignmentsByProjectAndPledgeAccess (optional) - Specifies that accounts should be automatically assigned when a project, pledge, or recurring donation is added or updated based on the functional category of the user
* autoAddEventAssignment (conditional; required to be `true` when `restrictEventViewsBasedOnAssignment` is `true`) - Specifies that new events and event types should be automatically assigned based on the functional category of the user
* defaultAccountSearchStatuses (optional) - Default Account Search Statuses object that contains the default statuses to be used when searching for accounts. Valid statuses are `active`, `inactive`, `acquired`, `duplicate`, and `merged`.

##### Returns

Returns the security role object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a security role

```
DEFINITION
DELETE http://apiserver/securityroles/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/securityroles/62", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a security role. It cannot be undone.

##### Arguments

* id (required) - The id of the security roles to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the security role does not exist, this call returns an error.

#### List all security roles

```
DEFINITION
GET http://apiserver/securityroles

EXAMPLE REQUEST
$.get("http://localhost:49195/securityroles?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "62",
            "roleId": "DEO",
            "description": "Data Entry Operator",
            "functionalCategory": null,
            "functionalCategoryDescription": null,
            "isActive": true,
            "sendEmailsOnBehalfOfOtherAccessors": false,
            "twoStepVerificationEnabled": false,
            "restrictViewsBasedOnAssignment": false,
            "restrictFinancialInformation": false,
            "restrictCommunications": false,
            "restrictEventViewsBasedOnAssignment": false,
            "autoAddAccountAssignment": false,
            "autoAddAccountAssignmentsByProjectAndPledgeAccess": false,
            "autoAddEventAssignment": false,
            "defaultAccountSearchStatuses": {
                "active": true,
                "inactive": true,
                "acquired": false,
                "duplicate": false,
                "merged": true
            }
        },
        {...},
    ]
}

```

Returns a list of all security roles.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* roleId (optional) - The Role Id
* description (optional) - The Description
* isActive (optional) - The Active bit

##### Returns

A dictionary with an items property that contains an array of up to limit security roles, starting at index offset. Each entry in the array is a separate security role object. If no more security roles are available, the resulting array will be empty. This request should never return an error.

### Security Role Security Functions

#### Create a security role security function

```
DEFINITION
POST http://apiserver/securityroles/:id/securityfunctions

EXAMPLE REQUEST
$.post("http://localhost:49195/securityroles/:id/securityfunctions", {
    "functionId": "DEC",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "86",
    "roleId": "DEO",
    "functionId": "DEC",
    "description": "Data Entry Clerk",
    "category": "DP",
    "isActive": true
}

```

Creates a new security role security function.

##### Arguments

* functionId (required) - The Function Id
* isActive (required) - The Active bit

##### Returns

Returns a security role security function object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a security role security function

```
DEFINITION
GET http://apiserver/securityroles/:id/securityfunctions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/securityroles/:id/securityfunctions/86");

EXAMPLE RESPONSE
{
    "id": "86",
    "roleId": "DEO",
    "functionId": "DEC",
    "description": "Data Entry Clerk",
    "category": "DP",
    "isActive": true
}

```

Retrieves the details of an existing security role security function. You need only supply the id.

##### Arguments

* id (required) - The id of the security role security function to be retrieved.

#### Update a security role security function

```
DEFINITION
POST http://apiserver/securityroles/:id/securityfunctions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/securityroles/59/securityfunctions/86", {
    "functionId": "DEC",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "86",
    "roleId": "DEO",
    "functionId": "DEC",
    "description": "Data Entry Clerk",
    "category": "DP",
    "isActive": true
}


```

Updates the specified security role security function by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* functionId () - The Function Id
* isActive () - The Active bit

##### Returns

Returns the security role security function object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a security role security function

```
DEFINITION
DELETE http://apiserver/securityroles/:id/securityfunctions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/securityroles/:id/securityfunctions/86", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a security role security function. It cannot be undone.

##### Arguments

* id (required) - The id of the security role security functions to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the security role security function does not exist, this call returns an error.

#### List all security role security functions

```
DEFINITION
GET http://apiserver/securityroles/:id/securityfunctions

EXAMPLE REQUEST
$.get("http://localhost:49195/securityroles/59/securityfunctions?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "86",
            "roleId": "DEO",
            "functionId": "DEC",
            "description": "Data Entry Clerk",
            "category": "DP",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all security role security functions.

##### Arguments

* roleId (required) - The Role Id

##### Returns

A dictionary with an items property that contains an array of up to limit security role security functions, starting at index offset. Each entry in the array is a separate security role security function object. If no more security role security functions are available, the resulting array will be empty. This request should never return an error.

### Security Role Module Configurations

#### Create a security role module configuration

```
DEFINITION
POST http://apiserver/securityroles/:id/moduleconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/securityroles/59/moduleconfigurations", {
    "moduleId": "77",
    "sequenceNumber": 5,
    "isDefault": true
});

EXAMPLE RESPONSE
{
    "id": "10100",
    "moduleId": "77",
    "sequenceNumber": 5,
    "isDefault": true
}

```

Creates a new security role module configuration.

##### Arguments

* moduleId (required) - The Module Id
* sequenceNumber (required) - The Sequence Number
* isDefault (required) - The Default bit

##### Returns

Returns a security role module configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a security role module configuration

```
DEFINITION
GET http://apiserver/securityroles/:id/moduleconfiguration/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/securityroles/59/moduleconfiguration/10100");

EXAMPLE RESPONSE
{
    "id": "10100",
    "moduleId": "77",
    "sequenceNumber": 5,
    "isDefault": true
}

```

Retrieves the details of an existing security role module configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the security role module configuration to be retrieved.

#### Update a security role module configuration

```
DEFINITION
POST http://apiserver/securityroles/:id/moduleconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/securityroles/59/moduleconfigurations/10100", {
    "moduleId": "77",
    "sequenceNumber": 5,
    "isDefault": true
});

EXAMPLE RESPONSE
{
    "id": "10100",
    "moduleId": "77",
    "sequenceNumber": 5,
    "isDefault": true
}


```

Updates the specified security role module configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* moduleId () - The Module Id
* sequenceNumber () - The Sequence Number
* isDefault () - The Default bit

##### Returns

Returns the security role module configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a security role module configuration

```
DEFINITION
DELETE http://apiserver/securityroles/:id/moduleconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/securityroles/59/moduleconfigurations/10100", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a security role module configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the security role module configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the security role module configuration does not exist, this call returns an error.

#### List all security role module configurations

```
DEFINITION
GET http://apiserver/securityroles/:id/moduleconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/securityroles/59/moduleconfigurations?");

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
            "moduleId": "77",
            "sequenceNumber": 5,
            "isDefault": true
        },
        {...},
    ]
}

```

Returns a list of all security role module configurations.

##### Arguments

* securityRoleId (required) - The Security Role Id to look for it's modules

##### Returns

A dictionary with an items property that contains an array of up to limit security role module configurations, starting at index offset. Each entry in the array is a separate security role module configuration object. If no more security role module configurations are available, the resulting array will be empty. This request should never return an error.

### Sessions

#### Create a session

```
DEFINITION
POST http://apiserver/sessions

EXAMPLE REQUEST
$.post("http://localhost:49195/sessions", {
    "environment": "USPROD"
});

EXAMPLE RESPONSE
{
    "SAWs": [
        "CAT10ACC",
        "AAT10ALK",
        "AAT11ARV",
        ...
    ],
    "accessor": 6647,
    "role": "DDCSTAFF",
    "impersonationToken": null
}

```

In order to use the API, you need to first create a session by sending a valid environment identifier to the sessions endpoint via the `POST` method. The response will contain a list of the SAWs available to the user through the user's role as well as the user's accessor and role. If no environment identifier is sent, the user's default environment is used.

##### Arguments

* environment (optional) - The environment id to use when creating the session. If not specified, will use the default environment for the user. If the current user does not have a default environment ancd no environment id is specified, an error will be retured.
* userAcount (optional) - The impersonator's StudioEnterprise account number. If specified, there will be an impersonation token generated for the user for use, but only if the user is authorized. If not specified, it will not return a separate token, and a session for the active directory user will be opened instead.

#### Delete a session

```
DEFINITION
DELETE http://apiserver/sessions

EXAMPLE REQUEST
$.ajax("http://localhost:49195/sessions", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Deletes any active sessions for the current user.

#### List all sessions

```
DEFINITION
GET http://apiserver/sessions

EXAMPLE REQUEST
$.get("http://localhost:49195/sessions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "USPROD",
            "description": "Dev local Environment",
            "isDefault": false
        }
    ]
}

```

Returns a list of active sessions for the current user.

##### Returns

A dictionary with an items property that contains an array of session objects. Each entry in the array is a session object. If the current user does not have any active sessions, the items array will be empty. This request should never return an error.

### Special Security Configurations

#### Create a special security configuration

```
DEFINITION
POST http://apiserver/specialsecurityconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/specialsecurityconfigurations", {
    "specialSecurityId": "VLIST",
    "type": "SPECIAL",
    "valueLow": "MD1",
    "valueHigh": "PL"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "specialSecurityId": "VLIST",
    "type": "SPECIAL",
    "valueLow": "MD1",
    "valueHigh": "PL"
}

```

Creates a new special security configuration.

##### Arguments

* specialSecurityId (required) - Special Security Id
* type (required) - Special Security Type
* valueLow (required) - Low Value Limit for Special Security Type Values
* valueHigh (required) - High Value Limit for Special Security Type Values

##### Returns

Returns a special security configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a special security configuration

```
DEFINITION
GET http://apiserver/specialsecurityconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/specialsecurityconfigurations/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "specialSecurityId": "VLIST",
    "type": "SPECIAL",
    "valueLow": "MD1",
    "valueHigh": "PL"
}

```

Retrieves the details of an existing special security configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the special security configuration to be retrieved.

#### Update a special security configuration

```
DEFINITION
POST http://apiserver/specialsecurityconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/specialsecurityconfigurations/9", {
    "specialSecurityId": "VLIST",
    "type": "SPECIAL",
    "valueLow": "MD1",
    "valueHigh": "PL"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "specialSecurityId": "VLIST",
    "type": "SPECIAL",
    "valueLow": "MD1",
    "valueHigh": "PL"
}


```

Updates the specified special security configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* specialSecurityId () - Special Security Id
* type () - Special Security Type
* valueLow () - Low Value Limit for Special Security Type Values
* valueHigh () - High Value Limit for Special Security Type Values

##### Returns

Returns the special security configuration object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a special security configuration

```
DEFINITION
DELETE http://apiserver/specialsecurityconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/specialsecurityconfigurations/9", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a special security configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the special security configuration to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the special security configuration does not exist, this call returns an error.

#### List all special security configurations

```
DEFINITION
GET http://apiserver/specialsecurityconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/specialsecurityconfigurations?");

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
    "specialSecurityId": "VLIST",
    "type": "SPECIAL",
    "valueLow": "MD1",
    "valueHigh": "PL"
        },
        {...},
    ]
}

```

Returns a list of all special security configurations.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* type () - Special Security Type
* valueHigh () - Value for Special Security Type Values

##### Returns

A dictionary with an items property that contains an array of up to limit special security configurations, starting at index offset. Each entry in the array is a separate special security configuration object. If no more special security configurations are available, the resulting array will be empty. This request should never return an error.

### Special Security Configuration Privileges

#### Create a special security configuration privilege

```
DEFINITION
POST http://apiserver/specialsecurityconfigurations/:id/privileges

EXAMPLE REQUEST
$.post("http://localhost:49195/specialsecurityconfigurations/12/privileges", {
    "role": "ADMINISTRATOR",
    "accountPrivilege": "Y",
    "transactionPrivilege": "Y",
    "contactInfoPrivilege": "Y"
});

EXAMPLE RESPONSE
{
    "id": "17",
    "specialSecurity": "ADMIN",
    "role": "ADMINISTRATOR",
    "roleDescription": "Used for Administration",
    "accountPrivilege": "Y",
    "transactionPrivilege": "Y",
    "contactInfoPrivilege": "Y"
}

```

Creates a new special security configuration privilege.

##### Arguments

* role (required) - Security Role Id
* accountPrivilege (required) - Account Privilege Indicator
* transacionPrivilege (required) - Transaction Privilege Indicator
* contactInfoPrivilege () - Contact Information Privilege Indicator

##### Returns

Returns a special security configuration privilege object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a special security configuration privilege

```
DEFINITION
GET http://apiserver/specialsecurityconfigurations/:id/privileges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/specialsecurityconfigurations/12/privileges/17");

EXAMPLE RESPONSE
{
    "id": "17",
    "specialSecurity": "ADMIN",
    "role": "ADMINISTRATOR",
    "roleDescription": "Used for Administration",
    "accountPrivilege": "Y",
    "transactionPrivilege": "Y",
    "contactInfoPrivilege": "Y"
}

```

Retrieves the details of an existing special security configuration privilege. You need only supply the id.

##### Arguments

* id (required) - The id of the special security configuration privilege to be retrieved.

#### Update a special security configuration privilege

```
DEFINITION
POST http://apiserver/specialsecurityconfigurations/:id/privileges/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/specialsecurityconfigurations/12/privileges/17", {
    "specialSecurity": "ADMIN",
    "role": "ADMINISTRATOR",
    "accountPrivilege": "Y",
    "transactionPrivilege": "Y",
    "contactInfoPrivilege": "Y"
});

EXAMPLE RESPONSE
{
    "id": "17",
    "specialSecurity": "ADMIN",
    "role": "ADMINISTRATOR",
    "roleDescription": "Used for Administration",
    "accountPrivilege": "Y",
    "transactionPrivilege": "Y",
    "contactInfoPrivilege": "Y"
}


```

Updates the specified special security configuration privilege by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* role () - Security Role Id
* accountPrivilege () - Account Privilege Indicator
* transacionPrivilege () - Transaction Privilege Indicator
* contactInfoPrivilege () - Contact Information Privilege Indicator

##### Returns

Returns the special security configuration privilege object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a special security configuration privilege

```
DEFINITION
DELETE http://apiserver/specialsecurityconfigurations/:id/privileges/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/specialsecurityconfigurations/12/privileges/17", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a special security configuration privilege. It cannot be undone.

##### Arguments

* id (required) - The id of the special security configuration privilege to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the special security configuration does not exist, this call returns an error.

#### List all special security configuration privileges

```
DEFINITION
GET http://apiserver/specialsecurityconfigurations/:id/privileges

EXAMPLE REQUEST
$.get("http://localhost:49195/specialsecurityconfigurations/12/privileges?");

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
            "specialSecurity": "ADMIN",
            "role": "ADMINISTRATOR",
            "roleDescription": "Used for Administration",
            "accountPrivilege": "Y",
            "transactionPrivilege": "Y",
            "contactInfoPrivilege": "Y"
        },
        {...},
    ]
}

```

Returns a list of all special security configuration privileges.

##### Returns

A dictionary with an items property that contains an array of up to limit special security configuration privileges, starting at index offset. Each entry in the array is a separate special security configuration privilege object. If no more special security configuration privileges are available, the resulting array will be empty. This request should never return an error.

### Users

#### Create a user

```
DEFINITION
POST http://apiserver/users

EXAMPLE REQUEST
$.post("http://localhost:49195/users", {
    "userId": "ddc\\jdoe",
    "description": "John Doe",
    "emailAddress": "johndoe@donordirect.com",
    "category": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "20238",
    "userId": "ddc\\jdoe",
    "description": "John Doe",
    "emailAddress": "johndoe@donordirect.com",
    "category": "DDC",
    "isActive": true
}

```

Creates a new user.

##### Arguments

* userId (required) - user domain id
* description (required) - user name or description
* emailAddress (required) - email address
* category (required) - user category
* isActive (optional; default `true`) - specifies if user is active

##### Returns

Returns a user object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a user

```
DEFINITION
GET http://apiserver/users/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/users/20238");

EXAMPLE RESPONSE
{
    "id": "20238",
    "userId": "ddc\\jdoe",
    "description": "John Doe",
    "emailAddress": "johndoe@donordirect.com",
    "category": "DDC",
    "isActive": true
}

```

Retrieves the details of an existing user. You need only supply the id.

##### Arguments

* id (required) - The id of the user to be retrieved.

#### Update a user

```
DEFINITION
POST http://apiserver/sers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/sers/20238", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "20238",
    "userId": "ddc\\jdoe",
    "description": "John Doe",
    "emailAddress": "johndoe@donordirect.com",
    "category": "DDC",
    "isActive": false
}


```

Updates the specified user by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* userId (optional) - user domain id
* description (optional) - user name or description
* emailAddress (optional) - email address
* category (optional) - user category
* isActive (optional) - specifies if user is active

##### Returns

Returns the user object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a user

```
DEFINITION
DELETE http://apiserver/users/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/users/20238", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a user. It cannot be undone.

##### Arguments

* id (required) - The id of the user to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the user does not exist, this call returns an error.

#### List all users

```
DEFINITION
GET http://apiserver/users

EXAMPLE REQUEST
$.get("http://localhost:49195/users?description=John");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "20238",
            "userId": "ddc\\jdoe",
            "description": "John Doe",
            "emailAddress": "johndoe@donordirect.com",
            "category": "DDC",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all users.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* userId
* description
* emailAddress
* category
* isActive

##### Returns

A dictionary with an items property that contains an array of up to limit users, starting at index offset. Each entry in the array is a separate user object. If no more users are available, the resulting array will be empty. This request should never return an error.