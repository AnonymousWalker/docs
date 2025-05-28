# Financial Management

### Accounting Controls

#### Create an accounting control

```
DEFINITION
POST http://apiserver/accountingcontrols

EXAMPLE REQUEST
$.post("http://localhost:49195/accountingcontrols", {
    "id": "DIMENSION1",
    "description": "Data type for GP Dimension 1",
    "value": "SOURCE"
});

EXAMPLE RESPONSE
{
    "id": "DIMENSION1",
    "description": "Data type for GP Dimension 1",
    "value": "SOURCE"
}

```

##### Arguments

* id (required) - The accounting control id
* description (required) - The description of the accounting control
* value (optional) - The value for the accounting control

##### Returns

Returns an accounting control object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accounting control

```
DEFINITION
GET http://apiserver/accountingcontrols/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accountingcontrols/DIMENSION1");

EXAMPLE RESPONSE
{
    "id": "DIMENSION1",
    "description": "Data type for GP Dimension 1",
    "value": "SOURCE"
}

```

Retrieves the details of an existing accounting control. You need only supply the accounting control id.

##### Returns

Returns an accounting control object if a valid id was provided.

#### Update an accounting control

```
DEFINITION
POST http://apiserver/accountingcontrols/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accountingcontrols/DIMENSION1", {
    "value": "ELEMENT"
});

EXAMPLE RESPONSE
{
    "id": "DIMENSION1",
    "description": "Data type for GP Dimension 1",
    "value": "ELEMENT"
}

```

##### Arguments

* description (required) - The description of the accounting control
* value (optional) - The value for the accounting control

##### Returns

Returns an accounting control object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete an accounting control

```
DEFINITION
DELETE http://apiserver/accountingcontrols/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accountingcontrols/DIMENSION1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an accounting control. It cannot be undone.

##### Arguments

* id (required) - The id of the accounting control to be deleted.

##### Returns

Returns a 204 No Content response on success. If the accounting control id does not exist, this call returns an error.

#### List all accounting controls

```
DEFINITION
GET http://apiserver/accountingcontrols

EXAMPLE REQUEST
$.get("http://localhost:49195/accountingcontrols");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "DIMENSION1",
            "description": "Data type for GP Dimension 1",
            "value": "ELEMENT"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all accounting controls.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in accounting control
* description () - Filter list by partial match in accounting control description

##### Returns

A dictionary with an items property that contains an array of up to limit accounting controls, starting at index offset. Each entry in the array is a separate accounting control object. If no more accounting controls are available, the resulting array will be empty. This request should never return an error.

### Accounting Instructions

#### Create an accounting instruction

```
DEFINITION
POST http://apiserver/accountinginstructions

EXAMPLE REQUEST
$.post("http://localhost:49195/accountinginstructions", {
    "company": "4",
    "type": "SUB",
    "detailCode": "DECISION",
    "glTransactionType": "REVENUE",
    "glTransactionTypeDescription": "Revenue",
    "glSegment1": "SubsRev",
    "glSegment2": "4"
});

EXAMPLE RESPONSE
{
    "id": "480",
    "company": "4",
    "companyDescription": "DonorDirect",
    "type": "SUB",
    "typeDescription": "Subscription code instructions",
    "detailCode": "DECISION",
    "detailSubCode": null,
    "glTransactionType": "REVENUE",
    "glTransactionTypeDescription": "Revenue",
    "glSegment1": "SubsRev",
    "glSegment2": "4",
    "glSegment3": null,
    "glSegment4": null,
    "glSegment5": null,
    "glSegment6": null,
    "glSegment7": null,
    "glSegment8": null,
    "glSegment9": null,
    "glSegment10": null
}

```

##### Arguments

* company (required) - The company of the accounting instruction. Must be a valid code value for the code type `DDCCOMPANY`
* type (required) - The instruction type of the accounting instruction. Must be a valid code value for the code type `DDCACTINTP`
* detailCode (required) - The instruction detail code of the accounting instruction
* glTransactionType (required) - The GL transaction type of the accounting instruction. Must be a valid code value for the code type `DDCGLTYPE`
* detailSubCode (optional) - The instruction detail subcode of the accounting instruction. If componentType=Event this must be a valid session code, if provided.
* glSegment1 (optional) - The GL segment 1 of the accounting instruction
* glSegment2 (optional) - The GL segment 2 of the accounting instruction
* glSegment3 (optional) - The GL segment 3 of the accounting instruction
* glSegment4 (optional) - The GL segment 4 of the accounting instruction
* glSegment5 (optional) - The GL segment 5 of the accounting instruction
* glSegment6 (optional) - The GL segment 6 of the accounting instruction
* glSegment7 (optional) - The GL segment 7 of the accounting instruction
* glSegment8 (optional) - The GL segment 8 of the accounting instruction
* glSegment9 (optional) - The GL segment 9 of the accounting instruction
* glSegment10 (optional) - The GL segment 10 of the accounting instruction
* componentType (optional) - Set this is more validation is required. Currently, the valid values are "Project", "Event", "Source", and "Subscription"

##### Returns

Returns an accounting instruction object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an accounting instruction

```
DEFINITION
GET http://apiserver/accountinginstructions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accountinginstructions/480");

EXAMPLE RESPONSE
{
    "id": "480",
    "company": "4",
    "companyDescription": "DonorDirect",
    "type": "SUB",
    "typeDescription": "Subscription code instructions",
    "detailCode": "DECISION",
    "detailSubCode": null,
    "glTransactionType": "REVENUE",
    "glTransactionTypeDescription": "Revenue",
    "glSegment1": "SubsRev",
    "glSegment2": "4",
    "glSegment3": null,
    "glSegment4": null,
    "glSegment5": null,
    "glSegment6": null,
    "glSegment7": null,
    "glSegment8": null,
    "glSegment9": null,
    "glSegment10": null
}

```

Retrieves the details of an existing accounting instruction. You need only supply the accounting instruction id.

##### Returns

Returns an accounting instruction object if a valid id was provided.

#### Update an accounting instruction

```
DEFINITION
POST http://apiserver/accountinginstructions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accountinginstructions/480", {
    "glSegment2": "15"
});

EXAMPLE RESPONSE
{
    "id": "480",
    "company": "4",
    "companyDescription": "DonorDirect",
    "type": "SUB",
    "typeDescription": "Subscription code instructions",
    "detailCode": "DECISION",
    "detailSubCode": null,
    "glTransactionType": "REVENUE",
    "glTransactionTypeDescription": "Revenue",
    "glSegment1": "SubsRev",
    "glSegment2": "15",
    "glSegment3": null,
    "glSegment4": null,
    "glSegment5": null,
    "glSegment6": null,
    "glSegment7": null,
    "glSegment8": null,
    "glSegment9": null,
    "glSegment10": null
}

```

##### Arguments

* company (required) - The company of the accounting instruction. Must be a valid code value for the code type `DDCCOMPANY`
* type (required) - The instruction type of the accounting instruction. Must be a valid code value for the code type `DDCACTINTP`
* detailCode (required) - The instruction detail code of the accounting instruction
* glTransactionType (required) - The GL transaction type of the accounting instruction. Must be a valid code value for the code type `DDCGLTYPE`
* detailSubCode (optional) - The instruction detail subcode of the accounting instruction
* glSegment1 (optional) - The GL segment 1 of the accounting instruction
* glSegment2 (optional) - The GL segment 2 of the accounting instruction
* glSegment3 (optional) - The GL segment 3 of the accounting instruction
* glSegment4 (optional) - The GL segment 4 of the accounting instruction
* glSegment5 (optional) - The GL segment 5 of the accounting instruction
* glSegment6 (optional) - The GL segment 6 of the accounting instruction
* glSegment7 (optional) - The GL segment 7 of the accounting instruction
* glSegment8 (optional) - The GL segment 8 of the accounting instruction
* glSegment9 (optional) - The GL segment 9 of the accounting instruction
* glSegment10 (optional) - The GL segment 10 of the accounting instruction
* componentType (optional) - Set this is more validation is required. Currently, the valid values are "Project", "Event", "Source", and "Subscription"

##### Returns

Returns an accounting instruction object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete an accounting instruction

```
DEFINITION
DELETE http://apiserver/accountinginstructions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accountinginstructions/480", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an accounting instruction. It cannot be undone.

##### Arguments

* id (required) - The id of the accounting instruction to be deleted.

##### Returns

Returns a 204 No Content response on success. If the accounting instruction id does not exist, this call returns an error.

#### List all accounting instructions

```
DEFINITION
GET http://apiserver/accountinginstructions

EXAMPLE REQUEST
$.get("http://localhost:49195/accountinginstructions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "480",
            "company": "4",
            "companyDescription": "DonorDirect",
            "type": "SUB",
            "typeDescription": "Subscription code instructions",
            "detailCode": "DECISION",
            "detailSubCode": null,
            "glTransactionType": "REVENUE",
            "glTransactionTypeDescription": "Revenue",
            "glSegment1": "SubsRev",
            "glSegment2": "15",
            "glSegment3": null,
            "glSegment4": null,
            "glSegment5": null,
            "glSegment6": null,
            "glSegment7": null,
            "glSegment8": null,
            "glSegment9": null,
            "glSegment10": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all accounting instructions.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* company () - The company of the accounting instruction. Must be a valid code value for the code type `DDCCOMPANY`
* type () - The instruction type of the accounting instruction. Must be a valid code value for the code type `DDCACTINTP`. This is required if componentType=Project.
* detailCode () - The instruction detail code of the accounting instruction. This is required if componentType=Project, componentType=Event, componentType=Source, or componentType=Subscription.
* glTransactionType () - The GL transaction type of the accounting instruction. Must be a valid code value for the code type `DDCGLTYPE`. This is required if componentType=Project.
* detailSubCode () - The instruction detail subcode of the accounting instruction
* glSegment1 () - The GL segment 1 of the accounting instruction
* glSegment2 () - The GL segment 2 of the accounting instruction
* glSegment3 () - The GL segment 3 of the accounting instruction
* glSegment4 () - The GL segment 4 of the accounting instruction
* glSegment5 () - The GL segment 5 of the accounting instruction
* glSegment6 () - The GL segment 6 of the accounting instruction
* glSegment7 () - The GL segment 7 of the accounting instruction
* glSegment8 () - The GL segment 8 of the accounting instruction
* glSegment9 () - The GL segment 9 of the accounting instruction
* glSegment10 () - The GL segment 10 of the accounting instruction
* componentType () - Set this is more validation is required. Currently, the valid values are "Project", "Event", "Source", and "Subscription"

##### Returns

A dictionary with an items property that contains an array of up to limit accounting instructions, starting at index offset. Each entry in the array is a separate accounting instruction object. If no more accounting instructions are available, the resulting array will be empty. This request should never return an error.

### Accounting Instruction Codes

#### Create an accounting instruction code

```
DEFINITION
POST http://apiserver/accountinginstructions/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/accountinginstructions/480/codes", {
    "type": "TYP1",
    "value": "Y"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "TYP1",
    "typeDescription": "Code Type 1",
    "value": "Y",
    "valueDescription": "Yes",
    "isActive": true
}

```

Creates a new accounting instruction code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an accounting instruction code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve an accounting instruction code

```
DEFINITION
GET http://apiserver/accountinginstructions/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accountinginstructions/480/codes/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "TYP1",
    "typeDescription": "Code Type 1",
    "value": "Y",
    "valueDescription": "Yes",
    "isActive": true
}

```

Retrieves the details of an existing accounting instruction code. You need only supply the accounting instruction id and accounting instruction code id.

##### Returns

Returns an accounting instruction code object if a valid id was provided.

#### Update an accounting instruction code

```
DEFINITION
POST http://apiserver/accountinginstructions/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accountinginstructions/480/codes/16", {
    "value": "N"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "TYP1",
    "typeDescription": "Code Type 1",
    "value": "N",
    "valueDescription": "No",
    "isActive": true
}


```

Updates the specified accounting instruction code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the accounting instruction code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete an accounting instruction code

```
DEFINITION
DELETE http://apiserver/accountinginstructions/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accountinginstructions/480/codes/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a accounting instruction code. It cannot be undone.

##### Arguments

* id (required) - The id of the accounting instruction code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the accounting instruction code id does not exist, this call returns an error.

#### List all accounting instruction codes

```
DEFINITION
GET http://apiserver/accountinginstructions/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/accountinginstructions/480/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "16",
            "type": "TYP1",
            "typeDescription": "Code Type 1",
            "value": "N",
            "valueDescription": "No",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all accounting instruction codes.

##### Returns

A dictionary with an items property that contains an array of up to limit accounting instruction codes, starting at index offset. Each entry in the array is a separate accounting instruction code object. If no more accounting instruction codes are available, the resulting array will be empty. This request should never return an error.

### Allocation Categories

#### Create an allocation category

```
DEFINITION
POST http://apiserver/allocations

EXAMPLE REQUEST
$.post("http://localhost:49195/allocations", {
    "id": "TRAVEL",
    "description": "Travel Reserve",
    "group": 30,
    "isActive": true,
    "processingSequence": 2,
    "type": "F",
    "processingMethod": "M",
    "balanceLevel": "P",
    "isCreditBalanceOnly": false,
    "fromObjectSegment": "51000",
    "fromSubaccount": "001",
    "toObjectSegment": "51000",
    "toSubaccount": "002"
});

EXAMPLE RESPONSE
{
    "id": "TRAVEL",
    "group": "30",
    "groupDescription": "30th of the Month",
    "isActive": true,
    "processingSequence": 2,
    "description": "Travel Reserve",
    "type": "F",
    "processingMethod": "M",
    "subaccountForBalance": null,
    "balanceLevel": "P",
    "isCreditBalanceOnly": false,
    "fromObjectSegment": "51000",
    "fromSubaccount": "001",
    "toProject": null,
    "toObjectSegment": "51000",
    "toSubaccount": "002",
    "objectLow": null,
    "objectHigh": null,
    "period": null
}

```

##### Arguments

* id (required) - The allocation id
* description (optional) - The description of the allocation
* group (optional) - The allocation group. Must be a valid code value for the code type `DDCALLCGRP`
* isActive (optional) - Whether or not the allocation is active. Will be set to true by default
* type (optional) - The type of allocation. Must be one of the following values: `F`=Fixed Amount, `P`=Percentage, `B`=Balance Transfer, `L`=Credit To Limit.
* processingSequence (optional) - The processing sequence for the allocation
* processingMethod (optional) - The processing method for allocation of the Percentage type. Must be one of the following values: `M`=Monthly, `B`=Depost Posted
* subaccountForBalance (optional) - The subaccount for allocation of the Percentage type with a subaccount balance level
* balanceLevel (optional) - The balance level for allocations of the Percentage type. Must be one of the following values: `P`=Project, `S`=Subaccount
* isCreditBalanceOnly (optional) - For allocations of the Balance Transfer type, whether it is credit balance only
* fromObjectSegment (optional) - The From Object Segment for the allocation
* fromSubaccount (optional) - The From Subaccount for the allocation
* toProject (optional) - The To Project for the allocation
* toObjectSegment (optional) - The To Object Segment for the allocation
* toSubaccount (optional) - The To Subaccount for the allocation
* objectHigh (optional) - The Object Low for allocations of the Percentage type
* objectLow (optional) - The Object High for allocations of the Percentage type
* period (optional) - The Period for allocations of the Percentage type. Must be one of the following values: `C`=Current, `P`=Last

##### Returns

Returns an allocation category object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an allocation category

```
DEFINITION
GET http://apiserver/allocations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/allocations/TRAVEL");

EXAMPLE RESPONSE
{
    "id": "TRAVEL",
    "group": "30",
    "groupDescription": "30th of the Month",
    "isActive": true,
    "processingSequence": 2,
    "description": "Travel Reserve",
    "type": "F",
    "processingMethod": "M",
    "subaccountForBalance": null,
    "balanceLevel": "P",
    "isCreditBalanceOnly": false,
    "fromObjectSegment": "51000",
    "fromSubaccount": "001",
    "toProject": null,
    "toObjectSegment": "51000",
    "toSubaccount": "002",
    "objectLow": null,
    "objectHigh": null,
    "period": null
}

```

Retrieves the details of an existing allocation category. You need only supply the allocation category id.

##### Returns

Returns an allocation category object if a valid id was provided.

#### Update an allocation category

```
DEFINITION
POST http://apiserver/allocations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/allocations/TRAVEL", {
    "group": "15"
});

EXAMPLE RESPONSE
{
    "id": "TRAVEL",
    "group": "15",
    "groupDescription": "15th of the Month",
    "isActive": true,
    "processingSequence": 2,
    "description": "Travel Reserve",
    "type": "F",
    "processingMethod": "M",
    "subaccountForBalance": null,
    "balanceLevel": "P",
    "isCreditBalanceOnly": false,
    "fromObjectSegment": "51000",
    "fromSubaccount": "001",
    "toProject": null,
    "toObjectSegment": "51000",
    "toSubaccount": "002",
    "objectLow": null,
    "objectHigh": null,
    "period": null
}

```

##### Arguments

* description (optional) - The description of the allocation
* group (optional) - The allocation group. Must be a valid code value for the code type `DDCALLCGRP`
* isActive (optional) - Whether or not the allocation is active
* type (optional) - The type of allocation. Must be one of the following values: `F`=Fixed Amount, `P`=Percentage, `B`=Balance Transfer, `L`=Credit To Limit.
* processingSequence (optional) - The processing sequence for the allocation
* processingMethod (optional) - The processing method for allocation of the Percentage type. Must be one of the following values: `M`=Monthly, `B`=Depost Posted
* subaccountForBalance (optional) - The subaccount for allocation of the Percentage type with a subaccount balance level
* balanceLevel (optional) - The balance level for allocations of the Percentage type. Must be one of the following values: `P`=Project, `S`=Subaccount
* isCreditBalanceOnly (optional) - For allocations of the Balance Transfer type, whether it is credit balance only
* fromObjectSegment (optional) - The From Object Segment for the allocation
* fromSubaccount (optional) - The From Subaccount for the allocation
* toProject (optional) - The To Project for the allocation
* toObjectSegment (optional) - The To Object Segment for the allocation
* toSubaccount (optional) - The To Subaccount for the allocation
* objectHigh (optional) - The Object Low for allocations of the Percentage type
* objectLow (optional) - The Object High for allocations of the Percentage type
* period (optional) - The Period for allocations of the Percentage type. Must be one of the following values: `C`=Current, `P`=Last

##### Returns

Returns an allocation category object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete an allocation category

```
DEFINITION
DELETE http://apiserver/allocations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/allocations/TRAVEL", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an allocation category. It cannot be undone.

##### Arguments

* id (required) - The id of the allocation category to be deleted.

##### Returns

Returns a 204 No Content response on success. If the allocation category id does not exist, this call returns an error.

#### List all allocation categories

```
DEFINITION
GET http://apiserver/allocations

EXAMPLE REQUEST
$.get("http://localhost:49195/allocations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "TRAVEL",
            "group": "30",
            "groupDescription": "30th of the Month",
            "isActive": true,
            "processingSequence": 2,
            "description": "Travel Reserve",
            "type": "F",
            "processingMethod": "M",
            "subaccountForBalance": null,
            "balanceLevel": "P",
            "isCreditBalanceOnly": false,
            "fromObjectSegment": "51000",
            "fromSubaccount": "001",
            "toProject": null,
            "toObjectSegment": "51000",
            "toSubaccount": "002",
            "objectLow": null,
            "objectHigh": null,
            "period": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all allocation categories.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in allocation category
* group () - Filter list by allocation group code
* description () - Filter list by partial match in allocation category description
* isActive () - Filter list by whether the allocation category is active

##### Returns

A dictionary with an items property that contains an array of up to limit allocation categories, starting at index offset. Each entry in the array is a separate allocation category object. If no more allocation categories are available, the resulting array will be empty. This request should never return an error.

### Allocations Process Run

```
DEFINITION
POST http://apiserver/projects/:id/allocationsprocess

EXAMPLE REQUEST
$.post("http://localhost:49195/allocationsprocess", {
    "company":"1",
    "departmentStart":"100",
    "departmentEnd":"200",
    "currencyCode":"USD",
    "projectCodeStart":"100000",
    "projectCodeEnd":"100100",
    "description":"Process Run 1"
    "glDate":"2015-05-01",
    "dateEnd":"2015-08-01",
    "groupType":"30",
});

EXAMPLE RESPONSE
204 No Content

```

This will begin the allocation category process run.

##### Arguments

* company (required) - The company code for the process run.
* departmentStart (required) - The starting department code for the process run.
* departmentEnd (required) - The starting department code for the process run.
* projectCodeStart (required) - The starting project code for the process run.
* projectCodeEnd (required) - The starting project code for the process run.
* description (optional) - The description for the process run.
* groupType (optional) - The allocation group type for the process run. Must be a valid code value for the code type `DDCALLCGRP`.
* glDate (optional) - The GL Date for the process run.
* currencyCode (optional) - The currency code for the process run.

##### Returns

Returns a 204 No Content response on success.

### Catalogs

#### Create a catalog

```
DEFINITION
POST http://apiserver/catalogs

EXAMPLE REQUEST
$.post("http://localhost:49195/catalogs", {
    "id": "SUMMER2018",
    "name": "Summer 2018 Giving Catalog",
    "startDate": "2018-05-25",
    "endDate": "2018-08-30",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "SUMMER2018",
    "name": "Summer 2018 Giving Catalog",
    "startDate": "2018-05-25",
    "endDate": "2018-08-30",
    "isActive": true
}

```

##### Arguments

* id (required) - The identifier of the catalog
* name (required) - The name of the catalog
* startDate (optional) - The start date of the catalog
* endDate (optional) - The end date of the catalog
* isActive (required) - If the catalog is active

##### Returns

Returns a catalog object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a catalog

```
DEFINITION
GET http://apiserver/catalogs/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/catalogs/SUMMER2018");

EXAMPLE RESPONSE
{
    "name": "Summer 2018 Giving Catalog",
    "startDate": "2018-05-25",
    "endDate": "2018-08-30",
    "isActive": true
}

```

Retrieves the details of an existing catalog. You need only supply the catalog id.

##### Arguments

* id (required) - The id of the catalog to be retrieved.

##### Returns

Returns a catalog object if a valid id was provided.

#### Update a catalog

```
DEFINITION
POST http://apiserver/catalogs/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/catalogs/SUMMER2018", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "name": "Summer 2018 Giving Catalog",
    "startDate": "2018-05-25",
    "endDate": "2018-08-30",
    "isActive": false
}


```

Updates the specified catalog by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the catalog object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a catalog

```
DEFINITION
DELETE http://apiserver/catalogs/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/catalogs/SUMMER2018", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* id (required) - The id of the catalog to be deleted.

##### Returns

Returns a 200 OK response on success. If the catalog id does not exist then this call returns an error.

#### List all catalogs

```
DEFINITION
GET http://apiserver/catalogs

EXAMPLE REQUEST
$.get("http://localhost:49195/catalogs");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "SUMMER2018",
            "name": "Summer 2018 Giving Catalog",
            "startDate": "2018-05-25",
            "endDate": "2018-08-30",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all catalogs on the account.

##### Returns

A dictionary with an items property that contains an array of up to limit catalogs, starting at index offset. Each entry in the array is a separate catalog object. If no more catalogs are available, the resulting array will be empty. This request should never return an error.

### Catalog Items

#### Create a catalog item

```
DEFINITION
POST http://apiserver/catalogs/:id/items

EXAMPLE REQUEST
$.post("http://localhost:49195/catalogs/SUMMER2018/items", {
    "item": "L1",
    "name": "12 Chicks",
    "project": "INDLIVESTK",
    "sequence": 20,
    "suggestedPrice": 3,
    "minimumAmount": 2.5
});

EXAMPLE RESPONSE
{
    "item": "L1",
    "name": "12 Chicks",
    "project": "INDLIVESTK",
    "projectDescription": "India - Livestock Fund",
    "sequence": 20,
    "suggestedPrice": 3,
    "minimumAmount": 2.5,
    "isProjectDeductible": true
}

```

##### Arguments

* item (required) - The identifier of the catalog item
* name (required) - The name of the catalog item
* project (required) - The project receiving the funds for the catalog item
* sequence (optional) - The sequence number of the catalog item
* suggestedPrice (required) - The suggested price of the catalog item
* minimumAmount (optional) - The minimum amount for the catalog item
* isProjectDeductible (optional) - Is the project on the catalog item deductible

##### Returns

Returns a catalog item object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a catalog item

```
DEFINITION
GET http://apiserver/catalogs/:id/items/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/catalogs/SUMMER2018/items/L1");

EXAMPLE RESPONSE
{
    "item": "L1",
    "name": "12 Chicks",
    "project": "INDLIVESTK",
    "projectDescription": "India - Livestock Fund",
    "sequence": 20,
    "suggestedPrice": 3,
    "minimumAmount": 2.5,
    "isProjectDeductible": true
}

```

Retrieves the details of an existing catalog item.

##### Arguments

* id (required) - The id of the catalog item to be retrieved.

##### Returns

Returns a catalog item object if a valid id was provided.

#### Update a catalog item

```
DEFINITION
POST http://apiserver/catalogs/:id/items/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/catalogs/SUMMER2018/items/L1", {
    "suggestedPrice": 4.5
});

EXAMPLE RESPONSE
{
    "item": "L1",
    "name": "12 Chicks",
    "project": "INDLIVESTK",
    "projectDescription": "India - Livestock Fund",
    "sequence": 20,
    "suggestedPrice": 4.5,
    "minimumAmount": 2.5,
    "isProjectDeductible": true
}


```

Updates the specified catalog item by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the catalog item object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a catalog item

```
DEFINITION
DELETE http://apiserver/catalogs/:id/items/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/catalogs/SUMMER2018/items/L1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* id (required) - The id of the catalog item to be deleted.

##### Returns

Returns a 200 OK response on success. If the catalog item id does not exist then this call returns an error.

#### List all catalog items

```
DEFINITION
GET http://apiserver/catalogs/:id/items

EXAMPLE REQUEST
$.get("http://localhost:49195/catalogs/SUMMER2018/items");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "item": "L1",
            "name": "12 Chicks",
            "project": "INDLIVESTK",
            "projectDescription": "India - Livestock Fund",
            "sequence": 20,
            "suggestedPrice": 3,
            "minimumAmount": 2.5,
            "isProjectDeductible": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all items on the catalog.

##### Returns

A dictionary with an items property that contains an array of up to limit catalogs, starting at index offset. Each entry in the array is a separate catalog item object. If no more catalogs are available, the resulting array will be empty. This request should never return an error.

### Causes

#### Retrieve a cause

```
DEFINITION
GET http://apiserver/causes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/causes/D10D0001");

EXAMPLE RESPONSE
{
    "id": "D10D0001",
    "description": "Support Pastor Picard in cleaning the gulf coast",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "project": "110115",
    "projectDescription": "Gulf Oil Spill Relief",
    "causeTemplate": "CTMP004",
    "causeTemplateName": "Help pastors clean gulf",
    "isActive": true,
    "goal": 5000,
    "totalRaised": 120,
    "summary": "test",
    "extendedDescription": "test"
}

```

Retrieves the details of an existing cause. You need only supply the id.

##### Arguments

* id (required) - The id of the cause to be retrieved.

#### Update a cause

```
DEFINITION
POST http://apiserver/causes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/causes/D10D0001", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "D10D0001",
    "description": "Support Pastor Picard in cleaning the gulf coast",
    "account": "27494",
    "accountName": "Captain Jean-Luc Picard",
    "project": "110115",
    "projectDescription": "Gulf Oil Spill Relief",
    "causeTemplate": "CTMP004",
    "causeTemplateName": "Help pastors clean gulf",
    "isActive": false,
    "goal": 5000,
    "totalRaised": 120,
    "summary": "test",
    "extendedDescription": "test"
}


```

Updates the specified cause by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* project (optional) - The project code for the cause. Must be a valid `DDCPROJ`.
* isActive (optional) - Indicates whether the cause is active.

##### Returns

Returns the cause object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause

```
DEFINITION
DELETE http://apiserver/causes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/causes/D10D0001", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause. It cannot be undone.

##### Arguments

* id (required) - The id of the cause to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause does not exist, this call returns an error.

#### List all causes

```
DEFINITION
GET http://apiserver/causes

EXAMPLE REQUEST
$.get("http://localhost:49195/causes?project=110115");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "D10D0001",
            "description": "Support Pastor Picard in cleaning the gulf coast",
            "account": "27494",
            "accountName": "Captain Jean-Luc Picard",
            "project": "110115",
            "projectDescription": "Gulf Oil Spill Relief",
            "causeTemplate": "CTMP004",
            "causeTemplateName": "Help pastors clean gulf",
            "isActive": false,
            "goal": 5000,
            "totalRaised": 120,
            "summary": "test",
            "extendedDescription": "test"
        },
        {...},
    ]
}

