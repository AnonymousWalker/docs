# NCOA Export

#### Run NCOA Export

```
DEFINITION
POST http://apiserver/ncoa/export

EXAMPLE REQUEST
$.post("http://localhost:49195/ncoa/export", {
    "job": "541",
    "segment": "1"
});

EXAMPLE RESPONSE
204 No Content

```

Runs the NCOA export process.

##### Arguments

* job (required) - the job number to use for export execution
* segment (required) - the segment number to use for export execution

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.

### Periodic Receipt Run

#### Reset a periodic receipt run

```
DEFINITION
POST http://apiserver/periodicreceipts/:id/reset

EXAMPLE REQUEST
$.post("http://localhost:49195/periodicreceipts/2055/reset");

EXAMPLE RESPONSE
204 No Content

```

Performs a reset of the specified periodic receipt run.

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.

#### Retrieve raw data for a periodic receipt run

```
DEFINITION
GET http://apiserver/periodicreceipts/:id/raw

EXAMPLE REQUEST
$.get("http://localhost:49195/periodicreceipts/2055/raw");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    }
    "items": [
        {
            "RecordId": 1839283,
            "RunId": 2055,
            "ReceiptId": 45138,
            "PageNumber": 1,
            "TotalNumberOfPages": 1,
            "AccountNumber": 45612,
            "FamilyId": 0,
            "AccountType": "I",
            ...
        },
        {...},
        {...}
    ]
}

```

Returns a list of periodic receipt run raw data records.

##### Returns

A dictionary with an items property that contains an array of up to limit periodic receipt run raw data records, starting at index offset. Each entry in the array is a separate periodic receipt run raw data record. If no more periodic receipt run raw data records are available, the resulting array will be empty. This request should never return an error.

#### Print a Periodic Receipt Run

```
DEFINITION
POST http://apiserver/periodicreceipts/:id/print

EXAMPLE REQUEST
$.post("http://localhost:49195/periodicreceipts/13829/print", {
    "accountNumber": "32345"
});

EXAMPLE RESPONSE
{
    "runId": "13829",
    "accountNumber": "32345",
    "formType": "MYFORMTP",
    "formTypeDeliveryMethod": "NOTEMAIL",
    "document": {
        "fileName": "Periodic Receipt Merge Doc.docx",
        "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
        "file": "UEsDBBQAAgAIAKyDe1AemujtOQEAAHcCAAARAAAAZG9jUHJvcHMvY29yZS54bWyVUstOwzAQ/JXI98S..."
    },
    "errors": [{
        "document": {
            "id": "12345",
            "sequenceNumber": 10,
            "documentAddress": "\\\\test\\path\\my-file.docx",
            "fileName": null,
            "fileMimeType": null,
            "reportId": null,
            "reportDescription": null
        },
        "message": "Could not find file '\\\\test\\path\\my-file.docx'."
    }]
}

```

Print a periodic receipt run.

##### Arguments

* id (required) - The run id of the periodic receipt run to be printed.
* accountNumber (optional) - A specific account number by which to filter the printed periodic receipt run.

##### Returns

If a mail merge for a single account would be performed, this will perform the merge and return the periodic receipt run object along with the generated document, or a zip file containing all generated documents if there is more than one, and any document errors. Otherwise it returns a periodic receipt run object immediately and the merge happens in the background. Returns an error if the periodic receipt run print parameters are invalid.

### Periodic Receipt Run Merged Documents

#### Retrieve a periodic receipt run merged document

```
DEFINITION
GET http://apiserver/periodicreceipts/:runId/documents/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/periodicreceipts/13829/documents/81382");

EXAMPLE RESPONSE
{
    "id": "81382",
    "runId": "13829",
    "sequenceNumber": 5,
    "fileName": "PeriodicReceipt.docx",
    "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
    "file": null,
    "printDate": "2018-07-15T02:31:37 PM"
}

```

Retrieves the details of an existing periodic receipt run merged document. You need only supply the id.

##### Arguments

* runId (required) - The id of the parent periodic receipt run.
* id (required) - The id of the periodic receipt run merged document to be retrieved.
* download (optional) - A `true` value will force the `file` to be retrieved as a Base64 string. Otherwise, `file` will be `null`.

#### Delete a periodic receipt run merged document

```
DEFINITION
DELETE http://apiserver/periodicreceipts/:runId/documents/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/periodicreceipts/13829/documents/81382", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a periodic receipt run merged document. It cannot be undone.

##### Arguments

* runId (required) - The id of the parent periodic receipt run.
* id (required) - The id of the periodic receipt run merged document to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the periodic receipt run merged document does not exist, this call returns an error.

#### List all periodic receipt run merged documents

```
DEFINITION
GET http://apiserver/periodicreceipts/:runId/documents

EXAMPLE REQUEST
$.get("http://localhost:49195/periodicreceipts/13829/documents");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "81382",
            "runId": "13829",
            "sequenceNumber": 5,
            "fileName": "PeriodicReceipt.docx",
            "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
            "file": null,
            "printDate": "2018-07-15T02:31:37 PM"
        },
        { ... },
        { ... }
    ]
}

