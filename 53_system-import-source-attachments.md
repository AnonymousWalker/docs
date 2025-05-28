# System Import Source Attachments

#### Retrieve a system import source attachment

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/attachments/49");

EXAMPLE RESPONSE
{
    "id": "49",
    "type": "IMAGE",
    "url": "\\networkshare123\logo64.png",
    "uploadFile": true,
    "fileName": "logo64.png",
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing system import source attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the attachment to retrieve.

#### Update a system import source attachment

```
DEFINITION
POST http://apiserver/systemimports/:importId/sources/:sourceId/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/sources/40812571/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "id": "49",
    "type": "LOGO",
    "url": "\\networkshare123\logo64.png",
    "uploadFile": true,
    "fileName": "logo64.png",
    "fileMimeType": "image/png"
}

```

Updates the specified system import source attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type to upate the pledge attachment with
* url (optional) - The external document address to update the pledge attachment with
* fileName (optional) - the name of the uploaded file.
* uploadFile (optional) - specifies whether or not the import process should upload the file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the system import source attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import source attachment

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/sources/:sourceId/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/sources/40812571/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import source attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the system import source attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import source attachment does not exist, this call returns an error.

#### List all system import source attachments

```
DEFINITION
GET http://apiserver/systemimports/:importId/sources/:sourceId/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/sources/40812571/attachments?");

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
            "type": "LOGO",
            "url": "\\networkshare123\logo64.png",
            "uploadFile": true,
            "fileName": "logo64.png",
            "fileMimeType": "image/png"
        },
        {...},
    ]
}

```

Returns a list of all system import source attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit system import source attachments, starting at index offset. Each entry in the array is a separate system import source attachment object. If no more system import source attachments are available, the resulting array will be empty. This request should never return an error.