```

Returns a list of all causes.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* causeCode (optional) - Filters the list by a partial match on cause code.
* causeTemplate (optional) - Filters the list by a partial match on cause template code.
* project (optional) - Filters the list by a partial match on project.
* account (optional) - Filters the list by an exact match on account number.
* activeOnly (optional) - Filters the list by whether or not the cause is active.
* description (optional) - Filters the list by a partial match on description.

##### Returns

A dictionary with an items property that contains an array of up to limit causes, starting at index offset. Each entry in the array is a separate cause object. If no more causes are available, the resulting array will be empty. This request should never return an error.

### Cause Attachments

#### Create a cause attachment

```
DEFINITION
POST http://apiserver/cause/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "2",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new cause attachment.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a cause attachment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause attachment

```
DEFINITION
GET http://apiserver/cause/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/attachments/2");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "2",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing cause attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the media network attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

#### Update a cause attachment

```
DEFINITION
POST http://apiserver/cause/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/attachments/2", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "2",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified cause attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the cause attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause attachment

```
DEFINITION
DELETE http://apiserver/cause/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/cause/D10D0001/attachments/2", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the cause attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause attachment does not exist, this call returns an error.

#### List all cause attachments

```
DEFINITION
GET http://apiserver/cause/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/attachments");

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
            "id": "2",
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

Returns a list of all cause attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit cause attachments, starting at index offset. Each entry in the array is a separate cause attachment object. If no more cause attachments are available, the resulting array will be empty. This request should never return an error.

### Cause Codes

#### Create a cause code

```
DEFINITION
POST http://apiserver/cause/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/codes", {
    "type": "CAUSCOD1",
    "value": "VALUE1"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSCOD1",
    "typeDescription": null,
    "value": "VALUE1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Creates a new cause code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a cause code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause code

```
DEFINITION
GET http://apiserver/cause/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/codes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSCOD1",
    "typeDescription": "Cause Code 1",
    "value": "VALUE1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Retrieves the details of an existing cause code. You need only supply the id.

##### Arguments

* id (required) - The id of the cause code to be retrieved.

#### Update a cause code

```
DEFINITION
POST http://apiserver/cause/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/codes/1", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSCOD1",
    "typeDescription": "Cause Code 1",
    "value": "VALUE1",
    "valueDescription": "Value 1",
    "isActive": false
}


```

Updates the specified cause code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the cause code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause code

```
DEFINITION
DELETE http://apiserver/cause/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/cause/D10D0001/codes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause code. It cannot be undone.

##### Arguments

* id (required) - The id of the cause code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause code does not exist, this call returns an error.

#### List all cause codes

```
DEFINITION
GET http://apiserver/cause/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/codes");

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
            "type": "CAUSCOD1",
            "typeDescription": "Cause Code 1",
            "value": "VALUE1",
            "valueDescription": "Value 1",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all cause codes.

##### Returns

A dictionary with an items property that contains an array of up to limit cause codes, starting at index offset. Each entry in the array is a separate cause code object. If no more cause codes are available, the resulting array will be empty. This request should never return an error.

### Cause Dates

#### Create a cause date

```
DEFINITION
POST http://apiserver/cause/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/dates", {
    "type": "CAUSECREDT",
    "value": "2011-10-14"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "CAUSECREDT",
    "typeDescription": null,
    "value": "2011-10-14",
    "isActive": true
}

```

Creates a new cause date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a cause date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause date

```
DEFINITION
GET http://apiserver/cause/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/dates/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "CAUSECREDT",
    "typeDescription": "Cause Created Date",
    "value": "2011-10-14",
    "isActive": true
}

```

Retrieves the details of an existing cause date. You need only supply the id.

##### Arguments

* id (required) - The id of the cause date to be retrieved.

#### Update a cause date

```
DEFINITION
POST http://apiserver/cause/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/dates/5", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "CAUSECREDT",
    "typeDescription": "Cause Created Date",
    "value": "2011-10-14",
    "isActive": false
}


```

Updates the specified cause date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the cause date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause date

```
DEFINITION
DELETE http://apiserver/cause/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/cause/D10D0001/dates/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause date. It cannot be undone.

##### Arguments

* id (required) - The id of the cause date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause date does not exist, this call returns an error.

#### List all cause dates

```
DEFINITION
GET http://apiserver/cause/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5",
            "type": "CAUSECREDT",
            "typeDescription": "Cause Created Date",
            "value": "2011-10-14",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all cause dates.

##### Returns

A dictionary with an items property that contains an array of up to limit cause dates, starting at index offset. Each entry in the array is a separate cause date object. If no more cause dates are available, the resulting array will be empty. This request should never return an error.

### Cause Notes

#### Create a cause note

```
DEFINITION
POST http://apiserver/cause/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/notes", {
    "type": "CAUSENOTE1",
    "shortComment": "Info about cause can be found on website"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "CAUSENOTE1",
    "typeDescription": null,
    "shortComment": "Info about cause can be found on website",
    "longComment": null
}

```

Creates a new cause note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a cause note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause note

```
DEFINITION
GET http://apiserver/cause/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/notes/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "CAUSENOTE1",
    "typeDescription": "Cause Note 1",
    "shortComment": "Info about cause can be found on website",
    "longComment": null
}

```

Retrieves the details of an existing cause note. You need only supply the id.

##### Arguments

* id (required) - The id of the cause note to be retrieved.

#### Update a cause note

```
DEFINITION
POST http://apiserver/cause/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/notes/3", {
    "longComment": "http://urlurlurl.example.donordirect.com"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "type": "CAUSENOTE1",
    "typeDescription": "Cause Note 1",
    "shortComment": "Info about cause can be found on website",
    "longComment": "http://urlurlurl.example.donordirect.com"
}


```

Updates the specified cause note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the cause note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause note

```
DEFINITION
DELETE http://apiserver/cause/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/cause/D10D0001/notes/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause note. It cannot be undone.

##### Arguments

* id (required) - The id of the cause note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause note does not exist, this call returns an error.

#### List all cause notes

```
DEFINITION
GET http://apiserver/cause/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "type": "CAUSENOTE1",
            "typeDescription": "Cause Note 1",
            "shortComment": "Info about cause can be found on website",
            "longComment": "http://urlurlurl.example.donordirect.com"
        },
        {...},
    ]
}

```

Returns a list of all cause notes.

##### Returns

A dictionary with an items property that contains an array of up to limit cause notes, starting at index offset. Each entry in the array is a separate cause note object. If no more cause notes are available, the resulting array will be empty. This request should never return an error.

### Cause Numbers

#### Create a cause number

```
DEFINITION
POST http://apiserver/cause/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/numbers", {
    "type": "CAUSEVIEWS",
    "value": 0
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSEVIEWS",
    "typeDescription": null,
    "value": 0,
    "isActive": true
}

```

Creates a new cause number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a cause number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause number

```
DEFINITION
GET http://apiserver/cause/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/numbers/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSEVIEWS",
    "typeDescription": "Cause Views",
    "value": 0,
    "isActive": true
}

```

Retrieves the details of an existing cause number. You need only supply the id.

##### Arguments

* id (required) - The id of the cause number to be retrieved.

#### Update a cause number

```
DEFINITION
POST http://apiserver/cause/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/cause/D10D0001/numbers/1", {
    "value": 100
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSEVIEWS",
    "typeDescription": "Cause Views",
    "value": 100,
    "isActive": true
}


```

Updates the specified cause number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the cause number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause number

```
DEFINITION
DELETE http://apiserver/cause/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/cause/D10D0001/numbers/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause number. It cannot be undone.

##### Arguments

* id (required) - The id of the cause number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause number does not exist, this call returns an error.

#### List all cause numbers

```
DEFINITION
GET http://apiserver/cause/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/cause/D10D0001/numbers");

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
            "type": "CAUSEVIEWS",
            "typeDescription": "Cause Views",
            "value": 100,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all cause numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit cause numbers, starting at index offset. Each entry in the array is a separate cause number object. If no more cause numbers are available, the resulting array will be empty. This request should never return an error.

### Cause Templates

#### Create a cause template

```
DEFINITION
POST http://apiserver/causetemplates

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates", {
    "id": "CTMP004",
    "elementGroup": "D10D",
    "type": "GENERAL"
});

EXAMPLE RESPONSE
{
    "id": "CTMP004",
    "elementGroup": "D10D",
    "elementGroupDescription": "Direct Mail Appeal 2010 April",
    "type": "GENERAL",
    "typeDescription": "General Fund Causes Type",
    "project": null,
    "projectDescription": null,
    "isActive": true,
    "name": null,
    "description": null,
    "shortCommentSection1": null,
    "longCommentSection1": null,
    "imageSection1": null,
    "shortCommentSection2": null,
    "longCommentSection2": null,
    "imageSection2": null,
    "shortCommentSection3": null,
    "longCommentSection3": null,
    "imageSection3": null,
    "shortCommentSection4": null,
    "longCommentSection4": null,
    "imageSection4": null
}

