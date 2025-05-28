# System Import Pledge Notes

#### Retrieve a system import pledge note

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/notes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "DDCNOTETYP",
    "shortComment": "Basic DDC Note",
    "longComment": "Basic DDC note content."
}

```

Retrieves the details of an existing system import pledge note. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge note to be retrieved.

#### Update a system import pledge note

```
DEFINITION
POST http://apiserver/systemimports/:importId/pledges/:pledgeId/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/pledges/40812571/notes/1", {
    "shortComment": "Advanced DDC Note"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "DDCNOTETYP",
    "shortComment": "Advanced DDC Note",
    "longComment": "Basic DDC note content."
}

```

Updates the specified system import pledge note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the note type to update the pledge note with
* shortComment (optional) - the short comment to update the pledge note with
* longComment (optional) - the long comment to update the pledge note with

##### Returns

Returns the system import pledge note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import pledge note

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/pledges/:pledgeId/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/pledges/40812571/notes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import pledge note. It cannot be undone.

##### Arguments

* id (required) - The id of the system import pledge note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import pledge note does not exist, this call returns an error.

#### List all system import pledge notes

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:pledgeId/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/notes");

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
            "type": "DDCNOTETYP",
            "shortComment": "Basic DDC Note",
            "longComment": "Basic DDC note content."
        },
        {...},
    ]
}

```

Returns a list of all system import pledge notes.

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledge notes, starting at index offset. Each entry in the array is a separate system import pledge note object. If no more system import pledge notes are available, the resulting array will be empty. This request should never return an error.