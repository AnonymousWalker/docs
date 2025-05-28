# NCOA Import

#### Run NCOA Import

```
DEFINITION
POST http://apiserver/ncoa/import

EXAMPLE REQUEST
$.post("http://localhost:49195/ncoa/import");

EXAMPLE RESPONSE
204 No Content

```

Runs the NCOA Import process.

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.