```

Creates a new cause template.

##### Arguments

* id (required) - The Cause Template Code for the cause template. Must be unique.
* elementGroup (required) - The element group for the cause template. Must be a valid `DDCELEMENT` element group.
* type (required) - The type of the cause template. Must be a valid `SOCAUSES` code.
* project (optional) - The project code for the cause template. Must be a valid `DDCPROJ` project.
* isActive (optional : default true) - Indicates whether the cause template is active.
* name (optional) - The name of the cause template.
* description (optional) - The description of the cause template.
* shortCommentSection1 (optional) - A short comment for section 1 of the cause.
* longCommentSection1 (optional) - A long comment for section 1 of the cause.
* imageSection1 (optional) - A file address to an image for section 1 of the cause.
* shortCommentSection2 (optional) - A short comment for section 2 of the cause.
* longCommentSection2 (optional) - A long comment for section 2 of the cause.
* imageSection2 (optional) - A file address to an image for section 2 of the cause.
* shortCommentSection3 (optional) - A short comment for section 3 of the cause.
* longCommentSection3 (optional) - A long comment for section 3 of the cause.
* imageSection3 (optional) - A file address to an image for section 3 of the cause.
* shortCommentSection4 (optional) - A short comment for section 4 of the cause.
* longCommentSection4 (optional) - A long comment for section 4 of the cause.
* imageSection4 (optional) - A file address to an image for section 4 of the cause.

##### Returns

Returns a cause template object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause template

```
DEFINITION
GET http://apiserver/causetemplates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004");

EXAMPLE RESPONSE
{
    "id": "CTMP004",
    "elementGroup": "D10D",
    "elementGroupDescription": "Direct Mail Appeal 2010 April",
    "type": "GENERAL",
    "typeDescription": "General Fund Causes Type",
    "project": null,
    "projectDescription": null,
    "isActive": true,
    "name": null,
    "description": null,
    "shortCommentSection1": null,
    "longCommentSection1": null,
    "imageSection1": null,
    "shortCommentSection2": null,
    "longCommentSection2": null,
    "imageSection2": null,
    "shortCommentSection3": null,
    "longCommentSection3": null,
    "imageSection3": null,
    "shortCommentSection4": null,
    "longCommentSection4": null,
    "imageSection4": null
}

```

Retrieves the details of an existing cause template. You need only supply the id.

##### Arguments

* id (required) - The id of the cause template to be retrieved.

#### Update a cause template

```
DEFINITION
POST http://apiserver/causetemplates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004", {
    "type": "SUPPORT",
    "project": "110115",
    "name": "Help pastors clean gulf"
});

EXAMPLE RESPONSE
{
    "id": "CTMP004",
    "elementGroup": "D10D",
    "elementGroupDescription": "Direct Mail Appeal 2010 April",
    "type": "SUPPORT",
    "typeDescription": "Support a Pastor Cause Type",
    "project": "110115",
    "projectDescription": "Gulf Oil Spill Relief",
    "isActive": true,
    "name": "Help pastors clean gulf",
    "description": null,
    "shortCommentSection1": null,
    "longCommentSection1": null,
    "imageSection1": null,
    "shortCommentSection2": null,
    "longCommentSection2": null,
    "imageSection2": null,
    "shortCommentSection3": null,
    "longCommentSection3": null,
    "imageSection3": null,
    "shortCommentSection4": null,
    "longCommentSection4": null,
    "imageSection4": null
}


```

Updates the specified cause template by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The type of the cause template. Must be a valid `SOCAUSES` code.
* project (optional) - The project code for the cause template. Must be a valid `DDCPROJ` project.
* isActive (optional) - Indicates whether the cause template is active.
* name (optional) - The name of the cause template.
* description (optional) - The description of the cause template.
* shortCommentSection1 (optional) - A short comment for section 1 of the cause.
* longCommentSection1 (optional) - A long comment for section 1 of the cause.
* imageSection1 (optional) - A file address to an image for section 1 of the cause.
* shortCommentSection2 (optional) - A short comment for section 2 of the cause.
* longCommentSection2 (optional) - A long comment for section 2 of the cause.
* imageSection2 (optional) - A file address to an image for section 2 of the cause.
* shortCommentSection3 (optional) - A short comment for section 3 of the cause.
* longCommentSection3 (optional) - A long comment for section 3 of the cause.
* imageSection3 (optional) - A file address to an image for section 3 of the cause.
* shortCommentSection4 (optional) - A short comment for section 4 of the cause.
* longCommentSection4 (optional) - A long comment for section 4 of the cause.
* imageSection4 (optional) - A file address to an image for section 4 of the cause.

##### Returns

Returns the cause template object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause template

```
DEFINITION
DELETE http://apiserver/causetemplates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/causetemplates/CTMP004", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause template. It cannot be undone.

##### Arguments

* id (required) - The id of the cause template to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause template does not exist, this call returns an error.

#### List all cause templates

```
DEFINITION
GET http://apiserver/causetemplates

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates?type=SUP");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "CTMP004",
            "elementGroup": "D10D",
            "elementGroupDescription": "Direct Mail Appeal 2010 April",
            "type": "SUPPORT",
            "typeDescription": "Support a Pastor Cause Type",
            "project": "110115",
            "projectDescription": "Gulf Oil Spill Relief",
            "isActive": true,
            "name": "Help pastors clean gulf",
            "description": null,
            "shortCommentSection1": null,
            "longCommentSection1": null,
            "imageSection1": null,
            "shortCommentSection2": null,
            "longCommentSection2": null,
            "imageSection2": null,
            "shortCommentSection3": null,
            "longCommentSection3": null,
            "imageSection3": null,
            "shortCommentSection4": null,
            "longCommentSection4": null,
            "imageSection4": null
        },
        {...},
    ]
}

```

Returns a list of all cause templates.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* causeTemplateCode (optional) - Filter list on partial match of cause template code.
* type (optional) - Filter list on partial match of cause template type.
* project (optional) - Filter list on partial match of cause template project code.
* elementGroup (optional) - Filter list on partial match of cause template element group.
* activeOnly (optional) - Filter list based on whether cause template is active. Use true to return only active cause templates.

##### Returns

A dictionary with an items property that contains an array of up to limit cause templates, starting at index offset. Each entry in the array is a separate cause template object. If no more cause templates are available, the resulting array will be empty. This request should never return an error.

### Cause Template Attachments

#### Create a cause template attachment

```
DEFINITION
POST http://apiserver/causetemplates/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "14",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new cause template attachment.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a cause template attachment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause template attachment

```
DEFINITION
GET http://apiserver/causetemplates/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/attachments/14");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "14",
    "type": "IMAGE",
    "typeDescription": "Just a plain old image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing cause template attachment. You need only supply the id.

##### Arguments

* id (required) - The id of the media network attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

#### Update a cause template attachment

```
DEFINITION
POST http://apiserver/causetemplates/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/attachments/14", {
    "type": "OTHER"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "14",
    "type": "OTHER",
    "typeDescription": "Other",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified cause template attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the cause template attachment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause template attachment

```
DEFINITION
DELETE http://apiserver/causetemplates/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/causetemplates/CTMP004/attachments/7", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause template attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the cause template attachment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause template attachment does not exist, this call returns an error.

#### List all cause template attachments

```
DEFINITION
GET http://apiserver/causetemplates/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/attachments");

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
            "id": "14",
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

Returns a list of all cause template attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit cause template attachments, starting at index offset. Each entry in the array is a separate cause template attachment object. If no more cause template attachments are available, the resulting array will be empty. This request should never return an error.

### Cause Template Codes

#### Create a cause template code

```
DEFINITION
POST http://apiserver/causetemplates/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/codes", {
    "type": "CAUSCOD1",
    "value": "VALUE1"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSCOD1",
    "typeDescription": null,
    "value": "VALUE1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Creates a new cause template code.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a cause template code object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause template code

```
DEFINITION
GET http://apiserver/causetemplates/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/codes/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSCOD1",
    "typeDescription": "Cause Code 1",
    "value": "VALUE1",
    "valueDescription": "Value 1",
    "isActive": true
}

```

Retrieves the details of an existing cause template code. You need only supply the id.

##### Arguments

* id (required) - The id of the cause template code to be retrieved.

#### Update a cause template code

```
DEFINITION
POST http://apiserver/causetemplates/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/codes/1", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSCOD1",
    "typeDescription": "Cause Code 1",
    "value": "VALUE1",
    "valueDescription": "Value 1",
    "isActive": false
}


```

Updates the specified cause template code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the cause template code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause template code

```
DEFINITION
DELETE http://apiserver/causetemplates/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/causetemplates/CTMP004/codes/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause template code. It cannot be undone.

##### Arguments

* id (required) - The id of the cause template code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause template code does not exist, this call returns an error.

#### List all cause template codes

```
DEFINITION
GET http://apiserver/causetemplates/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/codes");

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
            "type": "CAUSCOD1",
            "typeDescription": "Cause Code 1",
            "value": "VALUE1",
            "valueDescription": "Value 1",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all cause template codes.

##### Returns

A dictionary with an items property that contains an array of up to limit cause template codes, starting at index offset. Each entry in the array is a separate cause template code object. If no more cause template codes are available, the resulting array will be empty. This request should never return an error.

### Cause Template Dates

#### Create a cause template date

```
DEFINITION
POST http://apiserver/causetemplates/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/dates", {
    "type": "CAUSECREDT",
    "value": "2011-10-14"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "CAUSECREDT",
    "typeDescription": null,
    "value": "2011-10-14",
    "isActive": true
}

```

Creates a new cause template date.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a cause template date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause template date

```
DEFINITION
GET http://apiserver/causetemplates/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/dates/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "CAUSECREDT",
    "typeDescription": "Cause Created Date",
    "value": "2011-10-14",
    "isActive": true
}

```

Retrieves the details of an existing cause template date. You need only supply the id.

##### Arguments

* id (required) - The id of the cause template date to be retrieved.

#### Update a cause template date

```
DEFINITION
POST http://apiserver/causetemplates/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/dates/5", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "5",
    "type": "CAUSECREDT",
    "typeDescription": "Cause Created Date",
    "value": "2011-10-14",
    "isActive": false
}


```

Updates the specified cause template date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the cause template date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause template date

```
DEFINITION
DELETE http://apiserver/causetemplates/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/causetemplates/CTMP004/dates/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause template date. It cannot be undone.

##### Arguments

* id (required) - The id of the cause template date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause template date does not exist, this call returns an error.

#### List all cause template dates

```
DEFINITION
GET http://apiserver/causetemplates/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "5",
            "type": "CAUSECREDT",
            "typeDescription": "Cause Created Date",
            "value": "2011-10-14",
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all cause template dates.

##### Returns

A dictionary with an items property that contains an array of up to limit cause template dates, starting at index offset. Each entry in the array is a separate cause template date object. If no more cause template dates are available, the resulting array will be empty. This request should never return an error.

### Cause Template Notes

#### Create a cause template note

```
DEFINITION
POST http://apiserver/causetemplates/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/notes", {
    "type": "CAUSENOTE1",
    "shortComment": "Info about cause can be found on website"
});

EXAMPLE RESPONSE
{
    "id": "103",
    "type": "CAUSENOTE1",
    "typeDescription": null,
    "shortComment": "Info about cause can be found on website",
    "longComment": null
}

```

Creates a new cause template note.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a cause template note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause template note

```
DEFINITION
GET http://apiserver/causetemplates/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/notes/103");

EXAMPLE RESPONSE
{
    "id": "103",
    "type": "CAUSENOTE1",
    "typeDescription": "Cause Note 1",
    "shortComment": "Info about cause can be found on website",
    "longComment": null
}

```

Retrieves the details of an existing cause template note. You need only supply the id.

##### Arguments

* id (required) - The id of the cause template note to be retrieved.

#### Update a cause template note

```
DEFINITION
POST http://apiserver/causetemplates/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/notes/103", {
    "longComment": "http://urlurlurl.example.donordirect.com"
});

EXAMPLE RESPONSE
{
    "id": "103",
    "type": "CAUSENOTE1",
    "typeDescription": "Cause Note 1",
    "shortComment": "Info about cause can be found on website",
    "longComment": "http://urlurlurl.example.donordirect.com"
}


```

Updates the specified cause template note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the cause template note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause template note

```
DEFINITION
DELETE http://apiserver/causetemplates/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/causetemplates/CTMP004/notes/103", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause template note. It cannot be undone.

##### Arguments

* id (required) - The id of the cause template note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause template note does not exist, this call returns an error.

#### List all cause template notes

```
DEFINITION
GET http://apiserver/causetemplates/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "103",
            "type": "CAUSENOTE1",
            "typeDescription": "Cause Note 1",
            "shortComment": "Info about cause can be found on website",
            "longComment": "http://urlurlurl.example.donordirect.com"
        },
        {...},
    ]
}

```

Returns a list of all cause template notes.

##### Returns

A dictionary with an items property that contains an array of up to limit cause template notes, starting at index offset. Each entry in the array is a separate cause template note object. If no more cause template notes are available, the resulting array will be empty. This request should never return an error.

### Cause Template Numbers

#### Create a cause template number

```
DEFINITION
POST http://apiserver/causetemplates/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/numbers", {
    "type": "CAUSEVIEWS",
    "value": 0
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSEVIEWS",
    "typeDescription": null,
    "value": 0,
    "isActive": true
}

```

Creates a new cause template number.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a cause template number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a cause template number

```
DEFINITION
GET http://apiserver/causetemplates/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/numbers/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSEVIEWS",
    "typeDescription": "Cause Views",
    "value": 0,
    "isActive": true
}

```

Retrieves the details of an existing cause template number. You need only supply the id.

##### Arguments

* id (required) - The id of the cause template number to be retrieved.

#### Update a cause template number

```
DEFINITION
POST http://apiserver/causetemplates/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/causetemplates/CTMP004/numbers/1", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1",
    "type": "CAUSEVIEWS",
    "typeDescription": "Cause Views",
    "value": 0,
    "isActive": false
}


```

Updates the specified cause template number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the cause template number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a cause template number

```
DEFINITION
DELETE http://apiserver/causetemplates/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/causetemplates/CTMP004/numbers/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cause template number. It cannot be undone.

##### Arguments

* id (required) - The id of the cause template number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the cause template number does not exist, this call returns an error.

#### List all cause template numbers

```
DEFINITION
GET http://apiserver/causetemplates/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/causetemplates/CTMP004/numbers");

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
            "type": "CAUSEVIEWS",
            "typeDescription": "Cause Views",
            "value": 0,
            "isActive": false
        },
        {...},
    ]
}

```

Returns a list of all cause template numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit cause template numbers, starting at index offset. Each entry in the array is a separate cause template number object. If no more cause template numbers are available, the resulting array will be empty. This request should never return an error.

### Charitable Values

#### Create a charitable value

```
DEFINITION
POST http://apiserver/charitablevalues

EXAMPLE REQUEST
$.post("http://localhost:49195/charitablevalues", {
    "start": "2013-01-01",
    "end": "2013-12-31",
    "lowCostAmount": 10,
    "minimumValueAmount": 52,
    "otherInsubstantialBenefit": 105
});

EXAMPLE RESPONSE
{
    "id": "5",
    "start": "2013-01-01",
    "end": "2013-12-31",
    "lowCostAmount": 10,
    "minimumValueAmount": 52,
    "otherInsubstantialBenefit": 105
}

```

Creates a new charitable value.

##### Arguments

* start (required) - The start date for the charitable value.
* end (required) - The end date for the charitable value.
* lowCostAmount (required) - The low cost amount (money) for the charitable value.
* minimumValueAmount (required) - The minimum value amount (money) for the charitable value.
* otherInsubstantialBenefit (required) - The other insubstantial benefit (money) for the charitable value.

##### Returns

Returns a charitable value object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a charitable value

```
DEFINITION
GET http://apiserver/charitablevalues/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/charitablevalues/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "start": "2013-01-01",
    "end": "2013-12-31",
    "lowCostAmount": 10,
    "minimumValueAmount": 52,
    "otherInsubstantialBenefit": 105
}

```

Retrieves the details of an existing charitable value. You need only supply the id.

##### Arguments

* id (required) - The id of the charitable value to be retrieved.

#### Update a charitable value

```
DEFINITION
POST http://apiserver/charitablevalues/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/charitablevalues/5", {
    "minimumValueAmount": 52.50
});

EXAMPLE RESPONSE
{
    "id": "5",
    "start": "2013-01-01",
    "end": "2013-12-31",
    "lowCostAmount": 10,
    "minimumValueAmount": 52.5,
    "otherInsubstantialBenefit": 105
}


```

Updates the specified charitable value by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* start (optional) - The start date for the charitable value.
* end (optional) - The end date for the charitable value.
* lowCostAmount (optional) - The low cost amount (money) for the charitable value.
* minimumValueAmount (optional) - The minimum value amount (money) for the charitable value.
* otherInsubstantialBenefit (optional) - The other insubstantial benefit (money) for the charitable value.

##### Returns

Returns the charitable value object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a charitable value

```
DEFINITION
DELETE http://apiserver/charitablevalues/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/charitablevalues/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a charitable value. It cannot be undone.

##### Arguments

* id (required) - The id of the charitable value to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the charitable value does not exist, this call returns an error.

#### List all charitable values

```
DEFINITION
GET http://apiserver/charitablevalues

EXAMPLE REQUEST
$.get("http://localhost:49195/charitablevalues?start=2015-01-01");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "1",
            "start": "2015-01-01",
            "end": "2015-12-31",
            "lowCostAmount": 10.5,
            "minimumValueAmount": 52.5,
            "otherInsubstantialBenefit": 105
        },
        {...},
    ]
}

```

Returns a list of all charitable values.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* start (optional) - The start date of the charitable values to retrieve.
* end (optional) - The end date of the charitable values to retrieve.

##### Returns

A dictionary with an items property that contains an array of up to limit charitable values, starting at index offset. Each entry in the array is a separate charitable value object. If no more charitable values are available, the resulting array will be empty. This request should never return an error.

### Conversion Rates

#### Create a conversion rate

```
DEFINITION
POST http://apiserver/conversionrates

EXAMPLE REQUEST
$.post("http://localhost:49195/conversionrates", {
    "currencyCode": "EUR",
    "conversionRate": 0.69002,
    "asOfDate": "2015-01-04"
});

EXAMPLE RESPONSE
{
    "id": "1",
    "currencyCode": "EUR",
    "currencyCodeDescription": "Euro",
    "conversionRate": 0.69002,
    "asOfDate": "2015-01-04"
}

```

##### Arguments

* currencyCode (required) - The currency code of the conversion rate.
* rate (required) - The decimal rate of the conversion rate.
* asOfDate (required) - The exact asOfDate of the conversion rate.

##### Returns

Returns conversion rate object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a conversion rate

```
DEFINITION
GET http://apiserver/conversionrates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/conversionrates/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "currencyCode": "EUR",
    "currencyCodeDescription": "Euro",
    "conversionRate": 0.69002,
    "asOfDate": "2015-01-04"
}

