# Automatic AR Adjustment Run

```
DEFINITION
POST http://apiserver/:id/run

EXAMPLE REQUEST
$.post("http://localhost:49195/17/run", {
    "asOfDate": "2015-09-17"
});

EXAMPLE RESPONSE
204 No Content

```

Runs the automatic AR adjustment job.

##### Arguments

* asOfDate (required) - The as-of date to use for running the AR adjustment job

##### Returns

Returns a `204 No Content` response on success. If any exceptions occur or invalid data is provided, this call will return an error.