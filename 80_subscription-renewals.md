# Subscription Renewals

#### Create a subscription renewal

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/renewals

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/renewals", {
    "renewalCode": "R1215",
    "description": "Renewal - 12/15",
    "numberRemaining": 2,
    "mailTo": "S",
    "methodOfDelivery": "EMAIL",
    "source": "WEBS",
    "product": null,
    "letterCode": "2010YREND",
    "runId": null
});

EXAMPLE RESPONSE
{
    "id": "33",
    "renewalCode": "R1215",
    "description": "Renewal - 12/15",
    "numberRemaining": 2,
    "mailTo": "S",
    "methodOfDelivery": "EMAIL",
    "source": "WEBS",
    "sourceDescription": "Sage Website",
    "product": null,
    "letterCode": "2010YREND",
    "letterCodeDescription": "2010 Periodic Receipt",
    "runId": null
}

```

Creates a new subscription renewal.

##### Arguments

* renewalCode (required) - the renewal code to create the subscription renewal with
* description (required) - the renewal description to create the subscription renewal with
* numberRemaining (required) - the number of renewals remaining to create the subscription renewal with
* mailTo (required) - the mail to recipient to create the subscription renewal with
* methodOfDelivery (required) - the delivery method to create the subscription renewal with
* source (required) - the source code to create the subscription renewal with
* product (optional) - the product code to create the subscription renewal with
* letterCode (required) - the letter code to create the subscription renewal with
* runId (optional) - the renewal run id to create the subscription renewal with

##### Returns

Returns a subscription renewal object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription renewal

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/renewals/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/renewals/33");

EXAMPLE RESPONSE
{
    "id": "33",
    "renewalCode": "R1215",
    "description": "Renewal - 12/15",
    "numberRemaining": 2,
    "mailTo": "S",
    "methodOfDelivery": "EMAIL",
    "source": "WEBS",
    "sourceDescription": "Sage Website",
    "product": null,
    "letterCode": "2010YREND",
    "letterCodeDescription": "2010 Periodic Receipt",
    "runId": null
}

```

Retrieves the details of an existing subscription renewal. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription renewal to be retrieved.

#### Update a subscription renewal

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/renewals/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/renewals/33", {
    "description": "Renewal for Dec 2015"
});

EXAMPLE RESPONSE
{
    "id": "33",
    "renewalCode": "R1215",
    "description": "Renewal for Dec 2015",
    "numberRemaining": 2,
    "mailTo": "S",
    "methodOfDelivery": "EMAIL",
    "source": "WEBS",
    "sourceDescription": "Sage Website",
    "product": null,
    "letterCode": "2010YREND",
    "letterCodeDescription": "2010 Periodic Receipt",
    "runId": null
}

```

Updates the specified subscription renewal by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* renewalCode (optional) - the renewal code to update the subscription renewal with
* description (optional) - the renewal description to update the subscription renewal with
* numberRemaining (optional) - the number of renewals remaining to update the subscription renewal with
* mailTo (optional) - the mail to recipient to update the subscription renewal with
* methodOfDelivery (optional) - the delivery method to update the subscription renewal with
* source (optional) - the source code to update the subscription renewal with
* product (optional) - the product code to update the subscription renewal with
* letterCode (optional) - the letter code to update the subscription renewal with
* runId (optional) - the renewal run id to update the subscription renewal with

##### Returns

Returns the subscription renewal object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription renewal

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/renewals/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/renewals/33", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription renewal. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription renewal to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription renewal does not exist, this call returns an error.

#### List all subscription renewals

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/renewals

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/renewals");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "33",
            "renewalCode": "R1215",
            "description": "Renewal for Dec 2015",
            "numberRemaining": 2,
            "mailTo": "S",
            "methodOfDelivery": "EMAIL",
            "source": "WEBS",
            "sourceDescription": "Sage Website",
            "product": null,
            "letterCode": "2010YREND",
            "letterCodeDescription": "2010 Periodic Receipt",
            "runId": null
        },
        {...},
    ]
}

```

