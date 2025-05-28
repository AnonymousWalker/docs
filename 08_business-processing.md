# Business Processing

### Account Imports

#### Retrieve a account import

```
DEFINITION
GET http://apiserver/accountimports/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accountimports/1000000689");

EXAMPLE RESPONSE
{
    "id": "1000000689",
    "description": "Import Transaction Test",
    "externalSystemId": "DDC",
    "importType": "TEST",
    "batchProcessType": null,
    "status": "P",
    "dataSource": "DDC"
}

```

Retrieves the details of an existing account import. You need only supply the id.

##### Arguments

* id (required) - The id of the account import to be retrieved.

#### List all account imports

```
DEFINITION
GET http://apiserver/accountimports

EXAMPLE REQUEST
$.get("http://localhost:49195/accountimports?externalSystemId=DDC");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000000689",
            "description": "Import Transaction Test",
            "externalSystemId": "DDC",
            "importType": "TEST",
            "batchProcessType": null,
            "status": "P",
            "dataSource": "DDC"
        },
        {...},
    ]
}

```

Returns a list of all account imports.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* batchProcessType (optional) - Batch process type for the import
* description (optional) - Description for the import
* dataSource (optional) - Datasource of the import
* externalSystemId (optional) - External system id of the import
* importId (optional) - Id of the import
* importType (optional) - Type of the import
* status (optional) - Status of the import

##### Returns

A dictionary with an items property that contains an array of up to limit account imports, starting at index offset. Each entry in the array is a separate account import object. If no more account imports are available, the resulting array will be empty. This request should never return an error.

### Account Imports Process

#### Run an account import process

```
DEFINITION
POST http://apiserver/accountimports/:id/process

EXAMPLE REQUEST
$.post("http://localhost:49195/accountimports/1000000548/process", {
    "batchType": "N"
    "company": "4"
    "acquisitionImport": false
    "acquisitionDeduped": false
    "useBulkImport": true
});

EXAMPLE RESPONSE
204 No Content

```

Executes a new account import run process.

##### Arguments

* batchType (required) - The batch type: 'S' if specified in the import table, 'N' for create new batch from company, or 'E' for use existing batch.
* batchNumber (optional) - The batch number to use for import. Required if batchType is 'E'.
* company (optional) - The company to create a new batch for. Required if batchType is 'N'.
* acquisitionImport (optional) - Is the import an acquisition import.
* acquisitionDeduped (optional) - Is the import deduped.
* useBulkImport (optional) - Should we use bulk import (if supported).

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any invalid values are provided, this call will return an error.

### Account Import Details

#### Retrieve an account import detail

```
DEFINITION
GET http://apiserver/accountimports/:importId/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accountimports/1000000548/details/1000023268");

EXAMPLE RESPONSE
{
    "id": "1000023268",
    "account": "17309",
    "externalId": "",
    "methodOfAccountAssignment": null,
    "status": "P",
    "source": "EV11CPCATL",
    "mediaId": null,
    "accountStatus": null,
    "q05RecordId": null,
    "importGroupId": null,
    "title": null,
    "firstName": null,
    "middleName": null,
    "lastName": null,
    "suffix": null,
    "organization": null,
    "accountType": null,
    "familyMemberType": null,
    "familyConsolidate": false,
    "allowTransactions": false,
    "gender": null,
    "addressType": null,
    "addressLine1": null,
    "addressLine2": null,
    "addressLine3": null,
    "city": null,
    "state": null,
    "zipPostal": null,
    "country": null,
    "addressIsPoBox": null,
    "validatedDate": null,
    "deliveryPoint": null,
    "userVerifiedAccessorId": null,
    "userVerifiedAccessorIdDescription": null,
    "isDefaultBilling": null,
    "isDefaultShipping": null
}

```

Retrieves the details of an existing account import detail. You need only supply the ids.

##### Arguments

* id (required) - The id of the account import detail to be retrieved.

#### Update an account import detail