```

Returns periodic receipt run merged documents for the specified print group.

##### Arguments

* runId (required) - The id of the parent periodic receipt run.

##### Returns

A dictionary with an items property that contains an array of up to limit periodic receipt run merged documents, starting at index offset. Each entry in the array is a separate periodic receipt run merged document object. If no more periodic receipt run merged documents are available, the resulting array will be empty. This request should never return an error.

### Pledge Statement Detail Summary

#### Retrieve summary data for a pledge statement

```
DEFINITION
GET http://apiserver/pledgestatementdetailsummary/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgestatementdetailsummary/4370");

EXAMPLE RESPONSE
{
    "id": "4370",
    "statementId": "1000000037",
    "accountNumber": "16230",
    "accountName": "Mr. John A Doe Jr.",
    "totalAmountPledged": "50.0000",
    "pledges": [
        {
            "pledgeId": "1172",
            "accountNumber": "16230",
            "pledgeCode": "050098",
            "projectCode": 413005,
            "amount": "50.0000",
            "sourceCode": "0727111",
            "subAccount": null,
            "deductible": "True",
            "pledgeStatus": "A",
            "errorMessage": ""
        }
    ],
    "donationAmount": null,
    "batch": null,
    "paymentDetails": null,
    "prorate": false
}

```

Returns pledge statement detail summary data.

##### Returns

The summary information of this pledge statement detail. This will include a list of all of the details that make up this summary.

#### Print a Pledge Statement Run

```
DEFINITION
POST http://apiserver/pledgestatementdetailsummary/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgestatementdetailsummary/4370", {
    "id": "4370",
    "statementId": "1000000037",
    "donationAmount": "50.00",
    "batch": {...},
    "paymentDetails": [],
    "prorate": false
};

EXAMPLE RESPONSE
{
    "id": "1419108",
    "account": "16230",
    "batch": "10703",
    "date": "2017-03-27",
    "status": "Y",
    "isTaxExempt": false,
    "mediaOutlet": "KLTY",
    "dma": "623",
    "currency": "USD",
    "contactMethod": null,
    "amount": 105.0000,
    "amountDue": 0.0000,
    "remainingAmountDue": 0.0000,
    "deposit": null,
    "depositStatus": null,
    "donationTotal": null,
    "productTotal": null,
    "shippingTotal": null,
    "taxTotal": null,
    "eventTotal": null,
    "subscriptionTotal": null,
    "arPaymentTotal": null,
    "response": {
        "id": 2023990,
        "method": null,
        "type": "RECEIPT",
        "profileGroup": null,
        "printGroup": null,
        "printDate": null,
        "paragraphs": [],
        "letter": "DRTY01",
        "isAutoAssigned": true,
        "completionText": null,
        "address": "1000041057",
        "inserts": null,
        "status": "H"
    },
    "letter": "DRTY01",
    "accountName": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "receiptNumber": null,
    "autoCalculateShipping": true,
    "company": "BLUE",
    "companyDescription": "Bluefin - Encrypted Keypad",
    "excludeFromGiftAid": false,
    "additionalDetails": {
        "additionalDetail1": ""
    },
    "couponCode": null,
    "couponDescription": null
}

```

Create a transaction for this pledge statement detail summary

##### Arguments

* id (required) - The detail id of the pledge statement summary of the transaction that is going to be created
* statementId (required) - The statement id of the pledge statement summary of the transaction that is going to be created
* donationAmount (required) - The amount of the transaction that is going to be created
* batch - (required) - The full batch information of the transaction that is going to be created
* paymentDetails (required) - The full payment information of the transaction that is going to be created
* prorate (required) - When this flag is true and the donation amount does not equal the total amount pleged, the individual donations for each pledge will adjusted proportionally

##### Returns

Returns a transaction object if the call succeeded and created a transaction. Returns 204 No Content if the call succeeded but no transaction was created. Returns an error if create parameters are invalid (e.g. specifying an undefined currency code or failing to specify a batch).

### Pledge Statement Run

#### Retrieve raw data for a pledge statement run

```
DEFINITION
GET http://apiserver/pledgestatements/:id/raw

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgestatements/13829/raw");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 50
    }
    "items": [
        {
            "RecordId": 1839283,
            "StatementId": 13829,
            "AccountNumber": 12738,
            "FamilyId": 0,
            "AccountType": "I",
            "Title": "Dr.",
            "FirstName": "James",
            "MiddleName": "Tiberius",
            ...
        },
        {...},
        {...}
    ]
}

```

Returns a list of pledge statement run raw data records.

##### Returns

A dictionary with an items property that contains an array of all pledge statement run raw data records returned by executing the Document Filter Query associated with the pledge statement run Form Type. Each entry in the array is a separate pledge statement run raw data record. This request will return an error if the Document Filter Query is invalid.

#### Print a Pledge Statement Run

```
DEFINITION
POST http://apiserver/pledgestatements/:id/print

EXAMPLE REQUEST
$.post("http://localhost:49195/pledgestatements/13829/print", {
    "accountNumber": "32345"
});