```

Retrieves the details of an existing conversion rate. You need only supply the conversion rate id.

##### Returns

Returns conversion rate object if a valid id was provided.

#### Update a conversion rate

```
DEFINITION
POST http://apiserver/conversionrates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/conversionrates/1", {
        "conversionRate": 0.70172,
});

EXAMPLE RESPONSE
{
    "id": "1",
    "currencyCode": "EUR",
    "currencyCodeDescription": "Euro",
    "conversionRate": 0.70172,
    "asOfDate": "2015-01-04T00:00:00"
}

```

##### Arguments

* currencyCode (optional) - The currency code of the conversion rate.
* rate (optional) - The decimal rate of the conversion rate.
* asOfDate (optional) - The exact asOfDate of the conversion rate.

##### Returns

Returns conversion rate object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a conversion rate

```
DEFINITION
DELETE http://apiserver/conversionrates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/conversionrates/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes conversion rate. It cannot be undone.

##### Arguments

* id (required) - The id of the conversion rate to be deleted.

##### Returns

Returns a 204 No Content response on success. If the conversion rate id does not exist, this call returns an error.

#### List all conversion rates

```
DEFINITION
GET http://apiserver/conversionrates

EXAMPLE REQUEST
$.get("http://localhost:49195/conversionrates?currencyCode=EUR");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "1",
            "currencyCode": "EUR",
            "currencyCodeDescription": "Euro",
            "conversionRate": 0.70172,
            "asOfDate": "2015-01-04T00:00:00"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all conversion rates.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* currencyCode (optional) - The currency code of the conversion rates to retrieve.
* asOfDate (optional) - The exact asOfDate of the conversion rates to retrieve.

##### Returns

A dictionary with an items property that contains an array of up to limit conversion rates, starting at index offset. Each entry in the array is a separate conversion rate object. If no more conversion rates are available, the resulting array will be empty. This request should never return an error.

### Deposits

#### Create a deposit

```
DEFINITION
POST http://apiserver/deposits

EXAMPLE REQUEST
$.post("http://localhost:49195/deposits", {
    "company": "010",
    "controlAmount": 1999.00,
    "conversionRate": 1,
    "currency": "USD",
    "bank": "BOA",
    "batches": [],
    "description": "Online Transaction",
    "date": "2014-05-11",
    "type": "M",
    "status": "Y",
    "glDate": "2014-05-11",
    "shouldAutoPostJE": true,
    "journalReference": 0,
    "paymentGatewayCode": "CCONNECT"
});

EXAMPLE RESPONSE
{
    "id": 214455,
    "company": "010",
    "controlAmount": 1999.00,
    "conversionRate": 1,
    "currency": "USD",
    "bank": "BOA",
    "description": "Online Transaction",
    "date": "2014-05-11",
    "type": "M",
    "batches": [],
    "status": "Y",
    "glDate": "2014-05-11",
    "shouldAutoPostJE": true,
    "journalReference": 0,
    "declineAmount": 0,
    "amount": 0,
    "declineAmout": 0,
    "cancelAmount": 0,
    "companyDescription": "DDC Company",
    "bankDescription": "Bank of America",
    "currencyDescription": "US Dollars",
    "statusDescription": "available",
    "typeDescription": "Manually created",
    "paymentGatewayCode": "CCONNECT",
    "paymentGatewayDescription": "Clover Connect"
}

```

Creates a new deposit object.

##### Arguments

* company (required) - The company code of the deposit.
* controlAmount (required) - The control amount rate of the deposit.
* conversionRate (required) - The conversion rate of the deposit.
* bank (required) - The bank code of the deposit.
* description (optional) - The description of the deposit.
* date (optional) - The date of the deposit.
* type (optional) - The type of the deposit, will default to `M`.
* batches (optional) - An array of batch ids for the deposit.
* status (optional) - The status of the deposit.
* glDate (optional) - The general ledger date of the deposit.
* shouldAutoPostJE (optional) - Whether or not to auto post journal entry for the deposit, will default to false.
* paymentGatewayCode (optional) - The code of the company payment gateway to be used for CC and EFT payment types.

##### Returns

Returns a deposit object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid deposit type or an undefined deposit status).

#### Retrieve a deposit

```
DEFINITION
GET http://apiserver/deposits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/deposits/214455");

EXAMPLE RESPONSE
{
    "id": 214455,
    "company": "010",
    "controlAmount": 1999.00,
    "conversionRate": 1,
    "bank": "BOA",
    "description": "Online Transaction",
    "date": "2014-05-11",
    "type": "M",
    "batches": [],
    "status": "Y",
    "glDate": "2014-05-11",
    "shouldAutoPostJE": true,
    "journalReference": 0,
    "declineAmount": 0,
    "amount": 0,
    "currency": "USD",
    "declineAmout": 0,
    "cancelAmount": 0,
    "companyDescription": "DDC Company",
    "bankDescription": "Bank of America",
    "currencyDescription": "US Dollars",
    "statusDescription": "available",
    "typeDescription": "Manually created",
    "paymentGatewayCode": "CCONNECT",
    "paymentGatewayDescription": "Clover Connect"
}

```

Retrieves the details of an existing deposit. You need only supply the deposit id.

##### Arguments

* id (required) - The deposit id of the deposit to retrieve.

##### Returns

Returns a deposit object if a valid id was provided.

#### Update a deposit

```
DEFINITION
POST http://apiserver/deposits/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/deposits/214455, {
    "batches": ["17098"]
});

EXAMPLE RESPONSE
{
    "id": 214455,
    "company": "010",
    "controlAmount": 1999.00,
    "conversionRate": 1,
    "bank": "BOA",
    "description": "Online Transaction",
    "date": "2014-05-11",
    "type": "M",
    "batches": ["17098"],
    "status": "Y",
    "glDate": "2014-05-11",
    "shouldAutoPostJE": true,
    "journalReference": 0,
    "declineAmount": 0,
    "amount": 0,
    "currency": "USD",
    "declineAmout": 0,
    "cancelAmount": 0,
    "companyDescription": "DDC Company",
    "bankDescription": "Bank of America",
    "currencyDescription": "US Dollars",
    "statusDescription": "available",
    "typeDescription": "Manually created",
    "paymentGatewayCode": "CCONNECT",
    "paymentGatewayDescription": "Clover Connect"
}


```

Updates the specified deposit by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* company (optional) - The company code of the deposit.
* controlAmount (optional) - The control amount rate of the deposit.
* conversionRate (optional) - The conversion rate of the deposit.
* bank (optional) - The bank code of the deposit.
* description (optional) - The description of the deposit.
* date (optional) - The date of the deposit.
* type (optional) - The type of the deposit.
* batches (optional) - An array of batch ids for the deposit.
* status (optional) - The status of the deposit.
* glDate (optional) - The general ledger date of the deposit.
* shouldAutoPostJE (optional) - Whether or not to auto post journal entry for the deposit.
* paymentGatewayCode (optional) - The code of the company payment gateway to be used for CC and EFT payment types.

##### Returns

Returns the deposit object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid deposit type or an undefined deposit status).

#### Delete a deposit

```
DEFINITION
DELETE http://apiserver/deposits/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/deposits/214455", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a deposit. It cannot be undone.

##### Arguments

* id (required) - The deposit id of the deposit to be deleted.

##### Returns

Returns a 204 No Content response on success. If the deposit id does not exist or any transactions that reference it, this call returns an error.

#### List all deposits

```
DEFINITION
GET http://apiserver/deposits

EXAMPLE REQUEST
$.get("http://localhost:49195/deposits?status=C");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 479
    }
    "items": [
        {
            "id": 214455,
            "company": "010",
            "controlAmount": 1999.00,
            "conversionRate": 1,
            "bank": "BOA",
            "description": "Online Transaction",
            "date": "2014-05-11",
            "type": "M",
            "batches": [],
            "status": "C",
            "glDate": "2014-05-11",
            "shouldAutoPostJE": true,
            "journalReference": 0,
            "declineAmount": 0,
            "amount": 1999.00,
            "currency": "USD",
            "declineAmout": 0,
            "cancelAmount": 0,
            "companyDescription": "DDC Company",
            "bankDescription": "Bank of America",
            "currencyDescription": "US Dollars",
            "statusDescription": "available",
            "typeDescription": "Manually created",
            "paymentGatewayCode": "CCONNECT",
            "paymentGatewayDescription": "Clover Connect"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all deposits matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in deposit id
* status () - Filter list by partial match in deposit status
* type () - Filter list by partial match in deposit type
* date () - Filter list by partial match in deposit date
* glDate () - Filter list by partial match in deposit general ledger date
* journalReference () - Filter list by partial match in deposit journal reference
* company () - Filter list by partial match in deposit company
* bank () - Filter list by partial match in deposit bank
* currency () - Filter list by partial match in deposit currency

##### Returns

A dictionary with an items property that contains an array of up to limit deposits, starting at index offset. Each entry in the array is a separate deposit object. If no more deposits are available, the resulting array will be empty. This request should never return an error.

#### Complete a deposit

```
DEFINITION
POST http://apiserver/deposits/:id/complete

EXAMPLE REQUEST
$.post("http://localhost:49195/deposits/214455/complete", {controlamountoverride: true});

EXAMPLE RESPONSE
200 OK

```

Completes a deposit. It cannot be undone.

##### Arguments

* id (required) - The deposit id of the deposit to be completed.

##### Returns

Returns a 200 OK response on success and updates the status of the deposit to `C`. If the deposit id does not exist, this call returns an error.

#### Post a deposit

```
DEFINITION
POST http://apiserver/deposits/:id/post

EXAMPLE REQUEST
$.post("http://localhost:49195/deposits/214455/post");

EXAMPLE RESPONSE
200 OK

```

Posts a deposit.

##### Arguments

* id (required) - The deposit id of the deposit to be completed

##### Returns

Returns a 200 OK response on success and updates the status of the deposit to `P`. If the deposit id does not exist, this call returns an error.

#### Get Actual Amount of Deposit

```
DEFINITION
GET http://apiserver/deposits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/deposits/214455/actualamount");

EXAMPLE RESPONSE
{
    "actualAmount": 25
}

```

Retrieves the actual amount of the deposit. You need only supply the deposit id.

##### Arguments

* id (required) - The deposit id of the deposit to retrieve the actual amount.

##### Returns

Returns an object that contains the actual amount of the deposit.

### Deposit Batches

#### Create a deposit batch

```
DEFINITION
POST http://apiserver/deposits/:id/batches

EXAMPLE REQUEST
$.post("http://localhost:49195/deposits/4246/batches", {
    "id": "7159"
});

EXAMPLE RESPONSE
{
    "id": "7159",
    "type": "S",
    "batchDate": "2014-11-18",
    "closeDate": "2014-11-18",
    "actualAmount": 25,
    "actualNumber": 1,
    "category": null,
    "categoryDescription": null,
    "currency": "USD",
    "currencyDescription": "US Dollars",
    "defaultPaymentType": "CA",
    "defaultPaymentTypeDescription": "Cash",
    "numberTransactionsOnHold": 0
}

```

Creates a new deposit batch object

##### Arguments

* id (required) - The batch number. (This is the batch number of the batch for the deposit batch. It must be a valid batch number.)

##### Returns

Returns a deposit batch object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined batch number).

#### Retrieve a deposit batch

```
DEFINITION
GET http://apiserver/deposits/:id/batches/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/deposits/4246/batches/7159");

EXAMPLE RESPONSE
{
    "id": "7159",
    "type": "S",
    "batchDate": "2014-11-18",
    "closeDate": "2014-11-18",
    "actualAmount": 25,
    "actualNumber": 1,
    "category": null,
    "categoryDescription": null,
    "currency": "USD",
    "currencyDescription": "US Dollars",
    "defaultPaymentType": "CA",
    "defaultPaymentTypeDescription": "Cash",
    "numberTransactionsOnHold": 0
}

```

Retrieves the details of an existing deposit batch. You need only supply the deposit id and batch number.

##### Returns

Returns a deposit batch object if a valid id was provided.

#### Delete a deposit batch

```
DEFINITION
DELETE http://apiserver/deposits/:id/batches/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/deposits/4246/batches/7159", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a deposit batch. It cannot be undone.

##### Arguments

* id (required) - The id of the deposit batch to be deleted.

##### Returns

Returns a 204 No Content response on success. If the deposit batch id does not exist, this call returns an error.

#### List all deposit batches

```
DEFINITION
GET http://apiserver/deposits/:id/batches

EXAMPLE REQUEST
$.get("http://localhost:49195/deposits/4246/batches");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "7159",
            "type": "S",
            "batchDate": "2014-11-18",
            "closeDate": "2014-11-18",
            "actualAmount": 25,
            "actualNumber": 1,
            "category": null,
            "categoryDescription": null,
            "currency": "USD",
            "currencyDescription": "US Dollars",
            "defaultPaymentType": "CA",
            "defaultPaymentTypeDescription": "Cash",
            "numberTransactionsOnHold": 0
        }
    ]
}

```

Returns a list of all deposit batches.

##### Arguments

* getPageContainingId (optional) - Will return the page of deposit batches that contains the deposit batch with this id.

##### Returns

A dictionary with an items property that contains an array of up to limit deposit batches, starting at index offset. Each entry in the array is a separate deposit batch object. If no more deposit batches are available, the resulting array will be empty. This request should never return an error.

### Deposits EFT Transmission

```
DEFINITION
POST http://apiserver/deposits/efttransmission

EXAMPLE REQUEST
$.post("http://localhost:49195/deposits/efttransmission", {
    "company": "010",
    "paymentGatewayCode": "CCONNECT",
    "conversionRate": 1,
    "bank": "BOA",
    "description": "Online Transaction",
    "date": "2014-05-11",
    "glDate": "2014-05-11",
    "shouldAutoPostJE": true,
    "currency": "USD",
});

EXAMPLE RESPONSE
204 No Content

```

This will begin processing of an EFT Tranmission.

##### Arguments

* bank (optional) - The bank code of the EFT Transmission.
* company (required) - The company code of the EFT Transmission.
* currency (required) - The currency code of the EFT Transmission.
* paymentGatewayCode (optional) - The company payment gateway code of the EFT Transmission. If not provided, EFT Transmission will run on all payment gateways of the company.
* conversionRate (optional) - The conversion rate of the EFT Transmission.
* description (optional) - The description of the EFT Transmission.
* date (optional) - The date of the EFT Transmission.
* glDate (optional) - The general ledger date of the EFT Transmission.
* shouldAutoPostJE (optional) - Whether or not to auto post journal entry for the EFT Transmission.

##### Returns

Returns a 204 No Content response on success.

### Dimensions

#### Create a dimension

```
DEFINITION
POST http://apiserver/dimensions

EXAMPLE REQUEST
$.post("http://localhost:49195/dimensions", {
    "type": "DIMENSIONTYPE",
    "entityType":"Product",
    "codeType":"DDCGLCLASS",
    "isActive": true,
    "dimensionIdNumber": 1291
});

EXAMPLE RESPONSE
{
    "id": "23",
    "type": "DIMENSIONTYPE",
    "entityType":"Product",
    "codeType":"DDCGLCLASS",
    "isActive": true,
    "dimensionIdNumber": 1291
}

```

##### Arguments

* type (required) - The type of dimension.
* entityType (required) - The entity type of the dimension. Possible values are `AccountingControls`, `ElementGroup`, `MediaOutlet`, `Pledge`, `Product`, `Source`.
* codeType (optional) - The code type for the dimension.
  + If entityType is `AccountingControls`, codeType must be an active CodeType in the `ACCTINSTR` category.
  + If entityType is `ElementGroup`, codeType must be a CodeType in the `ELEMNT` category.
  + If entityType is `MediaOutlet`, codeType must be a CodeType in the `MEDIA` category.
  + If entityType is `Pledge`, codeType must be a CodeType in one of the `PLEDGE`, `PLEDGECHLD`, `PLEDGEOTH`, `PLEDGEPROJ`, `PLEDGESTAF` categories.
  + If entityType is `Product`, codeType must be a CodeType in the `PRODUCT` category.
  + If entityType is `Source`, codeType must be a CodeType in the `SOURCE` category.
* isActive (optional) - Whether the dimension is active or not
* dimensionIdNumber (optional) - The Dimension ID Number to be used.

##### Returns

Returns dimension object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a dimension

```
DEFINITION
GET http://apiserver/dimensions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/dimensions/DIMENSIONTYPE");

EXAMPLE RESPONSE
{
    "id": "23",
    "type": "DIMENSIONTYPE",
    "entityType":"Product",
    "codeType":"DDCGLCLASS",
    "isActive": true,
    "dimensionIdNumber": 1291
}

```

Retrieves the details of an existing dimension. You need only supply the dimension id.

##### Returns

Returns dimension object if a valid id was provided.

#### Update a dimension

```
DEFINITION
POST http://apiserver/dimensions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/dimensions/DIMENSIONTYPE", {
    "dimensionIdNumber": 1300
});

EXAMPLE RESPONSE
{
    "id": "23",
    "type": "DIMENSIONTYPE",
    "entityType":"Product",
    "codeType":"DDCGLCLASS",
    "isActive": true,
    "dimensionIdNumber": 1300
}

```

##### Arguments

* type (optional) - The type of dimension.
* entityType (optional) - The entity type of the dimension. Possible values are `AccountingControls`, `ElementGroup`, `MediaOutlet`, `Pledge`, `Product`, `Source`.
* codeType (optional) - The code type for the dimension.
   **If entityType is `AccountingControls`, codeType must be an active CodeType in the `ACCTINSTR` category.** If entityType is `ElementGroup`, codeType must be a CodeType in the `ELEMNT` category.
   **If entityType is `MediaOutlet`, codeType must be a CodeType in the `MEDIA` category.** If entityType is `Pledge`, codeType must be a CodeType in one of the `PLEDGE`, `PLEDGECHLD`, `PLEDGEOTH`, `PLEDGEPROJ`, `PLEDGESTAF` categories.
   **If entityType is `Product`, codeType must be a CodeType in the `PRODUCT` category.** If entityType is `Source`, codeType must be a CodeType in the `SOURCE` category.
* isActive (optional) - Whether the dimension is active or not
* dimensionIdNumber (optional) - The Dimension ID Number to be used.

##### Returns

Returns dimension object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a dimension

```
DEFINITION
DELETE http://apiserver/dimensions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/dimensions/DIMENSIONTYPE", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes dimension. It cannot be undone.

##### Arguments

* id (required) - The id of the dimension to be deleted.

##### Returns

Returns a 204 No Content response on success. If the dimension id does not exist, this call returns an error.

#### List all dimensions

```
DEFINITION
GET http://apiserver/dimensions

EXAMPLE REQUEST
$.get("http://localhost:49195/dimensions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "23",
            "type": "DIMENSIONTYPE",
            "entityType":"Product",
            "codeType":"DDCGLCLASS",
            "isActive": true,
            "dimensionIdNumber": 1300
        },
        {...},
        {...}
    ]
}