```
DEFINITION
POST http://apiserver/accountimports/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accountimports/1000000548/details/1000023268", {
    "source": "0700"
});

EXAMPLE RESPONSE
{
    "id": "1000023268",
    "account": "17309",
    "externalId": "",
    "methodOfAccountAssignment": null,
    "status": "P",
    "source": "0700",
    "mediaId": null,
    "accountStatus": null,
    "q05RecordId": null,
    "importGroupId": null,
    "title": null,
    "firstName": null,
    "middleName": null,
    "lastName": null,
    "suffix": null,
    "organization": null,
    "accountType": null,
    "familyMemberType": null,
    "familyConsolidate": false,
    "allowTransactions": false,
    "gender": null,
    "addressType": null,
    "addressLine1": null,
    "addressLine2": null,
    "addressLine3": null,
    "city": null,
    "state": null,
    "zipPostal": null,
    "country": null,
    "addressIsPoBox": null,
    "validatedDate": null,
    "deliveryPoint": null,
    "userVerifiedAccessorId": null,
    "userVerifiedAccessorIdDescription": null,
    "isDefaultBilling": null,
    "isDefaultShipping": null
}

```

Updates the specified account import detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* accountNumber (optional) - The account number for the import detail.
* accountStatus (optional) - The account status for the import detail.
* mediaId (optional) - The associated media Id for the import detail.
* source (optional) - The source code for the import detail.
* status (optional) - The import detail status of the import detail.

##### Returns

Returns the account import detail object if the update succeeded. Returns an error if update parameters are invalid.

#### List all account import details

```
DEFINITION
GET http://apiserver/accountimports/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/accountimports/1000000548/details?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000023268",
            "account": "17309",
            "externalId": "",
            "methodOfAccountAssignment": null,
            "status": "P",
            "source": "0700",
            "mediaId": null,
            "accountStatus": null,
            "q05RecordId": null,
            "importGroupId": null,
            "title": null,
            "firstName": null,
            "middleName": null,
            "lastName": null,
            "suffix": null,
            "organization": null,
            "accountType": null,
            "familyMemberType": null,
            "familyConsolidate": false,
            "allowTransactions": false,
            "gender": null,
            "addressType": null,
            "addressLine1": null,
            "addressLine2": null,
            "addressLine3": null,
            "city": null,
            "state": null,
            "zipPostal": null,
            "country": null,
            "addressIsPoBox": null,
            "validatedDate": null,
            "deliveryPoint": null,
            "userVerifiedAccessorId": null,
            "userVerifiedAccessorIdDescription": null,
            "isDefaultBilling": null,
            "isDefaultShipping": null
        },
        {...},
    ]
}

```

Returns a list of all account import details.

##### Arguments

* status (optional) - Filter on the status of the import detail. Valid statuses are E (Error in processing), P (Processed), and Y (Ready for processing).

##### Returns

A dictionary with an items property that contains an array of up to limit account import details, starting at index offset. Each entry in the array is a separate account import detail object. If no more account import details are available, the resulting array will be empty. This request should never return an error.

### AR Statement Run

#### Run an AR Statement Process

```
DEFINITION
POST http://apiserver/arstatements/process

EXAMPLE REQUEST
$.post("http://localhost:49195/arstatements/process", {
    "currency": "USD",
    "company": "BLUE",
    "start": "2016-03-16",
    "end": "2016-05-16",
    "jobNumber": "550",
    "segment": "1"
});

EXAMPLE RESPONSE
204 No Content

```

Creates a new AR Statement run.

##### Arguments

* currency (required) - The to currency code value be used to run the AR statement process.
* company (optional) - The company code to be used to run the AR statement process.
* start (optional) - The start date to use when processing the AR statement.
* end (optional) - The ending date to use when processing the AR statement.
* formType (optional) - The form type associate with the AR statement run when printing.
* thresholdAmount (optional) - The threshold amount to use when considering accounts for processing in the AR statement.
* jobNumber (required) - The segmentation job number to be used to run the AR statement process.
* segment (required) - The segmentation job segment number to be used to run the AR statement process.
* addressType (optional) - The optional override type for mailing address to be used to run the AR statement process.
* emailType (optional) - The optional override type for email address to be used to run the AR statement process.

##### Returns

Returns a HTTP status code 204 No Content if the call succeeded. Returns an error if AR statement run parameters are invalid.

