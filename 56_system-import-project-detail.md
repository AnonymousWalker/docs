# System Import Project Detail

#### Retrieve a system import project detail

```
DEFINITION
GET http://apiserver/systemimports/:importId/projects/:id/detail

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/projects/40812571/detail");

EXAMPLE RESPONSE
{
    "type": "MS",
    "description": "10 Days Project",
    "title": "Mr.",
    "firstName": "Steve",
    "lastName": "Johnson",
    "defaultDepartment": "20",
    "isActiveForDonor": true,
    "isActiveForAccounting": true,
    "emailAddress": "steve.johnson@email.com",
    "accountingSegment": "SEGMENT1",
    "company": "BLUE",
    "accountNumber": "16230",
    "balanceType": "T",
    "isDeductible": true,
    "isUseInShoppingCart": false,
    "isSecure": false
}

```

Retrieves the details of an existing system import project detail. You need only supply the id.

##### Arguments

* id (required) - The id of the system import project detail to be retrieved.

#### Update a system import project detail

```
DEFINITION
POST http://apiserver/systemimports/:importId/projects/:id/detail

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/projects/40812571/detail", {
    "firstName": "Steven"
});

EXAMPLE RESPONSE
{
    "type": "MS",
    "description": "10 Days Project",
    "title": "Mr.",
    "firstName": "Steven",
    "lastName": "Johnson",
    "defaultDepartment": "20",
    "isActiveForDonor": true,
    "isActiveForAccounting": true,
    "emailAddress": "steve.johnson@email.com",
    "accountingSegment": "SEGMENT1",
    "company": "BLUE",
    "accountNumber": "16230",
    "balanceType": "T",
    "isDeductible": true,
    "isUseInShoppingCart": false,
    "isSecure": false
}

```

Updates the specified system import project detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - the project type to update the project with
* description (optional) - the description to update the project with
* title (optional) - the title to update the project with
* firstName (optional) - the first name to update the project with
* lastName (optional) - the last name to update the project with
* defaultDepartment (optional) - the default department to update the project with
* isActiveForDonor (optional) - is the project active for donors
* isActiveForAccounting (optional) - is the project active for accounting
* emailAddress (optional) - the email address to update the project with
* accountingSegment (optional) - the accounting segment to update the project with
* company (optional) - the company code to update the project with
* accountNumber (optional) - the account number to update the project with
* balanceType (optional) - the balance type to update the project with
* isDeductible (optional) - is the project deductible
* isUseInShoppingCart (optional) - is the project used in StudioOnline
* isSecure (optional) - indicates if this is a secure project for Advanced Studio Online

##### Returns

Returns the system import project detail object if the update succeeded. Returns an error if update parameters are invalid.