Returns a list of all subscription renewals.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription renewals, starting at index offset. Each entry in the array is a separate subscription renewal object. If no more subscription renewals are available, the resulting array will be empty. This request should never return an error.

### Subscription Renewal Process

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/renewals/:id/process

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/renewals/33/process", {
    "job": "540",
    "segment": "1",
    "renewalDate": "2015-09-10"
});

EXAMPLE RESPONSE
204 No Content

```

Performs a subscription renewal process.

##### Arguments

* job (required) - the segmentation job number to use in the renewal process
* segment (required) - the segmentation segment number to use in the renewal process
* renewalDate (required) - the renewal run date to use in the renewal process

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.

### Subscription Fulfillment

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/fulfill

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/fulfill", {
    "issueCode": "2015MAY",
    "issueDate": "2015-04-12",
    "job": "540",
    "segment": "1",
    "company": "4",
    "source": "WEBS"
});

EXAMPLE RESPONSE
204 No Content

```

Performs a subscription renewal process.

##### Arguments

For subscriptions of type "M" (Magazine):

* issueCode (required) - the issue code to use for running the fulfillment process
* issueDate (required) - the issue date to use for running the fulfillment process
* job (required) - the segmentation job to use for running the fulfillment process
* segment (required) - the segment number to use for running the fulfillment process
* company (required) - the company code to use for running the fulfillment process
* source (required) - the source code to use for running the fulfillment process
* codeType (optional) - the code type to use for running the fulfillment process

For subscriptions of type "P" (Product):

* company (required) - the company code to use for running the fulfillment process
* currencyCode (required) - the currency code to use for running the fulfillment process
* warehouse (required) - the warehouse code to use for running the fulfillment process
* product (required) - the product code to use for running the fulfillment process
* priceCode (required) - the price code to use for running the fulfillment process
* source (required) - the source code to use for running the fulfillment process
* shipMethod (required) - the shipping method code to use for running the fulfillment process
* shouldCalculateTax (required) - should the fulfillment process calculate tax
* job (required) - the segmentation job to use for running the fulfillment process
* segment (required) - the segment number to use for running the fulfillment process

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.

### Subscription StudioOnline Publish Data

#### Retrieve the subscription StudioOnline publish data

```
DEFINITION
GET http://apiserver/subscriptions/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/studioonlinepublishdata");

EXAMPLE RESPONSE
{
    "subscriptionCode": "EXPLORERS",
    "id": "6459",
    "description": "Little Explorers",
    "summary": null,
    "extendedDescription": null,
    "isExtendedDescriptionLocked": false,
    "iconImage": null,
    "mediumImage": null,
    "keywords": null,
    "pageLayout": "SUBPACK1",
    "categories": null
}

```

Retrieves the details of the existing subscription StudioOnline publish data. You need only supply the subscription id.

##### Returns

Returns a subscription StudioOnline publish data object if a valid id was provided.

#### Update and publish the subscription StudioOnline publish data

```
DEFINITION
POST http://apiserver/subscriptions/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/studioonlinepublishdata", {
    "extendedDescription": "Extended Description",
});

EXAMPLE RESPONSE
{
    "subscriptionCode": "EXPLORERS",
    "id": "6459",
    "description": "Little Explorers",
    "summary": null,
    "extendedDescription": "Extended Description",
    "isExtendedDescriptionLocked": false,
    "iconImage": null,
    "mediumImage": null,
    "keywords": null,
    "pageLayout": "SUBPACK1"
}

```

Updates and publishes the specified subscription StudioOnline publish data by setting the values of the parameters passed. Any parameters not provided will be left unchanged. Any categories must already have been updated through the Event Codes resources. Any prices must already have been updated through their resources.

##### Arguments

