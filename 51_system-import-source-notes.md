# System Import Source Notes

#### Retrieve a system import source note

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/notes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "DDCNOTETYP",
    "shortComment": "Basic DDC Note",
    "longComment": "Basic DDC note content."
}

```

Retrieves the details of an existing system import source note. You need only supply the id.

##### Arguments

* id (required) - The id of the system import source note to be retrieved.

#### Update a system import source note

```
DEFINITION
POST http://apiserver/systemimports/:importId/sources/:sourceId/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/sources/40812571/notes/1", {
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

Updates the specified system import source note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the note type to update the source note with
* shortComment (optional) - the short comment to update the source note with
* longComment (optional) - the long comment to update the source note with

##### Returns

Returns the system import source note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import source note

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/sources/:sourceId/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/sources/40812571/notes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import source note. It cannot be undone.

##### Arguments

* id (required) - The id of the system import source note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import source note does not exist, this call returns an error.

#### List all system import source notes

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/notes");

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

Returns a list of all system import source notes.

##### Returns

A dictionary with an items property that contains an array of up to limit system import source notes, starting at index offset. Each entry in the array is a separate system import source note object. If no more system import source notes are available, the resulting array will be empty. This request should never return an error.