#### Retrieve raw data for an AR statement run

```
DEFINITION
GET http://apiserver/arstatements/:id/raw

EXAMPLE REQUEST
$.get("http://localhost:49195/arstatements/13829/raw");

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
            "ContactId": NULL,
            "PageNumber": 1,
            "TotalNumberOfPages": 1,
            "AccountNumber": 12738,
            "FamilyId": 0,
            "AccountType": "I",
            ...
        },
        {...},
        {...}
    ]
}

```

Returns a list of AR statement run raw data records.

##### Returns

A dictionary with an items property that contains an array of all AR statement run raw data records returned by executing the Document Filter Query associated with the AR statement run Form Type. Each entry in the array is a separate AR statement run raw data record. This request will return an error if the Document Filter Query is invalid.

#### Print an AR Statement Run

```
DEFINITION
POST http://apiserver/arstatements/:id/print

EXAMPLE REQUEST
$.post("http://localhost:49195/arstatements/13829/print", {
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

Print an AR Statement run.

##### Arguments

* id (required) - The statement id of the AR statement run to be printed.
* accountNumber (optional) - A specific account number by which to filter the printed AR statement.

##### Returns

If a mail merge for a single account would be performed, this will perform the merge and return the AR Statement Run object along with the generated document, or a zip file containing all generated documents if there is more than one, and any document errors. Otherwise it returns an AR Statement Run object immediately and the merge happens in the background. Returns an error if the AR Statement print parameters are invalid.

### AR Statement Run Merged Documents

#### Retrieve an AR statement run merged document

```
DEFINITION
GET http://apiserver/arstatements/:id/documents/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/arstatements/3728/documents/81382");

EXAMPLE RESPONSE
{
    "id": "81382",
    "statementId": "3728",
    "sequenceNumber": 5,
    "fileName": "ARStatement.docx",
    "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
    "printDate": "2018-07-15T02:31:37 PM"
}

```

Retrieves the details of an existing AR statement run merged document. You need only supply the id.

##### Arguments

* id (required) - The id of the AR statement run merged document to be retrieved.
* download (optional) - A `true` value will force the `file` to be retrieved as a Base64 string. Otherwise, `file` will be `null`.

#### Delete an AR statement run merged document

```
DEFINITION
DELETE http://apiserver/arstatements/:id/documents/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/arstatements/3728/documents/81382", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an AR statement run merged document. It cannot be undone.

##### Arguments

* id (required) - The id of the AR statement run merged document to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the AR statement run merged document does not exist, this call returns an error.

#### List all AR statement run merged documents

```
DEFINITION
GET http://apiserver/arstatements/:id/documents

EXAMPLE REQUEST
$.get("http://localhost:49195/arstatements/3728/documents");

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
            "statementId": "3728",
            "sequenceNumber": 5,
            "fileName": "ARStatement.docx",
            "fileMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
            "printDate": "2018-07-15T02:31:37 PM"
        },
        { ... },
        { ... }
    ]
}

```

Returns AR statement run merged documents for the specified print group.

##### Returns

A dictionary with an items property that contains an array of up to limit AR statement run merged documents, starting at index offset. Each entry in the array is a separate AR statement run merged document object. If no more AR statement run merged documents are available, the resulting array will be empty. This request should never return an error.

#### Create an automatic AR adjustment

```
DEFINITION
POST http://apiserver/aradjustments

EXAMPLE REQUEST
$.post("http://localhost:49195/aradjustments", {
    "job": 541,
    "segment": 1,
    "date": "2015-09-15",
    "amount": 5,
    "payType": "CC",
    "company": "2",
    "codeType": "CAMPUS",
    "codeValue": "PHCM",
    "letter": "ABC"
});

EXAMPLE RESPONSE
{
    "id": "17",
    "job": "541",
    "segment": "1",
    "date": "2015-09-15",
    "amount": 5,
    "payType": "CC",
    "company": "2",
    "codeType": "CAMPUS",
    "codeValue": "PHCM",
    "letter": "ABC",
    "status": null,
    "totalAmount": null,
    "numberOfTransactions": null
}

```

Creates a new automatic AR adjustment.