EXAMPLE RESPONSE
{
    "statementId": "13829",
    "accountNumber": "32345",
    "formType": "MYFORMTP",
    "formTypeDeliveryMethod": "NOTEMAIL",
    "document": {
        "fileName": "AR Statement Merge Doc.docx",
        "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
        "file": "UEsDBBQAAgAIAKyDe1AemujtOQEAAHcCAAARAAAAZG9jUHJvcHMvY29yZS54bWyVUstOwzAQ/JXI98S..."
    },
    "errors": [{
        "document": {
            "id": "12345",
            "sequenceNumber": 10,
            "documentAddress": "\\\\test\\path\\my-file.docx",
            "fileName": null,
            "fileMimeType": null,
            "reportId": null,
            "reportDescription": null
        },
        "message": "Could not find file '\\\\test\\path\\my-file.docx'."
    }]
}

```

Print a Pledge Statement run.

##### Arguments

* id (required) - The statement id of the pledge statement run to be printed.
* accountNumber (optional) - A specific account number by which to filter the printed pledge statement.

##### Returns

If a mail merge for a single account would be performed, this will perform the merge and return the Pledge Statement Run object along with the generated document, or a zip file containing all generated documents if there is more than one, and any document errors. Otherwise it returns an Pledge Statement Run object immediately and the merge happens in the background. Returns an error if the Pledge Statement print parameters are invalid.

### Pledge Statement Run Merged Documents

#### Retrieve a pledge statement run merged document

```
DEFINITION
GET http://apiserver/pledgestatements/:id/documents/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgestatements/13829/documents/81382");

EXAMPLE RESPONSE
{
    "id": "81382",
    "statementId": "13829",
    "sequenceNumber": 5,
    "fileName": "PledgeStatement.docx",
    "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
    "printDate": "2018-07-15T02:31:37 PM"
}

```

Retrieves the details of an existing pledge statement run merged document. You need only supply the id.

##### Arguments

* id (required) - The id of the pledge statement run merged document to be retrieved.
* download (optional) - A `true` value will force the `file` to be retrieved as a Base64 string. Otherwise, `file` will be `null`.

#### Delete a pledge statement run merged document

```
DEFINITION
DELETE http://apiserver/pledgestatements/:id/documents/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/pledgestatements/13829/documents/81382", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a pledge statement run merged document. It cannot be undone.

##### Arguments

* id (required) - The id of the pledge statement run merged document to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the pledge statement run merged document does not exist, this call returns an error.

#### List all pledge statement run merged documents

```
DEFINITION
GET http://apiserver/pledgestatements/:id/documents

EXAMPLE REQUEST
$.get("http://localhost:49195/pledgestatements/13829/documents");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "81382",
            "statementId": "13829",
            "sequenceNumber": 5,
            "fileName": "PledgeStatement.docx",
            "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
            "printDate": "2018-07-15T02:31:37 PM"
        },
        { ... },
        { ... }
    ]
}

```

Returns pledge statement run merged documents for the specified print group.

##### Returns

A dictionary with an items property that contains an array of up to limit pledge statement run merged documents, starting at index offset. Each entry in the array is a separate pledge statement run merged document object. If no more pledge statement run merged documents are available, the resulting array will be empty. This request should never return an error.

### Print Queue Items

#### Retrieve a print queue item

```
DEFINITION
GET http://apiserver/printqueueitems/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/printqueueitems/23491");

EXAMPLE RESPONSE
{
    "id": "23491",
    "communicationType": "RECEIPT",
    "communicationDescription": "Donation Receipts",
    "productionRunId": "13654",
    "profileGroupId": "56413",
    "printId": "9648",
    "queueDateTime": "2019-01-27T08:50:54 AM",
    "queuedByAccessorId": "56431",
    "queuedByAccessorDescription": "Jim Thompson - Internal User",
    "queuedByAccessorEmailAddressOverride": null,
    "startDateTime": "2019-01-27T09:45:21 AM",
    "endDateTime": "2019-01-27T09:45:48 AM",
    "status": "C",
    "statusDescription": "Completed",
    "processedRecordCount": 150,
    "totalRecordCount": 150,
    "shouldCancel": false,
    "cancelDateTime": null,
    "canceledByAccessorId": null,
    "canceledByAccessorDescription": null,
    "cancelReason": null,
    "errorMessage": null
}

```

Retrieves the details of an existing print queue item. You need only supply the id.

##### Arguments

* id (required) - The id of the print queue item to be retrieved.

#### List all print queue items

```
DEFINITION
GET http://apiserver/printqueueitems

EXAMPLE REQUEST
$.get("http://localhost:49195/printqueueitems");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "23491",
            "communicationType": "RECEIPT",
            "communicationDescription": "Donation Receipts",
            "productionRunId": "13654",
            "profileGroupId": "56413",
            "printId": "9648",
            "queueDateTime": "2019-01-27T08:50:54 AM",
            "queuedByAccessorId": "56431",
            "queuedByAccessorDescription": "Jim Thompson - Internal User",
            "queuedByAccessorEmailAddressOverride": null,
            "startDateTime": "2019-01-27T09:45:21 AM",
            "endDateTime": "2019-01-27T09:45:48 AM",
            "status": "C",
            "statusDescription": "Completed",
            "processedRecordCount": 150,
            "totalRecordCount": 150,
            "shouldCancel": false,
            "cancelDateTime": null,
            "canceledByAccessorId": null,
            "canceledByAccessorDescription": null,
            "cancelReason": null,
            "errorMessage": null
        },
        { ... },
        { ... }
    ]
}

```

