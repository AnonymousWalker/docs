# DACTA Execute

#### Run DACTA Execute

```
DEFINITION
POST http://apiserver/dacta/execute

EXAMPLE REQUEST
$.post("http://localhost:49195/dacta/execute");

EXAMPLE RESPONSE
204 No Content

```

Runs the DACTA Execute process.

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.