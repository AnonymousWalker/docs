# Two Step Verification

For authorized accounts it is possible to login in successfully but require Two Step Verification. An email is sent when logging in. However, a twoStepVerificationToken is returned so that it may be sent with following login attempts inorder to bypass Two Step Verification.

### Example

```
/*
* Two Step Verification process
*/

var username = "jdoe@domain.com";
var password = "somePassword123";


// Login
$.ajax({
    type: "POST",
    url: `https://apiserver/login`,
    beforeSend: jqXHR =>
        jqXHR.setRequestHeader("Authorization", `Basic ${btoa(`${username}:${password}`)}`),
    success: data => {
        if(data.status === "RequiresVerification") {
            // Request the user provide the code they were emailed
        }
    },
});

// Two Step Verification
$.ajax({
    type: "POST",
    data: {twoStepVerificationCode: "123456"},
    url: `https://apiserver/login`,
    beforeSend: jqXHR =>
        jqXHR.setRequestHeader("Authorization", `Basic ${btoa(`${username}:${password}`)}`),
    success: data => {
        // save JWT for future API requests
        sessionStorage.setItem("id_token", data.token);
        sessionStorage.setItem("environments", data.environments);
        if(data.twoStepVerificationToken) {
            localStorage.setItem("twoStepVerificationToken", data.twoStepVerificationToken);
        }
    }
});

// Subsequent Login
$.ajax({
    data: {twoStepVerificationToken: localStorage.getItem("twoStepVerificationToken")},
    type: "POST",
    url: `https://apiserver/login`,
    beforeSend: jqXHR =>
        jqXHR.setRequestHeader("Authorization", `Basic ${btoa(`${username}:${password}`)}`),
    success: data => {
        if(data.status === "RequiresVerification") {
            // Request the user provide the code they were emailed
        }
    },
});



```