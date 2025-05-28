# StudioOnline

#### StudioOnline Authenticate

```
DEFINITION
POST http://apiserver/studioonlineauthenticate

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineauthenticate", {
    "store": 19,
    "emailAddress": "john.doe@donordirect.com",
    "password": "Secur3Passw0rd",
    "guestToken": "0787c04d-d84d-4129-b3d8-ff713eeefb18",
    "includeActiveSession": true
});

EXAMPLE RESPONSE
{
    "token": "0787c04d-d84d-4129-b3d8-ff713eeefb18",
    "userSession": "0243438b-4423-4cc3-a046-2255eb6d816b"
}

```

Verifies that the email and password are valid StudioOnline account credentials.

##### Arguments

* store (required) - The StudioOnline store Id for which to authenticate.
* emailAddress - The email address to use to verify a StudioOnline account.
* password - The password to use to verify a StudioOnline account.
* guestToken - The user token currently stored in the user's session information.
* includeActiveSession - If using this authentication request for single-sign on, pass true. This will return a session id named `userSession` as well as the user token. It will also call into the ASO environment associated with the given store and mark this user as logged in with the user/session id combination.

##### Returns

Returns the user token associated with the StudioOnline account if successful, and the active user session id `userSession` if the includeActiveSession flag was passed. Returns a 403 Forbidden if an invalid email address or password is provided.

#### StudioOnline Change Password

```
DEFINITION
POST http://apiserver/studioonlinechangepassword

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinechangepassword", {
    "userToken": "0787c04d-d84d-4129-b3d8-ff713eeefb18"
    "currentPassword": "Secur3Passw0rd",
    "newPassword": "Secur3P4ssw0rd",
});

EXAMPLE RESPONSE
204 NoContent

```

Changes an existing password associated with a StudioOnline account.

##### Arguments

* userToken - The user token associated with with the StudioOnline account.
* currentPassword - The current password associated with the StudioOnline account.
* newPassword - The new password to update the StudioOnline account with.

##### Returns

Returns a 204 NoContent if the update succeeded. Returns an error if any of the arguments are invalid.

#### StudioOnline Contact Us Request

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/contactus

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/aa28cf39-54d7-4373-8549-b686951632a6/contactus", {
    "store": "19",
    "summary": "Prayer request for my family.",
    "comment": "I would like to request prayers for my family in this difficult time."
});

EXAMPLE RESPONSE
204 NoContent

```

Accepts a StudioOnline Contact Us request and creates an account communication, then attempts to merge duplicate accounts if necessary.

##### Arguments

* store (optional) - The StudioOnline store Id of the contact record to create (used to default the sourceCode). If sourceCode is provided, store is not required.
* sourceCode (optional) - The source code to use for the account communication. Will use the ASO default source code if not provided.
* summary (optional) - Used for the short comment in the account communication if provided.
* comment - Used as the long comment for the account communication.
* alternativeAccountNumber (optional) - Only needed if the account communication should be added to an account other than the logged in user.

#### StudioOnline Forgot Password

```
DEFINITION
POST http://apiserver/studioonlineforgotpassword

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineforgotpassword", {
    "store": "19",
    "emailAddress": "john.doe@donordirect.com"
});

EXAMPLE RESPONSE
204 NoContent

```

If the email address exists in the system, sends a password reset link email to that email address.

##### Arguments

* store (required) - The StudioOnline store id of the forgotten password account.
* emailAddress (required) - The email address associated with the StudioOnline account.

##### Returns

Returns a 204 NoContent. The email will only be sent if the email address exists in the system.

#### StudioOnline Logout

```
DEFINITION
POST http://apiserver/studioonlinelogout

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinelogout", {
    "userId": "0787c04d-d84d-4129-b3d8-ff713eeefb18",
    "userSession": "6778f569-5917-4972-a604-ebb4ee4aa30e",
    "store": "19"
});

EXAMPLE RESPONSE
204 NoContent