Returns a list of all print queue items.

##### Returns

A dictionary with an items property that contains an array of up to limit print queue items, starting at index offset. Each entry in the array is a separate print queue item object. If no more print queue items are available, the resulting array will be empty. This request should never return an error.

#### Cancel a print queue item

```
DEFINITION
POST http://apiserver/printqueueitems/:id/cancel

EXAMPLE REQUEST
$.post("http://localhost:49195/printqueueitems/23491/cancel", {
    "reason": "Accidentally printed this."
});

EXAMPLE RESPONSE
{
    "id": "23491",
    "communicationType": "RECEIPT",
    "communicationDescription": "Donation Receipts",
    "productionRunId": null,
    "profileGroupId": null,
    "printId": "9648",
    "queueDateTime": "2019-01-27T08:50:54 AM",
    "queuedByAccessorId": "56431",
    "queuedByAccessorDescription": "Jim Thompson - Internal User",
    "queuedByAccessorEmailAddressOverride": null,
    "startDateTime": "2019-01-27T09:45:21 AM",
    "endDateTime": null,
    "status": "W",
    "statusDescription": "Canceling",
    "processedRecordCount": 50,
    "totalRecordCount": 150,
    "shouldCancel": true,
    "cancelDateTime": "2019-01-27T09:46:32 AM",
    "canceledByAccessorId": "37281",
    "canceledByAccessorDescription": "Donna Lawson - Internal User",
    "cancelReason": "Accidentally printed this.\r\n\r\nProduction Run Id: 13654\r\nProfile Group Id: 56413",
    "errorMessage": null
}

```

Cancel a Ready or Running print queue item. Note that for Running print queue items cancellation may not happen immediately, in which case a "Canceling" status will be returned.

##### Arguments

* reason (optional) - The reason this print queue item is being canceled. If not provided, the default value is "Canceled By User."

##### Returns

Returns the canceling/canceled print queue item object if the call succeeded. Returns an error if the print queue item is not in a Ready or Running state.

### Production Runs

#### Process a new production run

```
DEFINITION
POST http://apiserver/productionruns/process

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/process" {
    "includeOrders": true
});

EXAMPLE RESPONSE
204 No Content

```

Executes a new production run process.

##### Arguments

* includeOrders (optional) - Whether the process should include orders.
* includeReceipts (optional) -Whether the process should include receipts.
* includeLetters (optional) -Whether the process should include letters.
* includeSubscriptions (optional) - Whether the process should include subscriptions.
* includeEvents (optional) - Whether the process should include event acknowledgements.
* includePledges (optional) - Whether the process should include pledge acknowledgements.
* includeNonCashGifts (optional) - Whether the process should include non-cash gifts.
* combo (optional) - Whether the process should include combos.
* company (optional) - The company to filter on.
* letterCode (optional) - The letter code to filter on.
* department (optional) - The organization department to filter on.
* dateFrom (optional) - The date start filtering by.
* dateTo (optional) - The date to end filtering by. If dateFrom and dateTo are provided, dateTo must be greater than or equal to dateFrom.
* warehouse (optional) - The warehouse to filter by.
* productCode (optional) - The product code to filter by.
* shouldPrintAutomatically (optional) - Whether all profile groups should be printed (when allowed) after the production run process has finished.

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any invalid values are provided, this call will return an error.

#### Process a new single response production run

```
DEFINITION
POST http://apiserver/productionruns/processsingleresponse

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/processsingleresponse", {
    "responseId": "476856"
});

EXAMPLE RESPONSE
{
    "responseId": "476856",
    "printGroup": "3618",
    "profileGroup": "3177",
    "formType": "LTR"
}

```

Executes a new production run process on a single response.

##### Arguments

* responseId (required) - a reponse id to perform a production run on.

##### Returns

Returns the print group id and profile group id created by the production run, as well as the form type associated with that profile group.

#### Retrieve a production run

```
DEFINITION
GET http://apiserver/productionruns/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2055");

EXAMPLE RESPONSE
{
    "runId": "2055",
    "quantity": 15,
    "available": 0,
    "errors": 2,
    "notShipped": 0,
    "onHold": 0,
    "printed": 13,
    "runDate": "2015-04-06",
    "status": "Y"
}

```

* Retrieves the details of an existing production run object. You only need supply the production run id.

##### Arguments

* id (required) - The run id of the production run to retrieve.

##### Returns

Returns a production run object if a valid id was provided.

#### Reset a production run

```
DEFINITION
POST http://apiserver/productionruns/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2055", {
    "reset": true
});

EXAMPLE RESPONSE
{
    "runId": "2055",
    "quantity": 0,
    "available": 0,
    "errors": 0,
    "notShipped": 0,
    "onHold": 0,
    "printed": 0,
    "runDate": "2015-04-06",
    "status": "Y"
}

```

