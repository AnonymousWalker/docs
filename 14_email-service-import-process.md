# Email Service Import Process

```
DEFINITION
POST http://apiserver/emailserviceimports/process

EXAMPLE REQUEST
$.post("http://localhost:49195/emailserviceimports/process", {
    "emailService": "SILVERPOP",
    "syncFromDate": "2015-01-01"
});

EXAMPLE RESPONSE
204 No Content

```

Creates a new email service import process.

##### Arguments

* emailService (required) - the email service code to process imports for
* syncFromDate (optional) - the starting date to retrieve email activity from; required if NOT using Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP`. If using Enhanced `SILVERPOP` or `MAILCHIMP` and action is `ACCOUNT` this value is used; if it is left blank, it will import from the last successful import run.
* action (optional) - the action to perform, either `EMAILEVENT` (import email events) or `ACCOUNT` (import accounts); required if using Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP`
* listName (optional) - the list name from which to import the accounts from the email service; only used for Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP` when the action is `ACCOUNT`. If not provided, all accounts in the email service database will be imported.
* databaseName (optional) - the database name from which to import the accounts from the email service; only used for Enhanced `SILVERPOP`, `ESILVERPOP`, or `MAILCHIMP`

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.

### File Imports

#### Create a file import

```
DEFINITION
POST http://apiserver/fileimports

EXAMPLE REQUEST
$.post("http://localhost:49195/fileimports", {
    "fileImportType": "DDCACCT",
    "batchProcessType": "N",
    "dataSource": "DDC",
    "batchCompany": "0",
    "fileImportFile": {
        "fileName": "Filename.csv",
        "file": "data:text/csv;base64,dXNlcl9pZCxuYW1lLGVtYWlaWwsMjAxOC0wNi0xMg0=="
    }
});

EXAMPLE RESPONSE
{
    "id": "123",
    "accessorId": "1234",
    "accessorDescription": "Accessor Person - Internal User",
    "batchCompany": "0",
    "batchNumber": null,
    "batchProcessType": "N",
    "batchProcessTypeDescription": "New",
    "dataSource": "DDC",
    "dataSourceDescription": "DDC",
    "fileColumnHeaders": ["FirstName", "LastName", "EmailAddress", "SourceCode",...]
    "fileImportFieldMapping": null
    "fileImportFile": {
        "fileImportFileId": "20",
        "fileImportId": "123",
        "fileName": "Filename.csv",
        "fileMimeType": "text/csv",
        "file": null
    },
    "fileImportType": "DDCACCT",
    "fileImportTypeDescription": "Account Import",
    "importId": null,
    "importStatus": null,
    "importStatusDescription": null,
    "status": "N",
    "statusDescription": "New"
}

```

Returns a file import object if the call succeeded. Returns an error if create parameters are invalid.

##### Arguments

* fileImportType (optional) - The fileImportType of the file import
* batchProcessType (optional) - The batchProcessType of the file import
* dataSource (optional) - The dataSource of the file import
* fileImportFieldMapping (optional) - The field mapping object used for this file import
* batchCompany (conditionally required) - The batch company of the file import. This field is required if the batch process type is New ('N'), otherwise it will be ignored.
* batchNumber (conditionally required) - The batch number of the file import. This field is required if the batch process type is Existing ('E'), otherwise it will be ignored.
* fileImportFile (required) - The file object to be imported
* fileImportFile.fileName (required) - The name of the file
* fileImportFile.file (required) - The MIME type and Base64 encoded file string sent in the following format: `data:{MIME Type};base64,{Base64 Encoded String}`

##### Returns

Returns a file import object if the call succeeded. Returns an error if the create parameters are invalid (e.g. specifying an invalid file import type).

#### Retrieve a file import

```
DEFINITION
GET http://apiserver/fileimports/:fileImportId

EXAMPLE REQUEST
$.get("http://localhost:49195/fileimports/123");

