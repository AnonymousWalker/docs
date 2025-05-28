# Subscription Notes

#### Create a subscription note

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/notes", {
    "type": "SOSBSTITLE",
    "shortComment": "Little Explorers"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "SOSBSTITLE",
    "typeDescription": "SO Subscription Title",
    "shortComment": "Little Explorers",
    "longComment": null
}

```

Creates a new subscription note.

##### Arguments

* type (required) - the note type to create the subscription note with
* shortComment (optional) - the short comment to create the subscription note with
* longComment (optional) - the long comment to create the subscription note with

##### Returns

Returns a subscription note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription note

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/notes/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "SOSBSTITLE",
    "typeDescription": "SO Subscription Title",
    "shortComment": "Little Explorers",
    "longComment": null
}

```

Retrieves the details of an existing subscription note. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription note to be retrieved.

#### Update a subscription note

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/:subscriptionCode/notes/6", {
    "shortComment": "Little Explorers Publications"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "SOSBSTITLE",
    "typeDescription": "SO Subscription Title",
    "shortComment": "Little Explorers Publications",
    "longComment": null
}

```

Updates the specified subscription note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the type to update the subscription note with
* shortComment (optional) - the short comment to update the subscription note with
* longComment (optional) - the long comment to update the subscription note with

##### Returns

Returns the subscription note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription note

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/notes/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription note. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription note does not exist, this call returns an error.

#### List all subscription notes

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "6",
            "type": "SOSBSTITLE",
            "typeDescription": "SO Subscription Title",
            "shortComment": "Little Explorers",
            "longComment": null
        },
        {...},
    ]
}

```

Returns a list of all subscription notes.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription notes, starting at index offset. Each entry in the array is a separate subscription note object. If no more subscription notes are available, the resulting array will be empty. This request should never return an error.