Performs a reset of the specified production run.

##### Arguments

* reset - Whether or not to perform a reset for the specified production run

##### Returns

* Returns the production run object if the reset succeeded. Returns an error if update parameters are invalid.

#### List all production runs

```
DEFINITION
GET http://apiserver/productionruns

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 90
    },
    "items": [
        {
            "runId": "2063",
            "quantity": 0,
            "available": 0,
            "errors": 8,
            "notShipped": 0,
            "onHold": 0,
            "printed": 0,
            "runDate": "2015-04-14",
            "status": "Y"
        },
        { ... },
        { ... }
    ]
}

```

Returns a list of all production runs matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by partial match on production run id
* profileGroupId (optional) - Filter list by partial match on profile group id
* runDate (optional) - Filter list by partial match on run date
* filter (optional) - Filter list by availability (`P` for Available to Print, `S` for Available to Ship)

##### Returns

A dictionary with an items property that contains an array of up to limit production runs, starting at index offset. Each entry in the array is a separate production run object.

### Production Run Address Validation Errors

#### Reset a production run address validation error

```
DEFINITION
POST http://apiserver/productionruns/:id/errors/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2058/errors/71106", {
    "reset": true
    "responseId": "453580"
});

EXAMPLE RESPONSE
204 No Content

```

Performs a reset of the specified production run address validation error.

##### Arguments

* reset () - Whether to perform a reset on the specified address validation error
* responseId (optional) - The associated transaction response id for the address validation error (required if performing a reset)

##### Returns

Returns a 204 No Content response on success.

#### List all production run address validation errors

```
DEFINITION
GET http://apiserver/productionruns/:id/errors

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2058/errors");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 10
    },
    "items": [
        {
            "id": "71106",
            "runId": "2058",
            "responseId": "453580",
            "account": "17450",
            "docNumber": "241217",
            "date": "2015-04-14",
            "errorMessage": "Missing Address"
        },
        { ... },
        { ... }
    ]
}

```

Returns a list of all production run address validation errors for the specified production run.

##### Arguments

* id (required) - The id of the production run to fetch address validation errors for

##### Returns

A dictionary with an items property that contains an array of up to limit address validation errors, starting at index offset. Each entry in the array is a separate address validation error object.

### Production Run Profile Groups

#### Retrieve a profile group

```
DEFINITION
GET http://apiserver/productionruns/:id/profilegroups/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2058/profilegroups/2972");

EXAMPLE RESPONSE
{
    "id": "2972",
    "runId": "2058",
    "description": "EVENTS/EVTACK",
    "status": "Y",
    "priority": null,
    "formType": "EVTACK",
    "pickableProducts": false,
    "responseMethod": null,
    "communicationType": "EVENTACK",
    "insertCode1": null,
    "insertCode2": null,
    "insertCode3": null,
    "insertCode4": null,
    "insertCode5": null,
    "isIdentical": false,
    "quantity": 5,
    "available": 2,
    "errors": 0,
    "onHold": 0,
    "printed": 3,
    "readyToShip": 4,
    "shipped": 5,
    "start": 0,
    "printDate": 0
}

```

Returns the specified profile group for the specified production run.

#### Reset a profile group

```
DEFINITION
POST http://apiserver/productionruns/:id/profilegroups/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2058/profilegroups/2972", {
    "reset": true
});

EXAMPLE RESPONSE
{
    "id": "2972",
    "runId": "2058",
    "description": "EVENTS/EVTACK",
    "status": "Y",
    "priority": null,
    "formType": "EVTACK",
    "pickableProducts": false,
    "responseMethod": null,
    "communicationType": "EVENTACK",
    "insertCode1": null,
    "insertCode2": null,
    "insertCode3": null,
    "insertCode4": null,
    "insertCode5": null,
    "isIdentical": false,
    "quantity": 0,
    "available": 0,
    "errors": 0,
    "onHold": 0,
    "printed": 0,
    "readyToShip": 4,
    "shipped": 5,
    "start": 0,
    "printDate": 0
}

```

Resets a specified profile group

##### Arguments

* reset (optional) - Send `true` to perform a reset of the profile group.
* resetPrinted (optional; if `reset` is `true`, this argument will be ignored) - Send `true` to reset the printing for the profile group.

##### Returns

Returns the updated state of the profile group after the reset has completed successfully. If the production run or the profile group do not exist, this call will return an error.

#### Print a profile group

```
DEFINITION
POST http://apiserver/productionruns/:id/profilegroups/:id/print

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2058/profilegroups/2972/print", {
    "numToPrint": 2
    "communicationType": "EVENTACK"
});

EXAMPLE RESPONSE
{
    "printGroupId": 3608
}

```

Performs a print on the responses available for the specified profile group.

##### Arguments