EXAMPLE RESPONSE
{
    "id": "123",
    "accessorId": "1234",
    "accessorDescription": "Accessor Person - Internal User",
    "batchCompany": "0",
    "batchNumber": null,
    "batchProcessType": "N",
    "batchProcessTypeDescription": "New",
    "dataSource": "DDC",
    "dataSourceDescription": "DDC",
    "fileColumnHeaders": ["FirstName", "LastName", "EmailAddress", "SourceCode",...]
    "fileImportFieldMapping": null
    "fileImportFile": {
        "fileImportFileId": "20",
        "fileImportId": "123",
        "fileName": "Filename.csv",
        "fileMimeType": "text/csv",
        "file": null
    },
    "fileImportType": "DDCACCT",
    "fileImportTypeDescription": "Account Import",
    "importId": null,
    "importStatus": null,
    "importStatusDescription": null,
    "status": "N",
    "statusDescription": "New"
}

```

Retrieves the details of an existing file import. You need only supply the id.

##### Arguments

* fileImportId (required) - The id of the file import to be retrieved.
* isPreview (optional) - `isPreview=true` will populate fileImportFieldMapping with the first row of the file.

##### Returns

Returns a file import object if a valid id was provided.

#### Update a file import

```
DEFINITION
POST http://apiserver/fileimports/:fileImportId

EXAMPLE REQUEST
$.post("http://localhost:49195/fileimports/123", {
    "batchCompany": "PAYCONEX",
    "fileImportFieldMapping": {
        "fieldMappings": {
            "account": {
                "sourceCode": {
                    "fileColumnName": "SourceCode"
                },
                "firstName": {
                    "fileColumnName": "FirstName"
                },
                "lastName": {
                    "fileColumnName": "LastName"
                },
                "codes": [
                    {
                        "type": {
                            "staticValue": "DDCGENDER"
                        },
                        "value": {
                            "fileColumnName": "Gender"
                        }
                    },
                    {
                        "type": {
                            "staticValue": "FAVCOLOR"
                        },
                        "value": {
                            "fileColumnName": "FavoriteColor"
                        }
                    }
                ],
                "dates": [
                    {
                        "type": {
                            "staticValue": "DDCBDAY"
                        },
                        "value": {
                            "fileColumnName": "BirthDay"
                        }
                    }
                ],
                "emails": [
                    {
                        "emailAddress": {
                            "fileColumnName": "EmailAddress"
                        },
                        "type": {
                            "fileColumnName": "EmailType"
                        },
                        "useAsPrimary": {
                            "fileColumnName": "IsPrimaryEmail"
                        }
                    },
                    {
                        "emailAddress": {
                            "fileColumnName": "EmailAddress2"
                        },
                        "type": {
                            "fileColumnName": "EmailType2"
                        },
                        "useAsPrimary": {
                            "fileColumnName": "IsPrimaryEmail2"
                        }
                    }
                ]
            },
            "transaction": {
                "amount": {
                    "fileColumnName": "TranAmount"
                },
                "batchNumber": {
                    "fileColumnName": "TranBatchNumber"
                },
                "documentNumber": {
                    "fileColumnName": "TranDocumentNumber"
                }
            }
        }
    }
});