* description (optional) - The description for the subscription on StudioOnline.
* summary (optional) - The summary for the subscription on StudioOnline.
* extendedDescription (optional) - The extended description for the subscription on StudioOnline.
* updateImages (optional) - Whether or not to update the icon and medium images. If this is selected and the icon or medium image are not provided, they will be deleted.
* iconImage (optional) - The icon image for the subscription on StudioOnline.
* mediumImage (optional) - The medium image for the subscription on StudioOnline.
* keywords (optional) - The keywords for the subscription on StudioOnline.
* pageLayout (optional) - The page layout (XML Package) for the subscription on StudioOnline.

##### Returns

Returns the subscription StudioOnline publish data object if the update and publish succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined page layout code).

#### Unpublish the subscription StudioOnline publish data

```
DEFINITION
DELETE http://apiserver/subscriptions/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/studioonlinepublishdata", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Unpublishes the subscription StudioOnline publish data. The actual data will not be deleted.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the subscription StudioOnline publish data cannot be unpublished, this call returns an error.

### Subscription Processing Runs

#### Retrieve a Subscription Processing Run

```
DEFINITION
GET http://apiserver/subscriptionprocessingruns/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptionprocessingruns/20015");

EXAMPLE RESPONSE
{
    "id": "20015",
    "previousRun": null,
    "nextRun": null,
    "type": "AUTORENEW",
    "typeDescription": "Auto-Renewal",
    "company": "PAYCONEX",
    "paymentGatewayCode": "CCONNECT",
    "paymentGatewayDescription": "Clover Connect",
    "runDate": "2020-06-19",
    "startDate": "2019-06-19T06:06:36 PM",
    "endDate": null,
    "processedCount": 0,
    "renewedCount": 0,
    "declinedCount": 0,
    "fulfilledCount": 0,
    "expiredCount": 0,
    "activatedCount": 0,
    "errorCount": 1,
    "accessor": "11800",
    "accessorDescription": "John Doe"
}

```

Retrieves the data of an existing Subscription Processing Run. You need only supply the id.

##### Arguments

* id (required) - The id of the Subscription Processing Run to be retrieved.

#### List all Subscription Processing Runs

```
DEFINITION
GET http://apiserver/subscriptionprocessingruns

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptionprocessingruns");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 33
    },
    "items": [
        {
            "id": "20035",
            "previousRun": "20016",
            "nextRun": null,
            "type": "AUTORENEW",
            "typeDescription": "Auto-Renewal",
            "company": "PAYCONEX",
            "paymentGatewayCode": "CCONNECT",
            "paymentGatewayDescription": "Clover Connect",
            "runDate": "2020-06-19",
            "startDate": "2019-06-27T11:26:40 AM",
            "endDate": "2019-06-27T11:26:42 AM",
            "processedCount": 0,
            "renewedCount": 0,
            "declinedCount": 0,
            "fulfilledCount": 0,
            "expiredCount": 0,
            "activatedCount": 0,
            "errorCount": 1,
            "accessor": "11806",
            "accessorDescription": "Jane Doe"
        },
        {
            "id": "20028",
            "previousRun": null,
            "nextRun": null,
            "type": "AUTORENEW",
            "typeDescription": "Auto-Renewal",
            "company": "PAYCONEX",
            "paymentGatewayCode": null,
            "paymentGatewayDescription": null,
            "runDate": "2020-06-27",
            "startDate": "2019-06-27T09:55:07 AM",
            "endDate": null,
            "processedCount": 0,
            "renewedCount": 0,
            "declinedCount": 0,
            "fulfilledCount": 0,
            "expiredCount": 0,
            "activatedCount": 0,
            "errorCount": 1,
            "accessor": "11800",
            "accessorDescription": "John Doe"
        },
        {
            "id": "20016",
            "previousRun": null,
            "nextRun": "20035",
            "type": "AUTORENEW",
            "typeDescription": "Auto-Renewal",
            "company": "PAYCONEX",
            "paymentGatewayCode": null,
            "paymentGatewayDescription": null,
            "runDate": "2020-06-19",
            "startDate": "2019-06-19T06:08:42 PM",
            "endDate": null,
            "processedCount": 0,
            "renewedCount": 0,
            "declinedCount": 0,
            "fulfilledCount": 0,
            "expiredCount": 0,
            "activatedCount": 0,
            "errorCount": 1,
            "accessor": "11800",
            "accessorDescription": "John Doe"
        }
    ]
}