* numToPrint (required) - The number of responses to print/send. `0` indicates all available. The number provided can not exceed the number of responses avialable for the specified profile group.
* contactType (optional) - The organization contact type to be used for the print.
* addressOverrideType (optional) - Override value for the address type for receipts and letters.
* emailOverrideType (optional) - Override value for the email type for receipts and letters.
* salutationOverrideType (optional) - Override value for the salutation type for receipts and letters.
* communicationType (required) - The communication type associated with the form type to print.
* suppressFileExport (optional) - Whether the file export process should be suppressed or bypassed.

##### Returns

Returns the ID of the print group created if successful. If invalid criteria is provided, this call will return an error.

#### Quick ship a profile group

```
DEFINITION
POST http://apiserver/productionruns/:id/profilegroups/:id/quickship

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2058/profilegroups/2972/quickship", {
    "shipMethod": "USPS"
    "shippingCost": 20
});

EXAMPLE RESPONSE
204 No Content

```

Performs a quick ship against the profile group.

##### Arguments

* shipMethod (optional) - The actual shipping method used for the profile group quick ship.
* shippingCost (optional) - The shipping cost associated with the quick ship.

##### Returns

Returns a 204 No Content repsonse code upon successful quick ship. If the production run or profile group do not exist, this call will return an error.

#### List all profile groups

```
DEFINITION
GET http://apiserver/productionruns/:id/profilegroups

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2058/profilegroups");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 6
    },
    "items": [
        {
            "id": "3148",
            "runId": "2058",
            "description": "PRODUCTS/10/PSUSA/STANDARD",
            "status": "Y",
            "priority": "STANDARD",
            "formType": "PSUSA",
            "pickableProducts": true,
            "responseMethod": null,
            "communicationType": "ORDER",
            "insertCode1": null,
            "insertCode2": null,
            "insertCode3": null,
            "insertCode4": null,
            "insertCode5": null,
            "isIdentical": false,
            "quantity": 7,
            "available": 5,
            "errors": 0,
            "onHold": 0,
            "printed": 2,
            "readyToShip": 4,
            "shipped": 5,
            "start": 0,
            "printDate": 0
        },
        { ... },
        { ... }
    ]
}

```

Return a list of profile groups for the specified production run.

##### Returns

A dictionary with an items property that contains an array of up to limit profile groups, starting at index offset. Each entry in the array is a separate profile gorup object. If no more profile groups are available, the resulting array will be empty. This request should never return an error.

### Production Run Profile Group Responses

#### List all profile group responses

```
DEFINITION
GET http://apiserver/productionruns/:id/profilegroups/:id/responses

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2058/profilegroups/2972/responses", {
    "isPrinted": true
});

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "account": "17286",
            "accountName": "Mr. and Mrs. Matthew Mason",
            "docNumber": "241567",
            "tableId": "T01",
            "id": 476747,
            "method": null,
            "type": null,
            "profileGroup": "2972",
            "printGroup": "8329",
            "printDate": null,
            "shippedStatus": "R",
            "shippedStatusDescription: "Ready to be Shipped",
            "paragraphs": [],
            "letter": "PACU",
            "isAutoAssigned": true,
            "completionText": null,
            "address": "1000026620",
            "inserts": null,
            "status": null
        },
        { ... },
        { ... }
    ]
}

```

Returns responses for the specified profile group.

##### Arguments

* isPrinted (optional) - Is the response printed or not. If not provided, the call will return both printed and not printed.

##### Returns

A dictionary with an items property that contains an array of up to limit profile group responses, starting at index offset. Each entry in the array is a separate response object. If no more responses are available, the resulting array will be empty. This request should never return an error.

#### Reset a profile group response

```
DEFINITION
POST http://apiserver/productionruns/:id/profilegroups/:id/responses

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2058/profilegroups/2972/responses", {
    "reset": true
});

EXAMPLE RESPONSE
204 No Content

```

Resets a specified profile group responses. Printed responses will be marked as not printed, and not printed responses will be removed from the print group.

##### Arguments

* reset (required) - If true, profile group response is reset.

##### Returns

Returns a 204 No Content HTTP status code if successful. If invalid values are provided, this call will return an error.

### Production Run Profile Group Print Groups

#### List all profile group print groups

```
DEFINITION
GET http://apiserver/productionruns/:id/profilegroups/:id/printgroups

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2058/profilegroups/2972/printgroups");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "4765",
            "profileGroupId": "2972",
            "printDate": "2019-02-19T07:59:03 PM",
            "emailSubject": null,
            "responseQuantity": 3
        },
        { ... },
        { ... }
    ]
}

```

Returns print groups for the specified profile group.

##### Returns

A dictionary with an items property that contains an array of up to limit profile group print groups, starting at index offset. Each entry in the array is a separate profile group print group object. If no more profile group print groups are available, the resulting array will be empty. This request should never return an error.

#### Reset a profile group print group

```
DEFINITION
POST http://apiserver/productionruns/:id/profilegroups/:id/printgroups/:id/reset

EXAMPLE REQUEST
$.post("http://localhost:49195/productionruns/2058/profilegroups/2972/printgroups/4765/reset");

EXAMPLE RESPONSE
204 No Content

```

Resets a specified profile group print group.

##### Returns