```

Returns a list of all dimension.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* type (optional) - The type of dimension.
* entityType (optional) - The entity type of the dimension.
* codeType (optional) - The code type for the dimension.
* isActive (optional) - Whether the dimension is active or not
* dimensionIdNumber (optional) - The Dimension ID Number to be used.

##### Returns

A dictionary with an items property that contains an array of up to limit dimensions, starting at index offset. Each entry in the array is a separate dimensions object. If no more dimensions are available, the resulting array will be empty. This request should never return an error.

### Journal Entries

#### Retrieve a journal entry

```
DEFINITION
GET http://apiserver/journalentries/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries/1349");

EXAMPLE RESPONSE
{
    "id": "1349",
    "type": "SHIPPING",
    "description": "Shipping of Group 691",
    "glDate": "2015-04-23",
    "glDocumentType": null,
    "glDocumentReference": null,
    "currency": "USD",
    "currencyDescription": "US Dollars",
    "conversionRate": 1,
    "company": "4",
    "companyDescription": "DonorDirect Company",
    "status": "Y"
}

```

Retrieves the details of an existing journal entry. You need only supply the journal entry id.

##### Returns

Returns journal entry object if a valid id was provided.

#### List all journal entries

```
DEFINITION
GET http://apiserver/journalentries

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "1349",
            "type": "SHIPPING",
            "description": "Shipping of Group 691",
            "glDate": "2015-04-23",
            "glDocumentType": null,
            "glDocumentReference": null,
            "currency": "USD",
            "currencyDescription": "US Dollars",
            "conversionRate": 1,
            "company": "4",
            "companyDescription": "DonorDirect Company",
            "status": "Y"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all journal entries.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* journalEntryId (optional) - The Id of the journal entry.
* company (optional) - The company of the journal entry.
* glDate (optional) - The GL date of the journal entry.
* status (optional) - The status of the journal entry.

##### Returns

A dictionary with an items property that contains an array of up to limit journal entries, starting at index offset. Each entry in the array is a separate journal entry object. If no more journal entries are available, the resulting array will be empty. This request should never return an error.

#### Remove a journal entry

```
DEFINITION
POST http://apiserver/journalentries/:id/remove

EXAMPLE REQUEST
$.post("http://localhost:49195/journalentries/1349/remove", {});

EXAMPLE RESPONSE
204 NoContent

```

Removes or undoes a journal entry.

##### Arguments

* id (required) - The journal entry id of the journal entry to be removed.

##### Returns

Returns a 204 NoContent response on success. If the journal entry id does not exist, this call returns an error.

#### Repost a journal entry

```
DEFINITION
POST http://apiserver/journalentries/:id/repost

EXAMPLE REQUEST
$.post("http://localhost:49195/journalentries/1349/repost", {});

EXAMPLE RESPONSE
204 NoContent

```

Reposts a journal entry.

##### Arguments

* id (required) - The journal entry id of the journal entry to be reposted.

##### Returns

Returns a 204 NoContent response on success. If the journal entry id does not exist, this call returns an error (422).

### Journal Entry Details

#### Retrieve a journal entry detail

```
DEFINITION
GET http://apiserver/journalentries/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries/1349/details/177008");

EXAMPLE RESPONSE
{
    "id": "177008",
    "journalEntryId": 1349,
    "glSegment1": "010",
    "glSegment2": "110100",
    "glSegment3": "62100",
    "glSegment4": "BKS",
    "glSegment5": null,
    "glSegment6": null,
    "glSegment7": null,
    "glSegment8": null,
    "glSegment9": null,
    "glSegment10": null,
    "amount": 3.23,
    "tableId": "D08E",
    "description": null,
    "documentNumber": null,
    "tableRecordId": 64,
    "glDimension1": "1109A328",
    "glDimension2": "G12BSCA",
    "glDimension3": "",
    "glDimension4": "",
    "glDimension5": ""
}

```

Retrieves the details of an existing journal entry detail. You need only supply the journal entry and journal entry detail ids.

##### Returns

Returns journal entry detail object if a valid id was provided.

#### Update a journal entry detail

```
DEFINITION
POST http://apiserver/journalentries/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/journalentries/1349/details/177008", {
        "glSegment3": "62200,
});

EXAMPLE RESPONSE
{
    "id": "177008",
    "journalEntryId": 1349,
    "glSegment1": "010",
    "glSegment2": "110100",
    "glSegment3": "62200",
    "glSegment4": "BKS",
    "glSegment5": null,
    "glSegment6": null,
    "glSegment7": null,
    "glSegment8": null,
    "glSegment9": null,
    "glSegment10": null,
    "amount": 3.23,
    "tableId": "D08E",
    "description": null,
    "documentNumber": null,
    "tableRecordId": 64,
    "glDimension1": "1109A328",
    "glDimension2": "G12BSCA",
    "glDimension3": "",
    "glDimension4": "",
    "glDimension5": ""
}

```

##### Arguments

* glSegment1 (optional) - The GL segment 1 for the journal entry detail.
* glSegment2 (optional) - The GL segment 2 for the journal entry detail.
* glSegment3 (optional) - The GL segment 3 for the journal entry detail.
* glSegment4 (optional) - The GL segment 4 for the journal entry detail.
* glSegment5 (optional) - The GL segment 5 for the journal entry detail.
* glSegment6 (optional) - The GL segment 6 for the journal entry detail.
* glSegment7 (optional) - The GL segment 7 for the journal entry detail.
* glSegment8 (optional) - The GL segment 8 for the journal entry detail.
* glSegment9 (optional) - The GL segment 9 for the journal entry detail.
* glSegment10 (optional) - The GL segment 10 for the journal entry detail.
* amount (optional) - The amount for the journal entry detail.
* tableId (optional) - The table id for the journal entry detail.
* tableRecordId (optional) - The table record id for the journal entry detail.
* glDimension1 (optional) - The GL dimension 1 for the journal entry detail.
* glDimension2 (optional) - The GL dimension 2 for the journal entry detail.
* glDimension3 (optional) - The GL dimension 3 for the journal entry detail.
* glDimension4 (optional) - The GL dimension 4 for the journal entry detail.
* glDimension5 (optional) - The GL dimension 5 for the journal entry detail.

##### Returns

Returns journal entry detail object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a journal entry detail

```
DEFINITION
DELETE http://apiserver/journalentries/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/journalentries/1349/details/177008", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes journal entry detail. It cannot be undone.

##### Arguments

* id (required) - The id of the journal entry detail to be deleted.

##### Returns

Returns a 204 No Content response on success. If the journal entry detail id does not exist, this call returns an error.

#### List all journal entry details

```
DEFINITION
GET http://apiserver/journalentries/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries/1349/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
        "id": "177008",
        "journalEntryId": 1349,
        "glSegment1": "010",
        "glSegment2": "110100",
        "glSegment3": "62200",
        "glSegment4": "BKS",
        "glSegment5": null,
        "glSegment6": null,
        "glSegment7": null,
        "glSegment8": null,
        "glSegment9": null,
        "glSegment10": null,
        "amount": 3.23,
        "tableId": "D08E",
        "description": null,
        "documentNumber": null,
        "tableRecordId": 64,
        "glDimension1": "1109A328",
        "glDimension2": "G12BSCA",
        "glDimension3": "",
        "glDimension4": "",
        "glDimension5": ""
        },
        {...},
        {...}
    ]
}

```

Returns a list of all journal entry details for a journal entry.

##### Arguments

Use these arguments if you want to look up details by segments. Parameter values can be retrieve from the Journal Entry Summaries. All applicable values from the summaries must be provided.

* firstId (optional) - The first record Id of the journal entry detail summary.
* glSegment1 (optional) - The GL segment 1 for the journal entry detail.
* glSegment2 (optional) - The GL segment 2 for the journal entry detail.
* glSegment3 (optional) - The GL segment 3 for the journal entry detail.
* glSegment4 (optional) - The GL segment 4 for the journal entry detail.
* glSegment5 (optional) - The GL segment 5 for the journal entry detail.
* glSegment6 (optional) - The GL segment 6 for the journal entry detail.
* glSegment7 (optional) - The GL segment 7 for the journal entry detail.
* glSegment8 (optional) - The GL segment 8 for the journal entry detail.
* glSegment9 (optional) - The GL segment 9 for the journal entry detail.
* glSegment10 (optional) - The GL segment 10 for the journal entry detail.
* glDimension1 (optional) - The GL dimension 1 for the journal entry detail.
* glDimension2 (optional) - The GL dimension 2 for the journal entry detail.
* glDimension3 (optional) - The GL dimension 3 for the journal entry detail.
* glDimension4 (optional) - The GL dimension 4 for the journal entry detail.
* glDimension5 (optional) - The GL dimension 5 for the journal entry detail.

##### Returns

A dictionary with an items property that contains an array of up to limit journal entry details, starting at index offset. Each entry in the array is a separate journal entry detail object. If no more journal entry details are available, the resulting array will be empty. This request should never return an error.

### Journal Entry Detail Dimensions

#### Retrieve a journal entry detail dimension

```
DEFINITION
GET http://apiserver/journalentries/:id/details/:id/dimensions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries/1349/details/177008/dimensions/2");

EXAMPLE RESPONSE
{
    "id": "2",
    "detailId": 177008,
    "dimensionId": "20",
    "dimensionValue": "Test Value 2",
    "dimensionType": "TEST5",
    "dimensionIdNumber": "999888"
}

```

Retrieves the details of an existing journal entry detail dimension You need only supply the journal entry, journal entry detail and journal entry detail dimension ids.

##### Returns

Returns journal entry detail dimension object if a valid id was provided.

#### Delete a journal entry detail dimension

```
DEFINITION
DELETE http://apiserver/journalentries/:id/details/:id/dimensions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/journalentries/1349/details/177008/dimensions/2", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes journal entry detail dimension. It cannot be undone.

##### Arguments

* id (required) - The id of the journal entry detail dimension to be deleted.

##### Returns

Returns a 204 No Content response on success. If the journal entry detail dimension id does not exist, this call returns an error.

#### List all journal entry detail dimensions

```
DEFINITION
GET http://apiserver/journalentries/:id/details/:id/dimensions

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries/1349/details/177008/dimensions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "2",
            "detailId": 177008,
            "dimensionId": "20",
            "dimensionValue": "Test Value 2",
            "dimensionType": "TEST5",
            "dimensionIdNumber": "999888"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all journal entry detail dimensions.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit journal entry detail dimensions, starting at index offset. Each entry in the array is a separate journal entry detail dimension object. If no more journal entry detail dimensions are available, the resulting array will be empty. This request should never return an error.

### Journal Entry Errors

#### List all journal entry errors

```
DEFINITION
GET http://apiserver/journalentries/:id/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries/1335/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "39943",
            "journalEntryId": "1335",
            "errorDescription": "No accounting instruction found for project code: 110100",
            "journalEntryDetailId": "22423"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all journal entry errors.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit journal entry errors, starting at index offset. Each entry in the array is a separate journal entry error object. If no more journal entry errors are available, the resulting array will be empty. This request should never return an error.

### Journal Entry Summaries

#### List all journal entry summaries

```
DEFINITION
GET http://apiserver/journalentries/:id/summaries

EXAMPLE REQUEST
$.get("http://localhost:49195/journalentries/1349/summaries");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "firstId": "177011",
            "amount": -9.06,
            "glSegment1": "010",
            "glSegment2": "1",
            "glSegment3": "13100",
            "glSegment4": "BKS",
            "glSegment5": null,
            "glSegment6": null,
            "glSegment7": null,
            "glSegment8": null,
            "glSegment9": null,
            "glSegment10": null,
            "balanceType": null,
            "glDimension1": null,
            "glDimension2": null,
            "glDimension3": null,
            "glDimension4": null,
            "glDimension5": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all journal entry summaries.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit journal entry summaries, starting at index offset. Each entry in the array is a separate journal entry summary object. If no more journal entry summaries are available, the resulting array will be empty. This request should never return an error.

### Projects

#### Create a project

```
DEFINITION
POST http://apiserver/projects

EXAMPLE REQUEST
$.post("http://localhost:49195/projects", {
    "id": "110102",
    "type": "PR",
    "description": "Action Packs for Iraq",
    "title": null,
    "firstName": null,
    "lastName": null,
    "defaultDepartment": "100",
    "isActiveForDonor": true,
    "isActiveForAccounting": true,
    "emailAddress": "donordirect@example.com",
    "accountingSegment": "110102",
    "company": "010",
    "account": null,
    "balanceType": "T",
    "isDeductible": true,
    "useInStudioOnline": true,
    "isSecure": false
});

EXAMPLE RESPONSE
{
    "id": "110102",
    "type": "PR",
    "description": "Action Packs for Iraq",
    "title": null,
    "firstName": null,
    "lastName": null,
    "defaultDepartment": "100",
    "isActiveForDonor": true,
    "isActiveForAccounting": true,
    "emailAddress": "donordirect@example.com",
    "accountingSegment": "110102",
    "company": "010",
    "account": null,
    "balanceType": "T",
    "useInStudioOnline": true,
    "isSecure": false,
    "typeDescription": "Project",
    "defaultDepartmentDescription": "North America",
    "companyDescription": "DDC Test Company",
    "isDeductible": true,
    "balanceTypeDescription": "Temp Restricted"
}

```

Creates a new project object.

##### Arguments

* id (required) - The project code. Must be unique.
* type (optional) - The project type for the project.
* description (optional) - A description for the project.
* defaultDepartment (optional) - The Default Department in which the project should be placed.
* isActiveForDonor (optional) - Is the project active for a donor to give. If not specified, it will default to false.
* isActiveForAccounting (optional) - Is the project active for accounting to view. If not specified, it will default to false.
* emailAddress (optional) - An email address for the project.
* accountingSegment (optional) - The accounting segment for the project.
* company (optional) - The company the project is for.
* balanceType (optional) - The balance Type for the project.
* isDeductible (optional) - Whether the project is deductible. If not provided, this will be set to match the value of the DONDEDUCT control record.
* useInStudioOnline (optional) - Whether to use this project in Studio Online. If not specified, it will default to false.
* isSecure (optional) - Indicates if this is a secure project for Advanced Studio Online. If not specified, it will default to false.

##### Additional arguments if type is `MS`

* account (optional) - The account number for whom the project is for.
* title (optional) - The title of the person for whom the project is for.
* firstName (optional) - The first name of the person for whom the project is for.
* lastName (optional) - The last name of the person for whom the project is for.

##### Returns

Returns a project object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an id that already exists).

#### Retrieve a project

```
DEFINITION
GET http://apiserver/projects/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110102");

EXAMPLE RESPONSE
{
    "id": "110102",
    "type": "PR",
    "description": "Action Packs for Iraq",
    "title": null,
    "firstName": null,
    "lastName": null,
    "defaultDepartment": "100",
    "isActiveForDonor": true,
    "isActiveForAccounting": true,
    "emailAddress": "donordirect@example.com",
    "accountingSegment": "110102",
    "company": "010",
    "account": null,
    "balanceType": "T",
    "useInStudioOnline": true,
    "isSecure": false,
    "typeDescription": "Project",
    "defaultDepartmentDescription": "North America",
    "companyDescription": "DDC Test Company",
    "balanceTypeDescription": "Temp Restricted",
    "isDeductible": true,
    "projectData": null
}

```

Retrieves the details of an existing project. You need only supply the project code.

##### Arguments

* id (required) - The project code of the project to retrieve.
* store (optional) - StudioOnline store Id; when provided, returns json that represents the project.

##### Returns

Returns a project object if a valid id was provided.

#### Update a project

```
DEFINITION
POST http://apiserver/projects/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/110102", {
    "isActiveForDonor": false
});

EXAMPLE RESPONSE
{
    "id": "110102",
    "type": "PR",
    "description": "Action Packs for Iraq",
    "title": null,
    "firstName": null,
    "lastName": null,
    "defaultDepartment": "100",
    "isActiveForDonor": false,
    "isActiveForAccounting": true,
    "emailAddress": "donordirect@example.com",
    "accountingSegment": "110102",
    "company": "010",
    "account": null,
    "balanceType": "T",
    "isDeductible": true,
    "useInStudioOnline": true,
    "isSecure": false,
    "typeDescription": "Project",
    "defaultDepartmentDescription": "North America",
    "companyDescription": "DDC Test Company",
    "balanceTypeDescription": "Temp Restricted"
}


```

Updates the specified project by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The project type for this project.
* description (optional) - A description for the project.
* defaultDepartment (optional) - The Default Department in which the project should be placed.
* isActiveForDonor (optional) - Is the project active for a donor to give. If not specified, it will default to false.
* isActiveForAccounting (optional) - Is the project active for accounting to view. If not specified, it will default to false.
* emailAddress (optional) - An email address for the project.
* accountingSegment (optional) - The accounting segment for the project.
* company (optional) - The company the project is for.
* balanceType (optional) - The balance Type for the project.
* isDeductible (optional) - Whether the project is deductible.
* useInStudioOnline (optional) - Whether to use this project in Studio Online. If not specified, it will default to false.
* isSecure (optional) - Indicates if this is a secure project for Advanced Studio Online. If not specified, it will default to false.

##### Additional arguments if type is `MS`

* account (optional) - The account number for whom the project is for.
* title (optional) - The title of the person for whom the project is for.
* firstName (optional) - The first name of the person for whom the project is for.
* lastName (optional) - The last name of the person for whom the project is for.

##### Returns

Returns the project object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined product type code).

#### Delete a project

```
DEFINITION
DELETE http://apiserver/projects/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/110102", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project. It cannot be undone.

##### Arguments

* id (required) - The project code of the project to be deleted.

##### Returns

Returns a 204 No Content response on success. If the product attachment id does not exist, this call returns an error.

#### List all projects

```
DEFINITION
GET http://apiserver/projects

EXAMPLE REQUEST
$.get("http://localhost:49195/projects?company=010");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 65
    }
    "items": [
        {
            "id": "110102",
            "type": "PR",
            "description": "Action Packs for Iraq",
            "title": null,
            "firstName": null,
            "lastName": null,
            "defaultDepartment": "100",
            "isActiveForDonor": true,
            "isActiveForAccounting": true,
            "emailAddress": "donordirect@example.com",
            "accountingSegment": "110102",
            "company": "010",
            "account": null,
            "balanceType": "T",
            "isDeductible": true,
            "useInStudioOnline": true,
            "isSecure": false,
            "typeDescription": "Project",
            "defaultDepartmentDescription": "North America",
            "companyDescription": "DDC Test Company",
            "balanceTypeDescription": "Temp Restricted"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all projects matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in project code
* type () - Filter list by partial match in project type
* description () - Filter list by partial match in project description
* title () - Filter list by partial match in project title
* firstName () - Filter list by partial match in project first name
* lastName () - Filter list by partial match in project last name
* company () - Filter list by partial match in project company code
* defaultDepartment () - Filter list by partial match in project default department
* accountNumber () - Filter list by match in project account number
* isActiveForDonor () - Filter list by whether project is active for donor
* isActiveForAccounting () - Filter list by whether project is active for accounting
* isDeductible () - Filter list by whether project is deductible
* useInStudioOnline () - Filter list by whether project can be used in Studio Online
* restrictBasedOnAccessorId (optional) - If provided, return only results where the project code is defined in the ProjectAccessors table for the given accessor Id.

##### Returns

A dictionary with an items property that contains an array of up to limit projects, starting at index offset. Each entry in the array is a separate project object. If no more projects are available, the resulting array will be empty. This request should never return an error.

#### Copy a Project to Another

```
DEFINITION
POST http://apiserver/projects/:id/copy