```

Returns a list of all Subscription Processing Runs.

##### Returns

A dictionary with an items property that contains an array of up to limit Subscription Processing Runs, starting at index offset. Each entry in the array is a separate subscription processing run object. If no more Subscription Processing Runs are available, the resulting array will be empty. This request should never return an error.

### Subscription Processing Run Details

#### List all Subscription Processing Run Details

```
DEFINITION
GET http://apiserver/subscriptionprocessingruns/:id/details/

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptionprocessingruns/20032/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 2
    },
    "items": [
        {
            "id": "10096",
            "runId": "20032",
            "status": "E",
            "subscription": "1000001450",
            "subscriptionType": "M",
            "subscriptionTypeDescription": "Magazine",
            "subscriptionCode": "BWBMAG",
            "subscriptionCodeDescription": "BWB Magazine Test",
            "purchaserAccount": "45819",
            "purchaserName": "Braden Boettcher",
            "recipientAccount": "45819",
            "recipientName": "Braden Boettcher",
            "isRenewalNotificationSent": false,
            "isRenewed": false,
            "isDeclined": false,
            "isDeclineNotificationSent": false,
            "isFulfilled": false,
            "isExpired": false,
            "isActivated": false,
            "log": "Subscription (id: 1000001450) selected for sending an upcoming auto-renewal notification.\r\nAttempting to send upcoming auto-renewal notification...\r\nERROR: Subscription (code: BWBMAG) does not have a frequency with the attribute type: 'FREQNUMMON' specifying the number of months for that frequency. No notifaction or auto-renewal date could be found.\r\n"
        },
        {
            "id": "10097",
            "runId": "20032",
            "status": "P",
            "subscription": "1000001472",
            "subscriptionType": "M",
            "subscriptionTypeDescription": "Magazine",
            "subscriptionCode": "BWBMAGNTF",
            "subscriptionCodeDescription": "BWB Magazine With Notifications",
            "purchaserAccount": "30386",
            "purchaserName": "Tayna Duett",
            "recipientAccount": "30386",
            "recipientName": "Tayna Duett",
            "isRenewalNotificationSent": true,
            "isRenewed": false,
            "isDeclined": false,
            "isDeclineNotificationSent": false,
            "isFulfilled": false,
            "isExpired": false,
            "isActivated": false,
            "log": "Subscription (id: 1000001472) selected for sending an upcoming auto-renewal notification.\r\nAttempting to send upcoming auto-renewal notification...\r\nAttempting notification via email...\r\nReplacing email tokens...\r\nAdding communication for account: 30386...\r\nAttempting to send upcoming auto-renewal email...\r\nUpcoming auto-renewal email sent.\r\n"
        },
        {
            "id": "10098",
            "runId": "20032",
            "status": "Y",
            "subscription": "1000001473",
            "subscriptionType": "M",
            "subscriptionTypeDescription": "Magazine",
            "subscriptionCode": "BWBMAGNTF",
            "subscriptionCodeDescription": "BWB Magazine With Notifications",
            "purchaserAccount": "30386",
            "purchaserName": "Tayna Duett",
            "recipientAccount": "30386",
            "recipientName": "Tayna Duett",
            "isRenewalNotificationSent": false,
            "isRenewed": false,
            "isDeclined": false,
            "isDeclineNotificationSent": false,
            "isFulfilled": false,
            "isExpired": false,
            "isActivated": false,
            "log": "Subscription (id: 1000001473) selected for sending an upcoming auto-renewal notification.\r\n"
        }
    ]
}

