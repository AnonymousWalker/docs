# System Import Data Type Code Value Attributes

#### Retrieve a system import data type code value attribute

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevalueattributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalueattributes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "codeValue": "DONOR",
    "oldType": "OLDATTRTYPE",
    "oldValue": "OLDLATTRVAL",
    "newType": "NEWATTRTYPE",
    "newValue": "NEWATTRVAL",
    "description": "New Value Description"
}

```

Retrieves the details of an existing system import data type code value attribute. You need only supply the id.

##### Arguments

* id (required) - The id of the system import data type code value attribute to be retrieved.

#### Update a system import data type code value attribute

```
DEFINITION
POST http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevalueattributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalueattributes/1", {
    "shortComment": "New Import Value Description"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "codeValue": "DONOR",
    "oldType": "OLDATTRTYPE",
    "oldValue": "OLDLATTRVAL",
    "newType": "NEWATTRTYPE",
    "newValue": "NEWATTRVAL",
    "description": "New Import Value Description"
}

```

Updates the specified system import data type code value attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* codeValue (optional) - the new code value
* oldType (optional) - the old attribute type
* oldValue (optional) - the old attribute value
* newType (optional) - the new attribute type
* newValue (optional) - the new attribute value
* description (optional) - the new attribute description

##### Returns

Returns the system import data type code value attribute object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import data type code value attribute

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/dataTypes/:dataTypeId/codevalueattributes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalueattributes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import data type code value attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the system import data type code value attribute to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import data type code value attribute does not exist, this call returns an error.

#### List all system import data type code value attributes

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevalueattributes

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevalueattributes");

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
            "codeValue": "DONOR",
            "oldType": "OLDATTRTYPE",
            "oldValue": "OLDLATTRVAL",
            "newType": "NEWATTRTYPE",
            "newValue": "NEWATTRVAL",
            "description": "New Value Description"
        },
        {...},
    ]
}

```

Returns a list of all system import data type code value attributes.

##### Returns

A dictionary with an items property that contains an array of up to limit system import data type code value attributes, starting at index offset. Each entry in the array is a separate system import data type code value attribute object. If no more system import data type code value attributes are available, the resulting array will be empty. This request should never return an error.