EXAMPLE REQUEST
$.post("http://localhost:49195/project/110102/copy", {
    "destinationProjectId": "110100"
});

EXAMPLE RESPONSE
204 No Content

```

This will copy all of the project components (codes, dates, notes, numbers, attachments, subaccounts, allocation, functional percentages, etc.) from the project id in the url to the destinationProjectId in the body of the request. Before the copy all of the project components of the destination project will be deleted.

##### Arguments

* id (required) - The project code of the project from which to copy (value in the url).
* destinationProjectId (required) - The project code of the destination project in which to copy the data to.

##### Returns

Returns a 204 No Content response on success. If the source or destination project does not exist, if the source or destination project are the same or if the isActiveForDonor is not true for the destination project, this call returns an error.

### Project Attachments

#### Create a project attachment

```
DEFINITION
POST http://apiserver/projects/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new project attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a project attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a project attachment

```
DEFINITION
GET http://apiserver/projects/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing project attachment. You need only supply the project id and project attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a project attachment object if a valid id was provided.

#### Update a project attachment

```
DEFINITION
POST http://apiserver/projects/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified project attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type. Must be a defined attachment type.
* url (optional) - The url of the attachment type.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the project attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a project attachment

```
DEFINITION
DELETE http://apiserver/projects/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project attachment id does not exist, this call returns an error.

#### List all project attachments

```
DEFINITION
GET http://apiserver/projects/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/attachments");

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
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all project attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit project attachments, starting at index offset. Each entry in the array is a separate project attachment object. If no more project attachments are available, the resulting array will be empty. This request should never return an error.

### Project Categories

#### Create a project category

```
DEFINITION
POST http://apiserver/projects/:projectCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/10/storeconfigurations/1/categories", {
    "categoryId": 20
});

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Creates a new project category for the given StudioOnline store configuration.

##### Arguments

* categoryId (required) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns a project category object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a project category

```
DEFINITION
GET http://apiserver/projects/:projectCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/10/storeconfigurations/1/categories/14");

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": false,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}

```

Retrieves the details of an existing project category for the given StudioOnline store configuration. You need only supply the id.

##### Arguments

* id (required) - The id of the project category to be retrieved.

#### Update a project category

```
DEFINITION
POST http://apiserver/projects/:projectCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/10/storeconfigurations/1/categories/14", {
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "14",
    "categoryId": "20",
    "categoryName": "Best Sellers",
    "isPrimary": true,
    "isActive": true,
    "breadcrumb": "best-sellers",
    "parentCategoryId": null,
    "parentCategoryName": null
}


```

Updates the specified project category for the given StudioOnline store configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* categoryId (optional) - The id of the category to add.
* isPrimary (optional) - Indicates whether the category is the primary. Only one category can be primary, setting this will cause any other primary category to be set to false.
* isActive (optional) - Indicates whether or not the category is active.

##### Returns

Returns the project category object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a project category

```
DEFINITION
DELETE http://apiserver/projects/:projectCode/storeconfigurations/:storeConfigurationId/categories/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/10/storeconfigurations/1/categories/14", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project category from the given StudioOnline store configuration. It cannot be undone.

##### Arguments

* id (required) - The id of the project category to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the project category does not exist, this call returns an error.

#### List all project categories

```
DEFINITION
GET http://apiserver/projects/:projectCode/storeconfigurations/:storeConfigurationId/categories

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/10/storeconfigurations/1/categories");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "14",
            "categoryId": "20",
            "categoryName": "Best Sellers",
            "isPrimary": true,
            "isActive": true,
            "breadcrumb": "best-sellers",
            "parentCategoryId": null,
            "parentCategoryName": null
        },
        {...},
    ]
}

```

Returns a list of all project categories for the given StudioOnline store configuration.

##### Returns

A dictionary with an items property that contains an array of up to limit project categories, starting at index offset. Each entry in the array is a separate project category object. If no more project categories are available, the resulting array will be empty. This request should never return an error.

### Project Codes

#### Create a project code

```
DEFINITION
POST http://apiserver/projects/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/codes", {
    "type": "DDCMISPROJ",
    "value": "Y"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCMISPROJ",
    "typeDescription": "General Missionary Project",
    "value": "Y",
    "valueDescription": "flag as general project",
    "isActive": true
}

```

Creates a new project code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a project code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a project code

```
DEFINITION
GET http://apiserver/projects/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/codes/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCMISPROJ",
    "typeDescription": "General Missionary Project",
    "value": "Y",
    "valueDescription": "flag as general project",
    "isActive": true
}

```

Retrieves the details of an existing project code. You need only supply the project id and project code id.

##### Returns

Returns a project code object if a valid id was provided.

#### Update a project code

```
DEFINITION
POST http://apiserver/projects/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/codes/16", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCMISPROJ",
    "typeDescription": "General Missionary Project",
    "value": "Y",
    "valueDescription": "flag as general project",
    "isActive": false
}


```

Updates the specified project code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the project code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a project code

```
DEFINITION
DELETE http://apiserver/projects/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/codes/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project code. It cannot be undone.

##### Arguments

* id (required) - The id of the project code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project code id does not exist, this call returns an error.

#### List all project codes

```
DEFINITION
GET http://apiserver/projects/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "16",
            "type": "DDCMISPROJ",
            "typeDescription": "General Missionary Project",
            "value": "Y",
            "valueDescription": "flag as general project",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all project codes.

##### Returns

A dictionary with an items property that contains an array of up to limit project codes, starting at index offset. Each entry in the array is a separate project code object. If no more project codes are available, the resulting array will be empty. This request should never return an error.

### Project Dates

#### Create a project date

```
DEFINITION
POST http://apiserver/projects/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/dates", {
    "type": "DDCPRJDT1",
    "value": "2015-03-18"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCPRJDT1",
    "typeDescription": "Project Date - Approved",
    "value": "2015-03-18",
    "isActive": true
}

```

Creates a new project date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a project date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a project date

```
DEFINITION
GET http://apiserver/projects/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/dates/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCPRJDT1",
    "typeDescription": "Project Date - Approved",
    "value": "2015-03-18",
    "isActive": true
}

```

Retrieves the details of an existing project date. You need only supply the project id and project date id.

##### Returns

Returns a project date object if a valid id was provided.

#### Update a project date

```
DEFINITION
POST http://apiserver/projects/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/dates/16", {
    "value": "2015-03-11",
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "DDCPRJDT1",
    "typeDescription": "Project Date - Approved",
    "value": "2015-03-11",
    "isActive": false
}


```

Updates the specified project date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the project date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a project date

```
DEFINITION
DELETE http://apiserver/projects/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/dates/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project date. It cannot be undone.

##### Arguments

* id (required) - The id of the account date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project date id does not exist, this call returns an error.

#### List all project dates

```
DEFINITION
GET http://apiserver/projects/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "16",
            "type": "DDCPRJDT1",
            "typeDescription": "Project Date - Approved",
            "value": "2015-03-11",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all project dates.

##### Returns

A dictionary with an items property that contains an array of up to limit project dates, starting at index offset. Each entry in the array is a separate project date object. If no more project dates are available, the resulting array will be empty. This request should never return an error.

### Project Images

#### Create a project image

```
DEFINITION
POST http://apiserver/projects/:projectId/images

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/100100/images", {
    "imageType": "IMAGEXS",
    "description": "Extra Small Project Img",
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
    "description": "Extra Small Project Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Creates a new project image.

##### Arguments

* imageType (required) - the ImageType code value for the project image.
* description (optional) - the description for the project image.
* imageUrl (required) - the image URL for the project image.
* alternateText (optional) - the alternate text for the project image.
* title (optional) - the image title for the project image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns a project image object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a project image

```
DEFINITION
GET http://apiserver/projects/:projectId/images/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/100100/images/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Project Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}

```

Retrieves the details of an existing project image. You need only supply the id.

##### Arguments

* id (required) - The id of the project image to be retrieved.

#### Update a project image

```
DEFINITION
POST http://apiserver/projects/:projectId/images/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/100100/images/6", {
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "imageType": "IMAGEXS",
    "imageTypeDescription": "Extra Small Image",
    "description": "Extra Small Project Img",
    "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
    "alternateText": "Image Alt Text",
    "title": "Image Title",
    "isActive": true
}


```

Updates the specified project image by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* imageType (optional) - the ImageType code value to update for the project image.
* description (optional) - the description to update for the project image.
* imageUrl (optional) - the image URL to update for the project image.
* alternateText (optional) - the alternate text to update for the project image.
* title (optional) - the image title to update for the project image.
* isActive (optional) - is the image active in StudioOnline.

##### Returns

Returns the project image object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a project image

```
DEFINITION
DELETE http://apiserver/projects/:projectId/images/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/100100/images/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project image. It cannot be undone.

##### Arguments

* id (required) - The id of the project image to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the project image does not exist, this call returns an error.

#### List all project images

```
DEFINITION
GET http://apiserver/projects/:projectId/images

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/100100/images");

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
            "description": "Extra Small Project Img",
            "imageUrl": "https://www.myministry.org/cdn/images/extrasmallimage.png",
            "alternateText": "Image Alt Text",
            "title": "Image Title",
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all project images by project code.

##### Returns

A dictionary with an items property that contains an array of up to limit project images, starting at index offset. Each entry in the array is a separate project image object. If no more project images are available, the resulting array will be empty. This request should never return an error.

### Project Notes

#### Create a project note

```
DEFINITION
POST http://apiserver/projects/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/notes", {
    "type": "SOPRJNOTE",
    "shortComment": "example",
    "longComment":"This is an example comment.\nMultiple lines are supported."
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SOPRJNOTE",
    "description": "SO Project Note",
    "shortComment": "example",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Creates a new project note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a project note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a project note

```
DEFINITION
GET http://apiserver/projects/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/notes/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SOPRJNOTE",
    "description": "SO Project Note",
    "shortComment": "example",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Retrieves the details of an existing project note. You need only supply the project id and project note id.

##### Returns

Returns a project note object if a valid id was provided.

#### Update a project note

```
DEFINITION
POST http://apiserver/projects/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/notes/9", {
    "shortComment": "time for an edit"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "SOPRJNOTE",
    "description": "SO Project Note",
    "shortComment": "time for an edit",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}


```

Updates the specified project note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the project note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type).

#### Delete a project note

```
DEFINITION
DELETE http://apiserver/projects/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/notes/11", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project note. It cannot be undone.

##### Arguments

* id (required) - The id of the account note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project note id does not exist, this call returns an error.

#### List all project notes

```
DEFINITION
GET http://apiserver/projects/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "9",
            "type": "SOPRJNOTE",
            "description": "SO Project Note",
            "shortComment": "time for an edit",
            "longComment": "This is an example comment.\nMultiple lines are supported."
        },
        {...},
        {...}
    ]
}

```

Returns a list of all project notes.

##### Returns

A dictionary with an items property that contains an array of up to limit project notes, starting at index offset. Each entry in the array is a separate project note object. If no more project notes are available, the resulting array will be empty. This request should never return an error.

### Project Numbers

#### Create a project number

```
DEFINITION
POST http://apiserver/projects/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/numbers", {
    "type": "PRDEPWKSUP",
    "value": "700"
});

EXAMPLE RESPONSE
{
    "id": "10",
    "type": "PRDEPWKSUP",
    "typeDescription": "Weekly support amount",
    "value": 700,
    "isActive": true
}

```

Creates a new project number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a project number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a project number

```
DEFINITION
GET http://apiserver/projects/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/numbers/10");

EXAMPLE RESPONSE
{
    "id": "10",
    "type": "PRDEPWKSUP",
    "typeDescription": "Weekly support amount",
    "value": 700,
    "isActive": true
}

```

Retrieves the details of an existing project number. You need only supply the project id and project number id.

##### Returns

Returns a project number object if a valid id was provided.

#### Update a project number

```
DEFINITION
POST http://apiserver/projects/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/numbers/10", {
    "value": 800
});

EXAMPLE RESPONSE
{
    "id": "10",
    "type": "PRDEPWKSUP",
    "typeDescription": "Weekly support amount",
    "value": 800,
    "isActive": true
}


```

Updates the specified project number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the project number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Delete a project number

```
DEFINITION
DELETE http://apiserver/projects/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/numbers/10", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project number. It cannot be undone.

##### Arguments

* id (required) - The id of the account number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project number id does not exist, this call returns an error.

#### List all project numbers

```
DEFINITION
GET http://apiserver/projects/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10",
            "type": "PRDEPWKSUP",
            "typeDescription": "Weekly support amount",
            "value": 800,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all project numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit project numbers, starting at index offset. Each entry in the array is a separate project number object. If no more project numbers are available, the resulting array will be empty. This request should never return an error.

### Project Subaccounts

#### Create a project subaccount

```
DEFINITION
POST http://apiserver/projects/:id/subaccounts

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/subaccounts", {
    "id": "001",
    "description": "Monetary Support"
    "balanceType": "U"
});

EXAMPLE RESPONSE
{
    "id": "001",
    "description": "Monetary Support",
    "balanceType": "U",
    "subaccountDescription": "General Support",
    "balanceTypeDescription": "Unrestricted",
    "useInStudioOnline": false
}

```

Creates a new project subaccount object

##### Arguments

* id (required) - The subaccount id code. Must be a valid subaccount code.
* description (optional) - An override description for the project subaccount.
* balanceType (optional) - The balance type for the project subaccount.

##### Returns

Returns a project subaccount object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined subaccount code or an invalid balanceType).

#### Retrieve a project subaccount

```
DEFINITION
GET http://apiserver/projects/:id/subaccounts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/subaccounts/001");

EXAMPLE RESPONSE
{
    "id": "001",
    "description": "Monetary Support",
    "balanceType": "U",
    "subaccountDescription": "General Support",
    "balanceTypeDescription": "Unrestricted",
    "useInStudioOnline": false
}

```

Retrieves the details of an existing project subaccount. You need only supply the project id and project subaccount id.

##### Returns

Returns a project subaccount object if a valid id was provided.

#### Update a project subaccount

```
DEFINITION
POST http://apiserver/projects/:id/subaccounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/subaccounts/001", {
    "balanceType": "R"
});

EXAMPLE RESPONSE
{
    "id": "001",
    "description": "Monetary Support",
    "balanceType": "R",
    "subaccountDescription": "General Support",
    "balanceTypeDescription": "Restricted",
    "useInStudioOnline": false
}


```

Updates the specified project subaccount by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - An override description for the project subaccount.
* balanceType (optional) - The balance type for the project subaccount.

##### Returns

Returns the project subaccount object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined subaccount code or an invalid balanceType).

#### Delete a project subaccount

```
DEFINITION
DELETE http://apiserver/projects/:id/subaccounts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/subaccounts/001", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project subaccount. It cannot be undone.

##### Arguments

* id (required) - The id of the account subaccount to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project subaccount id does not exist, this call returns an error.

#### List all project subaccounts

```
DEFINITION
GET http://apiserver/projects/:id/subaccounts

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110102/subaccounts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "001",
            "description": null,
            "balanceType": "R",
            "subaccountDescription": "General Support",
            "balanceTypeDescription": "Restricted",
            "useInStudioOnline": true
        }
    ]
}

```

Returns a list of all project subaccounts matching the provided filter criteria.

##### Arguments

* balanceType (optional) - The balance type of the subaccount.
* description (optional) - The description of the subaccount.
* active (optional) - Whether the subaccount is active.

##### Returns

A dictionary with an items property that contains an array of up to limit project subaccounts, starting at index offset. Each entry in the array is a separate project subaccount object. If no more project subaccounts are available, the resulting array will be empty. This request should never return an error.

### Project Allocations

#### Create a project allocation

```
DEFINITION
POST http://apiserver/projects/:id/allocations

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/allocations", {
    "id": "ADMIN",
    "allocationAmount": 120
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "ADMIN",
    "allocationAmount": 120,
    "lastAmountAllocated": null,
    "isActive": true,
    "allocationCategoryDescription": "Missionary Admin Services"
}

```

Creates a new project allocation object

##### Arguments

* id (required) - The allocation category code. Must be a valid allocation category code.
* allocationAmount (optional) - The amount allocated for the project allocation.
* lastAmountAllocated (optional) - The last amount allocated for the project allocation.
* isActive (optional) - Whether the project allocation is active.

##### Returns

Returns a project allocation object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined allocation category code).

#### Retrieve a project allocation

```
DEFINITION
GET http://apiserver/projects/:id/allocations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/allocations/ADMIN");

EXAMPLE RESPONSE
{
    "id": "ADMIN",
    "allocationAmount": 120,
    "lastAmountAllocated": null,
    "isActive": true,
    "allocationCategoryDescription": "Missionary Admin Services"
}

```

Retrieves the details of an existing project allocation. You need only supply the project id and project allocation id.

##### Returns

Returns a project allocation object if a valid id was provided.

#### Update a project allocation

```
DEFINITION
POST http://apiserver/projects/:id/allocations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/allocations/ADMIN", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "ADMIN",
    "allocationAmount": 120,
    "lastAmountAllocated": null,
    "isActive": false,
    "allocationCategoryDescription": "Missionary Admin Services"
}


```

Updates the specified project allocation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* allocationAmount (optional) - The amount allocated for the project allocation.
* lastAmountAllocated (optional) - The last amount allocated for the project allocation.
* isActive (optional) - Whether the project allocation is active.

##### Returns

Returns the project allocation object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined allocation category code).

#### Delete a project allocation

```
DEFINITION
DELETE http://apiserver/projects/:id/allocations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/allocations/ADMIN", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project allocation. It cannot be undone.

##### Arguments

* id (required) - The id of the account allocation to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project allocation id does not exist, this call returns an error.

#### List all project allocations

```
DEFINITION
GET http://apiserver/projects/:id/allocations

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110102/allocations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "ADMIN",
            "allocationAmount": 120,
            "lastAmountAllocated": null,
            "isActive": false,
            "allocationCategoryDescription": "Missionary Admin Services"
        }
    ]
}

```

Returns a list of all project allocations.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit project allocations, starting at index offset. Each entry in the array is a separate project allocation object. If no more project allocations are available, the resulting array will be empty. This request should never return an error.

### Project Functional Percentages

#### Create a project functional percentage