```

Returns a list of all Subscription Processing Run Details in a given Run.

##### Arguments

* id (required) - The run id of the subscription processing run that the details are found in.

##### Returns

A dictionary with an items property that contains an array of up to limit Subscription Processing Run Details, starting at index offset. Each entry in the array is a separate subscription processing run detail object. If no more Subscription Processing Runs are available, the resulting array will be empty. This request should never return an error.

### Venue Attachments

#### Create a venue attachment

```
DEFINITION
POST http://apiserver/venues/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "9",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new venue attachment.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a venue attachment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a venue attachment

```
DEFINITION
GET http://apiserver/venues/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/attachments/9");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "9",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing venue attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the media network attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

#### Update a venue attachment

```
DEFINITION
POST http://apiserver/venues/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/attachments/9", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "9",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified venue attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the venue attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a venue attachment

```
DEFINITION
DELETE http://apiserver/venues/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/venues/BESTHOTEL/attachments/9", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a venue attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the venue attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the venue attachment does not exist, this call returns an error.

#### List all venue attachments

```
DEFINITION
GET http://apiserver/venues/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/attachments");

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
            "id": "9",
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

Returns a list of all venue attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit venue attachments, starting at index offset. Each entry in the array is a separate venue attachment object. If no more venue attachments are available, the resulting array will be empty. This request should never return an error.

### Venue Codes

#### Create a venue code

```
DEFINITION
POST http://apiserver/venues/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/codes", {
    "type": "DDCVNUCD1",
    "value": "HTL"
});

EXAMPLE RESPONSE
{
    "id": "31",
    "type": "DDCVNUCD1",
    "typeDescription": null,
    "value": "HTL",
    "valueDescription": "Hotel",
    "isActive": true
}

```

Creates a new venue code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a venue code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a venue code

```
DEFINITION
GET http://apiserver/venues/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/codes/31");

EXAMPLE RESPONSE
{
    "id": "31",
    "type": "DDCVNUCD1",
    "typeDescription": "Venue Type",
    "value": "HTL",
    "valueDescription": "Hotel",
    "isActive": true
}

```

Retrieves the details of an existing venue code. You need only supply the id.

##### Arguments

* id (required) - The id of the venue code to be retrieved.

#### Update a venue code

```
DEFINITION
POST http://apiserver/venues/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/codes/31", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "31",
    "type": "DDCVNUCD1",
    "typeDescription": "Venue Type",
    "value": "HTL",
    "valueDescription": "Hotel",
    "isActive": false
}


```

Updates the specified venue code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the venue code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a venue code

```
DEFINITION
DELETE http://apiserver/venues/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/venues/BESTHOTEL/codes/31", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a venue code. It cannot be undone.

##### Arguments

* id (required) - The id of the venue code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the venue code does not exist, this call returns an error.

#### List all venue codes

```
DEFINITION
GET http://apiserver/venues/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/codes");

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
            "type": "DDCVNUCD1",
            "typeDescription": "Venue Type",
            "value": "HTL",
            "valueDescription": "Hotel",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all venue codes.

##### Returns

A dictionary with an items property that contains an array of up to limit venue codes, starting at index offset. Each entry in the array is a separate venue code object. If no more venue codes are available, the resulting array will be empty. This request should never return an error.

### Venue Dates

#### Create a venue date

```
DEFINITION
POST http://apiserver/venues/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/dates", {
    "type": "DDCVNUDT1",
    "value": "2011-10-14"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCVNUDT1",
    "typeDescription": null,
    "value": "2011-10-14",
    "isActive": true
}

```

Creates a new venue date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a venue date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a venue date

```
DEFINITION
GET http://apiserver/venues/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/dates/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCVNUDT1",
    "typeDescription": "Contracts Due By",
    "value": "2011-10-14",
    "isActive": true
}

```

Retrieves the details of an existing venue date. You need only supply the id.

##### Arguments

* id (required) - The id of the venue date to be retrieved.

#### Update a venue date

```
DEFINITION
POST http://apiserver/venues/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/dates/8", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCVNUDT1",
    "typeDescription": "Contracts Due By",
    "value": "2011-10-14",
    "isActive": false
}


```

Updates the specified venue date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the venue date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a venue date