Returns nothing if all responses under the profile group print group were reset and the profile group print group was deleted or the updated state of the profile group print group otherwise after the reset has completed successfully. If the production run, profile group, or profile group print group do not exist, this call will return an error.

#### Retrieve raw data for a profile group print group

```
DEFINITION
GET http://apiserver/productionruns/:id/profilegroups/:id/printgroups/:id/raw

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2058/profilegroups/2972/printgroups/4765/raw");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    }
    "items": [
        {
            "RecordId": 1839283,
            "ResponseId": 4561237,
            "PageNumber": 1,
            "TotalNumberOfPages": 1,
            "PrintGroupId": 4765,
            "AccountNumber": 235342,
            "FamilyId": 0,
            "AccountType": "I",
            ...
        },
        {...},
        {...}
    ]
}

```

Returns a list of profile group print group raw data records, fetched by executing the DocumentFilterQuery on the profile group's form type.

##### Returns

A dictionary with an items property that contains an array of up to limit profile group print group raw data records, starting at index offset. Each entry in the array is a separate profile group print group raw data record. If no more profile group print group raw data records are available, the resulting array will be empty. This request should never return an error.

### Production Run Profile Group Print Group Merged Documents

#### Retrieve a profile group print group merged document

```
DEFINITION
GET http://apiserver/productionruns/:id/profilegroups/:id/printgroups/:id/documents/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2058/profilegroups/2972/printgroups/4765/documents/78942");

EXAMPLE RESPONSE
{
    "id": "78942",
    "printGroupId": "4765",
    "sequenceNumber": 5,
    "fileName": "GenReceipt.docx",
    "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
}

```

Retrieves the details of an existing profile group print group merged document. You need only supply the id.

##### Arguments

* id (required) - The id of the profile group print group merged document to be retrieved.
* download (optional) - A `true` value will force the `file` to be retrieved as a Base64 string. Otherwise, `file` will be `null`.

#### List all profile group print group merged documents

```
DEFINITION
GET http://apiserver/productionruns/:id/profilegroups/:id/printgroups/:id/documents

EXAMPLE REQUEST
$.get("http://localhost:49195/productionruns/2058/profilegroups/2972/printgroups/4765/documents");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 7
    },
    "items": [
        {
            "id": "78942",
            "printGroupId": "4765",
            "sequenceNumber": 5,
            "fileName": "GenReceipt.docx",
            "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
        },
        { ... },
        { ... }
    ]
}

```

Returns print group merged documents for the specified print group.

##### Returns

A dictionary with an items property that contains an array of up to limit profile group print group merged documents, starting at index offset. Each entry in the array is a separate profile group print group merged document object. If no more profile group print group merged documents are available, the resulting array will be empty. This request should never return an error.

### Recurring Transactions

#### Retrieve a recurring transaction

```
DEFINITION
GET http://apiserver/recurringtransactions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/recurringtransactions/1000000398");

EXAMPLE RESPONSE
{
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "id": "1000000398",
    "errorGroupId": "30575",
    "status": "E",
    "isDonation": true,
    "account": "16231",
    "accountName": "Matt and Angie Mason",
    "total": 50,
    "currency": "USD",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "useOnDay": "1",
    "useOnDay": "1st",
    "category": null,
    "company": "BLUE",
    "paymentType": "CC",
    "paymentTypeDescription": "Credit Card",
    "cardNumber": null,
    "expiration": null,
    "nameOnCard": null,
    "accountNumber": null,
    "routingNumber": null,
    "accountType": null,
    "prenotification": null,
    "numberCommitted": 0,
    "numberRemaining": 0,
    "lastUsed": null,
    "lastBatch": null,
    "lastDocument": null,
    "start": "2014-12-01",
    "end": null,
    "shortComment": "",
    "source": "072711",
    "referenceNumber": "VISA-1111 01/2018 Matt Mason",
    "sourceDescription": "New Accounts",
    "linkedPledgeCode": null,
    "linkedPledgeDescription": null,
    "savedPayment": 12345,
    "savedPaymentName": "My Visa"
}

```

Retrieves the details of an existing recurring transaction. You need only supply the id.

##### Arguments

* id (required) - The id of the recurring transaction to be retrieved.

#### List all recurring transactions

```
DEFINITION
GET http://apiserver/recurringTransactions

EXAMPLE REQUEST
$.get("http://localhost:49195/recurringTransactions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 720
    },
    "items": [
        {
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null,
            "id": "1000000398",
            "errorGroupId": "30575",
            "status": "E",
            "isDonation": true,
            "account": "16231",
            "accountName": "Matt and Angie Mason",
            "total": 50,
            "currency": "USD",
            "frequency": "M",
            "frequencyDescription": "Monthly",
            "useOnDay": "1",
            "useOnDay": "1st",
            "category": null,
            "company": "BLUE",
            "paymentType": "CC",
            "paymentTypeDescription": "Credit Card",
            "cardNumber": null,
            "expiration": null,
            "nameOnCard": null,
            "accountNumber": null,
            "routingNumber": null,
            "accountType": null,
            "prenotification": null,
            "numberCommitted": 0,
            "numberRemaining": 0,
            "lastUsed": null,
            "lastBatch": null,
            "lastDocument": null,
            "start": "2014-12-01",
            "end": null,
            "shortComment": "",
            "source": "072711",
            "sourceDescription": "New Accounts",
            "referenceNumber": "VISA-1111 01/2018 Matt Mason",
            "linkedPledgeCode": null,
            "linkedPledgeDescription": null,
            "savedPayment": 12345,
            "savedPaymentName": "My Visa"
        },
        { ... },
        { ... }
    ]
}

```