```
DEFINITION
POST http://apiserver/projects/:id/functionalpercentages

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/functionalpercentages", {
    "id": "CL",
    "distributionPercentage": "15"
});

EXAMPLE RESPONSE
{
    "id": "CL",
    "distributionPercentage": 15,
    "functionalCategoryDescription": "Christian Literature"
}

```

Creates a new project functional percentage object

##### Arguments

* id (required) - The functional category code. Must be a valid functional category code.
* distributionPercentage (optional) - The percent that is distributed to this functional category.

##### Returns

Returns a project functional percentage object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined functional percentage code).

#### Retrieve a project functional percentage

```
DEFINITION
GET http://apiserver/projects/:id/functionalpercentages/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/functionalpercentages/CL");

EXAMPLE RESPONSE
{
    "id": "CL",
    "distributionPercentage": 15,
    "functionalCategoryDescription": "Christian Literature"
}

```

Retrieves the details of an existing project functional percentage. You need only supply the project id and project functional percentage id.

##### Returns

Returns a project functional percentage object if a valid id was provided.

#### Update a project functional percentage

```
DEFINITION
POST http://apiserver/projects/:id/functionalpercentages/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/functionalpercentages/CL", {
    "distributionPercentage": 20
});

EXAMPLE RESPONSE
{
    "id": "CL",
    "distributionPercentage": 20,
    "functionalCategoryDescription": "Christian Literature"
}


```

Updates the specified project functional percentage by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* distributionPercentage (optional) - The percent that is distributed to this functional category.

##### Returns

Returns the project functional percentage object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined functional percentage code).

#### Delete a project functional percentage

```
DEFINITION
DELETE http://apiserver/projects/:id/functionalpercentages/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/functionalpercentages/CL", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project functional percentage. It cannot be undone.

##### Arguments

* id (required) - The id of the account functional percentage to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project functional percentage id does not exist, this call returns an error.

#### List all project functional percentages

```
DEFINITION
GET http://apiserver/projects/:id/functionalpercentages

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110102/functionalpercentages");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "CL",
            "distributionPercentage": 20,
            "functionalCategoryDescription": "Christian Literature"
        }
    ]
}

```

Returns a list of all project functional percentage.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit project functional percentages, starting at index offset. Each entry in the array is a separate project functional percentage object. If no more project functional percentages are available, the resulting array will be empty. This request should never return an error.

### Project Commitments

#### List all project commitments

```
DEFINITION
GET http://apiserver/projects/:id/commitments

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110102/commitments");

EXAMPLE RESPONSE
{
    "status": "A",
    "totalMonthlyCommitment": 100.55,
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "1172",
            "pledge": "050098",
            "pledgeDescription": "Mark McLemore Outreach 2012",
            "type": "PROJECT",
            "currency": "USD",
            "totalAmount": 1200,
            "amountPerGift": 100,
            "numberPledged": 12,
            "totalAmountDonated": 0,
            "totalNumberDonated": 0,
            "totalRelatedAmountDonated": null,
            "frequency": "M",
            "start": "2012-04-01",
            "end": "2013-04-01",
            "isOpenEnded": false,
            "source": "EV11CPCATL",
            "sourceDescription": "General Source Code",
            "status": "A",
            "isActive": true,
            "cancelReason": null,
            "cancelDate": null,
            "numberOfAdjustmentMonths": null,
            "stmtAndAckAccount": null,
            "infoAndUpdatesAccount": null,
            "infoAndUpdatesAccountName": null,
            "paidThroughDate": null,
            "originalPledge": null,
            "company": "1",
            "account": "1483320",
            "accountName": "Henry Winkler",
            "response": null,
            "assignedToAccessor": null
        }
    ]
}

```

Returns a list of all project commitments (which are account pledges). It also returns the total monthly commitment.

##### Arguments

* status (optional) - Filter the commitments by the pledge status

##### Returns

An object that contains the search status, the total monthly commitment and an items property that contains an array of up to limit project commitments (pledges), starting at index offset. Each entry in the array is a separate project commitment (pledge) object. If no more project commitments (pledges) are available, the resulting array will be empty. This request should never return an error.

### Project StudioOnline Publish Data

#### Retrieve the project StudioOnline publish data

```
DEFINITION
GET http://apiserver/projects/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/studioonlinepublishdata");

EXAMPLE RESPONSE
{
    "id": "6440",
    "description": "Project Test",
    "summary": "Summary Test",
    "extendedDescription": "Description Test",
    "isExtendedDescriptionLocked": true,
    "iconImage": "iconImage.png",
    "mediumImage": "mediumImage.jpg",
    "keywords": "Test Keywords",
    "pageLayout": "PROJPACK2"
}

```

Retrieves the details of the existing project StudioOnline publish data. You need only supply the project id.

##### Returns

Returns a project StudioOnline publish data object if a valid id was provided.

#### Update and publish the project StudioOnline publish data

```
DEFINITION
POST http://apiserver/projects/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/studioonlinepublishdata", {
    "pageLayout": "PROJPACK3",
});

EXAMPLE RESPONSE
{
    "id": "6440",
    "description": "Project Test",
    "summary": "Summary Test",
    "extendedDescription": "Description Test",
    "isExtendedDescriptionLocked": true,
    "updateImages": true,
    "iconImage": "iconImage.png",
    "mediumImage": "mediumImage.jpg",
    "keywords": "Test Keywords",
    "pageLayout": "PROJPACK3"
}


```

Updates and publishes the specified project StudioOnline publish data by setting the values of the parameters passed. Any parameters not provided will be left unchanged. Any categories must already have been updated through the Project Codes resources.

##### Arguments

* description (optional) - The description for the project on StudioOnline.
* summary (optional) - The summary for the project on StudioOnline.
* extendedDescription (optional) - The extended description for the project on StudioOnline.
* updateImages (optional) - Whether or not to update the icon and medium images. If this is selected and the icon or medium image are not provided, they will be deleted.
* iconImage (optional) - The icon image for the project on StudioOnline.
* mediumImage (optional) - The medium image for the project on StudioOnline.
* keywords (optional) - The keywords for the project on StudioOnline.
* pageLayout (optional) - The page layout (XML Package) for the project on StudioOnline.

##### Returns

Returns the project StudioOnline publish data object if the update and publish succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined page layout code).

#### Unpublish the project StudioOnline publish data

```
DEFINITION
DELETE http://apiserver/projects/:id/studioonlinepublishdata

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/studioonlinepublishdata", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Unpublishes the project StudioOnline publish data. The actual data will not be deleted.

##### Arguments

##### Returns

Returns a 204 No Content response on success. If the project StudioOnline publish data cannot be unpublished, this call returns an error.

### Project Advanced StudioOnline Configuration

#### Create a project Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/projects/:id/storeconfigurations

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/110160/storeconfigurations", {
    "store": "19",
    "useInStudioOnline": true,
    "title": "Water Wells in Africa",
    "urlOverride": "water-wells-in-africa",
    "description": "Your donation will help us provide clean and safe drinking water in Africa."
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "project": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": null,
    "endDate": null,
    "hideFromSearch": false,
    "title": "Water Wells in Africa",
    "urlOverride": "water-wells-in-africa",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Your donation will help us provide clean and safe drinking water in Africa.",
    "keywords": null,
    "layoutOverride": null
}

```

Creates a new project Advanced StudioOnline configuration.

##### Arguments

* store (required) - The unique id of the store this configuration is for. Must be a valid store Id.
* title (required) - The online title for the project when used in the specified store.
* description (optional) - The online description for the project when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the project title.
* useInStudioOnline (optional) - Whether the project should be used in the specified store.
* startDate (optional) - The date the project will become visible in the specified store.
* endDate (optional) - The date the project will be removed from the specified store.
* hideFromSearch (optional) - Whether the project should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the project when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default project layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate project that should be shown in StudioOnline if someone tries to navigate to this project.

##### Returns

Returns a project Advanced StudioOnline configuration object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a project Advanced StudioOnline configuration

```
DEFINITION
GET http://apiserver/projects/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110160/storeconfigurations/10033");

EXAMPLE RESPONSE
{
    "id": "10033",
    "project": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": null,
    "endDate": null,
    "hideFromSearch": false,
    "title": "Water Wells in Africa",
    "urlOverride": "water-wells-in-africa",
    "url": "https://www.myministry.com/donate/water-wells-in-africa",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Your donation will help us provide clean and safe drinking water in Africa.",
    "keywords": null,
    "layoutOverride": null
}

```

Retrieves the details of a project Advanced StudioOnline configuration. You need only supply the project id and configuration id.

##### Returns

Returns a project Advanced StudioOnline configuration object if valid ids were provided.

#### Update a project Advanced StudioOnline configuration

```
DEFINITION
POST http://apiserver/projects/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/110160/storeconfigurations/10033", {
    "startDate": "2017-09-01",
    "endDate": "2018-10-25"
});

EXAMPLE RESPONSE
{
    "id": "10033",
    "project": "110160",
    "store": "19",
    "storeDescription": "ASO US-English",
    "useInStudioOnline": true,
    "startDate": "2017-09-01",
    "endDate": "2018-10-25",
    "hideFromSearch": false,
    "title": "Water Wells in Africa",
    "urlOverride": "water-wells-in-africa",
    "url": "https://www.myministry.com/donate/water-wells-in-africa",
    "permanentRedirect": null,
    "permanentRedirectDescription": null,
    "description": "Your donation will help us provide clean and safe drinking water in Africa.",
    "keywords": null,
    "layoutOverride": null
}


```

Updates the specified project Advanced StudioOnline configuration by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title (optional) - The online title for the project when used in the specified store.
* description (optional) - The online description for the project when used in the specified store.
* urlOverride (optional) - The relative Url path that should be used instead of the project title.
* useInStudioOnline (optional) - Whether the project should be used in the specified store.
* startDate (optional) - The date the project will become visible in the specified store.
* endDate (optional) - The date the project will be removed from the specified store.
* hideFromSearch (optional) - Whether the project should be searchable in the specified store.
* keywords (optional) - Searchable keywords for the project when used in the specified store.
* layoutOverride (optional) - The unique id of the Advanced StudioOnline layout to be used instead of the default project layout. Must be a valide layout id.
* permanentRedirect (optional) - The alternate project that should be shown in StudioOnline if someone tries to navigate to this project.

##### Returns

Returns a project Advanced StudioOnline configuration object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid permanentRedirect).

#### Delete a project Advanced StudioOnline configuration

```
DEFINITION
DELETE http://apiserver/projects/:id/storeconfigurations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/110160/storeconfigurations/10033", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project Advanced StudioOnline configuration. It cannot be undone.

##### Arguments

* id (required) - The project Advanced StudioOnline configuration id of the configuration to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project Advanced StudioOnline configuration does not exist, this call returns an error.

#### List all project Advanced StudioOnline configurations

```
DEFINITION
GET http://apiserver/projects/:id/storeconfigurations

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110160/storeconfigurations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10033",
            "project": "110160",
            "store": "19",
            "storeDescription": "ASO US-English",
            "useInStudioOnline": true,
            "startDate": "2017-09-01",
            "endDate": "2018-10-25",
            "hideFromSearch": false,
            "title": "Water Wells in Africa",
            "urlOverride": "water-wells-in-africa",
            "url": "https://www.myministry.com/donate/water-wells-in-africa",
            "permanentRedirect": null,
            "permanentRedirectDescription": null,
            "description": "Your donation will help us provide clean and safe drinking water in Africa.",
            "keywords": null,
            "layoutOverride": null
        }
        {...},
        {...}
    ]
}

```

Returns a list of all project Advanced StudioOnline configurations matching the provided filter criteria.

##### Arguments

* id () - Filter list by an exact match on configuration id
* store () - Filter list by an exact match on store id
* project () - Filter list by an exact match in project code

##### Returns

A dictionary with an items property that contains an array of up to limit project Advanced StudioOnline configurations, starting at index offset. Each entry in the array is a separate project Advanced StudioOnline configuration object. If no more project Advanced StudioOnline configurations are available, the resulting array will be empty. This request should never return an error.

### Project Balances By Subaccount

#### List all project balances by subaccount

```
DEFINITION
GET http://apiserver/projects/:id/balancesbysubaccount

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/140140/balancesbysubaccount");

EXAMPLE RESPONSE
{
    "totalIncomeStatementBalance": 41869.01,
    "totalBalanceSheetBalance": 3010,
    "balances": {
        "paging": {
            "limit": 10,
            "offset": 0,
            "total": 1
        }
        "items": [
            {
                "subaccount": "001       ",
                "description": "Donations                               ",
                "balanceType": null,
                "incomeStatementBalancew": 40803.51,
                "balanceSheetBalance": 3010
            }
        ]
    }
}

```

Returns a list of all project balances by subaccount. It also returns the total income statement balance and the total balance sheet balance.

##### Arguments

##### Returns

An object that contains the total income statement, total balance sheet balance and a balances object with an items property that contains an array of up to limit project balances by subaccount, starting at index offset. Each entry in the array is a separate project balance by subaccount object. If no more project balances by subaccount are available, the resulting array will be empty. This request should never return an error.

### Project Balance Details

#### List all project balance details

```
DEFINITION
GET http://apiserver/projects/:id/balancedetails

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/140140/balancedetails?balanceType=I&subaccount=001");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "month": "01",
            "year": "2013",
            "beginningBalance": 24067.98,
            "endingBalance": 24067.98,
            "income": 0,
            "expense": 0,
            "otherActivity": 0,
            "assets": 0,
            "liabilities": 0
        }
    ]
}

```

Returns a list of all project balance details.

##### Arguments

* balanceType (required) - Filter the details by balance type. Must either be "I" or "A"
* subaccount (optional) - Filter the details by subaccount.

##### Returns

A dictionary with an items property that contains an array of up to limit project balance details, starting at index offset. Each entry in the array is a separate project balance detail object. If no more project balance details are available, the resulting array will be empty.

### Project Balance Details By Month

#### List all project balance details by month

```
DEFINITION
GET http://apiserver/projects/:id/balancedetailsbymonth

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/140140/balancedetailsbymonth?balanceType=I&month=06&year=2013&subaccount=001");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "documentType": "JE",
            "document": 5455,
            "glDate": "2013-06-30T00:00:00",
            "description": "Missionary Income             ",
            "glAccount": "       140140.40015.001",
            "credit": 200,
            "debit": 0,
            "currentCode": "USD",
            "glStatus": "POSTED",
            "exr": "                              ",
            "ledger": "AA",
            "icu": 8100,
            "obj": 40015,
            "sbl": null,
            "abr1": null,
            "abt1": null,
            "abr2": null,
            "abt2": null,
            "abr3": null,
            "abt3": null,
            "abr4": null,
            "abt4": null,
            "itm": 0
        }
    ]
}

```

Returns a list of all project balance details by month.

##### Arguments

* balanceType (required) - Filter the details by balance type. Must either be "I" or "A".
* month (required) - Filter the details by month. Must be a 1 or 2 digit number that represents the month (01 - 12).
* year (required) - Filter the details by year. Must be a 4 digit number that represents the year (yyyy).
* subaccount (optional) - Filter the details by subaccount.

##### Returns

A dictionary with an items property that contains an array of up to limit project balance details by month, starting at index offset. Each entry in the array is a separate project balance detail by month object. If no more project balance details by month are available, the resulting array will be empty.

### Send Projects Report By Email

```
DEFINITION
POST http://apiserver/projects/sendreportbyemail

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/sendreportbyemail", {
    "company":"1",
    "departmentStart":"100",
    "departmentEnd":"200",
    "currencyCode":"USD",
    "projectCodeStart":"100000",
    "projectCodeEnd":"100100",
    "ledger":"AA",
    "dateStart":"2015-05-01",
    "dateEnd":"2015-08-01",
    "groupBy":"Department",
});

EXAMPLE RESPONSE
204 No Content

```

This will begin processing of a projects report and send it by email to the logged in user.

##### Arguments

* company (required) - The company code for the report.
* departmentStart (required) - The starting department code for the report.
* departmentEnd (required) - The starting department code for the report.
* projectCodeStart (required) - The starting project code for the report.
* projectCodeEnd (required) - The starting project code for the report.
* ledger (required) - The ledger for the report
* groupBy (required) - How the report should be grouped. Must either be 'Project' or 'Department'.
* dateStart (optional) - The starting date for the report.
* dateEnd (optional) - The ending date for the report.
* currencyCode (optional) - The currency code for the report.

##### Returns

Returns a 204 No Content response on success.

### Project Account Relationships

#### Create a project account relationship

```
DEFINITION
POST http://apiserver/projects/:id/accountrelationships

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/accountrelationships", {
    "id": "1483320"
});

EXAMPLE RESPONSE
{
    "id": "CL",
    "accountName": "Hentry Winkler"
}

```

Creates a new project account relationship object

##### Arguments

* id (required) - The account relationship id. (This is the id of the account for the account relationship. It must be a valid account id.)

##### Returns

Returns a project account relationship object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined account relationship id).

#### Retrieve a project account relationship

```
DEFINITION
GET http://apiserver/projects/:id/accountrelationships/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/accountrelationships/1483320");

EXAMPLE RESPONSE
{
    "id": "1483320",
    "accountName": "Henry Winkler"
}

```

Retrieves the details of an existing project account relationship. You need only supply the project id and project account relationship id.

##### Returns

Returns a project account relationship object if a valid id was provided.

#### Delete a project account relationship

```
DEFINITION
DELETE http://apiserver/projects/:id/accountrelationships/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/accountrelationships/1483320", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project account relationship. It cannot be undone.

##### Arguments

* id (required) - The id of the account relationship to be deleted.

##### Returns

Returns a 204 No Content response on success. If the project account relationship id does not exist, this call returns an error.

#### List all project account relationships

```
DEFINITION
GET http://apiserver/projects/:id/accountrelationships

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/110102/accountrelationships");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "188320",
            "accountName": "Henry Winkler"
        }
    ]
}

```

Returns a list of all project account relationship.

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit project account relationships, starting at index offset. Each entry in the array is a separate project account relationship object. If no more project account relationships are available, the resulting array will be empty. This request should never return an error.

### Project StudioOnline Premiums

#### Create a project StudioOnline premium

```
DEFINITION
POST http://apiserver/projects/:id/studioonlonepremiums

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/studioonlonepremiums", {
    "store": null,
    "product": "101010",
    "sequence": 0,
    "start": null,
    "end": null
});

EXAMPLE RESPONSE
{
    "id": "5",
    "project": "7399",
    "projectDescription": "Wall Builders",
    "store": null,
    "product": "101010",
    "productDescription": "Nehemiah: The Wall Builder",
    "sequence": 15,
    "start": null,
    "end": null
}

