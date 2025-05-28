# Subscription Issues

#### Create a subscription issue

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/issues

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/issues", {
    "id": "2015MAY",
    "description": "Little Explorers - May Issue",
    "issueDate": "2015-04-25",
    "numberOfSubscriptions": 12
});

EXAMPLE RESPONSE
{
    "id": "2015MAY",
    "description": "Little Explorers - May Issue",
    "issueDate": "2015-04-25",
    "quantityFulfilled": 0,
    "numberOfSubscriptions": 12,
    "cost": 0,
    "income": 0,
    "isActive": true
}

```

Creates a new subscription issue.

##### Arguments

* id (required) - the issue code to create the subscription issue with
* description (optional) - the issue description to create the subscription issue with
* issueDate (optional) - the issue date to create the subscription issue with
* quantityFulfilled (optional) - the number of fulfilled issues to create the subscription issue with
* numberOfSubscriptions (optional) - the number of subscriptions to create the subscription issue with
* cost (optional) - the cost per subscription to create the subscription issue with
* income (optional) - the total issue income to create the subscription issue with
* isActive (optional: defaults to true) - is the subscription issue active

##### Returns

Returns a subscription issue object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription issue

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/issues/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/issues/2015MAY");

EXAMPLE RESPONSE
{
    "id": "2015MAY",
    "description": "Little Explorers - May Issue",
    "issueDate": "2015-04-25",
    "quantityFulfilled": 12,
    "numberOfSubscriptions": 12,
    "cost": 0,
    "income": 12.13,
    "isActive": true
}

```

Retrieves the details of an existing subscription issue. You need only supply the id.

##### Arguments

* id (required) - The id of the subscription issue to be retrieved.

#### Update a subscription issue

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/issues/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/issues/2015MAY", {
    "description": "Little Explorers Magazine - May 2015"
});

EXAMPLE RESPONSE
{
    "id": "2015MAY",
    "description": "Little Explorers Magazine - May 2015",
    "issueDate": "2015-04-25",
    "quantityFulfilled": 12,
    "numberOfSubscriptions": 12,
    "cost": 0,
    "income": 12.13,
    "isActive": true
}

```

Updates the specified subscription issue by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (optional) - the issue code to update the subscription issue with
* description (optional) - the issue description to update the subscription issue with
* issueDate (optional) - the issue date to update the subscription issue with
* quantityFulfilled (optional) - the number of fulfilled issues to update the subscription issue with
* numberOfSubscriptions (optional) - the number of subscriptions to update the subscription issue with
* cost (optional) - the cost per subscription to update the subscription issue with
* income (optional) - the total issue income to update the subscription issue with
* isActive (optional) - is the subscription issue active

##### Returns

Returns the subscription issue object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a subscription issue

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/issues/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/issues/2015MAY", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription issue. It cannot be undone.

##### Arguments

* id (required) - The id of the subscription issue to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription issue does not exist, this call returns an error.

#### List all subscription issues

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/issues

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/issues");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "2015MAY",
            "description": "Little Explorers - May Issue",
            "issueDate": "2015-04-25",
            "quantityFulfilled": 12,
            "numberOfSubscriptions": 12,
            "cost": 0,
            "income": 12.13,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all subscription issues.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription issues, starting at index offset. Each entry in the array is a separate subscription issue object. If no more subscription issues are available, the resulting array will be empty. This request should never return an error.