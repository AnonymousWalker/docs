# Authorization

All requests must be made with a valid JWT (JSON Web Token) which can created through the [login](#login) resource. The login resource requires Basic authentication over HTTPS. All other requests should include the Authorization header with the Bearer token.

Once a valid token has been created, a StudioEnterprise [session](#sessions) must be created.

### Example

```
/*
* Create an Authorization token
*/
function createBasicAuth(user, pass) {
    var token = user + ":" + pass;
    var hash = btoa(token);
    return "Basic " + hash;
}
var username = "domain\jdoe";
var password = "somePassword123";

$.ajax({
    type: "POST",
    url: "https://apiserver/login",
    beforeSend: function(xhr) {
        xhr.setRequestHeader("Authorization", createBasicAuth(username, password));
        xhr.setRequestHeader("Content-Type", "application/json");
    },
    success: function(data) {
        // save JWT for future API requests
        sessionStorage.setItem("id_token", data.token);
        sessionStorage.setItem("environments", data.environments);
    },
    fail: function(error) {
        // Possible Errors include RequiresVerification, PasswordExpired, or Unauthorized
        alert(error);
    }
});

/*
* All future API requests will require the Authorization token.
* Configure jQuery to include the token.
*/
$.ajaxSetup({
    'beforeSend': function(xhr) {
        if (sessionStorage.getItem("id_token")) {
            xhr.setRequestHeader("Authorization",
                'Bearer ' + sessionStorage.getItem("id_token"));
            xhr.setRequestHeader("Content-Type", "application/json");
        }
    }
});

/*
* Create a StudioEnterprise session
*/
$.post("https://apiserver/sessions", {
    "environment": "USPROD"
});

/*
* Query accounts
*/
$.get("https://apiserver/accounts?lastName=Smith&addressPostalCode=75080");


```