```

Creates a new project StudioOnline premium object (Advanced StudioOnline only)

##### Arguments

* product (required) - The ProductCode which is the premium being offered for a donation to the project. (It must be a valid product code.)
* store () - The StoreCode in which the StudioOnline premium relationship exists. (It must be a valid store code.)
* sequence () - The soft order sequence for displaying in StudioOnline.
* start () - The start date for when the premium will be offered in StudioOnline. If null, the premium will always be offered. (If provided, it must be a valid SQL date.)
* end () - The end date for when the premium will be offered in StudioOnline. If null, the premium will always be offered. (If provided, it must be a valid SQL date.)

##### Returns

Returns a project StudioOnline premium object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined project or product code).

#### Retrieve a project StudioOnline premium

```
DEFINITION
GET http://apiserver/projects/:id/studioonlonepremiums/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/studioonlonepremiums/5");

EXAMPLE RESPONSE
{
    "id": "5",
    "project": "7399",
    "projectDescription": "Wall Builders",
    "store": null,
    "product": "101010",
    "productDescription": "Nehemiah: The Wall Builder",
    "sequence": 15,
    "start": null,
    "end": null
}

```

Retrieves the details of an existing project StudioOnline premium (Advanced StudioOnline only). You need only supply the project code and StudioOnline premium id.

##### Returns

Returns a project StudioOnline premium object if a valid id was provided.

#### Update a project StudioOnline premium

```
DEFINITION
POST http://apiserver/projects/:id/studioonlonepremiums/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/7399/studioonlonepremiums/5", {
    "start": "2018-01-27"
});

EXAMPLE RESPONSE
{
    "id": "5",
    "project": "7399",
    "projectDescription": "Wall Builders",
    "store": null,
    "product": "101010",
    "productDescription": "Nehemiah: The Wall Builder",
    "sequence": 15,
    "start": "2018-01-27",
    "end": null
}

```

##### Arguments

* product () - The ProductCode which is the premium being offered for a donation to the project. (It must be a valid product code.)
* store () - The StoreCode in which the StudioOnline premium relationship exists. (It must be a valid store code.)
* sequence () - The soft order sequence for displaying in StudioOnline.
* start () - The start date for when the premium will be offered in StudioOnline. If null, the premium will always be offered. (If provided, it must be a valid SQL date.)
* end () - The end date for when the premium will be offered in StudioOnline. If null, the premium will always be offered. (If provided, it must be a valid SQL date.)

##### Returns

Returns a subaccount object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a project StudioOnline premium

```
DEFINITION
DELETE http://apiserver/projects/:id/studioonlonepremiums/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/7399/studioonlonepremiums/5", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an StudioOnline premium (Advanced StudioOnline only). It cannot be undone.

##### Arguments

* id (required) - The id of the StudioOnline premium to be deleted.

##### Returns

Returns a 204 No Content response on success. If the StudioOnline premium id does not exist, this call returns an error.

#### List all project StudioOnline premiums

```
DEFINITION
GET http://apiserver/projects/:id/studioonlonepremiums

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/7399/studioonlonepremiums");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "5",
            "project": "7399",
            "projectDescription": "Wall Builders",
            "store": null,
            "product": "101010",
            "productDescription": "Nehemiah: The Wall Builder",
            "sequence": 15,
            "start": null,
            "end": null
        }
    ]
}

```

Returns a list of all StudioOnline premiums (Advanced StudioOnline only).

##### Arguments

##### Returns

A dictionary with an items property that contains an array of up to limit StudioOnline premiums, starting at index offset. Each entry in the array is a separate StudioOnline premium object. If no more StudioOnline premiums are available, the resulting array will be empty. This request should never return an error.

### Project Budgets

#### Create a project budget

```
DEFINITION
POST http://apiserver/projects/:projectId/budgets

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/MISSPROJ1/budgets", {
    "startDate": "2020-03-01",
    "endDate": "2021-02-28",
    "amount": 15043.55
});

EXAMPLE RESPONSE
{
    "id": "34879",
    "projectCode": "MISSPROJ1",
    "startDate": "2020-03-01",
    "endDate": "2021-02-28",
    "amount": 15043.55
}

```

Creates a new project budget. No budgets' start/end date ranges may overlap.

##### Arguments

* projectId (required) - The project code of the parent project under which to create the project budget.
* startDate (required) - The start date of the project budget. Must be less than or equal to endDate.
* endDate (required) - The end date of the project budget. Must be greater than or equal to startDate.
* amount (required) - The project budget amount. Must be greater than or equal to 0.

##### Returns

Returns a project budget object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a project budget

```
DEFINITION
GET http://apiserver/projects/:id/budgets/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/MISSPROJ1/budgets/34879");

EXAMPLE RESPONSE
{
    "id": "34879",
    "projectCode": "MISSPROJ1",
    "startDate": "2020-03-01",
    "endDate": "2021-02-28",
    "amount": 15043.55
}

```

Retrieves the details of an existing project budget.

##### Arguments

* projectId (required) - The parent project code of the project budget to be retrieved.
* id (required) - The id of the project budget to be retrieved.

#### Update a project budget

```
DEFINITION
POST http://apiserver/projects/:projectId/budgets/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/projects/MISSPROJ1/budgets/34879", {
    "endDate": "2021-01-31",
    "amount": 13590.68
});

EXAMPLE RESPONSE
{
    "id": "34879",
    "projectCode": "MISSPROJ1",
    "startDate": "2020-03-01",
    "endDate": "2021-01-31",
    "amount": 13590.68
}


```

Updates the specified project budget by setting the values of the parameters passed. Any parameters not provided will be left unchanged. The final properties of the project budget must correspond with the argument rules outlined in the [Create a project budget](#create-a-form-type-document) section.

##### Arguments

* projectId (required) - The parent project code of the project budget.
* id (required) - The id of the project budget.
* startDate (optional) - The start date of the project budget. Must be less than or equal to endDate.
* endDate (optional) - The end date of the project budget. Must be greater than or equal to startDate.
* amount (optional) - The project budget amount. Must be greater than or equal to 0.

##### Returns

Returns the project budget object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a project budget

```
DEFINITION
DELETE http://apiserver/projects/:projectId/budgets/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/projects/MISSPROJ1/budgets/41789", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a project budget. It cannot be undone.

##### Arguments

* projectId (required) - The parent project code of the project budget to be deleted.
* id (required) - The id of the project budget to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the project budget does not exist, this call returns an error.

#### List all project budgets

```
DEFINITION
GET http://apiserver/projects/:projectId/budgets

EXAMPLE REQUEST
$.get("http://localhost:49195/projects/MISSPROJ1/budgets");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "34879",
            "projectCode": "MISSPROJ1",
            "startDate": "2020-03-01",
            "endDate": "2021-01-31",
            "amount": 13590.68
        },
        {...}
    ]
}

```

Returns a list of all project budgets.

##### Arguments

* projectId (required) - The parent project code of all project budgets to be retrieved.

##### Returns

A dictionary with an items property that contains an array of up to limit project budgets, starting at index offset. Each entry in the array is a separate project budget object. If no more project budgets are available, the resulting array will be empty. This request should never return an error.

### Subaccounts

#### Create a subaccount

```
DEFINITION
POST http://apiserver/subaccounts

EXAMPLE REQUEST
$.post("http://localhost:49195/subaccounts", {
    "id": "001",
    "description": "General Support",
    "balanceType": "U"
});

EXAMPLE RESPONSE
{
    "id": "001",
    "description": "General Support",
    "objectAccount": null,
    "remitSubaccount": false,
    "balanceType": "U",
    "balanceTypeDescription": "Unrestricted",
    "isActive": true
}

```

##### Arguments

* id (required) - The subaccount id
* description (optional) - The subaccount description
* objectAccount (optional) - The object account
* remitSubaccount (optional) - Remit subaccount defaults to `false`
* balanceType (optional) - The subaccount balance type. Must be a valid code value for the code type `DDCBALTYPE`
* isActive (optional) - Specifies if the subaccount is active; defaults to `true`

##### Returns

Returns a subaccount object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a subaccount

```
DEFINITION
GET http://apiserver/subaccounts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/subaccounts/001");

EXAMPLE RESPONSE
{
    "id": "001",
    "description": "General Support",
    "objectAccount": null,
    "remitSubaccount": false,
    "balanceType": "U",
    "balanceTypeDescription": "Unrestricted",
    "isActive": true
}

```

Retrieves the details of an existing subaccount. You need only supply the subaccount id.

##### Returns

Returns a subaccount object if a valid id was provided.

#### Update a subaccount

```
DEFINITION
POST http://apiserver/subaccounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/subaccounts/001", {
    "balanceType": "T"
});

EXAMPLE RESPONSE
{
    "id": "001",
    "description": "General Support",
    "objectAccount": null,
    "remitSubaccount": false,
    "balanceType": "T",
    "balanceTypeDescription": "Temp Restricted",
    "isActive": true
}

```

##### Arguments

* description (optional) - The subaccount description
* objectAccount (optional) - The object account
* remitSubaccount (optional) - Remit subaccount defaults to `false`
* balanceType (optional) - The subaccount balance type. Must be a valid code value for the code type `DDCBALTYPE`
* isActive (optional) - Specifies if the subaccount is active; defaults to `true`

##### Returns

Returns a subaccount object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a subaccount

```
DEFINITION
DELETE http://apiserver/subaccount/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/subaccounts/001", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a subaccount. It cannot be undone.

##### Arguments

* id (required) - The id of the subaccount to be deleted.

##### Returns

Returns a 204 No Content response on success. If the subaccount id does not exist, this call returns an error.

#### List all subaccounts

```
DEFINITION
GET http://apiserver/subaccounts

EXAMPLE REQUEST
$.get("http://localhost:49195/subaccounts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 5
    }
    "items": [
        {
            "id": "001",
            "description": "General Support",
            "objectAccount": null,
            "remitSubaccount": false,
            "balanceType": "T",
            "balanceTypeDescription": "Temp Restricted",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all subaccounts.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in subaccount code
* description () - Filter list by partial match in subaccount description
* objectAccount () - Filter list by partial match in subaccount object account
* isActive () - Filter list by if the subaccount is active

##### Returns

A dictionary with an items property that contains an array of up to limit subaccounts, starting at index offset. Each entry in the array is a separate subaccount object. If no more subaccounts are available, the resulting array will be empty. This request should never return an error.

### Tax Rates

#### Create a tax rate

```
DEFINITION
POST http://apiserver/taxrates

EXAMPLE REQUEST
$.post("http://localhost:49195/taxrates", {
    "taxArea": "TX",
    "projectCategory": "BK",
    "taxRate1": 5,
    "isShippingTaxable": true,
    "shippingTaxRate1": 2.5,
    "startDate": "2010-01-01",
    "endDate": "2099-12-31"
});

EXAMPLE RESPONSE
{
    "id": "60",
    "taxArea": "TX",
    "projectCategory": "BK",
    "productCategoryDescription": "Books",
    "productCode": null,
    "productCodeDescription": null,
    "description": null,
    "taxRate1": 5,
    "taxRate2": 0,
    "taxRate3": 0,
    "taxRate4": 0,
    "taxRate5": 0,
    "isShippingTaxable": true,
    "shippingTaxRate1": 2.5,
    "shippingTaxRate2": 0,
    "shippingTaxRate3": 0,
    "shippingTaxRate4": 0,
    "shippingTaxRate5": 0,
    "startDate": "2010-01-01",
    "endDate": "2099-12-31"
}

```

##### Arguments

* taxArea (required) - The name of the tax area for the tax rate.
* description (optional) - The description of the tax rate.
* productCategory (optional) - The product category that this tax rate applies to. Values must be in `DDCPRODCAT`.
* productCode (optional) - The product code that this tax rate applies to. Values must be in `DDCPRODUCT`.
* taxRate1 (optional) - 1st tax rate.
* taxRate2 (optional) - 2nd tax rate.
* taxRate3 (optional) - 3rd tax rate.
* taxRate4 (optional) - 4th tax rate.
* taxRate5 (optional) - 5th tax rate.
* shippingTaxRate1 (optional) - 1st shipping tax rate.
* shippingTaxRate2 (optional) - 2nd shipping tax rate.
* shippingTaxRate3 (optional) - 3rd shipping tax rate.
* shippingTaxRate4 (optional) - 4th shipping tax rate.
* shippingTaxRate5 (optional) - 5th shipping tax rate.
* startDate (optional) - The date in which the tax rate is in effect.
* endDate (optional) - The date in which the tax rate is in is no longer effect.

##### Returns

Returns tax rate object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve a tax rate

```
DEFINITION
GET http://apiserver/taxrates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/taxrates/60");

EXAMPLE RESPONSE
{
    "id": "60",
    "taxArea": "TX",
    "projectCategory": "BK",
    "productCategoryDescription": "Books",
    "productCode": null,
    "productCodeDescription": null,
    "description": null,
    "taxRate1": 5,
    "taxRate2": 0,
    "taxRate3": 0,
    "taxRate4": 0,
    "taxRate5": 0,
    "isShippingTaxable": true,
    "shippingTaxRate1": 2.5,
    "shippingTaxRate2": 0,
    "shippingTaxRate3": 0,
    "shippingTaxRate4": 0,
    "shippingTaxRate5": 0,
    "startDate": "2010-01-01",
    "endDate": "2099-12-31"
}

```

Retrieves the details of an existing tax rate. You need only supply the tax rate id.

##### Returns

Returns tax rate object if a valid id was provided.

#### Update a tax rate

```
DEFINITION
POST http://apiserver/taxrates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/taxrates/60", {
        "taxRate2": 0.25,
});

EXAMPLE RESPONSE
{
    "id": "60",
    "taxArea": "TX",
    "projectCategory": "BK",
    "productCategoryDescription": "Books",
    "productCode": null,
    "productCodeDescription": null,
    "description": null,
    "taxRate1": 5,
    "taxRate2": 0.25,
    "taxRate3": 0,
    "taxRate4": 0,
    "taxRate5": 0,
    "isShippingTaxable": true,
    "shippingTaxRate1": 2.5,
    "shippingTaxRate2": 0,
    "shippingTaxRate3": 0,
    "shippingTaxRate4": 0,
    "shippingTaxRate5": 0,
    "startDate": "2010-01-01",
    "endDate": "2099-12-31"
}

```

##### Arguments

* taxArea (optional) - The name of the tax area for the tax rate.
* description (optional) - The description of the tax rate.
* productCategory (optional) - The product category that this tax rate applies to. Values must be in `DDCPRODCAT`.
* productCode (optional) - The product code that this tax rate applies to. Values must be in `DDCPRODUCT`.
* taxRate1 (optional) - 1st tax rate.
* taxRate2 (optional) - 2nd tax rate.
* taxRate3 (optional) - 3rd tax rate.
* taxRate4 (optional) - 4th tax rate.
* taxRate5 (optional) - 5th tax rate.
* shippingTaxRate1 (optional) - 1st shipping tax rate.
* shippingTaxRate2 (optional) - 2nd shipping tax rate.
* shippingTaxRate3 (optional) - 3rd shipping tax rate.
* shippingTaxRate4 (optional) - 4th shipping tax rate.
* shippingTaxRate5 (optional) - 5th shipping tax rate.
* startDate (optional) - The date in which the tax rate is in effect.
* endDate (optional) - The date in which the tax rate is in is no longer effect.

##### Returns

Returns tax rate object if the update succeeded. Any parameters not provided will be left unchanged.

#### Delete a tax rate

```
DEFINITION
DELETE http://apiserver/taxrates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/taxrates/60", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes tax rate. It cannot be undone.

##### Arguments

* id (required) - The id of the tax rate to be deleted.

##### Returns

Returns a 204 No Content response on success. If the tax rate id does not exist, this call returns an error.

#### List all tax rates

```
DEFINITION
GET http://apiserver/taxrates

EXAMPLE REQUEST
$.get("http://localhost:49195/taxrates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    }
    "items": [
        {
            "id": "60",
            "taxArea": "TX",
            "projectCategory": "BK",
            "productCategoryDescription": "Books",
            "productCode": null,
            "productCodeDescription": null,
            "description": null,
            "taxRate1": 5,
            "taxRate2": 0.25,
            "taxRate3": 0,
            "taxRate4": 0,
            "taxRate5": 0,
            "isShippingTaxable": true,
            "shippingTaxRate1": 2.5,
            "shippingTaxRate2": 0,
            "shippingTaxRate3": 0,
            "shippingTaxRate4": 0,
            "shippingTaxRate5": 0,
            "startDate": "2010-01-01",
            "endDate": "2099-12-31"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all tax rates.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* taxArea (optional) - The name of the tax area for the tax rate.
* productCategory (optional) - The product category that this tax rate applies to. Values must be in `DDCPRODCAT`.
* productCode (optional) - The product code that this tax rate applies to. Values must be in `DDCPRODUCT`.
* startDate (optional) - The date in which the tax rate is in effect.
* endDate (optional) - The date in which the tax rate is in is no longer effect.

##### Returns

A dictionary with an items property that contains an array of up to limit tax rates, starting at index offset. Each entry in the array is a separate tax rate object. If no more tax rates are available, the resulting array will be empty. This request should never return an error.

### Tax Quote

#### Get a tax quote

```
DEFINITION
POST http://apiserver/taxquote

EXAMPLE REQUEST
$.POST("http://localhost:49195/taxquote", {
    date: "2018-01-01",
    account: "9314",
    warehouse: "MAIN",
    company: "USA",
    shipTo: {
        line1: "8212 E Juneau Ave",
        postalCode: "53202",
        country: "USA"
    },
    shipToAddressId: "1234",
    currency: "USD",
    details: [{
        product: "BK1000",
        totalAmount: 12.0,
        quantity: 1,
        shipTo: {
            line1: "8212 E Juneau Ave",
            postalCode: "53202",
            country: "USA"
        },
        shipToAddressId: "1234"
    }]
});

EXAMPLE RESPONSE
{
    taxArea: "TX",
    totalTaxAdded: 0.91,
    totalTaxIncluded: 0,
    taxAmount1": 0.80,
    taxAmount2": 0.10,
    taxAmount3": 0.01,
    taxAmount4": 0,
    taxAmount5": 0
}

```

##### Returns

Returns the sales tax amounts.

##### Arguments

* date (optional) - The date the taxes will be calculated for.
* account (optional) - The account that the transaction is for, used to possibly consider exempt status.
* warehouse (optional) - The identifier of the warehouse (sets the origin address).
* company (required) - The company for the transaction.
* shipTo (required) - The destination of the shipment, the account's address. (required if not providing a shipToAddressId)
* shipToAddressId (required) - The address id for the destination of the shipment. (required if not providing a shipTo)
* currency (optional) - The currency type of the transaction.
* details (required) - An array of detail objects containing the following attributes:
* product (optional) - The product code for the order detail. Required if subscription is not provided. (Set the product to `SHIPPING` to calculate tax on shipping.)
* subscription (optional) - The subscription code for the order detail. Required if product is not provided.
* totalAmount (required) - The extended amount of the item (price \* quantity - discount).
* quantity (required) - The quantity of the order detail or subscription copy count.
* shipTo (optional) - This ship to address is primarily used for a subscription type details.
* shipToAddressId (optional) - This ship to address id is primarily used for a subscription type details.