# Subscription Dates

#### Create a subscription date

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/dates", {
    "type": "SBDATE",
    "value": "2011-07-25",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "SBDATE",
    "typeDescription": "Subscription Begin Date",
    "value": "2011-07-25",
    "isActive": true
}

```

Creates a new subscription date.

##### Arguments

* type (required) - the date type to create the subscription date with
* value (required) - the date value to create the subscription date with
* isActive (optional: defaults to true) - is the subscription date active

##### Returns

Returns a subscription date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription date

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/dates/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "SBDATE",
    "typeDescription": "Subscription Begin Date",
    "value": "2011-07-25",
    "isActive": true
}

```

Retrieves the details of an existing subscription date. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription date to be retrieved.

#### Update a subscription date

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/dates/8", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "SBDATE",
    "typeDescription": "Subscription Begin Date",
    "value": "2011-07-25",
    "isActive": false
}

```

Updates the specified subscription date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the date type to update the subscription date with
* value (optional) - the date value to update the subscription date with
* isActive (optional) - is the subscription date active

##### Returns

Returns the subscription date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription date

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/dates/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription date. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription date does not exist, this call returns an error.

#### List all subscription dates

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/:subscriptionCode/dates?");

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
            "type": "SBDATE",
            "typeDescription": "Subscription Begin Date",
            "value": "2011-07-25",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all subscription dates.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription dates, starting at index offset. Each entry in the array is a separate subscription date object. If no more subscription dates are available, the resulting array will be empty. This request should never return an error.

### Subscription Images

#### Create a subscription image

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionId/images

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/MBPRIME/images", {
    "imageType": "IMAGEXS",
    "description": "Xtra Small Subs Img",
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
    "description": "Xtra Small Subs Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Creates a new subscription image.

##### Arguments

* imageType (required) - the ImageType code value for the subscription image.
* description (optional) - the description for the subscription image.
* imageUrl (required) - the image URL for the subscription image.
* alternateText (optional) - the alternate text for the subscription image.
* title (optional) - the image title for the subscription image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns a subscription image object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription image

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionId/images/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/MBRPRIME/images/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Subs Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Retrieves the details of an existing subscription image. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription image to be retrieved.

#### Update a subscription image

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionId/images/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/MBRPRIME/images/6", {
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Xtra Small Subs Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}


```

Updates the specified subscription image by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* imageType (optional) - the ImageType code value to update for the subscription image.
* description (optional) - the description to update for the subscription image.
* imageUrl (optional) - the image URL to update for the subscription image.
* alternateText (optional) - the alternate text to update for the subscription image.
* title (optional) - the image title to update for the subscription image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns the subscription image object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription image

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionId/images/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/MBRPRIME/images/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription image. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription image to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription image does not exist, this call returns an error.

#### List all subscription images

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionId/images

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/MBRPRIME/images");

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
            "description": "Xtra Small Subs Img",
            "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
            "alternateText": "Image Alt Text",
            "title": "Image Title",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all subscription images by subscription code.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription images, starting at index offset. Each entry in the array is a separate subscription image object. If no more subscription images are available, the resulting array will be empty. This request should never return an error.