```
DEFINITION
DELETE http://apiserver/venues/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/venues/BESTHOTEL/dates/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a venue date. It cannot be undone.

##### Arguments

* id (required) - The id of the venue date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the venue date does not exist, this call returns an error.

#### List all venue dates

```
DEFINITION
GET http://apiserver/venues/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/dates");

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
            "type": "DDCVNUDT1",
            "typeDescription": "Contracts Due By",
            "value": "2011-10-14",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all venue dates.

##### Returns

A dictionary with an items property that contains an array of up to limit venue dates, starting at index offset. Each entry in the array is a separate venue date object. If no more venue dates are available, the resulting array will be empty. This request should never return an error.

### Venue Notes

#### Create a venue note

```
DEFINITION
POST http://apiserver/venues/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/notes", {
    "type": "DDCVNUNT1",
    "shortComment": "fun",
    "longComment": "Events here will be so much fun."
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCVNUNT1",
    "typeDescription": null,
    "shortComment": "fun",
    "longComment": "Events here will be so much fun."
}

```

Creates a new venue note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a venue note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a venue note

```
DEFINITION
GET http://apiserver/venues/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/notes/8");

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCVNUNT1",
    "typeDescription": "Event Note 1",
    "shortComment": "fun",
    "longComment": "Events here will be so much fun."
}

```

Retrieves the details of an existing venue note. You need only supply the id.

##### Arguments

* id (required) - The id of the venue note to be retrieved.

#### Update a venue note

```
DEFINITION
POST http://apiserver/venues/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/notes/8", {
    "longComment": "Events here will be so much fun!"
});

EXAMPLE RESPONSE
{
    "id": "8",
    "type": "DDCVNUNT1",
    "typeDescription": "Event Note 1",
    "shortComment": "fun",
    "longComment": "Events here will be so much fun!"
}


```

Updates the specified venue note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the venue note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a venue note

```
DEFINITION
DELETE http://apiserver/venues/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/venues/BESTHOTEL/notes/8", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a venue note. It cannot be undone.

##### Arguments

* id (required) - The id of the venue note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the venue note does not exist, this call returns an error.

#### List all venue notes

```
DEFINITION
GET http://apiserver/venues/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/notes");

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
            "type": "DDCVNUNT1",
            "typeDescription": "Event Note 1",
            "shortComment": "fun",
            "longComment": "Events here will be so much fun!"
        },
        {...},
    ]
}

```

Returns a list of all venue notes.

##### Returns

A dictionary with an items property that contains an array of up to limit venue notes, starting at index offset. Each entry in the array is a separate venue note object. If no more venue notes are available, the resulting array will be empty. This request should never return an error.

### Venue Numbers

#### Create a venue number

```
DEFINITION
POST http://apiserver/venues/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/numbers", {
    "type": "DDCVNUNR2",
    "value": 5000
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "DDCVNUNR2",
    "typeDescription": null,
    "value": 5000,
    "isActive": true
}

```

Creates a new venue number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a venue number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a venue number

```
DEFINITION
GET http://apiserver/venues/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/numbers/4");

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "DDCVNUNR2",
    "typeDescription": "Meeting Room Sq Footage",
    "value": 5000,
    "isActive": true
}

```

Retrieves the details of an existing venue number. You need only supply the id.

##### Arguments

* id (required) - The id of the venue number to be retrieved.

#### Update a venue number

```
DEFINITION
POST http://apiserver/venues/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/numbers/4", {
    "value": 1000
});

EXAMPLE RESPONSE
{
    "id": "4",
    "type": "DDCVNUNR2",
    "typeDescription": "Meeting Room Sq Footage",
    "value": 1000,
    "isActive": true
}


```

Updates the specified venue number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the venue number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a venue number

```
DEFINITION
DELETE http://apiserver/venues/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/venues/BESTHOTEL/numbers/4", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a venue number. It cannot be undone.

##### Arguments

* id (required) - The id of the venue number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the venue number does not exist, this call returns an error.

#### List all venue numbers