EXAMPLE RESPONSE
{
    "id": "123",
    "accessorId": "1234",
    "accessorDescription": "Accessor Person - Internal User",
    "batchProcessType": "N",
    "batchProcessTypeDescription": "New",
    "dataSource": "DDC",
    "dataSourceDescription": "DDC",
    "batchCompany": "PAYCONEX",
    "batchNumber": null,
    "fileImportFieldMapping": {
        "id": "22",
        "account": {
            "familyOrOrganizationGroupId": null,
            "accountNumber": null
            "accountStatus": null,
            "sourceCode": {
                "fileColumnName": "SourceCode"
            },
            "mediaId": null,
            "title": null,
            "firstName": {
                "fileColumnName": "FirstName"
            },
            "middleName": null,
            "lastName": {
                "fileColumnName": "LastName"
            },
            "suffix": null,
            "organizationName": null,
            "accountType": null,
            "relationshipId": null,
            "familyMemberType": null,
            "familyConsolidate": null,
            "allowTransactions": null,
            "gender": null,
            "address": {
                "type": null,
                "line1": null,
                "line2": null,
                "line3": null,
                "line4": null,
                "city": null,
                "state": null,
                "postalCode": null,
                "country": null,
                "isPOBox": null,
                "deliveryPoint": null,
                "validatedDate": null,
                "userVerifiedAccessorId": null
            },
            "shouldUpdateAddress": null,
            "otherAddresses": [],
            "phones": [],
            "emails": [
                {
                    "type": {
                        "fileColumnName": "EmailType"
                    },
                    "emailAddress": {
                        "fileColumnName": "EmailAddress"
                    },
                    "useAsPrimary": {
                        "fileColumName": "IsPrimaryEmail"
                    },
                    "functionalCategory": null,
                    "optOutIndicator": null,
                    "optOutReason": null,
                    "optOutDate": null
                },
                {
                    "type": {
                        "fileColumnName": "EmailType2"
                    },
                    "emailAddress": {
                        "fileColumnName": "EmailAddress2"
                    },
                    "useAsPrimary": {
                        "fileColumName": "IsPrimaryEmail2"
                    },
                    "functionalCategory": null,
                    "optOutIndicator": null,
                    "optOutReason": null,
                    "optOutDate": null
                }
            ],
            "relationships": [],
            "codes": [
                {
                    "type": {
                        "staticValue": "DDCGENDER"
                    },
                    "value": {
                        "fileColumnName": "Gender"
                    }
                },
                {
                    "type": {
                        "staticValue": "FAVCOLOR"
                    },
                    "value": {
                        "fileColumnName": "FavoriteColor"
                    }
                }
            ],
            "dates": [
                {
                    "type": {
                        "staticValue": "DDCBDAY"
                    },
                    "value": {
                        "fileColumnName": "BirthDay"
                    }
                }
            ],
            "notes": [],
            "numbers": [],
            "communication": {
                "date": null,
                "type": null,
                "shortComment": null,
                "longComment": null,
                "direction": null,
                "externalDocumentAddress": null,
                "sourceCode": null,
                "queueAssignedUserId": null,
                "category": null,
                "addToQueue": null,
                "assignedToAccessor": null,
                "status": null,
                "response": {
                    "letterCode": null,
                    "letterCompletionText": null,
                    "paragraphCode1": null,
                    "paragraphCompletionText1": null,
                    "paragraphCode2": null,
                    "paragraphCompletionText2": null,
                    "paragraphCode3": null,
                    "paragraphCompletionText3": null,
                    "paragraphCode4": null,
                    "paragraphCompletionText4": null,
                    "paragraphCode5": null,
                    "paragraphCompletionText5": null,
                    "paragraphCode6": null,
                    "paragraphCompletionText6": null
                },
                "codes": [],
                "dates": [],
                "notes": [],
                "numbers": []
            }
        },
        "transaction": {
            "documentNumber": {
                "fileColumnName": "TranDocumentNumber"
            },
            "batchNumber": {
                "fileColumnName": "TranBatchNumber"
            },
            "amount": {
                "fileColumnName": "TranAmount"
            },
            "amountDue": null,
            "status": null,
            "assignment": null,
            "currency": null,
            "contactMethod": null,
            "taxExempt": null,
            "designedMarketArea": null,
            "attachment": null,
            "excludeFromGiftAid": null,
            "response": {
                "letterCode": null,
                "letterCompletionText": null,
                "paragraphCode1": null,
                "paragraphCompletionText1": null,
                "paragraphCode2": null,
                "paragraphCompletionText2": null,
                "paragraphCode3": null,
                "paragraphCompletionText3": null,
                "paragraphCode4": null,
                "paragraphCompletionText4": null,
                "paragraphCode5": null,
                "paragraphCompletionText5": null,
                "paragraphCode6": null,
                "paragraphCompletionText6": null
            },
            "notes": [],
            "donations": [
                {
                    "catalogCode": null,
                    "catalogItemCode": null,
                    "isAnonymous": null,
                    "isDeductible": null,
                    "isFromIRA": null,
                    "pledgeCode": null,
                    "projectCode": null,
                    "relatedAccountRelationshipId": null,
                    "shortComment": null,
                    "sourceCode": {
                        "fileColumnName": "TranGiftSourceCode"
                    },
                    "subaccount": null,
                    "totalAmount": {
                        "fileColumnName": "TranGiftAmount"
                    }
                }
            ],
            "payments": [
                {
                    "amount": {
                        "fileColumnName": "TranPaymentAmount"
                    },
                    "depositStatus": null,
                    "eftBankAccountNumber": null,
                    "eftBankAccountType": null,
                    "eftRoutingNumber": null,
                    "expirationMonth": null,
                    "expirationYear": null,
                    "maskedCardNumber": null,
                    "merchantId": null,
                    "nameOnCard": null,
                    "paymentType": {
                        fileColumnName: "TranPaymentType"
                    },
                    "referenceNumber": null,
                    "token": null
                }
            ]
        }
    },
    "fileImportFile": {
        "fileImportFileId": "21",
        "fileImportId": "123",
        "fileName": "Filename2.csv",
        "fileMimeType": "text/csv",
        "file": null
    },
    "fileImportType": "DDCACCT",
    "fileImportTypeDescription": "Account Import",
    "importId": null,
    "importStatus": null,
    "importStatusDescription": null,
    "status": "V",
    "statusDescription": "Validation Required"
}

