# Subscription Attachments

#### Create a subscription attachment

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "8",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new subscription attachment.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns asubscription attachment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription attachment

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/attachments/8");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "8",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing subscription attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the media network attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

#### Update a subscription attachment

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/attachments/8", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "8",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified subscription attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the subscription attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription attachment

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/attachments/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription attachment does not exist, this call returns an error.

#### List all subscription attachments

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/attachments");

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
            "id": "8",
            "type": "OTHER",
            "typeDescription": "Other",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
    ]
}

```

Returns a list of all subscription attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription attachments, starting at index offset. Each entry in the array is a separate subscription attachment object. If no more subscription attachments are available, the resulting array will be empty. This request should never return an error.

### Subscription Prices

#### Create a subscription price

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/prices

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/prices", {
    "id": "2YR",
    "price": 15,
    "numberOfIssues": 12
});

EXAMPLE RESPONSE
{
    "id": "2YR",
    "description": "2 Year Price",
    "price": 15,
    "numberOfIssues": 12,
    "start": null,
    "end": null,
    "isActive": true,
    "useInStudioOnline": false,
    "defaultRenewalPriceCode": null,
    "defaultRenewalPriceCodeDescription": null,
    "title": null,
    "additionalDescription1": null,
    "additionalDescription2": null,
    "additionalDescription3": null,
    "additionalDescription4": null
}

```

Creates a new subscription price.

##### Arguments

* id (required) - the price code to create the subscription price with
* price (required) - the price value to create the subscription price with
* numberOfIssues (optional) - the number of issues to create the subscription price with
* start (optional) - the start date to create the subscription price with
* end (optional) - the end date to create the subscription price with
* isActive (optional) - is the subscription price active
* useInStudioOnline (optional) - is the subscription price used in StudioOnline
* defaultRenewalPriceCode (optional) - If subscription is type Membership, this value is used when performing auto-renewal. This value must be a valid price code for the current subscription code.

##### Returns

Returns a subscription price object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription price

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/prices/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/prices/1YR");

EXAMPLE RESPONSE
{
    "id": "1YR",
    "description": "1 Year Price",
    "price": 10,
    "numberOfIssues": 12,
    "start": "2014-07-29",
    "end": "2099-07-29",
    "isActive": true,
    "defaultRenewalPriceCode": null,
    "defaultRenewalPriceCodeDescription": null,
    "title": null,
    "additionalDescription1": null,
    "additionalDescription2": null,
    "additionalDescription3": null,
    "additionalDescription4": null
}

```

Retrieves the details of an existing subscription price. You need only supply the price code.

##### Arguments

* id (required) - The price code of the subscription price to retrieve.

##### Returns

Returns a subscription price object if a valid id was provided.

#### Update a subscription price

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/prices/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/prices/2YR", {
    "price": 20,
    "end": "2015-12-31"
});

EXAMPLE RESPONSE
{
    "id": "2YR",
    "description": "2 Year Price",
    "price": 20,
    "numberOfIssues": 12,
    "start": null,
    "end": "2015-12-31",
    "isActive": true,
    "useInStudioOnline": false,
    "defaultRenewalPriceCode": null,
    "defaultRenewalPriceCodeDescription": null,
    "title": null,
    "additionalDescription1": null,
    "additionalDescription2": null,
    "additionalDescription3": null,
    "additionalDescription4": null
}

```

Updates the specified subscription price by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - the price code to update the subscription price with
* price (optional) - the price value to update the subscription price with
* numberOfIssues (optional) - the number of issues to update the subscription price with
* start (optional) - the start date to update the subscription price with
* end (optional) - the end date to update the subscription price with
* isActive (optional) - is the subscription price active
* useInStudioOnline (optional) - is the subscription price used in StudioOnline
* defaultRenewalPriceCode (optional) - If subscription is type Membership, this value is used when performing auto-renewal. This value must be a valid price code for the current subscription code.

##### Returns

Returns the subscription price object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription price

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/prices/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/prices/1YR", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription price. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription price to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription price does not exist, this call returns an error.

#### List all subscription prices

```
DEFINITION
GET http://apiserver/subscriptions/:id/prices

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/prices");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "2YR",
            "description": "2 Year Price",
            "price": 20,
            "numberOfIssues": 12,
            "start": null,
            "end": "2015-12-31",
            "isActive": true,
            "useInStudioOnline": false,
            "defaultRenewalPriceCode": null,
            "defaultRenewalPriceCodeDescription": null,
            "title": null,
            "additionalDescription1": null,
            "additionalDescription2": null,
            "additionalDescription3": null,
            "additionalDescription4": null
        },
        {...},
    ]
}

```

Returns a list of all subscription prices.

##### Arguments

* forSubscriptionEntry () - `forSubscriptionEntry=true` filters the list of prices to only the prices which are valid for subscription entry

##### Returns

A dictionary with an items property that contains an array of up to limit subscription prices, starting at index offset. Each entry in the array is a separate subscription price object. If no more subscription prices are available, the resulting array will be empty. This request should never return an error.