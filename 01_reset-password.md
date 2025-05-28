# Reset Password

For authorized accounts it is possible to change the password before logging in using a resetPasswordToken.

### Example

```
/*
* Change the password with a reset token
*/

var username = "jdoe@domain.com";
var password = "someNewPassword123";

$.ajax({
    type: "POST",
    url: `https://apiserver/resetPassword?resetPasswordToken=${resetPasswordToken}`,
    beforeSend: jqXHR =>
        jqXHR.setRequestHeader("Authorization", `Basic ${btoa(`${username}:${password}`)}`),
    success: () => alert("Password Changed!"),
});


```