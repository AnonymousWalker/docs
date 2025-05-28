# System Import Pledge Substitutions

#### Retrieve a system import pledge substitution

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledgesubstitutions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledgesubstitutions/40812571");

EXAMPLE RESPONSE
{
    "id": "40812571",
    "status": "Y",
    "oldPledgeCode": "OLDPLDGCD",
    "newPledgeCode": "NEWPLDGCD",
    "reasonCode": "ACTIVE",
    "letterCode": "LTRCODE",
    "paragraphCode": "PARARGRAPH"
}

```

Retrieves the details of an existing system import pledge substitution. You need only supply the id.

##### Arguments

* id (required) - The id of the system import pledge substitution to be retrieved.

#### Update a system import pledge substitution

```
DEFINITION
POST http://apiserver/systemimports/:systemImportId/pledgesubstitutions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/pledgesubstitutions/40812571", {
    "reasonCode": "UPDATE"
});

EXAMPLE RESPONSE
{
    "id": "40812571",
    "status": "Y",
    "oldPledgeCode": "OLDPLDGCD",
    "newPledgeCode": "NEWPLDGCD",
    "reasonCode": "UPDATE",
    "letterCode": "LTRCODE",
    "paragraphCode": "PARARGRAPH"
}

```

Updates the specified system import pledge substitution by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* status (optional) - the status to update the pledge substitution with
* reasonCode (optional) - the reason code to update the pledge substitution with
* letterCode (optional) - the letter code to update the pledge substitution with
* paragraphCode (optional) - the paragraph code to update the pledge substitution with

##### Returns

Returns the system import pledge substitution object if the update succeeded. Returns an error if update parameters are invalid.

#### List all system import pledge substitutions

```
DEFINITION
GET http://apiserver/systemimports/:importId/pledgesubstitutions

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/pledgesubstitutions?status=Y");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "40812571",
            "status": "Y",
            "oldPledgeCode": "OLDPLDGCD",
            "newPledgeCode": "NEWPLDGCD",
            "reasonCode": "ACTIVE",
            "letterCode": "LTRCODE",
            "paragraphCode": "PARARGRAPH"
        },
        {...},
    ]
}

```

Returns a list of all system import pledge substitutions.

##### Arguments

* status (optional) - the status to filter the returned pledge substitution results on
* oldPledgeCode (optional) - the old pledge code to filter the returned pledge substitution results on
* newPledgeCode (optional) - the new pledge code to filter the returned pledge substitution results on
* reasonCode (optional) - the reason code to filter the returned pledge substitution results on
* letterCode (optional) - the letter code to filter the returned pledge substitution results on
* paragraphCode (optional) - the paragraph code to filter the returned pledge substitution results on

##### Returns

A dictionary with an items property that contains an array of up to limit system import pledge substitutions, starting at index offset. Each entry in the array is a separate system import pledge substitution object. If no more system import pledge substitutions are available, the resulting array will be empty. This request should never return an error.