```

Updates the specified file import by setting the values of the parameters passed. Any parameters not provided will be left unchanged. Note that the `fileImportFile` object cannot be updated. It can only be used to replace the original file with a new one.

##### Arguments

* fileImportType (optional) - The fileImportType of the file import
* batchProcessType (optional) - The batchProcessType of the file import
* dataSource (optional) - The dataSource of the file import
* fileImportFieldMapping (optional) - The field mapping object for this file import
* importId (optional) - The import Id of the import created by this file import
* batchCompany (conditionally required) - The batch company of the file import. This field is required if the batch process type is New ('N'), otherwise it will be ignored.
* batchNumber (conditionally required) - The batch number of the file import. This field is required if the batch process type is Existing ('E'), otherwise it will be ignored.
* fileImportFile (optional) - The file object to be imported
* fileImportFile.fileName (required if replacing the existing file) - The name of the replacement file
* fileImportFile.file (required if replacing the existing file) - The MIME type and base64 encoded file string sent in the following format: `data:{MIME Type};base64,{Base64 Encoded String}`

##### Returns

Returns the file import object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid file import type).

#### Delete a file import

```
DEFINITION
DELETE http://apiserver/fileimports/:fileImportId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/fileimports/123", { type: DELETE });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a file import. It cannot be undone.

##### Arguments

* fileImportId (required) - The id of the file import to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the file import does not exist, this call returns an error.

#### List all file imports

```
DEFINITION
GET http://apiserver/fileimports

EXAMPLE REQUEST
$.get("http://localhost:49195/fileimports");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 10
    },
     "items": [
        {
            "id": "123",
            "accessorId": "1234",
            "accessorDescription": "Accessor Person - Internal User",
            "fileImportType": "DDCACCT",
            "fileImportTypeDescription": "Account Import",
            "batchProcessType": "N",
            "batchProcessTypeDescription": "New",
            "dataSource": "DDC",
            "dataSourceDescription": "DDC",
            "status": "N",
            "statusDescription": "New",
            "fileImportFieldMapping": null,
            "importId": null,
            "importStatus": null,
            "importStatusDescription": null,
            "batchCompany": "0",
            "batchNumber": null,
            "fileImportFile": {
                "fileImportFileId": "20",
                "fileImportId": "123",
                "fileName": "Filename.csv",
                "fileMimeType": "text/csv",
                "file": null
            }
        },
        {...},
    ]
}

```

Returns a list of all file imports.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* fileImportId (optional) - The fileImportId of the file import
* accessorId (optional) - The accessor id of the file import
* fileImportType (optional) - The fileImportType of the file import
* batchProcessType (optional) - The batchProcessType of the file import
* dataSource (optional) - The dataSource of the file import
* status (optional) - The status of the file import
* fieldMappingId (optional) - The fieldMappingId of the file import
* importId (optional) - The import Id of the import created by this file import
* importStatus (optional) - The import status of the import created by this file import
* batchCompany (optional) - The batch company of the file import
* batchNumber (optional) - The batch number of the file import
* fileName (optional) - The name of the file to be imported

##### Returns

A dictionary with an items property that contains an array of up to limit file imports, starting at index offset. Each entry in the array is a separate file import object. If no more file imports are available, the resulting array will be empty. This request should never return an error.

#### Validate a file import

```
DEFINITION
POST http://apiserver/fileimports/:fileImportId/validate

EXAMPLE REQUEST
$.post("http://localhost:49195/fileimports/161/validate", {});

EXAMPLE RESPONSE
{
    "isValid": true
}

```

Returns the validation result for the file import.

##### Returns

Returns a `200 OK` response on success. Returns an error if the file import cannot be found, has no associated file or field mappings, or is in a "New" status.