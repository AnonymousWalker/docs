# Decline Rules

#### Create a decline rule

```
DEFINITION
POST http://apiserver/declinerules

EXAMPLE REQUEST
$.post("http://localhost:49195/declinerules", {
    "company": "1",
    "numberOfDeclines": 3,
    "job": "100",
    "cancelRecurring": false,
    "isActive": true
});

EXAMPLE RESPONSE
204 No Content

```

Creates a new decline rule.

##### Arguments

* company (required) - The company for the decline rule
* numberOfDeclines (required) - Number of declines needed for this rule to execute
* job (required) - The job for the decline rule
* cancelRecurring (optional) - If the recurring should be cancelled when the rule applies
* newCategory (optional) - A new category to stamp on the recurring when the rule applies
* isActive (optional) - If the rule is active

##### Returns

Returns a 204 No Content HTTP status code if the rule was added successfully. If any invalid values are provided, this call will return an error.

#### Retrieve a decline rule

```
DEFINITION
GET http://apiserver/declinerules/:ruleId

EXAMPLE REQUEST
$.get("http://localhost:49195/declinerules/18");

EXAMPLE RESPONSE
{
    "id": "18",
    "company": "1",
    "companyDescription": "US 1",
    "numberOfDeclines": 3,
    "job": "100",
    "jobDescription": "Mailing List",
    "cancelRecurring": false,
    "newCategory": null,
    "newCategoryDescription": null,
    "isActive": true
}

```

Retrieves the details of an existing decline rule. You need only supply the id.

##### Arguments

* ruleId (required) - The id of the decline rule to be retrieved.

#### Update a decline rule

```
DEFINITION
POST http://apiserver/declinerules/:ruleId

EXAMPLE REQUEST
$.post("http://localhost:49195/declinerules/18", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "18",
    "company": "1",
    "companyDescription": "US 1",
    "numberOfDeclines": 3,
    "job": "100",
    "jobDescription": "Mailing List",
    "cancelRecurring": false,
    "newCategory": null,
    "newCategoryDescription": null,
    "isActive": false
}

```

Updates the specified decline rule by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* company (optional) - The company for the decline rule
* numberOfDeclines (optional) - Number of declines needed for this rule to execute
* job (optional) - The job for the decline rule
* cancelRecurring (optional) - If the recurring should be cancelled when the rule applies
* newCategory (optional) - A new category to stamp on the recurring when the rule applies
* isActive (optional) - If the rule is active

##### Returns

Returns the decline rule object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a decline rule

```
DEFINITION
DELETE http://apiserver/declinerules/:ruleId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/declinerules/18", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a decline rule. It cannot be undone.

##### Arguments

* ruleId (required) - The id of the decline rule to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the decline rule does not exist, this call returns an error.

#### List all decline rules

```
DEFINITION
GET http://apiserver/declinerules

EXAMPLE REQUEST
$.get("http://localhost:49195/declinerules?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "18",
            "company": "1",
            "companyDescription": "US 1",
            "numberOfDeclines": 3,
            "job": "100",
            "jobDescription": "Mailing List",
            "cancelRecurring": false,
            "newCategory": null,
            "newCategoryDescription": null,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all decline rule.

##### Arguments

* company (optional) - The company for the decline rule
* job (optional) - The job for the decline rule
* isActive (optional) - If the rule is active

##### Returns

A dictionary with an items property that contains an array of up to limit decline rule, starting at index offset. Each entry in the array is a separate decline rule object. If no more decline rule are available, the resulting array will be empty. This request should never return an error.