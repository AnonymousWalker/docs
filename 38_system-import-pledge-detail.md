# System Import Pledge Detail

#### Retrieve a system import pledge detail

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledges/:id/detail

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledges/40812571/detail");

EXAMPLE RESPONSE
{
    "id": null,
    "description": "",
    "company": "010",
    "isActive": true,
    "defaultFrequency": "",
    "defaultStart": "2015-08-10",
    "defaultEnd": null,
    "defaultAmountPerGift": 1,
    "defaultNumberPledged": 12,
    "defaultSource": "",
    "isDefaultOpenEnded": false,
    "pledgeType": "PROJECT",
    "singleOrMultiSponsorship": "A",
    "totalAmountRequiredMonthly": 1,
    "isUseInShoppingCart": false,
    "isSecure": false
}

```

Retrieves the details of an existing system import pledge detail. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge detail to be retrieved.

#### Update a system import pledge detail

```
DEFINITION
POST http://apiserver/systemimports/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/pledges/40812571/detail", {
    "defaultNumberPledged": 9
});

EXAMPLE RESPONSE
{
    "id": null,
    "description": "",
    "company": "010",
    "isActive": true,
    "defaultFrequency": "",
    "defaultStart": "2015-08-10",
    "defaultEnd": null,
    "defaultAmountPerGift": 1,
    "defaultNumberPledged": 9,
    "defaultSource": "",
    "isDefaultOpenEnded": false,
    "pledgeType": "PROJECT",
    "singleOrMultiSponsorship": "A",
    "totalAmountRequiredMonthly": 1,
    "isUseInShoppingCart": false,
    "isSecure": false
}

```

Updates the specified system import pledge detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* pledgeType (optional) - the pledge type to update the detail with
* company (optional) - the company code to update the detail with
* totalAmountRequiredMonthly (optional) the total amount required monthly to update the detail with
* singleOrMultiSponsorship (optional) is the pledge a single- or multi-sponsorship
* isActive (optional) is the pledge active
* isUseInShoppingCart (optional) - is the pledge used in Studio Online
* defaultFrequency (optional) - the default frequency to update the detail with
* isOpenEnded (optional) is the pledge open ended
* defaultStart (optional) the default start date to update the detail with
* defaultEnd (optional) the default end date to update the detail with
* defaultAmountPerGift (optional) the default amount per gift to update the detail with
* defaultNumberPledged (optional) the default number pledged to update the detail with
* defaultSource (optional) the default source to update the detail with
* isSecure (optional) - indicates if this is a secure project for Advanced Studio Online

##### Returns

Returns the system import pledge detail object if the update succeeded. Returns an error if update parameters are invalid.