```
DEFINITION
GET http://apiserver/venues/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4",
            "type": "DDCVNUNR2",
            "typeDescription": "Meeting Room Sq Footage",
            "value": 1000,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all venue numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit venue numbers, starting at index offset. Each entry in the array is a separate venue number object. If no more venue numbers are available, the resulting array will be empty. This request should never return an error.

### Venue Rooms

#### Create a venue room

```
DEFINITION
POST http://apiserver/venues/:id/rooms

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/rooms", {
    "roomCode": "L100",
    "actualCapacity": 100,
    "sellToCapacity": 105
});

EXAMPLE RESPONSE
{
    "id": "61",
    "roomCode": "L100",
    "description": null,
    "actualCapacity": 100,
    "sellToCapacity": 105,
    "isActive": true
}

```

Creates a new venue room.

##### Arguments

* roomCode (required) - The room code uniquely identifies the room for each venue.
* description (optional) - The description of the room.
* actualCapacity (optional) - The actual capacity of the room.
* sellToCapacity (required) - The sell to capacity, represents the total number of seats to be sold. Must be greater than 0.
* isActive (optional : default true) - Indicates whether this room is active.

##### Returns

Returns a venue room object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a venue room

```
DEFINITION
GET http://apiserver/venues/:id/rooms/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/rooms/61");

EXAMPLE RESPONSE
{
    "id": "61",
    "roomCode": "L100",
    "description": null,
    "actualCapacity": 100,
    "sellToCapacity": 105,
    "isActive": true
}

```

Retrieves the details of an existing venue room. You need only supply the id.

##### Arguments

* id (required) - The id of the venue room to be retrieved.

#### Update a venue room

```
DEFINITION
POST http://apiserver/venues/:id/rooms/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL/rooms/61", {
    "description": "The nicest room in the place."
});

EXAMPLE RESPONSE
{
    "id": "61",
    "roomCode": "L100",
    "description": "The nicest room in the place.",
    "actualCapacity": 100,
    "sellToCapacity": 105,
    "isActive": true
}


```

Updates the specified venue room by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* roomCode (optional) - The room code uniquely identifies the room for each venue.
* description (optional) - The description of the room.
* actualCapacity (optional) - The actual capacity of the room.
* sellToCapacity (optional) - The sell to capacity, represents the total number of seats to be sold. Must be greater than 0.
* isActive (optional) - Indicates whether this room is active.

##### Returns

Returns the venue room object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a venue room

```
DEFINITION
DELETE http://apiserver/venues/:id/rooms/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/venues/BESTHOTEL/rooms/61", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a venue room. It cannot be undone.

##### Arguments

* id (required) - The id of the venue room to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the venue room does not exist, this call returns an error.

#### List all venue rooms

```
DEFINITION
GET http://apiserver/venues/:id/rooms

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL/rooms");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "61",
            "roomCode": "L100",
            "description": "The nicest room in the place.",
            "actualCapacity": 100,
            "sellToCapacity": 105,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all venue rooms.

##### Returns

A dictionary with an items property that contains an array of up to limit venue rooms, starting at index offset. Each entry in the array is a separate venue room object. If no more venue rooms are available, the resulting array will be empty. This request should never return an error.

### Venues

#### Create a venue

```
DEFINITION
POST http://apiserver/venues

EXAMPLE REQUEST
$.post("http://localhost:49195/venues", {
    "id": "BESTHOTEL",
    "mailingAddress": {
        "country": "USA",
        "postalCode": "75080"
    }
});

EXAMPLE RESPONSE
{
    "id": "BESTHOTEL",
    "description": null,
    "account": "28034",
    "owner": null,
    "comment": null,
    "isActive": true,
    "phone": null,
    "fax": null,
    "email": null,
    "mailingAddress": {
        "id": "1000028324",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000028325",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000028326",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    }
}