##### Arguments

* account (optional) - Filter by account number
* includeFamily (optional) - When `true` is provided, all recurring transactions on the family are be returned. Ignored if `account` is not specified.
* activeAccountsOnly (optional; Default: `true`) - When `true` is provided, the results will filter to only return records that for active accounts.
* category (optional) - Filter by partial match on category
* company (optional) - Filter by partial match on company
* errorGroupId (optional) - Filter by error group
* frequency (optional) - Filter by partial match on frequency
* isDonation (optional) - When value is `true`, only recurring donations will be returned. When value is `false`, only AR recurring payments will be returned.
* linkedPledgeId (optional) - Filter by pledge id
* nameOnCard (optional) - Partial match by nameOnCard
* status (optional) - Filter by status
* paymentType (optional) - Filter by payment type
* useOnDayFrom (optional; Default: `1`) - Specify the start of the use on day range. Criteria is ignored when `useOnDayTo` is not specified
* useOnDayTo (optional; Default: `31`) - Specify the end of the use on day range. Criteria is ignored when `useOnDayFrom` is not specified
* endDateFrom (optional) - Specify the start of the end date range. It will be all recurring transactions where the endDate is greater than or equal to the `endDateFrom`.

##### Returns

Returns a list of all recurring transactions across all accounts. See [Account Recurring Transactions](#account-recurring-transactions) if needing to add or edit a recurring transaction.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

#### Delete a recurring transaction

```
DEFINITION
DELETE http://apiserver/recurringtransactions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/recurringtransactions/1000000398", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a recurring transaction. It cannot be undone.

##### Arguments

* id (required) - The id of the recurring transaction to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the recurring transaction does not exist, this call returns an error.

#### Recurring transactions post

```
DEFINITION
POST http://apiserver/recurringTransactionsPost

EXAMPLE REQUEST
$.post("http://localhost:49195/recurringTransactionsPost", {
    "company": "4",
    "currency": "USD"
});

EXAMPLE RESPONSE
204 No Content

```

Initiates an asynchronous recurring transaction post.

##### Arguments

* paymentType (optional)
* company (required)
* currency (required)
* frequency (optional)
* dayFrom (optional; Default: `1`)
* dayTo (optional; Default: `31`)
* category (optional)
* isDonation (optional; Default: `true`)
* batchDate (optional)
* isPrintReceipt (optional; Default `true`)
* paymentGatewayCode (optional) - The company payment gateway code to perform recurring for. If not provided, recurring will run on all payment gateways of the company.
* batchCategory (optional) - if provided, the batch created for the transactions is stamped with this batch category.
* letterCode (optional) - if provided, the response created for the transaction will be be assigned the provided letter code. This sets isAutoAssigned to false;
* product (optional; required if `warehouse` is specified) - Indicates an additional order with the product code should be built on the resulting transactions.
* warehouse (optional; required if `product` is specified) - Specifies the warehouse for the `product`.
* quantity (optional; Default: `1` when `product` and `warehouse` are specified) - Specifies the quantity of the `product`
* shipMethod (optional) - Shiping method for the `product`
* merchant (deprecated, optional) - if provided, the recurring that are processed must match the merchant (Should use `paymentGatewayCode` instead.)

##### Returns

Returns a 204 No Content response if the asynchronous recurring transaction post process was successfully initiated.

#### Recurring transactions repost

```
DEFINITION
POST http://apiserver/recurringTransactionsRepost

EXAMPLE REQUEST
$.post("http://localhost:49195/recurringTransactionsRepost", {
    "errorGroupId": "30507",
    "useSameBatch": true,
    "batchNumber": "7487"
});

EXAMPLE RESPONSE
204 No Content

```

Initiates an asynchronous recurring transaction repost.

##### Arguments

* errorGroupId (required)
* useSameBatch (required; default: `true`)
* batchNumber (required; if `useSameBatch` is true, provided batch number will be used. if `useSameBatch` is false, value should be 0)
* isPrintReceipt (optional; Default `true`)
* batchCategory (optional) - if provided and a new batch is being created, the batch is stamped with this batch category.
* letterCode (optional) - if provided, the response created for the transaction will be be assigned the provided letter code. This sets isAutoAssigned to false;
* product (optional; required if `warehouse` is specified) - Indicates an additional order with the product code should be built on the resulting transactions.
* warehouse (optional; required if `product` is specified) - Specifies the warehouse for the `product`.
* quantity (optional; Default: `1` when `product` and `warehouse` are specified) - Specifies the quantity of the `product`
* shipMethod (optional) - Shiping method for the `product`

##### Returns

Returns a 204 No Content response if the asynchronous recurring transaction repost process was successfully initiated.