```

Marks the user with the provided user id and session id as logged out.

##### Arguments

* userId (required) - The user id to mark as logged out.
* userSession (required) - The active session id to mark as logged out.
* store (required) - The StudioOnline store id for which to logout of.

##### Returns

Returns a 204 NoContent.

#### StudioOnline Get Pledge Statement Session

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/pledgestatementsessions

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/0787c04d-d84d-4129-b3d8-ff713eeefb18/pledgestatementsessions", {
    "storeId": 19,
    "sessionId": "6778f569-5917-4972-a604-ebb4ee4aa30e",
    "pledgeStatementId": "478965",
    "accountNumber": "44525"
});

EXAMPLE RESPONSE
{
    "userId": "0787c04d-d84d-4129-b3d8-ff713eeefb18",
    "sessionId": "8854796f-3244-9956-f1f4-ybb5457ar668"
}

```

Gets a Pledge Statement session if one exists or creates a session if one doesn't exist.

##### Arguments

* storeId (required) - The StudioOnline store id for the new session.
* sessionId (required) - The active session id for the given user.
* pledgeStatementId (required) - The id of a pledge statement. The combination of pledgeStatementId and accountNumber are used to get the pledges that will be added to the cart.
* accountNumber (required) - An account number on the pledge statement. The combination of pledgeStatementId and accountNumber are used to get the pledges that will be added to the cart.

##### Returns

If the call is successful, returns a userId and sessionId. The userId may be different from the one provided.

#### StudioOnline Reset Password

```
DEFINITION
POST http://apiserver/studioonlineresetpassword

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineresetpassword", {
    "store": "19",
    "emailAddress": "john.doe@donordirect.com",
    "resetToken": "AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAewwMAs+sJkqAU0LwPUGBEQAAAAACAAAAAAAQZgAAAAEAACAAAADonAgEPiiXHpGlSbVhdBd5z3YYIf9NKGYrDU55F3CQ3QAAAAAOgAAAAAIAACAAAACY25CVaiawFSbO5L7/uPIlWu5E+O94KkTs9nQE7sFLhEAAAAC6Or7gkGRgz7XzPGG7zxocigD/E7IkD7x5cw10GsI0hUG6A0Zitv0R+o6Z8wkDAzKQloEbAXrRHQbVHOKa7ZDUQAAAAKzA8hvZcL9iyCPxn0UFk5whZ0LaztOd3dLoKD4dBiLcyolysfUw4asef85oj3Br0TaDJ84EyloMJgCvsE3K+cg="
    "newPassword": "Secur3Passw0rd2",
});

EXAMPLE RESPONSE
204 NoContent

```

Resets a StudioOnline account password if it has been forgotten.

##### Arguments

* store (required) - The StudioOnline store Id for which to reset the password.
* emailAddress - The email address associated with the StudioOnline account.
* password - The generated reset token used to reset the password associated with the StudioOnline account.
* newPassword - The new password to update the StudioOnline account with.

##### Returns

Returns a 204 NoContent if succeeded. Returns an error if any of the arguments provided are invalid.

#### StudioOnline Verify User Session

```
DEFINITION
POST http://apiserver/studioonlineverifyusersession

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineverifyusersession", {
    "userId": "0787c04d-d84d-4129-b3d8-ff713eeefb18",
    "userSession": "6778f569-5917-4972-a604-ebb4ee4aa30e",
    "store": 19
});

EXAMPLE RESPONSE
{
    "isLoggedIn": true,
    "isInPledgeStatementSession": false
}

```

Verifies that the user id and session id combination belong to a valid and active StudioOnline session.

##### Arguments

* userId (required) - The user id to verify the current session for.
* userSession (required) - The active session id to verify.
* store (required) - The StudioOnline store id for which to verify in.

##### Returns

If call is successful, returns whether or not the provided user/session combination is logged in and active. If logged in, this call will also update the session expiration date & time, making this session active for x minutes, where x is the session timeout configured in that StudioOnline configuration.