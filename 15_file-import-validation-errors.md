# File Import Validation Errors

#### Retrieve a file import validation error

```
DEFINITION
GET http://apiserver/fileimports/:fileImportId/validationerrors/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/fileimports/1234/validationerrors/123");

EXAMPLE RESPONSE
{
    "id": "123",
    "fileImportId": "1234",
    "rowNumber": 1,
    "fieldMappingPath": "transaction.amount",
    "fileColumnName": "TransactionAmount",
    "fileColumnValue": "5 dollars",
    "errorText": "This column can only contain numbers."
}

```

Retrieves the details of an existing file import validation error. You need only supply the id.

##### Arguments

* id (required) - The id of the file import validation error to be retrieved.

##### Returns

Returns a file import validation error object if a valid id was provided.

#### List all file import validation errors

```
DEFINITION
GET http://apiserver/fileimports/:fileImportId/validationerrors

EXAMPLE REQUEST
$.get("http://localhost:49195/fileimports/1234/validationerrors");

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
            "fileImportId": "1234",
            "rowNumber": 1,
            "fieldMappingPath": "transaction.amount",
            "fileColumnName": "TransactionAmount",
            "fileColumnValue": "5 dollars",
            "errorText": "This column can only contain numbers."
        },
        {...},
    ]
}

```

Returns a list of all file import validation errors. You need only supply the fileImportId.

May be sorted by providing column criteria. Please see the [Paged Response](#paged-response) section above for more details about sorting.

##### Returns

A dictionary with an items property that contains an array of up to limit file import validation errors, starting at index offset. Each entry in the array is a separate file import validation error object. If no more file import validation errors are available, the resulting array will be empty. This request should never return an error.