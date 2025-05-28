# System Import Data Type Detail

#### Retrieve a system import data type detail

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:id/detail

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/detail");

EXAMPLE RESPONSE
{
    "description": "Favorite Ice Cream",
    "displaySequence": 15,
    "isSecurityRequired": false,
    "labelDescription": "Favorite Ice Cream Value",
    "isUserDefined": true,
    "isActive": true,
    "dataType": "X06",
    "category": "ACCOUNT",
    "isFamilyCode": false,
    "accountTypeRequired": "ALL",
    "isSingleValueOnly": true
}

```

Retrieves the details of an existing system import data type detail. You need only supply the id.

##### Arguments

* id (required) - The id of the system import data type detail to be retrieved.

##### Returns

Returns the system import data type detail object is the call succeeds. If there is no data type detail defined, this call will return an error.

#### Update a system import data type detail

```
DEFINITION
POST http://apiserver/systemimports/:importId/datatypes/:id/detail

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/datatypes/40812571/detail", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "description": "Favorite Ice Cream",
    "displaySequence": 15,
    "isSecurityRequired": false,
    "labelDescription": "Favorite Ice Cream Value",
    "isUserDefined": true,
    "isActive": false,
    "dataType": "X06",
    "category": "ACCOUNT",
    "isFamilyCode": false,
    "accountTypeRequired": "ALL",
    "isSingleValueOnly": true
}

```

Updates the specified system import data type detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* dataType (optional) - the data type value to update the data type with
* category (optional) - the category value to update the data type with
* accountTypeRequired (optional) - the account type(s) the data type is required for
* description (optional) - the description value to update the data type with
* isActive (optional) - is the data type active?
* isFamilyCode (optional) - is the data type a family code?
* isUserDefined (optional) - is the data type user-defined?
* displaySequence (optional) - the display sequence to update the data type with
* labelDescription (optional) - the label description to update the data type with
* isSingleValueOnly (optional) - is the data type a single-value type?
* isSecurityRequired (optional) - does the data type require special security?

##### Returns

Returns the system import data type detail object if the update succeeded. Returns an error if update parameters are invalid.