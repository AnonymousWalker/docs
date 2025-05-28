# Subscription Promotional Code Prices

#### Create a subscription promotional code price

```
DEFINITION
POST http://apiserver/subscriptions/:subscriptionCode/promotionalcodes/:promoCodeId/prices

EXAMPLE REQUEST
$.post("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes/1/prices", {
    "id": "1YR"
});

EXAMPLE RESPONSE
{
    "priceCodeRecordId": "10101",
    "id": "1YR",
    "description": "One Year Renewal Price",
    "price": 12,
    "numberOfIssues": 12,
    "start": "2016-01-01",
    "end": "2099-01-01",
    "isActive": true,
    "useInStudioOnline": true,
    "defaultRenewalPriceCode": null,
    "defaultRenewalPriceCodeDescription": null,
    "title": "One Year",
    "additionalDescription1": null,
    "additionalDescription2": null,
    "additionalDescription3": null,
    "additionalDescription4": null
}

```

Creates a new subscription promotional code price.

##### Arguments

* id (required) - the price code value to be added to the promotional code

##### Returns

Returns a subscription promotional code price object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subscription promotional code price

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/promotionalcodes/:promoCodeId/prices/:priceCode

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes/1/prices/1YR");

EXAMPLE RESPONSE
{
    "priceCodeRecordId": "10101",
    "id": "1YR",
    "description": "One Year Renewal Price",
    "price": 12,
    "numberOfIssues": 12,
    "start": "2016-01-01",
    "end": "2099-01-01",
    "isActive": true,
    "useInStudioOnline": true,
    "defaultRenewalPriceCode": null,
    "defaultRenewalPriceCodeDescription": null,
    "title": "One Year",
    "additionalDescription1": null,
    "additionalDescription2": null,
    "additionalDescription3": null,
    "additionalDescription4": null
}

```

Retrieves the details of an existing subscription promotional code price. You need only supply the id.

##### Arguments

* priceCode (required) - The priceCode of the subscription promotional code price to be retrieved.

#### Delete a subscription promotional code price

```
DEFINITION
DELETE http://apiserver/subscriptions/:subscriptionCode/promotionalcodes/:promoCodeId/prices/:priceCode

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes/1/prices/1YR", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subscription promotional code price. It cannot be undone.

##### Arguments

* priceCode (required) - The price code of the subscription promotional code price to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the subscription promotional code price does not exist, this call returns an error.

#### List all subscription promotional code prices

```
DEFINITION
GET http://apiserver/subscriptions/:subscriptionCode/promotionalcodes/:promoCodeId/prices

EXAMPLE REQUEST
$.get("http://localhost:49195/subscriptions/EXPLORERS/promotionalcodes/1/prices");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "priceCodeRecordId": "10101",
            "id": "1YR",
            "description": "One Year Renewal Price",
            "price": 12,
            "numberOfIssues": 12,
            "start": "2016-01-01",
            "end": "2099-01-01",
            "isActive": true,
            "useInStudioOnline": true,
            "defaultRenewalPriceCode": null,
            "defaultRenewalPriceCodeDescription": null,
            "title": "One Year",
            "additionalDescription1": null,
            "additionalDescription2": null,
            "additionalDescription3": null,
            "additionalDescription4": null
        },
        {...},
    ]
}

```

Returns a list of all subscription promotional code prices.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription promotional code prices, starting at index offset. Each entry in the array is a separate subscription promotional code price object. If no more subscription promotional code prices are available, the resulting array will be empty. This request should never return an error.