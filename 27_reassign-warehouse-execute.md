# Reassign Warehouse Execute

#### Create a reassign warehouse execute

```
DEFINITION
POST http://apiserver/reassignwarehouses/execute

EXAMPLE REQUEST
$.post("http://localhost:49195/reassignwarehouses/execute", {
    "product": "CD1004",
    "currentWarehouse": "10",
    "newWarehouse": "10"
});

EXAMPLE RESPONSE
{
    "id": "1000000009",
    "runDate": "2015-09-15T01:31:28 PM",
    "product": "CD1004",
    "currentWarehouse": "10",
    "newWarehouse": "10"
}

```

Executes the reassign warehouse process.

##### Arguments

* product (required) - the product code to reassign warehouses for
* currentWarehouse (required) - the current warehouse of the selected product code
* newWarehouse (required) - the new warehouse to reassign to

##### Returns

Returns a reassign warehouse run object if the call succeeded. Returns an error if any execute parameters are invalid.