```

Creates a new venue.

##### Arguments

* id (required) - The venue code for the venue.
* description (optional) - The description of the venue.
* account (optional) - An existing account number to use for the venue. If not provided, a new account will be created.
* owner (optional) - The owner of the venue.
* comment (optional) - A comment about the venue.
* isActive (optional : default true) - Indicates whether the venue is active.
* phone (optional) - Phone for the venue account. If account is provided, this field represents changes to existing account phone.
* fax (optional) - Fax for the venue account. If account is provided, this field represents changes to existing account fax.
* email (optional) - Email for the venue account. If account is provided, this field represents changes to existing account email.
* mailingAddress (required) - Mailing Address for the venue account. If account is provided, this field represents changes to existing account mailing address. 'country' is required. 'postalCode' and 'state' must be valid for the 'country', and 'postalCode' is required for some countries. 'city', 'line1', 'line2', 'line3', and 'line4' are optional.
* billingAddress (optional) - Billing Address for the venue account. If account is provided, this field represents changes to existing account billing address. If not provided, and an existing account is not used, this address will be copied from the mailing address.
* shippingAddress (optional) - Shipping Address for the venue account. If account is provided, this field represents changes to existing account shipping address. If not provided, and an existing account is not used, this address will be copied from the mailing address.

##### Returns

Returns a venue object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a venue

```
DEFINITION
GET http://apiserver/venues/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/venues/BESTHOTEL");

EXAMPLE RESPONSE
{
    "id": "BESTHOTEL",
    "description": null,
    "account": "28034",
    "owner": null,
    "comment": null,
    "isActive": true,
    "phone": null,
    "fax": null,
    "email": null,
    "mailingAddress": {
        "id": "1000028324",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000028325",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000028326",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    }
}

```

Retrieves the details of an existing venue. You need only supply the id.

##### Arguments

* id (required) - The id of the venue to be retrieved.

#### Update a venue

```
DEFINITION
POST http://apiserver/venues/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/venues/BESTHOTEL", {
    "comment": "The bestest"
});

EXAMPLE RESPONSE
{
    "id": "BESTHOTEL",
    "description": null,
    "account": "28034",
    "owner": null,
    "comment": "The bestest",
    "isActive": true,
    "phone": null,
    "fax": null,
    "email": null,
    "mailingAddress": {
        "id": "1000028324",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "billingAddress": {
        "id": "1000028325",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "shippingAddress": {
        "id": "1000028326",
        "line1": null,
        "line2": null,
        "line3": null,
        "line4": null,
        "city": null,
        "state": null,
        "postalCode": "75080",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": false,
        "isActive": true,
        "countryDescription": null,
        "validatedDate": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    }
}


```

Updates the specified venue by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the venue.
* owner (optional) - The owner of the venue.
* comment (optional) - A comment about the venue.
* isActive (optional) - Indicates whether the venue is active.
* phone (optional) - Phone for the venue account.
* fax (optional) - Fax for the venue account.
* email (optional) - Email for the venue account.
* mailingAddress (optional) - Mailing Address for the venue account.
* billingAddress (optional) - Billing Address for the venue account.
* shippingAddress (optional) - Shipping Address for the venue account.

##### Returns

Returns the venue object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a venue

```
DEFINITION
DELETE http://apiserver/venues/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/venues/BESTHOTEL", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a venue. It cannot be undone.

##### Arguments

* id (required) - The id of the venue to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the venue does not exist, this call returns an error.

#### List all venues

```
DEFINITION
GET http://apiserver/venues

EXAMPLE REQUEST
$.get("http://localhost:49195/venues?comment=the");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "BESTHOTEL",
            "description": null,
            "account": "28034",
            "owner": null,
            "comment": "The bestest",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all venues.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match on venue code.
* description (optional) - Filter list by partial match on description.
* account (optional) - Filter list by exact match on account number.
* owner (optional) - Filter list by partial match on owner.
* comment (optional) - Filter list by partial match on comment.
* activeOnly (optional) - Indicates whether the list should be filtered to only active venues.

##### Returns

A dictionary with an items property that contains an array of up to limit venues, starting at index offset. Each entry in the array is a separate venue object. If no more venues are available, the resulting array will be empty. This request should never return an error.