# Wealth Engine Imports Run

```
DEFINITION
POST http://apiserver/wealthengineimports/run

EXAMPLE REQUEST
$.post("http://localhost:49195/wealthengineimports/run", {
    "job": "540",
    "segment": "1"
});

EXAMPLE RESPONSE
204 No Content

```

Runs the wealth engine import process.

##### Arguments

* job (required) - the segmentation job to run wealth engine import process for
* segment (optional) - the segment number to run wealth engine import process for. **If not provided, all segments will be used.**

##### Returns

Returns a 204 No Content HTTP status code if the process executed successfully. If any exceptions occur, this call will return an error.