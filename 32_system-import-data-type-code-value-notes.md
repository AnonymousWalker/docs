# System Import Data Type Code Value Notes

#### Retrieve a system import data type code value note

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevaluenotes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevaluenotes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "codeValue": "DONOR",
    "type": "DONORALERT",
    "shortComment": "Major Donor",
    "longComment": "This is a major donor."
}

```

Retrieves the details of an existing system import data type code value note. You need only supply the id.

##### Arguments

* id (required) - The id of the system import data type code value note to be retrieved.

#### Update a system import data type code value note

```
DEFINITION
POST http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevaluenotes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevaluenotes/1", {
    "shortComment": "Major Donor Notice"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "codeValue": "DONOR",
    "type": "DONORALERT",
    "shortComment": "Major Donor Notice",
    "longComment": "This is a major donor."
}

```

Updates the specified system import data type code value note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* codeValue (optional) - the new code value
* type (optional) - the new note type
* shortComment (optional) - the new note short comment
* longComment (optional) - the new note long comment

##### Returns

Returns the system import data type code value note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import data type code value note

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/dataTypes/:dataTypeId/codevaluenotes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevaluenotes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import data type code value note. It cannot be undone.

##### Arguments

* id (required) - The id of the system import data type code value note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import data type code value note does not exist, this call returns an error.

#### List all system import data type code value notes

```
DEFINITION
GET http://apiserver/systemimports/:importId/datatypes/:dataTypeId/codevaluenotes

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/datatypes/40812571/codevaluenotes");

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
            "type": "DONORALERT",
            "shortComment": "Major Donor",
            "longComment": "This is a major donor."
        },
        {...},
    ]
}

```

Returns a list of all system import data type code value notes.

##### Returns

A dictionary with an items property that contains an array of up to limit system import data type code value notes, starting at index offset. Each entry in the array is a separate system import data type code value note object. If no more system import data type code value notes are available, the resulting array will be empty. This request should never return an error.