##### Arguments

* job (required) - the segmentation job for the newly created AR adjustment
* segment (required) - the segment number for the newly created AR adjustment
* date (required) - the on-or-before date for the newly created AR adjustment
* amount (required) - the amount for the newly created AR adjustment
* payType (required) - the payment type for the newly created AR adjustment
* company (required) - the company code for the newly created AR adjustment
* codeType (optional) - the code type for the newly created AR adjustment
* codeValue (optional) - the code value for the newly created AR adjustment
* letter (optional) - the letter code for the newly created AR adjustment

##### Returns

Returns an automatic AR adjustment object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an automatic AR adjustment

```
DEFINITION
GET http://apiserver/aradjustments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/aradjustments/17");

EXAMPLE RESPONSE
{
    "id": "17",
    "job": "541",
    "segment": "1",
    "date": "2015-09-15",
    "amount": 5,
    "payType": "CC",
    "company": "2",
    "codeType": "CAMPUS",
    "codeValue": "PHCM",
    "letter": "ABC",
    "status": null,
    "totalAmount": null,
    "numberOfTransactions": null
}

```

Retrieves the details of an existing automatic AR adjustment. You need only supply the id.

##### Arguments

* id (required) - The id of the automatic AR adjustment to be retrieved.

#### Update an automatic AR adjustment

```
DEFINITION
POST http://apiserver/aradjustments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/aradjustments/17", {
    "job": "539",
    "segment": "0"
});

EXAMPLE RESPONSE
{
    "id": "17",
    "job": "539",
    "segment": "0",
    "date": "2015-09-15",
    "amount": 5,
    "payType": "CC",
    "company": "2",
    "codeType": "CAMPUS",
    "codeValue": "PHCM",
    "letter": "ABC",
    "status": null,
    "totalAmount": null,
    "numberOfTransactions": null
}

```

Updates the specified automatic AR adjustment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* job (optional) - the segmentation job to update the automatic AR adjustment with
* segment (optional) - the segment number to update the automatic AR adjustment with
* date (optional) - the on-or-before date to update the automatic AR adjustment with
* amount (optional) - the amount to update the automatic AR adjustment with
* payType (optional) - the payment type to update the automatic AR adjustment with
* company (optional) - the company code to update the automatic AR adjustment with
* codeType (optional) - the code type to update the automatic AR adjustment with
* codeValue (optional) - the code value to update the automatic AR adjustment with
* letter (optional) - the letter code to update the automatic AR adjustment with

##### Returns

Returns the automatic AR adjustment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an automatic AR adjustment

```
DEFINITION
DELETE http://apiserver/aradjustments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/aradjustments/17", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a automatic AR adjustment. It cannot be undone.

##### Arguments

* id (required) - The id of the automatic AR adjustment to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the automatic AR adjustment does not exist, this call returns an error.

#### List all automatic AR adjustments

```
DEFINITION
GET http://apiserver/aradjustments

EXAMPLE REQUEST
$.get("http://localhost:49195/aradjustments?payType=CC&company=2");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "17",
            "job": "541",
            "segment": "1",
            "date": "2015-09-15",
            "amount": 5,
            "payType": "CC",
            "company": "2",
            "codeType": "CAMPUS",
            "codeValue": "PHCM",
            "letter": "ABC",
            "status": null,
            "totalAmount": null,
            "numberOfTransactions": null
        },
        {...},
    ]
}

```

Returns a list of all automatic AR adjustment.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* job (optional) - the segmentation job to filter the search results on
* segment (optional) - the segment number to filter the search results on
* date (optional) - the on-or-before date to filter the search results on
* amount (optional) - the amount to filter the search results on
* payType (optional) - the payment type to filter the search results on
* company (optional) - the company code to filter the search results on
* codeType (optional) - the code type to filter the search results on
* codeValue (optional) - the code value to filter the search results on
* letter (optional) - the letter code to filter the search results on

##### Returns

A dictionary with an items property that contains an array of up to limit automatic AR adjustment, starting at index offset. Each entry in the array is a separate automatic AR adjustment object. If no more automatic AR adjustment are available, the resulting array will be empty. This request should never return an error.