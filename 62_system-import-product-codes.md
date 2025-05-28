# System Import Product Codes

#### Retrieve a system import product code

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/codes/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "newCodeType": "ITEMCHAR",
    "newCodeValue": "GLCLASS 1",
    "oldCodeType": null,
    "oldCodeValue": null,
    "isActive": true
}

```

Retrieves the details of an existing system import product code. You need only supply the id.

##### Arguments

* id (required) - The id of the system import product code to be retrieved.

#### Update a system import product code

```
DEFINITION
POST http://apiserver/systemimports/:importId/products/:productId/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/systemimports/10000047/products/40812571/codes/9", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "9",
    "newCodeType": "ITEMCHAR",
    "newCodeValue": "GLCLASS 1",
    "oldCodeType": null,
    "oldCodeValue": null,
    "isActive": false
}


```

Updates the specified system import product code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* newCodeType (optional) - the new code type to update the product code with
* newCodeValue (optional) - the new code value to update the product code with
* oldCodeType (optional) - the old code type to update the product code with
* oldCodeValue (optional) - the old code value to update the product code with
* isActive (optional) - is the product code active

##### Returns

Returns the system import product code object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete a system import product code

```
DEFINITION
DELETE http://apiserver/systemimports/:importId/products/:productId/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/systemimports/10000047/products/40812571/codes/9", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a system import product code. It cannot be undone.

##### Arguments

* id (required) - The id of the system import product code to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the system import product code does not exist, this call returns an error.

#### List all system import product codes

```
DEFINITION
GET http://apiserver/systemimports/:importId/products/:productId/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/systemimports/10000047/products/40812571/codes");

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
            "newCodeType": "ITEMCHAR",
            "newCodeValue": "GLCLASS 1",
            "oldCodeType": null,
            "oldCodeValue": null,
            "isActive": true
        },
        {...},
    ]
}

```

Returns a list of all system import product codes.

##### Returns

A dictionary with an items property that contains an array of up to limit system import product codes, starting at index offset. Each entry in the array is a separate system import product code object. If no more system import product codes are available, the resulting array will be empty. This request should never return an error.