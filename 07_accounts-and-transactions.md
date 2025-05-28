# Accounts and Transactions

### Accounts

#### Create an individual account

```
DEFINITION
POST http://apiserver/accounts

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts", {
    "type": "I",
    "firstName": "Henry",
    "lastName": "Winkler",
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "line1": "8212 E Juneau Ave",
        "postalCode": "53202",
        "country": "USA"
    },
    "source": "AD1D2234A",
    "codes": [
        {
            "type": "MAILCODE",
            "value": "0"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1483320",
    "type": "I",
    "title": null,
    "firstName": "Henry",
    "middleName": null,
    "lastName": "Winkler",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Henry",
    "gender": "U",
    "birthdate": null,
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "id": "4388112",
        "line1": "8212 E Juneau Ave",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Milwaukee",
        "state": "WI",
        "postalCode": "53202",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "validatedDate": "2019-07-22",
        "deliveryPoint": 12,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}

```

Creates a new individual account object.

##### Arguments

* type (required) - The account type must be specified as `I` when creating an individual account.
* accountAddressDefaults (optional) - The default values for the primary address.
* address (required) - An address object for the primary address of the account. Only the `country` field of the primary address is required.
* source (required) - The source code of the account. Must be a defined source code.
* codes (optional) - A dictionary of required and optional code types and valid values. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.
* mediaOutlet (optional) - The media outlet id of the account. Must be a defined media outlet id.
* phone (optional) - A phone object for the primary phone of the account. If specified, the type and phoneNumber fields are required.

##### Returns

Returns an account object of type `I` if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a valid address or a required code and value).

#### Create a family account

```
DEFINITION
POST http://apiserver/accounts

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts", {
    "type": "F",
    "spouses": [
        { "firstName": "Avery", "lastName": "Shumway", "codes": [ { "type": "MAILCODE", "value": "0" } ] },
        { "firstName": "Reese", "lastName": "Shumway", "codes": [ { "type": "MAILCODE", "value": "0" } ] }
    ],
    "dependents": [
        { "firstName": "Pat", "codes": [ { "type": "MAILCODE", "value": "0" } ] },
        { "firstName": "Alexis", "codes": [ { "type": "MAILCODE", "value": "0" } ] }
    ],
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "line1": "2800 University Ave NE",
        "postalCode": "55413",
        "country": "USA"
    },
    "source": "AD1D2234A",
    "codes": [
        {
            "type": "MAILCODE",
            "value": "0"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1483306",
    "type": "F",
    "name": "Avery and Reese Shumway",
    "isFamilyConsolidated": true,
    "status": "A",
    "salutation": "Avery and Reese ",
    "spouses": [
        {
            "id": "1483307",
            "type": "SP",
            "title": null,
            "firstName": "Avery",
            "middleName": null,
            "lastName": "Shumway",
            "suffix": null,
            "status": "A",
            "email": null,
            "salutation": "Avery",
            "gender": "U",
            "birthdate": null
        },
        {
            "id": "1483308",
            "type": "SP",
            "title": null,
            "firstName": "Reese",
            "middleName": null,
            "lastName": "Shumway",
            "suffix": null,
            "status": "A",
            "email": null,
            "salutation": "Reese",
            "gender": "U",
            "birthdate": null
        }
    ],
    "dependents": ["1483309", "1483310"],
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "id": "4394024",
        "line1": "2800 University Ave NE",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Minneapolis",
        "state": "MN",
        "postalCode": "55413",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "validatedDate": null,
        "deliveryPoint": null,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}

```

Creates a new family account object.

##### Arguments

* type (required) : The account type must be specified as `F` when creating a family account.
* accountAddressDefaults (optional) - The default values for the primary address for the new family account.
* address (required) : An address object for the primary address of the account. Only the `country` field of the primary address is required.
* source (required) : The source code of the account. Must be a defined source code.
* codes (optional) : A dictionary of required and optional code types and valid values. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* name (optional) : The organization name of the account. If not specified, a name will be generated based on spouse name(s).
* isFamilyConsolidated (optional) : Whether or not transactions on spouse accounts roll up to the family account. If not specified, will default to true.
* status (optional) : The status of the account.
* salutation (optional) : A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* spouses (required) : An array of at least 1 and no more than 2 spouse account objects to be created. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* dependents (optional) : An array of dependent account objects to be created. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=DEP` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* mediaOutlet (optional) : The media outlet id of the account. Must be a defined media outlet id.
* phone (optional) : A phone object for the primary phone of the account. If specified, the type and phoneNumber fields are required.

##### Returns

Returns an account object of type `F` if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a valid address or a required code and value).

#### Create a spouse account

```
DEFINITION
POST http://apiserver/accounts

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts", {
    "type": "SP",
    "family": "1488709",
    "firstName": "Connor",
    "lastName": "Baker",
    "codes": [ { "type": "MAILCODE", "value": "0" } ],
});

EXAMPLE RESPONSE
{
    "id": "1488711",
    "type": "SP",
    "family": "1488709",
    "familyName": "Trudy and Connor Baker",
    "title": null,
    "firstName": "Connor",
    "middleName": null,
    "lastName": "Baker",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Connor",
    "gender": "U",
    "birthdate": null,
    "accountAddressDefaults": null,
    "address": {
        "id": "4394024",
        "line1": "2800 University Ave NE",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Minneapolis",
        "state": "MN",
        "postalCode": "55413",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "validatedDate": "2019-07-22",
        "deliveryPoint": 28,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}

```

Creates a new spouse account object.

##### Arguments

* type (required) - The account type must be specified as `SP` when creating a spouse account.
* family (required) - The account number of the family under which the spouse should be created. If the specified family account already has two spouses, an error will result.
* codes (optional) - A dictionary of required and optional code types and valid values. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.

##### Returns

Returns an account object of type `SP` if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a valid family id or a required code and value).

#### Create a dependent account

```
DEFINITION
POST http://apiserver/accounts

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts", {
    "type": "DP",
    "family": "1488709",
    "firstName": "Ruth",
    "lastName": "Baker",
    "codes": [ { "type": "MAILCODE", "value": "0" } ],
});

EXAMPLE RESPONSE
{
    "id": "1488712",
    "type": "DP",
    "family": "1488709",
    "familyName": "Trudy and Connor Baker",
    "title": null,
    "firstName": "Ruth",
    "middleName": null,
    "lastName": "Baker",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Ruth",
    "gender": "U",
    "birthdate": null,
    "address": {
        "id": "4394024",
        "line1": "2800 University Ave NE",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Minneapolis",
        "state": "MN",
        "postalCode": "55413",
        "country": "USA",
        "isPoBox": false,
        "isPrimary": true,
        "isActive": true,
        "validatedDate": "2019-07-22",
        "deliveryPoint": 28,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}

```

Creates a new dependent account object.

##### Arguments

* type (required) - The account type must be specified as `DP` when creating a dependent account.
* family (required) - The account number of the family under which the dependent should be created.
* codes (optional) - A dictionary of required and optional code types and valid values. Any codes types in the collections `/codetypes?requiredForAccountType=ALL`, `/codetypes?requiredForAccountType=DEP`, and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.

##### Returns

Returns an account object of type `DP` if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a valid family id or a required code and value).

#### Create an organization account

```
DEFINITION
POST http://apiserver/accounts

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts", {
    "type": "O",
    "name": "Big City Lights",
    "address": {
        "line1": "25 W 32ND ST",
        "postalCode": "10001",
        "country": "USA"
    },
    "source": "AD1D2234A",
    "codes": [
        {
            "type": "MAILCODE",
            "value": "0"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1483490",
    "type": "O",
    "name": "Big City Lights",
    "status": "A",
    "email": null,
    "salutation": "Friends",
    "contacts": [],
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "id": "7249",
        "line1": "25 W 32ND ST",
        "postalCode": "10001",
        "country": "USA",
        "validatedDate": "2019-07-22",
        "deliveryPoint": 25,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}

```

Creates a new organization account object.

##### Arguments

* type (required) - The account type must be specified as `O` when creating an organization account.
* name (required) - The organization name of the account.
* address (required) - An address object for the primary address of the account. Only the `country` field of the primary address is required.
* source (required) - The source code of the account. Must be a defined source code.
* codes (optional) - A dictionary of required and optional code types and valid values. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=ORG` must be specified.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* contacts (optional) - An array of contact account objects to be created. Any codes types in the collection `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* mediaOutlet (optional) - The media outlet id of the account. Must be a defined media outlet id.
* phone (optional) - A phone object for the primary phone of the account. If specified, the type and phoneNumber fields are required.

##### Returns

Returns an account object of type `O` if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a valid address or a required code and value).

#### Create a contact account

```
DEFINITION
POST http://apiserver/accounts

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts", {
    "type": "CN",
    "organization": "1488713",
    "firstName": "Heber",
    "lastName": "Krel",
    "codes": [ { "type": "MAILCODE", "value": "0" } ],
});

EXAMPLE RESPONSE
{
    "id": "1488714",
    "type": "CN",
    "organization": "1488713",
    "organizationName": "Great Ministry",
    "title": null,
    "firstName": "Heber",
    "middleName": null,
    "lastName": "Krel",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Heber",
    "gender": "U",
    "birthdate": null,
    "contactType": null,
    "contactTypeDescription": null,
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "id": "7249",
        "line1": "25 W 32ND ST",
        "postalCode": "10001",
        "country": "USA",
        "validatedDate": "2019-07-22",
        "deliveryPoint": 25,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null,
    "noteShortComment": null,
    "noteLongComment": null
}

```

Creates a new contact account object.

##### Arguments

* type (required) - The account type must be specified as `CN` when creating a contact account.
* organization (required) - The account number of the organization under which the contact should be created.
* codes (optional) - A dictionary of required and optional code types and valid values. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.
* contactType (optional) - The contact type of the account. Must be a defined contact type.

##### Returns

Returns an account object of type `CN` if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a valid organization id or a required code and value).

#### Retrieve an account

```
DEFINITION
GET http://apiserver/accounts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483307");

EXAMPLE RESPONSE
{
    "id": "1483307",
    "type": "SP",
    "firstName": "Avery",
    "lastName": "Shumway",
    "family": "1483306",
    "familyName": "Avery and Reese Shumway",
    "inceptionDate": "2015-01-23",
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "id": "230515",
        "line1": "2800 University Ave NE",
        "postalCode": "55413",
        "country": "USA",
        "validatedDate": "2019-07-22",
        "deliveryPoint": 28,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null,
        "isSavedPaymentBillingAddress": false
    },
    "mediaOutlet": null,
    "mediaOutletDescription": null,
    "gender": "U",
    "source": "AD1D2234A",
    "sourceDescription": "New Donors",
    "status": "A",
    "arBalance": 10.55
}

```

Retrieves the details of an existing account. You need only supply the account id. Note: arBalance will only appear in the response if `includeArBalance` is true.

##### Arguments

* id (required) - The id of the account to retrieve.
* includeArBalance (optional) - Whether or not to include the account's AR balance in the response.
* getContactByFunctionalCategory (optional) - Whether or not a contact's email and phone number should be retrieved by the functional category saved with the contact. `false` is the default and the contact's email and phone number will be retrieved by the functional category of the signed in user. Only applies to getting accounts that are contacts (type="CN").

##### Returns

Returns an account object if a valid id was provided.
Note: This resource retrieves the preferred phone and email address by functional category based on the user's role. If no preferred phone or email address is available, the primary will be returned. If there is no primary, no email or phone address will be returned. The phone and email must be active and the email address must not be Opted-Out.

#### Update an individual account

```
DEFINITION
POST http://apiserver/accounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320", {
    "middleName": "Franklin",
    "gender": "M"
});

EXAMPLE RESPONSE
{
    "id": "1483320",
    "type": "I",
    "title": null,
    "firstName": "Henry",
    "middleName": "Franklin",
    "lastName": "Winkler",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Henry",
    "gender": "M",
    "birthdate": null,
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "id": "230528",
        "line1": "8212 E Juneau Ave",
        "postalCode": "53202",
        "country": "USA",
        "validatedDate": "2019-07-22",
        "deliveryPoint": 12,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}


```

Updates the specified account by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The account type can be any of `O`, `SP`, `DP`, and `CN`. If the new type is `SP` or `DP` the `family` argument must be specified. If the new type is `CN` the `organization` argument must be specified
* accountAddressDefaults (optional) - The default values for the primary address.
* family (optional) - The account number of the family to which the account (as it is changed to type `SP` or `DP`) should be joined. If the new type is `SP` and the specified family already has two spouses, an error will result. This argument is required if the new type is `SP` or `DP` and is otherwise ignored.
* organization (optional) - The account number of the organization to which the account (as it is changed to type `CN`) should be joined. This argument is required if the new type is `CN` and is otherwise ignored.
* codes (optional) - A dictionary of required and optional code types and valid values. If type is being changed, all required codes for the new type must be provided if they don't already exist on the account. If type is not being changed, this argument is ignored.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.
* address (optional) - An address object for the primary address of the account. Only the `country` field of the primary address is required.
* source (optional) - The source code of the account. Must be a defined source code.
* mediaOutlet (optional) - The media outlet id of the account. Must be a defined media outlet id.
* phone (optional) - A phone object for the primary phone of the account. If specified, the type and phoneNumber fields are required.
* isSalutationChanged (optional) - Only needs to be set to `false` if you would like the API to default the account primary salutation, if it has not been manually set.
* getContactByFunctionalCategory (optional) - Whether or not the a contact's email and phone number should be updated and returned in the response by the functional category saved with the contact. `false` is the default and the contact's email and phone number will be updated and returned in the response by the functional category of the signed in user. Only applies to updating accounts that are contacts (type="CN"). This field is not saved with the contact account.

##### Returns

Returns the account object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid title).
Note: This resource retrieves the preferred phone and email address by functional category based on the user's role. If no preferred phone or email address is available, the primary will be returned.

#### Update a family account

```
DEFINITION
POST http://apiserver/accounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483306", {
    "isFamilyConsolidated": false,
    "spouses": [
        {
            "id": "1483307",
            "accountAddressDefaults": {
                "isDefaultBilling": true,
                "isDefaultShipping": false
            }
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1483306",
    "type": "F",
    "name": "Avery and Reese Shumway",
    "isFamilyConsolidated": false,
    "status": "A",
    "salutation": "Avery and Reese Shumway",
    "spouses": [
        {
            "id": "1483307",
            "type": "SP",
            "title": null,
            "firstName": "Avery",
            "middleName": null,
            "lastName": "Shumway",
            "suffix": null,
            "status": "A",
            "email": null,
            "salutation": "Avery",
            "gender": "U",
            "birthdate": null,
            "accountAddressDefaults": {
                "isDefaultBilling": true,
                "isDefaultShipping": false
            }
        },
        {
            "id": "1483308",
            "type": "SP",
            "title": null,
            "firstName": "Reese",
            "middleName": null,
            "lastName": "Shumway",
            "suffix": null,
            "status": "A",
            "email": null,
            "salutation": "Reese",
            "gender": "U",
            "birthdate": null
        }
    ],
    "dependents": ["1483309", "1483310"],
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
    "address": {
        "id": "230515",
        "line1": "2800 University Ave NE",
        "postalCode": "55413",
        "country": "USA",
        "validatedDate": "2019-07-22",
        "deliveryPoint": 28,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}


```

Updates the specified account by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (ignored) - The account type cannot be changed on a family account.
* accountAddressDefaults (optional) - The default values for the primary address. These can be placed on the family account and on the spouses.
* name (optional) - The organization name of the account. If not specified, a name will be generated based on spouse name(s).
* isFamilyConsolidated (optional) - Whether or not transactions on spouse accounts roll up to the family account. If not specified, will default to true.
* status (optional) - The status of the account.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* spouses (optional) - An array of at least 1 and no more than 2 spouse account objects to be updated. Any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be specified.
* dependents (ignored) - The dependents array is read-only. Dependents can only be added to or removed from a family by updating each dependent account.
* address (optional) - An address object for the primary address of the account. Only the `country` field of the primary address is required.
* source (optional) - The source code of the account. Must be a defined source code.
* mediaOutlet (optional) - The media outlet id of the account. Must be a defined media outlet id.
* phone (optional) - A phone object for the primary phone of the account. If specified, the type and phoneNumber fields are required.
* isSalutationChanged (optional) - Only needs to be set to `false` if you would like the API to default the account primary salutation, if it has not been manually set. (This can be set in the spouses too.)
* isNameChanged (optional) - Only needs to be set to `false` if you would like the API to default the account family name, if it has not been manually set.

##### Returns

Returns the account object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid source).
Note: This resource retrieves the preferred phone and email address by functional category based on the user's role. If no preferred phone or email address is available, the primary will be returned.

#### Update a spouse account

```
DEFINITION
POST http://apiserver/accounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1488711", {
    "gender": "M"
});

EXAMPLE RESPONSE
{
    "id": "1488711",
    "type": "SP",
    "family": "1488709",
    "familyName": "Trudy and Connor Baker",
    "title": null,
    "firstName": "Connor",
    "middleName": null,
    "lastName": "Baker",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Connor",
    "gender": "M",
    "birthdate": null,
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
}


```

Updates the specified account by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The account type can only be changed to `I`. If type is being changed to `I` the `family` argument must be specified as null.
* accountAddressDefaults (optional) - The default values for the primary address.
* family (optional) - If the type is changing to `I` this argument must be specified as null. If type is not being changed, this argument is ignored.
* familyName (ignored) - The family name is read-only on a spouse account. It can only be updated on the family account.
* codes (optional) - A dictionary of required and optional code types and valid values. If the type is changing to `I`, any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be provided if they don't already exist on the account. If type is not being changed, this argument is ignored.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.
* isSalutationChanged (optional) - Only needs to be set to `false` if you would like the API to default the account primary salutation, if it has not been manually set.

##### Returns

Returns the account object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid title).
Note: This resource retrieves the preferred phone and email address by functional category based on the user's role. If no preferred phone or email address is available, the primary will be returned.

#### Update a dependent account

```
DEFINITION
POST http://apiserver/accounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1488712", {
    "gender": "F"
});

EXAMPLE RESPONSE
{
    "id": "1488712",
    "type": "DP",
    "family": "1488709",
    "familyName": "Trudy and Connor Baker",
    "title": null,
    "firstName": "Ruth",
    "middleName": null,
    "lastName": "Baker",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Ruth",
    "gender": "U",
    "birthdate": null,
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    }
}


```

Updates the specified account by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The account type can only be changed to `I`. If type is being changed to `I` the `family` argument must be specified as null.
* family (optional) - If the type is changing to `I` this argument must be specified as null. If type is not being changed, this argument is ignored.
* familyName (ignored) - The family name is read-only on a dependent account. It can only be updated on the family account.
* codes (optional) - A dictionary of required and optional code types and valid values. If the type is changing to `I`, any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be provided if they don't already exist on the account. If type is not being changed, this argument is ignored.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.
* isSalutationChanged (optional) - Only needs to be set to `false` if you would like the API to default the account primary salutation, if it has not been manually set.

##### Returns

Returns the account object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid title).
Note: This resource retrieves the preferred phone and email address by functional category based on the user's role. If no preferred phone or email address is available, the primary will be returned.

#### Update an organization account

```
DEFINITION
POST http://apiserver/accounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483490", {
    "salutation": "Our Friends"
});

EXAMPLE RESPONSE
{
    "id": "1483490",
    "type": "O",
    "name": "Big City Lights",
    "status": "A",
    "salutation": "Our Friends",
    "address": {
        "id": "7249",
        "line1": "25 W 32ND ST",
        "postalCode": "10001",
        "country": "USA",
        "validatedDate": "2019-07-22",
        "deliveryPoint": 25,
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    },
    "contacts": [],
    "source": "AD1D2234A",
    "mediaOutlet": null,
    "phone": null
}


```

Updates the specified account by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (ignored) - The account type cannot be changed on an organization account.
* name (optional) - The organization name of the account.
* status (optional) - The status of the account.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* address (optional) - An address object for the primary address of the account. Only the `country` field of the primary address is required.
* contacts (ignored) - The contacts array is read-only. Contacts can only be added to or removed from an organization by updating each contact account.
* source (optional) - The source code of the account. Must be a defined source code.
* mediaOutlet (optional) - The media outlet id of the account. Must be a defined media outlet id.
* phone (optional) - A phone object for the primary phone of the account. If specified, the type and phoneNumber fields are required.
* isSalutationChanged (optional) - Only needs to be set to `false` if you would like the API to default the account primary salutation, if it has not been manually set.

##### Returns

Returns the account object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid source).
Note: This resource retrieves the preferred phone and email address by functional category based on the user's role. If no preferred phone or email address is available, the primary will be returned.

#### Update a contact account

```
DEFINITION
POST http://apiserver/accounts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1488714", {
    "title": "Mr"
});

EXAMPLE RESPONSE
{
    "id": "1488714",
    "type": "CN",
    "organization": "1488713",
    "organizationName": "Great Ministry",
    "title": "Mr",
    "firstName": "Heber",
    "middleName": null,
    "lastName": "Krel",
    "suffix": null,
    "status": "A",
    "email": null,
    "salutation": "Heber",
    "gender": "U",
    "birthdate": null,
    "contactType": null,
    "contactTypeDescription": null,
    "noteShortComment": null,
    "noteLongComment": ,
    "accountAddressDefaults": {
        "isDefaultBilling": true,
        "isDefaultShipping": true
    },
}


```

Updates the specified account by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The account type can only be changed to `I`. If type is being changed to `I` the `organization` argument must be specified as null.
* organization (optional) - If the type is changing to `I` this argument must be specified as null. If type is not being changed, this argument is ignored.
* organizationName (ignored) - The organization name is read-only on a contact account. It can only be updated on the organization account.
* codes (optional) - A dictionary of required and optional code types and valid values. If the type is changing to `I`, any codes types in the collections `/codetypes?requiredForAccountType=ALL` and `/codetypes?requiredForAccountType=INDFAM` must be provided if they don't already exist on the account. If type is not being changed, this argument is ignored.
* title (optional) - The title of the account. If specified, must be a [valid title](#list-all-titles).
* firstName (optional) - The first name of the account.
* middleName (optional) - The middle name of the account.
* lastName (optional) - The last name of the account.
* suffix (optional) - The suffix of the account.
* status (optional) - The status of the account.
* email (optional) - An email object for the primary email of the account. If specified, the type and emailAddress fields are required.
* salutation (optional) - A salutation string for the primary salutation of the account. If not specified, a default salutation will be generated.
* gender (optional) - The gender of the account. If not specified will default to `U`. Other possible values are `M` and `F`.
* birthdate (optional) - The birthdate of the account.
* contactType (optional) - The contact type of the account. Must be a defined contact type.
* isSalutationChanged (optional) - Only needs to be set to `false` if you would like the API to default the account primary salutation, if it has not been manually set.

##### Returns

Returns the account object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid title).
Note: This resource retrieves the preferred phone and email address by functional category based on the user's role. If no preferred phone or email address is available, the primary will be returned.

#### List all accounts

```
DEFINITION
GET http://apiserver/accounts

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts?type=I,SP");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1483320",
            "type": "I",
            "title": null,
            "firstName": "Henry",
            "middleName": null,
            "lastName": "Winkler",
            "suffix": null,
            "accountAddressDefaults": null
            "address": {
                "id": "230528",
                "line1": "8212 E Juneau Ave",
                "postalCode": "53202",
                "country": "USA",
                "validatedDate": "2019-07-22",
                "userVerifiedAccessorId": null,
                "userVerifiedAccessorIdDescription": null
            },
            "salutation": "Henry",
            "mediaOutlet": null,
            "gender": "U",
            "source": "AD1D2234A",
            "status": "A"
        },
        {
            "id": "1483320",
            "type": "SP",
            "title": null,
            "firstName": "Timothy",
            "middleName": null,
            "lastName": "Green",
            "suffix": null,
            "address": {
                "id": "232348",
                "line1": "1212 Sunset Dr",
                "postalCode": "75025",
                "country": "USA",
                "validatedDate": "2019-07-23",
                "userVerifiedAccessorId": null,
                "userVerifiedAccessorIdDescription": null
            },
            "salutation": "Timothy",
            "mediaOutlet": null,
            "gender": "U",
            "source": "AD1D2234A",
            "status": "A"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all accounts.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting. However use the following syntax for the column criteria parameter if sending Advanced Find Criteria:
columnCriteria=[{"column":"TransType","sortOrder":"D"}]

##### Arguments

* id () - Filter list by partial match in account number
* type () - Filter list by list match in account type. Provide a comma separated list off account types. Possible values are `I` for individual accounts not in a family, `F` for family accounts, `O` for organization accounts, `CN` for contacts, `SP` for spouse accounts, and `DP` for dependent accounts.
* firstName () - Filter list by partial match in first name
* lastName () - Filter list by partial match in last name
* name () - Filter list by partial match in family name or organization name
* status () - Filter list by list match in account status
* phoneAreaCode () - Filter list by partial match in phone area code
* phoneNumber () - Filter list by partial match in phone number
* emailAddress () - Filter list by partial match in email address
* addressCity () - Filter list by partial match in address city
* addressState () - Filter list by partial match in address state
* addressPostalCode () - Filter list by partial match in address postal code
* addressCountry () - Filter list by partial match in address country
* addressLine1 () - Filter list by partial match in address line 1
* addressLine2 () - Filter list by partial match in address line 2
* addressLine3 () - Filter list by partial match in address line 3
* addressLine4 () - Filter list by partial match in address line 4
* combinedAddress (optional) - Filter list by partial match on a combination of address lines 1-4. Values for all lines are concatenated with a space and compared with the search criteria.
* transactionStart () - Filter list by transaction date on or after the specified value
* transactionEnd () - Filter list by transaction date on or before the specified value
* transaction () - Filter list by partial match in document number
* transactionPaymentType () - Filter list by exact match in transaction payment type
* transactionReferenceNumber () - Filter list by partial match in transaction reference number
* codeType () - Filter list by exact match in code type
* codeValue () - Filter list by exact match in code value
* dateType () - Filter list by exact match in date type
* dateValue () - Filter list by exact match in date value
* noteType () - Filter list by exact match in note type
* noteShortComment () - Filter list by partial match in note short comment
* noteLongComment () - Filter list by partial match in note long comment
* numberType () - Filter list by exact match in number type
* numberValue () - Filter list by exact match in number value
* soundsLike () - Filter list by sounds-like first name and/or last name
* sortMethod () - Method for sorting the result set. Possible values are 'A' to sort by account number, 'Z' to sort by zip/postal code, last name and first name, 'L' to sort by last name and first name, 'Y' to sort by zip/postal code and organization or 'O' to sort by organization.
* otherAddresses () - Specify which addresses on the account to return along with the Primary address. A value of "active" will return only active other addresses. A value of "all" will return all other addresses (both active and inactive).
* criteriaGroupId () - Filter list by advanced find criteria group. Either criteriaGroupId or advancedFindCriteria (or both) should be null.
* isAssignedToMe () - Filter list to only include those accounts which are assinged the current user's accessor or the accessor of any group the current user is a member of
* multiColumnSearch () - Filter list by a partial match on formatted name or organization name
* advancedFindCriteria () - The criteria array to use for executing an advanced find search
* excludeFamiliesAndOrganizations (deprecated, defaults to `false`) - Filter out all family and organization accounts. If true, any account type provided in the `type` field will be ignored.

Note: `excludeFamiliesAndOrganizations` has been deprecated. Use a list match in `type` instead. Sending `I,CN,SP,DP` for `type` will result in the same behavior.

##### Returns

A dictionary with an items property that contains an array of up to limit accounts, starting at index offset. Each entry in the array is a separate account object. If no more accounts are available, the resulting array will be empty. This request should never return an error.

Note: The Retrieve an account resource returns the inceptionDate, mediaOutletDescription and sourceDescription. If you need these values without making additional calls to get each one, please use the [Retrieve an account](#retrieve-an-account) resource.

### Activity Counts

#### Retrieve all activity counts

```
DEFINITION
GET http://apiserver/activitycounts?interfaceId&id&interfaceIdList

EXAMPLE REQUEST
$.get("http://localhost:49195/activitycounts?interfaceId=AccountsView&id=16403&interfaceIdList=AccountCodes,AccountDates,AccountNumbers");

EXAMPLE RESPONSE
{
    "AccountCodes": 5,
    "AccountDates": 2,
    "AccountNotes": 0,
    "AccountNumbers": 2,
    "AccountAttachments": 0,
    "AccountPhones": 0,
    "AccountEmails": 0,
    "AccountTransactions": 0,
    "AccountRelationships": 0
}

```

Returns a single object that contains all requested activity counts for the provided interfaceId and Id.

#### Arguments

* interfaceId (required) - The Interface ID to return counts for.
* id (required) - The record id or other id of the component to return the counts for..
* interfaceIdList (required) - The list of Activity Interface IDs to return counts for.

#### Returns

An object containing a map of each activity defined for the provided interfaceId and a count of the number of that item associated with that record.

### Account Addresses

#### Create an account address

```
DEFINITION
POST http://apiserver/accounts/:id/addresses

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/addresses", {
    "type": "MAIL",
    "line1": "30 Rockefeller Plaza",
    "postalCode": "10112",
    "country": "USA"
});

EXAMPLE RESPONSE
{
    "id": "230529",
    "accountNumber": "1483320",
    "type": "MAIL",
    "typeDescription": "Mailing Address",
    "line1": "30 Rockefeller Plaza",
    "line2": null,
    "line3": null,
    "line4": null,
    "city": null,
    "state": null,
    "stateDescription": null,
    "postalCode": "10112",
    "country": "USA",
    "countryDescription": "United States of America",
    "isPoBox": false,
    "start": null,
    "end": null,
    "isPrimary": false,
    "isActive": true,
    "isDefaultBilling": false,
    "isDefaultShipping": false,
    "functionalCategory": null,
    "latitudeOverride": null,
    "longitudeOverride": null,
    "validatedDate": "2019-07-22",
    "userVerifiedAccessorId": null,
    "userVerifiedAccessorIdDescription": null,
    "isSavedPaymentBillingAddress": false
}

```

Creates a new account address object.

##### Arguments

* type (required) - The address type. Must be a defined address type.
* country (required) - The country of the address. Must be a defined country.
* line1 (optional) - The first line of the address.
* line2 (optional) - The second line of the address.
* line3 (optional) - The third line of the address.
* line4 (optional) - The fourth line of the address.
* city (optional) - The city of the address. If not specified, will default based on specified postal code's default city.
* state (optional) - The state of the address. If not specified, will default based on specified postal code's default state.
* postalCode (optional) - The postal code of the address. Must be a defined postal code of the specified country.
* isPoBox (optional) - Whether or not the address is a PO Box.
* isPrimary (optional) - Whether or not the address is the primary address for the account. If not specified, will default to false.
* start (optional) - The first date the address is in use. Ignored if isPrimary is true.
* end (optional) - The last date the address is in use. Ignored if isPrimary is true.
* isActive (optional) - Whether or not the address is active.
* isDefaultBilling (optional) - Whether or not the address is the default billing address for the account. If not specified, will default to false.
* isDefaultShipping (optional) - Whether or not the address is the default shipping address for the account. If not specified, will default to false.
* functionalCategory (optional) - The functional category of this address.
* latitudeOverride (optional) - The latitude override for mapping integration. Only used if both functionalCategory and longitudeOverride have valid values
* longitudeOverride (optional) - The longitude override for mapping integration. Only used if both functionalCategory and latitudeOverride have valid values
* validatedDate (optional) - The date the address was validated.
* userVerifiedAccessorId (optional) - The AccessorId of the user that manually verified the address. (The address was not validated through address standardization)
* standardizationResult (optional) - Notifies Services if address standardization has already been performed
  + status - Can be either `Verified`, `UserCertified`, or `Error`. `Verified` means that the address has been standardized and verified correct. `UserCertified` means that the user has verified that this address is correct, even if the standardization provider used did not recognize it. An account note (A01a) will be placed on the account. `Error` means that the address standardization failed, so Services can go ahead and try standardization, if it has been set up with a provider. Also, an account note (A01a) will be placed on the account.
  + provider - The name of the Address Standardization provider that has already been used on this address.
  + message - Error message that should be included on the A01a when the status is `Error`.

##### Returns

Returns an account address object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined address type).

#### Retrieve an account address

```
DEFINITION
GET http://apiserver/accounts/:id/addresses/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/addresses/230529");

EXAMPLE RESPONSE
{
    "id": "230529",
    "accountNumber": "1483320",
    "type": "MAIL",
    "typeDescription": "Mailing Address",
    "line1": "30 Rockefeller Plaza",
    "line2": null,
    "line3": null,
    "line4": null,
    "city": null,
    "state": null,
    "stateDescription": null,
    "postalCode": "10112",
    "country": "USA",
    "countryDescription": "United States of America",
    "isPoBox": false,
    "start": null,
    "end": null,
    "isPrimary": false,
    "isActive": true,
    "isDefaultBilling": false,
    "isDefaultShipping": false,
    "functionalCategory": "DM",
    "latitudeOverride": null,
    "longitudeOverride": null,
    "validatedDate": "2019-07-22",
    "userVerifiedAccessorId": null,
    "userVerifiedAccessorIdDescription": null,
    "isSavedPaymentBillingAddress": false
}

```

Retrieves the details of an existing account address. You need only supply the account address id.

##### Arguments

* id (required) - The id of the account address to retrieve.

##### Returns

Returns an account address object if a valid id was provided.

#### Update an account address

```
DEFINITION
POST http://apiserver/accounts/:id/addresses/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/addresses/230529", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "230529",
    "accountNumber": "1483320",
    "type": "MAIL",
    "typeDescription": "Mailing Address",
    "line1": "30 Rockefeller Plaza",
    "line2": null,
    "line3": null,
    "line4": null,
    "city": null,
    "state": null,
    "stateDescription": null,
    "postalCode": "10112",
    "country": "USA",
    "countryDescription": "United States of America",
    "isPoBox": false,
    "start": null,
    "end": null,
    "isPrimary": false,
    "isActive": false,
    "isDefaultBilling": false,
    "isDefaultShipping": false,
    "functionalCategory": "DM",
    "latitudeOverride": null,
    "longitudeOverride": null,
    "validatedDate": "2019-07-22",
    "userVerifiedAccessorId": null,
    "userVerifiedAccessorIdDescription": null,
    "isSavedPaymentBillingAddress": false
}


```

Updates the specified account address by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The address type. Must be a defined address type.
* line1 (optional) - The first line of the address.
* line2 (optional) - The second line of the address.
* line3 (optional) - The third line of the address.
* line4 (optional) - The fourth line of the address.
* city (optional) - The city of the address.
* state (optional) - The state of the address.
* postalCode (optional) - The postal code of the address. Must be a defined postal code of the specified country.
* country (optional) - The country of the address. Must be a defined country.
* isPoBox (optional) - Whether or not the address is a PO Box.
* isPrimary (optional) - Whether or not the address is the primary address for the account. This value can only be changed to false by setting isPrimary to true on a different account address.
* isDefaultBilling (optional) - Whether or not the address is the default billing address for the account. If not specified, will default to false.
* isDefaultShipping (optional) - Whether or not the address is the default shipping address for the account. If not specified, will default to false.
* start (optional) - The first date the address is in use. Ignored if isPrimary is true.
* end (optional) - The last date the address is in use. Ignored if isPrimary is true.
* isActive (optional) - Whether or not the address is active.
* functionalCategory (optional) - The functional category of this address.
* latitudeOverride (optional) - The latitude override for mapping integration. Only used if both functionalCategory and longitudeOverride have valid values
* longitudeOverride (optional) - The longitude override for mapping integration. Only used if both functionalCategory and latitudeOverride have valid values
* validatedDate (optional) - The date the address was validated.
* userVerifiedAccessorId (optional) - The AccessorId of the user that manually verified the address. (The address was not validated through address standardization)
* standardizationResult (optional) - Notifies Services if address standardization has already been performed
  + status - Can be either `Verified`, `UserCertified`, or `Error`. `Verified` means that the address has been standardized and verified correct. `UserCertified` means that the user has verified that this address is correct, even if the standardization provider used did not recognize it. An account note (A01a) will be placed on the account. `Error` means that the address standardization failed, so Services can go ahead and try standardization, if it has been set up with a provider. Also, an account note (A01a) will be placed on the account.
  + provider - The name of the Address Standardization provider that has already been used on this address.
  + message - Error message that should be included on the A01a when the status is `Error`.

##### Returns

Returns the account address object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined address type or address type value).

#### Delete an account address

```
DEFINITION
DELETE http://apiserver/accounts/:id/addresses/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/addresses/230529", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account address. It cannot be undone.

##### Arguments

* id (required) - The id of the account address to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account address id does not exist, this call returns an error.

#### List all account addresses

```
DEFINITION
GET http://apiserver/accounts/:id/addresses

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/addresses");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "230529",
            "accountNumber": "1483320",
            "type": "MAIL",
            "typeDescription": "Mailing Address",
            "line1": "30 Rockefeller Plaza",
            "line2": null,
            "line3": null,
            "line4": null,
            "city": null,
            "state": null,
            "stateDescription": null,
            "postalCode": "10112",
            "country": "USA",
            "countryDescription": "United States of America",
            "isPoBox": false,
            "start": null,
            "end": null,
            "isPrimary": false,
            "isActive": true,
            "isDefaultBilling": false,
            "isDefaultShipping": false,
            "functionalCategory": "DM",
            "latitudeOverride": null,
            "longitudeOverride": null,
            "validatedDate": "2019-07-22",
            "userVerifiedAccessorId": null,
            "userVerifiedAccessorIdDescription": null,
            "isSavedPaymentBillingAddress": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account addresses.

##### Arguments

* isActive (optional) - Specifies the active status of the account addresses to return: A value of true will only return active addresses. A value of false will return only inactive addresses. A value of null will return both active and inactive addresses.
* functionalCategory (optional) - Specifies to return only addresses with the given functional category
* includePrimary (optional) - Specifies whether to include the primary address in the response
* includeFamily (optional) - Specifies whether to include addresses across all family members in the response

##### Returns

A dictionary with an items property that contains an array of up to limit account addresses, starting at index offset. Each entry in the array is a separate account address object. If no more account addresses are available, the resulting array will be empty. This request should never return an error.

Note: This listing does not include primary addresses, unless the "includePrimary" parameter is true.

#### Standardize an address

```
DEFINITION
POST http://apiserver/standardizeaddress

EXAMPLE REQUEST
$.post("http://localhost:49195/standardizeaddress", {
    "line1": "3308 Fountainviuw",
    "line2": null,
    "line3": null,
    "line4": null,
    "city": "monsey",
    "state": "ny",
    "postalCode": "10952",
    "country": "USA",
    "secondaryNumber" null,
    "integrationConfigurationCode": null
});

EXAMPLE RESPONSE
{
    "isSuccessful": true,
    "notes": [ "We fixed the street spelling." ],
    "isMissingSecondaryNumber": false,
    "shouldPromptUserConfirmation": false,
    "shouldRemoveState": false,
    "shouldRemovePostalCode": false,
    "candidates": [{
        "id": null,
        "type": null,
        "typeDescription": null,
        "line1": "3308 Fountainview Dr",
        "line2": null,
        "line3": null,
        "line4": null,
        "city": "Monsey",
        "state": "NY",
        "stateDescription": null,
        "postalCode": "10952-2870",
        "country": "USA",
        "countryDescription": null,
        "isPoBox": null,
        "start": null,
        "end": null,
        "isPrimary": null,
        "isActive": null,
        "functionalCategory": null,
        "latitudeOverride": null,
        "longitudeOverride": null,
        "validatedDate": "2019-07-22",
        "userVerifiedAccessorId": null,
        "userVerifiedAccessorIdDescription": null
    }]
}


```

Attempts to find a matching validated address based on the parameters.

##### Arguments

* line1 (optional) - The first line of the address.
* line2 (optional) - The second line of the address.
* line3 (optional) - The third line of the address. This field will not be considered during standardization.
* line4 (optional) - The fourth line of the address. This field will not be considered during standardization.
* city (optional) - The city of the address.
* state (optional) - The state of the address.
* postalCode (required) - The postal code of the address. Must be a defined postal code of the specified country.
* country (required) - The country of the address. Must be a defined country.
* secondaryNumber (optional) - This field is used by ASO when a secondary number is required for standarization.
* integrationConfigurationCode (optional) - The Integration Configuration Code of the address standardization service to use instead of the default StudioEnterprise configured address standardization service in the `ADDRSTDSVC` Control Record.

##### Returns

Returns a response object with zero to five candidates of potentially matching addresses. Notes will contain some information about the changes made or things that must be fixed before the address can be validated. The response will be marked as unsuccessful if no matching addresses were found.

### Account Advanced Find Saved Views

#### Create an account advanced find saved view

```
DEFINITION
POST http://apiserver/advancedfindsegments

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedfindsegments", {
    description: "Deleted Accounts",
    isSystemView: false,
    assignedToAccessor: 1111
});

EXAMPLE RESPONSE
{
    "id": "62",
    "description": "Deleted Accounts",
    "isSystemView": false,
    "sawId": null,
    "assignedToAccessor": 1111
}

```

Creates a new account advanced find saved view

##### Arguments

* description (required) - The description of the advanced find saved view
* isSystemView (required) - If creating a system view, set to true. If creating a user view, set to false.
* assignedToAccessor (optional) - If isSystemView equals false: To create a saved view for a specific user, the accessor of the user. To create a saved view for the current user, no value is required.
* sawId (optional) - If isSystemView equals true: the sawId required to use the view.

##### Returns

Returns an account advanced find saved view object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account advanced find saved view

```
DEFINITION
GET http://apiserver/advancedfindsegments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedfindsegments/62");

EXAMPLE RESPONSE
{
    "id": "62",
    "description": "Deleted Accounts",
    "isSystemView": false,
    "sawId": null,
    "assignedToAccessor": 1111
}

```

Retrieves the details of an existing account advanced find saved view.

##### Arguments

* id (required) - The id of the account advanced find saved view to retrieve.

##### Returns

Returns an account advanced find saved view object if a valid id was provided.

#### Update an account advanced find saved view

```
DEFINITION
POST http://apiserver/advancedfindsegments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedfindsegments/62", {
    "description": "All Deleted Accounts"
});

EXAMPLE RESPONSE
{
    "id": "62",
    "description": "All Deleted Accounts",
    "isSystemView": false,
    "sawId": null,
    "assignedToAccessor": 1111
}


```

Updates the specified account advanced find saved view by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the advanced find saved view
* isSystemView (optional) - If updating to a system view, set to true. If updating to a user view, set to false.
* assignedToAccessor (optional) - If isSystemView equals false: To assign the saved view to a specific user, the accessor of the user. To assign a saved view to the current user, no value is required.
* sawId (optional) - If isSystemView equals true: the sawId required to use the view.

##### Returns

Returns the account advanced find saved view object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account advanced find saved view

```
DEFINITION
DELETE http://apiserver/advancedfindsegments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedfindsegments/62", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Deletes an account advanced find saved view and all related account advanced find saved view details.

##### Arguments

* id (required) - The id of the account advanced find saved view to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account advanced find saved view does not exist, this call returns an error.

#### List all account advanced find saved views

```
DEFINITION
GET http://apiserver/advancedfindsegments

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedfindsegments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "62",
            "description": "All Deleted Accounts",
            "isSystemView": false,
            "sawId": null,
            "assignedToAccessor": 1111
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account advanced find saved views which match the given criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* description (optional) - The description of the advanced find saved view
* view (optional) - The view to retrieve (null, "user", "system", "both").
   **null (Default) - return all system and user views regardless of user** "user" - return only user views (defaults to current user)
   **"system" - return only system views** "both" - return system and user views for a user (defaults to current user)
* assignedToAccessor (optional) - If view equals "user" OR "both": The accessor of the user to retrieve views for. If null or no value is provided, defaults to the accessor of the current user. Otherwise this value is ignored.
* roleId (optional) - If view equals "system" or "both": restrict the system views returned by roleId. If no value is provided, all system views are returned.
* sawId (required conditionally) - If roleId is provided, sawID is required.

##### Returns

A dictionary with an items property that contains an array of up to limit account advanced find saved views, starting at index offset. Each entry in the array is a separate account advanced find saved view object. If no more account advanced find saved views are available, the resulting array will be empty. This request should never return an error.

### Account Advanced Find Saved View Details

#### Create an account advanced find saved view detail

```
DEFINITION
POST http://apiserver/advancedfindsegments/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedfindsegments/62/details", {
    "criteriaType": "ACCTSTAT",
    "processingSequence": 1,
    "comparisonType": "EQ",
    "comparisonValue": "A",
    "isActive": true
});

EXAMPLE RESPONSE
{
    "id": "123",
    "segment": "62",
    "criteriaGroup": "62",
    "criteriaType": "ACCTSTAT",
    "processingSequence": 1,
    "comparisonType": "EQ",
    "comparisonValue": "A",
    "isActive": true
}

```

Creates a new account advanced find saved view detail object

##### Arguments

* criteriaType (required) - A valid criteria Type
* processingSequence (optional) - If multiple detail records exist, the order of processing.
* comparisonType (required) - A valid comparison type for the provided criteria type
* comparisonValue (required) - A valid comparison value for the provided comparison type
* isActive (required) - whether or not the detail record is active

##### Returns

Returns an account advanced find saved view detail object if the call succeeded. Returns an error if create parameters are invalid.

#### Update an account advanced find saved view detail

```
DEFINITION
POST http://apiserver/advancedfindsegments/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedfindsegments/51/details/95", {
    "comparisonType": "EQ",
    "comparisonValue": "2014-01-01",
});

EXAMPLE RESPONSE
{
    "id": "95",
    "segment": "51",
    "criteriaGroup": "51",
    "criteriaType": "BIRTHDAY",
    "processingSequence": 1,
    "comparisonType": "EQ",
    "comparisonValue": "2014-01-01",
    "isActive": true
}


```

Updates the specified account advanced find saved view detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* criteriaType (optional) - The criteria type.
* comparisonType (optional) - A valid comparison type given the criteria type.
* comparisonValue (optional) - A valid comparison value given the comparison type.
* processingSequence (optional) - If multiple detail records exist, the order of processing.
* isActive (optional) - true makes the detail record active, false makes the detail record inactive.

##### Returns

Returns the account advanced find saved view detail object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account advanced find saved view detail

```
DEFINITION
DELETE http://apiserver/advancedfindsegments/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedfindsegments/51/details/95", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Deletes an account advanced find saved view detail.

##### Arguments

* id (required) - The id of the account advanced find saved view detail to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account advanced find saved view detail does not exist, this call returns an error.

#### List all account advanced find saved view details

```
DEFINITION
GET http://apiserver/advancedfindsegments/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedfindsegments/51/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "95",
            "segment": "51",
            "criteriaGroup": "51",
            "criteriaType": "BIRTHDAY",
            "processingSequence": 1,
            "comparisonType": "BETWEEN",
            "comparisonValue": "1944-01-01;2015-01-31",
            "isActive": true
        }
    ]
}

```

Returns a list of all account advanced find saved view details.

##### Returns

A dictionary with an items property that contains an array of up to limit account advanced find saved view details, starting at index offset. Each entry in the array is a separate account advanced find saved view detail object. If no more account advanced find saved view details are available, the resulting array will be empty. This request should never return an error.

### Account Alerts

#### List all account alerts

```
DEFINITION
GET http://apiserver/accounts/:id/alerts

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/alerts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "account": "1483320",
            "accountName": "John Doe",
            "shortComment": "Big dog",
            "longComment": "He has a big dog named Russ. Ask how his dog is doing.",
            "fontColor": "#001122",
            "backgroundColor": "#DDEEFF",
            "priority": 1
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account alerts for the account and for the family, if one exists.

### Account AR Statements

#### Delete an account AR statement

```
DEFINITION
DELETE http://apiserver/accounts/:accountId/arstatements/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16403/arstatements/10059", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account AR statement. It cannot be undone.

##### Arguments

* accountId (required) - The account number for which to delete an AR statement.
* id (required) - The id of the account AR statement to be deleted.

##### Returns

Returns a `204 No Content` response on success.

#### List all account AR statements

```
DEFINITION
GET http://apiserver/accounts/:id/arstatements

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/arstatements");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 3,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "4370",
            "statementId": "1000000037",
            "accountNumber": "16230",
            "accountName": "Mr. John A Doe Jr.",
            "start": "2014-09-11",
            "end": "2014-10-10",
            "totalAmount": 20.15,
            "beginningBalance": 30.57,
            "endingBalance": 10.42,
            "formType": "ARSTMT"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account AR statements. If the account is in a family, then all AR statements within the family are returned.

##### Returns

A dictionary with an items property that contains an array of up to limit account AR statements, starting at index offset. Each entry in the array is a separate account AR statement object. If no more account AR statements are available, the resulting array will be empty. This request should never return an error.

### Account Assignments

#### Create an account assignment

```
DEFINITION
POST http://apiserver/accounts/:id/assignments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/9318/assignments", {
    "assignedToAccessor": "6630",
    "functionalCategory": "OCC",
    "type": "VOLUNTEER",
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20"
});

EXAMPLE RESPONSE
{
    "id": "1011",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "OCC",
    "functionalCategoryDescription": "Operation Christmas Child"
    "type": "VOLUNTEER",
    "typeDescription": "Region volunteer"
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20",
    "end": null
}

```

Creates a new account assignment object.

##### Arguments

* assignedToAccessor (required) - The accessor of the user or authorized account assigned to the account.
* functionalCategory (optional) - The function of the assignment. This can be used to denote the department of the accessor.
* type (optional) - The type of the assignment.
* isPrimary (optional) - Whether or not the assignment is primary for the functional category. Defaulted to false.
* isActive (optional) - Whether or not the account assignment is active. Defaulted to true.
* start (optional) - When the assignment starts. Defaulted to today's date.
* end (optional) - When the assignment ends.

##### Returns

Returns an account assignment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined accessor).

#### Retrieve an account assignment

```
DEFINITION
GET http://apiserver/accounts/:id/assignments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/9318/assignments/1011");

EXAMPLE RESPONSE
{
    "id": "1011",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "OCC",
    "functionalCategoryDescription": "Operation Christmas Child"
    "type": "VOLUNTEER",
    "typeDescription": "Region volunteer"
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20",
    "end": null
}

```

Retrieves the details of an existing account assignment.

##### Arguments

* id (required) - The id of the account assignment to retrieve.

##### Returns

Returns an account assignment object if a valid id was provided.

#### Update an account assignment

```
DEFINITION
POST http://apiserver/accounts/:id/assignments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/9318/assignments/1011", {
    "functionalCategory": "DM",
    "type": "REGIONDIR"
});

EXAMPLE RESPONSE
{
    "id": "1011",
    "assignedToAccessor": "6630",
    "assignedToAccessorDescription": "Webber Bradley",
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Donor Ministries"
    "type": "REGIONDIR",
    "typeDescription": "Regional Director"
    "isPrimary": true,
    "isActive": true,
    "start": "2015-02-20",
    "end": null
}


```

Updates the specified account assignment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.
* functionalCategory (optional) - The function of the assignment. This can be used to denote the department of the accessor.
* type (optional) - The type of the assignment.
* isPrimary (optional) - Whether or not the assignment is primary for the functionalCategory.
* isActive (optional) - Whether or not the account assignment is active.
* start (optional) - When the assignment starts.
* end (optional) - When the assignment ends.

##### Returns

Returns the account assignment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined account or accessor).

#### Delete an account assignment

```
DEFINITION
DELETE http://apiserver/accounts/:id/assignment/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/9318/assignment/1011", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Disables an account assignment by setting the active flag and end date.

##### Arguments

* id (required) - The id of the account assignment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account assignment does not exist, this call returns an error.

#### List all account assignments

```
DEFINITION
GET http://apiserver/accounts/:id/assignments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/9318/assignments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1011",
            "assignedToAccessor": "6630",
            "assignedToAccessorDescription": "Webber Bradley",
            "functionalCategory": "OCC",
            "functionalCategoryDescription": "Operation Christmas Child"
            "type": "VOLUNTEER",
            "typeDescription": "Region volunteer"
            "isPrimary": true,
            "isActive": true,
            "start": "2015-02-20",
            "end": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account assignments.

##### Returns

A dictionary with an items property that contains an array of up to limit account assignments, starting at index offset. Each entry in the array is a separate account assignment object. If no more account assignments are available, the resulting array will be empty. This request should never return an error.

### Account Attachments

#### Create an account attachment

```
DEFINITION
POST http://apiserver/accounts/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new account attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns an account attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve an account attachment

```
DEFINITION
GET http://apiserver/accounts/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing account attachment. You need only supply the account attachment id.

##### Arguments

* id (required) - The id of the account attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns an account attachment object if a valid id was provided.

#### Update an account attachment

```
DEFINITION
POST http://apiserver/accounts/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified account attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the account attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined account attachment type code).

#### Delete an account attachment

```
DEFINITION
DELETE http://apiserver/accounts/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account attachment id does not exist, this call returns an error.

#### List all account attachments

```
DEFINITION
GET http://apiserver/accounts/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit account attachments, starting at index offset. Each entry in the array is a separate account attachment object. If no more account attachments are available, the resulting array will be empty. This request should never return an error.

### Account Codes

#### Create an account code

```
DEFINITION
POST http://apiserver/accounts/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/codes", {
    "type": "ACCTSTATUS",
    "value": "59"
});

EXAMPLE RESPONSE
{
    "id": "1761507",
    "type": "ACCTSTATUS",
    "value": "59",
    "dataSource": "DDC",
    "isActive": true
}

```

Creates a new account code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* dataSource (optional) - The data source of the code. If not specified, a default value will be set.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an account code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve an account code

```
DEFINITION
GET http://apiserver/accounts/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/codes/1761507");

EXAMPLE RESPONSE
{
    "id": "1761507",
    "type": "ACCTSTATUS",
    "value": "59",
    "dataSource": "DDC",
    "isActive": true
}

```

Retrieves the details of an existing account code. You need only supply the account code id.

##### Arguments

* id (required) - The id of the account code to retrieve.

##### Returns

Returns an account code object if a valid id was provided.

#### Update an account code

```
DEFINITION
POST http://apiserver/accounts/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/codes/1761507", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1761507",
    "type": "ACCTSTATUS",
    "value": "59",
    "dataSource": "DDC",
    "isActive": false
}


```

Updates the specified account code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the account code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete an account code

```
DEFINITION
DELETE http://apiserver/accounts/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/codes/1761507", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account code. It cannot be undone.

##### Arguments

* id (required) - The id of the account code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account code id does not exist, this call returns an error.

#### List all account codes

```
DEFINITION
GET http://apiserver/accounts/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "1761507",
            "type": "ACCTSTATUS",
            "value": "59",
            "dataSource": "DDC",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account codes.

##### Returns

A dictionary with an items property that contains an array of up to limit account codes, starting at index offset. Each entry in the array is a separate account code object. If no more account codes are available, the resulting array will be empty. This request should never return an error.

### Account Communications

#### Create an account communication

```
DEFINITION
POST http://apiserver/accounts/:id/communications

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications", {
    "type": "LETTER",
    "source": "EV11CPCATL",
    "response": {
        "letter": "LETTER"
    }
});

EXAMPLE RESPONSE
{
    "id": "4218",
    "type": "LETTER",
    "date": "2014-11-24",
    "isInbound": false,
    "shortComment": null,
    "longComment": null,
    "url": null,
    "source": "EV11CPCATL",
    "sourceDescription": "Pastor's Conf March 2011 Atlanta",
    "elementGroup": "PC11C",
    "elementGroupDescription": "Pastor's Conference March 2011",
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "sendEmailAfterSave": false
    "response": {
        "id": 379156,
        "method": null,
        "type": "LETTER",
        "profileGroup": null,
        "printGroup": null,
        "printDate": null,
        "paragraphs": [],
        "letter": "LETTER",
        "completionText": null,
        "address": "1000022533",
        "inserts": null,
        "status": "Y"
    }
}

```

Creates a new account communication object.

##### Arguments

* type (required) - The communication type code of the account communication. Must be a defined communication type code.
* source (required) - The source code of the account communication. Must be a defind source code.
* response (optional) - The response object of the account communication. Required if type is LETTER.
* date (optional) - The date of the account communication.
* isInbound (optional) - Whether or not the account communication is inbound.
* shortComment (optional) - The short comment of the account communication.
* longComment (optional) - The long comment of the account communication.
* url (optional) - The url where the account communication is located.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.
* sendEmailAfterSave (optional) - Whether or not to send an open, outbound Account Communication of type EMAIL to the account holder, ignored if type is not EMAIL
* ignoreAdditionalInformation (optional) - If true, then in the API Response, the following properties will be null: response, elementGroup and elementGroupDescription
* deleteAllParagraphs (optional) - If true, delete all paragraph codes.
* location (optional) - Only valid if the type is APPOINTMNT, used in syncing with calendar integrations
* startDateTimeUtc (optional) - Only valid if the type is APPOINTMNT or PHONE, used in syncing with calendar integrations, in 24 hour UTC format
* endDateTimeUtc (optional) - Only valid if the type is APPOINTMNT or PHONE, used in syncing with calendar integrations, in 24 hour UTC format
* fromEmailAddress (optional) - Only valid if the type is EMAIL, sets the from address for email communications, primarily used in syncing with email integrations
* toEmailAddresses (optional) - Only valid if the type is EMAIL, sets the to addresses for email communications, in a comma separated list, primarily used in syncing with email integrations
* ccEmailAddresses (optional) - Only valid if the type is EMAIL, sets the cc addresses for email communications, in a comma separated list, primarily used in syncing with email integrations
* originalCommunicationId (optional) - Only valid if the type is EMAIL, the id of the originating communication that should be updated to a status of 'C', this is used when creating a reply communication

##### Returns

Returns an account communication object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined communication type or not specifying a source code).

#### Retrieve an account communication

```
DEFINITION
GET http://apiserver/accounts/:accountId/communications/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/245862");

EXAMPLE RESPONSE
{
    "id": "245862",
    "type": "LETTER",
    "date": "2014-11-24",
    "isInbound": true,
    "shortComment": null,
    "longComment": null,
    "url": null,
    "source": "EV11CPCATL",
    "sourceDescription": "Pastor's Conf March 2011 Atlanta",
    "elementGroup": "PC11C",
    "elementGroupDescription": "Pastor's Conference March 2011",
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "response": {
        "id": 379156,
        "method": null,
        "type": "LETTER",
        "profileGroup": null,
        "printGroup": null,
        "printDate": null,
        "paragraphs": [],
        "letter": "2010YREND",
        "completionText": null,
        "address": "1000022533",
        "inserts": null,
        "status": "N"
    }
}

```

Retrieves the details of an existing account communication. You need only supply the account communication id.

##### Arguments

* id (required) - The id of the account communication to retrieve.
* accountId (required) - The id of the account to retrieve a communication for.
* ignoreAdditionalInformation (optional) - If true, then in the API Response, the following properties will be null: response, elementGroup and elementGroupDescription

##### Returns

Returns an account communication object if a valid id was provided.

#### Update an account communication

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/4218", {
    "isInbound": false
});

EXAMPLE RESPONSE
{
    "id": "245862",
    "type": "LETTER",
    "date": "2014-11-24",
    "isInbound": false,
    "shortComment": null,
    "longComment": null,
    "url": null,
    "source": "EV11CPCATL",
    "sourceDescription": "Pastor's Conf March 2011 Atlanta",
    "elementGroup": "PC11C",
    "elementGroupDescription": "Pastor's Conference March 2011",
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "sendEmailAfterSave": false,
    "response": {
        "id": 379156,
        "method": null,
        "type": "LETTER",
        "profileGroup": null,
        "printGroup": null,
        "printDate": null,
        "paragraphs": [],
        "letter": "2010YREND",
        "completionText": null,
        "address": "1000022533",
        "inserts": null,
        "status": "N"
    }
}


```

Updates the specified account communication by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The communication type code of the account communication. Must be a defined communication type code.
* source (optional) - The source code of the account communication. Must be a defind source code.
* date (optional) - The date of the account communication.
* isInbound (optional) - Whether or not the account communication is inbound.
* shortComment (optional) - The short comment of the account communication.
* longComment (optional) - The long comment of the account communication.
* url (optional) - The url where the account communication is located.
* response (optional) - The account communication response object if type is LETTER
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.
* sendEmailAfterSave (optional) - Whether or not to send an open, outbound Account Communication of type EMAIL to the account holder, ignored if type is not EMAIL
* ignoreAdditionalInformation (optional) - If true, then in the API Response, the following properties will be null: response, elementGroup and elementGroupDescription
* deleteAllParagraphs (optional) - If true, delete all paragraph codes.
* location (optional) - Only valid if the type is APPOINTMNT, used in syncing with calendar integrations
* startDateTimeUtc (optional) - Only valid if the type is APPOINTMNT or PHONE, used in syncing with calendar integrations, in 24 hour UTC format
* endDateTimeUtc (optional) - Only valid if the type is APPOINTMNT or PHONE, used in syncing with calendar integrations, in 24 hour UTC format
* fromEmailAddress (optional) - Only valid if the type is EMAIL, sets the from address for email communications, primarily used in syncing with email integrations
* toEmailAddresses (optional) - Only valid if the type is EMAIL, sets the to addresses for email communications, in a comma separated list, primarily used in syncing with email integrations
* ccEmailAddresses (optional) - Only valid if the type is EMAIL, sets the cc addresses for email communications, in a comma separated list, primarily used in syncing with email integrations

##### Returns

Returns the account communication object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined account communication type code).

#### Delete an account communication

```
DEFINITION
DELETE http://apiserver/accounts/:id/communications/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/communications/4218", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account communication. It cannot be undone.

##### Arguments

* id (required) - The id of the account communication to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account communication id does not exist, this call returns an error.

#### List all account communications

```
DEFINITION
GET http://apiserver/accounts/:id/communications

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "245862",
            "type": "LETTER",
            "date": "2014-11-24",
            "isInbound": true,
            "shortComment": null,
            "longComment": null,
            "url": null,
            "source": "EV11CPCATL",
            "sourceDescription": "Pastor's Conf March 2011 Atlanta",
            "elementGroup": "PC11C",
            "elementGroupDescription": "Pastor's Conference March 2011",
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null,
            "response": {
                "id": 379156,
                "method": null,
                "type": "LETTER",
                "profileGroup": null,
                "printGroup": null,
                "printDate": null,
                "paragraphs": [],
                "letter": "2010YREND",
                "completionText": null,
                "address": "1000022533",
                "inserts": null,
                "status": "N"
            }
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account communications.

##### Arguments

* getPageContainingId (optional) - To support Queue Item Processing, setting this query param to a valid account communication id, will return the page of account communications that the id is included in. If an invalid id is provided, it will be ignored and the first page of account communications will be returned.
* getPageContainingSource (optional) - Setting this query param to a valid source code will return the page of account communications that contains a communication record with the specified source code. If an invalid source code is provided, it will be ignored and the first page of account communications will be returned. If the `getPageContainingId` and `getPageContainingSource` criteria are both provided, then `getPageContainingSource` will be ignored.
* ignoreAdditionalInformation (optional) - If true, then in the API Response, the following properties will be null for every account communication object in the items array: response, elementGroup and elementGroupDescription
* accessorId (optional) - When provided, the communications returned will be filtered to only the communications that are assigned to the accessor.
* includeGroups (optional) - Only used if `accessorId` is also provided. It will include any communication that is assigned to any group member of a group that the `accessorId` is in.
* groupMemberAccessorId (optional) - Only used if `includeGroups` is provided. It will filter the communications to only return communications that are assigned to the specified group member.

##### Returns

A dictionary with an items property that contains an array of up to limit account communications, starting at index offset. Each entry in the array is a separate account communication object. If no more account communications are available, the resulting array will be empty. This request should never return an error.

### Account Communication Attachments

#### Create an account communication attachment

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new account communication attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns an account communication attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve an account communication attachment

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing account communication attachment. You need only supply the account communication attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns an account communication attachment object if a valid id was provided.

#### Update an account communication attachment

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified account communication attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the account communication attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined account communication attachment type code).

#### Delete an account communication attachment

```
DEFINITION
DELETE http://apiserver/accounts/:id/communications/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/communications/620701/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account communication attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the account communication attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account communication attachment id does not exist, this call returns an error.

#### List all account communication attachments

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account communication attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit account communication attachments, starting at index offset. Each entry in the array is a separate account communication attachment object. If no more account communication attachments are available, the resulting array will be empty. This request should never return an error.

### Account Communication Codes

#### Create an account communication code

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/codes", {
    "type": "DDCCOMMCD1",
    "value": "BJU"
});

EXAMPLE RESPONSE
{
    "id": "461",
    "type": "DDCCOMMCD1",
    "typeDescription": "First Quarter Communication"
    "value": "BJU",
    "valueDescription": "BJU Comm"
    "isActive": true
}

```

Creates a new account communication code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an account communication code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve an account communication code

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/codes/461");

EXAMPLE RESPONSE
{
    "id": "461",
    "type": "DDCCOMMCD1",
    "typeDescription": "First Quarter Communication"
    "value": "BJU",
    "valueDescription": "BJU Comm"
    "isActive": true
}

```

Retrieves the details of an existing account communication code. You need only supply the account communication code id.

##### Arguments

* id (required) - The id of the account communication code to retrieve.

##### Returns

Returns an account communication code object if a valid id was provided.

#### Update an account communication code

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/codes/461", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "461",
    "typeDescription": "First Quarter Communication"
    "value": "BJU",
    "valueDescription": "BJU Comm"
    "isActive": false
}


```

Updates the specified account communication code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the account communication code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete an account communication code

```
DEFINITION
DELETE http://apiserver/accounts/:id/communications/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/communications/620701/codes/461", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account communication code. It cannot be undone.

##### Arguments

* id (required) - The id of the account communication code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account communication code id does not exist, this call returns an error.

#### List all account communication codes

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "461",
            "type": "DDCCOMMCD1",
            "typeDescription": "First Quarter Communication"
            "value": "BJU",
            "valueDescription": "BJU Comm"
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account communication codes.

##### Returns

A dictionary with an items property that contains an array of up to limit account communication codes, starting at index offset. Each entry in the array is a separate account communication code object. If no more account communication codes are available, the resulting array will be empty. This request should never return an error.

### Account Communication Dates

#### Create an account communication date

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/dates", {
    "type": "COMMSTART",
    "value": "2012-12-05"
});

EXAMPLE RESPONSE
{
    "id": "949",
    "type": "COMMSTART",
    "typeDescription": "Communication Start Date",
    "value": "2012-12-05",
    "isActive": true
}

```

Creates a new account communication date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an account communication date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve an account communication date

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/dates/949");

EXAMPLE RESPONSE
{
    "id": "949",
    "type": "COMMSTART",
    "typeDescription": "Communication Start Date",
    "value": "2012-12-05",
    "isActive": true
}

```

Retrieves the details of an existing account communication date. You need only supply the account communication date id.

##### Arguments

* id (required) - The id of the account communication date to retrieve.

##### Returns

Returns an account communication date object if a valid id was provided.

#### Update an account communication date

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/dates/949", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "949",
    "type": "COMMSTART",
    "typeDescription": "Communication Start Date",
    "value": "2012-12-05",
    "isActive": false
}


```

Updates the specified account communication date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the account communication date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete an account communication date

```
DEFINITION
DELETE http://apiserver/accounts/:id/communications/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/communications/620701/dates/949", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account communication date. It cannot be undone.

##### Arguments

* id (required) - The id of the account communication date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account communication date id does not exist, this call returns an error.

#### List all account communication dates

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "949",
            "type": "COMMSTART",
            "typeDescription": "Communication Start Date",
            "value": "2012-12-05",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account communication dates.

##### Returns

A dictionary with an items property that contains an array of up to limit account communication dates, starting at index offset. Each entry in the array is a separate account communication date object. If no more account communication dates are available, the resulting array will be empty. This request should never return an error.

### Account Communication Email

#### Send an account communication email

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/email

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/825234/email", {
    "to": "home@example.com",
    "from": "admin@example.com"
});

EXAMPLE RESPONSE
200 OK

```

Sends an account communication email. The communication shortComment will be used as the email subject and the communication longComment will be used as the email body. The request will return an error if the communication type is not `EMAIL`.

##### Arguments

* to (required) - The email address of the recipient.
* from (required) - The email address of the sender.

### Account Communication Notes

#### Create an account communication note

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/notes", {
    "type": "DDCCOMMNT1",
    "shortComment": "Communication Note"
});

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCCOMMNT1",
    "typeDescription": "Account Communication",
    "shortComment": "Communication Note",
    "longComment": null
}

```

Creates a new account communication note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns an account communication note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve an account communication note

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/notes/31884");

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCCOMMNT1",
    "typeDescription": "Account Communication",
    "shortComment": "Communication Note",
    "longComment": null
}

```

Retrieves the details of an existing account communication note. You need only supply the account communication note id.

##### Arguments

* id (required) - The id of the account communication note to retrieve.

##### Returns

Returns an account communication note object if a valid id was provided.

#### Update an account communication note

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/notes/31884", {
    "shortComment": null,
    "longComment": "Communication Note"
});

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCCOMMNT1",
    "typeDescription": "Account Communication",
    "shortComment": null,
    "longComment": "Communication Note"
}


```

Updates the specified account communication note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the account communication note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete an account communication note

```
DEFINITION
DELETE http://apiserver/accounts/:id/communications/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/communications/620701/notes/31884", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account communication note. It cannot be undone.

##### Arguments

* id (required) - The id of the account communication note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account communication note id does not exist, this call returns an error.

#### List all account communication notes

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "31884",
            "type": "DDCCOMMNT1",
            "typeDescription": "Account Communication",
            "shortComment": "Communication Note",
            "longComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account communication notes.

##### Returns

A dictionary with an items property that contains an array of up to limit account communication notes, starting at index offset. Each entry in the array is a separate account communication note object. If no more account communication notes are available, the resulting array will be empty. This request should never return an error.

### Account Communication Numbers

#### Create an account communication number

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/numbers", {
    "type": "DDCCOMMNB1",
    "value": 12
});

EXAMPLE RESPONSE
{
    "id": "7413",
    "type": "DDCCOMMNB1",
    "typeDescription": "Number of Communications",
    "value": 12,
    "isActive": true
}

```

Creates a new account communication number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an account communication number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve an account communication number

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/numbers/7413");

EXAMPLE RESPONSE
{
    "id": "7413",
    "type": "DDCCOMMNB1",
    "typeDescription": "Number of Communications",
    "value": 12,
    "isActive": true
}

```

Retrieves the details of an existing account communication number. You need only supply the account communication number id.

##### Arguments

* id (required) - The id of the account communication number to retrieve.

##### Returns

Returns an account communication number object if a valid id was provided.

#### Update an account communication number

```
DEFINITION
POST http://apiserver/accounts/:id/communications/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/communications/620701/numbers/7413", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "7413",
    "type": "DDCCOMMNB1",
    "typeDescription": "Number of Communications",
    "value": 12,
    "isActive": false
}


```

Updates the specified account communication number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the account communication number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete an account communication number

```
DEFINITION
DELETE http://apiserver/accounts/:id/communications/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/communications/620701/numbers/7413", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account communication number. It cannot be undone.

##### Arguments

* id (required) - The id of the account communication number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account communication number id does not exist, this call returns an error.

#### List all account communication numbers

```
DEFINITION
GET http://apiserver/accounts/:id/communications/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/communications/620701/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7413",
            "type": "DDCCOMMNB1",
            "typeDescription": "Number of Communications",
            "value": 12,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account communication numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit account communication numbers, starting at index offset. Each entry in the array is a separate account communication number object. If no more account communication numbers are available, the resulting array will be empty. This request should never return an error.

### Account Compliance Tracking

#### Create an account compliance tracking record

```
DEFINITION
POST http://apiserver/accounts/:id/compliancetracking

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/32654/compliancetracking", {
    "contactMethod": "EMAIL"
    "contactMethodDescription": "Email"
    "file": "data:application/pdf;base64,JVBERi0xLjYNJeLjz9MNCjQ2NSAwIG9iag08PC9MaW5lYXJpemVkIDEvTCAzMD"
    "fileName": "Document.pdf"
    "optInDate": "2018-05-02"
    "optOutDate": "2018-05-25"
    "type": "GIFTAID"
    "typeDescription": "Gift Aid"
});

EXAMPLE RESPONSE
{
    "id": "10022"
    "account": "32654"
    "optInDate": "2018-05-02"
    "optOutDate": "2018-05-25"
    "type": "GIFTAID"
    "typeDescription": "Gift Aid"
    "contactMethod": "EMAIL"
    "contactMethodDescription": "Email"
    "file": "JVBERi0xLjYNJeLjz9MNCjQ2NSAwIG9iag08PC9MaW5lYXJpemVkIDEvTCAzMD"
    "fileMimeType": "application/pdf"
    "fileName": "Document.pdf"
}

```

Creates a new account compliance tracking record.

##### Arguments

* type(required) - The type of compliance tracking record
* optInDate (required) - The date that the compliance tracking record is in effect
* optOutDate (optional) - The date that the compliance tracking reocord is no longer in effect
* contactMethod (required) - The method of contact that initiated the compliance tracking record
* file (optional) - File attached to the compliance tracking record
* fileName (optional) - The name of the file attached to the compliance tracking record

##### Returns

Returns an account compliance tracking record object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account compliance tracking record

```
DEFINITION
GET http://apiserver/accounts/:id/compliancetracking/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/32654/compliancetracking/10022");

EXAMPLE RESPONSE
{
    "id": "10022"
    "account": "32654"
    "optInDate": "2018-05-02"
    "optOutDate": "2018-05-25"
    "type": "GIFTAID"
    "typeDescription": "Gift Aid"
    "contactMethod": "EMAIL"
    "contactMethodDescription": "Email"
    "file": "JVBERi0xLjYNJeLjz9MNCjQ2NSAwIG9iag08PC9MaW5lYXJpemVkIDEvTCAzMD"
    "fileMimeType": "application/pdf"
    "fileName": "Document.pdf"
}

```

Retrieves the details of an existing account compliance tracking record. You need only supply the id.

##### Arguments

* id (required) - The id of the account compliance tracking record to be retrieved.

#### Update an account compliance tracking record

```
DEFINITION
POST http://apiserver/accounts/:id/compliancetracking/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/32654/compliancetracking/10022", {
    "optOutDate": "2019-02-25"
});

EXAMPLE RESPONSE
{
    "id": "10022"
    "account": "32654"
    "optInDate": "2018-05-02"
    "optOutDate": "2019-02-25"
    "type": "GIFTAID"
    "typeDescription": "Gift Aid"
    "contactMethod": "EMAIL"
    "contactMethodDescription": "Email"
    "file": "JVBERi0xLjYNJeLjz9MNCjQ2NSAwIG9iag08PC9MaW5lYXJpemVkIDEvTCAzMD"
    "fileMimeType": "application/pdf"
    "fileName": "Document.pdf"
}


```

Updates the specified account compliance tracking record by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type(optional) - The type of compliance tracking record
* optInDate (optional) - The date that the compliance tracking record is in effect
* optOutDate (optional) - The date that the compliance tracking reocord is no longer in effect
* contactMethod (optional) - The method of contact that initiated the compliance tracking record
* file (optional) - File attached to the compliance tracking record
* fileName (optional) - The name of the file attached to the compliance tracking record

##### Returns

Returns the account compliance tracking record object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account compliance tracking record

```
DEFINITION
DELETE http://apiserver/accounts/:id/compliancetracking/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/32654/compliancetracking/10022", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account compliance tracking record. It cannot be undone.

##### Arguments

* id (required) - The id of the account compliance tracking record to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the account compliance tracking record does not exist, this call returns an error.

#### List all account compliance tracking records

```
DEFINITION
GET http://apiserver/accounts/:id/compliancetracking

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/:id/compliancetracking?");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10022"
            "account": "32654"
            "optInDate": "2018-05-02"
            "optOutDate": "2019-02-25"
            "type": "GIFTAID"
            "typeDescription": "Gift Aid"
            "contactMethod": "EMAIL"
            "contactMethodDescription": "Email"
            "file": "JVBERi0xLjYNJeLjz9MNCjQ2NSAwIG9iag08PC9MaW5lYXJpemVkIDEvTCAzMD"
            "fileMimeType": "application/pdf"
            "fileName": "Document.pdf"
        },
        {...},
    ]
}

```

Returns a list of all account compliance tracking records.

##### Returns

A dictionary with an items property that contains an array of up to limit account compliance tracking records, starting at index offset. Each entry in the array is a separate account compliance tracking object. If no more account compliance records are available, the resulting array will be empty. This request should never return an error.

### Account CRM Tracking

#### Create an account CRM tracking record

```
DEFINITION
POST http://apiserver/accounts/:id/crmtracking

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1234/crmtracking", {
    "crmRole": "CRM2013",
    "owner": "myDomain\myUser"
});

EXAMPLE RESPONSE
{
    "id": 10,
    "crmId": "I",
    "crmRole": "CRM2013",
    "owner": "myDomain\myUser"
    "processedDate": null
    "isActive": true
}

```

Creates an account CRM tracking object by setting the values of the parameters passed.

##### Arguments

* crmId (optional, Default: "I") - The id of the associated CRM environment.
* crmRole (required) - The CRM Role
* owner (required) - The owner within the CRM Role
* processedDate (optional) - The date the record was processed
* isActive (optional, Default: true) - Whether or not the CRM tracking record is active.

##### Returns

Returns an account CRM tracking object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account CRM tracking record

```
DEFINITION
GET http://apiserver/accounts/:id/crmtracking/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1234/crmtracking/10");

EXAMPLE RESPONSE
{
    "id": 10,
    "crmId": "2e2b81ef-8b24-e411-xxxx-00155dfc623c",
    "crmRole": "CRM2013",
    "description": "Donor Development"
    "owner": "myDomain\myUser"
    "processedDate": "2015-01-05"
    "isActive": true
}

```

Retrieves the details of an existing account CRM tracking record. You need only supply the account CRM tracking id.

##### Arguments

* id (required) - The id of the account CRM tracking record to retrieve.

##### Returns

Returns an account CRM tracking object if a valid id was provided.

#### Update an account CRM tracking record

```
DEFINITION
POST http://apiserver/accounts/:id/crmtracking/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1234/crmtracking/10", {
    "owner": "company\jDoe"
});

EXAMPLE RESPONSE
{
    "id": 10,
    "crmId": "2e2b81ef-8b24-e411-xxxx-00155dfc623c",
    "crmRole": "CRM2013",
    "description": "Donor Development"
    "owner": "company\jDoe"
    "processedDate": "2015-01-05"
    "isActive": true
}

```

Updates the specified account CRM tracking record by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* crmId (optional) - The id of the associated CRM environment.
* owner (optional) - The owner within the CRM Role
* processedDate (optional) - The date the record was processed
* isActive (optional) - Whether or not the CRM tracking record is active.

##### Returns

Returns the account CRM tracking object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account CRM tracking record

```
DEFINITION
DELETE http://apiserver/accounts/:id/crmtracking/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1234/crmtracking/10", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account CRM tracking record. It cannot be undone.

##### Arguments

* id (required) - The id of the account CRM tracking record to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account CRM tracking record id does not exist, this call returns an error.

#### List all account CRM tracking records

```
DEFINITION
GET http://apiserver/accounts/:id/crmtracking

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1234/crmtracking");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": 10,
            "crmId": "2e2b81ef-8b24-e411-xxxx-00155dfc623c",
            "crmRole": "CRM2013",
            "description": "Donor Development"
            "owner": "myDomain\myUser"
            "status": "Y"
            "processedDate": "2015-01-05"
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account CRM tracking records.

##### Returns

A dictionary with an items property that contains an array of up to limit account CRM tracking records, starting at index offset. Each entry in the array is a separate account CRM tracking object. If no more account CRM tracking records are available, the resulting array will be empty. This request should never return an error.

### Account Cultivation Tracks

#### List all account cultivation tracks

```
DEFINITION
GET http://apiserver/accounts/:id/cultivationtracks

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/806/cultivationtracks");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "track": "DONDEV",
            "segment": "REPEAT",
            "assignmentDate": "2011-08-08",
            "isActive": true,
            "letter": "APOL",
            "product": "002",
            "deactivateDate": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account cultivation tracks.

##### Returns

A dictionary with an items property that contains an array of up to limit account cultivation tracks, starting at index offset. Each entry in the array is a separate account cultivation track object. If no more account cultivation tracks are available, the resulting array will be empty. This request should never return an error.

### Account Custom Entities

#### Create an account custom entity

```
DEFINITION
POST http://apiserver/accounts/:id/customentities/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/customentities/103", {
    "TYPE": "DOG",
    "NAME": "Rusty",
    "COLOR": "BROWN",
    "PURDATE": "2014-03-03"
});

EXAMPLE RESPONSE
{
    "id": "67231",
    "TYPE": "DOG",
    "NAME": "Rusty",
    "COLOR": "BROWN",
    "PURDATE": "2014-03-03"
}

```

Creates a new account custom entity object.

##### Arguments

The arguments list for create (including which are required) depends on the fields configured on the custom entity.

##### Returns

Returns an account custom entity object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid date for a date field or failing to specify a required field).

#### Retrieve an account custom entity

```
DEFINITION
GET http://apiserver/accounts/:id/customentities/:id/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/customentities/103/67231");

EXAMPLE RESPONSE
{
    "id": "67231",
    "TYPE": "DOG",
    "NAME": "Rusty",
    "COLOR": "BROWN",
    "PURDATE": "2014-03-03"
}

```

Retrieves the details of an existing account custom entity. You need only supply the account custom entity id.

##### Arguments

* id (required) - The id of the account custom entity to retrieve.

##### Returns

Returns an account custom entity object if a valid id was provided.

#### Update an account custom entity

```
DEFINITION
POST http://apiserver/accounts/:id/customentities/:id/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/customentities/103/67231", {
    "COLOR": "BLACK"
});

EXAMPLE RESPONSE
{
    "id": "67231",
    "TYPE": "DOG",
    "NAME": "Rusty",
    "COLOR": "BLACK",
    "PURDATE": "2014-03-03"
}


```

Updates the specified account custom entity by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

The arguments list for create (including which are required) depends on the fields configured on the custom entity.

##### Returns

Returns the account custom entity object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid date for a date field or attempting to set to null a required field).

#### Delete an account custom entity

```
DEFINITION
DELETE http://apiserver/accounts/:id/customentities/:id/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/customentities/103/67231", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account custom entity. It cannot be undone.

##### Arguments

* id (required) - The id of the account custom entity to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account custom entity id does not exist, this call returns an error.

#### List all account custom entities

```
DEFINITION
GET http://apiserver/accounts/:id/customentities/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/customentities/103");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "67231",
            "TYPE": "DOG",
            "NAME": "Rusty",
            "COLOR": "BROWN",
            "PURDATE": "2014-03-03"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account custom entities.

##### Returns

A dictionary with an items property that contains an array of up to limit account custom entities, starting at index offset. Each entry in the array is a separate account custom entity object. If no more account custom entities are available, the resulting array will be empty. This request should never return an error.

### Account Dates

#### Create an account date

```
DEFINITION
POST http://apiserver/accounts/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/dates", {
    "type": "DDCBDATE",
    "value": "1976-03-23"
});

EXAMPLE RESPONSE
{
    "id": "1857",
    "type": "DDCBDATE",
    "value": "1976-03-23",
    "dataSource": "ADMIN",
    "isActive": true
}

```

Creates a new account date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* dataSource (optional) - The data source of the code. If not specified, a default value will be set.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an account date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve an account date

```
DEFINITION
GET http://apiserver/accounts/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/dates/1857");

EXAMPLE RESPONSE
{
    "id": "1857",
    "type": "DDCBDATE",
    "value": "1976-03-23",
    "dataSource": "ADMIN",
    "isActive": true
}

```

Retrieves the details of an existing account date. You need only supply the account date id.

##### Arguments

* id (required) - The id of the account date to retrieve.

##### Returns

Returns an account date object if a valid id was provided.

#### Update an account date

```
DEFINITION
POST http://apiserver/accounts/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/dates/1857", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "1857",
    "type": "DDCBDATE",
    "value": "1976-03-23",
    "dataSource": "ADMIN",
    "isActive": false
}


```

Updates the specified account date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the account date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete an account date

```
DEFINITION
DELETE http://apiserver/accounts/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/dates/1857", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account date. It cannot be undone.

##### Arguments

* id (required) - The id of the account date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account date id does not exist, this call returns an error.

#### List all account dates

```
DEFINITION
GET http://apiserver/accounts/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "1857",
            "type": "DDCBDATE",
            "value": "1976-03-23",
            "dataSource": "ADMIN",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account dates.

##### Returns

A dictionary with an items property that contains an array of up to limit account dates, starting at index offset. Each entry in the array is a separate account date object. If no more account dates are available, the resulting array will be empty. This request should never return an error.

### Account Default Donation

#### Create an account default donation

```
DEFINITION
POST http://apiserver/accounts/:id/defaultdonation

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/defaultdonation", {
    "mediaOutlet": "FAST"
});

EXAMPLE RESPONSE
{
    "mediaOutlet": "FAST",
    "shouldGenerateReceipt": true
}

```

Creates a new account default donation object.

##### Arguments

* mediaOutlet (optional) - The media outlet id of the account default donation. Must be a defined media outlet id.
* shouldGenerateReceipt (optional) - Whether or not a receipt should be generated for the account default donation. If not specified, will default to true.

##### Returns

Returns an account default donation object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined media outlet id).

#### Retrieve an account default donation

```
DEFINITION
GET http://apiserver/accounts/:id/defaultdonation

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/defaultdonation");

EXAMPLE RESPONSE
{
    "mediaOutlet": "FAST",
    "shouldGenerateReceipt": true
}

```

Retrieves the header of an existing account default donation.

##### Returns

Returns an account default donation object.

#### Update an account default donation

```
DEFINITION
POST http://apiserver/accounts/:id/defaultdonation

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/defaultdonation", {
    "shouldGenerateReceipt": false
});

EXAMPLE RESPONSE
{
    "mediaOutlet": "FAST",
    "shouldGenerateReceipt": false
}


```

Updates the specified account default donation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* mediaOutlet (optional) - The media outlet id of the account default donation. Must be a defined media outlet id.
* shouldGenerateReceipt (optional) - Whether or not a receipt should be generated for the account default donation.

##### Returns

Returns the account default donation object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined media outlet id).

#### Delete an account default donation

```
DEFINITION
DELETE http://apiserver/accounts/:id/defaultdonation

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/defaultdonation", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account default donation including all its details. It cannot be undone.

##### Returns

Returns a 204 No Content response on success. If an account default donation does not exist for the specified account, this call returns an error.

### Account Default Donation Details

#### Create an account default donation detail

```
DEFINITION
POST http://apiserver/accounts/:id/defaultdonation/details

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/defaultdonation/details", {
    "amount": 500,
    "source": "ABC08",
    "project": "220000"
});

EXAMPLE RESPONSE
{
    "id": "150",
    "amount": 500,
    "source": "ABC08",
    "sourceDescription": "Jan Bible Appeal",
    "project": "220000",
    "projectDescription": "Bright Futures Endowment",
    "subaccount": "001",
    "relatedAccount": null,
    "relatedAccountName": null,
    "accountPledge": "1576",
    "pledgeCode": "082011",
    "pledgeDescription": "August 2011 Fund",
    "isDeductible": true,
    "isAnonymous": false,
    "shortComment": null
}

```

Creates a new account default donation detail object.

##### Arguments

* amount (required) - The amount of the account default donation detail.
* source (required) - The source code of the account default donation detail.
* project (required) - The project code of the account default donation detail.
* subaccount (optional) - The subaccount code of the account default donation detail.
* relatedAccount (optional) - The associated account number of the account default donation detail.
* accountPledge (optional) - The account pledge id of the account default donation detail.
* isDeductible (optional) - Whether or not the account default donation detail is deductible. If not specified, will default to true.
* isAnonymous (optional) - Whether or not the account default donation detail is anonymous. If not specified, will default to false.
* shortComment (optional) - The short comment of the account default donation detail.

##### Returns

Returns an account default donation detail object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined default donation detail type).

#### Retrieve an account default donation detail

```
DEFINITION
GET http://apiserver/accounts/:id/defaultdonation/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/defaultdonation/details/150");

EXAMPLE RESPONSE
{
    "id": "150",
    "amount": 500,
    "source": "ABC08",
    "sourceDescription": "Jan Bible Appeal",
    "project": "220000",
    "projectDescription": "Bright Futures Endowment",
    "subaccount": "001",
    "relatedAccount": null,
    "relatedAccountName": null,
    "accountPledge": "1576",
    "pledgeCode": "082011",
    "pledgeDescription": "August 2011 Fund",
    "isDeductible": true,
    "isAnonymous": false,
    "shortComment": null
}

```

Retrieves the details of an existing account default donation detail. You need only supply the account default donation detail id.

##### Arguments

* id (required) - The id of the account default donation detail to retrieve.

##### Returns

Returns an account default donation detail object if a valid id was provided.

#### Update an account default donation detail

```
DEFINITION
POST http://apiserver/accounts/:id/defaultdonation/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/defaultdonation/details/150", {
    "isAnonymous": true
});

EXAMPLE RESPONSE
{
    "id": "150",
    "amount": 500,
    "source": "ABC08",
    "sourceDescription": "Jan Bible Appeal",
    "project": "220000",
    "projectDescription": "Bright Futures Endowment",
    "subaccount": "001",
    "relatedAccount": null,
    "relatedAccountName": null,
    "accountPledge": "1576",
    "pledgeCode": "082011",
    "pledgeDescription": "August 2011 Fund",
    "isDeductible": true,
    "isAnonymous": true,
    "shortComment": null
}


```

Updates the specified account default donation detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* amount (optional) - The amount of the account default donation detail.
* source (optional) - The source code of the account default donation detail.
* project (optional) - The project code of the account default donation detail.
* subaccount (optional) - The subaccount code of the account default donation detail.
* relatedAccount (optional) - The associated account number of the account default donation detail.
* accountPledge (optional) - The account pledge id of the account default donation detail.
* isDeductible (optional) - Whether or not the account default donation detail is deductible. If not specified, will default to true.
* isAnonymous (optional) - Whether or not the account default donation detail is anonymous. If not specified, will default to false.
* shortComment (optional) - The short comment of the account default donation detail.

##### Returns

Returns the account default donation detail object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined default donation detail type or default donation detail type value).

#### Delete an account default donation detail

```
DEFINITION
DELETE http://apiserver/accounts/:id/defaultdonation/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/defaultdonation/details/150", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account default donation detail. It cannot be undone.

##### Arguments

* id (required) - The id of the account default donation detail to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account default donation detail id does not exist, this call returns an error.

#### List all account default donation details

```
DEFINITION
GET http://apiserver/accounts/:id/defaultdonation/details

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/defaultdonation/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "150",
            "amount": 500,
            "source": "ABC08",
            "sourceDescription": "Jan Bible Appeal",
            "project": "220000",
            "projectDescription": "Bright Futures Endowment",
            "subaccount": "001",
            "relatedAccount": null,
            "relatedAccountName": null,
            "accountPledge": "1576",
            "pledgeCode": "082011",
            "pledgeDescription": "August 2011 Fund",
            "isDeductible": true,
            "isAnonymous": false,
            "shortComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account default donation details.

##### Returns

A dictionary with an items property that contains an array of up to limit account default donation details, starting at index offset. Each entry in the array is a separate account default donation detail object. If no more account default donation details are available, the resulting array will be empty. This request should never return an error.

### Account Duplicate Detection

#### List all duplicate detection accounts

```
DEFINITION
GET http://apiserver/accounts?isDuplicateDetection=true

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts?isDuplicateDetection=true&lastName=Jones&firstName=Bob&name=&addressPostalCode=75093&addressLine1=2909%20Copper%20Ridge%20Dr&addressCity=Plano&addressState=TX&addressCountry=USA&accountType=I&accountToExclude=0&isInFamily=false");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "16446",
            "type": "I",
            "title": "Mr.",
            "firstName": "Bob",
            "middleName": "Q",
            "lastName": "Jones",
            "suffix": "Jr.",
            "status": "A",
            "email": " ",
            "salutation": null,
            "gender": null,
            "birthdate": null,
            "address": {
                "id": "1000017330",
                "line1": "2909 Copper Ridge Dr",
                "line2": "2",
                "line3": "3",
                "line4": "4",
                "city": "Plano",
                "state": "TX",
                "postalCode": "75093",
                "country": "USA",
                "isPoBox": false,
                "isPrimary": true,
                "isActive": true,
                "isDefaultBilling": false,
                "isDefaultShipping": false,
                "validatedDate": "2019-07-22",
                "userVerifiedAccessorId": null,
                "userVerifiedAccessorIdDescription": null
            },
            "source": null,
            "mediaOutlet": null,
            "phone": " "
        },
        { ... }
    ]
}


```

##### Arguments

* isDuplicateDetection (required) - A value of `true` is required to enable the duplicate detection search
* firstName (optional) - First name of the account by which to check for duplicate accounts
* lastName (optional) - Last name of the account by which to check for duplicate accounts
* name (optional) - Organization or Family name by which to check for duplicate accounts
* addressPostalCode (optional) - Postal Code by which to check for duplicate accounts
* addressLine1 (optional) - Address Line 1 by which to check for duplicate accounts
* addressCity (optional) - City by which to check for duplicates
* addressState (optional) - State by which to check for duplicates
* addressCountry (optional) - Country by which to check for duplicates
* accountType (optional) - Account Type by which to check for duplicates
* accountToExclude (optional) - Account Number to exclude from the results. In the case where the account does not exist yet, use the value of `0`.
* isInFamily (optional) - Specifies if the account for which duplicates are being searched for is in a family

##### Returns

Returns accounts that meet the duplicate detection criteria.

### Account Donation Acknowledgments

#### Create an account donation acknowledgment

```
DEFINITION
POST http://apiserver/accounts/:id/donationacknowledgments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/184688/donationacknowledgments", {
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "zipPostal": "54364",
    "letterCode": "HONOR",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": false,
    "donorAddress": "465536"
});

EXAMPLE RESPONSE
{
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "addressLine1": "800 F St NW",
    "addressLine2": null,
    "addressLine3": null,
    "addressLine4": null,
    "city": "Washington",
    "state": "DC",
    "zipPostal": "20004",
    "country": "US",
    "responseId": "63546",
    "letterCode": "HONOR",
    "letterCodeDescription": "In honor of",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": false,
    "donorAddress": "465536",
    "donorAddressLine1": "119 Hemenway St",
    "donorAddressLine2": null,
    "donorAddressLine3": null,
    "donorAddressLine4": null,
    "donorCity": "Boston",
    "donorState": "MA",
    "donorZipPostal": "02115",
    "donorCountry": "US",
    "responseStatus": "H",
    "profileGroupId": "5847",
    "printGroupId": null,
    "printDate": null
}

```

##### Arguments

* documentNumber (required) - The document number (transactionId) of the donation acknowledgment
* recipientAccountNumber (required) - The account number of the recipient of the donation acknowledgment
* recipientAddress (required) - The addressId of the recipient of the donation acknowledgment
* letterCode (required) - The letter code used in the response for the donation acknowledgment
* fromName (required) - The name used in the from line of the donation acknowledgment
* toName (required) - The name used in the to line of the donation acknowledgment
* message (optional) - The message put on the donation acknowledgment
* sendToDonor (required) - Whether to send the donation acknowledgment to the recipient or the donor
* donorAddress (required if sendToDonor is true) - The address of the donor, used if we are sending the acknowledgment to the donor

##### Returns

Returns a donation acknowledgment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined recipient account).

#### Retrieve an account donation acknowledgment

```
DEFINITION
GET http://apiserver/accounts/:id/donationacknowledgments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/184688/donationacknowledgments/45");

EXAMPLE RESPONSE
{
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "addressLine1": "800 F St NW",
    "addressLine2": null,
    "addressLine3": null,
    "addressLine4": null,
    "city": "Washington",
    "state": "DC",
    "zipPostal": "20004",
    "country": "US",
    "responseId": "63546",
    "letterCode": "HONOR",
    "letterCodeDescription": "In honor of",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": false,
    "donorAddress": "465536",
    "donorAddressLine1": "119 Hemenway St",
    "donorAddressLine2": null,
    "donorAddressLine3": null,
    "donorAddressLine4": null,
    "donorCity": "Boston",
    "donorState": "MA",
    "donorZipPostal": "02115",
    "donorCountry": "US",
    "responseStatus": "H",
    "profileGroupId": "5847",
    "printGroupId": null,
    "printDate": null
}

```

Retrieves the details of an existing donation acknowledgment. You need only supply the donation acknowledgment id.

##### Arguments

* id (required) - The id of the donation acknowledgment to be retrieved.

##### Returns

Returns a donation acknowledgment object if a valid id was provided.

#### Update an account donation acknowledgment

```
DEFINITION
POST http://apiserver/accounts/:id/donationacknowledgments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/184688/donationacknowledgments/45", {
    "sendToDonor": true
});

EXAMPLE RESPONSE
{
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "addressLine1": "800 F St NW",
    "addressLine2": null,
    "addressLine3": null,
    "addressLine4": null,
    "city": "Washington",
    "state": "DC",
    "zipPostal": "20004",
    "country": "US",
    "responseId": "63546",
    "letterCode": "HONOR",
    "letterCodeDescription": "In honor of",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": true,
    "donorAddress": "465536",
    "donorAddressLine1": "119 Hemenway St",
    "donorAddressLine2": null,
    "donorAddressLine3": null,
    "donorAddressLine4": null,
    "donorCity": "Boston",
    "donorState": "MA",
    "donorZipPostal": "02115",
    "donorCountry": "US",
    "responseStatus": "H",
    "profileGroupId": "5847",
    "printGroupId": null,
    "printDate": null
}


```

Updates the specified donation acknowledgment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the donation acknowledgment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### Delete an account donation acknowledgment

```
DEFINITION
DELETE http://apiserver/accounts/:id/donationacknowledgments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/184688/donationacknowledgments/45", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* id (required) - The id of the account donation acknowledgment to be deleted.

##### Returns

Returns a 200 OK response on success. If the donation acknowledgment id does not exist then this call returns an error.

#### Reset an account donation acknowledgment

```
DEFINITION
POST http://apiserver/accounts/:id/donationacknowledgments/:id/reset

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/184688/donationacknowledgments/45/reset");

EXAMPLE RESPONSE
204 No Content

```

Resets the response of the specified donation acknowledgment.

##### Returns

Returns a 200 OK response on success. If the donation acknowledgment id does not exist then this call returns an error.

#### List all account donation acknowledgments

```
DEFINITION
GET http://apiserver/accounts/:id/donationacknowledgments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/83309/donationacknowledgments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "45",
            "documentNumber": "44635",
            "recipientAccountNumber": "6345",
            "recipientAccountName": "Robert Franklin",
            "recipientAddress": "87649",
            "addressLine1": "800 F St NW",
            "addressLine2": null,
            "addressLine3": null,
            "addressLine4": null,
            "city": "Washington",
            "state": "DC",
            "zipPostal": "20004",
            "country": "US",
            "responseId": "63546",
            "letterCode": "HONOR",
            "letterCodeDescription": "In honor of",
            "fromName": "Bobby",
            "toName": "Jack",
            "message": "Thanks for speaking at our event!",
            "sendToDonor": false,
            "donorAddress": "465536",
            "donorAddressLine1": "119 Hemenway St",
            "donorAddressLine2": null,
            "donorAddressLine3": null,
            "donorAddressLine4": null,
            "donorCity": "Boston",
            "donorState": "MA",
            "donorZipPostal": "02115",
            "donorCountry": "US",
            "responseStatus": "H",
            "profileGroupId": "5847",
            "printGroupId": null,
            "printDate": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all donation acknowledgments on the account.

##### Returns

A dictionary with an items property that contains an array of up to limit donation acknowledgments, starting at index offset. Each entry in the array is a separate donation acknowledgment object. If no more donation acknowledgments are available, the resulting array will be empty. This request should never return an error.

### Account Donation Acknowledgment Items

#### Create a account donation acknowledgment item

```
DEFINITION
POST http://apiserver/accounts/:id/donationacknowledgments/:id/items

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/184688/donationacknowledgments/45/items", {
    "donationId": "6596"
});

EXAMPLE RESPONSE
{
    "id": "53",
    "donationAcknowledgmentId": "45",
    "donationId": "6596",
    "amount": 20.5,
    "description": "Water Wells in Africa"
}

```

##### Arguments

* donationId (required) - The identifier (or temporary identifier) of the donation that is being acknowledged.

##### Returns

Returns the account donation acknowledgment item object the was created.

#### Retrieve a account donation acknowledgment item

```
DEFINITION
GET http://apiserver/accounts/:id/donationacknowledgments/:id/items/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/184688/donationacknowledgments/45/items/53");

EXAMPLE RESPONSE
{
    "id": "53",
    "donationAcknowledgmentId": "45",
    "donationId": "6596",
    "amount": 20.5,
    "description": "Water Wells in Africa"
}

```

Retrieves the details of an existing account donation acknowledgment item. You need only supply the donation acknowledgment item id.

##### Arguments

* id (required) - The id of the account donation acknowledgment item to be retrieved.

##### Returns

Returns a account donation acknowledgment item object if a valid id was provided.

#### Delete a account donation acknowledgment item

```
DEFINITION
DELETE http://apiserver/accounts/:id/donationacknowledgments/:id/items/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/184688/donationacknowledgments/45/items/53", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

This will permanently delete a account donation acknowledgment item from the account.

##### Arguments

* id (required) - The id of the account donation acknowledgment to be deleted.

##### Returns

Returns a 200 OK response on success. If the account donation acknowledgment item id does not exist or if the response has been printed, then this call returns an error.

#### List all account donation acknowledgment items

```
DEFINITION
GET http://apiserver/accounts/:id/donationacknowledgments/:id/items

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/83309/donationacknowledgments/45/items");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "53",
            "donationAcknowledgmentId": "45",
            "donationId": "6596",
            "amount": 20.5,
            "description": "Water Wells in Africa"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account donation acknowledgment items.

##### Returns

A dictionary with an items property that contains an array of up to limit account donation acknowledgment items, starting at index offset. Each entry in the array is a separate account donation acknowledgment item object. If no more account donation acknowledgment items are available, the resulting array will be empty. This request should never return an error.

### Account Email Subscriptions

#### Create an account email subscription

```
DEFINITION
POST http://apiserver/accounts/:id/emailsubscriptions

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/emailsubscriptions", {
    "emailId": "97426",
    "type": "DAILYDEV",
    "status": "A",
    "source": "EV11CPCATL",
    "start": "2014-05-01",
    "end": "2015-05-18"
});

EXAMPLE RESPONSE
{
    "id": "26",
    "account": "1483320",
    "accountName": "John Doe",
    "emailId": "97426",
    "emailAddress": "home@example.com",
    "type": "DAILYDEV",
    "typeDescription": "Daily devotional",
    "status": "A",
    "statusDescription": "Active",
    "source": "EV11CPCATL",
    "sourceDescription": "Pastor's Conf March 2011 Atlanta",
    "start": "2014-05-01",
    "end": "2015-05-18",
    "cancelReasonCode": null,
    "cancelReasonDescription": null
}

```

Creates a new account email subscription object.

##### Arguments

* emailId (optional) - The email address of the subscription.
* type (required) - The email subscription type. Must be a defined email subscription type.
* status (required) - Status of the email subscription.
* source (required) - Source of the subscription.
* start (required) - Start date of the subscription.
* end (optional) - End date of the subscription.
* cancelReasonCode (optional) - Reason the account has canceled this subscription.

##### Returns

Returns an account email subscription object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined email subscription type).

#### Retrieve an account email subscription

```
DEFINITION
GET http://apiserver/accounts/:id/emailsubscriptions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/emailsubscriptions/97426");

EXAMPLE RESPONSE
{
    "id": "26",
    "account": "1483320",
    "accountName": "John Doe",
    "emailId": "97426",
    "emailAddress": "home@example.com",
    "type": "DAILYDEV",
    "typeDescription": "Daily devotional",
    "status": "A",
    "statusDescription": "Active",
    "source": "EV11CPCATL",
    "sourceDescription": "Pastor's Conf March 2011 Atlanta",
    "start": "2014-05-01",
    "end": "2015-05-18",
    "cancelReasonCode": "NIL",
    "cancelReasonDescription": "Not Interested Any Longer"
}

```

Retrieves the details of an existing account email subscription. You need only supply the account email subscription id.

##### Arguments

* id (required) - The id of the account email subscription to retrieve.

##### Returns

Returns an account email subscription object if a valid id was provided.

#### Update an account email subscription

```
DEFINITION
POST http://apiserver/accounts/:id/emailsubscriptions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/emailsubscriptions/97426", {
    "type": "NEWSLET"
});

EXAMPLE RESPONSE
{
    "id": "26",
    "account": "1483320",
    "accountName": "John Doe",
    "emailId": "97426",
    "emailAddress": "home@example.com",
    "type": "NEWSLET",
    "typeDescription": "Newsletter",
    "status": "A",
    "source": "EV11CPCATL",
    "statusDescription": "Active",
    "sourceDescription": "Pastor's Conf March 2011 Atlanta",
    "start": "2014-05-01",
    "end": "2015-05-18",
    "cancelReasonCode": "NIL",
    "cancelReasonDescription": "Not Interested Any Longer"
}


```

Updates the specified account email subscription by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* account (optional) - Account to change the on the email subscription.
* emailId (optional) - The email address of the subscription. Passing null will always use primary email address.
* type (optional) - The email subscription type. Must be a defined email subscription type.
* status (optional) - Status of the email subscription.
* source (optional) - Source of the subscription.
* start (optional) - Start date of the subscription.
* end (optional) - End date of the subscription.
* cancelReasonCode (optional) - Reason the account has canceled this subscription.

##### Returns

Returns the account email subscription object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined cancel reason or subscription type).

#### Delete an account email subscription

```
DEFINITION
DELETE http://apiserver/accounts/:id/emailsubscriptions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/emailsubscriptions/97426", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account email subscription. It cannot be undone.

##### Arguments

* id (required) - The id of the account email subscription to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account email subscription id does not exist, this call returns an error.

#### List all account email subscriptions

```
DEFINITION
GET http://apiserver/accounts/:id/emailsubscriptions

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/emailsubscriptions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "26",
            "account": "1483320",
            "accountName": "John Doe",
            "emailId": "97426",
            "emailAddress": "home@example.com",
            "type": "NEWSLET",
            "typeDescription": "Newsletter",
            "status": "A",
            "statusDescription": "Active",
            "source": "EV11CPCATL",
            "sourceDescription": "Pastor's Conf March 2011 Atlanta",
            "start": "2014-05-01",
            "end": "2015-05-18",
            "cancelReasonCode": "NIL",
            "cancelReasonDescription": "Not Interested Any Longer"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account email subscriptions.

##### Returns

A dictionary with an items property that contains an array of up to limit account email subscriptions, starting at index offset. Each entry in the array is a separate account email subscription object. If no more account email subscriptions are available, the resulting array will be empty. This request should never return an error.

#### List all account email subscriptions by user id

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/emailsubscriptions

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/AA28CF39-54D7-4373-8549-B686951632A6/emailsubscriptions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "21202",
            "account": "41749",
            "accountName": "John Doe",
            "emailId": "319736",
            "emailAddress": "john.doe@donordirect.com",
            "type": "DAILYDEV",
            "typeDescription": "Daily Devotional",
            "status": "A",
            "statusDescription": "Active",
            "source": "EV11CPCATL",
            "sourceDescription": "Pastor's Conf March 2011 Atlanta",
            "start": "2018-12-20",
            "end": null,
            "cancelReasonCode": null,
            "cancelReasonDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account email subscriptions.

##### Returns

A dictionary with an items property that contains an array of up to limit account email subscriptions, starting at index offset. Each entry in the array is a separate account email subscription object. If no more account email subscriptions are available, the resulting array will be empty. This request should never return an error.

#### Subscribe or unsubscribe from account email subscriptions by user id

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/emailsubscriptions

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/AA28CF39-54D7-4373-8549-B686951632A6/emailsubscriptions", {
    "emailAddress": "john.doe@donordirect.com",
    "source": "EV11CPCATL",
    "store": "10023",
    "subscriptionTypes": ["DAILYDEV"]
});

EXAMPLE RESPONSE
204 No Content

```

Subscribes or unsubscribes to all email subscriptions of the provided types on the account linked to the provided token.

##### Arguments

* emailAddress (required if cancelReason is not provided) - The email address of the subscription when subscribing. If cancelReason is provided we are unsubscribing.
* source (required) - Source of the subscription.
* store (required) - Store the email subscription has been created in. Used for defaulting source code on subscribe when one is not provided.
* cancelReason (optional: will unsubscribe if provided) - Reason the account has cancelled this subscription.

##### Returns

Returns 204 No Content response if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined email subscription type).

### Account Emails

#### Create an account email

```
DEFINITION
POST http://apiserver/accounts/:id/emails

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/emails", {
    "type": "HOME",
    "emailAddress": "home@example.com"
});

EXAMPLE RESPONSE
{
    "id": "97426",
    "account": "1483320",
    "accountName": "John Doe",
    "type": "HOME",
    "emailAddress": "home@example.com",
    "dateAdded": "2016-06-09",
    "isPrimary": false,
    "isActive": true,
    "dataSource": null,
    "functionalCategory": null,
    "functionalCategoryDescription": null,
    "optOutIndicator": null,
    "optOutReasonCode": null,
    "optOutReasonCodeDescription": null,
    "optOutDate": null,
    "dateLastSynced": null,
    "externalSystem": null,
    "externalSystemId": null
}

```

Creates a new account email object.

##### Arguments

* type (required) - The email type. Must be a defined email type.
* emailAddress (required) - The email address.
* isPrimary (optional) - Whether or not the email is the primary address for the account.
* isActive (optional) - Whether or not the email is active.
* dataSource (optional) - The data source of the email. If not specified, a default value will be set.
* functionalCategory (optional) - The functional category of this email.
* optOutIndicator (optional) - Whether or not the account has opted out of this email.
* optOutReasonCode (optional) - Reason the account has opted out of this email.
* optOutDate (optional) - Date the account has opted out of this email.

##### Returns

Returns an account email object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined email type).

#### Retrieve an account email

```
DEFINITION
GET http://apiserver/accounts/:id/emails/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/emails/97426");

EXAMPLE RESPONSE
{
    "id": "97426",
    "account": "1483320",
    "accountName": "John Doe",
    "type": "HOME",
    "emailAddress": "home@example.com",
    "isPrimary": false,
    "isActive": true,
    "dataSource": null
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Direct Mail"
    "optOutIndicator": true,
    "optOutReasonCode": "SPAM",
    "optOutReasonCodeDescription": "Spam Mail",
    "optOutDate": "2015-05-13",
    "dateLastSynced": null,
    "externalSystem": null,
    "externalSystemId": null
}

```

Retrieves the details of an existing account email. You need only supply the account email id.

##### Arguments

* id (required) - The id of the account email to retrieve.

##### Returns

Returns an account email object if a valid id was provided.

#### Update an account email

```
DEFINITION
POST http://apiserver/accounts/:id/emails/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/emails/97426", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "97426",
    "account": "1483320",
    "accountName": "John Doe",
    "type": "HOME",
    "emailAddress": "home@example.com",
    "isPrimary": false,
    "isActive": false,
    "dataSource": null,
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Direct Mail"
    "optOutIndicator": true,
    "optOutReasonCode": "SPAM",
    "optOutReasonCodeDescription": "Spam Mail",
    "optOutDate": "2015-05-13",
    "dateLastSynced": null,
    "externalSystem": null,
    "externalSystemId": null
}


```

Updates the specified account email by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* account (optional) - Account to change the on the email.
* type (optional) - The email type. Must be a defined email type.
* emailAddress (optional) - The email address.
* isPrimary (optional) - Whether or not the email is the primary address for the account.
* isActive (optional) - Whether or not the email is active.
* dataSource (optional) - The data source of the email. If not specified, a default value will be set.
* functionalCategory (optional) - The functional category of this email.
* optOutIndicator (optional) - Whether or not the account has opted out of this email.
* optOutReasonCode (optional) - Reason the account has opted out of this email.
* optOutDate (optional) - Date the account has opted out of this email.

##### Returns

Returns the account email object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined email type or email type value).

#### Delete an account email

```
DEFINITION
DELETE http://apiserver/accounts/:id/emails/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/emails/97426", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account email. It cannot be undone.

##### Arguments

* id (required) - The id of the account email to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account email id does not exist, this call returns an error.

#### List all account emails

```
DEFINITION
GET http://apiserver/accounts/:id/emails

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/emails");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "97426",
            "account": "1483320",
            "accountName": "John Doe",
            "type": "HOME",
            "emailAddress": "home@example.com",
            "dateAdded": "2016-06-09",
            "isPrimary": false,
            "isActive": true,
            "dataSource": null,
            "functionalCategory": "DM",
            "functionalCategoryDescription": "Direct Mail"
            "optOutIndicator": true,
            "optOutReasonCode": "SPAM",
            "optOutReasonCodeDescription": "Spam Mail",
            "optOutDate": "2015-05-13",
            "dateLastSynced": null,
            "externalSystem": null,
            "externalSystemId": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account emails.

##### Returns

A dictionary with an items property that contains an array of up to limit account emails, starting at index offset. Each entry in the array is a separate account email object. If no more account emails are available, the resulting array will be empty. This request should never return an error.

#### Send a password reset email

```
DEFINITION
GET http://apiserver/accounts/:id/emails/:id/resetpassword?store=:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/emails/97426/resetpassword?store=19");

EXAMPLE RESPONSE
204 No Content

```

Sends a password reset email to the specified email address from the specified Advanced StudioOnline store.

##### Arguments

* id (required) - The id of the account email to retrieve.

##### Query Parameters

* store (required) - The Id of the Advanced StudioOnline store to send the password reset email from.

### Account Event Invitations

#### Create an account event invitation

```
DEFINITION
POST http://apiserver/accounts/:accountId/eventInvitations

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/40640/eventInvitations", {
    "eventCode": "10ATL1",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "account": "42640",
    "eventCode": "10ALT1",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
}

```

Create a new account event invitation

##### Arguments

* accountId (required) - the account number for the invitation
* eventCode (required) - the event code for the invitation.
* firstName (required) - first name on the invitation.
* lastName (required) - last name on the invitation.
* email (required) - email address on the invitation.
* registrationType (optional) - event registration type.
* status (required) - status on the event invitation.

##### Returns

Returns a event invitation object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account event invitation

```
DEFINITION
GET http://apiserver/accounts/:accountId/eventInvitations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/40640/eventInvitations/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "account": "40640",
    "eventCode": "10ATL1",
    "eventCodeDescription": "10ALT1 - Description",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "registrationTypeDescription": "REGTYPE Description",
    "status": "A"
}

```

Retrieves the details of an existing account event invitation.

##### Arguments

* accountId (required) - The account number on the invitation.
* id (required) - The id of the event invitation to be retrieved.

#### Update an account event invitation

```
DEFINITION
POST http://apiserver/accounts/:accountId/eventInvitations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/40640/eventInvitations/6", {
    "eventCode": "10ALT1",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "account": "40640",
    "eventCode": "10ALT1",
    "firstName": "John",
    "lastName": "Smith",
    "email": "john.smith@test.com",
    "registrationType": "REGTYPE",
    "status": "A"
}


```

Updates the specified account event invitation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - the unique identifier for the event invitation.
* eventCode - the event code for the invitation.
* accountId (required) - the account number on the invitation .
* firstName - first name on the invitation.
* lastName - last name on the invitation.
* email - email address on the invitation.
* registrationType - event registration type.
* status - status on the event invitation.

##### Returns

Returns the event invitation object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account event invitation

```
DEFINITION
DELETE http://apiserver/accounts/:accountId/eventInvitations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/42640/eventInvitations/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a Account's Event Invitation. It cannot be undone.

##### Arguments

* id (required) - The id of the event invitation to be deleted.
* accountId (required) - The account number for the invitation.

##### Returns

Returns a `204 No Content` response on success. If the event invitation does not exist, this call returns an error.

#### List all account event invitations

```
DEFINITION
GET http://apiserver/accounts/:accountId/eventInvitations

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/42640/eventInvitations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 9
    },
    "items": [
        {
            "id": "6",
            "account": "42640",
            "eventCode": "10ALT1",
            "eventCodeDescription": "10ALT1 - Description",
            "firstName": "John",
            "lastName": "Smith",
            "email": "john.smith@test.com",
            "registrationType": "REGTYPE",
            "registrationTypeDescription": "REGTYPE Description",
            "status": "A"
        },
        {...},
    ]
}

```

Returns a list of all event invitations by account number.

##### Arguments

* accountId (required) - The account number for the invitations.

##### Returns

A dictionary with an items property that contains an array of up to limit event invitations, starting at index offset. Each entry in the array is a separate event invitation object. If no more event invitations are available, the resulting array will be empty. This request should never return an error.

### Account Events Attended

#### List all account events attended

```
DEFINITION
GET http://apiserver/accounts/:id/eventsattended

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/eventsattended");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "date": "2013-11-20",
            "transaction": "184688",
            "event": "EVPAS2011",
            "eventDescription": "Passion 2011 Conference",
            "hasAttended": false,
            "quantity": 1,
            "status": "C",
            "priceCode": "I",
            "amount": 129,
            "source": "ABC08",
            "attendeeAccountNumber": "1483320",
            "attendeeAccountName": "Henry Winkler",
            "purchaserAccount": "1483320",
            "purchaserAccountName": "Henry Winkler",
            "shortComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account events attended.

##### Returns

A dictionary with an items property that contains an array of up to limit account events attended, starting at index offset. Each entry in the array is a separate account events attended object. If no more account events attended are available, the resulting array will be empty. This request should never return an error.

### Account Feedback Comments

#### Create an account feedback comment

```
DEFINITION
POST http://apiserver/accounts/:id/feedbackcomments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/feedbackcomments", {
    "date": "2014-01-07",
    "category": "POSITIVE",
    "comment": "It was great!"
});

EXAMPLE RESPONSE
{
    "id": "284",
    "date": "2014-01-07",
    "category": "POSITIVE",
    "subject": null,
    "topic": null,
    "isPrayerRequest": false,
    "isForCommentsReport": false,
    "comment": "It was great!"
}

```

Creates a new account feedback comment object.

##### Arguments

* date (optional) - The date of the feedback comment.
* category (optional) - The category code of the feedback comment. If provided, must be a defined feedback category code.
* subject (optional) - The subject code of the feedback comment. If provided, must be a defined feedback subject code.
* topic (optional) - The topic code of the feedback comment. If provided, must be a defined feedback topic code.
* isPrayerRequest (optional) - Whether or not the feedback comment is a prayer request. If not provided, will default to false.
* isForCommentsReport (optional) - Whether or not the feedback comment should be included in the comments report.
* comment (optional) - The comment of the feedback comment.

##### Returns

Returns an account feedback comment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined feedback comment type).

#### Retrieve an account feedback comment

```
DEFINITION
GET http://apiserver/accounts/:id/feedbackcomments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/feedbackcomments/284");

EXAMPLE RESPONSE
{
    "id": "284",
    "date": "2014-01-07",
    "category": "POSITIVE",
    "subject": null,
    "topic": null,
    "isPrayerRequest": false,
    "isForCommentsReport": false,
    "comment": "It was great!"
}

```

Retrieves the details of an existing account feedback comment. You need only supply the account feedback comment id.

##### Arguments

* id (required) - The id of the account feedback comment to retrieve.

##### Returns

Returns an account feedback comment object if a valid id was provided.

#### Update an account feedback comment

```
DEFINITION
POST http://apiserver/accounts/:id/feedbackcomments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/feedbackcomments/284", {
    "isForCommentsReport": true
});

EXAMPLE RESPONSE
{
    "id": "284",
    "date": "2014-01-07",
    "category": "POSITIVE",
    "subject": null,
    "topic": null,
    "isPrayerRequest": false,
    "isForCommentsReport": true,
    "comment": "It was great!"
}


```

Updates the specified account feedback comment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* date (optional) - The date of the feedback comment.
* category (optional) - The category code of the feedback comment. If provided, must be a defined feedback category code.
* subject (optional) - The subject code of the feedback comment. If provided, must be a defined feedback subject code.
* topic (optional) - The topic code of the feedback comment. If provided, must be a defined feedback topic code.
* isPrayerRequest (optional) - Whether or not the feedback comment is a prayer request. If not provided, will default to false.
* isForCommentsReport (optional) - Whether or not the feedback comment should be included in the comments report.
* comment (optional) - The comment of the feedback comment.

##### Returns

Returns the account feedback comment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined feedback comment type or feedback comment type value).

#### Delete an account feedback comment

```
DEFINITION
DELETE http://apiserver/accounts/:id/feedbackcomments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/feedbackcomments/284", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account feedback comment. It cannot be undone.

##### Arguments

* id (required) - The id of the account feedback comment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account feedback comment id does not exist, this call returns an error.

#### List all account feedback comments

```
DEFINITION
GET http://apiserver/accounts/:id/feedbackcomments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/feedbackcomments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "284",
            "date": "2014-01-07",
            "category": "POSITIVE",
            "subject": null,
            "topic": null,
            "isPrayerRequest": false,
            "isForCommentsReport": false,
            "comment": "It was great!"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account feedback comments.

##### Returns

A dictionary with an items property that contains an array of up to limit account feedback comments, starting at index offset. Each entry in the array is a separate account feedback comment object. If no more account feedback comments are available, the resulting array will be empty. This request should never return an error.

### Account First Contacts

#### List all account first contacts

```
DEFINITION
GET http://apiserver/accounts/:id/firstcontacts

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/firstcontacts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "company": "010",
            "source": "AD1D2234A",
            "description": null,
            "date": "2011-06-26"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account first contacts.

##### Returns

A dictionary with an items property that contains an array of up to limit account first contacts, starting at index offset. Each entry in the array is a separate account first contact object. If no more account first contacts are available, the resulting array will be empty. This request should never return an error.

### Account Giving Plans

#### Create an account giving plan

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans", {
    "representative": "RAP001",
    "source": "ABC08"
});

EXAMPLE RESPONSE
{
    "id": "23832802",
    "representative": "RAP001",
    "source": "ABC08",
    "description": null,
    "isActive": true,
    "type": null,
    "date": "2014-01-10",
    "redeemDate": "2014-01-10",
    "estimatedValue": 0,
    "cashValue": 0,
    "frequency": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null
}

```

Creates a new account giving plan object.

##### Arguments

* representative (required) - The representative code of the account giving plan. Must be a defined giving plan representative code.
* source (required) - The source code of the account giving plan. Must be a defined source code.
* description (optional) - The description of the account giving plan.
* isActive (optional) - Whether or not the account giving plan is active.
* type (optional) - The type of the account giving plan. If specified, must be a defined giving plan type.
* date (optional) - The plan date of the account giving plan.
* redeemDate (optional) - The redeem date of the account giving plan.
* estimatedValue (optional) - The estimated value of the account giving plan.
* cashValue (optional) - The cash value of the account giving plan.
* frequency (optional) - The frequency of the account giving plan. If specified, must be a defined recurring transaction frequency.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.

##### Returns

Returns an account giving plan object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined plan type).

#### Retrieve an account giving plan

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802");

EXAMPLE RESPONSE
{
    "id": "23832802",
    "representative": "RAP001",
    "source": "ABC08",
    "description": null,
    "isActive": true,
    "type": null,
    "date": "2014-01-10",
    "redeemDate": "2014-01-10",
    "estimatedValue": 0,
    "cashValue": 0,
    "frequency": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null
}

```

Retrieves the details of an existing account giving plan. You need only supply the account giving plan id.

##### Arguments

* id (required) - The id of the account giving plan to retrieve.

##### Returns

Returns an account giving plan object if a valid id was provided.

#### Update an account giving plan

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802", {
    "description": "giving plan"
});

EXAMPLE RESPONSE
{
    "id": "23832802",
    "representative": "RAP001",
    "source": "ABC08",
    "description": "giving plan",
    "isActive": true,
    "type": null,
    "date": "2014-01-10",
    "redeemDate": "2014-01-10",
    "estimatedValue": 0,
    "cashValue": 0,
    "frequency": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null
}


```

Updates the specified account giving plan by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* representative (optional) - The representative code of the account giving plan. Must be a defined giving plan representative code.
* source (optional) - The source code of the account giving plan. Must be a defined source code.
* description (optional) - The description of the account giving plan.
* isActive (optional) - Whether or not the account giving plan is active.
* type (optional) - The type of the account giving plan. If specified, must be a defined giving plan type.
* date (optional) - The plan date of the account giving plan.
* redeemDate (optional) - The redeem date of the account giving plan.
* estimatedValue (optional) - The estimated value of the account giving plan.
* cashValue (optional) - The cash value of the account giving plan.
* frequency (optional) - The frequency of the account giving plan. If specified, must be a defined frequency code.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.

##### Returns

Returns the account giving plan object if the update succeeded. Returns an error if update parameters are invalid (e.g. changing representative to an undefined giving plan representative code).

#### Delete an account giving plan

```
DEFINITION
DELETE http://apiserver/accounts/:id/givingplans/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/givingplans/23832802", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account giving plan. It cannot be undone.

##### Arguments

* id (required) - The id of the account giving plan to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account giving plan id does not exist, this call returns an error.

#### List all account giving plans

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 15
    },
    "items": [
        {
            "id": "23832802",
            "representative": "RAP001",
            "source": "ABC08",
            "description": null,
            "isActive": true,
            "type": null,
            "date": "2014-01-10",
            "redeemDate": "2014-01-10",
            "estimatedValue": 0,
            "cashValue": 0,
            "frequency": null,
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account giving plans.

##### Returns

A dictionary with an items property that contains an array of up to limit account giving plans, starting at index offset. Each entry in the array is a separate account giving plan object. If no more account giving plans are available, the resulting array will be empty. This request should never return an error.

### Account Giving Plan Attachments

#### Create an account giving plan attachment

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new account giving plan attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns an account giving plan attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve an account giving plan attachment

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing account giving plan attachment. You need only supply the account giving plan attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns an account giving plan attachment object if a valid id was provided.

#### Update an account giving plan attachment

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified account giving plan attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the account giving plan attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined account giving plan attachment type code).

#### Delete an account giving plan attachment

```
DEFINITION
DELETE http://apiserver/accounts/:id/givingplans/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/givingplans/23832802/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account giving plan attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the account giving plan attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account giving plan attachment id does not exist, this call returns an error.

#### List all account giving plan attachments

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account giving plan attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit account giving plan attachments, starting at index offset. Each entry in the array is a separate account giving plan attachment object. If no more account giving plan attachments are available, the resulting array will be empty. This request should never return an error.

### Account Giving Plan Codes

#### Create an account giving plan code

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/codes", {
    "type": "PLGFUND",
    "value": "110500"
});

EXAMPLE RESPONSE
{
    "id": "540",
    "type": "PLGFUND",
    "value": "110500",
    "isActive": true
}

```

Creates a new account giving plan code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an account giving plan code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve an account giving plan code

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/codes/540");

EXAMPLE RESPONSE
{
    "id": "540",
    "type": "PLGFUND",
    "value": "110500",
    "isActive": true
}

```

Retrieves the details of an existing account giving plan code. You need only supply the account giving plan code id.

##### Arguments

* id (required) - The id of the account giving plan code to retrieve.

##### Returns

Returns an account giving plan code object if a valid id was provided.

#### Update an account giving plan code

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/codes/540", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "540",
    "type": "PLGFUND",
    "value": "110500",
    "isActive": false
}


```

Updates the specified account giving plan code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the account giving plan code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete an account giving plan code

```
DEFINITION
DELETE http://apiserver/accounts/:id/givingplans/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/givingplans/23832802/codes/540", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account giving plan code. It cannot be undone.

##### Arguments

* id (required) - The id of the account giving plan code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account giving plan code id does not exist, this call returns an error.

#### List all account giving plan codes

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "540",
            "type": "PLGFUND",
            "value": "110500",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account giving plan codes.

##### Returns

A dictionary with an items property that contains an array of up to limit account giving plan codes, starting at index offset. Each entry in the array is a separate account giving plan code object. If no more account giving plan codes are available, the resulting array will be empty. This request should never return an error.

### Account Giving Plan Dates

#### Create an account giving plan date

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/dates", {
    "type": "DDCPLGDT1",
    "value": "2014-07-26"
});

EXAMPLE RESPONSE
{
    "id": "958",
    "type": "DDCPLGDT1",
    "value": "2014-07-26",
    "isActive": true
}

```

Creates a new account giving plan date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an account giving plan date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve an account giving plan date

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/dates/958");

EXAMPLE RESPONSE
{
    "id": "958",
    "type": "DDCPLGDT1",
    "value": "2014-07-26",
    "isActive": true
}

```

Retrieves the details of an existing account giving plan date. You need only supply the account giving plan date id.

##### Arguments

* id (required) - The id of the account giving plan date to retrieve.

##### Returns

Returns an account giving plan date object if a valid id was provided.

#### Update an account giving plan date

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/dates/958", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "958",
    "type": "DDCPLGDT1",
    "value": "2014-07-26",
    "isActive": false
}


```

Updates the specified account giving plan date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the account giving plan date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete an account giving plan date

```
DEFINITION
DELETE http://apiserver/accounts/:id/givingplans/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/givingplans/23832802/dates/958", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account giving plan date. It cannot be undone.

##### Arguments

* id (required) - The id of the account giving plan date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account giving plan date id does not exist, this call returns an error.

#### List all account giving plan dates

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "958",
            "type": "DDCPLGDT1",
            "value": "2014-07-26",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account giving plan dates.

##### Returns

A dictionary with an items property that contains an array of up to limit account giving plan dates, starting at index offset. Each entry in the array is a separate account giving plan date object. If no more account giving plan dates are available, the resulting array will be empty. This request should never return an error.

### Account Giving Plan Notes

#### Create an account giving plan note

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/notes", {
    "type": "DDCPLGNT",
    "shortComment": "Plan Reminder"
});

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCPLGNT",
    "shortComment": "Plan Reminder",
    "longComment": null
}

```

Creates a new account giving plan note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns an account giving plan note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve an account giving plan note

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/notes/31884");

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCPLGNT",
    "shortComment": "Plan Reminder",
    "longComment": null
}

```

Retrieves the details of an existing account giving plan note. You need only supply the account giving plan note id.

##### Arguments

* id (required) - The id of the account giving plan note to retrieve.

##### Returns

Returns an account giving plan note object if a valid id was provided.

#### Update an account giving plan note

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/notes/31884", {
    "shortComment": null,
    "longComment": "Plan Reminder"
});

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCPLGNT",
    "shortComment": null,
    "longComment": "Plan Reminder"
}


```

Updates the specified account giving plan note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the account giving plan note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete an account giving plan note

```
DEFINITION
DELETE http://apiserver/accounts/:id/givingplans/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/givingplans/23832802/notes/31884", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account giving plan note. It cannot be undone.

##### Arguments

* id (required) - The id of the account giving plan note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account giving plan note id does not exist, this call returns an error.

#### List all account giving plan notes

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "31884",
            "type": "DDCPLGNT",
            "shortComment": "Plan Reminder",
            "longComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account giving plan notes.

##### Returns

A dictionary with an items property that contains an array of up to limit account giving plan notes, starting at index offset. Each entry in the array is a separate account giving plan note object. If no more account giving plan notes are available, the resulting array will be empty. This request should never return an error.

### Account Giving Plan Numbers

#### Create an account giving plan number

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/numbers", {
    "type": "DDCPLGNR1",
    "value": 33
});

EXAMPLE RESPONSE
{
    "id": "3328",
    "type": "DDCPLGNR1",
    "value": 33,
    "isActive": true
}

```

Creates a new account giving plan number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an account giving plan number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve an account giving plan number

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/numbers/3328");

EXAMPLE RESPONSE
{
    "id": "3328",
    "type": "DDCPLGNR1",
    "value": 33,
    "isActive": true
}

```

Retrieves the details of an existing account giving plan number. You need only supply the account giving plan number id.

##### Arguments

* id (required) - The id of the account giving plan number to retrieve.

##### Returns

Returns an account giving plan number object if a valid id was provided.

#### Update an account giving plan number

```
DEFINITION
POST http://apiserver/accounts/:id/givingplans/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/givingplans/23832802/numbers/3328", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "3328",
    "type": "DDCPLGNR1",
    "value": 33,
    "isActive": false
}


```

Updates the specified account giving plan number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the account giving plan number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete an account giving plan number

```
DEFINITION
DELETE http://apiserver/accounts/:id/givingplans/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/givingplans/23832802/numbers/3328", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account giving plan number. It cannot be undone.

##### Arguments

* id (required) - The id of the account giving plan number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account giving plan number id does not exist, this call returns an error.

#### List all account giving plan numbers

```
DEFINITION
GET http://apiserver/accounts/:id/givingplans/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/givingplans/23832802/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3328",
            "type": "DDCPLGNR1",
            "value": 33,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account giving plan numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit account giving plan numbers, starting at index offset. Each entry in the array is a separate account giving plan number object. If no more account giving plan numbers are available, the resulting array will be empty. This request should never return an error.

### Account Images

#### Create an account image

```
DEFINITION
POST http://apiserver/accounts/:id/images

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/images", {
    "type": "PIC",
    "fileName": "Old DonorDirect Logo.png",
    "imageMimeType": "image/png",
    "image":"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",
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "PIC",
    "typeDescription": "Account Picture",
    "fileName": "Old DonorDirect Logo.png",
    "image": null,
    "imageMimeType": "image/png",
    "thumbnailImage": "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",
    "thumbnailImageMimeType": "image/jpeg",
    "isPrimary": true
}

```

Creates a new account image object.

##### Arguments

* type (required) - The image type code. (Must be a defined account image code type value of `DDCACCIMG` code type.)
* fileName (required) - The name of the image that is being uploaded to StudioEnterprise. (Max length of 200 characters.)
* image (required) - The base64 encoded string of the image contents. (A 64px/64px jpeg thumbnail will be attempted to be created from this image.)
* imageMimeType (required) - The mime type of the image that is being uploaded to StudioEnterprise.
* isPrimary (optional) - Whether this image is the primary image (`true`/`false`). The default is `false`.

##### Returns

Returns an account image object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined image type or not specifying an image).

#### Retrieve an account image

```
DEFINITION
GET http://apiserver/accounts/:id/images/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/images/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "PIC",
    "typeDescription": "Account Picture",
    "fileName": "Old DonorDirect Logo.png",
    "image": null,
    "imageMimeType": "image/png",
    "thumbnailImage": "/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCABAAEADASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwDgLDRrK30mxb7PG8srRs7soJOcEjntV2XTbXdf4s4PlhBH7sccNWlp9k8+kadsGSBCx57ADNab6XK5vyqD97CFTnqcN/iK86ddJ6s+bUak223/AFdGBp2nWZvtID2cBVwdwMQ+b90TzxXWroulsf8AkG2f/fhf8Ky1tWtr7REcYZSyt9RE1dNCOa87F1W5Jp9P1Z95w5BLBPm195/oQR6BpR/5hln/AN+F/wAKlPh7Ssf8guz/APAdf8K1YFFWnjUJXnOtO+567Ub7HFX1rodnMYpNJywGcxaY8i/99KhH61z/AIgtNAvdGulXTJ4ZkjZo5U0yWMqwGRk7Bx654rur6K+aUm3ubaOPH3ZLdnP5hx/KsDWYtSGkX2+7tCv2eTIFqwJG0/8ATSu2hU1Tu7+v/AInDmhJcqt6f8ENAUf2RY/9cE/9BFdFFEpSuX0KYDSbIZ/5YJ/6CK3UusL1rTEQk5Ox+b05xuyvqmn214EEysfLbchV2Ug4x1BHY15H4svLzTvEM9taX13FCqqQouH4yo967LUfiLpdteXFq9veGSGRo2IRcEg44+bpxXmuuan/AGxrE97s2LIQFU9QAMD+VehgqM4/GtDvwvtYz6qJ6t8Kr+5udEvHurmWZhc4DSuWIG0cc122p6qunadNdujSLEM7Fxk847187aP4h1TQXkbTroxCT76lQyt+BrYXxzr+pyRWVzdI0M0iK6iJRkbh3xWFXLJVcRz6crZ9LQzCnGioO/Md/d+IbC9lMs/hxpZCMb5FhY/mTWVqOoac+m3YTw4sbGFwH2Q/KcHng1ObU4qjqMZTT7n/AK5N/I19AslwsV7t9PMbxFSz/wAkXtKlZNMtMf8APFP/AEEVpC8IFc7p9tdPYWu3UJVBiXAEaccD2rVi0i5kHOpz/wDfuP8A+JrGWUV3rZfefnTUlJ2kvx/yOEvfC+r6jqV5eW9urRS3MpUmRRn5z71kalomoaRs+225jV/usGBB/EV7ZYaZ9ktFhDtJgsxdgMkkknp9a5f4hWU0uiQLBBJK4uVJCIWIG1vSvRngoQo31ukepQx85VFB2secaTYHU9ThtA20OTlsdABk/wAq7+x8BadHPFOJ7svGwcAsuCQc/wB2uU8NwXFhrkM91bXEUShssYW7g+1eo6Xf212rGFy2w7WBUqQcZ6EVlQpx5byWp79D2cl5lhrTC9KxdZh26bd/9cX/AJGuoklQx4rntcYHTLz/AK4v/wCgmupN2Z1PYwNOhtzZ2xbR95MS5bZFzwOeWrotMit0uFZNI+zt/wA9dkQx/wB8sTXK6Rf20+mwH+1midECtGxjBUgY7r0rcs9RtYnDPrKuB/A8kWD+QB/WuuLg4pr9D4mampSi/wBTtYZUCc1TumBJxWUuuafj/j/tv+/y/wCNRS63YEf8f1sf+2q/41acb7mPJLsJdkZqhpspivb/ALZkUj/vhaSXVLJ2/wCPy3/7+r/jWct/areXJF3DglcHzBz8opV3FxSv1PSyZNYq7XRmrbarPLYaVI7gvcKplOOuY2Y/TkCqmoXbS2epoxyEDKv08sH+ZNZVrfwCw0lTcxAoq7gXHH7phzUN9qtpBa6hmdHeRiqKjAk5jUflXFeKjdv+rH1HMrav+rH/2Q==",
    "thumbnailImageMimeType": "image/jpeg",
    "isPrimary": true
}

```

Retrieves the details of an existing account image. You need only supply the account image id.

##### Arguments

* id (required) - The id of the account image to retrieve.
* download (optional) - `download=true` will force the `image` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns an account image object if a valid id was provided.

#### Update an account image

```
DEFINITION
POST http://apiserver/accounts/:id/images/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/images/6", {
    "fileName": "DonorDirect Logo.png",
    "image":"iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAIAAAAlC+aJAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH5AMTEysJVcEpcQAAA0BJREFUaN7tmVtIVEEYgOdyzt5320tr4bZqSxprlBZmWz101cR6iCgkekkKoqRIqxcRgkAiIro8RGQ9hUJGgVFpBF2M1oduSGXbTYnUKNvdQtN1zzkzPSmlua7irE6deTqcc2bm/37+/5///wdSSgHPQ0jYTgdb7vlDHbH/oQAYsGgVtRZB4zU5fDaXS2dK1pn0WJh8gEBPqCncOeZplAJKi9yZVQsKzIJm+Hc01U0EQoDQ5Y6AteF0RaCRQ4CBQSitfOPf9uwGrwAAAIBQzacX1e0t3AIAABDe0VxPfoucvAEA0E/kdz/DHAMAAI+89XMNAGo7A3wDyESWKeEYAAAgEc4BCKB8A/DtAyrA1KwH7j96vWn7qXjmaLWiXis67Ka0FKcnJSl3kacwL1uv00wygCAgi1kff27YFezuCnY/ft5afc2/s/TC7uK1h0rW26xG/kxIwGiaxVBz1Z+9qvxD21eOfQBCmLflaDDcw7ETE0J96w4rCuE4CkUlpenJe44BIARnzjfwfQ7caXzJN4CIccfnEMcACKNvoR6eASDsi0T5zoUoSVDLdTytxdkpTrvNBMCIIkqSYjbphrz0mhzhaCTGshjCh6H2RAAc2FO4IX/hWGcdz1w5egi+fgxAyNyEZFlR6wEV4B+syOIfrR+7nja3xbibIpR605PNpj/Ko5buYEjqi7GsEYsJAjh5rv7E2VuxEtKoXHepdFluxu8vy17dvf1ltCwV4UQAYIxwzI0opXBYNBQQGod8qhOrACqACqACqAAqgAqgAqgA/yEARJCp3JApAKFUp2V7ZSZAxBKAEIeN7WWZZqA2YgIgSYrb5WAnfbZ1JlsfWLHUy1L7tMyzmC3A/l0FLK0fb3V5GQJgjJb7Mphpn+Y70wY9eOIBKKUP6ipEATOSP0lnvLlkM6tzACF45eK+Wcl2Rsp3aPSdeSVDLWpiwo6s+HLm1FbtxZjNyUjkyszV5em+v7jE4JOi0N7e/rhUAQCllBCalurMyfIUbfRlzXNPt5tjz4ooMpCl+JYHAFAA0VzLjDXO1GL3fK/ZMVLjEQ62OKOS/P1HbzwAoog1omA0aMekxLAUiShxXSxoEdZhbIivVfoLrMX956FHg1QAAAAASUVORK5CYII="
});

EXAMPLE RESPONSE
{
    "id": "6",
    "type": "PIC",
    "typeDescription": "Account Picture",
    "fileName": "DonorDirect Logo.png",
    "image": null,
    "imageMimeType": "image/png",
    "thumbnailImage": "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",
    "thumbnailImageMimeType": "image/jpeg",
    "isPrimary": true
}


```

Updates the specified account image by setting the values of the parameters passed. Any parameters not provided will be left unchanged (except for thumbmailImage, see below).

##### Arguments

* type (optional) - The image type code. (Must be a defined account image code type value of `DDCACCIMG` code type.)
* fileName (optional) - The name of the image that is being uploaded to StudioEnterprise. (Max length of 200 characters.)
* image (optional) - The base64 encoded string of the image contents. (A 64px/64px jpeg thumbnail will be attempted to be created from this image.)
* imageMimeType (optional) - The mime type of the image that is being uploaded to StudioEnterprise. (If the image type is changed, a new `imageMimeType` would need to be included.)
* isPrimary (optional) - Whether this image is the primary image (`true`/`false`).

##### Returns

Returns the account image object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined account image type code).

#### Delete an account image

```
DEFINITION
DELETE http://apiserver/accounts/:id/images/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/images/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account image. It cannot be undone.

##### Arguments

* id (required) - The id of the image to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account images id does not exist, this call returns an error.

#### List all account images

```
DEFINITION
GET http://apiserver/accounts/:id/images

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/images");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "6",
            "type": "PIC",
            "typeDescription": "Account Picture",
            "fileName": "DonorDirect Logo.png",
            "image": null,
            "imageMimeType": "image/png",
            "thumbnailImage": "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",
            "thumbnailImageMimeType": "image/jpeg",
            "isPrimary": true
        ,
        {...},
        {...}
    ]
}

```

Returns a list of all account images.

##### Arguments

* type (optional) - The image type code by which to filter.
* isPrimary (optional) - Whether to return primary or non-primary account images (`true`/`false`), or do not include argument to return both.

##### Returns

A dictionary with an items property that contains an array of up to limit account images, starting at index offset. Each entry in the array is a separate account image object. If no more account images are available, the resulting array will be empty. This request should never return an error.

### Account Interactions

#### List all account interactions

```
DEFINITION
GET http://apiserver/accounts/:id/interactions

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/interactions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "date": "2013-11-20",
            "account": "1483320",
            "name": "Henry Winkler",
            "transaction": "184688",
            "isInbound": false,
            "letter": "CHURCH",
            "type": "RECEIPT",
            "description": "Receipt for document: 184688",
            "originatingAccount": "1483320",
            "originatingName": "Henry Winkler"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account interactions.

##### Returns

A dictionary with an items property that contains an array of up to limit account interactions, starting at index offset. Each entry in the array is a separate account interaction object. If no more account interactions are available, the resulting array will be empty. This request should never return an error.

### Account Marketing Attributes

#### Create an account marketing attribute

```
DEFINITION
POST http://apiserver/accounts/:id/marketingattributes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingattributes", {
    "attributeType": "TRACK",
    "attributeValue": "2",
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "12",
    "attributeType": "TRACK",
    "attributeTypeDescription": "Donor Track",
    "attributeValue": "2",
    "attributeValueDescription": "Track 2",
    "lastUpdated": "2016-04-27T09:45:20 AM",
    "dataSource": "DDC"
}

```

Creates a new account marketing attribute.

##### Arguments

* attributeType (required) - The type of marketing attribute; must be a valid type (see `GET /datatypes/CODETYPE/values?category=ACCTMKATTR` for valid types)
* attributeValue (required) - The value of the marketing attribute; must be a valid value for the `attributeType` (see `GET /datatypes/:attributeType/values` for valid values)
* dataSource (optional) - The source from which the marketing attribute is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns an account marketing attribute object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account marketing attribute

```
DEFINITION
GET http://apiserver/accounts/:id/marketingattributes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingattributes/12");

EXAMPLE RESPONSE
{
    "id": "12",
    "attributeType": "TRACK",
    "attributeTypeDescription": "Donor Track",
    "attributeValue": "2",
    "attributeValueDescription": "Track 2",
    "lastUpdated": "2016-04-27T09:46:20 AM",
    "dataSource": "DDC"
}

```

Retrieves the details of an existing account marketing attribute. You need only supply the id.

##### Arguments

* id (required) - The id of the account marketing attribute to be retrieved.

#### Update an account marketing attribute

```
DEFINITION
POST http://apiserver/accounts/:id/marketingattributes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingattributes/12", {
    "attributeValue": "1",
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "12",
    "attributeType": "TRACK",
    "attributeTypeDescription": "Donor Track",
    "attributeValue": "1",
    "attributeValueDescription": "Track 1",
    "dataSource": "DDC"
}


```

Updates the specified account marketing attribute by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* attributeType - The type of marketing attribute; must be a valid type (see `GET /datatypes/CODETYPE/values?category=ACCTMKATTR` for valid types)
* attributeValue - The value of the marketing attribute; must be a valid value for the `attributeType` (see `GET /datatypes/:attributeType/values` for valid values)
* dataSource - The source from which the marketing attribute is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns the account marketing attribute object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account marketing attribute

```
DEFINITION
DELETE http://apiserver/accounts/:id/marketingattributes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16234/marketingattributes/12", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account marketing attribute. It cannot be undone.

##### Arguments

* id (required) - The id of the account marketing attribute to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the account marketing attribute does not exist, this call returns an error.

#### List all account marketing attributes

```
DEFINITION
GET http://apiserver/accounts/:id/marketingattributes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingattributes?attributeType=TRACK");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "12",
            "attributeType": "TRACK",
            "attributeTypeDescription": "Donor Track",
            "attributeValue": "1",
            "attributeValueDescription": "Track 1",
            "lastUpdated": "2016-04-27T09:46:20 AM",
            "dataSource": "DDC"
        },
        {...},
    ]
}

```

Returns a list of all account marketing attributes.

##### Arguments

* attributeType (optional) - filters results on partial match

##### Returns

A dictionary with an items property that contains an array of up to limit account marketing attributes, starting at index offset. Each entry in the array is a separate account marketing attribute object. If no more account marketing attributes are available, the resulting array will be empty. This request should never return an error.

### Account Marketing Dates

#### Create an account marketing date

```
DEFINITION
POST http://apiserver/accounts/:id/marketingdates

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingdates", {
    "dateType": "LSTCONTACT",
    "dateValue": "2016-05-28"
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "dateType": "LSTCONTACT",
    "dateTypeDescription": "Last Contact Date",
    "dateValue": "2016-05-28",
    "lastUpdated": "2016-06-10T03:48:12 PM",
    "dataSource": "DDC"
}

```

Creates a new account marketing date.

##### Arguments

* dateType (required) - The type of marketing date; must be a valid type (see `GET /datatypes/DATETYPE/values?category=ACCTMKATTR` for valid types)
* dateValue (required) - The value of the marketing date; must be a valid value for the `dateType` (see `GET /datatypes/:dateType/values` for valid values)
* dataSource (optional) - The source from which the marketing date is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns an account marketing date object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account marketing date

```
DEFINITION
GET http://apiserver/accounts/:id/marketingdates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingdates/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "dateType": "LSTCONTACT",
    "dateTypeDescription": "Last Contact Date",
    "dateValue": "2016-05-28",
    "lastUpdated": "2016-06-10T03:48:12 PM",
    "dataSource": "DDC"
}

```

Retrieves the details of an existing account marketing date. You need only supply the id.

##### Arguments

* id (required) - The id of the account marketing date to be retrieved.

#### Update an account marketing date

```
DEFINITION
POST http://apiserver/accounts/:id/marketingdates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingdates/3", {
    "dateValue": "2016-06-09",
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "3",
    "dateType": "LSTCONTACT",
    "dateTypeDescription": "Last Contact Date",
    "dateValue": "2016-06-09",
    "lastUpdated": "2016-06-10T03:51:52 PM",
    "dataSource": "DDC"
}


```

Updates the specified account marketing date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* dateType - The type of marketing date; must be a valid type (see `GET /datatypes/DATETYPE/values?category=ACCTMKATTR` for valid types)
* dateValue - The value of the marketing date; must be a valid value for the `dateType` (see `GET /datatypes/:dateType/values` for valid values)
* dataSource - The source from which the marketing date is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns the account marketing date object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account marketing date

```
DEFINITION
DELETE http://apiserver/accounts/:id/marketingdates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16234/marketingdates/3", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account marketing date. It cannot be undone.

##### Arguments

* id (required) - The id of the account marketing date to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the account marketing date does not exist, this call returns an error.

#### List all account marketing dates

```
DEFINITION
GET http://apiserver/accounts/:id/marketingdates

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingdates?dateType=LSTCONTACT");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "dateType": "LSTCONTACT",
            "dateTypeDescription": "Last Contact Date",
            "dateValue": "2016-06-09",
            "lastUpdated": "2016-06-10T03:51:52 PM",
            "dataSource": "DDC"
        },
        {...},
    ]
}

```

Returns a list of all account marketing dates.

##### Arguments

* dateType (optional) - filters results on partial match

##### Returns

A dictionary with an items property that contains an array of up to limit account marketing dates, starting at index offset. Each entry in the array is a separate account marketing date object. If no more account marketing dates are available, the resulting array will be empty. This request should never return an error.

### Account Marketing Notes

#### Create an account marketing note

```
DEFINITION
POST http://apiserver/accounts/:id/marketingnotes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingnotes", {
    "noteType": "MKTNOTE",
    "noteValue": "He enjoys attending baseball games with his family.",
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "noteType": "MKTNOTE",
    "noteTypeDescription": "Marketing note",
    "noteValue": "He enjoys attending baseball games with his family.",
    "lastUpdated": "2016-06-10T03:59:19 PM",
    "dataSource": "DDC"
}

```

Creates a new account marketing note.

##### Arguments

* noteType (required) - The type of marketing note; must be a valid type (see `GET /datatypes/NOTETYPE/values?category=ACCTMKATTR` for valid types)
* noteValue (required) - The value of the marketing note; must be a valid value for the `noteType` (see `GET /datatypes/:noteType/values` for valid values)
* dataSource (optional) - The source from which the marketing note is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns an account marketing note object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account marketing note

```
DEFINITION
GET http://apiserver/accounts/:id/marketingnotes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingnotes/6");

EXAMPLE RESPONSE
{
    "id": "6",
    "noteType": "MKTNOTE",
    "noteTypeDescription": "Marketing note",
    "noteValue": "He enjoys attending baseball games with his family.",
    "lastUpdated": "2016-06-10T03:59:19 PM",
    "dataSource": "DDC"
}

```

Retrieves the details of an existing account marketing note. You need only supply the id.

##### Arguments

* id (required) - The id of the account marketing note to be retrieved.

#### Update an account marketing note

```
DEFINITION
POST http://apiserver/accounts/:id/marketingnotes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingnotes/6", {
    "noteValue": "He enjoys attending football games with his family.",
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "6",
    "noteType": "MKTNOTE",
    "noteTypeDescription": "Marketing note",
    "noteValue": "He enjoys attending football games with his family.",
    "lastUpdated": "2016-06-10T04:03:00 PM",
    "dataSource": "DDC"
}


```

Updates the specified account marketing note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* noteType - The type of marketing note; must be a valid type (see `GET /datatypes/NOTETYPE/values?category=ACCTMKATTR` for valid types)
* noteValue - The value of the marketing note; must be a valid value for the `noteType` (see `GET /datatypes/:noteType/values` for valid values)
* dataSource - The source from which the marketing note is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns the account marketing note object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account marketing note

```
DEFINITION
DELETE http://apiserver/accounts/:id/marketingnotes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16234/marketingnotes/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account marketing note. It cannot be undone.

##### Arguments

* id (required) - The id of the account marketing note to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the account marketing note does not exist, this call returns an error.

#### List all account marketing notes

```
DEFINITION
GET http://apiserver/accounts/:id/marketingnotes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingnotes?noteType=MKTNOTE");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "6",
            "noteType": "MKTNOTE",
            "noteTypeDescription": "Marketing note",
            "noteValue": "He enjoys attending football games with his family.",
            "lastUpdated": "2016-06-10T04:03:00 PM",
            "dataSource": "DDC"
        },
        {...},
    ]
}

```

Returns a list of all account marketing notes.

##### Arguments

* noteType (optional) - filters results on partial match

##### Returns

A dictionary with an items property that contains an array of up to limit account marketing notes, starting at index offset. Each entry in the array is a separate account marketing note object. If no more account marketing notes are available, the resulting array will be empty. This request should never return an error.

### Account Marketing Numbers

#### Create an account marketing number

```
DEFINITION
POST http://apiserver/accounts/:id/marketingnumbers

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingnumbers", {
    "numberType": "LSTGIFTAMT",
    "numberValue": 250,
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "7",
    "numberType": "LSTGIFTAMT",
    "numberTypeDescription": "Amount of last gift",
    "numberValue": 250,
    "lastUpdated": "2016-06-10T04:05:40 PM",
    "dataSource": "DDC"
}

```

Creates a new account marketing number.

##### Arguments

* numberType (required) - The type of marketing number; must be a valid type (see `GET /datatypes/NUMBERTYPE/values?category=ACCTMKATTR` for valid types)
* numberValue (required) - The value of the marketing number; must be a valid value for the `numberType` (see `GET /datatypes/:numberType/values` for valid values)
* dataSource (optional) - The source from which the marketing number is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns an account marketing number object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account marketing number

```
DEFINITION
GET http://apiserver/accounts/:id/marketingnumbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingnumbers/7");

EXAMPLE RESPONSE
{
    "id": "7",
    "numberType": "LSTGIFTAMT",
    "numberTypeDescription": "Amount of last gift",
    "numberValue": 250,
    "lastUpdated": "2016-06-10T04:05:40 PM",
    "dataSource": "DDC"
}

```

Retrieves the details of an existing account marketing number. You need only supply the id.

##### Arguments

* id (required) - The id of the account marketing number to be retrieved.

#### Update an account marketing number

```
DEFINITION
POST http://apiserver/accounts/:id/marketingnumbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/marketingnumbers/7", {
    "numberValue": 325,
    "dataSource": "DDC"
});

EXAMPLE RESPONSE
{
    "id": "7",
    "numberType": "LSTGIFTAMT",
    "numberTypeDescription": "Amount of last gift",
    "numberValue": 325,
    "lastUpdated": "2016-06-10T04:06:58 PM",
    "dataSource": "DDC"
}


```

Updates the specified account marketing number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* numberType - The type of marketing number; must be a valid type (see `GET /datatypes/NUMBERTYPE/values?category=ACCTMKATTR` for valid types)
* numberValue - The value of the marketing number; must be a valid value for the `numberType` (see `GET /datatypes/:numberType/values` for valid values)
* dataSource - The source from which the marketing number is being set. If it is not populated, it will be set to DDC.

##### Returns

Returns the account marketing number object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account marketing number

```
DEFINITION
DELETE http://apiserver/accounts/:id/marketingnumbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16234/marketingnumbers/7", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account marketing number. It cannot be undone.

##### Arguments

* id (required) - The id of the account marketing number to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the account marketing number does not exist, this call returns an error.

#### List all account marketing numbers

```
DEFINITION
GET http://apiserver/accounts/:id/marketingnumbers

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/marketingnumbers?numberType=LSTGIFTAMT");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7",
            "numberType": "LSTGIFTAMT",
            "numberTypeDescription": "Amount of last gift",
            "numberValue": 325,
            "lastUpdated": "2016-06-10T04:06:58 PM",
            "dataSource": "DDC"
        },
        {...},
    ]
}

```

Returns a list of all account marketing numbers.

##### Arguments

* numberType (optional) - filters results on partial match

##### Returns

A dictionary with an items property that contains an array of up to limit account marketing numbers, starting at index offset. Each entry in the array is a separate account marketing number object. If no more account marketing numbers are available, the resulting array will be empty. This request should never return an error.

### Account Merges

#### Create an account merge

```
DEFINITION
POST http://apiserver/accounts/:id/merges

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/120003/merges", {
    "mergedAccount": "120007"
});

EXAMPLE RESPONSE
{
    "id": "1000123374",
    "mergedAccount": "120007",
    "date": "1/19/2015 12:00:00 AM",
    "shortComment": null,
    "type": "I",
    "familyId": "0",
    "memberType": null,
    "mergedFirstName": "Steven",
    "mergedLastName": "Smith",
    "mergedOrganization": null,
    "familyConsolidate": true,
    "allowTransactions": true
}

```

Creates a new account merge object.

##### Arguments

* mergedAccount (required) - The account number of the account to be merged. Both accounts must be of the same type, Individual or Organization. For Family type, see [Create a family account merge](#create-a-family-account-merge).
* shortComment (optional) - A short comment to be associated with the account merge.

##### Returns

Returns an account merge object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an account of a type different than the specified account).

#### Create a family account merge

```
DEFINITION
POST http://apiserver/accounts/:id/merges

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/120003/merges", {
    "mergedAccount": "120008",
    "familyMembers": [
        { "winningAccount": "120333", "losingAccount": "76464" },
        { "winningAccount": "120334", "losingAccount": "76465" },
        { "winningAccount": "120335", "losingAccount": "76466" },
        { "winningAccount": "120336", "losingAccount": "76467" },
        { "winningAccount": "120331", "losingAccount": "76468" },
        { "winningAccount": "120332", "losingAccount": "76469" }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1000123377",
    "mergedAccount": "120008",
    "date": "1/19/2015 12:00:00 AM",
    "shortComment": null,
    "type": "F",
    "familyId": "120008",
    "memberType": "F",
    "mergedFirstName": "Tom",
    "mergedLastName": "Jordan",
    "mergedOrganization": "Tom Jordan",
    "familyConsolidate": true,
    "allowTransactions": true
}

```

Creates a new family account merge object.

##### Arguments

* mergedAccount (required) - The account number of the family account to be merged.
* shortComment (optional) - A short comment to be associated with the account merge.
* familyMembers (optional) - A map of account numbers of family members to account numbers of members to merge. After a family is merged, the merged family cannot end up with more than two spouses, so some number of maps may need to be specified in order for the merge to be allowed.

##### Returns

Returns an account family merge object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an account of a type different than the specified account).

#### Retrieve an account merge

```
DEFINITION
GET http://apiserver/accounts/:id/merges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/120003/merges/1000123374");

EXAMPLE RESPONSE
{
    "id": "1000123374",
    "mergedAccount": "120007",
    "date": "1/19/2015 12:00:00 AM",
    "shortComment": null,
    "type": "I",
    "familyId": "0",
    "memberType": null,
    "mergedFirstName": "Steven",
    "mergedLastName": "Smith",
    "mergedOrganization": null,
    "familyConsolidate": true,
    "allowTransactions": true
}

```

Retrieves the details of an existing account merge. You need only supply the account merge id.

##### Arguments

* id (required) - The id of the account merge to retrieve.

##### Returns

Returns an account merge object if a valid id was provided.

#### Delete an account merge

```
DEFINITION
DELETE http://apiserver/accounts/:id/merges/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/120003/merges/1000123374", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account merge. This will unmerge the accounts.

##### Arguments

* id (required) - The id of the account merge to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account merge id does not exist, this call returns an error.

#### List all account merges

```
DEFINITION
GET http://apiserver/accounts/:id/merges

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/120003/merges");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000123374",
            "mergedAccount": "120007",
            "date": "1/19/2015 12:00:00 AM",
            "shortComment": null,
            "type": "I",
            "familyId": "0",
            "memberType": null,
            "mergedFirstName": "Steven",
            "mergedLastName": "Smith",
            "mergedOrganization": null,
            "familyConsolidate": true,
            "allowTransactions": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account merges.

##### Returns

A dictionary with an items property that contains an array of up to limit account merges, starting at index offset. Each entry in the array is a separate account merge object. If no more account merges are available, the resulting array will be empty. This request should never return an error.

### Account My Donations

#### List all account my donations

```
DEFINITION
GET http://apiserver/accounts/:accountId/mydonations

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/30199/mydonations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "446154",
            "documentNumber": "505890",
            "transactionDate": "2016-11-20",
            "totalAmount": 44,
            "sourceCode": "CRM",
            "sourceCodeDescription": "CRM",
            "elementGroup": "D10D",
            "elementGroupDescription": "Direct Mail Appeal 2010 April",
            "projectCode": "101010",
            "projectCodeDescription": "Billy Key",
            "subaccount": null,
            "subaccountDescription": null,
            "associatedAccountNumber": null,
            "associatedAccountName": null,
            "pledgeCode": "050098",
            "pledgeCodeDescription": "Mark McLemore Outreach 2012",
            "isDeductible": true,
            "shortComment": null
        },
        {...},
    ]
}

```

Returns a list of all account my donations.

##### Returns

A dictionary with an items property that contains an array of up to limit account my donations, starting at index offset. Each entry in the array is a separate account my donation object. If no more account my donations are available, the resulting array will be empty. This request should never return an error.

### Account My Recurrings

#### List all account my recurrings

```
DEFINITION
GET http://apiserver/accounts/:accountId/myrecurrings

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/29154/myrecurrings");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "151747",
            "amount": 1000000.0000,
            "source": "0_A",
            "sourceDescription": "Zero",
            "project": "101010",
            "projectDescription": "Billy (William) Key",
            "subaccount": null,
            "subaccountDescription": null,
            "relatedAccount": null,
            "relatedAccountName": null,
            "accountPledge": null,
            "pledgeCode": null,
            "accountPledgeDescription": null,
            "isDeductible": true,
            "isAnonymous": false,
            "shortComment": null,
            "mediaOutlet": null,
            "mediaOutletDescription": null,
            "elementGroup": null,
            "elementGroupDescription": null,
            "header": {
                "id": "1000001125",
                "currency": "USD",
                "frequency": "M",
                "frequencyDescription": "Monthly",
                "start": "2021-12-17",
                "end": null,
                "numberCommitted": null,
                "numberRemaining": null,
                "useOnDay": "1",
                "category": "ACTIVE",
                "shortComment": null,
                "source": "EV11CPCATL",
                "sourceDescription": "Pastor's Conf March 2011 Atlanta",
                "contactMethod": "EMAIL",
                "status": "D",
                "lastUsedDate": null,
                "assignedToAccessor": null,
                "assignedToAccessorDescription": null,
                "account": "29154",
                "accountName": "Calvin and Jackie Morris",
                "numberOfDeclines": 2,
                "referenceNumber": {
                    "cardType": "VISA",
                    "last4Digits": "1111",
                    "expirationMonth": "12",
                    "expirationYear": "2025",
                    "nameOnCard": "Calvin Morris",
                    "text": "VISA-1111 12/2025 Calvin Morris"
                },
                "paymentType": "CC",
                "paymentTypeDescription": "Credit Cards",
                "useOnDayDescription": "1st of the Month",
                "elementGroup": "D10D",
                "elementGroupDescription": "Direct Mail Appeal 2010 April"
            }
        },
        {
            "id": "151889",
            "amount": 33.0000,
            "source": "0_A",
            "sourceDescription": "Zero",
            "project": "101011",
            "projectDescription": "Betty Key",
            "subaccount": "AUDIO",
            "subaccountDescription": "Audio",
            "relatedAccount": "12584",
            "relatedAccountName": "First Baptist Church",
            "accountPledge": null,
            "pledgeCode": null,
            "accountPledgeDescription": null,
            "isDeductible": false,
            "isAnonymous": false,
            "shortComment": null,
            "mediaOutlet": "KLTY",
            "mediaOutletDescription": "KLTY FM Radio 94.9",
            "elementGroup": null,
            "elementGroupDescription": null,
            "header": {
                "id": "1000001126",
                "currency": "USD",
                "frequency": "Q",
                "frequencyDescription": "Quarterly",
                "start": "2022-06-24",
                "end": "2023-06-23",
                "numberCommitted": null,
                "numberRemaining": null,
                "useOnDay": "13",
                "category": "ACTIVE",
                "shortComment": null,
                "source": "EV11CPCATL",
                "sourceDescription": "Pastor's Conf March 2011 Atlanta",
                "contactMethod": "EMAIL",
                "status": "Y",
                "lastUsedDate": null,
                "assignedToAccessor": "25846",
                "assignedToAccessorDescription": "John Doe - Internal User",
                "account": "29154",
                "accountName": "Calvin and Jackie Morris",
                "numberOfDeclines": 0,
                "referenceNumber": {
                    "bankAccountType": "C",
                    "last4Digits": "6789",
                    "text": "xxxxx6789-C"
                },
                "paymentType": "EFT",
                "paymentTypeDescription": "Electronic Fund Transfers",
                "useOnDayDescription": "13th of the Month",
                "elementGroup": "D10D",
                "elementGroupDescription": "Direct Mail Appeal 2010 April"
            }
        },
        {
            "id": "151890",
            "amount": 12.0000,
            "source": "TT13P06R00",
            "sourceDescription": "March Renewal",
            "project": "101010",
            "projectDescription": "Billy (William) Key",
            "subaccount": "002",
            "subaccountDescription": "Travel Reserve",
            "relatedAccount": null,
            "relatedAccountName": null,
            "accountPledge": null,
            "pledgeCode": null,
            "accountPledgeDescription": null,
            "isDeductible": true,
            "isAnonymous": false,
            "shortComment": null,
            "mediaOutlet": null,
            "mediaOutletDescription": null,
            "elementGroup": "D10D",
            "elementGroupDescription": "Direct Mail Appeal 2010 April",
            "header": {
                "id": "1000001127",
                "currency": "USD",
                "frequency": "M",
                "frequencyDescription": "Monthly",
                "start": "2022-06-01",
                "end": null,
                "numberCommitted": null,
                "numberRemaining": null,
                "useOnDay": "5",
                "category": "ACTIVE",
                "shortComment": null,
                "source": "0_A",
                "sourceDescription": "Zero",
                "contactMethod": "EMAIL",
                "status": "Y",
                "lastUsedDate": null,
                "assignedToAccessor": null,
                "assignedToAccessorDescription": null,
                "account": "29154",
                "accountName": "Calvin and Jackie Morris",
                "numberOfDeclines": 0,
                "referenceNumber": {
                    "text": "4564"
                },
                "paymentType": "CK",
                "paymentTypeDescription": "Check",
                "useOnDayDescription": "5th of the Month",
                "elementGroup": null,
                "elementGroupDescription": null
            }
        },
        {...},
    ]
}

```

Returns a list of all account my recurrings.

##### Arguments

* accountId (required) - The id of the account for which to return account my recurrings.

##### Returns

A dictionary with an items property that contains an array of up to limit account my recurrings, starting at index offset. Each entry in the array is a separate account my recurring object. If no more account my recurrings are available, the resulting array will be empty. This request should never return an error.

### Account Notes

#### Create an account note

```
DEFINITION
POST http://apiserver/accounts/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/notes", {
    "type": "DDCACALERT",
    "shortComment": "Account Alert"
});

EXAMPLE RESPONSE
{
    "id": "22793",
    "date": "2014-05-11",
    "dateModified": "2014-05-12",
    "type": "DDCACALERT",
    "shortComment": "Account Alert",
    "longComment": null,
    "dataSource": "ADMIN"
}

```

Creates a new account note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.
* dataSource (optional) - The data source of the code. If not specified, a default value will be set.

##### Returns

Returns an account note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve an account note

```
DEFINITION
GET http://apiserver/accounts/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/notes/22793");

EXAMPLE RESPONSE
{
    "id": "22793",
    "date": "2014-05-11",
    "dateModified": "2014-05-12",
    "type": "DDCACALERT",
    "shortComment": "Account Alert",
    "longComment": null,
    "dataSource": "ADMIN"
}

```

Retrieves the details of an existing account note. You need only supply the account note id.

##### Arguments

* id (required) - The id of the account note to retrieve.

##### Returns

Returns an account note object if a valid id was provided.

#### Update an account note

```
DEFINITION
POST http://apiserver/accounts/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/notes/22793", {
    "shortComment": null,
    "longComment": "Account Alert"
});

EXAMPLE RESPONSE
{
    "id": "22793",
    "date": "2014-05-11",
    "dateModified": "2014-05-12",
    "type": "DDCACALERT",
    "shortComment": null,
    "longComment": "Account Alert",
    "dataSource": "ADMIN"
}


```

Updates the specified account note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the account note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete an account note

```
DEFINITION
DELETE http://apiserver/accounts/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/notes/22793", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account note. It cannot be undone.

##### Arguments

* id (required) - The id of the account note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account note id does not exist, this call returns an error.

#### List all account notes

```
DEFINITION
GET http://apiserver/accounts/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "22793",
            "date": "2014-05-11",
            "dateModified": "2014-05-12",
            "type": "DDCACALERT",
            "shortComment": "Account Alert",
            "longComment": null,
            "dataSource": "ADMIN"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account notes.

##### Arguments

* includeFamilyNotes (optional) - If true, this will return a list of all account notes from the family accounts also.

##### Returns

A dictionary with an items property that contains an array of up to limit account notes, starting at index offset. Each entry in the array is a separate account note object. If no more account notes are available, the resulting array will be empty. This request should never return an error.

### Account Numbers

#### Create an account number

```
DEFINITION
POST http://apiserver/accounts/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/numbers", {
    "type": "DDCJOBS",
    "value": 2
});

EXAMPLE RESPONSE
{
    "id": "4217",
    "type": "DDCJOBS",
    "value": 2,
    "dataSource": "ADMIN",
    "isActive": true
}

```

Creates a new account number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* dataSource (optional) - The data source of the code. If not specified, a default value will be set.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an account number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve an account number

```
DEFINITION
GET http://apiserver/accounts/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/numbers/4217");

EXAMPLE RESPONSE
{
    "id": "4217",
    "type": "DDCJOBS",
    "value": 2,
    "dataSource": "ADMIN",
    "isActive": true
}

```

Retrieves the details of an existing account number. You need only supply the account number id.

##### Arguments

* id (required) - The id of the account number to retrieve.

##### Returns

Returns an account number object if a valid id was provided.

#### Update an account number

```
DEFINITION
POST http://apiserver/accounts/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/numbers/4217", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "4217",
    "type": "DDCJOBS",
    "value": 2,
    "dataSource": "ADMIN",
    "isActive": false
}


```

Updates the specified account number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the account number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete an account number

```
DEFINITION
DELETE http://apiserver/accounts/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/numbers/4217", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account number. It cannot be undone.

##### Arguments

* id (required) - The id of the account number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account number id does not exist, this call returns an error.

#### List all account numbers

```
DEFINITION
GET http://apiserver/accounts/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4217",
            "type": "DDCJOBS",
            "value": 2,
            "dataSource": "ADMIN",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit account numbers, starting at index offset. Each entry in the array is a separate account number object. If no more account numbers are available, the resulting array will be empty. This request should never return an error.

### Account Overrides

#### Create an account override

```
DEFINITION
POST http://apiserver/accounts/:id/overrides

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/overrides", {
    "type": "DDCOVERTAX",
    "value": "Y"
});

EXAMPLE RESPONSE
{
    "id": "8265",
    "type": "DDCOVERTAX",
    "value": "Y",
    "isActive": true
}

```

Creates a new account override object.

##### Arguments

* type (required) - The override type. Must be a defined override type.
* value (required) - The override value. Must be a defined value of the specified override type.
* isActive (optional) - Whether or not the override is active.

##### Returns

Returns an account override object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined override type).

#### Retrieve an account override

```
DEFINITION
GET http://apiserver/accounts/:id/overrides/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/overrides/8265");

EXAMPLE RESPONSE
{
    "id": "8265",
    "type": "DDCOVERTAX",
    "value": "Y",
    "isActive": true
}

```

Retrieves the details of an existing account override. You need only supply the account override id.

##### Arguments

* id (required) - The id of the account override to retrieve.

##### Returns

Returns an account override object if a valid id was provided.

#### Update an account override

```
DEFINITION
POST http://apiserver/accounts/:id/overrides/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/overrides/8265", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "8265",
    "type": "DDCOVERTAX",
    "value": "Y",
    "isActive": false
}


```

Updates the specified account override by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The override type. Must be a defined override type.
* value (optional) - The override value. Must be a defined value of the override type.
* isActive (optional) - Whether or not the override is active.

##### Returns

Returns the account override object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined override type or override type value).

#### Delete an account override

```
DEFINITION
DELETE http://apiserver/accounts/:id/overrides/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/overrides/8265", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account override. It cannot be undone.

##### Arguments

* id (required) - The id of the account override to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account override id does not exist, this call returns an error.

#### List all account overrides

```
DEFINITION
GET http://apiserver/accounts/:id/overrides

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/overrides");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "8265",
            "type": "DDCOVERTAX",
            "value": "Y",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account overrides.

##### Returns

A dictionary with an items property that contains an array of up to limit account overrides, starting at index offset. Each entry in the array is a separate account override object. If no more account overrides are available, the resulting array will be empty. This request should never return an error.

### Account Periodic Receipts

#### Delete an account periodic receipt

```
DEFINITION
DELETE http://apiserver/accounts/:accountId/periodicreceipts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16403/periodicreceipts/10059", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account periodic receipt. It cannot be undone.

##### Arguments

* accountId (required) - The account number for which to delete a periodic receipt.
* id (required) - The id of the account periodic receipt to be deleted.

##### Returns

Returns a `204 No Content` response on success.

#### List all account periodic receipts

```
DEFINITION
GET http://apiserver/accounts/:id/periodicreceipts

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/periodicreceipts?offset=0&limit=5");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 5,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4370",
            "receiptId": "4229",
            "runId": "1000000037",
            "runDate": "2022-05-24"
            "accountNumber": "16230",
            "accountName": "Mr. Phil A Buster II",
            "yearToDateDeductibleDonationsTotal": 40.00,
            "yearToDateNonDeductibleDonationsTotal": 0.00,
            "yearToDateFairMarketValueTotal": 85.86,
            "yearToDateIRADonationsTotal": 120.00,
            "formType": "PERRCPTTST"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account periodic receipts. If the account is in a family, then all periodic receipts within the family are returned.

##### Arguments

* id (required) - The account number for which to retrieve periodic receipts.

##### Returns

A dictionary with an `items` property that contains an array of up to `limit` account periodic receipts, starting at index `offset`. Each entry in the array is a separate account periodic receipt object. If no more account periodic receipts are available, the resulting array will be empty. This request should never return an error.

### Account Phones

#### Create an account phone

```
DEFINITION
POST http://apiserver/accounts/:id/phones

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/phones", {
    "type": "HOME",
    "phoneNumber": "867-5309"
});

EXAMPLE RESPONSE
{
    "id": "555",
    "type": "HOME",
    "internationalCode": null,
    "areaCode": null,
    "phoneNumber": "867-5309",
    "extension": null,
    "dataSource": "DDC",
    "isPrimary": false,
    "isActive": true,
    "functionalCategory": null,
    "functionalCategoryDescription": null
}

```

Creates a new account phone object.

##### Arguments

* type (required) - The phone type. Must be a defined phone type.
* phoneNumber (required) - The phone number.
* internationalCode (optional) - The international code of the phone.
* areaCode (optional) - The area code of the phone.
* extension (optional) - The extension of the phone.
* dataSource (optional) - The data source of the phone. If not specified, a default value will be set.
* isPrimary (optional) - Whether or not the phone is the primary address for the account.
* isActive (optional) - Whether or not the phone is active.
* functionalCategory (optional) - The functional category of this phone.

##### Returns

Returns an account phone object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined phone type).

#### Retrieve an account phone

```
DEFINITION
GET http://apiserver/accounts/:id/phones/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/phones/555");

EXAMPLE RESPONSE
{
    "id": "555",
    "type": "HOME",
    "internationalCode": null,
    "areaCode": null,
    "phoneNumber": "867-5309",
    "extension": null,
    "dataSource": "DDC",
    "isPrimary": false,
    "isActive": true,
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Direct Mail"
}

```

Retrieves the details of an existing account phone. You need only supply the account phone id.

##### Arguments

* id (required) - The id of the account phone to retrieve.

##### Returns

Returns an account phone object if a valid id was provided.

#### Update an account phone

```
DEFINITION
POST http://apiserver/accounts/:id/phones/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/phones/555", {
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "555",
    "type": "HOME",
    "internationalCode": null,
    "areaCode": null,
    "phoneNumber": "867-5309",
    "extension": null,
    "dataSource": "DDC",
    "isPrimary": true,
    "isActive": true,
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Direct Mail"
}


```

Updates the specified account phone by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The phone type. Must be a defined phone type.
* internationalCode (optional) - The international code of the phone.
* areaCode (optional) - The area code of the phone.
* phoneNumber (optional) - The phone number.
* extension (optional) - The extension of the phone.
* isPrimary (optional) - Whether or not the phone is the primary address for the account.
* isActive (optional) - Whether or not the phone is active.
* dataSource (optional) - The data source of the phone. If not specified, a default value will be set.
* functionalCategory (optional) - The functional category of this phone.

##### Returns

Returns the account phone object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined phone type or phone type value).

#### Delete an account phone

```
DEFINITION
DELETE http://apiserver/accounts/:id/phones/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/phones/555", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account phone. It cannot be undone.

##### Arguments

* id (required) - The id of the account phone to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account phone id does not exist, this call returns an error.

#### List all account phones

```
DEFINITION
GET http://apiserver/accounts/:id/phones

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/phones");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "555",
            "type": "HOME",
            "internationalCode": null,
            "areaCode": null,
            "phoneNumber": "867-5309",
            "extension": null,
            "dataSource": "DDC",
            "isPrimary": false,
            "isActive": true,
            "functionalCategory": "DM",
            "functionalCategoryDescription": "Direct Mail"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account phones.

##### Arguments

* id (required) - The id of the account to get the phones.
* isPrimary (optional) - Whether to retrieve the single primary phone.
* functionalCategory (optional) - The functionalCategory of the single preferred phone number to retrieve.
* includeFamilyNotes (optional) - If true, this will return a list of all account notes from the family accounts also.

##### Returns

A dictionary with an items property that contains an array of up to limit account phones, starting at index offset. Each entry in the array is a separate account phone object. If no more account phones are available, the resulting array will be empty. This request should never return an error.

### Account Pledges

#### Create an account pledge

```
DEFINITION
POST http://apiserver/accounts/:id/pledges

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges", {
    "pledge": "050098",
    "currency": "USD",
    "totalAmount": 2004,
    "amountPerGift": 501,
    "numberPledged": 4,
    "frequency": "M",
    "start": "2012-04-01",
    "end": "2013-04-01",
    "source": "EV11CPCATL",
    "response": {
        "letter": "THANKYOU",
        "paragraphs": [
            {
                "type": "PR1",
                "completionText": "Thank you for your support."
            }
        ]
    }
});

EXAMPLE RESPONSE
{
    "id": "1172",
    "pledge": "050098",
    "pledgeDescription": "Mark McLemore Outreach 2012",
    "type": "PROJECT",
    "currency": "USD",
    "totalAmount": 2004,
    "amountPerGift": 501,
    "numberPledged": 4,
    "totalAmountDonated": 0,
    "totalNumberDonated": null,
    "totalRelatedAmountDonated": null,
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2012-04-01",
    "end": "2013-04-01",
    "isOpenEnded": false,
    "source": "EV11CPCATL",
    "sourceDescription": "General Source Code",
    "elementGroup": "PC11C",
    "elementGroupDescription": "Pastor's Conference March 2011",
    "status": "A",
    "isActive": false,
    "cancelReason": null,
    "cancelDate": null,
    "numberOfAdjustmentMonths": null,
    "stmtAndAckAccount": null,
    "stmtAndAckAccountName": null,
    "infoAndUpdatesAccount": null,
    "infoAndUpdatesAccountName": null,
    "paidThroughDate": null,
    "originalPledge": null,
    "company": null,
    "account": "1483320",
    "accountName": "Henry Winkler",
    "defaultProjetCode": null,
    "response": {
        "id": 476182,
        "method": null,
        "type": "PLDGACK",
        "profileGroup": null,
        "printGroup": null,
        "printDate": null,
        "paragraphs": [
            {
                "id": "110646",
                "type": "PR1",
                "completionText": "Thank you for your support."
            }
        ],
        "letter": "THANKYOU",
        "isAutoAssigned": false,
        "completionText": "",
        "address": "1000026701",
        "inserts": null,
        "status": "Y"
    },
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "hasRecurring": false
}

```

Creates a new account pledge object.

##### Arguments

* pledge (required) - The pledge code of the account pledge.
* currency (required) - The currency code of the account pledge.
* totalAmount (required) - The total amount of the account pledge.
* amountPerGift (required) - The amount per gift of the account pledge.
* numberPledged (required) - The number of gifts of the account pledge.
* frequency (required) - The frequency of the account pledge. Must be a defined pledge frequency.
* start (required) - The start date of the account pledge.
* end (optional) - The end date of the account pledge. If not specified, the account pledge will be created as open ended.
* source (required) - The source code of the account pledge. Must be a defined source code.
* response (required) - A response object for the account pledge. Must include at least a letter code.
* numberOfAdjustmentMonths (optional) - The number of adjustment months of the account pledge.
* infoAndUpdatesAccount (optional) - The account number to use for info and updates. If not specified, will default to the account of the account pledge.
* stmtAndAckAccount (optional) - The account number to use for statements and acknowledgments. If not specified, will default to the account of the account pledge.
* originalPledge (optional) - The id of the original account pledge. Specify in order to continue a pledge. Note: continuing a pledge does not copy premiums, codes, dates, notes, numbers, or attachments from the source pledge.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.
* securePageType (optional) - The secure page type that originated the request.
* secureMatchingText (optional) - The criteria used when matching a secure pledge to a PledgeCode/Description.
* store (optional) - If created from a StudioOnline store, passing a StudioOnline store Id will be used to default the pledge source code, if the source code is not provided.

##### Returns

Returns an account pledge object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined pledge code).

#### Retrieve an account pledge

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/4402");

EXAMPLE RESPONSE
{
    "id": "1172",
    "pledge": "050098",
    "pledgeDescription": "Mark McLemore Outreach 2012",
    "type": "PROJECT",
    "currency": "USD",
    "totalAmount": 1200,
    "amountPerGift": 100,
    "numberPledged": 12,
    "totalAmountDonated": 0,
    "totalNumberDonated": null,
    "totalRelatedAmountDonated": null,
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2012-04-01",
    "end": "2013-04-01",
    "isOpenEnded": false,
    "source": "EV11CPCATL",
    "sourceDescription": "General Source Code",
    "elementGroup": "PC11C",
    "elementGroupDescription": "Pastor's Conference March 2011",
    "status": "A",
    "isActive": false,
    "cancelReason": null,
    "cancelDate": null,
    "numberOfAdjustmentMonths": null,
    "stmtAndAckAccount": null,
    "stmtAndAckAccountName": null,
    "infoAndUpdatesAccount": null,
    "infoAndUpdatesAccountName": null,
    "paidThroughDate": null,
    "originalPledge": null,
    "company": null,
    "account": "1483320",
    "accountName": "Henry Winkler",
    "defaultProjetCode": null,
    "response": {
        "id": 476182,
        "method": null,
        "type": "PLDGACK",
        "profileGroup": "3137",
        "printGroup": null,
        "printDate": "2015-04-19",
        "paragraphs": [
            {
                "id": "110646",
                "type": "A02",
                "completionText": ""
            }
        ],
        "letter": "0613APPL",
        "isAutoAssigned": false,
        "completionText": "",
        "address": "1000026701",
        "inserts": null,
        "status": "R"
    },
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "pledgeData": null,
    "hasRecurring": false,
    "recurringTransactionStatuses": "[]",
    "lastPaymentDate": "2024-01-23",
    "lastPaymentAmount": 300.0000,
    "nextPaymentDate": null,
    "deficientAmount": 0.0000
}

```

Retrieves the details of an existing account pledge. You need only supply the account pledge id.

##### Arguments

* id (required) - The id of the account pledge to retrieve.
* store (optional) - StudioOnline store Id; when provided, returns json that represents the pledge.

##### Returns

Returns an account pledge object if a valid id was provided.

#### Update an account pledge

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/1172", {
    "status": "X",
    "cancelReason": "NIL",
    "cancelDate": "2013-09-01"
});

EXAMPLE RESPONSE

{
    "id": "1172",
    "pledge": "050098",
    "pledgeDescription": "Mark McLemore Outreach 2012",
    "type": "PROJECT",
    "currency": "USD",
    "totalAmount": 2004,
    "amountPerGift": 501,
    "numberPledged": 12,
    "totalAmountDonated": 0,
    "totalNumberDonated": null,
    "totalRelatedAmountDonated": null,
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2012-04-01",
    "end": "2013-04-01",
    "isOpenEnded": false,
    "source": "EV11CPCATL",
    "sourceDescription": "General Source Code",
    "elementGroup": "PC11C",
    "elementGroupDescription": "Pastor's Conference March 2011",
    "status": "A",
    "isActive": false,
    "cancelReason": null,
    "cancelDate": null,
    "numberOfAdjustmentMonths": null,
    "stmtAndAckAccount": null,
    "stmtAndAckAccountName": null,
    "infoAndUpdatesAccount": null,
    "infoAndUpdatesAccountName": null,
    "paidThroughDate": null,
    "originalPledge": null,
    "company": null,
    "account": "1483320",
    "accountName": "Henry Winkler",
    "defaultProjetCode": null,
    "response": {
        "id": 476182,
        "method": null,
        "type": "PLDGACK",
        "profileGroup": "3137",
        "printGroup": null,
        "printDate": "2015-04-19",
        "paragraphs": [
            {
                "id": "110646",
                "type": "A02",
                "completionText": ""
            }
        ],
        "letter": "0613APPL",
        "isAutoAssigned": false,
        "completionText": "",
        "address": "1000026701",
        "inserts": null,
        "status": "R"
    },
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "hasRecurring": false
}

```

Updates the specified account pledge by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* pledge (optional) - The pledge code of the account pledge.
* currency (optional) - The currency code of the account pledge.
* totalAmount (optional) - The total amount of the account pledge.
* amountPerGift (optional) - The amount per gift of the account pledge.
* numberPledged (optional) - The number of gifts of the account pledge.
* frequency (optional) - The frequency of the account pledge. Must be a defined pledge frequency.
* start (optional) - The start date of the account pledge.
* end (optional) - The end date of the account pledge. If not specified, the account pledge will be created as open ended.
* source (optional) - The source code of the account pledge. Must be a defined source code.
* numberOfAdjustmentMonths (optional) - The number of adjustment months of the account pledge.
* infoAndUpdatesAccount (optional) - The account number to use for info and updates. If not specified, will default to the account of the account pledge.
* stmtAndAckAccount (optional) - The account number to use for statements and acknowledgments. If not specified, will default to the account of the account pledge.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.

##### Returns

Returns the account pledge object if the update succeeded. Returns an error if update parameters are invalid (e.g. changing status to `X` without specifying a defined cancel reason and date).

#### Delete an account pledge

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/pledges/4402", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge. It cannot be undone.

##### Arguments

* id (required) - The id of the account pledge to be deleted.
* deletePremiums (optional) - `true` if account pledge premiums should be deleted as well.

##### Returns

Returns a 204 No Content response on success. If the account pledge id does not exist, this call returns an error.

#### List all account pledges

```
DEFINITION
GET http://apiserver/accounts/:id/pledges

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "1172",
            "pledge": "050098",
            "pledgeDescription": "Mark McLemore Outreach 2012",
            "type": "PROJECT",
            "currency": "USD",
            "totalAmount": 1200,
            "amountPerGift": 100,
            "numberPledged": 12,
            "totalAmountDonated": 0,
            "totalNumberDonated": 0,
            "totalRelatedAmountDonated": null,
            "frequency": "M",
            "frequencyDescription": "Monthly",
            "start": "2012-04-01",
            "end": "2013-04-01",
            "isOpenEnded": false,
            "source": "EV11CPCATL",
            "sourceDescription": "General Source Code",
            "elementGroup": "PC11C",
            "elementGroupDescription": "Pastor's Conference March 2011",
            "status": "A",
            "isActive": true,
            "cancelReason": null,
            "cancelDate": null,
            "numberOfAdjustmentMonths": null,
            "stmtAndAckAccount": null,
            "stmtAndAckAccountName": null,
            "infoAndUpdatesAccount": null,
            "infoAndUpdatesAccountName": null,
            "paidThroughDate": null,
            "originalPledge": null,
            "company": "1",
            "account": "1483320",
            "accountName": "Henry Winkler",
            "defaultProjetCode": null,
            "response": {
                "id": 476182,
                "method": null,
                "type": "PLDGACK",
                "profileGroup": "3137",
                "printGroup": null,
                "printDate": "2015-04-19",
                "paragraphs": [
                    {
                        "id": "110646",
                        "type": "A02",
                        "completionText": ""
                    }
                ],
                "letter": "0613APPL",
                "isAutoAssigned": false,
                "completionText": "",
                "address": "1000026701",
                "inserts": null,
                "status": "R"
            },
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null,
            "pledgeData": null,
            "hasRecurring": false,
            "recurringTransactionStatuses": "[]",
            "lastPaymentDate": "2024-01-23",
            "lastPaymentAmount": 300.0000,
            "nextPaymentDate": null,
            "deficientAmount": 0.0000
        }
    ]
}

```

Returns a list of all account pledges. If the account is in a family, then all pledges within the family are returned.

##### Arguments

* excludeResponseProperty (optional; default is `false`) - Skips populating the `response` property which is somewhat of an expensive opperation due to current implementation details. This argument is intended for very specific scenarios where the account pledge response information is not necessary.
* getPageContainingId (optional) - Will return the page of account pledges that contains the pledge with this id.
* accessorId (optional) - When provided, the account pledges will be filtered to only the account pledges for which the accessor has access.
* includeGroups (optional) - Only used if `accessorId` is provided. It will include any account pledge that any group member has access to. The group members are any member of a group the `accessorId` is also a part of.
* groupMemberAccessorId (optional) - Only used if `includeGroups` is provided. It will filter the communications to only return communications that are assigned to the specified group member.
* status (optional) - The status of the pledges you would like to return. `AP` will return all Active and Pending pledges.
* company (optional) - Will return the page of account pledges that contains the pledge with this company.
* store (optional) - StudioOnline store Id; when provided, returns json that represents the pledge.
* sponsorshipType (optional) - Determines what type of sponsorships to return. A null value returns all pledges, NONE returns only non-sponsorship pledges, BOTH returns CHILD and OTHER sponsorships, and CHILD / OTHER return only sponsorships that match CHILD / OTHER.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledges, starting at index offset. Each entry in the array is a separate account pledge object. If no more account pledges are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Attachments

#### Create an account pledge attachment

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/pledges/11921/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new account pledge attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.
* originalId (optional: if set, file is not required) - The id of an attachment to copy the file from. This is intended for use with continuing a pledge; a file can be copied without being downloaded.

##### Returns

Returns an account pledge attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve an account pledge attachment

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/pledges/11921/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing account pledge attachment.

##### Arguments

* id (required) - The id of the account attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns an account pledge attachment object if a valid id was provided.

#### Update an account pledge attachment

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16234/pledges/11921/attachments/49", {
    "type": "LOGO",
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Updates the specified attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the account pledge attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete an account pledge attachment

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16234/pledges/11921/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account pledge attachment id does not exist, this call returns an error.

#### List all account pledge attachments

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16234/pledges/11921/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge attachments, starting at index offset. Each entry in the array is a separate account pledge attachment object. If no more account pledge attachments are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Codes

#### Create an account pledge code

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/codes", {
    "type": "PLDGMATCH",
    "value": "UCM"
});

EXAMPLE RESPONSE
{
    "id": "540",
    "type": "PLDGMATCH",
    "typeDescription": "Pledge Matching",
    "value": "UCM",
    "valueDescription": "Match Used",
    "isActive": true
}

```

Creates a new account pledge code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns an account pledge code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve an account pledge code

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/codes/540");

EXAMPLE RESPONSE
{
    "id": "540",
    "type": "PLDGMATCH",
    "typeDescription": "Pledge Matching",
    "value": "UCM",
    "valueDescription": "Match Used",
    "isActive": true
}

```

Retrieves the details of an existing account pledge code. You need only supply the account pledge code id.

##### Arguments

* id (required) - The id of the account pledge code to retrieve.

##### Returns

Returns an account pledge code object if a valid id was provided.

#### Update an account pledge code

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/codes/540", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "540",
    "type": "PLDGMATCH",
    "typeDescription": "Pledge Matching",
    "value": "UCM",
    "valueDescription": "Match Used",
    "isActive": false
}


```

Updates the specified account pledge code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the account pledge code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete an account pledge code

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/pledges/620701/codes/540", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge code. It cannot be undone.

##### Arguments

* id (required) - The id of the account pledge code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account pledge code id does not exist, this call returns an error.

#### List all account pledge codes

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "540",
            "type": "PLDGMATCH",
            "typeDescription": "Pledge Matching",
            "value": "UCM",
            "valueDescription": "Match Used",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge codes.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge codes, starting at index offset. Each entry in the array is a separate account pledge code object. If no more account pledge codes are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Dates

#### Create an account pledge date

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/dates", {
    "type": "DDCPLGDT1",
    "value": "2014-07-26"
});

EXAMPLE RESPONSE
{
    "id": "958",
    "type": "DDCPLGDT1",
    "typeDescription": "Pledge Date",
    "value": "2014-07-26",
    "isActive": true
}

```

Creates a new account pledge date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns an account pledge date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve an account pledge date

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/dates/958");

EXAMPLE RESPONSE
{
    "id": "958",
    "type": "DDCPLGDT1",
    "typeDescription": "Pledge Date",
    "value": "2014-07-26",
    "isActive": true
}

```

Retrieves the details of an existing account pledge date. You need only supply the account pledge date id.

##### Arguments

* id (required) - The id of the account pledge date to retrieve.

##### Returns

Returns an account pledge date object if a valid id was provided.

#### Update an account pledge date

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/dates/958", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "958",
    "type": "DDCPLGDT1",
    "typeDescription": "Pledge Date",
    "value": "2014-07-26",
    "isActive": false
}


```

Updates the specified account pledge date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the account pledge date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete an account pledge date

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/pledges/620701/dates/958", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge date. It cannot be undone.

##### Arguments

* id (required) - The id of the account pledge date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account pledge date id does not exist, this call returns an error.

#### List all account pledge dates

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "958",
            "type": "DDCPLGDT1",
            "typeDescription": "Pledge Date",
            "value": "2014-07-26",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge dates.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge dates, starting at index offset. Each entry in the array is a separate account pledge date object. If no more account pledge dates are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Notes

#### Create an account pledge note

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/notes", {
    "type": "DDCPLGNT",
    "shortComment": "Pledge Reminder"
});

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCPLGNT",
    "typeDescription": "Pledge Record Note",
    "shortComment": "Pledge Reminder",
    "longComment": null
}

```

Creates a new account pledge note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns an account pledge note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve an account pledge note

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/notes/31884");

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCPLGNT",
    "typeDescription": "Pledge Record Note",
    "shortComment": "Pledge Reminder",
    "longComment": null
}

```

Retrieves the details of an existing account pledge note. You need only supply the account pledge note id.

##### Arguments

* id (required) - The id of the account pledge note to retrieve.

##### Returns

Returns an account pledge note object if a valid id was provided.

#### Update an account pledge note

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/notes/31884", {
    "shortComment": null,
    "longComment": "Pledge Reminder"
});

EXAMPLE RESPONSE
{
    "id": "31884",
    "type": "DDCPLGNT",
    "typeDescription": "Pledge Record Note",
    "shortComment": null,
    "longComment": "Pledge Reminder"
}


```

Updates the specified account pledge note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the account pledge note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete an account pledge note

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/pledges/620701/notes/31884", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge note. It cannot be undone.

##### Arguments

* id (required) - The id of the account pledge note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account pledge note id does not exist, this call returns an error.

#### List all account pledge notes

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "31884",
            "type": "DDCPLGNT",
            "typeDescription": "Pledge Record Note",
            "shortComment": "Pledge Reminder",
            "longComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge notes.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge notes, starting at index offset. Each entry in the array is a separate account pledge note object. If no more account pledge notes are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Numbers

#### Create an account pledge number

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/numbers", {
    "type": "DDCPLGNR1",
    "value": 4
});

EXAMPLE RESPONSE
{
    "id": "3328",
    "type": "DDCPLGNR1",
    "typeDescription": "Pledge Number - Household Size",
    "value": 4,
    "isActive": true
}

```

Creates a new account pledge number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns an account pledge number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve an account pledge number

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/numbers/3328");

EXAMPLE RESPONSE
{
    "id": "3328",
    "type": "DDCPLGNR1",
    "typeDescription": "Pledge Number - Household Size",
    "value": 4,
    "isActive": true
}

```

Retrieves the details of an existing account pledge number. You need only supply the account pledge number id.

##### Arguments

* id (required) - The id of the account pledge number to retrieve.

##### Returns

Returns an account pledge number object if a valid id was provided.

#### Update an account pledge number

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/numbers/3328", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "3328",
    "type": "DDCPLGNR1",
    "typeDescription": "Pledge Number - Household Size",
    "value": 4,
    "isActive": false
}


```

Updates the specified account pledge number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the account pledge number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete an account pledge number

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/pledges/620701/numbers/3328", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge number. It cannot be undone.

##### Arguments

* id (required) - The id of the account pledge number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account pledge number id does not exist, this call returns an error.

#### List all account pledge numbers

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3328",
            "type": "DDCPLGNR1",
            "typeDescription": "Pledge Number - Household Size",
            "value": 4,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge numbers, starting at index offset. Each entry in the array is a separate account pledge number object. If no more account pledge numbers are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Premiums

#### Create an account pledge premium

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/premiums

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/premiums", {
    "warehouse": "UKWH",
    "product": "BK-5SLVG",
    "quantity": 1,
    "fulfillmentActivity": "1"
});

EXAMPLE RESPONSE
{
    "id": "1629",
    "warehouse": "UKWH",
    "product": "BK-5SLVG",
    "quantity": 1,
    "fulfillmentActivity": "1",
    "amount": null,
    "shippingMethod": null,
    "shippingAccount": null,
    "shippingInstructions": null,
    "documentNumber": null
}

```

Creates a new account pledge premium object.

##### Arguments

* warehouse (required) - The warehouse code of the premium.
* product (required) - The product code of the premium.
* quantity (required) - The quantity of the premium.
* fulfillmentActivity (required) - The fufillment activity of the premium. Must be a defined fulfillment activity.
* amount (optional) - The amount of the premium.
* shippingMethod (optional) - The shipping method of the premium.
* shippingAccount (optional) - The account number for shipping the premium.
* shippingInstructions (optional) - Instructions for shipping the premium.

##### Returns

Returns an account pledge premium object if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a quantity or a defined fulfillment activity).

#### Retrieve an account pledge premium

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/premiums/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/premiums/1629");

EXAMPLE RESPONSE
{
    "id": "1629",
    "warehouse": "UKWH",
    "product": "BK-5SLVG",
    "quantity": 1,
    "fulfillmentActivity": "1",
    "amount": null,
    "shippingMethod": null,
    "shippingAccount": null,
    "shippingInstructions": null,
    "documentNumber": 1142570
}

```

Retrieves the details of an existing account pledge premium. You need only supply the account pledge premium id.

##### Arguments

* id (required) - The id of the account pledge premium to retrieve.

##### Returns

Returns an account pledge premium object if a valid id was provided.

#### Update an account pledge premium

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/premiums/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/premiums/1629", {
    "quantity": 2
});

EXAMPLE RESPONSE
{
    "id": "1629",
    "warehouse": "UKWH",
    "product": "BK-5SLVG",
    "quantity": 2,
    "fulfillmentActivity": "1",
    "amount": null,
    "shippingMethod": null,
    "shippingAccount": null,
    "shippingInstructions": null,
    "documentNumber": 1142570
}


```

Updates the specified account pledge premium by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* warehouse (optional) - The warehouse code of the premium.
* product (optional) - The product code of the premium.
* quantity (optional) - The quantity of the premium.
* fulfillmentActivity (optional) - The fufillment activity of the premium. Must be a defined fulfillment activity.
* amount (optional) - The amount of the premium.
* shippingMethod (optional) - The shipping method of the premium.
* shippingAccount (optional) - The account number for shipping the premium.
* shippingInstructions (optional) - Instructions for shipping the premium.

##### Returns

Returns the account pledge premium object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined fulfillment activity or shipping method).

#### Delete an account pledge premium

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id/premiums/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/pledges/620701/premiums/1629", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge premium. It cannot be undone.

##### Arguments

* id (required) - The id of the account pledge premium to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account pledge premium id does not exist, this call returns an error.

#### List all account pledge premiums

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/premiums

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/premiums");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1629",
            "warehouse": "UKWH",
            "product": "1025",
            "productDescription": "Book Series",
            "quantity": 1,
            "fulfillmentActivity": "A",
            "fulfillmentActivityDescription": "Premium Released with Pledge Amount",
            "amount": null,
            "shippingMethod": null,
            "shippingAccount": null,
            "shippingInstructions": null,
            "documentNumber": 1142570,
            "shipDate": "2024-01-19",
            "trackingNumber": "555999y"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge premiums.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge premiums, starting at index offset. Each entry in the array is a separate account pledge premium object. If no more account pledge premiums are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Recurring Transactions

#### List all account pledge recurring transactions

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/recurringtransactions

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/33567/pledges/2241/recurringtransactions?all=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "total": 25.0000,
            "company": "4",
            "isDonation": true,
            "lastBatchNum": "10548",
            "lastDocNum": "686473",
            "linkedPledgeId": "",
            "id": "121516",
            "currency": "USD",
            "frequency": "Q",
            "start": "2016-06-14",
            "end": null,
            "numberCommitted": null,
            "numberRemaining": 0,
            "useOnDay": "3",
            "category": null,
            "shortComment": null,
            "source": "0727111",
            "sourceDescription": null,
            "contactMethod": null,
            "status": "E",
            "lastUsedDate": "2017-02-21",
            "assignedToAccessor": "",
            "assignedToAccessorDescription": null,
            "account": "33567",
            "accountName": null,
            "numberOfDeclines": 0
        },
        {...},
        {...}
    ]
}

```

Returns a paged response of all account recurring transaction headers that have recurring donations attributed to the provided pledge.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Returns

A dictionary with an items property that contains an array of all account recurring transaction headers that have recurring donations attributed to the provided pledge. Each entry in the array is a separate account recurring transaction object. If no more account recurring transactions are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Response

#### Retrieve an account pledge response

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/response

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/4402/response");

EXAMPLE RESPONSE
{
    "letter": "THANKYOU",
    "completionText": null,
    "address": "230529",
    "inserts": [],
    "status": "Y"
}

```

Retrieves the details of an existing account pledge response.

##### Returns

Returns the account pledge response object.

#### Update an account pledge response

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/response

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/response", {
    "address": "41"
});

EXAMPLE RESPONSE
{
    "letter": "THANKYOU",
    "completionText": null,
    "address": "41",
    "inserts": [],
    "status": "Y"
}


```

Updates the specified account pledge response by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* letter (optional) - The letter code of the response. Must be a defined letter code.
* completionText (optional) - The completion text of the response.
* address (optional) - The address id of the response.
* status (optional) - The status of the response. Must be a valid [response status](#response-status) value.

##### Returns

Returns the account pledge response object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined letter code).

### Account Pledge Response Paragraphs

#### Create an account pledge response paragraph

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/response/paragraphs

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/response/paragraphs", {
    "type": "PR1",
    "completionText": "Thank you for your support."
});

EXAMPLE RESPONSE
{
    "id": "53774",
    "type": "PR1",
    "completionText": "Thank you for your support."
}

```

Creates a new account pledge response paragraph object.

##### Arguments

* type (required) - The paragraph type. Must be a defined paragraph type.
* completionText (optional) - The completion text.

##### Returns

Returns an account pledge response paragraph object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined paragraph type).

#### Retrieve an account pledge response paragraph

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/response/paragraphs/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/response/paragraphs/53774");

EXAMPLE RESPONSE
{
    "id": "53774",
    "type": "PR1",
    "completionText": "Thank you for your support."
}

```

Retrieves the details of an existing account pledge response paragraph. You need only supply the account pledge response paragraph id.

##### Arguments

* id (required) - The id of the account pledge response paragraph to retrieve.

##### Returns

Returns an account pledge response paragraph object if a valid id was provided.

#### Update an account pledge response paragraph

```
DEFINITION
POST http://apiserver/accounts/:id/pledges/:id/response/paragraphs/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/pledges/620701/response/paragraphs/53774", {
    "type": "PR2"
});

EXAMPLE RESPONSE
{
    "id": "53774",
    "type": "PR2",
    "completionText": "Thank you for your support."
}


```

Updates the specified account pledge response paragraph by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The paragraph type. Must be a defined paragraph type.
* completionText (optional) - The completion text.

##### Returns

Returns the account pledge response paragraph object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined paragraph type).

#### Delete an account pledge response paragraph

```
DEFINITION
DELETE http://apiserver/accounts/:id/pledges/:id/response/paragraphs/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/pledges/620701/response/paragraphs/53774", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge response paragraph. It cannot be undone.

##### Arguments

* id (required) - The id of the account pledge response paragraph to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account pledge response paragraph id does not exist, this call returns an error.

#### List all account pledge response paragraphs

```
DEFINITION
GET http://apiserver/accounts/:id/pledges/:id/response/paragraphs

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/pledges/620701/response/paragraphs");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "53774",
            "type": "PR1",
            "completionText": "Thank you for your support."
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge response paragraphs.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge response paragraphs, starting at index offset. Each entry in the array is a separate account pledge response paragraph object. If no more account pledge response paragraphs are available, the resulting array will be empty. This request should never return an error.

### Account Products Received

#### List all account products received

```
DEFINITION
GET http://apiserver/accounts/:id/productsreceived

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/productsreceived");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "product": "0103D",
            "description": "Nature's Melody - DVD",
            "status": "B",
            "orderedQuantity": 1,
            "returnedQuantity": 0,
            "transactionDate": "2013-11-20",
            "shippingDate": null,
            "shippingAccount": "1483320",
            "shippingAccountName": "Henry Winkler",
            "shippingAddress": "8212 E Juneau Ave",
            "shippingMethod": "FREE",
            "shippingTrackingNumber": null,
            "shortComment": null,
            "transaction": "184688",
            "purchaserAccount": "1483320",
            "purchaserAccountName": "Henry Winkler",
            "priceCode": "EA",
            "amount": 10,
            "discount": 0,
            "fmv": 0,
            "cogs": 0,
            "expense": null,
            "committedDate": null,
            "backorderDate": "2014-01-07",
            "cancelDate": null,
            "returnDate": null,
            "source": "ABC08",
            "shippingMethodActual": null,
            "shippingCost": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account products received.

##### Returns

A dictionary with an items property that contains an array of up to limit account products received, starting at index offset. Each entry in the array is a separate account products received object. If no more account products received are available, the resulting array will be empty. This request should never return an error.

### Account Pledge Statements

#### Delete an account pledge statement

```
DEFINITION
DELETE http://apiserver/accounts/:accountId/pledgestatements/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16403/pledgestatements/10059", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account pledge statement. It cannot be undone.

##### Arguments

* accountId (required) - The account number for which to delete a pledge statement.
* id (required) - The id of the account pledge statement to be deleted.

##### Returns

Returns a `204 No Content` response on success.

#### List all account pledge statements

```
DEFINITION
GET http://apiserver/accounts/:id/pledgestatements

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/pledgestatements");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 3,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "4370",
            "accountNumber": "16230",
            "accountName": "Mr. John A Doe Jr.",
            "statementId": "1000000037",
            "start": "2014-09-11",
            "end": "2014-10-10",
            "source": null,
            "amount": 50,
            "paidDate": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledge statements. If the account is in a family, then all pledge statements within the family are returned.

##### Returns

A dictionary with an items property that contains an array of up to limit account pledge statements, starting at index offset. Each entry in the array is a separate account pledge statement object. If no more account pledge statements are available, the resulting array will be empty. This request should never return an error.

### Account Project Relationships

#### Create an account project relationship

```
DEFINITION
POST http://apiserver/accounts/:accountId/projectrelationships

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16403/projectrelationships", {
    "project": "110150"
});

EXAMPLE RESPONSE
{
    "id": "10059",
    "project": "110150",
    "projectDescription": "Hurricane Sandy Relief & Reconstruction"
}

```

Creates a new account project relationship.

##### Arguments

* project (required) - The project code to create a project relationship with.

##### Returns

Returns a account project relationship object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account project relationship

```
DEFINITION
GET http://apiserver/accounts/:accountId/projectrelationships/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16403/projectrelationships/10059");

EXAMPLE RESPONSE
{
    "id": "10059",
    "project": "110150",
    "projectDescription": "Hurricane Sandy Relief & Reconstruction"
}

```

Retrieves the details of an existing account project relationship. You need only supply the id.

##### Arguments

* id (required) - The id of the account project relationship to be retrieved.

#### Update an account project relationship

```
DEFINITION
POST http://apiserver/accounts/:accountId/projectrelationships/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16403/projectrelationships/10059", {
    "project": "LEADERSHIP"
});

EXAMPLE RESPONSE
{
    "id": "10059",
    "project": "LEADERSHIP",
    "projectDescription": "Leadership Development"
}

```

Updates the specified account project relationship by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* project (optional) - The project code to update the existing project relationship with.

##### Returns

Returns the account project relationship object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account project relationship

```
DEFINITION
DELETE http://apiserver/accounts/:accountId/projectrelationships/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16403/projectrelationships/10059", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a account project relationship. It cannot be undone.

##### Arguments

* id (required) - The id of the account project relationship to be deleted.

##### Returns

Returns a `204 No Content` response on success. If the account project relationship does not exist, this call returns an error.

#### List all account project relationships

```
DEFINITION
GET http://apiserver/accounts/:accountId/projectrelationships

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16403/projectrelationships");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10059",
            "project": "110150",
            "projectDescription": "Hurricane Sandy Relief & Reconstruction"
        },
        {...},
    ]
}

```

Returns a list of all account project relationships.

##### Returns

A dictionary with an items property that contains an array of up to limit account project relationships, starting at index offset. Each entry in the array is a separate account project relationship object. If no more account project relationships are available, the resulting array will be empty. This request should never return an error.

### Account Recurring Transactions

#### Create an account recurring transaction

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/recurringtransactions", {
    "isDonation":true,
    "start":"2016-03-01",
    "currency":"USD",
    "frequency":"M",
    "useOnDay":"1",
    "category":"ACTIVE",
    "company":"4",
    "source":"EV11CPCATL",
    "contactMethod":"EMAIL",
    "numberCommitted":12,
    "payment":{
        "type":"CC",
        "cardNumber":"4444333322221111",
        "expMonth":"01",
        "expYear":"2018",
        "cardName":"Dave Duncan",
        "paymentOrigin": "SE",
        "merchant": "BLUE"
    },
    "donations":[
        {
            "isDeductible":true,
            "isAnonymous":false,
            "pledgeCode":null,
            "accountPledge":null,
            "amount":15,
            "source":"1109A328",
            "project":"100101"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1000001125",
    "currency": "USD",
    "total": 15,
    "company": "4",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2016-03-01",
    "end": null,
    "numberCommitted": 12,
    "numberRemaining": 12,
    "useOnDay": "1",
    "useOnDayDescription": "1st of Month",
    "category": "ACTIVE",
    "shortComment": null,
    "source": "EV11CPCATL",
    "sourceDescription": null,
    "contactMethod": "EMAIL",
    "status": "Y",
    "isDonation": true,
    "linkedPledgeId": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "account": 29154,
    "accountName": "Calvin and Jackie Morris",
    "payment": {
        "id": null,
        "type": "CC",
        "typeDescription: "Credit Card",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2018",
        "cvv": null,
        "token": "120768345103",
        "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null,
        "savedPaymentId": 10,
        "savedPaymentName": "My Visa",
        "savedPaymentReferenceNumber": "VISA-1111 01/2018 Dave Duncan"
    }
}

```

Creates a new account recurring transaction object.

##### Arguments

* currency (required) - The currency of the recurring transaction.
* company (required) - The company code of the recurring transaction.
* payment (required) - The payment of the recurring transaction. The required and optional arguments for this object are identical to [transaction payment](#create-a-transaction-payment) except the amount cannot be specified.
* arPayments (optional) - An array of recurring transaction AR payment objects to be created as part of the recurring transaction. Must not be specified if `donations` is specified. See [recurring transaction AR payments](#create-an-account-recurring-transaction-ar-payment) for required fields.
* donations (optional) - An array of recurring transaction donation objects to be created as part of the recurring transaction. Must not be specified if `arPayments` is specified. See [recurring transaction donations](#create-an-account-recurring-transaction-donation) for required fields.
* frequency (required) - The frequency code of the recurring transaction. Must be a defined recurring transaction frequency code.
* start (optional) - The start date of the recurring transaction.
* end (optional) - The end date of the recurring transaction.
* numberCommitted (optional) - The number committed of the recurring transaction.
* useOnDay (required) - The use on day of the recurring transaction. Must be a defined recurring use on day code.
* category (required) - The category code of the recurring transaction. Must be a defined recurring transaction category code.
* shortComment (optional) - The short comment of the recurring transaction.
* source (required) - The source code of the recurring transaction. Must be a defined source code.
* contactMethod (optional) - The contact method of the recurring transaction.
* linkedPledgeId (optional) - The ID of the account pledge that the recurring transaction is linked to.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.

##### Returns

Returns an account recurring transaction object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined recurring transaction type).

#### Create an account recurring transaction with an existing CC or EFT token

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/recurringtransactions", {
    "isDonation":true,
    "start":"2016-03-01",
    "currency":"USD",
    "frequency":"M",
    "useOnDay":"1",
    "category":"ACTIVE",
    "company":"4",
    "source":"EV11CPCATL",
    "contactMethod":"EMAIL",
    "numberCommitted":12,
    "payment":{
        "type":"CC",
        "cardNumber":"4444xxxxxxxx1111",
        "expMonth":"01",
        "expYear":"2018",
        "cardName":"Dave Duncan",
        "token": "120476839615",
        "paymentOrigin": "SE",
        "merchant": "BLUE"
    },
    "donations":[
        {
            "isDeductible":true,
            "isAnonymous":false,
            "pledgeCode":null,
            "accountPledge":null,
            "amount":15,
            "source":"1109A328",
            "project":"100101"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1000001127",
    "currency": "USD",
    "total": 15,
    "company": "4",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2016-03-01",
    "end": null,
    "numberCommitted": 12,
    "numberRemaining": 12,
    "useOnDay": "1",
    "useOnDayDescription": "1st of Month",
    "category": "ACTIVE",
    "shortComment": null,
    "source": "EV11CPCATL",
    "sourceDescription": null,
    "contactMethod": "EMAIL",
    "status": "Y",
    "isDonation": true,
    "linkedPledgeId": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "account": 29154,
    "accountName": "Calvin and Jackie Morris",
    "payment": {
        "id": null,
        "type": "CC",
        "typeDescription: "Credit Card",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2018",
        "cvv": null,
        "token": "120476839615",
        "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null,
        "savedPaymentId": 0,
        "savedPaymentName": null,
        "savedPaymentReferenceNumber": null
    }
}


EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/recurringtransactions", {
    "isDonation":true,
    "start":"2016-03-01",
    "currency":"USD",
    "frequency":"M",
    "useOnDay":"1",
    "category":"ACTIVE",
    "company":"PAYCONEX",
    "source":"EV11CPCATL",
    "contactMethod":"EMAIL",
    "numberCommitted":12,
    "payment":{
        "type":"EFT",
        "accountType":"CHECKING",
        "accountNumber":"xxxxx1321",
        "token": "000000201261",
        "paymentOrigin": "SE",
        "merchant": "BLUE"
    },
    "donations":[
        {
            "isDeductible":true,
            "isAnonymous":false,
            "pledgeCode":null,
            "accountPledge":null,
            "amount":15,
            "source":"1109A328",
            "project":"100101"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1000001132",
    "currency": "USD",
    "total": 15,
    "company": "PAYCONEX",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2016-03-01",
    "end": null,
    "numberCommitted": 12,
    "numberRemaining": 12,
    "useOnDay": "1",
    "useOnDayDescription": "1st of Month",
    "category": "ACTIVE",
    "shortComment": null,
    "source": "EV11CPCATL",
    "sourceDescription": null,
    "contactMethod": "EMAIL",
    "status": "Y",
    "isDonation": true,
    "linkedPledgeId": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "account": 29154,
    "accountName": "Calvin and Jackie Morris",
    "payment": {
        "id": null,
        "type": "EFT",
        "typeDescription: "Electronic Funds Transfer",
        "amount": null,
        "merchant": "BLUE",
        "routingNumber": "xxxxxxxxx",
        "accountNumber": "xxxxx1321",
        "accountType": "CHECKING",
        "token": "000000201261",
        "referenceNumber": "xxxxx1321-C",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null,
        "savedPaymentId": 0,
        "savedPaymentName": null,
        "savedPaymentReferenceNumber": null
    }
}

```

Creates a new account recurring transaction object.

##### Arguments

If payment `type` is `CC`, then provide:

* cardNumber - credit card mask
* expMonth - expiration month
* expYear - expiration year
* cardName - the name on card
* token - the CC token which is a reusable token received from the payment gateway
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

If payment `type` is `EFT`, then provide:

* accountType - either `CHECKING` or `SAVINGS`
* accountNumber - the mask of the bank account number
* token - the EFT token which is a reusable token received from the payment gateway
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

Other arguments are the same as [create an account recurring transaction](#create-an-account-recurring-transaction).

##### Returns

Returns an account recurring transaction object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined recurring transaction type).

#### Create an account recurring transaction using a hosted payment page token

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/recurringtransactions", {
    "isDonation":true,
    "start":"2016-03-01",
    "currency":"USD",
    "frequency":"M",
    "useOnDay":"1",
    "category":"ACTIVE",
    "company":"4",
    "source":"EV11CPCATL",
    "contactMethod":"EMAIL",
    "numberCommitted":12,
    "payment": {
        "hostedPageToken": "1234567890",
        "cardName": "Dave Duncan",
        "type": "CC",
        "paymentOrigin": "SE",
        "merchant": "CCONNECT"
    }
    "donations":[
        {
            "isDeductible":true,
            "isAnonymous":false,
            "pledgeCode":null,
            "accountPledge":null,
            "amount":15,
            "source":"1109A328",
            "project":"100101"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1000001127",
    "currency": "USD",
    "total": 15,
    "company": "4",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2016-03-01",
    "end": null,
    "numberCommitted": 12,
    "numberRemaining": 12,
    "useOnDay": "1",
    "useOnDayDescription": "1st of Month",
    "category": "ACTIVE",
    "shortComment": null,
    "source": "EV11CPCATL",
    "sourceDescription": null,
    "contactMethod": "EMAIL",
    "status": "Y",
    "isDonation": true,
    "linkedPledgeId": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "account": 29154,
    "accountName": "Calvin and Jackie Morris",
    "payment": {
        "id": null,
        "type": "CC",
        "typeDescription: "Credit Card",
        "amount": null,
        "merchant": "CCONNECT",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2018",
        "cvv": null,
        "token": "120476839615",
        "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null,
        "savedPaymentId": 0,
        "savedPaymentName": null,
        "savedPaymentReferenceNumber": null
    }
}


```

Creates a new account recurring transaction object using a hosted payment page token.

##### Arguments

If payment `type` is `CC`, then provide:

* hostedPageToken - the hosted payment page token returned by the payment gateway
* cardName - the name on card
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

Other arguments are the same as [create an account recurring transaction](#create-an-account-recurring-transaction).

##### Returns

Returns an account recurring transaction object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined recurring transaction type).

#### Create an account recurring transaction using a saved payment

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/recurringtransactions", {
    "isDonation":true,
    "start":"2016-03-01",
    "currency":"USD",
    "frequency":"M",
    "useOnDay":"1",
    "category":"ACTIVE",
    "company":"4",
    "source":"EV11CPCATL",
    "contactMethod":"EMAIL",
    "numberCommitted":12,
    "payment": {
        "savedPaymentId": "10"
    }
    "donations":[
        {
            "isDeductible":true,
            "isAnonymous":false,
            "pledgeCode":null,
            "accountPledge":null,
            "amount":15,
            "source":"1109A328",
            "project":"100101"
        }
    ]
});

EXAMPLE RESPONSE
{
    "id": "1000001127",
    "currency": "USD",
    "total": 15,
    "company": "4",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2016-03-01",
    "end": null,
    "numberCommitted": 12,
    "numberRemaining": 12,
    "useOnDay": "1",
    "useOnDayDescription": "1st of Month",
    "category": "ACTIVE",
    "shortComment": null,
    "source": "EV11CPCATL",
    "sourceDescription": null,
    "contactMethod": "EMAIL",
    "status": "Y",
    "isDonation": true,
    "linkedPledgeId": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "account": 29154,
    "accountName": "Calvin and Jackie Morris",
    "payment": {
        "id": null,
        "type": "CC",
        "typeDescription: "Credit Card",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2018",
        "cvv": null,
        "token": "120476839615",
        "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null,
        "savedPaymentId": 10,
        "savedPaymentName": "My Visa",
        "savedPaymentReferenceNumber": "VISA-1111 01/2018 Dave Duncan"
    }
}


```

Creates a new account recurring transaction object using a saved payment.

##### Arguments

* savedPaymentId - the saved payment id of the payment to use to create the recurring

Other arguments are the same as [create an account recurring transaction](#create-an-account-recurring-transaction).

##### Returns

Returns an account recurring transaction object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined recurring transaction type).

#### Retrieve an account recurring transaction

```
DEFINITION
GET http://apiserver/accounts/:id/recurringtransactions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/29155/recurringtransactions/1000001125");

EXAMPLE RESPONSE
{
    "id": "1000001125",
    "currency": "USD",
    "total": 15,
    "company": "4",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2016-03-01",
    "end": null,
    "numberCommitted": 12,
    "numberRemaining": 12,
    "useOnDay": "1",
    "useOnDayDescription": "1st of Month",
    "category": "ACTIVE",
    "shortComment": null,
    "source": "EV11CPCATL",
    "sourceDescription": null,
    "contactMethod": "EMAIL",
    "status": "Y",
    "isDonation": true,
    "linkedPledgeId": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "account": 29154,
    "accountName": "Calvin and Jackie Morris",
    "payment": {
        "id": null,
        "type": "CC",
        "typeDescription: "Credit Card",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2018",
        "cvv": null,
        "token": "120768345103",
        "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null,
        "savedPaymentId": 10,
        "savedPaymentName": "My Visa",
        "savedPaymentReferenceNumber": "VISA-1111 01/2018 Dave Duncan",
        "billingAddressId": 100121,
        "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242"
    }
}

```

Retrieves the details of an existing account recurring transaction. You need only supply the account recurring transaction id.

##### Arguments

* id (required) - The id of the account recurring transaction to retrieve.

##### Returns

Returns an account recurring transaction object if a valid id was provided.

#### Update an account recurring transaction

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/recurringtransactions/1000001125", {
    "end": "2017-03-01",
    "payment":{
        "type":"CC",
        "expMonth":"01",
        "expYear":"2020",
        "token": "120768345103",
        "updateExpOnly": true,
        "paymentOrigin": "SE",
        "merchant": "BLUE"
    }
});

EXAMPLE RESPONSE
{
    "id": "1000001125",
    "currency": "USD",
    "total": 15,
    "company": "4",
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2016-03-01",
    "end": "2017-03-01",
    "numberCommitted": 12,
    "numberRemaining": 12,
    "useOnDay": "1",
    "useOnDayDescription": "1st of Month",
    "category": "ACTIVE",
    "shortComment": null,
    "source": "EV11CPCATL",
    "sourceDescription": null,
    "contactMethod": "EMAIL",
    "status": "Y",
    "isDonation": true,
    "linkedPledgeId": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "account": 29154,
    "accountName": "Calvin and Jackie Morris",
    "payment": {
        "id": null,
        "type": "CC",
        "typeDescription: "Credit Card",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2020",
        "cvv": null,
        "token": "120768345103",
        "referenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null,
        "savedPaymentId": 10,
        "savedPaymentName": "My Visa",
        "savedPaymentReferenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "billingAddressId": 100121,
        "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242"
    }
}


```

Updates the specified account recurring transaction by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* donations (required if isDonation = true) - the collection of donations on the recurring transaction.
* arPayments (required if isDonation = false) - the collection of ar payments on the recurring transaction.
* currency (optional) - The currency of the recurring transaction.
* company (optional) - The company code of the recurring transaction.
* payment (optional) - The payment of the recurring transaction.
* frequency (optional) - The frequency code of the recurring transaction. Must be a defined recurring transaction frequency code.
* start (optional) - The start date of the recurring transaction.
* end (optional) - The end date of the recurring transaction.
* numberCommitted (optional) - The number committed of the recurring transaction.
* useOnDay (optional) - The use on day of the recurring transaction. Must be a defined recurring use on day code.
* category (optional) - The category code of the recurring transaction. Must be a defined recurring transaction category code.
* shortComment (optional) - The short comment of the recurring transaction.
* source (optional) - The source code of the recurring transaction. Must be a defined source code.
* contactMethod (optional) - The contact method of the recurring transaction.
* status (optional) - The status of the recurring transaction.
* updateStatusOnly (optional) - Indicates whether or not we should only update the recurring transaction status. If true, all other fields are ignored.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.
* newTokenRequired (optional) - Indicates whether or not the recurring transaction need to request a new payment gateway token.
* studioOnlineStore (optional) - StudioOnline store Id; when provided, causes any changes in frequency made to the recurring to also be made to any associated pledges.
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

##### Returns

Returns the account recurring transaction object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined recurring transaction type or recurring transaction type value).

#### Delete an account recurring transaction

```
DEFINITION
DELETE http://apiserver/accounts/:id/recurringtransactions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/29155/recurringtransactions/1000001125", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account recurring transaction. It cannot be undone.

##### Arguments

* id (required) - The id of the account recurring transaction to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account recurring transaction id does not exist, this call returns an error.

#### List all account recurring transactions

```
DEFINITION
GET http://apiserver/accounts/:id/recurringtransactions

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/29155/recurringtransactions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000001125",
            "currency": "USD",
            "total": 15,
            "company": "4",
            "frequency": "M",
            "frequencyDescription": "Monthly",
            "start": "2016-03-01",
            "end": "2017-03-01",
            "numberCommitted": 12,
            "numberRemaining": null,
            "useOnDay": "1",
            "useOnDayDescription": "1st of Month",
            "category": "ACTIVE",
            "shortComment": null,
            "source": "EV11CPCATL",
            "sourceDescription": null,
            "contactMethod": "EMAIL",
            "status": "Y",
            "isDonation": true,
            "linkedPledgeId": null,
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null,
            "account": 29154,
            "accountName": "Calvin and Jackie Morris",
            "payment": {
                "id": null,
                "type": "CC",
                "typeDescription: "Credit Card",
                "amount": null,
                "merchant": "BLUE",
                "cardNumber": "VISA-1111",
                "cardName": "Dave Duncan",
                "expMonth": "01",
                "expYear": "2018",
                "cvv": null,
                "token": "120768345103",
                "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
                "deposit": null,
                "depositStatus": null,
                "depositDate": null,
                "savedPaymentId": 10,
                "savedPaymentName": "My Visa",
                "savedPaymentReferenceNumber": "VISA-1111 01/2018 Dave Duncan",
                "billingAddressId": 100121,
                "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242"
            }
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account recurring transactions.

##### Arguments

* linkedPledgeId (optional) - The id of the pledge that the recurring transaction should be associated with.

##### Returns

A dictionary with an items property that contains an array of up to limit account recurring transactions, starting at index offset. Each entry in the array is a separate account recurring transaction object. If no more account recurring transactions are available, the resulting array will be empty. This request should never return an error.

### Account Recurring Transaction AR Payments

#### Create an account recurring transaction AR payment

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions/:id/arpayments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/17796/recurringtransactions/21801/arpayments", {
    "amount": 5,
    "transaction": "53005"
});

EXAMPLE RESPONSE
{
    "id": "18",
    "amount": 5,
    "transaction": "53005"
}

```

Creates a new account recurring transaction AR payment object.

##### Arguments

* amount (required) - The amount of the recurring transaction AR payment.
* transaction (required) - The document number to which the recurring transaction AR payment should be applied.

##### Returns

Returns an account recurring transaction AR payment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined recurring transaction AR payment type).

#### Retrieve an account recurring transaction AR payment

```
DEFINITION
GET http://apiserver/accounts/:id/recurringtransactions/:id/arpayments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/17796/recurringtransactions/21801/arpayments/18");

EXAMPLE RESPONSE
{
    "id": "18",
    "amount": 5,
    "transaction": "53005"
}

```

Retrieves the details of an existing account recurring transaction AR payment. You need only supply the account recurring transaction AR payment id.

##### Arguments

* id (required) - The id of the account recurring transaction AR payment to retrieve.

##### Returns

Returns an account recurring transaction AR payment object if a valid id was provided.

#### Update an account recurring transaction AR payment

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions/:id/arpayments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/17796/recurringtransactions/21801/arpayments/18", {
    "amount": 10
});

EXAMPLE RESPONSE
{
    "id": "18",
    "amount": 10,
    "transaction": "53005"
}


```

Updates the specified account recurring transaction AR payment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* amount (optional) - The amount of the recurring transaction AR payment.
* transaction (optional) - The document number to which the recurring transaction AR payment should be applied.

##### Returns

Returns the account recurring transaction AR payment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined recurring transaction AR payment type or recurring transaction AR payment type value).

#### Delete an account recurring transaction AR payment

```
DEFINITION
DELETE http://apiserver/accounts/:id/recurringtransactions/:id/arpayments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/17796/recurringtransactions/21801/arpayments/18", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account recurring transaction AR payment. It cannot be undone.

##### Arguments

* id (required) - The id of the account recurring transaction AR payment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account recurring transaction AR payment id does not exist, this call returns an error.

#### List all account recurring transaction AR payments

```
DEFINITION
GET http://apiserver/accounts/:id/recurringtransactions/:id/arpayments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/17796/recurringtransactions/21801/arpayments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "18",
            "amount": 5,
            "transaction": "53005"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account recurring transaction AR payments.

##### Returns

A dictionary with an items property that contains an array of up to limit account recurring transaction AR payments, starting at index offset. Each entry in the array is a separate account recurring transaction AR payment object. If no more account recurring transaction AR payments are available, the resulting array will be empty. This request should never return an error.

### Account Recurring Transaction Donations

#### Create an account recurring transaction donation

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions/:id/donations

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/recurringtransactions/27054/donations", {
    "amount": 1,
    "source": "ABC08",
    "project": "220000",
});

EXAMPLE RESPONSE
{
    "id": "269345",
    "amount": 1,
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "relatedAccount": null,
    "accountPledge": null,
    "pledgeCode": null,
    "isDeductible": true,
    "isAnonymous": false,
    "shortComment": null,
    "mediaOutlet": null
}

```

Creates a new account recurring transaction donation object.

##### Arguments

* amount (required) - The amount of the recurring transaction donation.
* source (required) - The source code of the recurring transaction donation.
* project (required) - The project code of the recurring transaction donation.
* subaccount (optional) - The subaccount code of the recurring transaction donation.
* relatedAccount (optional) - The associated account number of the recurring transaction donation.
* accountPledge (optional) - The account pledge id of the recurring transaction donation.
* isDeductible (optional) - Whether or not the recurring transaction donation is deductible. If not specified, will default to true.
* isAnonymous (optional) - Whether or not the recurring transaction donation is anonymous. If not specified, will default to false.
* shortComment (optional) - The short comment of the recurring transaction donation.
* mediaOutlet (optional) - The media outlet id of the recurring transaction donation.

##### Returns

Returns an account recurring transaction donation object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined recurring transaction donation type).

#### Retrieve an account recurring transaction donation

```
DEFINITION
GET http://apiserver/accounts/:id/recurringtransactions/:id/donations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/recurringtransactions/27054/donations/269345");

EXAMPLE RESPONSE
{
    "id": "269345",
    "amount": 1,
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "mediaOutlet": null,
    "relatedAccount": null,
    "accountPledge": null,
    "pledgeCode": null,
    "isDeductible": true,
    "isAnonymous": false,
    "shortComment": null,
    "projectData": null,
    "pledgeData": null
}

```

Retrieves the details of an existing account recurring transaction donation. You need only supply the account recurring transaction donation id.

##### Arguments

* id (required) - The id of the account recurring transaction donation to retrieve.
* store (optional) - StudioOnline store Id; when provided, returns json that represents the project and pledge.

##### Returns

Returns an account recurring transaction donation object if a valid id was provided.

#### Update an account recurring transaction donation

```
DEFINITION
POST http://apiserver/accounts/:id/recurringtransactions/:id/donations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/recurringtransactions/27054/donations/269345", {
    "amount": 15
});

EXAMPLE RESPONSE
{
    "id": "269345",
    "amount": 15,
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "mediaOutlet": null,
    "relatedAccount": null,
    "accountPledge": null,
    "pledgeCode": null,
    "isDeductible": true,
    "isAnonymous": false,
    "shortComment": null
}


```

Updates the specified account recurring transaction donation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* amount (optional) - The amount of the recurring transaction donation.
* source (optional) - The source code of the recurring transaction donation.
* project (optional) - The project code of the recurring transaction donation.
* subaccount (optional) - The subaccount code of the recurring transaction donation.
* relatedAccount (optional) - The associated account number of the recurring transaction donation.
* accountPledge (optional) - The account pledge id of the recurring transaction donation.
* isDeductible (optional) - Whether or not the recurring transaction donation is deductible. If not specified, will default to true.
* isAnonymous (optional) - Whether or not the recurring transaction donation is anonymous. If not specified, will default to false.
* shortComment (optional) - The short comment of the recurring transaction donation.
* mediaOutlet (optional) - The media outlet id of the recurring transaction donation.

##### Returns

Returns the account recurring transaction donation object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined recurring transaction donation type or recurring transaction donation type value).

#### Delete an account recurring transaction donation

```
DEFINITION
DELETE http://apiserver/accounts/:id/recurringtransactions/:id/donations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/recurringtransactions/27054/donations/269345", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account recurring transaction donation. It cannot be undone.

##### Arguments

* id (required) - The id of the account recurring transaction donation to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account recurring transaction donation id does not exist, this call returns an error.

#### List all account recurring transaction donations

```
DEFINITION
GET http://apiserver/accounts/:id/recurringtransactions/:id/donations

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/recurringtransactions/27054/donations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "269345",
            "amount": 1,
            "source": "ABC08",
            "project": "220000",
            "subaccount": null,
            "mediaOutlet": null,
            "relatedAccount": null,
            "accountPledge": null,
            "pledgeCode": null,
            "isDeductible": true,
            "isAnonymous": false,
            "shortComment": null,
            "projectData": null,
            "pledgeData": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account recurring transaction donations.

##### Arguments

* store (optional) - StudioOnline store Id; when provided, returns json that represents the project and pledge.

##### Returns

A dictionary with an items property that contains an array of up to limit account recurring transaction donations, starting at index offset. Each entry in the array is a separate account recurring transaction donation object. If no more account recurring transaction donations are available, the resulting array will be empty. This request should never return an error.

### Account Recurring Transaction Notes

#### Create an account recurring transaction note

```
DEFINITION
POST http://apiserver/account/:id/recurringtransactions/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16230/recurringtransactions/1000000458/notes", {
    "type": "DDCNOTETYP",
    "shortComment": "Alert Note"
});

EXAMPLE RESPONSE
{
    {
        "headerId": "1000000458",
        "id": "40",
        "type": "DDCNOTETYP",
        "typeDescription": "Account Recurring Note",
        "shortComment": "Alert Note",
        "longComment": null
    }
}

```

Creates a new account recurring transaction note.

##### Arguments

* type (required) - Type for the account recurring transaction note.
* shortComment (optional) - Short comment for the account recurring transaction note.
* longComment (optional) - Long comment for the account recurring transaction note.

##### Returns

A new account recurring transaction note object if a valid account id and recurring transaction id are provided.

#### Retrieve an account recurring transaction note

```
DEFINITION
GET http://apiserver/account/:id/recurringtransactions/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/recurringtransactions/1000000458/notes/40");

EXAMPLE RESPONSE
{
    {
        "headerId": "1000000458",
        "id": "40",
        "type": "DDCNOTETYP",
        "typeDescription": "Account Recurring Note",
        "shortComment": "Alert Note",
        "longComment": null
    }
}

```

Returns a single account recurring transaction note object.

##### Returns

An account recurring transaction note object if the provided account id, recurring transaction id, and note id are valid.

#### Update an account recurring transaction note

```
DEFINITION
POST http://apiserver/account/:id/recurringtransactions/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16230/recurringtransactions/1000000458/notes/40", {
    "longComment": "Follow up on 12/1"
});

EXAMPLE RESPONSE
{
    {
        "headerId": "1000000458",
        "id": "40",
        "type": "DDCNOTETYP",
        "typeDescription": "Account Recurring Note",
        "shortComment": "Alert Note",
        "longComment": "Follow up on 12/1"
    }
}

```

Updates an existing account recurring transaction note object if all provided id's are valid.

##### Arguments

* type (optional) - Type for the account recurring transaction note.
* shortComment (optional) - Short comment for the account recurring transaction note.
* longComment (optional) - Long comment for the account recurring transaction note.

##### Returns

Returns the account recurring transaction note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined recurring transaction note type).

#### Delete an account recurring transaction note

```
DEFINITION
DELETE http://apiserver/account/:id/recurringtransactions/:id/notes/:id

EXAMPLE REQUEST
$.delete("http://localhost:49195/accounts/16230/recurringtransactions/1000000458/notes/40");

EXAMPLE RESPONSE
204 NO CONTENT

```

##### Returns

Returns a 204 No Content response on success. If the account recurring transaction note id does not exist, this call returns an error.

#### List all account recurring transaction notes

```
DEFINITION
GET http://apiserver/account/:id/recurringtransactions/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/recurringtransactions/1000000458/notes");

EXAMPLE RESPONSE
{
    {
        "paging": {
            "limit": 10,
            "offset": 0,
            "total": 2
        },
        "items": [
            {
                "headerId": "1000000458",
                "id": "40",
                "type": "SAMPLENOTE",
                "typeDescription": "Sample Account Recurring Note",
                "shortComment": "Alert Note",
                "longComment": null
            },
            {...}
        ]
    }
}

```

Returns all account recurring transaction notes associated with the provided account recurring transaction.

##### Returns

A dictionary with an items property that contains an array of up to limit account recurring transaction notes, starting at index offset. Each entry in the array is a separate account recurring transaction note object. If no more account recurring transaction notes are available, the resulting array will be empty. This request should never return an error.

### Account Related Giving

#### List all account related giving

```
DEFINITION
GET http://apiserver/accounts/:id/relatedgiving

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/relatedgiving");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "176159",
            "date": "2014-10-28",
            "transaction": "134029",
            "account": "16230",
            "accountName": "Mr. John A Doe Jr.",
            "amount": 15,
            "letter": "DTYDC",
            "source": "EV11CPCATL",
            "sourceDescription": "Pastor's Conf March 2011 Atlanta",
            "elementGroup": "PC11C",
            "elementGroupDescription": "Pastor's Conference March 2011",
            "project": "110100",
            "projectDescription": "FCA Dallas Project",
            "pledgeCode": "082011",
            "pledgeDescription": "August 2011 Fund",
            "isDeductible": true,
            "isAnonymous": false,
            "shortComment": "anual attendee",
            "response": {
                "id": "358471",
                "communicationType": "RECEIPT",
                "method": null,
                "status": "Y",
                "profileGroup": null,
                "printGroup": null,
                "printDate": null
            }
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account related givings.

##### Returns

A dictionary with an items property that contains an array of up to limit account related givings, starting at index offset. Each entry in the array is a separate account related giving object. If no more account related givings are available, the resulting array will be empty. This request should never return an error.

### Account Related Pledges

#### List all account related pledges

```
DEFINITION
GET http://apiserver/accounts/:id/relatedpledges

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/151065/relatedpledges");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "pledge": "MSN1201TST",
            "description": "2008 December Mission Pledge",
            "totalAmount": 366,
            "status": "P",
            "infoAndUpdatesAccount": "151065",
            "stmtAndAckAccount": "162"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account related pledges.

##### Returns

A dictionary with an items property that contains an array of up to limit account related pledges, starting at index offset. Each entry in the array is a separate account related pledge object. If no more account related pledges are available, the resulting array will be empty. This request should never return an error.

##### Arguments

* status () - Filter list by exact match in pledge status

### Account Relationships

#### Create an account relationship

```
DEFINITION
POST http://apiserver/accounts/:id/relationships

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/relationships", {
    "type": "BUSINESS",
    "relatedAccount": "114",
    "relatedType": "OWNER"
});

EXAMPLE RESPONSE
{
    "id": "26937",
    "type": "BUSINESS",
    "typeDescription": "Business",
    "relatedAccount": "114",
    "relatedAccountName": "Carol Costa"
    "relatedType": "OWN",
    "relatedTypeDescription": "Owner",
    "isForRelatedGiving": false,
}

```

Creates a new account relationship object.

##### Arguments

* type (required) - The relationship type. Must be a defined relationship type.
* relatedAccount (required) - The account number of the related account.
* relatedType (required) - The relationship type of the related account. Must be a defined relationship type.
* isForRelatedGiving (optional) - Whether or not the relationship is for related giving.

##### Returns

Returns an account relationship object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined relationship type).

#### Retrieve an account relationship

```
DEFINITION
GET http://apiserver/accounts/:id/relationships/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/relationships/26937");

EXAMPLE RESPONSE
{
    "id": "26937",
    "type": "BUSINESS",
    "typeDescription": "Business",
    "relatedAccount": "114",
    "relatedAccountName": "Carol Costa"
    "relatedType": "OWN",
    "relatedTypeDescription": "Owner",
    "isForRelatedGiving": false
}

```

Retrieves the details of an existing account relationship. You need only supply the account relationship id.

##### Arguments

* id (required) - The id of the account relationship to retrieve.

##### Returns

Returns an account relationship object if a valid id was provided.

#### Update an account relationship

```
DEFINITION
POST http://apiserver/accounts/:id/relationships/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/relationships/26937", {
    "isForRelatedGiving": true
});

EXAMPLE RESPONSE
{
    "id": "26937",
    "type": "BUSINESS",
    "typeDescription": "Business",
    "relatedAccount": "114",
    "relatedAccountName": "Carol Costa"
    "relatedType": "OWN",
    "relatedTypeDescription": "Owner",
    "isForRelatedGiving": true
}


```

Updates the specified account relationship by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The relationship type. Must be a defined relationship type.
* relatedAccount (optional) - The account number of the related account.
* relatedType (optional) - The relationship type of the related account. Must be a defined relationship type.
* isForRelatedGiving (optional) - Whether or not the relationship is for related giving.

##### Returns

Returns the account relationship object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined relationship type or relationship type value).

#### Delete an account relationship

```
DEFINITION
DELETE http://apiserver/accounts/:id/relationships/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/relationships/26937", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account relationship. It cannot be undone.

##### Arguments

* id (required) - The id of the account relationship to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account relationship id does not exist, this call returns an error.

#### List all account relationships

```
DEFINITION
GET http://apiserver/accounts/:id/relationships

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/relationships");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "26937",
            "type": "BUSINESS",
            "typeDescription": "Business",
            "relatedAccount": "114",
            "relatedAccountName": "Carol Costa"
            "relatedType": "OWN",
            "relatedTypeDescription": "Owner",
            "isForRelatedGiving": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account relationships.

##### Arguments

* includeFamilyRelationships (optional) - Whether or not to include all the relationships to family members as well.

##### Returns

A dictionary with an items property that contains an array of up to limit account relationships, starting at index offset. Each entry in the array is a separate account relationship object. If no more account relationships are available, the resulting array will be empty. This request should never return an error.

### Account Relationship Pledges

#### List all account relationship pledges

```
DEFINITION
GET http://apiserver/accounts/:id/relationshippledges

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/relationshippledges?relationshipType=BO&relationshipRelatedType=BE");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "relationship": {
                "id": "343968",
                "type": "BO",
                "typeDescription": "Business Owner",
                "relatedAccountNumber": "85695",
                "relatedAccountName": "Randall Sumter",
                "relatedAccount": {
                    "formattedName": "Randall Sumter",
                    "title": null,
                    "firstName": "Randall",
                    "middleName": null,
                    "lastName": "Sumter",
                    "suffix": null,
                    "organizationName": null
                },
                "relatedType": "BE",
                "relatedTypeDescription": "Business Employee",
                "isForRelatedGiving": true,
                "accountNumber": 85695
            },
            "accountPledge": {
                "id": "4270",
                "pledge": "Generic Pledge w Project",
                "pledgeDescription": null,
                "type": "PROJECT",
                "currency": "USD",
                "totalAmount": 44.0000,
                "amountPerGift": 23.0000,
                "numberPledged": 0,
                "totalAmountDonated": 0.0000,
                "totalNumberDonated": 0,
                "totalRelatedAmountDonated": null,
                "frequency": "M",
                "frequencyDescription": "Monthly",
                "start": "2015-01-08",
                "end": "2999-01-08",
                "isOpenEnded": false,
                "source": "0_A",
                "sourceDescription": "Zero",
                "elementGroup": null,
                "elementGroupDescription": null,
                "status": "A",
                "isActive": null,
                "cancelReason": null,
                "cancelDate": null,
                "numberOfAdjustmentMonths": null,
                "stmtAndAckAccount": "0",
                "stmtAndAckAccountName": null,
                "infoAndUpdatesAccount": "0",
                "infoAndUpdatesAccountName": null,
                "paidThroughDate": null,
                "originalPledge": "4270",
                "company": "1",
                "account": "85696",
                "accountName": "Admiral Fran Joffry Bingleson Jr",
                "defaultProjectCode": "10",
                "response": {
                    "id": 2093151,
                    "method": null,
                    "type": "PLDGACK",
                    "profileGroup": null,
                    "printGroup": null,
                    "printDate": null,
                    "paragraphs": [],
                    "letter": "ABC",
                    "isAutoAssigned": false,
                    "completionText": null,
                    "address": "1000097454",
                    "inserts": null,
                    "status": "Y"
                },
                "assignedToAccessor": "0",
                "assignedToAccessorDescription": null,
                "hasRecurring": true
            }
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account relationship pledges.

##### Arguments

* company (optional) - The company that the account pledge should be in.
* excludeResponseProperty (optional; default is `false`) - Skips populating the `response` property which is somewhat of an expensive opperation due to current implementation details. This argument is intended for very specific scenarios where the account pledge response information is not necessary.
* relationshipType (optional) - The relationship type that the requested account should have to the accounts on the returned pledges.
* relationshipRelatedType (optional) - The relationship type that the accounts should have for the accounts on the returned pledges.
* store (optional) - The store record id that the returned pledges are published to.

##### Returns

A dictionary with an items property that contains an array of up to limit account relationship pledges, starting at index offset. Each entry in the array is a separate account relationship pledge object. If no more account relationship pledges are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Resolve Account Duplicates

#### Resolve Account Duplicates

```
DEFINITION
POST http://apiserver/studioonlineresolveaccountduplicates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineresolveaccountduplicates/1483320");

```

Processes account duplicates for the account.

##### Returns

Returns an status code OK if the call succeeded.

### Account Salutations

#### Create an account salutation

```
DEFINITION
POST http://apiserver/accounts/:id/salutations

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/salutations", {
    "type": "INFORMAL",
    "salutation": "Henry"
});

EXAMPLE RESPONSE
{
    "id": "1795",
    "type": "INFORMAL",
    "salutation": "Henry",
    "isPrimary": false,
    "functionalCategory": null,
    "functionalCategoryDescription": null
}

```

Creates a new account salutation object.

##### Arguments

* type (required) - The salutation type. Must be a defined salutation type.
* salutation (required) - The salutation.
* isPrimary (optional) - Whether or not the salutation is the primary salutation for the account.
* isActive (optional) - Whether or not the salutation is active.
* functionalCategory (optional) - The functional category of the salutation.

##### Returns

Returns an account salutation object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined salutation type).

#### Retrieve an account salutation

```
DEFINITION
GET http://apiserver/accounts/:id/salutations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/salutations/1795");

EXAMPLE RESPONSE
{
    "id": "1795",
    "type": "INFORMAL",
    "salutation": "Henry",
    "isPrimary": false,
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Donor Ministries"
}

```

Retrieves the details of an existing account salutation. You need only supply the account salutation id.

##### Arguments

* id (required) - The id of the account salutation to retrieve.

##### Returns

Returns an account salutation object if a valid id was provided.

#### Update an account salutation

```
DEFINITION
POST http://apiserver/accounts/:id/salutations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/salutations/1795", {
    "isPrimary": true
});

EXAMPLE RESPONSE
{
    "id": "1795",
    "type": "INFORMAL",
    "salutation": "Henry",
    "isPrimary": true,
    "functionalCategory": "DM",
    "functionalCategoryDescription": "Donor Ministries"
}


```

Updates the specified account salutation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The salutation type. Must be a defined salutation type.
* salutation (optional) - The salutation.
* isPrimary (optional) - Whether or not the salutation is the primary salutation for the account.
* isActive (optional) - Whether or not the salutation is active.
* functionalCategory (optional) - The functional category of the salutation.

##### Returns

Returns the account salutation object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined salutation type or salutation type value).

#### Delete an account salutation

```
DEFINITION
DELETE http://apiserver/accounts/:id/salutations/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/salutations/1795", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account salutation. It cannot be undone.

##### Arguments

* id (required) - The id of the account salutation to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account salutation id does not exist, this call returns an error.

#### List all account salutations

```
DEFINITION
GET http://apiserver/accounts/:id/salutations

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/salutations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1795",
            "type": "INFORMAL",
            "salutation": "Henry",
            "isPrimary": true,
            "functionalCategory": "DM",
            "functionalCategoryDescription": "Donor Ministries"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account salutations.

##### Returns

A dictionary with an items property that contains an array of up to limit account salutations, starting at index offset. Each entry in the array is a separate account salutation object. If no more account salutations are available, the resulting array will be empty. This request should never return an error.

### Account Saved Payments

#### Create an account saved payment using an already tokenized payment

```
DEFINITION
POST http://apiserver/accounts/:id/savedpayments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/savedpayments", {
    "companyCode":"QUICK",
    "paymentName":"VISA",
    "paymentType":"CC",
    "token":"1234567890",
    "referenceNumber":"VISA-1111 01/2020 Dave Duncan",
    "isPrimary":true,
    "isActive":true,
    "newTokenRequired":false
});

EXAMPLE RESPONSE
{
    "id": "11004",
    "accountNumber": 29155",
    "paymentName": "VISA",
    "companyCode": "QUICK",
    "isPrimary": true,
    "isActive": true,
    "hasRecurring": false,
    "hasSubscription": false,
    "payment": {
        "id": null,
        "type": "CC",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2020",
        "cvv": null,
        "token": "1234567890",
        "referenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "savedPaymentId": 11004,
        "savedPaymentReferenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null
    }
}

```

Creates a new account saved payment object.

##### Arguments

* companyCode (required) - The company code of the saved payment.
* paymentName - The name of the saved payment.
* paymentType (required) - The type of saved payment.
* token (required) - The token for the saved payment.
* referenceNumber (required) - The reference number for the saved payment.
* isPrimary
* isActive
* newTokenRequired - Tells the system if the payment needs to be tokenized. If this is set to true then payment information is required.

##### Returns

Returns an account saved payment object if the call succeeds. Returns an error if create parameters are invalid.

#### Create an account saved payment using new payment information

```
DEFINITION
POST http://apiserver/accounts/:id/savedpayments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/savedpayments", {
    "companyCode":"QUICK",
    "paymentName":"My Card",
    "isPrimary":true,
    "isActive":true,
    "newTokenRequired":true,
    "payment":{
        "type":"CC",
        "cardNumber":"4444333322221111",
        "expMonth":"01",
        "expYear":"2020",
        "cardName":"Dave Duncan",
        "cvv": "123",
        "paymentOrigin": "SE",
        "merchant": "BLUE"
    }
});

EXAMPLE RESPONSE
{
    "id": "11006",
    "accountNumber": 29155",
    "paymentName": "My Card",
    "companyCode": "QUICK",
    "isPrimary": true,
    "isActive": true,
    "hasRecurring": false,
    "payment": {
        "id": null,
        "type": "CC",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2020",
        "cvv": null,
        "token": "000000330361",
        "referenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "savedPaymentId": 11006,
        "savedPaymentReferenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null
    }
}

```

Creates a new account saved payment object.

##### Arguments

* companyCode (required) - The company code of the saved payment.
* paymentName - The name of the saved payment.
* isPrimary
* isActive
* newTokenRequired - Tells the system if the payment needs to be tokenized. If this is set to true then payment information is required.
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.

If payment `type` is `CC`, then provide:

* cardNumber - credit card mask
* expMonth - expiration month
* expYear - expiration year
* cardName - the name on card
* cvv - the cvv for the card
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

If payment `type` is `EFT`, then provide:

* accountType - either `CHECKING` or `SAVINGS`
* accountNumber - the bank account number
* routingNumber - the routing number
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

##### Returns

Returns an account saved payment object if the call succeeds. Returns an error if create parameters are invalid.

#### Create an account saved payment using a hosted payment page token

```
DEFINITION
POST http://apiserver/accounts/:id/savedpayments

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/savedpayments", {
    "companyCode":"QUICK",
    "paymentName":"My Visa Card",
    "isPrimary":true,
    "isActive":true,
    "newTokenRequired":true,
    "payment": {
        "hostedPageToken": "1234567890",
        "cardName": "Dave Duncan",
        "type": "CC",
        "paymentOrigin": "SE",
        "merchant": "CCONECT"
    }
});

EXAMPLE RESPONSE
{
    "id": "11006",
    "accountNumber": 29155",
    "paymentName": "My Card",
    "companyCode": "QUICK",
    "isPrimary": true,
    "isActive": true,
    "hasRecurring": false,
    "payment": {
        "id": null,
        "type": "CC",
        "amount": null,
        "merchant": "CCONNECT",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2020",
        "cvv": null,
        "token": "000000330361",
        "referenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "savedPaymentId": 11006,
        "savedPaymentReferenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null
    }
}

```

Creates a new account saved payment object.

##### Arguments

* companyCode (required) - The company code of the saved payment.
* paymentName - The name of the saved payment.
* isPrimary
* isActive
* newTokenRequired - Tells the system if the payment is already tokenized. If this is set to true then payment information is required.
* hostedPageToken - The eToken retrieved from a hosted payment page that will be captured.
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

If payment `type` is `CC`, then provide:

* cardName - the name on card

##### Returns

Returns an account saved payment object if the call succeeds. Returns an error if create parameters are invalid.

#### Retrieve an account saved payment

```
DEFINITION
GET http://apiserver/accounts/:id/savedpayments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/29155/savedpayments/11006");

EXAMPLE RESPONSE
{
    "id": "11006",
    "accountNumber": 29155",
    "paymentName": "My Visa Card",
    "companyCode": "QUICK",
    "isPrimary": true,
    "isActive": true,
    "hasRecurring": false,
    "payment": {
        "id": null,
        "type": "CC",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2020",
        "cvv": null,
        "token": "000000330361",
        "referenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "savedPaymentId": 11006,
        "savedPaymentReferenceNumber": "VISA-1111 01/2020 Dave Duncan",
        "billingAddressId": 100121,
        "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null
    }
}

```

Retrieves the details of an existing account saved payment. You need only supply the account saved payment id.

##### Arguments

* id (required) - The id of the account saved payment to retrieve.

##### Returns

Returns an account saved payment object if a valid id was provided.

#### Update an account saved payment

```
DEFINITION
POST http://apiserver/accounts/:id/savedpayments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/29155/savedpayments/11006", {
    "paymentName": "My Visa Card",
    "payment":{
        "type":"CC",
        "expMonth":"01",
        "expYear":"2022",
        "token": "000000330361",
        "updateExpOnly": true,
        "paymentOrigin": "SE",
        "merchant": "BLUE"
    }
});

EXAMPLE RESPONSE
{
    "id": "11006",
    "accountNumber": 29155",
    "paymentName": "My Visa Card",
    "companyCode": "QUICK",
    "isPrimary": true,
    "isActive": true,
    "hasRecurring": false,
    "payment": {
        "id": null,
        "type": "CC",
        "amount": null,
        "merchant": "BLUE",
        "cardNumber": "VISA-1111",
        "cardName": "Dave Duncan",
        "expMonth": "01",
        "expYear": "2022",
        "cvv": null,
        "token": "000000330361",
        "referenceNumber": "VISA-1111 01/2022 Dave Duncan",
        "savedPaymentId": 11006,
        "savedPaymentReferenceNumber": "VISA-1111 01/2022 Dave Duncan",
        "billingAddressId": 100121,
        "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242",
        "deposit": null,
        "depositStatus": null,
        "depositDate": null
    }
}

```

Updates the specified account saved payment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* companyCode - The company code of the saved payment.
* paymentName - The name of the saved payment.
* paymentType - The type of saved payment.
* token - The token for the saved payment.
* referenceNumber - The reference number for the saved payment.
* isPrimary
* isActive
* newTokenRequired - Tells the system if the payment needs to be re-tokenized.
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.
* merchant (optional) - The company payment gateway. Used to override the default payment gateway code for the company.

##### Returns

Returns the account saved payment object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account saved payment

```
DEFINITION
DELETE http://apiserver/accounts/:id/savedpayments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/29155/savedpayments/11006", { type: "DELETE" });
0
EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account saved payment. It cannot be undone.

##### Arguments

* id (required) - The id of the account saved payment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account saved payment id does not exist, this call returns an error.

#### List all account saved payments

```
DEFINITION
GET http://apiserver/accounts/:id/savedpayments

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/29155/savedpayments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 8
    },
    "items": [
    {
        "id": "11006",
        "accountNumber": 29157",
        "paymentName": "My Card",
        "companyCode": "QUICK",
        "isPrimary": true,
        "isActive": true,
        "hasRecurring": false,
        "payment": {
            "id": null,
            "type": "CC",
            "amount": null,
            "merchant": "BLUE",
            "cardNumber": "VISA-1111",
            "cardName": "Dave Duncan",
            "expMonth": "01",
            "expYear": "2020",
            "cvv": null,
            "token": "000000330361",
            "referenceNumber": "VISA-1111 01/2020 Dave Duncan",
            "savedPaymentId": 11006,
            "savedPaymentReferenceNumber": "VISA-1111 01/2020 Dave Duncan",
            "billingAddressId": 100121,
            "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242",
            "deposit": null,
            "depositStatus": null,
            "depositDate": null
        }
    },
    {...},
    {...},
    {...}
    ]
}

```

Returns a list of all account saved payments.

* Account number could be different than the current account since this call will return all saved payments for the account and family members.

##### Returns

A dictionary with an items property that contains an array of up to limit account saved payments, starting at index offset. Each entry in the array is a separate account saved payment object. If no more account saved payments are available, the resulting array will be empty. This request should never return an error.

### Account Sponsorship Communications

#### Create an Account Sponsorship Communication

```

DEFINITION
POST http://apiserver/accounts/:accountId/sponsorshipcommunications

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/42820/sponsorshipcommunications", {
    "accountNumber":"42820",
    "pledgeCode":"220102",
    "type":"D",
    "sourceCode":"0_A_B_C_M",
    "contactMethod":"WEB",
    "communication":"Test Test",
    "status":"T",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":null,
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797"
});

EXAMPLE RESPONSE
{
    "id":"6",
    "accountNumber":"42820",
    "formattedName": "Robert Jameson",
    "pledgeCode":"220102",
    "pledgeCodeDescription": "Sanjay in India",
    "type":"D",
    "typeDescription":"Donor To Child",
    "sourceCode":"0_A_B_C_M",
    "sourceCodeDescription":"Zero",
    "contactMethod":"WEB",
    "contactMethodDescription":"Website",
    "communication":"Test Test",
    "status":"T",
    "statusDescription":"Translated",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":null,
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797",
    "accessorName":"Nathan Johnson - Internal User"
}

```

Creates a new account sponsorship communication.

##### Arguments

* accountNumber (required) - The account number for the account sponsorship communication
* pledgeCode (required) - The pledge code for the account sponsorship communication
* type (required) - Type of communication
* sourceCode (optional) - Source code for the pledge
* contactMethod (optional) - Contact method for the account
* status (required) - Status of communication
* communication (optional) - Communication data
* dateCreated (required) - Communication created date
* dateApproved (optional) - Communication approved date
* dateTranslated (optional) - Communication translated date
* dateSent (optional) - Communication sent date
* dateDelivered (optional) - Communication delivered date
* dateCanceled (optional) - Communication canceled date
* assignedToAccessorId (optional) - Assigned accessor id

##### Returns

Returns a communication object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an Account Sponsorship Communication

```
DEFINITION
GET http://apiserver/accounts/:accountId/sponsorshipcommunications/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/42820/sponsorshipcommunications/6");

EXAMPLE RESPONSE
{
    "id":"6",
    "accountNumber":"42820",
    "formattedName": "Robert Jameson",
    "pledgeCode":"220102",
    "pledgeCodeDescription": "Sanjay in India",
    "type":"D",
    "typeDescription":"Donor To Child",
    "sourceCode":"0_A_B_C_M",
    "sourceCodeDescription":"Zero",
    "contactMethod":"WEB",
    "contactMethodDescription":"Website",
    "communication":"Test Test",
    "status":"T",
    "statusDescription":"Translated",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":null,
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797",
    "accessorName":"Nathan Johnson - Internal User"
}

```

Retrieves the details of an existing account sponsorship communication. You need only supply the id and the account number.

##### Arguments

* id (required) - Id of the sponsorship communication to retrieve
* accountId (required) - Account number of the associated account

#### Update an Account Sponsorship Communication

```
DEFINITION
POST http://apiserver/accounts/:accountId/sponsorshipcommunications/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/42820/sponsorshipcommunications/6", {
    "dateTranslated": "2018-10-31"
});

EXAMPLE RESPONSE
{
    "id":"6",
    "accountNumber":"42820",
    "formattedName": "Robert Jameson",
    "pledgeCode":"220102",
    "pledgeCodeDescription": "Sanjay in India",
    "type":"D",
    "typeDescription":"Donor To Child",
    "sourceCode":"0_A_B_C_M",
    "sourceCodeDescription":"Zero",
    "contactMethod":"WEB",
    "contactMethodDescription":"Website",
    "communication":"Test Test",
    "status":"T",
    "statusDescription":"Translated",
    "dateCreated":"2018-10-25",
    "dateApproved":"2018-10-25",
    "dateTranslated":"2018-10-31",
    "dateSent":null,
    "dateDelivered":null,
    "dateCanceled":null,
    "assignedToAccessorId":"11797",
    "accessorName":"Nathan Johnson - Internal User"
}


```

Updates the specified sponsorship communication by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* pledgeCode (optional) - The pledge code for the account sponsorship communication
* type (optional) - Type of communication
* sourceCode (optional) - Source code for the pledge
* contactMethod (optional) - Contact method for the account
* status (optional) - Status of communication
* communication (optional) - Communication data
* dateCreated (optional) - Communication created date
* dateApproved (optional) - Communication approved date
* dateTranslated (optional) - Communication translated date
* dateSent (optional) - Communication sent date
* dateDelivered (optional) - Communication delivered date
* dateCanceled (optional) - Communication canceled date
* assignedToAccessorId (optional) - Assigned accessor id

##### Returns

Returns the communication object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an Account Sponsorship Communication

```
DEFINITION
DELETE http://apiserver/accounts/:accountId/sponsorshipcommunications/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/42820/sponsorshipcommunications/6", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a communication. It cannot be undone.

##### Arguments

* id (required) - The id of the communication to be deleted.
* accountId (required) - Account number of the associated account

##### Returns

Returns a `204 No Content` response on success. If the communication does not exist, this call returns an error.

#### List all Account Sponsorship Communications

```

DEFINITION
GET http://apiserver/accounts/:accountId/sponsorshipcommunications

EXAMPLE REQUEST
$.get("http://localhost:8000/api/accounts/42820/sponsorshipcommunications/?offset=0&limit=5", {});

EXAMPLE RESPONSE
{
    "paging":    {
                    "limit":5,
                    "offset":0,
                    "total":13
                },
    "items":    [
                    {
                        "id":"6",
                        "accountNumber":"42820",
                        "formattedName": "Robert Jameson",
                        "pledgeCode":"220102",
                        "pledgeCodeDescription": "Sanjay in India",
                        "type":"D",
                        "typeDescription":"Donor To Child",
                        "sourceCode":"0_A_B_C_M",
                        "sourceCodeDescription":"Zero",
                        "contactMethod":"WEB",
                        "contactMethodDescription":"Website",
                        "communication":"Test Test",
                        "status":"T",
                        "statusDescription":"Translated",
                        "dateCreated":"2018-10-25",
                        "dateApproved":"2018-10-25",
                        "dateTranslated":null,
                        "dateSent":null,
                        "dateDelivered":null,
                        "dateCanceled":null,
                        "assignedToAccessorId":"11797",
                        "accessorName":"Nathan Johnson - Internal User"
                    },
                    {...},
                ]
}

```

Gets a list of all account sponsorship communications.

##### ARGUMENTS

* accountNumber - Filters list by matching the account number with the given account and any family accounts
* pledgeCode - Filter list by partial matching the pledge code
* type - Filter list by matching the type of communication
* sourceCode - Filter list by partial matching the source code for the pledge
* contactMethod - Filter list by partial matching the contact method for the account
* communication - Filter list by partial matching communication data
* status - Filter list by matching the status of communication
* dateCreated - Filter list by matching communication created date
* dateApproved - Filter list by matching communication approved date
* dateTranslated - Filter list by matching communication translated date
* dateSent - Filter list by matching communication sent date
* dateDelivered - Filter list by matching communication delivered date
* dateCanceled - Filter list by matching communication canceled date
* assignedToAccessorId - Filter list by matching the assigned accessor id

##### Returns

A dictionary with an items property that contains an array of up to limit communications, starting at index offset. Each entry in the array is a separate communication object. If no more communications are available, the resulting array will be empty. This request should never return an error.

### Account Subscriptions

#### Create an account subscription

```
DEFINITION
POST http://apiserver/accounts/:id/subscriptions

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16230/subscriptions", {
    "subscription": "EXPLOREREM",
    "start": "2015-01-20",
    "copyCount": 1,
    "numberOfIssues": 12,
    "numberRemaining": 12,
    "source": "EV11CPCATL",
    "priceCode": "1YR",
    "fulfillmentMethod": "EMAIL",
    "email": "31776",
    "mediaOutlet": "KAPP"
});

EXAMPLE RESPONSE
{
    "id": "1000000580",
    "subscription": "EXPLOREREM",
    "documentNumber": null,
    "status": null,
    "start": "2015-01-20",
    "copyCount": 1,
    "numberOfIssues": 12,
    "numberRemaining": 12,
    "source": "EV11CPCATL",
    "fulfillmentMethod": "EMAIL",
    "end": null,
    "priceCode": "1YR",
    "totalAmount": null,
    "remainingDeferredAmount": null,
    "shortComment": null,
    "cancelDate": null,
    "cancelReasonDescription": null,
    "cancelReasonCode": null,
    "lastIssue": null,
    "lastIssueDate": null,
    "purchaserAccount": null,
    "purchaserAccountName": null,
    "mediaOutlet": "KAPP",
    "willNeverExpire": null,
    "address": null,
    "email": "31776",
    "autoRenew": null,
    "renewalPriceCode": null,
    "savedPaymentId": null,
    "nextRenewalDate": null,
    "externalId": null,
    "type": "M",
}

```

Creates a new account subscription object.

##### Arguments

* subscription (required) - The subscription code which the account is subscribing to.
* copyCount (required) - The number of copies the account will receive from this subscription.
* source (required) - The source code for the account subscription.
* priceCode (required) - The price code for the account subscription.
* fulfillmentMethod (required) - The method by which this subscription will be delivered to the account.
* email (required, depending on fulfillmentMethod) - The account's email to send the subscription to.
* address (required, depending on fulfillmentMethod) - The account's address to send the subscription to.
* mediaOutlet (required) - The media outlet of the account subscription.
* start (optional) - The date to start the subscription.
* numberOfIssues (optional) - The number of issues the account will subscribe to.
* numberRemaining (optional) - The number of issues remaining for the account to receive.
* willNeverExpire (optional) - Send true if the subscription will not expire for this account.
* shortComment (optional) - A short comment about the account subscription.
* expirationDate (optional) - The date which the subscription expires for the account.
* autoRenew (optional) - If the subscription is going to auto-renew.
* renewalPriceCode (optional) - If auto-renewing, the price code to renew with.
* savedPaymentId (optional) - If the subscription is auto-renewing, the saved payment that contains the payment token.
* nextRenewalDate (optional) - If the subscription is auto-renewing and active, the future date that it will attempt auto-renewal.
* externalId (optional) - An external identifier for the subscription.

##### Returns

Returns an account subscription object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an account subscription

```
DEFINITION
GET http://apiserver/accounts/:id/subscriptions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16316/subscriptions/1000000580");

EXAMPLE RESPONSE
{
    "id": "1000000580",
    "subscription": "EXPLOREREM",
    "documentNumber": null,
    "status": null,
    "start": "2015-01-20",
    "copyCount": 1,
    "numberOfIssues": 12,
    "numberRemaining": 12,
    "source": "EV11CPCATL",
    "fulfillmentMethod": "EMAIL",
    "end": null,
    "priceCode": "1YR",
    "totalAmount": null,
    "remainingDeferredAmount": null,
    "shortComment": null,
    "cancelDate": null,
    "cancelReasonDescription": null,
    "cancelReasonCode": null,
    "lastIssue": null,
    "lastIssueDate": null,
    "purchaserAccount": null,
    "purchaserAccountName": null,
    "mediaOutlet": "KAPP",
    "willNeverExpire": null,
    "address": null,
    "email": "31776",
    "autoRenew": null,
    "renewalPriceCode": null,
    "savedPaymentId": null,
    "nextRenewalDate": null,
    "externalId": "14414",
    "type": "M",
}

```

Retrieves the details of an existing account subscription. You need only supply the account subscription id.

##### Arguments

* id (required) - The id of the account subscription to retrieve.

##### Returns

Returns an account subscription object if a valid id was provided.

#### Update an account subscription

```
DEFINITION
POST http://apiserver/accounts/:id/subscriptions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16316/subscriptions/1000000580", {
    "status": "H"
});

EXAMPLE RESPONSE
{
    "id": "1000000580",
    "subscription": "EXPLOREREM",
    "documentNumber": null,
    "status": "H",
    "start": "2015-01-20",
    "copyCount": 1,
    "numberOfIssues": 12,
    "numberRemaining": 12,
    "source": "EV11CPCATL",
    "fulfillmentMethod": "EMAIL",
    "end": null,
    "priceCode": "1YR",
    "totalAmount": null,
    "remainingDeferredAmount": null,
    "shortComment": null,
    "cancelDate": null,
    "cancelReasonDescription": null,
    "cancelReasonCode": null,
    "lastIssue": null,
    "lastIssueDate": null,
    "purchaserAccount": null,
    "purchaserAccountName": null,
    "mediaOutlet": "KAPP",
    "willNeverExpire": null,
    "address": null,
    "email": "31776",
    "autoRenew": null,
    "renewalPriceCode": null,
    "savedPaymentId": null,
    "nextRenewalDate": null,
    "externalId": "551143",
    "type": "M",
}


```

Updates the specified account subscription by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* subscription (optional) - The subscription code which the account is subscribing to.
* copyCount (optional) - The number of copies the account will receive from this subscription.
* source (optional) - The source code for the account subscription.
* priceCode (optional) - The price code for the account subscription.
* fulfillmentMethod (optional) - The method by which this subscription will be delivered to the account.
* email (optional, depending on fulfillmentMethod) - The account's email to send the subscription to.
* address (optional, depending on fulfillmentMethod) - The account's address to send the subscription to.
* mediaOutlet (optional) - The media outlet of the account subscription.
* start (optional) - The date to start the subscription.
* numberOfIssues (optional) - The number of issues the account will subscribe to.
* numberRemaining (optional) - The number of issues remaining for the account to receive.
* willNeverExpire (optional) - Send true if the subscription will not expire for this account.
* shortComment (optional) - A short comment about the account subscription.
* expirationDate (optional) - The date which the subscription expires for the account.
* autoRenew (optional) - If the subscription is going to auto-renew.
* renewalPriceCode (optional) - If auto-renewing, the price code to renew with.
* savedPaymentId (optional) - If the subscription is auto-renewing, the saved payment that contains the payment token.
* nextRenewalDate (optional) - If the subscription is auto-renewing and active, the future date that it will attempt auto-renewal.
* externalId (opotional) - An external identifier for the subscription.

##### Returns

Returns the account subscription object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete an account subscription

```
DEFINITION
DELETE http://apiserver/accounts/:id/subscriptions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/16316/subscriptions/1000000580", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account subscription. It cannot be undone.

##### Arguments

* id (required) - The id of the account subscription to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account subscription id does not exist, this call returns an error.

#### List all account subscriptions

```
DEFINITION
GET http://apiserver/accounts/:id/subscriptions

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16316/subscriptions?includeFamilySubscriptions=false");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "1000000577",
            "subscription": "EXPLOREREM",
            "documentNumber": null,
            "status": null,
            "start": "2015-01-20",
            "copyCount": 1,
            "numberOfIssues": 12,
            "numberRemaining": 12,
            "source": "EV11CPCATL",
            "fulfillmentMethod": "EMAIL",
            "end": null,
            "priceCode": "1YR",
            "totalAmount": null,
            "totalTax": null,
            "isTaxIncluded": null,
            "remainingDeferredAmount": null,
            "shortComment": null,
            "cancelDate": null,
            "cancelReasonDescription": null,
            "cancelReasonCode": null,
            "lastIssue": null,
            "lastIssueDate": null,
            "purchaserAccount": null,
            "purchaserAccountName": null,
            "mediaOutlet": "KAPP",
            "willNeverExpire": null,
            "address": null,
            "email": "31776",
            "autoRenew": null,
            "renewalPriceCode": null,
            "savedPaymentId": 219788,
            "billingAddressId": 100101,
            "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242"
            "referenceNumber": "VISA-1111 12/2014 Marc Smith",
            "nextRenewalDate": null,
            "numberOfMonthsPerIssue": 1,
            "externalId": null,
            "type": "M",
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account subscriptions.

##### Arguments

* includeFamilySubscriptions (optional) - Send true to include all family subscriptions in the results.

##### Returns

A dictionary with an items property that contains an array of up to limit account subscriptions, starting at index offset. Each entry in the array is a separate account subscriptions object. If no more account subscriptions are available, the resulting array will be empty. This request should never return an error.

#### List all account subscriptions having an external identifier

```
DEFINITION
GET http://apiserver/accountsubscriptions?externalId=:externalId&subscriptionCode=:subscriptionCode

EXAMPLE REQUEST
$.get("http://localhost:49195/accountsubscriptions?externalId=524132&subscriptionCode=EXPLOREREM");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "1000000577",
            "subscription": "EXPLOREREM",
            "documentNumber": null,
            "status": null,
            "start": "2015-01-20",
            "copyCount": 1,
            "numberOfIssues": 12,
            "numberRemaining": 12,
            "source": "EV11CPCATL",
            "fulfillmentMethod": "EMAIL",
            "end": null,
            "priceCode": "1YR",
            "totalAmount": null,
            "remainingDeferredAmount": null,
            "shortComment": null,
            "cancelDate": null,
            "cancelReasonDescription": null,
            "cancelReasonCode": null,
            "lastIssue": null,
            "lastIssueDate": null,
            "purchaserAccount": null,
            "purchaserAccountName": null,
            "mediaOutlet": "KAPP",
            "willNeverExpire": null,
            "address": null,
            "email": "31776",
            "autoRenew": null,
            "renewalPriceCode": null,
            "savedPaymentId": 219788,
            "billingAddressId": 100101,
            "formattedBillingAddress": "1234 Main St., Dallas, TX, 75242"
            "referenceNumber": "VISA-1111 12/2014 Marc Smith",
            "nextRenewalDate": null,
            "numberOfMonthsPerIssue": 1,
            "externalId": "524132",
            "type": "M",
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account subscriptions having the specified external identifier.

##### Arguments

* externalId (required) - An external identifier for a subscription.
* subscriptionCode (optional) - The subscription code to filter results by.

##### Returns

A dictionary with an items property that contains an array of up to limit account subscriptions, starting at index offset. Each entry in the array is a separate account subscriptions object. If no more account subscriptions are available, the resulting array will be empty. This request should never return an error.
Subsequent actions will be performed through other methods in the [account subscriptions section](#account-subscriptions)

#### Cancel an account subscription

```
DEFINITION
POST http://apiserver/accounts/:id/subscriptions/:id/cancel

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/16316/subscriptions/1000000577/cancel", {
    cancelDate: "2014-11-17",
    repaymentMethod: "REFUND",
    cancelReasonCode: "NI",
    amount: 10
});

EXAMPLE RESPONSE
{
    "Success": true,
    "FriendlyUIMessage": null,
    "AdditionalUIMessages": [],
    "CCResult":
        [
            {
                "Success": true,
                "ReferenceNumber": "VISA-1111 12/2014 Marc Smith",
                "ProcessorErrorCode": 0,
                "FriendlyUICCMessage": null,
                "TechnicalErrorMessage": null,
                "Amount": 10.0000,
                "Tax": 0.0
            }
        ],
    "TechnicalErrorMessage": null,
    "NewDocumentNumber": null
}


```

Cancels the specified transaction subscription.

##### Arguments

* cancelDate (optional; defaults to current date) - Date for the cancellation. Used for identifying the correct deposit.
* repaymentMethod (required) - Method for repayment. Valid values: `REFUND`, `CREDIT`, `CONVERTTODONATION` or any valid value for the `DDCPAYTYPE` code type.
* cancelReasonCode (optional) - reason for the cancellation. Valid values are values for the `DDCCANCRCD` code type.
* amount (optional) - amount to apply towards the cancellation
* convertToDonationsOptions (optional when repaymentMethod is not `CONVERTTODONATION`) - options for creating a donation from the refund amount.
  + projectCode (required) - the project to assign this donation to
  + accountPledge (optional) - the pledge to assign this donation to
  + pledgeCode (optional) - the pledge code associated with the account pledge
  + letterCode (optional) - the letter code to assign to the donation
* isProcessed (optional; defaults to `false`) - Only applicable when `repaymentMethod` is `REFUND` and the original transaction payment was with a `CC`. When `true`, the cancellation will process in StudioEnterprise, but the funds will not be returned to the CC. This should only be used in scenarios where the funds have already been refunded to the CC such as by an external system.

##### Returns

Returns a result object, containing various messages regarding the result of the transaction cancellation.

#### Retrieve an account subscriptions isRealTimeRefundAllowed flag

```
DEFINITION
GET http://apiserver/accounts/:id/subscriptions/:id/realtimerefund

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16316/subscriptions/1000000577/realtimerefund");

EXAMPLE RESPONSE
{
    "isRealTimeRefundAllowed": true
}

```

Retrieves the isRealTimeRefundAllowed flag of an existing subscription.

##### Arguments

* id (required) - The id of the transaction for the isRealTimeRefundAllowed flag to be retrieved.

#### Returns

Returns isRealTimeRefundAllowed flag with the value 'true' or 'false'

### Account Social Media Handles

#### Create an account social media handle

```
DEFINITION
POST http://apiserver/accounts/:id/socialmediahandles

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/socialmediahandles", {
    "network": "T",
    "handle": "hwinkler4real"
});

EXAMPLE RESPONSE
{
    "id": "184703",
    "network": "T",
    "networkDescription": "Twitter",
    "handle": "hwinkler4real",
    "isDefault": false,
    "isActive": true
}

```

Creates a new account social media handle object.

##### Arguments

* network (required) - The social network id of the account social media handle. Must be a defined social network id.
* handle (required) - The handle of the account social media handle.
* isDefault (optional) - Whether or not the account social media handle is the default for the account. If not specified, will default to true if no other social media handle exists, otherwise will default to false.
* isActive (optional) - Whether or not the account social media handle is active. If not specified, will default to true.

##### Returns

Returns an account social media handle object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined social media handle type).

#### Retrieve an account social media handle

```
DEFINITION
GET http://apiserver/accounts/:id/socialmediahandles/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/socialmediahandles/184703");

EXAMPLE RESPONSE
{
    "id": "184703",
    "network": "T",
    "networkDescription": "Twitter",
    "handle": "hwinkler4real",
    "isDefault": false,
    "isActive": true
}

```

Retrieves the details of an existing account social media handle. You need only supply the account social media handle id.

##### Arguments

* id (required) - The id of the account social media handle to retrieve.

##### Returns

Returns an account social media handle object if a valid id was provided.

#### Update an account social media handle

```
DEFINITION
POST http://apiserver/accounts/:id/socialmediahandles/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1483320/socialmediahandles/184703", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "184703",
    "network": "T",
    "networkDescription": "Twitter",
    "handle": "hwinkler4real",
    "isDefault": false,
    "isActive": false
}


```

Updates the specified account social media handle by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* network (optional) - The social network id of the account social media handle. Must be a defined social network id.
* handle (optional) - The handle of the account social media handle.
* isDefault (optional) - Whether or not the account social media handle is the default for the account. If not specified, will default to true if no other social media handle exists, otherwise will default to false.
* isActive (optional) - Whether or not the account social media handle is active. If not specified, will default to true.

##### Returns

Returns the account social media handle object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined social media handle type or social media handle type value).

#### Delete an account social media handle

```
DEFINITION
DELETE http://apiserver/accounts/:id/socialmediahandles/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/1483320/socialmediahandles/184703", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account social media handle. It cannot be undone.

##### Arguments

* id (required) - The id of the account social media handle to be deleted.

##### Returns

Returns a 204 No Content response on success. If the account social media handle id does not exist, this call returns an error.

#### List all account social media handles

```
DEFINITION
GET http://apiserver/accounts/:id/socialmediahandles

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/socialmediahandles");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "184703",
            "network": "T",
            "handle": "hwinkler4real",
            "isDefault": false,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account social media handles.

##### Returns

A dictionary with an items property that contains an array of up to limit account social media handles, starting at index offset. Each entry in the array is a separate account social media handle object. If no more account social media handles are available, the resulting array will be empty. This request should never return an error.

### Account Social Media Handle Profiles

#### Retrieve an account social media handle profile

```
DEFINITION
GET http://apiserver/accounts/:id/socialmediahandles/:id/profile

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/socialmediahandles/184703/profile");

EXAMPLE RESPONSE
{
    "id": "1234567890",
    "name": "John Doe",
    "description": "",
    "imageUrl": "http://abs.twimg.com/sticky/default_profile_images/default_profile_6_normal.png",
    "imageUrlHttps": "https://abs.twimg.com/sticky/default_profile_images/default_profile_6_normal.png",
    "statuses": 21,
    "followers": 5,
    "friends": 69
}

```

Returns an account social media handle profile. You need only supply the account social media handle id.

##### Arguments

* id (required) - The id of the account social media handle to retrieve the profile for

##### Returns

Returns an account social media handle profile object if a valid id was provided. If the handle is invalid for the specified social media network, returns a 404, not found.

### Account Social Media Handle Statuses

#### List all Account Social Media Handle Statuses

```
DEFINITION
GET http://apiserver/accounts/:id/socialmediahandles/:id/statuses

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/socialmediahandles/184703/statuses");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "560862547276886016",
            "date": "2015-01-29",
            "text": "My first tweet!"
        },
        {...},
        {...}
    ]
}

```

Returns a list of account social media handle statuses. You need only supply the account social media handle id.

##### Arguments

* id (required) - The id of the account social media handle to list statuses for
* last (optional) - Returns results with an ID less than (that is, older than) or equal to the specified ID (Social Media services external to Studio Enterprise do not support paging in the same way as the interal Services. Therefore this argument is supported to allow fetching of multiple pages of statuses.)

##### Returns

A dictionary with an items property that contains an array of up to limit account social media handle statuses, starting at index offset. Each entry in the array is a separate account social media handle status object. If no more account social media handle statuses are available, the resulting array will be empty. If the handle is invalid for the specified social media network, returns a 404, not found.

### Account Source Quick Picks

#### List all account source code quick picks

```
DEFINITION
GET https://apiserver/accounts/:id/sourceQuickPicks

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/sourceQuickPicks");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "account": 0,
            "id": "072711",
            "description": "New Accounts",
            "date": "7/29/2014 12:00:00 AM",
            "commType": "LETTER"
        },
        {
            "account": 0,
            "id": "EV11CPCATL",
            "description": "Pastor's Conf March 2011 Atlanta",
            "date": null,
            "commType": "QuickPick"
        }
        {...},
        {...}
    ]
}

```

Returns a list of all account source quick picks.

##### Arguments

* id (required) - The id of the account to retrieve quick picks for.
* company (optional) - Filters the source code quick picks returned to those from the specified company.
* sourceCode - The id of the source code quick pick for the specified account.
* descriptions - The description of the source code quick pick for the specified account.
* shouldOnlyReturnQuickPicks (optional) - Whether to only return quick picks instead of returning all source codes, if no quick picks are found.

##### Returns

A dictionary with an items property that contains an array of up to limit account source quick picks, starting at index offset. Each entry in the array is a separate account source quick pick object. If no more account source quick pick objects are available, the resulting array will be empty. This request should never return an error.

### Account StudioOnline Cross Reference

#### Retrieve an account studioonline cross reference

```
DEFINITION
GET http://apiserver/accounts/studioonlinecrossreference

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/studioonlinecrossreference?ecommerceId=234490");

EXAMPLE RESPONSE
{
    "accountId": 29130,
    "ecommerceId": 234490
}

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/studioonlinecrossreference?accountId=29130");

EXAMPLE RESPONSE
{
    "accountId": 29130,
    "ecommerceId": 234490
}

```

Retrieves the details of an existing account studioonline cross reference. `HTTP 404` is returned if no cross reference is found.

##### Arguments

* accountId (required when `ecommerceId` is not specified) - The StudioEnterprise AccountNumber
* ecommerceId (required when `accountId` is not specified) - The StudioOnline Customer Id

### Account Summaries

#### Retrieve all account summary years

```
DEFINITION
GET http://apiserver/accounts/:accountId/summaries/:id/annual

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/summaries/1/annual");

EXAMPLE RESPONSE
[
    {
        "id": "2012",
        "summaryId": "1",
        "summaryDescription": "Deductible Donations",
        "totalNumber": 5,
        "totalAmount": 316,
        "averageAmount": 63.2
    },
    {...},
    {...}
]

```

Returns a list of all account annual summaries.

##### Arguments

* accountId (required) - The id of the account for which to retrieve summaries.
* id (required) - The id of the account summary object to retrieve.
* includeGroups (optional) - It will include any donations that have projects assigned to any group member of a group that the user's accessor id is in.
* groupMemberAccessorId (optional) - Only used if `includeGroups` is provided. It will filter the donations to only return projects that are assigned to the specified group member.
* projectDepartment (optional) - It will filter the summaries to only include projects that have a project default deparment matching the specified value. All non-donation summaries will not be returned.

##### Returns

An array of account annual summary objects. Each entry in the array is a separate account annual summary object. This request should never return an error.

#### Retrieve all account summary details by year

```
DEFINITION
GET http://apiserver/accounts/:accountId/summaries/:summaryId/annual/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/16230/summaries/1/annual/2012");

EXAMPLE RESPONSE
{
    "monthly": [
        {
            "summaryId": "1",
            "summaryDescription": "Deductible Donations",
            "year": 2012,
            "month": 9,
            "totalNumber": 5,
            "totalAmount": 316,
            "averageAmount": 63.2
        }
    ],
    "project": [
        {
            "summaryId": "1",
            "summaryDescription": "Deductible Donations",
            "year": 2012,
            "project": "110100",
            "projectDescription": "FCA Dallas Project",
            "totalNumber": 5,
            "totalAmount": 316,
            "averageAmount": 63.2
        }
    ]
}

```

Retrieves the details of an account annual summary for a given year.

##### Arguments

* accountId (required) - The id of the account for which to retrieve summaries.
* summaryId (required) - The id of the account summary object for which to retrieve annual account summaries.
* id (required) - The year of the annual account summary to retrieve.
* includeGroups (optional) - It will include any donations that have projects assigned to any group member of a group that the user's accessor id is in.
* groupMemberAccessorId (optional) - Only used if `includeGroups` is provided. It will filter the donations to only return projects that are assigned to the specified group member.
* projectDepartment (optional) - It will filter the summaries to only include projects that have a project default deparment matching the specified value. All non-donation summaries will not be returned.

##### Returns

Returns an account annual summary details object if a valid year was provided.

#### List all account summaries

```
DEFINITION
GET http://apiserver/accounts/:id/summaries

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483320/summaries");

EXAMPLE RESPONSE
[
    {
        "id": "1",
        "type": "Deductible Donations",
        "totalNumber": 221,
        "totalAmount": 12458.64,
        "averageAmount": 56.3739,
        "firstDate": "2012-09-13",
        "firstAmount": 100,
        "lastDate": "2014-11-06",
        "lastAmount": 13.99,
        "largestDate": "2014-08-13",
        "largestAmount": 1501
    },
    {...},
    {...}
]

```

Returns a list of all account summaries.

##### Arguments

* id (required) - The id of the account for which to retrieve summaries.
* includeGroups (optional) - It will include any donations that have projects assigned to any group member of a group that the user's accessor id is in.
* groupMemberAccessorId (optional) - Only used if `includeGroups` is provided. It will filter the donations to only return projects that are assigned to the specified group member.
* projectDepartment (optional) - It will filter the summaries to only include projects that have a project default deparment matching the specified value. All non-donation summaries will not be returned.

##### Returns

An array of all account summaries. This request should never return an error.

### Account Wealth Engine Screenings

#### Retrieve an account wealth engine screening

```
DEFINITION
GET http://apiserver/accounts/:id/wealthenginescreenings/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483434/wealthenginescreenings/27");

EXAMPLE RESPONSE
{
    "id": "27",
    "weRun": "90931001",
    "weId": "161870009",
    "date": "2013-07-31",
    "gcAgeUsed": 0,
    "age": null,
    "dateOfBirth": null,
    "p2gScoreCombo": 1,
    "p2gDescription": "Excellent",
    "p2gScore1": "1",
    "p2gScore2": "0",
    "totalAssets": "$500MM+",
    "totalAssetRating": 12,
    "netWorth": "$500MM+",
    "netWorthRating": 12,
    "cashOnHand": "$500K+",
    "cashOnHandRating": "4",
    "estimatedAnnualDonations": "$100K+",
    "estimatedAnnualDonationRating": 7,
    "giftCapacityRange": "$5MM+",
    "giftCapacityRating": 20,
    "giftCapacityIncome": "Unable to rate",
    "giftCapacityRealEstate": "Unable to rate",
    "giftCapacityStock": "Unable to rate",
    "giftCapacityPension": "Unable to rate",
    "giftCapacityDonations": "Unable to rate",
    "estimatedGiftCapacity": "$5MM+",
    "influenceRating": 1,
    "inclinationAffiliation": "Older w/ Strong Political, Charitable Affiliation",
    "inclinationGiving": "Giving Data Not Provided",
    "bequest": "Y",
    "annuity": 2,
    "trust": 2,
    "income": "$100K-$250K",
    "incomeRating": 3,
    "pension": "Unable to rate",
    "pensionRating": 0,
    "realEstateValue": "$750K-$1MM",
    "realEstateValueRating": 4,
    "realEstateProperties": 2,
    "stockDirectHoldings": "$100MM+",
    "stockDirectHoldingsRating": 8,
    "stockTotalValue": "$100MM+",
    "stockTotalValueRating": 8,
    "charitableDonations": "$1MM+",
    "charitableDonationsRating": 14,
    "politicalDonations": "$100K - $500K",
    "politicalDonationsRating": 14,
    "totalDonations": "$100K - $500K",
    "totalDonationsRating": "14",
    "coOwnershipValue": "Unable to rate",
    "coOwnershipValueRating": null,
    "coSalesVolume": "$100MM+",
    "coSalesVolumeRating": 8,
    "rfmTotal": null,
    "rfmRecency": null,
    "rfmFrequency": null,
    "rfmAmount": null,
    "aircraftOwner": "N",
    "boatOwner": "N",
    "children": "",
    "innerCircleMatch": "N",
    "innerCircleMember": "N",
    "majorDonor": "N",
    "boardMember": "",
    "matchCount": 16,
    "folderName": "ONLINE",
    "qomAircraft": "Low",
    "qomAirmen": "Low",
    "qomCharitableDonations": "Medium",
    "qomDunBradstreet": "Medium",
    "qomFedElectionCampaign": "Medium",
    "qomGuideStarFoundation": "High",
    "qomGuideStarDirectors": "High",
    "qomHouseholdProfile": "High",
    "qomHoovers": "High",
    "qomMajorDonor": "Low",
    "qomPhysiciansProfile": "Low",
    "qomMarketGuide": "High",
    "qomIRSSection527Directors": "Low",
    "qomIRSSection527PoliticalOrg": "Low",
    "qomPension": "Low",
    "qomPhilanthropicDonations": "Low",
    "qomRealEstate": "High",
    "qomStatePolitical": "High",
    "qomSSADeathIndex": "Low",
    "qomWealthIDSecurities": "High",
    "qomFoundationTrustees": "High",
    "qomMerchantVessels": "Low",
    "qomMarquisWhosWho": "High",
    "attribute1": "",
    "attribute2": "",
    "attribute3": "",
    "attribute4": "",
    "attribute5": "",
    "attribute6": "",
    "attribute7": "",
    "attribute8": "",
    "attribute9": "",
    "attribute10": "",
    "attribute11": "",
    "attribute12": "",
    "attribute13": "",
    "attribute14": "",
    "attribute15": "",
    "majorGiftDecile": null,
    "majorGiftScore": null,
    "annualFundDecile": null,
    "annualFundScore": null,
    "plannedGivingDecile": null,
    "plannedGivingScore": null,
    "likelihoodToGiveDecile": null,
    "likelihoodToGiveScore": null,
    "nextAskAmountDecile": null,
    "nextAskAmountScore": null,
    "clusterNumber": null,
    "isPrimary": false
}

```

Retrieves the details of an account wealth engine screening. You need only supply the account wealth engine screening id.

##### Arguments

* id (required) - The id of the account wealth engine screening object to retrieve.

##### Returns

Returns an account wealth engine screening object if a valid id was provided.

#### List all account wealth engine screenings

```
DEFINITION
GET http://apiserver/accounts/:id/wealthenginescreenings

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/1483434/wealthenginescreenings");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "27",
            "weRun": "90931001",
            "weId": "161870009",
            "date": "2013-07-31",
            "gcAgeUsed": 0,
            "age": null,
            "dateOfBirth": null,
            "p2gScoreCombo": 1,
            "p2gDescription": "Excellent",
            "p2gScore1": "1",
            "p2gScore2": "0",
            "totalAssets": "$500MM+",
            "totalAssetRating": 12,
            "netWorth": "$500MM+",
            "netWorthRating": 12,
            "cashOnHand": "$500K+",
            "cashOnHandRating": "4",
            "estimatedAnnualDonations": "$100K+",
            "estimatedAnnualDonationRating": 7,
            "giftCapacityRange": "$5MM+",
            "giftCapacityRating": 20,
            "giftCapacityIncome": "Unable to rate",
            "giftCapacityRealEstate": "Unable to rate",
            "giftCapacityStock": "Unable to rate",
            "giftCapacityPension": "Unable to rate",
            "giftCapacityDonations": "Unable to rate",
            "estimatedGiftCapacity": "$5MM+",
            "influenceRating": 1,
            "inclinationAffiliation": "Older w/ Strong Political, Charitable Affiliation",
            "inclinationGiving": "Giving Data Not Provided",
            "bequest": "Y",
            "annuity": 2,
            "trust": 2,
            "income": "$100K-$250K",
            "incomeRating": 3,
            "pension": "Unable to rate",
            "pensionRating": 0,
            "realEstateValue": "$750K-$1MM",
            "realEstateValueRating": 4,
            "realEstateProperties": 2,
            "stockDirectHoldings": "$100MM+",
            "stockDirectHoldingsRating": 8,
            "stockTotalValue": "$100MM+",
            "stockTotalValueRating": 8,
            "charitableDonations": "$1MM+",
            "charitableDonationsRating": 14,
            "politicalDonations": "$100K - $500K",
            "politicalDonationsRating": 14,
            "totalDonations": "$100K - $500K",
            "totalDonationsRating": "14",
            "coOwnershipValue": "Unable to rate",
            "coOwnershipValueRating": null,
            "coSalesVolume": "$100MM+",
            "coSalesVolumeRating": 8,
            "rfmTotal": null,
            "rfmRecency": null,
            "rfmFrequency": null,
            "rfmAmount": null,
            "aircraftOwner": "N",
            "boatOwner": "N",
            "children": "",
            "innerCircleMatch": "N",
            "innerCircleMember": "N",
            "majorDonor": "N",
            "boardMember": "",
            "matchCount": 16,
            "folderName": "ONLINE",
            "qomAircraft": "Low",
            "qomAirmen": "Low",
            "qomCharitableDonations": "Medium",
            "qomDunBradstreet": "Medium",
            "qomFedElectionCampaign": "Medium",
            "qomGuideStarFoundation": "High",
            "qomGuideStarDirectors": "High",
            "qomHouseholdProfile": "High",
            "qomHoovers": "High",
            "qomMajorDonor": "Low",
            "qomPhysiciansProfile": "Low",
            "qomMarketGuide": "High",
            "qomIRSSection527Directors": "Low",
            "qomIRSSection527PoliticalOrg": "Low",
            "qomPension": "Low",
            "qomPhilanthropicDonations": "Low",
            "qomRealEstate": "High",
            "qomStatePolitical": "High",
            "qomSSADeathIndex": "Low",
            "qomWealthIDSecurities": "High",
            "qomFoundationTrustees": "High",
            "qomMerchantVessels": "Low",
            "qomMarquisWhosWho": "High",
            "attribute1": "",
            "attribute2": "",
            "attribute3": "",
            "attribute4": "",
            "attribute5": "",
            "attribute6": "",
            "attribute7": "",
            "attribute8": "",
            "attribute9": "",
            "attribute10": "",
            "attribute11": "",
            "attribute12": "",
            "attribute13": "",
            "attribute14": "",
            "attribute15": "",
            "majorGiftDecile": null,
            "majorGiftScore": null,
            "annualFundDecile": null,
            "annualFundScore": null,
            "plannedGivingDecile": null,
            "plannedGivingScore": null,
            "likelihoodToGiveDecile": null,
            "likelihoodToGiveScore": null,
            "nextAskAmountDecile": null,
            "nextAskAmountScore": null,
            "clusterNumber": null,
            "isPrimary": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account wealth engine screenings.

##### Returns

A dictionary with an items property that contains an array of up to limit account wealth engine screenings, starting at index offset. Each entry in the array is a separate account wealth engine screening object. If no more account wealth engine screenings are available, the resulting array will be empty. This request should never return an error.

#### Perform a wealth engine screening

```
DEFINITION
POST http://apiserver/accounts/:id/wealthenginescreenings/process

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/1/wealthenginescreenings/process", {});

EXAMPLE RESPONSE
{
    "WeRunId": "92596070",
    "WeRecId": "225216966",
    "OriginalId": "1",
    "OriginalId2": null,
    "P2gScore": "3",
    "P2gScore2": "5",
    "P2gCombo": "3|5",
    "P2GDesc": "Average",
    "AssetRange": "$100K-$500K",
    "AssetRating": "WE.ASSETS.004",
    "NetworthRange": "$100K-$500K",
    "NetworthRating": "WE.NETWRTH.004",
    "LiquidityRange": "<$10K",
    "LiquidityRating": "WE.LIQUID.001",
    "EadRange": "$1K-$5K",
    "EadRating": "WE.ANNDON.002",
    "InclinationGiv": "Prospect",
    "InclinationAff": "Younger w/out Affiliation",
    "CapacityRating": "7",
    "GivingCapacityRating": "WE.GIVCAP.011",
    "CapacityRange": "$25K-$50K",
    "GivingCapacityRange": "$30K - $40K",
    "Bequest": "NO",
    "Annuity": "0",
    "Trust": "0",
    "InfluenceRating": "2",
    "IncomeRange": "$50K-$100K",
    "IncomeRating": "WE.INCOME.002",
    "RealEstateValueRange": "$1-$250K",
    "RealEstateValueRating": "WE.RELEST.001",
    "RealEstateCount": "1",
    "DirectStockRange": "Unable to rate",
    "DirectStockRating": "WE.DSTOCK.999",
    "TotalStockRange": "Unable to rate",
    "TotalStockRating": "WE.TSTOCK.999",
    "NPOGiveRating": "WE.NPOGIV.999",
    "NPOGiveRange": "Unable to rate",
    "DonTotRange": "Unable to rate",
    "DonTotRating": "WE.DONTOT.999",
    "PolTotRange": "Unable to rate",
    "PolTotRating": "WE.POLDON.999",
    "PensionsRange": "Unable to rate",
    "PensionsRating": "WE.PENSON.999",
    "BoatOwner": "No",
    "AircraftOwner": "No",
    "DbCompanyValueRange": "Unable to rate",
    "DbCompanyValueRating": "WE.COVALU.999",
    "BsnsSalesVolumeRange": "Unable to rate",
    "BsnsSalesVolRating": "WE.BIZVOL.999",
    "BoardMember": "No",
    "GcIncomeRange": "$20K-$25K",
    "GcIncomeRating": "WE.GC-INC.005",
    "GcStocksRange": "Unable to rate",
    "GcStocksRating": "WE.GCSTOK.999",
    "GcRealEstateRange": "$5K-10K",
    "GcRealEstateRating": "WE.GCREAL.002",
    "GcPensionRange": "Unable to rate",
    "GcPensionRating": "WE.GCPENS.999",
    "GcGiftRange": "$30K - $40K",
    "GcGiftRating": "WE.GCGIFT.999",
    "AirQom2": null,
    "AmenQom2": null,
    "BregQom2": null,
    "DbQom2": "High",
    "DirQom2": null,
    "DnmQom2": null,
    "DonQom2": "Medium",
    "FecQom2": null,
    "GsfdnQom2": null,
    "GsQom2": null,
    "HprofQom2": null,
    "HvrQom2": null,
    "MdQom2": null,
    "MedQom2": null,
    "MgQom2": null,
    "PdirQom2": null,
    "PenQom2": null,
    "PhilQom2": null,
    "PoloQom2": null,
    "RealEstQom2": "High",
    "SpdQom2": null,
    "SsdmQom2": null,
    "StockQom2": null,
    "TrustQom2": null,
    "VdsQom2": null,
    "WwQom2": null,
    "SpOriginalId": null,
    "SpOriginalId2": null,
    "GcAgeUsed": "48"
}

```

Performs a new wealth engine screening.

##### Returns

Returns a wealth engine screening object from the wealth engine service if the call succeeded. A Wealth Engine Screening record is created for the given account. Returns an error if create parameters are invalid or the service fails to execute.

#### Advanced Find Manage Marketing Attributes

```
DEFINITION
POST http://apiserver/accounts/managemarketingattributes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/managemarketingattributes", {
    "advancedFind":{
        "table":"A01",
        "isDistinct":true,
        "selectionCriteria":[
            {
                "group":1,
                "table":"A01",
                "field":"FIRSTNAME",
                "operator":"EQ",
                "value":"Larry",
                "isJoin":false
            },
            {
                "group":1,
                "table":"A01",
                "field":"LASTNAME",
                "operator":"EQ",
                "value":"Holt",
                "isJoin":false
            }
        ]
    },
    "action":"set",
    "attributeType":"DONTRACK",
    "attributeValue":"4"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* advancedFind () - The criteria array to use for executing an advanced find search.
* action (optional) - The action to perform on account marketing codes in the advanced find manage marketing attributes process. (Must be one of the following: `SET`, `DELETE`.)
* attributeType (optional) - The account marketing code type to perform the action on in the advanced find manage marketing attributes process. (Must be a valid and active code type in the `ACCTMKATTR` category. Required if action is `SET`, `DELETE`.)
* attributeValue (optional) - The value of the attributeType to perform the action on in the advanced find manage marketing attributes process. (Must be a valid code value for the attributeType. Required if action is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the advanced find manage marketing attributes process has an error, a 400 or 500 will be returned.

#### Advanced Find Manage Marketing Dates

```
DEFINITION
POST http://apiserver/accounts/managemarketingdates

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/managemarketingdates", {
    "advancedFind":{
        "table":"A01",
        "isDistinct":true,
        "selectionCriteria":[
            {
                "group":1,
                "table":"A01",
                "field":"FIRSTNAME",
                "operator":"EQ",
                "value":"Larry",
                "isJoin":false
            },
            {
                "group":1,
                "table":"A01",
                "field":"LASTNAME",
                "operator":"EQ",
                "value":"Holt",
                "isJoin":false
            }
        ]
    },
    "action":"set",
    "dateType":"LSTCONTACT",
    "dateValue":"2016-06-01"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* advancedFind () - The criteria array to use for executing an advanced find search.
* action (optional) - The action to perform on account marketing dates in the advanced find manage marketing dates process. (Must be one of the following: `SET`, `DELETE`.)
* dateType (optional) - The account marketing date type to perform the action on in the advanced find manage marketing dates process. (Must be a valid and active date type in the `ACCTMKATTR` category. Required if action is `SET`, `DELETE`.)
* dateValue (optional) - The value of the dateType to perform the action on in the advanced find manage marketing dates process. (Must be a valid date value for the dateType. Required if action is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the advanced find manage marketing dates process has an error, a 400 or 500 will be returned.

#### Advanced Find Manage Marketing Notes

```
DEFINITION
POST http://apiserver/accounts/managemarketingnotes

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/managemarketingnotes", {
    "advancedFind":{
        "table":"A01",
        "isDistinct":true,
        "selectionCriteria":[
            {
                "group":1,
                "table":"A01",
                "field":"FIRSTNAME",
                "operator":"EQ",
                "value":"Larry",
                "isJoin":false
            },
            {
                "group":1,
                "table":"A01",
                "field":"LASTNAME",
                "operator":"EQ",
                "value":"Holt",
                "isJoin":false
            }
        ]
    },
    "action":"set",
    "noteType":"MKTNOTE",
    "noteValue":"He enjoys attending hockey games with his family."
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* advancedFind () - The criteria array to use for executing an advanced find search.
* action (optional) - The action to perform on account marketing notes in the advanced find manage marketing notes process. (Must be one of the following: `SET`, `DELETE`.)
* noteType (optional) - The account marketing note type to perform the action on in the advanced find manage marketing notes process. (Must be a valid and active note type in the `ACCTMKATTR` category. Required if action is `SET`, `DELETE`.)
* noteValue (optional) - The value of the noteType to perform the action on in the advanced find manage marketing notes process. (Required if action is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the advanced find manage marketing notes process has an error, a 400 or 500 will be returned.

#### Advanced Find Manage Marketing Numbers

```
DEFINITION
POST http://apiserver/accounts/managemarketingnumbers

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/managemarketingnumbers", {
    "advancedFind":{
        "table":"A01",
        "isDistinct":true,
        "selectionCriteria":[
            {
                "group":1,
                "table":"A01",
                "field":"FIRSTNAME",
                "operator":"EQ",
                "value":"Larry",
                "isJoin":false
            },
            {
                "group":1,
                "table":"A01",
                "field":"LASTNAME",
                "operator":"EQ",
                "value":"Holt",
                "isJoin":false
            }
        ]
    },
    "action":"set",
    "numberType":"LSTGIFTAMT",
    "numberValue":"125"
});

EXAMPLE RESPONSE
204 No Content

```

##### Arguments

* advancedFind () - The criteria array to use for executing an advanced find search.
* action (optional) - The action to perform on account marketing numbers in the advanced find manage marketing numbers process. (Must be one of the following: `SET`, `DELETE`.)
* numberType (optional) - The account marketing number type to perform the action on in the advanced find manage marketing numbers process. (Must be a valid and active number type in the `ACCTMKATTR` category. Required if action is `SET`, `DELETE`.)
* numberValue (optional) - The value of the numberType to perform the action on in the advanced find manage marketing numbers process. (Must be a valid number value for the numberType. Required if action is `SET`, `DELETE`.)

##### Returns

Returns a 204 No Content response on success. If the advanced find manage marketing numbers process has an error, a 400 or 500 will be returned.

### Advanced Find View Overrides

#### Create an advanced find view override

```
DEFINITION
POST http://apiserver/advancedfindviews/:id/overrides

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedfindviews/50038/overrides", {
    "field": "A03State",
    "title": "State",
    "displaySequence": 34,
    "width": "10em",
    "isHidden": false
});

EXAMPLE RESPONSE
{
    "id": "3",
    "viewId": "50038",
    "field": "A03State",
    "title": "State",
    "displaySequence": 34,
    "sortSequence": null,
    "sortDirection": null,
    "width": "10em",
    "isHidden": false
}

```

Creates a new advanced find view override.

##### Arguments

* viewId (required) - The unique view identifier for which to associate this override (From URI).
* field (required) - The field returned by the view which is being overridden.
* title (required) - The overriden display title for the field,
* displaySequence () - The overridden field display sequence in the results of the view
* sortSequence () - If the results of the view are to be sorted by this field, the sort order for this field
* sortDirection () - If the results of the view are to be sorted by this field, the sort direction (ascending / descending) for this field
* width () - The overridden display width for the field
* isHidden () - The overridden visability for the field

##### Returns

Returns an advanced find view override object if the call succeeded. Returns an error if create parameters are invalid.

#### Retrieve an advanced find view override

```
DEFINITION
GET http://apiserver/advancedfindviews/:id/overrides/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedfindviews/50038/overrides/3");

EXAMPLE RESPONSE
{
    "id": "3",
    "viewId": "50038",
    "field": "A03State",
    "title": "State",
    "displaySequence": 34,
    "sortSequence": null,
    "sortDirection": null,
    "width": "10em",
    "isHidden": false
}

```

Retrieves the details of an existing advanced find view override. You need only supply the id of the view and the override.

##### Arguments

* id (required) - The id of the advanced find view override to be retrieved.

#### Update an advanced find view override

```
DEFINITION
POST http://apiserver/advancedfindviews/:id/overrides/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/advancedfindviews/50038/overrides/3", {
    "isHidden": true
});

EXAMPLE RESPONSE
{
    "id": "3",
    "viewId": "50038",
    "field": "A03State",
    "title": "State",
    "displaySequence": 34,
    "sortSequence": null,
    "sortDirection": null,
    "width": "10em",
    "isHidden": true
}


```

Updates the specified advanced find view override by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* title () - The overriden display title for the field,
* displaySequence () - The overridden field display sequence in the results of the view
* sortSequence () - If the results of the view are to be sorted by this field, the sort order for this field
* sortDirection () - If the results of the view are to be sorted by this field, the sort direction (ascending / descending) for this field
* width () - The overridden display width for the field
* isHidden () - The overridden visability for the field

##### Returns

Returns the advanced find view override object if the update succeeded. Returns an error if update parameters are invalid.

#### Delete advanced find view overrides

```
DEFINITION
DELETE http://apiserver/advancedfindviews/:id/overrides

EXAMPLE REQUEST
$.ajax("http://localhost:49195/advancedfindviews/50038/overrides", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes all advanced find view overrides associated with the specified view. It cannot be undone.

##### Arguments

* id (required) - The id of the advanced find view to delete all the overrides for.

##### Returns

Returns a `204 No Content` response on success. If the advanced find view does not exist, this call returns an error.

#### List all advanced find view overrides

```
DEFINITION
GET http://apiserver/advancedfindviews/:id/overrides

EXAMPLE REQUEST
$.get("http://localhost:49195/advancedfindviews/50038/overrides");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "3",
            "viewId": "50038",
            "field": "A03State",
            "title": "State",
            "displaySequence": 34,
            "sortSequence": null,
            "sortDirection": null,
            "width": "10em",
            "isHidden": true
        },
        {...},
    ]
}

```

Returns a list of all advanced find view overrides for the specified view.

##### Arguments

* id (required) - The id of the advanced find view

##### Returns

A dictionary with an items property that contains an array of up to limit advanced find view overrides, starting at index offset. Each entry in the array is a separate advanced find view override object. If no more advanced find view overrides are available, the resulting array will be empty. This request should never return an error.

### Apple Pay

#### Get an Apple Pay Configuration

```
DEFINITION
GET http://apiserver/applepay/configuration/:integrationConfigurationCode

EXAMPLE REQUEST
$.get("http://localhost:49195/applepay/configuration/APPLEPAY1");

EXAMPLE RESPONSE
{
    "merchantDisplayName": "Merchant Name",
    "merchantIdentifier": "merchant.com.example.applepay",
    "merchantCountry": "US"
}

```

Retrieves the non-sensitive properties of an Apple Pay configuration.

##### Arguments

* integrationConfigurationCode (required) - The integration configuration code for which to retrieve the configuration.

##### Returns

Returns an Apple Pay configuration object.

### Batches

#### Create a standard batch

```
DEFINITION
POST http://apiserver/batches

EXAMPLE REQUEST
$.post("http://localhost:49195/batches", {
    "batchDate": "2012-09-13",
    "company": "010",
    "currency": "USD"
});

EXAMPLE RESPONSE
{
    "id": "17098",
    "type": "S",
    "batchDate": "2012-09-13",
    "closeDate": null,
    "status": "O",
    "controlAmount": 0,
    "controlNumber": 0,
    "category": null,
    "company": "010",
    "currency": "USD",
    "assignee": null,
    "defaultPaymentType": null,
    "defaultSource": null,
    "creditCardPaymentGatewayCode": null,
    "creditCardPaymentGatewayDescription": null,
    "eftPaymentGatewayCode": null,
    "eftPaymentGatewayDescription": null
}

```

Creates a new standard batch object.

##### Arguments

* batchDate (required) - The batch date.
* company (required) - The company code of the batch.
* currency (required) - The currency code of the batch.
* controlAmount (optional) - The total amount of all transactions that are expected to be in the batch.
* countrolNumber (optional) - The number of transaction that are expected to be in the batch.
* category (optional) - The category code of the batch.
* assignee (optional) - The username of the person processing the batch.
* defaultPaymentType (optional) - The default payment type for each transaction in the batch.
* defaultSource (optional) - The default source for each transaction in the batch.
* creditCardPaymentGatewayCode (optional) - For credit card payment types, the code of the override company payment gateway to be used.
* eftPaymentGatewayCode (optional) - For EFT payment types, the code of the override company payment gateway to be used.

##### Returns

Returns a standard batch object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an invalid company code or currency code).

#### Create an automatic batch

```
DEFINITION
POST http://apiserver/batches

EXAMPLE REQUEST
$.post("http://localhost:49195/batches", {
    "type": "A",
    "company": "10",
});

EXAMPLE RESPONSE
{
    "id": "6561",
    "type": "A",
    "batchDate": "2014-09-02",
    "closeDate": null,
    "controlAmount": 0,
    "controlNumber": 0,
    "category": null,
    "company": "10",
    "currency": "USD",
    "assignee": "jsmith",
    "defaultPaymentType": null,
    "defaultSource": null,
    "isClosed": true,
    "creditCardPaymentGatewayCode": null,
    "creditCardPaymentGatewayDescription": null,
    "eftPaymentGatewayCode": null,
    "eftPaymentGatewayDescription": null
}

```

Creates a new automatic batch object.

##### Arguments

* type (required) - The batch type (A).
* company (required) - The company code of the batch

##### Returns

Returns an automatic batch object if the call succeeded. Returns an error if the parameters are invalid (e.g. specifying an invalid company code).

#### Retrieve a batch

```
DEFINITION
GET http://apiserver/batches/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/17098");

EXAMPLE RESPONSE
{
    "id": "17098",
    "type": "S",
    "batchDate": "2012-09-13",
    "closeDate": null,
    "status": "O",
    "controlAmount": 0,
    "controlNumber": 0,
    "category": null,
    "company": "010",
    "currency": "USD",
    "assignee": null,
    "defaultPaymentType": null,
    "defaultSource": null,
    "creditCardPaymentGatewayCode": null,
    "creditCardPaymentGatewayDescription": null,
    "eftPaymentGatewayCode": null,
    "eftPaymentGatewayDescription": null
}

```

Retrieves the details of an existing batch. You need only supply the batch number.

##### Arguments

* id (required) - The batch number of the batch to retrieve.

##### Returns

Returns a batch object if a valid id was provided.

#### Update a batch

```
DEFINITION
POST http://apiserver/batches/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/17098", {
    "currency": "CAD"
});

EXAMPLE RESPONSE
{
    "id": "17098",
    "type": "S",
    "batchDate": "2012-09-13",
    "closeDate": null,
    "status": "O"
    "controlAmount": 0,
    "controlNumber": 0,
    "category": null,
    "company": "020",
    "currency": "CAD",
    "assignee": null,
    "defaultPaymentType": null,
    "deafultSource": null,
    "creditCardPaymentGatewayCode": null,
    "creditCardPaymentGatewayDescription": null,
    "eftPaymentGatewayCode": null,
    "eftPaymentGatewayDescription": null
}


```

Updates the specified batch by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

If isClosed is set to true and the control amount and control number don't match actual values, this method will return an error.

##### Arguments

* batchDate (optional) - The batch date.
* company (optional) - The company code of the batch.
* currency (optional) - The currency code of the batch.
* controlAmount (optional) - The total amount of all transactions that are expected to be in the batch.
* countrolNumber (optional) - The number of transaction that are expected to be in the batch.
* category (optional) - The category code of the batch.
* assignee (optional) - The username of the person processing the batch.
* defaultPaymentType (optional) - The default payment type for each transaction in the batch.
* defaultSource (optional) - The default source for each transaction in the batch.
* creditCardPaymentGatewayCode (optional) - For credit card payment types, the code of the override company payment gateway to be used.
* eftPaymentGatewayCode (optional) - For EFT payment types, the code of the override ompany payment gateway to be used.

##### Returns

Returns the batch object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid company code or currency code).

#### Delete a batch

```
DEFINITION
DELETE http://apiserver/batches/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/batches/17098", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a batch. It cannot be undone.

##### Arguments

* id (required) - The batch number of the batch to be deleted.

##### Returns

Returns a 204 No Content response on success. If the batch number does not exist, this call returns an error.

#### List all batches

```
DEFINITION
GET http://apiserver/batches

EXAMPLE REQUEST
$.get("http://localhost:49195/batches?status=O");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 344
    }
    "items": [
        {
            "id": "17098",
            "type": "S",
            "batchDate": "2012-09-13",
            "closeDate": null,
            "status": "O",
            "controlAmount": 0,
            "controlNumber": 0,
            "category": null,
            "company": "010",
            "currency": "USD",
            "assignee": null,
            "defaultPaymentType": null,
            "defaultSource": null,
            "creditCardPaymentGatewayCode": null,
            "creditCardPaymentGatewayDescription": null,
            "eftPaymentGatewayCode": null,
            "eftPaymentGatewayDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all batches matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id () - Filter list by partial match in batch number.
* category () - Filter list by partial match in batch category.
* assignee () - Filter list by partial match in assignee username.
* controlAmount () - Filter list by exact match on control amount.
* batchDate () - Filter list by batch date date on the specified value.
* batchStartDate () - Filter list by batch date on or after the specified value. Only used if batchDate is not provided.
* batchEndDate () - Filter list by batch date on or before the specified value. Only used if batchDate is not provided.
* closeDate () - Filter list by close date on the specified value.
* closeStartDate () - Filter list by close date on or after the specified value. Only used if closeDate is not provided.
* closeEndDate () - Filter list by close date on or before the specified value. Only used if closeDate is not provided.
* status () - Filter list by batch status.
* type () - Filter list by batch type.

##### Returns

A dictionary with an items property that contains an array of up to limit batches, starting at index offset. Each entry in the array is a separate batch object. If no more batches are available, the resulting array will be empty. This request should never return an error.

### Batch Attachments

#### Create a batch attachment

```
DEFINITION
POST http://apiserver/batches/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new batch attachment object

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a batch attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Retrieve a batch attachment

```
DEFINITION
GET http://apiserver/batches/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing batch attachment. You need only supply the batch id and batch attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a batch attachment object if a valid id was provided.

#### Update a batch attachment

```
DEFINITION
POST http://apiserver/batches/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified batch attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type. Must be a defined attachment type.
* url (optional) - The url of the attachment type.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the batch attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined attachment type or attachment url).

#### Delete a batch attachment

```
DEFINITION
DELETE http://apiserver/batches/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/batches/7399/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a batch attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the batch attachment id does not exist, this call returns an error.

#### List all batch attachments

```
DEFINITION
GET http://apiserver/batches/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all batch attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit batch attachments, starting at index offset. Each entry in the array is a separate batch attachment object. If no more batch attachments are available, the resulting array will be empty. This request should never return an error.

### Batch Codes

#### Create a batch code

```
DEFINITION
POST http://apiserver/batches/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/codes", {
    "type": "BATDEPT",
    "value": "MP"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "BATDEPT",
    "typeDescription": "Batch Department Ownership",
    "value": "MP",
    "valueDescription": "Mail Processing Dept",
    "isActive": true
}

```

Creates a new batch code object

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a batch code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a batch code

```
DEFINITION
GET http://apiserver/batches/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/codes/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "BATDEPT",
    "typeDescription": "Batch Department Ownership",
    "value": "MP",
    "valueDescription": "Mail Processing Dept",
    "isActive": true
}

```

Retrieves the details of an existing batch code. You need only supply the batch id and batch code id.

##### Returns

Returns a batch code object if a valid id was provided.

#### Update a batch code

```
DEFINITION
POST http://apiserver/batches/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/codes/16", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "BATDEPT",
    "typeDescription": "Batch Department Ownership",
    "value": "MP",
    "valueDescription": "Mail Processing Dept",
    "isActive": false
}


```

Updates the specified batch code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the batch code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a batch code

```
DEFINITION
DELETE http://apiserver/batches/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/batches/7399/codes/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a batch code. It cannot be undone.

##### Arguments

* id (required) - The id of the account code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the batch code id does not exist, this call returns an error.

#### List all batch codes

```
DEFINITION
GET http://apiserver/batches/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "16",
            "type": "BATDEPT",
            "typeDescription": "Batch Department Ownership",
            "value": "MP",
            "valueDescription": "Mail Processing Dept",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all batch codes.

##### Returns

A dictionary with an items property that contains an array of up to limit batch codes, starting at index offset. Each entry in the array is a separate batch code object. If no more batch codes are available, the resulting array will be empty. This request should never return an error.

### Batch Dates

#### Create a batch date

```
DEFINITION
POST http://apiserver/batches/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/dates", {
    "type": "BATMDATE",
    "value": "2015-02-11"
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "BATMDATE",
    "typeDescription": "Batch Mail Received Date",
    "value": "2015-02-11",
    "isActive": true
}

```

Creates a new batch date object

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be a defined value of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a batch date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Retrieve a batch date

```
DEFINITION
GET http://apiserver/batches/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/dates/16");

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "BATMDATE",
    "typeDescription": "Batch Mail Received Date",
    "value": "2015-02-11",
    "isActive": true
}

```

Retrieves the details of an existing batch date. You need only supply the batch id and batch date id.

##### Returns

Returns a batch date object if a valid id was provided.

#### Update a batch date

```
DEFINITION
POST http://apiserver/batches/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/dates/16", {
    "value": "2015-03-11",
});

EXAMPLE RESPONSE
{
    "id": "16",
    "type": "BATMDATE",
    "typeDescription": "Batch Mail Received Date",
    "value": "2015-03-11",
    "isActive": false
}


```

Updates the specified batch date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be a defined value of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the batch date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a batch date

```
DEFINITION
DELETE http://apiserver/batches/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/batches/7399/dates/16", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a batch date. It cannot be undone.

##### Arguments

* id (required) - The id of the account date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the batch date id does not exist, this call returns an error.

#### List all batch dates

```
DEFINITION
GET http://apiserver/batches/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "16",
            "type": "BATMDATE",
            "typeDescription": "Batch Mail Received Date",
            "value": "2015-03-11",
            "isActive": false
        },
        {...},
        {...}
    ]
}

```

Returns a list of all batch dates.

##### Returns

A dictionary with an items property that contains an array of up to limit batch dates, starting at index offset. Each entry in the array is a separate batch date object. If no more batch dates are available, the resulting array will be empty. This request should never return an error.

### Batch Notes

#### Create a batch note

```
DEFINITION
POST http://apiserver/batches/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/notes", {
    "type": "BATDEPT",
    "value": "MP"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "DDCBATCHNT",
    "description": "Batch Note Type",
    "shortComment": "example",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Creates a new batch note object

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a batch note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a batch note

```
DEFINITION
GET http://apiserver/batches/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/notes/9");

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "DDCBATCHNT",
    "description": "Batch Note Type",
    "shortComment": "example",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}

```

Retrieves the details of an existing batch note. You need only supply the batch id and batch note id.

##### Returns

Returns a batch note object if a valid id was provided.

#### Update a batch note

```
DEFINITION
POST http://apiserver/batches/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/notes/9", {
    "shortComment": "time for an edit"
});

EXAMPLE RESPONSE
{
    "id": "9",
    "type": "DDCBATCHNT",
    "description": "Batch Note Type",
    "shortComment": "time for an edit",
    "longComment": "This is an example comment.\nMultiple lines are supported."
}


```

Updates the specified batch note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the batch note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type).

#### Delete a batch note

```
DEFINITION
DELETE http://apiserver/batches/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/batches/7399/notes/11", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a batch note. It cannot be undone.

##### Arguments

* id (required) - The id of the account note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the batch note id does not exist, this call returns an error.

#### List all batch notes

```
DEFINITION
GET http://apiserver/batches/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/notes");

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
            "type": "DDCBATCHNT",
            "description": "Batch Note Type",
            "shortComment": "example",
            "longComment": "This is an example comment.\nMultiple lines are supported."
        },
        {...},
        {...}
    ]
}

```

Returns a list of all batch notes.

##### Returns

A dictionary with an items property that contains an array of up to limit batch notes, starting at index offset. Each entry in the array is a separate batch note object. If no more batch notes are available, the resulting array will be empty. This request should never return an error.

### Batch Numbers

#### Create a batch number

```
DEFINITION
POST http://apiserver/batches/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/numbers", {
    "type": "BATDEPT",
    "value": "MP"
});

EXAMPLE RESPONSE
{
    "id": "10",
    "isActive": true,
    "isMultiValue": true,
    "type": "DDCBATNR2",
    "description": "Batch Number 2",
    "value": 42
}

```

Creates a new batch number object

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a batch number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a batch number

```
DEFINITION
GET http://apiserver/batches/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/numbers/10");

EXAMPLE RESPONSE
{
    "id": "10",
    "isActive": true,
    "isMultiValue": true,
    "type": "DDCBATNR2",
    "description": "Batch Number 2",
    "value": 42
}

```

Retrieves the details of an existing batch number. You need only supply the batch id and batch number id.

##### Returns

Returns a batch number object if a valid id was provided.

#### Update a batch number

```
DEFINITION
POST http://apiserver/batches/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/batches/7399/numbers/10", {
    "value": 78
});

EXAMPLE RESPONSE
{
    "id": "10",
    "isActive": true,
    "isMultiValue": true,
    "type": "DDCBATNR2",
    "description": "Batch Number 2",
    "value": 78
}


```

Updates the specified batch number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the batch number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Delete a batch number

```
DEFINITION
DELETE http://apiserver/batches/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/batches/7399/numbers/10", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a batch number. It cannot be undone.

##### Arguments

* id (required) - The id of the account number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the batch number id does not exist, this call returns an error.

#### List all batch numbers

```
DEFINITION
GET http://apiserver/batches/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/batches/7399/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10",
            "isActive": true,
            "isMultiValue": true,
            "type": "DDCBATNR2",
            "description": "Batch Number 2",
            "value": 42
        },
        {...},
        {...}
    ]
}

```

Returns a list of all batch numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit batch numbers, starting at index offset. Each entry in the array is a separate batch number object. If no more batch numbers are available, the resulting array will be empty. This request should never return an error.

### Braintree

#### Get Braintree Configuration

```
DEFINITION
GET http://apiserver/braintree/configuration/{companyCode}/{paymentGatewayCode}

EXAMPLE REQUEST
$.get("http://localhost:49195/braintree/configuration/BRAINTREE/BTREE");

EXAMPLE RESPONSE
{
    "achMandateText": "I authorize Braintree, a service of Paypal, on behalf of Son Ministries (i) to verify my bank account information using bank information and consumer reports and (ii) to debit my bank account.",
    "isCvvRequired": true
}

```

Retrieves the Braintree configuration without returning sensitive data such as private and public keys.

##### Arguments

* companyCode (required) - The company associated with the braintree configuration.
* paymentGatewayCode (required) - The company payment gateway associated with the braintree configuration.

##### Returns

Returns a Braintree configuration object.

#### Get Braintree Client Token

```
DEFINITION
GET http://apiserver/braintreeclienttoken/{companyCode}/{paymentGatewayCode}

EXAMPLE REQUEST
$.get("http://localhost:49195/braintreeclienttoken/BRAINTREE/BTREE");

EXAMPLE RESPONSE
{
    "clientToken": "eyJ2ZXJzaW9uIjoyLCJhdXRob3JpemF0aW9uRmluZ2VycHJpbnQiOiJleUowZVhBaU9pSktWMVFpTENKaGJHY2lPaUpGVXpJMU5pSXNJbXRwWkNJNklqSXdNVGd3TkRJmk1UWXRjMkZ1WkdKdmVDSXNJbWx6Y3lJNkltaDBkSEJ6T2k4dllYQnBMbk5oYm1SaWIzZ3VZbkpoYVc1MGNtVmxaMkYwWlhkaGVTNWpiMjBpZlEuZXlKbGVIQWlPakUyTkRNME5qVTFOallzSW1wMGFTSTZJbUZsTkRJNE1EazNMV000TVRJdE5HVXdOQzFpT1RNNExXWTJPRFEwTkRCaFpEZzFZeUlzSW5OMVlpSTZJbVoyWkhkeFkyTjBZM0IyYlhodGVUZ2lMQ0pwYzNNaU9pSm9kSFJ3Y3pvdkwyRndhUzV6WVc1a1ltOTRMbUp5WVdsdWRISmxaV2RoZEdWM1lYa3VZMjl0SWl3aWJXVnlZMmhoYm5RaU9uc2ljSFZpYkdsalgybGtJam9pWm5aa2QzRmpZM1JqY0hadGVHMTVPQ0lzSW5abGNtbG1lVjlqWVhKa1gySjVYMlJsWm1GMWJIUWlPblJ5ZFdWOUxDSnlhV2RvZEhNaU9sc2liV0Z1WVdkbFgzWmhkV3gwSWwwc0luTmpiM0JsSWpwYklrSnlZV2x1ZEhKbFpUcFdZWFZzZENKZExDSnZjSFJwYjI1eklqcDdmWDAubEFpNmsxSHhWODR3dUlLcEYwZUVnMV9vYXhyYnFVdmZReVdjdkpHQVdWNEpBZ25uVnlZc2VGSVkxYmY1RE1lQVN3MDE3cVdRN0ZFdDBJbVVpeWN5a2ciLCJjb25maWdVcmwiOiJodHRwczovL2FwaS5zYW5kYm94LmJyYWludHJlZWdhdGV3YXkuY29tOjQ0My9tZXJjaGFudHMvZnZkd3FjY3RjcHZteG15OC9jbGllbnRfYXBpL3YxL2NvbmZpZ3VyYXRpb24iLCJncmFwaFFMIjp7InVybCI6Imh0dHBzOi8vcGF5bWVudHMuc2FuZGJveC5icmFpbnRyZWUtYXBpLmNvbS9ncmFwaHFsIiwiZGF0ZSI6IjIwMTgtMDUtMDgiLCJmZWF0dXJlcyI6WyJ0b2tlbml6ZV9jcmVkaXRfY2FyZHMiXX0sImNsaWVudEFwaVVybCI6Imh0dHBzOi8vYXBpLnNhbmRib3guYnJhaW50cmVlZ2F0ZXdheS5jb206NDQzL21lcmNoYW50cy9mdmR3cWNjdGNwdm14bXk4L2NsaWVudF9hcGkiLCJlbnZpcm9ubWVudCI6InNhbmRib3giLCJtZXJjaGFudElkIjoiZnZkd3FjY3RjcHZteG15OCIsImFzc2V0c1VybCI6Imh0dHBzOi8vYXNzZXRzLmJyYWludHJlZWdhdGV3YXkuY29tIiwiYXV0aFVybCI6Imh0dHBzOi8vYXV0aC52ZW5tby5zYW5kYm94LmJyYWludHJlZWdhdGV3YXkuY29tIiwidmVubW8iOiJvZmYiLCJjaGFsbGVuZ2VzIjpbXSwidGhyZWVEU2VjdXJlRW5hYmxlZCI6dHJ1ZSwiYW5hbHl0aWNzIjp7InVybCI6Imh0dHBzOi8vb3JpZ2luLWFuYWx5dGljcy1zYW5kLnNhbmRib3guYnJhaW50cmVlLWFwaS5jb20vZnZkd3FjY3RjcHZteG15OCJ9LCJwYXlwYWxFbmFibGVkIjp0cnVlLCJicmFpbnRyZWVfYXBpIjp7InVybCI6Imh0dHBzOi8vcGF5bWVudHMuc2FuZGJveC5icmFpbnRyZWUtYXBpLmNvbSIsImFjY2Vzc190b2tlbiI6ImV5SjBlWEFpT2lKS1YxUWlMQ0poYkdjaU9pSkZVekkxTmlJc0ltdHBaQ0k2SWpJd01UZ3dOREkyTVRZdGMyRnVaR0p2ZUNJc0ltbHpjeUk2SW1oMGRIQnpPaTh2WVhCcExuTmhibVJpYjNndVluSmhhVzUwY21WbFoyRjBaWGRoZVM1amIyMGlmUS5leUpsZUhBaU9qRTJORE0wTmpVMU5qWXNJbXAwYVNJNklqTTRPV1k1TkRRM0xUZ3dOamt0TkRGbE15MWlOR0ZoTFdNME5UUXhNak5rWXpjME9DSXNJbk4xWWlJNkltWjJaSGR4WTJOMFkzQjJiWGh0ZVRnaUxDSnBjM01pT2lKb2RIUndjem92TDJGd2FTNXpZVzVrWW05NExtSnlZV2x1ZEhKbFpXZGhkR1YzWVhrdVkyOXRJaXdpYldWeVkyaGhiblFpT25zaWNIVmliR2xqWDJsa0lqb2lablprZDNGalkzUmpjSFp0ZUcxNU9DSXNJblpsY21sbWVWOWpZWEprWDJKNVgyUmxabUYxYkhRaU9uUnlkV1Y5TENKeWFXZG9kSE1pT2xzaWRHOXJaVzVwZW1VaUxDSnRZVzVoWjJWZmRtRjFiSFFpWFN3aWMyTnZjR1VpT2xzaVFuSmhhVzUwY21WbE9sWmhkV3gwSWwwc0ltOXdkR2x2Ym5NaU9udDlmUS52WGQ0MjhZMEs2S04xNlByRHczMno2SjBjQjVBRlA4SDVZSkdRZF9hV1RkSG9hX2kxS2JYalFVVGlsUmxYTGQxdmNZb1pYU01nMzdGVU84al9Ib0lzQSJ9LCJwYXlwYWwiOnsiYmlsbGluZ0FncmVlbWVudHNFbmFibGVkIjp0cnVlLCJlbnZpcm9ubWVudE5vTmV0d29yayI6dHJ1ZSwidW52ZXR0ZWRNZXJjaGFudCI6ZmFsc2UsImFsbG93SHR0cCI6dHJ1ZSwiZGlzcGxheU5hbWUiOiJEb25vckRpcmVjdCIsImNsaWVudElkIjpudWxsLCJwcml2YWN5VXJsIjoiaHR0cDovL2V4YW1wbGUuY29tL3BwIiwidXNlckFncmVlbWVudFVybCI6Imh0dHA6Ly9leGFtcGxlLmNvbS90b3MiLCJiYXNlVXJsIjoiaHR0cHM6Ly9hc3NldHMuYnJhaW50cmVlZ2F0ZXdheS5jb20iLCJhc3NldHNVcmwiOiJodHRwczovL2NoZWNrb3V0LnBheXBhbC5jb20iLCJkaXJlY3RCYXNlVXJsIjpudWxsLCJlbnZpcm9ubWVudCI6Im9mZmxpbmUiLCJicmFpbnRyZWVDbGllbnRJZCI6Im1hc3RlcmNsaWVudDMiLCJtZXJjaGFudEFjY291bnRJZCI6ImRvbm9yZGlyZWN0IiwiY3VycmVuY3lJc29Db2RlIjoiVVNEIn19"
}

```

Retrieves the Braintree client token.

##### Arguments

* companyCode (required) - The company associated with the braintree configuration.
* paymentGatewayCode (required) - The company payment gateway code associated with the braintree configuration.

##### Returns

Returns a braintree client token that is needed for interacting with the Braintree payment gateway.

### CardConnect

#### Get CardConnect Configuration

```
DEFINITION
GET http://apiserver/cardconnect/configuration/{companyCode}/{paymentGatewayCode}

EXAMPLE REQUEST
$.get("http://localhost:49195/cardconnect/configuration/CCONNECT/CLOVERCONN");

EXAMPLE RESPONSE
{
    "isIframeEnabled": true,
    "iframeUrl": "https://ddc.cardconnect.com/itoke/ajax-tokenizer.html"
}

```

Retrieves the CardConnect configuration without returning sensitive data such as private and public keys.

##### Arguments

* companyCode (required) - The company associated with the cardconnect configuration.
* paymentGatewayCode (required) - The company payment gateway associated with the cardconnect configuration.

##### Returns

Returns a CardConnect configuration object. Returns a `204 No Content` response if the integration configuration does not exist.

### Google Pay

#### Get a Google Pay Configuration

```
DEFINITION
GET http://apiserver/googlepay/configuration/:integrationConfigurationCode/company/:companyCode/paymentgateway/:paymentGatewayCode

EXAMPLE REQUEST
$.get("http://localhost:49195/googlepay/configuration/GOOGLE1/company/COMPANY1/paymentgateway/CCONNECT");

EXAMPLE RESPONSE
{
    "environment": "TEST",
    "merchantCountry": "US"
    "merchantDisplayName": "Merchant Name",
    "merchantIdentifier": "1119388440244",
    "paymentProviderIdentifier": "119999111"
}

```

Retrieves the non-sensitive properties of a Google Pay configuration.

##### Arguments

* integrationConfigurationCode (required) - The integration configuration code for which to retrieve the configuration.
* companyCode (required) - The company code for which to retrieve the `paymentProviderIdentifier` in the returned configuration.
* paymentGatewayCode (required) - The company payment gateway code for which to retrieve the `paymentProviderIdentifier` in the returned configuration.

##### Returns

Returns an Google Pay configuration object.
(Note: Only Companies with `CCONNECT` as the Provider will return a `paymentProviderIdentifier`)

### Non-Cash Gifts

#### Create a non-cash gift

```
DEFINITION
POST http://apiserver/noncashgifts

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts", {
    "account": "1483320",
    "date": "2013-05-08",
    "status": "C",
    "description": "Car",
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "response": {
        "type": "MAIL",
        "letter": "CHURCH",
        "paragraphs": [
            {
                "type": "PR1"
            }
        ]
    }
});

EXAMPLE RESPONSE
{
    "id": "23832813",
    "account": "1483320",
    "date": "2013-05-08",
    "status": "C",
    "description": "Car",
    "expectedDate": null,
    "committedValue": null,
    "receivedValue": null,
    "liquidationValue": null,
    "liquidationCost": null,
    "liquidationDate": null,
    "liquidationComment": null,
    "comment": null
}

```

Creates a new non-cash gift object.

##### Arguments

* account (required) - The account number of the non-cash gift donor.
* date (required) - The date of the non-cash gift.
* status (required) - The status of the non-cash gift. Must be a valid <a href="#non-cash-gift-status">non-cash gift status</a>.
* description (optional) - The description of the non-cash gift.
* expectedDate (optional) - The expected date of the non-cash gift.
* committedValue (optional) - The committed value of the non-cash gift.
* receivedValue (optional) - The received value of the non-cash gift.
* liquidationValue (optional) - The liquidation value of the non-cash gift.
* liquidationCost (optional) - The liquidation cost of the non-cash gift.
* liquidationDate (optional) - The liquidation date of the non-cash gift.
* liquidationComment (optional) - The liquidation comment of the non-cash gift.
* comment (optional) - The comment of the non-cash gift.
* response (optional) - A response object for the non-cash gift. Must include at least a letter code.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.

##### Returns

Returns a non-cash gift object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined pledge code).

#### Retrieve a non-cash gift

```
DEFINITION
GET http://apiserver/noncashgifts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813");

EXAMPLE RESPONSE
{
    "id": "23832813",
    "account": "1483320",
    "date": "2013-05-08",
    "status": "C",
    "description": "Car",
    "expectedDate": null,
    "committedValue": null,
    "receivedValue": null,
    "liquidationValue": null,
    "liquidationCost": null,
    "liquidationDate": null,
    "liquidationComment": null,
    "comment": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null
}

```

Retrieves the header of an existing non-cash gift. You need only supply the non-cash gift header id.

##### Arguments

* id (required) - The header id of the non-cash gift to retrieve.

##### Returns

Returns a non-cash gift object if a valid id was provided.

#### Update a non-cash gift

```
DEFINITION
POST http://apiserver/noncashgifts/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813", {
    "description": "Old car"
});

EXAMPLE RESPONSE
{
    "id": "23832813",
    "account": "1483320",
    "date": "2013-05-08",
    "status": "C",
    "description": "Old car",
    "expectedDate": null,
    "committedValue": null,
    "receivedValue": null,
    "liquidationValue": null,
    "liquidationCost": null,
    "liquidationDate": null,
    "liquidationComment": null,
    "comment": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null
}


```

Updates the specified non-cash gift by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* account (optional) - The account number of the non-cash gift donor.
* date (optional) - The date of the non-cash gift.
* status (optional) - The status of the non-cash gift. Must be a valid <a href="#non-cash-gift-status">non-cash gift status</a>.
* description (optional) - The description of the non-cash gift.
* expectedDate (optional) - The expected date of the non-cash gift.
* committedValue (optional) - The committed value of the non-cash gift.
* receivedValue (optional) - The received value of the non-cash gift.
* liquidationValue (optional) - The liquidation value of the non-cash gift.
* liquidationCost (optional) - The liquidation cost of the non-cash gift.
* liquidationDate (optional) - The liquidation date of the non-cash gift.
* liquidationComment (optional) - The liquidation comment of the non-cash gift.
* comment (optional) - The comment of the non-cash gift.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.

##### Returns

Returns the non-cash gift object if the update succeeded. Returns an error if update parameters are invalid (e.g. changing status to an invalid value).

#### Delete a non-cash gift

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift. It cannot be undone.

##### Arguments

* id (required) - The header id of the non-cash gift to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift header id does not exist, this call returns an error.

#### List all non-cash gifts

```
DEFINITION
GET http://apiserver/noncashgifts

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 15
    },
    "items": [
        {
            "id": "23832813",
            "account": "1483320",
            "date": "2013-05-08",
            "status": "C",
            "description": "Car",
            "expectedDate": null,
            "committedValue": null,
            "receivedValue": null,
            "liquidationValue": null,
            "liquidationCost": null,
            "liquidationDate": null,
            "liquidationComment": null,
            "comment": null,
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gifts.

##### Arguments

* account () - Filter list by exact match in account number

##### Returns

A dictionary with an items property that contains an array of up to limit non-cash gifts, starting at index offset. Each entry in the array is a separate non-cash gift object. If no more non-cash gifts are available, the resulting array will be empty. This request should never return an error.

#### Non-Cash Gift Status

* C () - Commitment Received
* R () - Received Asset
* L () - Liquidated Asset

### Non-Cash Gift Attachments

#### Create a non-cash gift attachment

```
DEFINITION
POST http://apiserver/noncashgifts/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new non-cash gift attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a non-cash gift attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve a non-cash gift attachment

```
DEFINITION
GET http://apiserver/noncashgifts/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing non-cash gift attachment. You need only supply the non-cash gift attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a non-cash gift attachment object if a valid id was provided.

#### Update a non-cash gift attachment

```
DEFINITION
POST http://apiserver/noncashgifts/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified non-cash gift attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type code. Must be a defined attachment type code.
* url (optional) - The url where the attachment is located.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the non-cash gift attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined non-cash gift attachment type code).

#### Delete a non-cash gift attachment

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the non-cash gift attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift attachment id does not exist, this call returns an error.

#### List all non-cash gift attachments

```
DEFINITION
GET http://apiserver/noncashgifts/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gift attachments.

##### Returns

A dictionary with an items property that contains an array of up to limit non-cash gift attachments, starting at index offset. Each entry in the array is a separate non-cash gift attachment object. If no more non-cash gift attachments are available, the resulting array will be empty. This request should never return an error.

### Non-Cash Gift Codes

#### Create a non-cash gift code

```
DEFINITION
POST http://apiserver/noncashgifts/:id/codes

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/codes", {
    "type": "DDCNCGTCD3",
    "value": "JANUS"
});

EXAMPLE RESPONSE
{
    "id": "60",
    "type": "DDCNCGTCD3",
    "value": "JANUS",
    "isActive": true
}

```

Creates a new non-cash gift code object.

##### Arguments

* type (required) - The code type. Must be a defined code type.
* value (required) - The value of the code type. Must be a defined value of the specified code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns a non-cash gift code object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Retrieve a non-cash gift code

```
DEFINITION
GET http://apiserver/noncashgifts/:id/codes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/codes/60");

EXAMPLE RESPONSE
{
    "id": "60",
    "type": "DDCNCGTCD3",
    "value": "JANUS",
    "isActive": true
}

```

Retrieves the details of an existing non-cash gift code. You need only supply the non-cash gift code id.

##### Arguments

* id (required) - The id of the non-cash gift code to retrieve.

##### Returns

Returns a non-cash gift code object if a valid id was provided.

#### Update a non-cash gift code

```
DEFINITION
POST http://apiserver/noncashgifts/:id/codes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/codes/60", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "60",
    "type": "DDCNCGTCD3",
    "value": "JANUS",
    "isActive": false
}


```

Updates the specified non-cash gift code by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The code type. Must be a defined code type.
* value (optional) - The value of the code type. Must be a defined value of the code type.
* isActive (optional) - Whether or not the code is active.

##### Returns

Returns the non-cash gift code object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined code type or code type value).

#### Delete a non-cash gift code

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id/codes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813/codes/60", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift code. It cannot be undone.

##### Arguments

* id (required) - The id of the non-cash gift code to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift code id does not exist, this call returns an error.

#### List all non-cash gift codes

```
DEFINITION
GET http://apiserver/noncashgifts/:id/codes

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/codes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "60",
            "type": "DDCNCGTCD3",
            "value": "JANUS",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gift codes.

##### Returns

A dictionary with an items property that contains an array of up to limit non-cash gift codes, starting at index offset. Each entry in the array is a separate non-cash gift code object. If no more non-cash gift codes are available, the resulting array will be empty. This request should never return an error.

### Non-Cash Gift Dates

#### Create a non-cash gift date

```
DEFINITION
POST http://apiserver/noncashgifts/:id/dates

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/dates", {
    "type": "DDCNCGTDT1",
    "value": "2014-01-11"
});

EXAMPLE RESPONSE
{
    "id": "27",
    "type": "DDCNCGTDT1",
    "value": "2014-01-11",
    "isActive": true
}

```

Creates a new non-cash gift date object.

##### Arguments

* type (required) - The date type. Must be a defined date type.
* value (required) - The value of the date type. Must be within an active range of the specified date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns a non-cash gift date object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined date type or a value outside of all active ranges for the date type).

#### Retrieve a non-cash gift date

```
DEFINITION
GET http://apiserver/noncashgifts/:id/dates/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/dates/27");

EXAMPLE RESPONSE
{
    "id": "27",
    "type": "DDCNCGTDT1",
    "value": "2014-01-11",
    "isActive": true
}

```

Retrieves the details of an existing non-cash gift date. You need only supply the non-cash gift date id.

##### Arguments

* id (required) - The id of the non-cash gift date to retrieve.

##### Returns

Returns a non-cash gift date object if a valid id was provided.

#### Update a non-cash gift date

```
DEFINITION
POST http://apiserver/noncashgifts/:id/dates/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/dates/27", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "27",
    "type": "DDCNCGTDT1",
    "value": "2014-01-11",
    "isActive": false
}


```

Updates the specified non-cash gift date by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The date type. Must be a defined date type.
* value (optional) - The value of the date type. Must be within an active range of the date type.
* isActive (optional) - Whether or not the date is active.

##### Returns

Returns the non-cash gift date object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined date type or date type value).

#### Delete a non-cash gift date

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id/dates/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813/dates/27", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift date. It cannot be undone.

##### Arguments

* id (required) - The id of the non-cash gift date to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift date id does not exist, this call returns an error.

#### List all non-cash gift dates

```
DEFINITION
GET http://apiserver/noncashgifts/:id/dates

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/dates");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 12
    },
    "items": [
        {
            "id": "27",
            "type": "DDCNCGTDT1",
            "value": "2014-01-11",
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gift dates.

##### Returns

A dictionary with an items property that contains an array of up to limit non-cash gift dates, starting at index offset. Each entry in the array is a separate non-cash gift date object. If no more non-cash gift dates are available, the resulting array will be empty. This request should never return an error.

### Non-Cash Gift Details

#### Create a non-cash gift detail

```
DEFINITION
POST http://apiserver/noncashgifts/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/details", {
    "source": "ABC08",
    "project": "220000"
});

EXAMPLE RESPONSE
{
    "id": "241",
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "relatedAccount": null,
    "pledgeCode": null,
    "pledge", null,
    "totalAmount": null,
    "shortComment": null
}

```

Creates a new non-cash gift detail object.

##### Arguments

* source (required) - The source code of the non-cash gift detail.
* project (required) - The project code of the non-cash gift detail.
* subaccount (optional) - The sub account of the non-cash gift detail.
* relatedAccount (optional) - The associated account of the non-cash gift detail.
* pledge (optional) - The account pledge id of the non-cash gift detail.
* totalAmount (optional) - The total amount of the non-cash gift detail.
* shortComment (optional) - The short comment of the non-cash gift detail.

##### Returns

Returns a non-cash gift detail object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined source code or project code).

#### Retrieve a non-cash gift detail

```
DEFINITION
GET http://apiserver/noncashgifts/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/details/241");

EXAMPLE RESPONSE
{
    "id": "241",
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "relatedAccount": null,
    "pledgeCode": null,
    "pledge": null,
    "totalAmount": null,
    "shortComment": null
}

```

Retrieves the details of an existing non-cash gift detail. You need only supply the non-cash gift detail id.

##### Arguments

* id (required) - The id of the non-cash gift detail to retrieve.

##### Returns

Returns a non-cash gift detail object if a valid id was provided.

#### Update a non-cash gift detail

```
DEFINITION
POST http://apiserver/noncashgifts/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/details/241", {
    "totalAmount": 42
});

EXAMPLE RESPONSE
{
    "id": "241",
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "relatedAccount": null,
    "pledgeCode": null,
    "pledge", null,
    "totalAmount": 42,
    "shortComment": null
}


```

Updates the specified non-cash gift detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* source (optional) - The source code of the non-cash gift detail.
* project (optional) - The project code of the non-cash gift detail.
* subaccount (optional) - The sub account of the non-cash gift detail.
* relatedAccount (optional) - The associated account of the non-cash gift detail.
* pledgeCode (optional) - The pledge code of the non-cash gift detail.
* pledge (optional) - The account pledge id of the non-cash gift detail.
* totalAmount (optional) - The total amount of the non-cash gift detail.
* shortComment (optional) - The short comment of the non-cash gift detail.

##### Returns

Returns the non-cash gift detail object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined source code or project code).

#### Delete a non-cash gift detail

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813/details/1629", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift detail. It cannot be undone.

##### Arguments

* id (required) - The id of the non-cash gift detail to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift detail id does not exist, this call returns an error.

#### List all non-cash gift details

```
DEFINITION
GET http://apiserver/noncashgifts/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "241",
            "source": "ABC08",
            "project": "220000",
            "subaccount": null,
            "relatedAccount": null,
            "pledgeCode": null,
            "pledge", null,
            "totalAmount": null,
            "shortComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gift details.

##### Returns

A dictionary with an items property that contains an array of up to limit non-cash gift details, starting at index offset. Each entry in the array is a separate non-cash gift detail object. If no more non-cash gift details are available, the resulting array will be empty. This request should never return an error.

### Non-Cash Gift Notes

#### Create a non-cash gift note

```
DEFINITION
POST http://apiserver/noncashgifts/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/notes", {
    "type": "DDCNCGTNT1",
    "shortComment": "Non-Cash Gift Note"
});

EXAMPLE RESPONSE
{
    "id": "37",
    "type": "DDCNCGTNT1",
    "shortComment": "Non-Cash Gift Note",
    "longComment": null
}

```

Creates a new non-cash gift note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a non-cash gift note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a non-cash gift note

```
DEFINITION
GET http://apiserver/noncashgifts/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/notes/37");

EXAMPLE RESPONSE
{
    "id": "37",
    "type": "DDCNCGTNT1",
    "shortComment": "Non-Cash Gift Note",
    "longComment": null
}

```

Retrieves the details of an existing non-cash gift note. You need only supply the non-cash gift note id.

##### Arguments

* id (required) - The id of the non-cash gift note to retrieve.

##### Returns

Returns a non-cash gift note object if a valid id was provided.

#### Update a non-cash gift note

```
DEFINITION
POST http://apiserver/noncashgifts/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/notes/37", {
    "shortComment": null,
    "longComment": "Non-Cash Gift Note"
});

EXAMPLE RESPONSE
{
    "id": "37",
    "type": "DDCNCGTNT1",
    "shortComment": null,
    "longComment": "Non-Cash Gift Note"
}


```

Updates the specified non-cash gift note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the non-cash gift note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a non-cash gift note

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813/notes/37", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift note. It cannot be undone.

##### Arguments

* id (required) - The id of the non-cash gift note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift note id does not exist, this call returns an error.

#### List all non-cash gift notes

```
DEFINITION
GET http://apiserver/noncashgifts/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "37",
            "type": "DDCNCGTNT1",
            "shortComment": "Non-Cash Gift Note",
            "longComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gift notes.

##### Returns

A dictionary with an items property that contains an array of up to limit non-cash gift notes, starting at index offset. Each entry in the array is a separate non-cash gift note object. If no more non-cash gift notes are available, the resulting array will be empty. This request should never return an error.

### Non-Cash Gift Numbers

#### Create a non-cash gift number

```
DEFINITION
POST http://apiserver/noncashgifts/:id/numbers

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/numbers", {
    "type": "DDCNCGTNB1",
    "value": 878
});

EXAMPLE RESPONSE
{
    "id": "30",
    "type": "DDCNCGTNB1",
    "value": 878,
    "isActive": true
}

```

Creates a new non-cash gift number object.

##### Arguments

* type (required) - The number type. Must be a defined number type.
* value (required) - The value of the number type. Must be within an active range of the specified number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns a non-cash gift number object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined number type or a value outside of all active ranges for the number type).

#### Retrieve a non-cash gift number

```
DEFINITION
GET http://apiserver/noncashgifts/:id/numbers/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/numbers/30");

EXAMPLE RESPONSE
{
    "id": "30",
    "type": "DDCNCGTNB1",
    "value": 878,
    "isActive": true
}

```

Retrieves the details of an existing non-cash gift number. You need only supply the non-cash gift number id.

##### Arguments

* id (required) - The id of the non-cash gift number to retrieve.

##### Returns

Returns a non-cash gift number object if a valid id was provided.

#### Update a non-cash gift number

```
DEFINITION
POST http://apiserver/noncashgifts/:id/numbers/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/numbers/30", {
    "isActive": false
});

EXAMPLE RESPONSE
{
    "id": "30",
    "type": "DDCNCGTNB1",
    "value": 878,
    "isActive": false
}


```

Updates the specified non-cash gift number by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The number type. Must be a defined number type.
* value (optional) - The value of the number type. Must be within an active range of the number type.
* isActive (optional) - Whether or not the number is active.

##### Returns

Returns the non-cash gift number object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined number type or number type value).

#### Delete a non-cash gift number

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id/numbers/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813/numbers/30", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift number. It cannot be undone.

##### Arguments

* id (required) - The id of the non-cash gift number to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift number id does not exist, this call returns an error.

#### List all non-cash gift numbers

```
DEFINITION
GET http://apiserver/noncashgifts/:id/numbers

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/numbers");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "30",
            "type": "DDCNCGTNB1",
            "value": 878,
            "isActive": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gift numbers.

##### Returns

A dictionary with an items property that contains an array of up to limit non-cash gift numbers, starting at index offset. Each entry in the array is a separate non-cash gift number object. If no more non-cash gift numbers are available, the resulting array will be empty. This request should never return an error.

### Non-Cash Gift Response

#### Retrieve a non-cash gift response

```
DEFINITION
GET http://apiserver/noncashgifts/:id/response

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/response");

EXAMPLE RESPONSE
{
    "letter": "CHURCH",
    "completionText": null,
    "address": "230529",
    "status": "Y"
}

```

Retrieves the details of an existing non-cash gift response.

##### Returns

Returns the non-cash gift response object.

#### Update a non-cash gift response

```
DEFINITION
POST http://apiserver/noncashgifts/:id/response

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/response", {
    "address": "41"
});

EXAMPLE RESPONSE
{
    "letter": "CHURCH",
    "completionText": null,
    "address": "41",
    "status": "Y"
}


```

Updates the specified non-cash gift response by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* letter (optional) - The letter code of the response. Must be a defined letter code.
* completionText (optional) - The completion text of the response.
* address (optional) - The address id of the response.
* status (optional) - The status of the response. Must be a valid [response status](#response-status) value.

##### Returns

Returns the non-cash gift response object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined letter code).

### Non-Cash Gift Response Paragraphs

#### Create a non-cash gift response paragraph

```
DEFINITION
POST http://apiserver/noncashgifts/:id/response/paragraphs

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/response/paragraphs", {
    "type": "PR1",
    "completionText": "Thank you for your gift."
});

EXAMPLE RESPONSE
{
    "id": "53774",
    "type": "PR1",
    "completionText": "Thank you for your gift."
}

```

Creates a new non-cash gift response paragraph object.

##### Arguments

* type (required) - The paragraph type. Must be a defined paragraph type.
* completionText (optional) - The completion text.

##### Returns

Returns a non-cash gift response paragraph object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined paragraph type).

#### Retrieve a non-cash gift response paragraph

```
DEFINITION
GET http://apiserver/noncashgifts/:id/response/paragraphs/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/response/paragraphs/53774");

EXAMPLE RESPONSE
{
    "id": "53774",
    "type": "PR1",
    "completionText": "Thank you for your gift."
}

```

Retrieves the details of an existing non-cash gift response paragraph. You need only supply the non-cash gift response paragraph id.

##### Arguments

* id (required) - The id of the non-cash gift response paragraph to retrieve.

##### Returns

Returns a non-cash gift response paragraph object if a valid id was provided.

#### Update a non-cash gift response paragraph

```
DEFINITION
POST http://apiserver/noncashgifts/:id/response/paragraphs/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/noncashgifts/23832813/response/paragraphs/53774", {
    "type": "PR2"
});

EXAMPLE RESPONSE
{
    "id": "53774",
    "type": "PR2",
    "completionText": "Thank you for your gift."
}


```

Updates the specified non-cash gift response paragraph by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The paragraph type. Must be a defined paragraph type.
* completionText (optional) - The completion text.

##### Returns

Returns the non-cash gift response paragraph object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined paragraph type).

#### Delete a non-cash gift response paragraph

```
DEFINITION
DELETE http://apiserver/noncashgifts/:id/response/paragraphs/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/noncashgifts/23832813/response/paragraphs/53774", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a non-cash gift response paragraph. It cannot be undone.

##### Arguments

* id (required) - The id of the non-cash gift response paragraph to be deleted.

##### Returns

Returns a 204 No Content response on success. If the non-cash gift response paragraph id does not exist, this call returns an error.

#### List all non-cash gift response paragraphs

```
DEFINITION
GET http://apiserver/noncashgifts/:id/response/paragraphs

EXAMPLE REQUEST
$.get("http://localhost:49195/noncashgifts/23832813/response/paragraphs");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "53774",
            "type": "PR1",
            "completionText": "Thank you for your gift."
        },
        {...},
        {...}
    ]
}

```

Returns a list of all non-cash gift response paragraphs.

### PCIPal

#### Get PCIPal Configuration

```
DEFINITION
GET http://apiserver/pcipal/configurations?companyCode=:companyCode&paymentGatewayCode=:paymentGatewayCode

EXAMPLE REQUEST
$.get("http://localhost:49195/pcipal/configurations?companyCode=1&paymentGatewayCode=BLUE");

EXAMPLE RESPONSE
{
    "companyCode": "1",
    "paymentGatewayCode": "BLUE",
    "flowId": "1111",
    "grantType": "client_credentials",
    "isActive": true,
    "platform": "pcipal.com",
    "region": "usa1",
    "tenantId": "1234",
    "tenantName": "Tenant2"
}

```

Retrieves the PCIPal configuration without returning sensative data such as API keys or Client Secret keys.

##### Arguments

* companyCode (required) - The company being used that has PCI Pal enabled.
* paymentGatewayCode (required) - The company payment gateway code being used that has PCI Pal enabled.

##### Returns

Returns a PCI Pal configuration object.

#### Get PCIPal Session Data

```
DEFINITION
GET http://apiserver/pcipal/sessions/:sessionId?companyCode=:companyCode&paymentGatewayCode=:paymentGatewayCode

EXAMPLE REQUEST
$.get("http://localhost:49195/pcipal/sessions/99bb27c1-cf85-4077-8914-7c5525578fec?companyCode=1&paymentGatewayCode=BLUE");

EXAMPLE RESPONSE
{
    "sessionId": "99bb27c1-cf85-4077-8914-7c5525578fec",
    "linkId": "8282",
    "accessToken": null,
    "refreshToken": null,
    "isSuccessful": true,
    "errorMessage": null,
    "isSessionComplete": true,
    "transactionId": "000000921801",
    "referenceNumber": "MASTERCARD-5454 07/2025 Thomas Anderson",
    "expirationMonth": "07",
    "expirationYear": "2025",
    "nameOnCard": "Thomas Anderson",
    "cardType": "MASTERCARD",
    "last4Digits": "5454"
}

```

Retrieves the PCIPal session data. You need only supply the session Id.

##### Arguments

* sessionId (required) - The PCIPal session Id.
* companyCode (required) - The company being used that has PCI Pal enabled.
* paymentGatewayCode (required) - The company payment gateway code being used that has PCI Pal enabled.

##### Returns

Returns a session data object if a valid id was provided.

#### Start PCIPal Session

```
DEFINITION
POST http://apiserver/pcipal/sessions

EXAMPLE REQUEST
$.post("http://localhost:49195/pcipal/sessions", {
    "companyCode": "1",
    "paymentGatewayCode": "BLUE",
    "transactionAmount": "11.55",
    "firstName": "Thomas",
    "lastName": "Anderson",
    "streetAddress1": "1234 Main St.",
    "city": "Dallas",
    "state": "TX",
    "zip": "75080",
    "phone": "214-222-3333"
});

EXAMPLE RESPONSE
{
    "sessionId": "99bb27c1-cf85-4077-8914-7c5525578fec",
    "linkId": "8282",
    "accessToken": "xxxxxxx",
    "refreshToken": "xxxxxxx",
    "isSuccessful": null,
    "errorMessage": null,
    "isSessionComplete": null,
    "transactionId": null,
    "referenceNumber": null,
    "expirationMonth": null,
    "expirationYear": null,
    "nameOnCard": null,
    "cardType": null,
    "last4Digits": null
}

```

Starts a new PCIPal session using the data provided.

##### Arguments

* companyCode (required) - The company being used that has PCI Pal enabled.
* paymentGatewayCode (required) - The company payment gateway code being used that has PCI Pal enabled.
* transactionAmount (required) - Transaction payment amount.
* firstName (required) - First name on the account.
* lastName (required) - Last name on the account.
* streetAddress1 (optional) - Address line 1 on the account.
* city (optional) - Address city on the account.
* state (optional) - Address state on the account (Two letter state code).
* zip (optional) - Address zip code on the account.
* phone (optional) - Phone number on the account.

##### Returns

Returns PCIPal session object which contains information needed by the PCIPal modal.

### Queues

#### Retrieve a queue

```
DEFINITION
GET http://apiserver/queues/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/queues/1000000070");

EXAMPLE RESPONSE
{
    "id": "1000000070",
    "description": "Welcome call backs",
    "type": "ACCOUNT",
    "category": null,
    "processingType": "PHONE",
    "status": "Y",
    "assignee": "Bob",
    "batchType": null,
    "batchId": "6556",
    "scriptId": null,
    "instructionId": null
}

```

Retrieves the details of an existing queue. You need only supply the queue id.

##### Arguments

* id (required) - The id of the queue to retrieve.

##### Returns

Returns a queue object if a valid id was provided.

#### List all queues

```
DEFINITION
GET http://apiserver/queues

EXAMPLE REQUEST
$.get("http://localhost:49195/queues?type=ACCOUNT");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "1000000070",
            "description": "Welcome call backs",
            "type": "ACCOUNT",
            "category": null,
            "processingType": "PHONE",
            "status": "Y",
            "assignee": "Bob",
            "batchType": null,
            "batchId": "6556",
            "scriptId": null,
            "instructionId": null
        },
        { ... },
        { ... },
    ]
}

```

Returns a list of all queues matching the provided filter criteria.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* type (required) - Filter list by exact match on queue type
* id () - Filter list by exact match on id
* status () - Filter list by partial match on status
* description () - Filter list by partial match on description
* assignee () - Filter list by partial match on the Assigned To user
* category () - Filter list by partial match on the category
* processingType () - Filter list by partial match on processingType

##### Returns

A dictionary with an items property that contains an array of up to limit queues, starting at index offset. Each entry in the array is a separate queue object. If no queues are available, the resulting array will be empty. This request should never return an error.

### Queue Items

#### Create a queue item

```
DEFINITION
POST http://apiserver:49195/queues/:id/items

EXAMPLE REQUEST
$.post("http://localhost:49195/queues/1000000075/items", {
    "description": "Update acct information",
    "actionCode": "LOOKUP",
    "accountId": "16444"
});

EXAMPLE RESPONSE
{
    "id": "30903",
    "queue": "1000000075",
    "description": "Update acct information",
    "account": "16444",
    "accountStatus": "A",
    "actionCode": "LOOKUP",
    "actionId": null,
    "status": "Y"
}

```

Creates a new queue item object.

##### Arguments

* description (optional) - The description of the queue item.
* account (optional) - The account Id for processing the queue item.
* actionCode (required) - The action to perform for processing the queue item.
* actionId (optional) - The ID of the action item to be used for processing the queue item.
* status (optional) - The status of the queue item.

##### Returns

Returns a queue item if the call succeeded. Returns an error if the create parameters are invalid (e.g. specifying an invalid action code).

#### Retrieve a queue item

```
DEFINITION
GET http://apiserver/queues/:id/items/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/queues/1000000075/items/30903");

EXAMPLE RESPONSE
{
    "id": "30903",
    "queue": "1000000075",
    "description": "Update acct information",
    "account": "16444",
    "accountName": "John Doe",
    "accountStatus": "A",
    "actionCode": "LOOKUP",
    "actionId": null,
    "status": "Y"
}

```

Retrieves the details of an existing queue item.

##### Returns

Returns a queue item object if a valid id was provided.

#### Update a queue item

```
DEFINITION
POST http://apiserver/queues/:id/items/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/queues/1000000075/items/30903", {
    "actionId": "456"
});

EXAMPLE RESPONSE
{
    "id": "30903",
    "queue": "1000000075",
    "description": "Update acct information",
    "account": "16444",
    "accountStatus": "A",
    "actionCode": "LOOKUP",
    "actionId": "456",
    "status": "Y"
}

```

Updates the specified queue item by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* description (optional) - The description of the queue item.
* account (optional) - The account Id for processing the queue item.
* actionCode (required) - The action to perform for processing the queue item.
* actionId (optional) - The ID of the action item to be used for processing the queue item.
* status (optional) - The status of the queue item.

##### Returns

Returns the queue item object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined action code).

#### Delete a queue item

```
DEFINITION
DELETE http://apiserver/queues/:id/items/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/queues/1000000075/items/30903", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes an account merge. This will unmerge the accounts.

##### Arguments

* id (required) - The id of the queue item to be deleted.

##### Returns

Returns a 204 No Content response on success. If the queue item id does not exist, this call returns an error.

#### List all queue items

```
DEFINITION
GET http://apiserver/queues/:id/items

EXAMPLE REQUEST
$.get("http://localhost:49195/queues/1000000075/items");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "id": "30903",
            "queue": "1000000075",
            "description": "Update acct information",
            "account": "16444",
            "accountStatus": "A",
            "actionCode": "LOOKUP",
            "actionId": "456",
            "status": "Y"
        },
        {...},
        {...}
    ]
}

```

### Quick Address Search

#### Get all available countries

```
DEFINITION
GET http://apiserver/QAS/countries

EXAMPLE REQUEST
$.get("http://localhost:49195/QAS/countries");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "value": "US",
            "description": "United States",
            "attributeValue": "USA"
        },
        {...}
    ]
}

```

Performs a fetch of all countries available to the QAS service.

##### Returns

A dictionary with an items property that contains an array of up to limit country definitions, starting at index offset. Each entry in the array is a separate country definition object. If no countries are available, the resulting array will be empty. This request should never return an error.

#### Perform an address search

```
DEFINITION
GET http://apiserver/QAS

EXAMPLE REQUEST
$.get("http://localhost:49195/QAS", {
    "criteria": "75075",
    "dataId": "USA",
    "engineType": "typeDown"
    "moniker": ""
});

EXAMPLE RESPONSE
{
    "moniker": "",
    "prompt": "Enter ZIP code, city name, county name or state code",
    "criteria": null,
    "pickList": [
        {
            "moniker": "USA|6e133428-a289-4a1c-a959-edb20b45e5b3|wTUSADwHfBwIAAABAAAAAAQAAAJC5DAAAAAAANzUwNzUA",
            "text": "75075, Plano, TX",
            "postCode": "",
            "partialAddress": "Plano TX 75075",
            "isFullAddress": false,
            "isInformation": false
        }
    ]
}

```

Performs a QAS lookup using the specified criteria

##### Arguments

* criteria (optional) - The criteria to be used for searching against the current 'moniker'.
* dataId (required) - The country definition to be used when performing a QAS search.
* engineType (required) - The engine type used by QAS to perform the lookup. Available options are ["typeDown", "singleLine"].
* moniker (optional) - The 'moniker' to be used as the context for the search. Each search result contains a moniker to use for successive searches.

##### Returns

A dictionary with a pickList property that contains an array of up to limit QAS results, starting at index offset. Each entry in the array is a separate result object. If no results are available, the resulting array will be empty. The object also returns a prompt, which is used as an indicator for what criteria to pass in for the next step in the search process. This request should never return an error.

#### Lookup a full address

```
DEFINITION
GET http://apiserver/QAS/address/:moniker

EXAMPLE REQUEST
$.get("http://localhost:49195/QAS/address/USA|ddb6499a-8c44-4f71-a6bd-7c6ad2868bea|dOUSADwHfBwECAQAHM_DPAAAAAAAAAAA-");

EXAMPLE RESPONSE
{
    "addressLines": [
        {
            "dataplusGroups": null,
            "isOverflow": false,
            "isTruncated": false,
            "label": "",
            "line": "200 Coit Rd",
            "lineType": "Address"
        },
        {
            "dataplusGroups": null,
            "isOverflow": false,
            "isTruncated": false,
            "label": "Secondary number",
            "line": "",
            "lineType": "Address"
        },
        {
            "dataplusGroups": null,
            "isOverflow": false,
            "isTruncated": false,
            "label": "City name",
            "line": "Plano",
            "lineType": "Address"
        },
        {
            "dataplusGroups": null,
            "isOverflow": false,
            "isTruncated": false,
            "label": "State code",
            "line": "TX",
            "lineType": "Address"
        },
        {
            "dataplusGroups": null,
            "isOverflow": false,
            "isTruncated": false,
            "label": "",
            "line": "75075-5707",
            "lineType": "Address"
        },
        {
            "dataplusGroups": null,
            "isOverflow": false,
            "isTruncated": false,
            "label": "Three character ISO country code",
            "line": "USA",
            "lineType": "Address"
        }
    ],
    "dpvStatus": "DPVNotConfigured",
    "isOverflow": false,
    "isTruncated": false,
    "length": 6
}

```

Returns a full address object.

##### Arguments

* moniker (required) - The 'moniker' for the address object indicated as a full address.

##### Returns

Returns a verified address object containing all lines of the address.

### StudioOnline Funnel Report

#### Retrieve a funnel report

```
DEFINITION
GET http://apiserver/studioonlinefunnelreport/:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinefunnelreport/19?layoutIds=1,52");

EXAMPLE RESPONSE
[
    {
        "LayoutId": 1,
        "Conversion Rate": "100%",
        "Conversion Amount": null,
        "# Visits": 5,
        "# Unique Visitors": 2,
        "# Converted": 2,
        "Average Conversion Amount": 25,
        "Average Amount per Visitor": 25,
        "Recurring Conversion Rate": "50%"
        "Recurring Conversion Amount":25,
        "# Recurring Converted": 1,
        "Average Recurring Conversion Amount": 25,
        "Average Recurring Amount Per Visitor": 12.5
        "Pages": [
            {
                "LayoutId": 1,
                "Page": "Page1",
                "# Visitors": 1,
                "# Continued": 2,
                "# Converted": 2,
                "# Recurring Converted": 1,
                "Exits": 1,
                "Continuation Rate": "0%",
                "Name": "Layout",
                "FunnelType": "Project",
                "IsLastPage": false
            },{
                "LayoutId": 1,
                "Page": "Page2",
                "# Visitors": 0,
                "# Continued": 2,
                "# Converted": 2,
                "# Recurring Converted": 1,
                "Exits": 0,
                "Continuation Rate": null,
                "Name": "ShoppingCart",
                "FunnelType": "Project",
                "IsLastPage": false
            }, {
                "LayoutId": 1,
                "Page": "Page3",
                "# Visitors": 0,
                "# Continued": 2,
                "# Converted": 2,
                "# Recurring Converted": 1,
                "Exits": null,
                "Continuation Rate": null,
                "Name": "Confirmation",
                "FunnelType": "Project",
                "IsLastPage": true
            },{
                "LayoutId": 1,
                "Page": "Page2",
                "# Visitors": 0,
                "# Continued": 2,
                "# Converted": 2,
                "# Recurring Converted": 1,
                "Exits": null,
                "Continuation Rate": null,
                "Name": "Confirmation",
                "FunnelType": "OnePageCheckout",
                "IsLastPage": true
            }
        ]
    },
    {...},
    {...}
]

```

Retrieves the funnel details for layouts. You need only supply the layout ids.

##### Arguments

* layoutIds (required) - Comma separated list of layout ids to get report for.
* startDate (optional) - The starting date of the report.
* endDate (optional) - The ending date of the report.

##### Returns

Returns an array of funnel reports for the layouts.

### StudioOnline Layout Report

#### Retrieve a layout report

```
DEFINITION
GET http://apiserver/studioonlinelayoutreport/:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinelayoutreport/19?layoutIds=1,52&groupings=BrowserType");

EXAMPLE RESPONSE
[
    {
        "LayoutId": 1,
        "BrowserType": "Chrome",
        "Page Visits": 1,
        "Conversions": 0,
        "Unique Visitors": 1,
        "Entrances": 1,
        "Bounce Rate": "100%",
        "Exit Rate": "100%",
        "Conversion Rate": "0%",
        "Conversion Amount": null,
        "Time On Page (s)": null
    },
    {...},
    {...}
]

```

Retrieves the layout report details for layouts requested. You need only supply the layout ids.

##### Arguments

* layoutIds (required) - Comma separated list of layout ids to get report for.
* groupings (optional) - Comma separated list of columns to group the data on. Must be valid column.
* startDate (optional) - The starting date of the report.
* endDate (optional) - The ending date of the report.

##### Returns

Returns an array of layout reports for the layouts requested.

### StudioOnline Search Weights

#### Get search weights

```
DEFINITION
GET http://apiserver/studioonlinesearchweights

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinesearchweights");

EXAMPLE RESPONSE
[
    {
        "type": "MISSINFO",
        "description": "Missionary serving this project",
        "category": "PROJECT",
        "userDefined": true,
        "exactMatch": 199,
        "wordMatch": 0,
        "partialMatch": 0
    },
    {...},
    {...}
]

```

Retrieves the search weights defined for StudioOnline.

##### Returns

Returns a list of all search weights currently defined. Each entry in the array is a separate search weight object. If no search weights are defined, the resulting array will be empty. This request should never return an error.

#### Set search weights

```
DEFINITION
POST http://apiserver/studioonlinesearchweights

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinesearchweights", {
    searchWeights: [
        {
            "type": "DATECODE",
            "userDefined": true,
            "exactMatch": 200,
            "wordMatch": 2,
            "partialMatch": 1
        },
        {...},
        {...}
    ]
});

```

Creates or updates a StudioOnline search weight object.

##### Arguments

* searchWeights (required) - The list of search weights to add or update.
* searchWeights.type (required) - The X02 value to set a search weight for. This value should be marked as SOSearch = 1.
* searchWeights.userDefined (optional) - Indicates whether the search weight is user defined. This should be true for all values not set by DDC.
* searchWeights.exactMatch (optional) - The weight to apply to exact matches. Default is 0, should be between 0 and 10000 (inclusive).
* searchWeights.wordMatch (optional) - The weight to apply to word matches. Default is 0, should be between 0 and 10000 (inclusive).
* searchWeights.partialMatch (optional) - The weight to apply to partial matches. Default is 0, should be between 0 and 10000 (inclusive).

##### Returns

Returns a 200 OK response on success.

### StudioOnline Sessions

#### Create a session

```
DEFINITION
POST http://apiserver/studioonlinesessions

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinesessions", {
    "store": "19",
    "id": "6bba6645-ee26-481e-a2ad-a94ac6486018",
    "userAgent": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36",
    "browserSize": "desktop",
    "pageType": "Layout",
    "layoutId": "1",
    "url": "http://localhost:49196/donate/alderaan-disaster-relief",
    "actionDate": "2017-03-07 10:19:47.2245528"
});

```

Creates a new StudioOnline session object.

##### Arguments

* store (required) - The StudioOnline store Id for which to create the session.
* id (required) - The session id.
* userId (optional) - The unique id for the user.
* accountNumber (optional) - The users SE account number.
* userAgent (optional) - The user agent from the users browser.
* browserSize (optional) - The browser size, this should be mobile, tablet, desktop, or largeDesktop.
* pageType (optional) - The funnel page type, see R08\_FunnelPages.PageName.
* layoutId (optional) - The id of the layout visited.
* queryParameters (optional) - Additional query parameters to store for the user visit.
* referer (optional) - The referer to the page.
* url (optional) - The url of the page visited.
* actionDate (optional) - The date of the action.
* timeOnPage (optional) - The amount of time spent on the page. Generally not supplied on creating a session since it is calculated on leaving.
* exited (optional) - Indicates whether the user exited on this page. Generally not supplied on creating a session.
* cartItems (optional) - Items in cart to track the item through a funnel.

##### Returns

Returns a 200 OK response on success.

#### Retrieve a StudioOnline session object (R09)

```
DEFINITION
GET http://apiserver/studioonlinesessions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinesessions/6bba6645-ee26-481e-a2ad-a94ac6486018");

EXAMPLE RESPONSE
{
    "id": "6bba6645-ee26-481e-a2ad-a94ac6486018",
    "account": "30107",
    "isActive": true,
    "lastModifiedDate": "2017-09-28T09:07:14 AM"
}

```

Retrieves the session object that includes the Account number, if any, associated with the session.

##### Arguments

* id (optional) - The session id.

##### Returns

Returns the session object that includes the Account number, if any.

#### Update a session

```
DEFINITION
POST http://apiserver/studioonlinesessions/:id?store=:storeId

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinesessions/6bba6645-ee26-481e-a2ad-a94ac6486018?store=19", {
    "browserSize": "largeDesktop",
    "timeOnPage": 55,
    "layoutId": 1
});

```

Updates the specified session by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* store (require) - The StudioOnline store id for which the session exists.
* userId (optional) - The unique id for the user.
* accountNumber (optional) - The users SE account number.
* userAgent (optional) - The user agent from the users browser.
* browserSize (optional) - The browser size, this should be mobile, tablet, desktop, or largeDesktop.
* pageType (optional) - The funnel page type, see R08\_FunnelPages.PageName.
* layoutId (optional) - The id of the layout visited. Required if updating previous page visit (timeOnPage/exited).
* queryParameters (optional) - Additional query parameters to store for the user visit.
* referer (optional) - The referer to the page.
* url (optional) - The url of the page visited.
* actionDate (optional) - The date of the action.
* timeOnPage (optional) - The amount of time spent on the page. Generally not supplied on creating a session since it is calculated on leaving.
* exited (optional) - Indicates whether the user exited on this page. Generally not supplied on creating a session.
* converted (optional) - Indicates whether the user converted from this page.
* convertedAmount (optional) - The monetary amount that was converted from this page.
* cartItems (optional) - Items in cart to track the item through a funnel.

##### Returns

Returns a 200 OK response on success.

### Checkout with current cart

```
DEFINITION
POST http://apiserver/studioonlinesessions/:id/checkout

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinesessions/6bba6645-ee26-481e-a2ad-a94ac6486018/checkout", {
    "store": "19",
    "account": "123456",
    "cartType": "CURRENT",
    "company": "10",
    "payment": {...}
});

EXAMPLE RESPONSE
{
    "cart": "5647"
}

```

Completes the `CURRENT` or `OPCO` (One Page Checkout) cart for the StudioOnline user using the payment information provided.

##### Arguments

* store (required) - The StudioOnline store Id for which to checkout.
* account (required) - The users SE account number.
* cartType (required) - The cart type to checkout, can either be the `CURRENT` or `OPCO` (one page checkout cart)
* company (required) - The company to use for automatic batch.
* payment (required) - A payment object to be created as part of the transaction. See [transaction payment](#create-a-transaction-payment) for required fields.
* mediaOutlet (optional) - The media outlet id for the transaction.
* shippingMethod (optional) - The shipping method for the order on the transaction.
* source (optional) - The source for any transaction details.
* contactMethod (optional) - The contact method for the transaction.
* securePageType (optional) - The secure page type that originated the request.
* secureMatchingText (optional) - The criteria used when matching a secure project/pledge to a ProjectCode/Description or PledgeCode/Description.

##### Returns

Returns a 200 OK response on success. The cart that was completed will be returned.

### StudioOnline Failed Account Pledges

#### Retrieve a failed account pledge

```
DEFINITION
GET http://apiserver/studioonlinefailedaccountpledges/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinefailedaccountpledges/1172");

EXAMPLE RESPONSE
{
    "id": "1172",
    "pledge": "050098",
    "pledgeDescription": "Mark McLemore Outreach 2012",
    "type": "PROJECT",
    "currency": "USD",
    "totalAmount": 2004,
    "amountPerGift": 501,
    "numberPledged": 4,
    "totalAmountDonated": 0,
    "totalNumberDonated": null,
    "totalRelatedAmountDonated": null,
    "frequency": "M",
    "frequencyDescription": "Monthly",
    "start": "2012-04-01",
    "end": "2013-04-01",
    "isOpenEnded": false,
    "source": "EV11CPCATL",
    "sourceDescription": "General Source Code",
    "elementGroup": "PC11C",
    "elementGroupDescription": "Pastor's Conference March 2011",
    "status": "N",
    "isActive": false,
    "cancelReason": null,
    "cancelDate": null,
    "numberOfAdjustmentMonths": null,
    "stmtAndAckAccount": null,
    "stmtAndAckAccountName": null,
    "infoAndUpdatesAccount": null,
    "infoAndUpdatesAccountName": null,
    "paidThroughDate": null,
    "originalPledge": null,
    "company": null,
    "account": "1483320",
    "accountName": "Henry Winkler",
    "defaultProjectCode": null,
    "response": null,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "hasRecurring": false
}

```

Retrieves the details of a failed account pledge. You need only supply the pledge id.

##### Arguments

* id (required) - The pledge id of the failed account pledge.

##### Returns

Returns information for a failed account pledge as an object if a pledge id was provided.

#### List all failed account pledges

```
DEFINITION
GET http://apiserver/studioonlinefailedaccountpledges

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinefailedaccountpledges");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 6
    },
    "items": [
        {
            "id": "1172",
            "pledge": "050098",
            "pledgeDescription": "Mark McLemore Outreach 2012",
            "type": "PROJECT",
            "currency": "USD",
            "totalAmount": 2004,
            "amountPerGift": 501,
            "numberPledged": 4,
            "totalAmountDonated": 0,
            "totalNumberDonated": null,
            "totalRelatedAmountDonated": null,
            "frequency": "M",
            "frequencyDescription": "Monthly",
            "start": "2012-04-01",
            "end": "2013-04-01",
            "isOpenEnded": false,
            "source": "EV11CPCATL",
            "sourceDescription": "General Source Code",
            "elementGroup": "PC11C",
            "elementGroupDescription": "Pastor's Conference March 2011",
            "status": "N",
            "isActive": false,
            "cancelReason": null,
            "cancelDate": null,
            "numberOfAdjustmentMonths": null,
            "stmtAndAckAccount": null,
            "stmtAndAckAccountName": null,
            "infoAndUpdatesAccount": null,
            "infoAndUpdatesAccountName": null,
            "paidThroughDate": null,
            "originalPledge": null,
            "company": null,
            "account": "1483320",
            "accountName": "Henry Winkler",
            "defaultProjectCode": null,
            "response": null,
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account pledges with status of "N" (Not Found Secure) and matching the provided filter criteria.

##### Arguments

* account (optional) - Filter list by exact match on account number.
* frequency (optional) - Filter list by partial match on frequency.
* amountPerGift (optional) - Filter list by exact match on amountPerGift.
* pledgeCode (optional) - Filter list by exact match on pledgeCode.
* startDateBegin (optional) - Filter list on startDate returning all failed account pledges with a start date on or after startDateBegin.
* startDateEnd (optional) - Filter list on startDate returning all failed account pledges with a start date on or before startDateEnd.

##### Returns

A dictionary with an items property that contains an array of up to limit failed account pledges, starting at index offset. Each entry in the array is a separate failed account pledge object. If no more failed account pledges are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Failed Transactions

#### Retrieve a failed transaction

```
DEFINITION
GET http://apiserver/studioonlinefailedtransactions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinefailedtransactions/718157");

EXAMPLE RESPONSE
{
    "id": "718157",
    "account": "42191",
    "batch": "11233",
    "date": "2017-10-05",
    "status": "H",
    "isTaxExempt": false,
    "mediaOutlet": null,
    "dma": "623",
    "currency": "USD",
    "contactMethod": "MAIL",
    "amount": 25,
    "amountDue": 0,
    "remainingAmountDue": 0,
    "deposit": "5657",
    "depositStatus": "C",
    "donationTotal": 25,
    "productTotal": 0,
    "shippingTotal": 0,
    "taxTotal": 0,
    "eventTotal": 0,
    "subscriptionTotal": 0,
    "arPaymentTotal": 0,
    "response": {
        "id": 1170695,
        "method": null,
        "type": "RECEIPT",
        "profileGroup": null,
        "printGroup": null,
        "printDate": null,
        "paragraphs": [],
        "letter": "",
        "isAutoAssigned": true,
        "completionText": "",
        "address": "1000041997",
        "inserts": null,
        "status": "Y"
    },
    "accountName": "John Doe",
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "receiptNumber": null,
    "autoCalculateShipping": true
}

```

Retrieves the details of a failed transaction. You need only supply the transaction id.

##### Arguments

* id (required) - The transaction id or document number to get information for.

##### Returns

Returns information for a failed transaction as an object if a transation id was provided.

#### List all failed transactions

```
DEFINITION
GET http://apiserver/studioonlinefailedtransactions

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinefailedtransactions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "718157",
            "account": "42191",
            "batch": "11233",
            "date": "2017-10-05",
            "status": "H",
            "isTaxExempt": false,
            "mediaOutlet": null,
            "dma": "623",
            "currency": "USD",
            "contactMethod": "MAIL",
            "amount": 25,
            "amountDue": 0,
            "remainingAmountDue": 0,
            "deposit": "5657",
            "depositStatus": "C",
            "donationTotal": 25,
            "productTotal": 0,
            "shippingTotal": 0,
            "taxTotal": 0,
            "eventTotal": 0,
            "subscriptionTotal": 0,
            "arPaymentTotal": 0,
            "response": {
                "id": 1170695,
                "method": null,
                "type": "RECEIPT",
                "profileGroup": null,
                "printGroup": null,
                "printDate": null,
                "paragraphs": [],
                "letter": "",
                "isAutoAssigned": true,
                "completionText": "",
                "address": "1000041997",
                "inserts": null,
                "status": "Y"
            },
            "accountName": "John Doe",
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null,
            "receiptNumber": null,
            "autoCalculateShipping": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all failed transaction matching the provided filter criteria.

##### Arguments

* id (optional) - Filter list by exact match on transaction id or document number.
* account (optional) - Filter list by exact match on account number.
* mode (optional) - Filter list by transaction type. Can be one of the following `DONATION`, `EVENT`, `ORDER`, or `SUBSCRIPT`. If the value is anything else, all transaction types will be returned.

##### Returns

A dictionary with an items property that contains an array of up to limit pins, starting at index offset. Each entry in the array is a separate pin information object. If no more pins are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Pins

#### Create a pin

```
DEFINITION
POST http://apiserver/studioonlinepins

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinepins", {
    "store": "19",
    "token": "6bba6645-ee26-481e-a2ad-a94ac6486018"
});

EXAMPLE RESPONSE
{
    "pin": "N423"
}

```

Creates a new StudioOnline pin object or returns the existing pin.

##### Arguments

* store (required) - The StudioOnline store Id for which to create the pin.
* token (required) - The token id for the current user. Must be a valid R09\_TokenMaster Token.

##### Returns

Returns a pin for a quick lookup of the StudioOnline users information.

#### Retrieve a pin

```
DEFINITION
GET http://apiserver/studioonlinepins/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinepins/N423");

EXAMPLE RESPONSE
{
    "id": "N423",
    "accountNumber": null,
    "accountName": null,
    "lastModifiedDate": "2017-02-16",
    "store": "19",
    "storeDescription": "StudioOnline Store"
}

```

Retrieves the details of an pin. You need only supply the StudioOnline pin.

##### Arguments

* id (required) - The pin to get information for.

##### Returns

Returns information for a pin as an object if a valid pin was provided.

#### Link a pin

```
DEFINITION
POST http://apiserver/studioonlinepins/:id/link

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinepins/N423/link", {
    "accountNumber": 123456
});

EXAMPLE RESPONSE
204 No Content

```

Updates the specified pin by linking it to an account.

##### Returns

Returns 204 No Content.

#### List all pins

```
DEFINITION
GET http://apiserver/studioonlinepins

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinepins");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "N423",
            "accountNumber": null,
            "accountName": null,
            "lastModifiedDate": "2017-02-16",
            "store": "19",
            "storeDescription": "StudioOnline Store"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all pins matching the provided filter criteria.

##### Arguments

* pin (optional) - Filter list by exact match on pin.
* accountNumber (optional) - Filter list by exact match on account number.
* lastActivityStartDate (optional) - Filter list by last modified date greater than lastActivityStartDate.
* lastActivityEndDate (optional) - Filter list by last modified date less than lastActivityEndDate.

##### Returns

A dictionary with an items property that contains an array of up to limit pins, starting at index offset. Each entry in the array is a separate pin information object. If no more pins are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Carts

#### Retrieve a cart

```
DEFINITION
GET http://apiserver/studioonlinecarts/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts/25445");

EXAMPLE RESPONSE
{
    "id": "25445",
    "cartType": "COMPLETED",
    "cartTypeDescription": "Completed",
    "lastModifiedDate": "2016-05-13",
    "completedDate": "2016-05-13",
    "t01RecordId": 469686,
    "store": "19",
    "storeDescription": "StudioOnline Store"
}

```

Retrieves the details of an existing cart. You need only supply the cart id.

##### Arguments

* id (required) - The id of the cart to retrieve.

##### Returns

Returns a cart object if a valid id was provided.

#### Merge a cart

```
DEFINITION
POST http://apiserver/studioonlinecarts/:id/merge

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinecarts/25445/merge", {
    "cartType": "SFL"
});

EXAMPLE RESPONSE
204 No Content

```

Updates the specified cart by changing the cart type or merging into another cart type.

##### Arguments

* cartType (required) - Cart type to move to. Must be a valid SOCARTTYPE.

##### Returns

Returns 204 No Content.

#### Delete a cart

```
DEFINITION
DELETE http://apiserver/studioonlinecarts/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlinecarts/25445", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cart. It cannot be undone.

##### Arguments

* id (required) - The record id of the cart to be deleted.

##### Returns

Returns a 204 No Content response on success. If the cart does not exist, this call returns an error.

#### List all carts

```
DEFINITION
GET http://apiserver/studioonlinecarts

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "3",
            "cartType": "COMPLETED",
            "cartTypeDescription": "Completed",
            "lastModifiedDate": "2016-05-13",
            "completedDate": "2016-05-13",
            "t01RecordId": 469686,
            "store": "19",
            "storeDescription": "StudioOnline Store"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all carts matching the provided filter criteria.

##### Arguments

* pin (optional) - Filter list by exact match on pin.
* accountNumber (optional) - Filter list by exact match on account number.
* cartType (optional) - Filter list by exact match on cart type

##### Returns

A dictionary with an items property that contains an array of up to limit carts, starting at index offset. Each entry in the array is a separate cart object. If no more carts are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Cart Donations

#### Move a cart donation

```
DEFINITION
POST http://apiserver/studioonlinecarts/:cartId/donations/:donationId/move

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinecarts/25445/donations/1/move", {
    "cartType": "SFL"
});

EXAMPLE RESPONSE
204 No Content

```

Updates the specified cart donation by moving it to the cart type specified, creating a new cart if necessary.

##### Arguments

* cartType (required) - Cart type to move to. Must be a valid SOCARTTYPE.

##### Returns

Returns 204 No Content.

#### Delete a cart donation

```
DEFINITION
DELETE http://apiserver/studioonlinecarts/:cartId/donations/:donationId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlinecarts/25445/donations/284", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cart donation. It cannot be undone. Will also delete the cart if empty.

##### Arguments

* cartId (required) - The record id of the cart to delete a donation from.
* donationId (required) - The record id of the donation to be deleted.

##### Returns

Returns a 204 No Content response on success. If the donation does not exist, this call returns an error.

#### List all cart donations

```
DEFINITION
GET http://apiserver/studioonlinecarts/:cartId/donations

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts/25445/donations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "25445",
            "project": "501110",
            "projectDescription": "SO Project",
            "amount": 75,
            "source": "PH8002013",
            "sourceDescription": "800 Phone Line - 2013",
            "subaccount": null,
            "subaccountDescription": null,
            "anonymous": false,
            "deductible": true,
            "relatedAccount": null,
            "relatedAccountName": null,
            "pledgeId": null,
            "pledge": null,
            "pledgeDescription": null,
            "shortComment": "Stuff",
            "isRecurring": true,
            "customerChoseChargeToday": true,
            "frequency": "A",
            "useOnDay": 1,
            "t04RecordId": null,
            "t17RecordId": null,
            "premium": null,
            "premiumDescription": null,
            "allowSEDetailLookup": false,
            "isEditableInCart": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all cart donations for the cart specified.

##### Arguments

* cartId (required) - Record Id of the cart to get donations for.

##### Returns

A dictionary with an items property that contains an array of up to limit cart donations, starting at index offset. Each entry in the array is a separate donation object. If no more donations are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Cart Event Attendees

#### List all cart event attendees

```
DEFINITION
GET http://apiserver/studioonlinecarts/:cartId/eventAttendees

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts/25445/eventAttendees");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "1",
            "addressId": null,
            "attendeeAccountNumber": 43703,
            "formattedName": "Nathan Johnson"
            "isMe": true,
            "eventCode": "10ALT1",
            "eventDescription": "Atlanta, GA - September 1st 2018",
            "groupId": 17
            "groupCode": "501",
            "groupDescription": "Five-oh-first",
            "priceCode": "P",
            "priceDescription": "Promotional",
            "price": 0,
            "discountAmount": 0,
            "sourceCode": null,
            "sourceCodeDescription": null,
            "shortComment": "No comment...",
            "quantity": 1,
            "coupleId": null,
            "t05EventAttendeeDetailsId": null
        },
        {...},
        {...}
    ]

}

```

Returns a list of all cart event attendees for the cart specified.

##### Arguments

* cartId (required) - Record Id of the cart to get event attendees for.

##### Returns

A dictionary with an items property that contains an array of up to limit cart event attendee, starting at index offset. Each entry in the array is a separate event attendee object. If no more event attendees are available, the resulting array will be empty. This request should never return an error.

#### Delete a cart event attendee

```
DEFINITION
DELETE http://apiserver/studioonlinecarts/:cartId/eventAttendees/:eventAttendeeId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlinecarts/25445/eventAttendees/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cart event attendee. It cannot be undone.

##### Arguments

* cartId (required) - The record id of the cart to delete an event attendee from.
* eventAttendeeId (required) - The record id of the event attendee to delete.

##### Returns

Returns a 204 No Content response on success. If the event attendee does not exist, this call returns an error.

#### Move a cart event attendee

```
DEFINITION
POST http://apiserver/studioonlinecarts/:cartId/eventAttendees/:eventAttendeeId/move

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinecarts/25445/eventAttendees/1/move", {
    "cartType": "SFL"
});

EXAMPLE RESPONSE
204 No Content

```

Updates the specified cart event attendee by moving it to the cart type specified, creating a new cart if necessary.

##### Arguments

* cartType (required) - Cart type to move to. Must be a valid SOCARTTYPE.

##### Returns

Returns 204 No Content.

### StudioOnline Cart Event Attendee Sessions

#### List all cart event attendee sessions

```
DEFINITION
GET http://apiserver/studioonlinecarts/:cartId/eventAttendees/:eventAttendeeId/sessions

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts/25445/eventAttendees/1/sessions")

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 1
    },
    "items": [
        {
            "id": "1",
            "sessionCode": "S104",
            "sessionDescription": "What Every Marriage Needs",
            "priceCode": "P",
            "priceDescription": "Promotional",
            "price": 0,
            "shortComment": "No comment",
            "quantity": 1,
            "t06AttendeeSessionDetailsId": null
        },
        {...},
        {...}
    ]
}

Returns a list of all cart event attendee sessions for the event attendee specified.

```

##### Arguments

* shoppingCartId (required) - Record Id of the shopping cart to get attendee sessions for.
* eventAttendeeId (required) - Record Id of the event attendee to get attendee sessions for.

##### Returns

A dictionary with an items property that contains an array of up to limit cart event attendee sessions, starting at index offset. Each entry in the array is a separate event attendee session object. If no more event attendee sessions are available, the resulting array will be empty. This request should never return an error.

#### Delete a cart event attendee session

```
DEFINITION
DELETE http://apiserver/studioonlinecarts/:cartId/eventAttendees/:eventAttendeeId/sessions/:sessionId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlinecarts/25445/eventAttendees/1/sessions/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cart event attendee session. It cannot be undone.

##### Arguments

* cartId (required) - The record id of the cart to delete an event attendee from.
* eventAttendeeId (required) - The record id of the event attendee to delete an attendee session from.
* sessionId (required) - The record id of the attendee session to delete.

##### Returns

Returns a 204 No Content response on success. If the attendee session does not exist, this call returns an error.

### StudioOnline Cart Orders

#### List all cart orders

```
DEFINITION
GET http://apiserver/studioonlinecarts/:cartId/orders

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts/25445/orders");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "1",
            "recipientAccountNumber": 30134,
            "addressId": 1000039001,
            "warehouse": "10",
            "warehouseDescription": "Warehouse 10",
            "shipMethod": "FEDEX",
            "t02RecordId": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all cart orders for the cart specified.

##### Arguments

* cartId (required) - Record Id of the cart to get orders for.

##### Returns

A dictionary with an items property that contains an array of up to limit cart orders, starting at index offset. Each entry in the array is a separate order object. If no more orders are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Cart Order Details

#### Move a cart order detail

```
DEFINITION
POST http://apiserver/studioonlinecarts/:cartId/orders/:orderId/details/:detailId/move

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinecarts/25445/orders/1/details/1/move", {
    "cartType": "SFL"
});

EXAMPLE RESPONSE
204 No Content

```

Updates the specified cart order detail by moving it to the cart type specified, creating a new cart and order if necessary.

##### Arguments

* cartType (required) - Cart type to move to. Must be a valid SOCARTTYPE.

##### Returns

Returns 204 No Content.

#### Delete a cart order detail

```
DEFINITION
DELETE http://apiserver/studioonlinecarts/:cartId/orders/:orderId/details/:detailId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlinecarts/25445/orders/1/details/1", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cart order detail. It cannot be undone. Will also delete the cart and order if empty.

##### Arguments

* cartId (required) - The record id of the cart to delete an order detail from.
* orderId (required) - The record id of the order to delete a detail from.
* donationId (required) - The record id of the detail to be deleted.

##### Returns

Returns a 204 No Content response on success. If the detail does not exist, this call returns an error.

#### List all cart order details

```
DEFINITION
GET http://apiserver/studioonlinecarts/:cartId/orders/:orderId/details

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts/25445/orders/1/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "1",
            "productCode": "BK1000",
            "productDescription": "So Long, Insecurity",
            "quantity": 2,
            "priceCode": "RP",
            "priceCodeDescription": "Retail Price",
            "price": 20,
            "extendedAmount": 37.99,
            "discountAmount": 2.01,
            "shortComment": null,
            "sourceCode": "0727111",
            "sourceDescription": null,
            "suggestedDonation": false,
            "t03RecordId": null,
            "isShippable": true
        },
        {...},
        {...}
    ]
}

```

Returns a list of all cart order details for the cart and order specified.

##### Arguments

* cartId (required) - Record Id of the cart to get order details for.
* orderId (required) - Record Id of the order to get details for.

##### Returns

A dictionary with an items property that contains an array of up to limit cart order details, starting at index offset. Each entry in the array is a separate order detail object. If no more order details are available, the resulting array will be empty. This request should never return an error.

### StudioOnline Cart Subscriptions

#### Move a cart subscription

```
DEFINITION
POST http://apiserver/studioonlinecarts/:cartId/subscriptions/:subscriptionId/move

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlinecarts/25445/subscriptions/1/move", {
    "cartType": "SFL"
});

EXAMPLE RESPONSE
204 No Content

```

Updates the specified cart subscription by moving it to the cart type specified, creating a new cart if necessary.

##### Arguments

* cartType (required) - Cart type to move to. Must be a valid SOCARTTYPE.

##### Returns

Returns 204 No Content.

#### Delete a cart subscription

```
DEFINITION
DELETE http://apiserver/studioonlinecarts/:cartId/subscriptions/:subscriptionId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlinecarts/25445/subscriptions/284", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a cart subscription. It cannot be undone. Will also delete the cart if empty.

##### Arguments

* cartId (required) - The record id of the cart to delete a subscription from.
* subscriptionId (required) - The record id of the subscription to be deleted.

##### Returns

Returns a 204 No Content response on success. If the subscription does not exist, this call returns an error.

#### List all cart subscriptions

```
DEFINITION
GET http://apiserver/studioonlinecarts/:cartId/subscriptions

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlinecarts/25445/subscriptions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "4",
            "subscriptionCode": "OMM",
            "subscriptionDescription": "One Month Membership",
            "recipientAccountNumber": 43703,
            "recipientAccountPrimaryAddressId": "1234",
            "formattedName": "Dr. Nathan Test Johnson",
            "isT01Account": false,
            "sourceCode": "0_A_B_M_N",
            "sourceDescription": "Zero",
            "startDate": "2019-08-06",
            "quantity": "1",
            "priceCode": "P",
            "priceCodeDescription": "Promotional (Free)",
            "price": 0,
            "discountAmount": 0,
            "totalAmount": 0,
            "autoRenew": false,
            "s01RecordId": null,
            "fulfillmentMethod": "TEST",
            "deliveryId": "1",
            "shortComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all cart subscriptions for the cart specified.

##### Arguments

* cartId (required) - Record Id of the cart to get subscriptions for.

##### Returns

A dictionary with an items property that contains an array of up to limit cart subscriptions, starting at index offset. Each entry in the array is a separate subscription object. If no more subscriptions are available, the resulting array will be empty. This request should never return an error.

### StudioOnline User Carts

#### Retrieve a cart

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/carts/:cartType?store=:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/CURRENT?store=19");

EXAMPLE RESPONSE
{
    "cartType": "CURRENT",
    "userId": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "couponCode": null,
    "couponCodeMessage": null,
    "freeShippingMethod": null,
    "freeShippingMethodDescription": null,
    "lastMinuteDonationCalculation": null,
    "lastMinuteDonationAmount": null,
    "donations": [
        {
            "id": "328",
            "project": "PROJ002",
            "projectDescription": "Sponsor a Battalion",
            "amount": 999,
            "source": "MARC",
            "sourceDescription": "Marc's Source Code",
            "subaccount": null,
            "subaccountDescription": null,
            "anonymous": false,
            "deductible": false,
            "relatedAccount": null,
            "relatedAccountName": null,
            "pledgeId": null,
            "pledge": null,
            "pledgeDescription": null,
            "shortComment": null,
            "isRecurring": false,
            "customerChoseChargeToday": false,
            "frequency": "O",
            "useOnDay": null,
            "t04RecordId": null,
            "t17RecordId": null,
            "premium": null,
            "premiumDescription": null,
            "allowSEDetailLookup": false
        },
        {...},
        {...}
    ],
    "eventAttendees": [
        {
            "id": "234",
            "addressId": 1,
            "attendeeAccountNumber": 43703,
            "formattedName": "John Smith",
            "isMe": false,
            "eventCode": "10ALT1",
            "eventDescription": "Conference",
            "groupCode": null,
            "priceCode": "P",
            "priceCodeDescription": "Standard Price",
            "price": 100,
            "discountAmount": 0,
            "sourceCode": null,
            "sourceCodeDescription": null,
            "shortComment": "No comment...",
            "quantity": 1,
            "coupleId": null,
            "t05EventAttendeeDetailsId": null,
            "eventAttendeeSessions": [
                {
                    "id": "6545"
                    "sessionCode": "S104",
                    "priceCode": "P",
                    "priceCodeDescription": "Standard Session Price",
                    "price": 7,
                    "shortComment": "No comment",
                    "quantity": 1,
                    "t06AttendeeSessionDetailsId": null
                }
            ]
        }
    ],
    "subscriptions": [
        {
            "id": "123",
            "subscriptionCode": "OMM",
            "subscriptionDescription": "One Month Membership",
            "recipientAccountNumber": "43703",
            "formattedName": "Dr. Nathan Test Johnson",
            "isT01Account": true,
            "sourceCode": "0_A_B_M_N",
            "sourceDescription": "Zero",
            "startDate": "2019-08-20",
            "quantity": 1,
            "priceCode": "1YR",
            "priceCodeDescription": "One Year",
            "price": 130.1100,
            "discountAmount": 0.00,
            "totalAmount": 130.11,
            "autoRenew": false,
            "s01RecordId": null,
            "fulfillmentMethod": "EMAIL",
            "fulfillmentMethodDescription": "Email to Subscriber",
            "deliveryId": "1",
            "shortComment": "This is probably a comment of some kind."
        },
        {...}
    ]
}

```

Retrieves the details of an existing cart. You need only supply the user id and cart type.

##### Arguments

* store (required) - The StudioOnline store Id of the cart to retrieve.
* userId (required) - The unique id for the StudioOnline user.
* cartType (required) - The Type of the cart. Must be a valid SOCARTTYPE value.

##### Returns

Returns a cart object if a valid id and cart type was provided.

#### Add items to a cart

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/carts/:cartType

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/CURRENT", {
    "store": "19"
    "donations": [
        {
            "project": "PROJ001",
            "amount": 100,
            "frequency": "M",
            "isRecurring": true,
            "anonymous": false,
            "useOnDay": 15,
            "deductible": true
        }
    ],
    "eventAttendees": [
        {
            "addressId": "1",
            "attendeeAccountNumber": "43703",
            "isMe": true,
            "eventCode": "10ALT1",
            "groupCode": null,
            "priceCode": "P",
            "price": 0,
            "discountAmount": 0,
            "sourceCode": null,
            "shortComment": "No comment...",
            "quantity": 1,
            "coupleId": null,
            "t05EventAttendeeDetailsId": null
            "eventAttendeeSessions": [
                {
                    "sessionCode": "S104",
                    "priceCode": "P",
                    "price": 0,
                    "shortComment": "No comment",
                    "quantity": 1,
                    "t06AttendeeSessionDetailsId": null
                }
            ],
            "newAttendeeAccount": null
        }
    ],
    "subscriptions": [
        {
            "autoRenew": true,
            "deliveryId": "54787",
            "fulfillmentMethod": "MAIL",
            "isT01Account": true,
            "newRecipientAccount": null,
            "otherAddressId": "12345",
            "otherEmailId": null,
            "priceCode": "1YR",
            "price": 12.00,
            "quantity": 1,
            "recipientAccountNumber": "43703",
            "shortComment": null,
            "sourceCode": null,
            "startDate": "2020-05-05",
            "subscriptionCode": "SUB1",
        }
    ]
});

EXAMPLE RESPONSE
200 OK

```

Adds items to a shopping cart.

##### Arguments

* store (required) - The StudioOnline store Id of the cart for which to add this iten.
* userId (required) - The unique id for the StudioOnline user.
* cartType (required) - The Type of the cart. Must be a valid SOCARTTYPE value.
* lastMinuteDonationCalculation (optional) - The donation upsell calculation type; must be either `static` or `percentage`.
* lastMinuteDonationAmount (optional) - The donation upsell calculation amount.
* donations.project (required) - The project code for the donation.
* donations.amount (required) - The amount of the donation.
* donations.source (required) - The source code of the donation.
* donations.subaccount (optional) - The subaccount for the donation.
* donations.anonymous (optional) - Indicates whether the donation is anonymous.
* donations.deductible (optional) - Indicates whether the donation is deductible.
* donations.relatedAccount (optional) - The related account for the donation.
* donations.pledge (optional) - The pledge id for the donation.
* donations.shortComment (optional) - The short comment for the donation.
* donations.isRecurring (optional) - Indicates whether the donation is recurring, should be true if frequency is set.
* donations.customerChoseChargeToday (optional) - Indicates whether the user chose to be charged today, for cases such as when the use on day is already passed for a monthly donation.
* donations.frequency (optional) - The frequency of the donation.
* donations.useOnDay (optional) - The use on day for the donation.
* donations.premium (optional) - The ProductCode of the donation premium.
* donations.allowSEDetailLoopup (optional) - Whether the details of this donation and/or pledge can be retrieved from StudioEnterprise (SE) if not published to StudioOnline [`true`/`false`].
* eventAttendees.addressId (optional) - Attendee address id.
* eventAttendees.attendeeAccountNumber (optional) - Account number of the attendee.
* eventAttendees.isMe (optional) - Boolean value that indicates whether or not this event registration is for the registering account.
* eventAttendees.eventCode (optional) - Code for the event.
* eventAttendees.groupCode (optional) - Registration group code. If this is not null, the price code will be overridden by the group price.
* eventAttendees.priceCode (optional) - Price code for the event.
* eventAttendees.price (optional) - Event price.
* eventAttendees.discountAmount (optional) - Amount that the price is being discounted.
* eventAttendees.sourceCode (optional) - Event source code.
* eventAttendees.shortComment (optional) - Short comment for the event.
* eventAttendees.quantity (optional) - Number of event registrations purchased for this registration.
* eventAttendees.coupleId (optional) - Couple registration records are tied together. This contains the recordId of the corresponding couple record.
* eventAttendees.t05EventAttendeeDetailsId (optional) - Record id of the corresponding T05 record.
* eventAttendees.newAttendeeAccount (optional) - The account data of the account you would like to create or update. This would be in the same format as if you were using the create account resource.
* eventAttendees.eventAttendeeSessions.sessionCode (optional) - Code for the session.
* eventAttendees.eventAttendeeSessions.priceCode (optional) - Price code for the session.
* eventAttendees.eventAttendeeSessions.price (optional) - Session price.
* eventAttendees.eventAttendeeSessions.shortComment (optional) - Short comment for the session.
* eventAttendees.eventAttendeeSessions.quantity (optional) - Number of session registrations purchased for this registration.
* eventAttendees.eventAttendeeSessions.t06AttendeeSessionDetailsId (optional) - Record id of the corresponding T06 record.
* subscriptions.autoRenew (optional) - Boolean value that indicates whether or not this subscription should be auto renewed.
* subscriptions.deliveryId (optional) - Either the address id (A03) or email id (A07) where the subscription should be delivered, depending on the fulfillment method.
* subscriptions.fulfillmentMethod (optional) - Whether the subscription is `MAIL` or `EMAIL` fulfillment.
* subscriptions.isT01Account (optional) - Boolean value that indicates whether or not this subscription is for the purchasing account.
* subscriptions.newRecipientAccount (optional) - The account data of the account you would like to create or update. This would be in the same format as if you were using the create account resource.
* subscriptions.organizationPrimaryContactAccountId (optional) - The primary contact id of the organization. If adding an organization with primary contact fields (title, firstName, middleName, lastName, suffix), this should be populated.
* subscriptions.organizationPrimaryContactTypeCodeType (optional) - The contact type of the primary contact of the organization. If this is not set, the primary contact for an organization will not be updated or added, even if primary contact fields are populated.
* subscriptions.organizationTypeCodeType (optional) - The organization type code type. If this is not set, the organization type code for an organization will not be updated or added, even if it is populated.
* subscriptions.organizationTypeCodeValue (optional) - The organization type code value. Must be a value of the subscriptions.organizationTypeCodeValue code type.
* subscriptions.otherAddressId (optional) - The address id if an address other than the primary should be used for MAIL fulfillment.
* subscriptions.otherEmailId (optional) - The email id if an email other than the primary should be used for EMAIL fulfillment.
* subscriptions.priceCode (optional) - Price code of the subscription.
* subscriptions.price (optional) - Price of the subscription.
* subscriptions.quantity (optional) - Quantity of the subscription.
* subscriptions.recipientAccountNumber (optional) - Account number of the recipient.
* subscriptions.shortcomment (optional) - Short comment for the subscription.
* subscriptions.sourceCode (optional) - Source code for the subscription.
* subscriptions.startDate (optional) - The date the subscription should start.
* subscriptions.subscriptionCode (optional) - Code for the subscription.

##### Returns

Returns a 200 OK if items were successfully added to the cart. Returns an error if create parameters are invalid (e.g. specifying an undefined currency code or failing to specify a batch).

#### Remove items from a cart

```
DEFINITION
DELETE http://apiserver/studioonlineusers/:userId/carts/:cartType

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/CURRENT", {
    type: "DELETE",
    data: {
        "donations": [ 329, 328 ]
    }
});

EXAMPLE RESPONSE
204 No Content

```

Permanently removes items from a cart. It cannot be undone.

##### Arguments

* userId (required) - The unique id for the StudioOnline user.
* cartType (required) - The Type of the cart. Must be a valid SOCARTTYPE value.
* donations (optional) - Array of donation ids to be removed from cart. (At least one donation or one eventAttendee or one product is required.)
* eventAttendees (optional) - Array of eventAttendee ids to be removed from the cart. (At least one donation or one eventAttendee or one product is required.)
* products (optional) - Array of order detail ids to be removed from cart. (At least one donation or one eventAttendee or one product is required.)

##### Returns

Returns a 204 No Content response on success. Returns an error message if any exceptions occured while applying the coupon to the cart.

#### Apply a coupon to a cart

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/carts/:cartType/applycoupon

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/CURRENT/applyCoupon", {
    "store": "19",
    "couponCode": "30OFF"
});

EXAMPLE RESPONSE
204 No Content

```

Applies a coupon to the designated cart for the provided user id. NOTE: We currently only support one coupon applied per cart. Any additional applications will overwrite the previous application.

##### Arguments

* store (require) - The StudioOnline store Id for which to apply the coupon.
* userId (required) - The unique id for the StudioOnline user.
* cartType (required) - The Type of the cart. Must be a valid SOCARTTYPE value.
* couponCode (required) - The coupon code to use when applying the discount.
* country (optional) - If you're not an identified user based on your userId, the country code of the country you're purchasing from.
* postalCode (optional) - If you're not an identified user based on your userId, the postal or zip code you're purchasing from.

##### Returns

Returns a 204 No Content response on success.

#### Apply a coupon to a one page checkout

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/applyonepagecoupon

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/applyonepagecoupon", {
    "cart": {
        "account": {
            "firstName": "John",
            "lastName": "Smith",
            "address": {
                "line1": "123 Main St.",
                "city": "Plano",
                "state": "TX",
                "postalCode": "75075",
                "country": "USA"
            },
            "type": "I"
        },
        "contactMethod": "WEB",
        "shippingMethod": null,
        "tangibleCode": "100BKLET",
        "cartItems": {
            "products": [
                {
                    "product": "100BKLET",
                    "isShippable": true,
                    "quantity": 1,
                    "suggestedDonationUserProvided": null,
                    "suggestedDonation": null,
                    "warehouse": "30"
                }
            ]
        },
        "tangibleType": "Product"
    },
    "couponCode": "DISCBKLET"
});

EXAMPLE RESPONSE
{
    "discountAmount": "0.23"
}

```

Applies a coupon to the current one page checkout cart data and returns the discount amount for the product in that cart. NOTE: We currently only support one coupon applied per cart. Any additional applications will overwrite the previous application.

##### Arguments

* cart (required) - The current cart representation. This is the same data that is passed to the Add To Cart logic for products.
* couponCode (required) - The coupon code to use when applying the discount.

##### Returns

Returns a calculated discount amount if successful, or nothing if the coupon code was not able to be applied.

#### Move items into cart

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/carts/:cartType/moveinto

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/SFL", {
    type: "POST",
    data: {
        "donations": [ 329, 328 ]
    }
});

EXAMPLE RESPONSE
204 No Content

```

Moves the items into the specified cart.

##### Arguments

* userId (required) - The unique id for the StudioOnline user.
* cartType (required) - The Type of the cart. Must be a valid SOCARTTYPE value.
* donations (optional) - Array of donation ids to be removed from cart. (At least one donation or one eventAttendee or one product is required.)
* eventAttendees (optional) - Array of eventAttendee ids to be removed from the cart. (At least one donation or one eventAttendee or one product is required.)
* products (optional) - Array of order detail ids to be removed from cart. (At least one donation or one eventAttendee or one product is required.)

##### Returns

Returns a 204 No Content response on success. Returns an error message if any exceptions occured while moving the item.

#### Transfers a cart to a different StudioOnline User

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/carts/:cartType/transfer

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/CURRENT/transfer", {
    "store": "19",
    "destinationUserId": "52C57565-0085-49F7-8DCB-3B5AB1BA2AB0"
});

EXAMPLE RESPONSE
204 No Content

```

Transfers the specified cart for the provided user id to the StudioOnline user of the destinationUserId.

##### Arguments

* store (require) - The StudioOnline store Id for which the cart should be transferred.
* destinationUserId (required) - The unique id for the StudioOnline user to which the cart is transferred.
* userId (required) - The unique id for the StudioOnline user from which the cart is transferred.
* cartType (required) - The Type of the cart to transfer. Must be a valid SOCARTTYPE value, and cannot be COMPLETED

##### Returns

Returns a 204 No Content response on success.

#### Update Last-Minute Donation in a cart

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/carts/:cartType/donationupsell

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/CURRENT/donationupsell", {
    "store": "19",
    "lastMinuteDonationCalculation": "percentage",
    "lastMinuteDonationAmount": "5"
});

EXAMPLE RESPONSE
204 No Content

```

Updates the Last-Minute Donation Calculation and Amount values for the specified cart for the provided user id.

##### Arguments

* store (required) - The StudioOnline store Id.
* userId (required) - The unique id for the StudioOnline user.
* cartType (required) - The Type of the cart on which to update the Last-Minute Donation. Valid values: `CURRENT` and `OPCO`.
* lastMinuteDonationCalculation (optional) - Type of Last-Minute Donation calculation. Valid values: `none` (if Last-Minute Donation is declined by the user), `static`, `percentage`. If not provided, lastMinuteDonationCalculation will be cleared.
* lastMinuteDonationAmount (optional) - The static or percentage amount that should be used for calculating the Last-Minute Donation. If not provided, lastMinuteDonationAmount will be cleared.

##### Returns

Returns a 204 No Content response on success.

### StudioOnline User Cart Donations

#### Update a cart donation

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/carts/:cartType/donations/:id?store=:storeId

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/carts/CURRENT/donations/428?store=19", {
    "id": "428",
    "project": "10",
    "amount": 500,
    "source": "CHRIS_TEST",
    "subaccount": null,
    "anonymous": false,
    "deductible": true,
    "relatedAccount": null,
    "pledge": null,
    "shortComment": null,
    "isRecurring": false,
    "customerChoseChargeToday": false,
    "frequency": "O",
    "useOnDay": null,
    "t04RecordId": null,
    "t17RecordId": null,
    "premium": null,
    "premiumDescription": null,
    "allowSEDetailLookup": false
});

EXAMPLE RESPONSE
200 OK

```

Updates the specified cart donation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* store (required) - The StudioOnline store id for which to update the donation.
* id (required) - The id for the donation.
* project (required) - The project code for the donation.
* amount (required) - The amount for the donation.
* source (optional) - The source code for the donation.
* subaccount (optional) - The subaccount id for the donation.
* anonymous (optional) - Indicates whether the donation is anonymous.
* deductible (optional) - Indicates whether the donation is deductible.
* relatedAccount (optional) - The related account id for the donation.
* pledge (optional) - The pledge code for the donation.
* shortComment (optional) - The short comment for the donation.
* isRecurring (optional) - Indicates whether the donation is recurring.
* customerChoseChargeToday (optional) - Indicates whether the customer chose charge today (upsell) for the donation.
* frequency (optional) - The frequency for the donation. Should be a valid "DDCFREQNCY" value.
* useOnDay (optional) - The use on day for the donation. Should be a valid "DDCUSEDAY" value.
* t04RecordId (optional) - The t04RecordId for the donation. Used for transaction entry.
* t17RecordId (optional) - The t17RecordId for the donation. Used for transaction entry.
* premium (optional) - The ProductCode of the donation premium.
* allowSEDetailLoopup (optional) - Whether the details of this donation and/or pledge can be retrieved from StudioEnterprise (SE) if not published to StudioOnline [`true`/`false`].

Note: any parameter not passed will be set to null or an error will occur if the parameter is required.

##### Returns

Returns 200 OK if the update succeeded. Returns an error if update parameters are invalid.

### StudioOnline User Pledges

#### Pledge Checkout

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/pledgecheckout

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/pledgecheckout", {
    "pledeCode": "WATERWELLS",
    "minutesUntilExpiration": 60
});

EXAMPLE RESPONSE
204 No Content

```

Checks out the pledge if it is not already checked out.

##### Arguments

* pledgeCode (required) - The pledge code to check out.
* minutesUntilExpiration (required) - The number of minutes until the pledge checkout expires and can be checked in. (Note: The expire checkout process needs to be run before the pledge is actually checked in.)

##### Returns

Returns 204 No Content if the pledge code was successfully checked out or was already in the StudioOnline users checkout group. A 400 Bad Request will be returned if the pledge could not be checked out, mostly likely because it was already checkout out.

#### Delete a StudioOnline user checkout group

```
DEFINITION
DELETE http://apiserver/studioonlineusers/:userId/pledgecheckout

EXAMPLE REQUEST
$.ajax("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/pledgecheckout", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a StudioOnline user's checkout group and any checkout details and checkout history for that checkout group. It cannot be undone.

##### Arguments

* userId (required) - The StudioOnline userId of the checkout group to be deleted.

##### Returns

Returns a 204 No Content response on success. If the userId does not exist, this call returns an error.

#### Retrieve a User Pledge

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/pledges?store=:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/pledges?store=19");

EXAMPLE RESPONSE
{
    "store": "19",
    "store": "StudioOnline Store"
    "token": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "pledeCode": "WATERWELLS",
    "pledgeFrequency": "M",
    "amountPerGift": 4.50
}

```

Retrieves the details of an existing user pledge. You need only supply the user id.

##### Arguments

* userId (required) - The id of the user whose pledge you would like to retrieve.
* store (required) - The store for which to get the pledge for the user

##### Returns

Returns a user pledge object if a valid id was provided.

#### Add a User Pledge

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/pledges

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/pledges", {
    "store": "19",
    "token": "01199F6A-F669-4AFB-BE78-87E4E8C1E4FF",
    "pledeCode": "WATERWELLS",
    "pledgeFrequency": "M",
    "amountPerGift": 4.50
});

EXAMPLE RESPONSE
204 No Content

```

Creates the user pledge.

##### Arguments

* store (required) - StoreId to which to add the pledge.
* token (required) - UserId of the Unidentified User.
* pledgeCode (required) - The Pledge Code.
* pledgeFrequency (required) - The Pledge Donation Frequency.
* amountPerGift (required) - The amount of each donation.

##### Returns

Returns 204 No Content.

### StudioOnline User Reports

#### Retrieve Report Parameter Defaults

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/reportparameterdefaults?store=:storeId&reportPath=:reportPath&reportTitle=:reportTitle

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/reportparameterdefaults?store=19&reportTitle=Donations");

EXAMPLE RESPONSE
[
    {
        "parameterName": "projectCode",
        "defaultValue": "1010010",
    },
    {
        "parameterName": "subaccount",
        "defaultValue": "1010"
    }
    {...},
    {...},
]

```

Retrieves report parameter defaults using the supplied user id and additional criteria.

##### Arguments

* userId (required) - The user ID for which to find report parameter defaults.
* store (optional) - The store for which to find report parameter defaults.
* reportPath (optional) - The report path for which to find report parameter defaults.
* reportTitle (optional) - The report title for which to find report parameter defaults.

##### Returns

Returns a list of report parameter default objects for the provided criteria.

### StudioOnline User Saved Payments

#### Create a Hosted Page Token

```
DEFINITION
POST http://apiserver/studioonlineusers/:userId/savedpayments/:recordId/hostedpagetoken?companyCode=:companyCode&paymentGatewayCode=:paymentGatewayCode

EXAMPLE REQUEST
$.post("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/savedpayments/100035131/hostedpagetoken?companyCode=010&paymentGatewayCode=BRAINTREE");

EXAMPLE RESPONSE
{
    "hostedPageToken": "1234567890",
    "bin": "642413"
}

```

Creates a new hosted page token and retrieves related information for the saved payment.

##### Arguments

None

##### Returns

A new hosted page token and related information for the saved payment. Returns an error if a hosted page token could not be created.

### StudioOnline User Transaction History

#### Retrieve donation history

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/donationhistory?store=:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/donationhistory?store=19");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "625924",
            "projectCode": "110100",
            "project": {
                "AccountingSegment": "110100",
                "ActiveForAccounting": "1",
                "ActiveForDonor": "1",
                "BalanceType": "U",
                "Codes": {
                    "ECPROJCAT": "Projects"
                },
                "Company": "1",
                "DefaultDepartment": "100",
                "Description": "FCA Dallas Project",
                "Images": {
                    "IMAGELG": {
                        "ImageUrl": "https://www.example.donordirect.com/logo.png",
                        "Title": "FCA Logo",
                        "Description": "Large Image for 110100",
                        "AlternateText": "FCA Logo"
                    },
                    "IMAGESM": {
                        "ImageUrl": "https://www.example.donordirect.com/img2.png",
                        "Title": "Title2",
                        "Description": "Small Image for 110100",
                        "AlternateText": "Alt text2"
                    },
                    "IMAGEXS": {
                        "ImageUrl": "https://www.example.donordirect.com/img3.png",
                        "Description": "XS image"
                    }
                },
                "Notes": {
                    "ECPROJDESC": "Reaching almost 2 million people annually on the professional, college, high school, junior high and youth levels, FCA has grown into the largest sports ministry in the world.<br><br>Through this shared passion for athletes and faith, lives \"are\" changed for current and future generations. Your partnership is greatly appreciated & will help advance the Gospel in your local area."
                },
                "ProjectCode": "110100",
                "ProjectType": "PR",
                "RecordId": "1",
                "Subaccounts": [
                    "001"
                ],
                "Title": "Dallas \"FCA\" Project & Other Giving",
                "Url": "dallas-fca-project-other-giving",
                "UseInShoppingCart": "1",
                "PublishStart": "2017-11-30",
                "PublishEnd": "2030-12-31"
            },
            "pledge": null
            "totalAmount": 25,
            "subaccount": null,
            "subaccountDescription": null,
            "pledgeId": null,
            "pledgeDescription": null,
            "shortComment": null,
            "anonymous": "No",
            "date": "2017-09-13"
        },
        {...},
    ]
}

```

Returns a list of all donation history.

##### Arguments

* store (required) - StudioOnline store Id.
* startDate (required if endDate is provided) - A start date to filter history items by.
* endDate (required if startDate is provided) - An end date to filter history items by.
* forYearEndGiving - if true, only deductible donations will be returned.

##### Returns

A dictionary with an items property that contains an array of up to limit donation history objects, starting at index offset. Each entry in the array is a separate donation history object. If no more donation history objects are available, the resulting array will be empty. This request should never return an error.

#### Retrieve event attendee history

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/eventhistory?store=:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/43703/eventhistory?store=10029&all=true");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 0
    },
    "items": [
        {
            "id": "189498",
            "attendeeId": "1000008887",
            "attendeeFormattedName": "Nathan Johnson",
            "purchaserFormattedName": "Nathan Johnson",
            "documentNumber": "1142570",
            "quantity": 1
            "eventCode": "10ALT1",
            "eventData": {
                "Tangible": {
                    "@Id": "552",
                    "@RecordId": "6",
                    "@EventCode": "10ALT1",
                    "@Description": "Atlanta, GA - September 1st 2018",
                    "@Status": "1",
                    "@StartDate": "2018-12-22T00:00:00",
                    "@EndDate": "2018-12-23T00:00:00",
                    "@VenueCode": "RENNRICH",
                    "@PrimaryRoomCode": "WOODLAND",
                    "@AllowedToExceedCapacity": "1",
                    "@AllowedWaitlistProcessing": "1",
                    "@UseInShoppingCart": "0",
                    "@JournalReference": "0",
                    "@JEStatus": "Y",
                    "@EvaluationType": "TEST",
                    "@Warehouse": "30",
                    "@Title": "Atlanta, GA - September 1st 2018",
                    "@xmlns": "",
                    "Codes": {
                        "Entry": {
                            "@Key": "DDCEVNTAPP",
                            "@Value": "US Trip Applications"
                        }
                    },
                    "Notes": {
                        "Entry": {
                            "@Key": "DDCEVTINST",
                            "@Value": "Here are the Event Instructions!"
                        }
                    },
                    "Images": {
                        "Image": [
                            {
                                "@Type": "IMAGESM",
                                "@ImageUrl": "imageUrl/smimage.png",
                                "@Title": "Test",
                                "@Description": "Small Event Image For StudioOnline Use",
                                "@AlternateText": "Alt"
                            },
                            {
                                "@Type": "IMAGEXS",
                                "@ImageUrl": "imageUrl/xsimage.png",
                                "@Title": "Image Title",
                                "@Description": "Extra Small Event Img",
                                "@AlternateText": "Image Alt Text"
                            },
                            {
                                "@Type": "IMAGEXL",
                                "@ImageUrl": "imageUrl/xlargeimage.png",
                                "@Description": "Extra Large Image With Long Description"
                            },
                            {
                                "@Type": "IMAGEMD",
                                "@ImageUrl": "imageUrl/mdimage.png",
                                "@Title": "Event Image",
                                "@Description": "Event Image - Hands Raised",
                                "@AlternateText": "People in crowd raising hands"
                            }
                        ]
                    },
                    "Numbers": {
                        "Entry": [
                            {
                                "@Key": "DDCEVTNR1",
                                "@Value": "7"
                            },
                            {
                                "@Key": "DDCEVTNRM",
                                "@Value": "7"
                            }
                        ]
                    },
                    "Dates": {
                        "Entry": {
                            "@Key": "EVTPREREQ",
                            "@Value": "2015-10-13T00:00:00"
                        }
                    },
                    "Venue": {
                        "PrimaryVenue": {
                            "@Code": "RENNRICH",
                            "@Name": "Rennaissance Hotel Richardson",
                            "@AddressLine1": "5502 Ben Davis Rd",
                            "@Country": "USA",
                            "@CountryDescription": "United States of America",
                            "@PostalCode": "75048",
                            "@City": "Garland",
                            "@State": "TX",
                            "@StateDescription": "Texas"
                        }
                    }
                }
            },
            "eventDescription": "Atlanta, GA - September 1st 2018",
            "eventStatus": "C",
            "totalAmount": "219.99"
            "price": 99.99,
            "attended": false,
            "shortComment": "Once upon a time...",
            "sessions": [
                {
                    "id": "60872",
                    "documentNumber": "1142570",
                    "attendeeId": "1000008887",
                    "eventCode": "10ALT1",
                    "eventDescription": "Atlanta, GA - September 1st 2018",
                    "sessionCode": "S105",
                    "sessionDescription": "tWe Fight Too",
                    "price": 10.25,
                    "sessionStatus": null,
                    "shortComment": "Nill",
                    "sessionData": {
                        "Tangible": {
                            "@RecordId": "24",
                            "@EventCode": "10ALT1",
                            "@SessionCode": "S105",
                            "@Description": "test",
                            "@RoomCode": "RM102",
                            "@Date": "2010-09-30T00:00:00",
                            "@StartTime": "2019-03-25T14:00:00",
                            "@EndTime": "2019-03-25T15:30:00",
                            "@SessionType": "SEM",
                            "@AllowedToExceedCapacity": "0",
                            "@UseInShoppingCart": "1",
                            "@Title": "test",
                            "@xmlns": "",
                            "Dates": {
                                "Entry": {
                                    "@Key": "EVTSESSORG",
                                    "@Value": "2019-08-31T00:00:00"
                                }
                            },
                            "Room": {
                                "Room": {
                                    "@Code": "RM102",
                                    "@Name": "New room 2",
                                    "@ActualCapacity": "1",
                                    "@SellToCapacity": "1"
                                }
                            }
                        }
                    }
                },
                {...},
                {...}
            ]
        },
        {...},
        {...}
    ]
}

```

Returns a list of all event history for this user.

##### Arguments

* userId (required) - The user's guid.
* store (required) - StudioOnline store Id.

##### Returns

A dictionary with an items property that contains an array of up to limit event history objects, starting at index offset. Each entry in the array is a separate event history object. If no more event history objects are available, the resulting array will be empty. This request should never return an error.

#### Retrieve order history

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/orderhistory?store=:storeId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/01199F6A-F669-4AFB-BE78-87E4E8C1E4FF/orderhistory?store=19");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "425586",
            "productCode": "100STPR1",
            "product": {
                "Description": "ABC Booklet",
                "DiscountAllowed": "1",
                "Packaging": "P",
                "ProductCode": "100STPR1",
                "RecordId": "353",
                "Status": "A",
                "Title": "ABC Booklet",
                "Type": "P",
                "Url": "abc-booklet",
                "UseInShoppingCart": "1",
                "Weight": "1.0000"
            },
            "amount": 6.3,
            "shortComment": null,
            "quantity": 1,
            "orderDate": "2017-06-12",
            "shipDate": null,
            "shipMethod": null,
            "trackingNumber": null,
            "backorder": "No"
        },
        {...},
    ]
}

```

Returns a list of all order history.

##### Arguments

* store (required) - StudioOnline store Id.
* startDate (required if endDate is provided) - A start date to filter history items by.
* endDate (required if startDate is provided) - An end date to filter history items by.
* forYearEndGiving - if true, only deductible, promotional items will be returned.

##### Returns

A dictionary with an items property that contains an array of up to limit order history objects, starting at index offset. Each entry in the array is a separate order history object. If no more order history objects are available, the resulting array will be empty. This request should never return an error.

#### Retrieve subscription history

```
DEFINITION
GET http://apiserver/studioonlineusers/:userId/subscriptionhistory?store=:storeId&subscriptionType=:subscriptionType&fulfillmentMethod=:fulfillmentMethod&subscriptionId=:subscriptionId

EXAMPLE REQUEST
$.get("http://localhost:49195/studioonlineusers/74547B4B-780C-4786-BD98-A461F07D4CB2/subscriptionhistory?store=10029&subscriptionType=B&fulfillmentMethod=EMAIL");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "162345",
            "accountNumber": "43703",
            "formattedName": "Dr. Nathan Test Johnson",
            "subscriptionType": "B",
            "subscriptionCode": "OMM",
            "subscriptionData": {
                "Tangible": {
                    "@RecordId": "49",
                    "@SubscriptionCode": "OMM",
                    "@Description": "A generic subscription for a generic membership.",
                    "@SubscriptionType": "B",
                    "@SubscriptionFrequency": "M",
                    "@Active": "1",
                    "@UseInShoppingCart": "1",
                    "@AutoRenewDefault": "0",
                    "@Title": "Generic Membership",
                    "@Url": "generic-membership",
                    "@PublishStart": "2019-01-10",
                    "@PublishEnd": "2019-12-12",
                    "@xmlns": "",
                    "Codes": {
                        "Entry": {
                            "@Key": "DDCDEFSUB",
                            "@Value": "Yes"
                        }
                    },
                    "Images": {
                        "Image": {
                            "@Type": "IMAGEMD",
                            "@ImageUrl": "imageUrl",
                            "@Title": "A Title",
                            "@Description": "Generic image for a generic membership",
                            "@AlternateText": "There is no alternative."
                        }
                    },
                    "Numbers": {
                        "Entry": {
                            "@Key": "DDCGRCPRD",
                            "@Value": "15"
                        }
                    }
                }
            },
            "subscriptionStatus": "P",
            "statusDescription": "Pending",
            "startDate": "2019-09-04",
            "copyCount": 1,
            "numberOfIssues": 1,
            "numberRemaining": 0,
            "sourceCode": "0_A_B_M_N",
            "sourceDescription": "Zero",
            "fulfillmentMethod": null,
            "fulfillmentMethodDescription": null,
            "neverExpires": false,
            "priceCode": "1Y",
            "priceCodeDescription": "One Year Price",
            "totalAmount": 130.1100,
            "remainingDeferredAmount": 0.0000,
            "shortComment": null,
            "cancelDate": null,
            "cancelReasonCode": null,
            "cancelReasonDescription": null,
            "expirationDate": null,
            "lastDate": "2019-09-04",
            "deliveryId": 0,
            "deliveryDescription": null,
            "autoRenew": true,
            "nextRenewalDate": null,
            "renewalPriceCode": "1YR",
            "renewalPriceCodeDescription": "One Year Renewal Price",
            "savedPaymentId": 222,
            "paymentName": null,
            "paymentType": "CC",
            "paymentTypeDescription": "Credit Card",
            "referenceNumber": "VISA-1111 03/2021 Nathan Johnson",
            "purchasedByAccountNumber": "46199",
            "purchasedByFormattedName": "Nathan Johnson"
        },
        {...},
    ]
}

```

Returns a list of all subscription history.

##### Arguments

* store (required) - StudioOnline store Id.
* subscriptionType (required) - The type of transaction to retrieve: B: Membership, M: Magazine, P: Product.
* fulfillmentMethod (required for Magazine) - The type of fulfillment method used to deliver the magazine: EMAIL and MAIL.
* subscriptionId (optional) - The record Id of the subscription to retrieve.

##### Returns

A dictionary with an items property that contains an array of up to limit subscription history objects, starting at index offset. Each entry in the array is a separate subscription history object. If no more subscription history objects are available, the resulting array will be empty. This request should never return an error.

### Transactions

#### Create a transaction

```
DEFINITION
POST http://apiserver/transactions

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions", {
    "account": "7",
    "batch": "17098",
    "currency": "USD",
    "arPayments": [...],
    "donations": [...],
    "donationAcknowledgments": [...],
    "donationAcknowledgmentItems": [...],
    "events": [...],
    "orders": [...],
    "payments": [...],
    "subscriptions": [...],
    "response": {
        "letter": "LETTER"
    },
    "source": "AD1D2234A"
});

EXAMPLE RESPONSE
{
    "id": "25445",
    "account": "7",
    "batch": "17098",
    "currency": "USD",
    "response": {
        "letter": "LETTER"
    },
    "isTaxExempt": false,
    "mediaOutlet": null,
    "dma": null,
    "contactMethod": null,
    "status": "A",
    "amount": 200,
    "amountDue": 0,
    "remainingAmountDue": 0,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "autoCalculateShipping": true,
    "company": "4",
    "companyDescription": "DonorDirect",
    "recurringHeaderId": null,
    "warnings": ["Recurring creation failed. Manual entry is needed", ...]
}

```

Creates a new transaction object.

##### Arguments

* account (required) - The account number of the transaction.
* batch (required) - The batch number of the transaction.
* currency (required) - The currency code of the transaction.
* source (required) - The source code of the transaction.
* arPayments (optional) - An array of transaction AR payment objects to be created as part of the transaction. See [transaction AR payments](#create-a-transaction-ar-payment) for required fields.
* donations (optional) - An array of transaction donation objects to be created as part of the transaction. See [transaction donation](#create-a-transaction-donation) for required fields.
* donationAcknowledgments (optional) - An array of transaction donation acknowledgment objects to be created as part of the transaction. See [transaction donation acknowledgment](#create-a-transaction-donation-acknowledgment) for required fields.
* donationAcknowledgmentItems (optional) - An array of transaction donation acknowledgment item objects to be created as part of the transaction. See [transaction donation acknowledgment item](#create-a-transaction-donation-acknowledgment-item) for required fields.
* events (optional) - An array of transaction event objects to be created as part of the transaction. See [transaction event](#create-a-transaction-event) for required fields.
* orders (optional) - An array of transaction order objects to be created as part of the transaction. See [transaction order](#create-a-transaction-order) for required fields.
* payments (optional) - An array of transaction payment objects to be created as part of the transaction. See [transaction payment](#create-a-transaction-payment) for required fields.
* subscriptions (optional) - An array of transaction subscription objects to be created as part of the transaction. See [transaction subscription](#create-a-transaction-subscription) for required fields.
* attachments (optional) - An array of transaction attachment objects to be created as part of the transaction. See [transaction attachment](#create-a-transaction-attachment) for required fields.
* notes (optional) - An array of transaction note objects to be created as part of the transaction. See [transaction note](#create-a-transaction-note) for required fields.
* isTaxExempt (optional) - Whether or not the transaction is tax exempt.
* mediaOutlet (optional) - The media outlet id of the transaction.
* contactMethod (optional) - The contact method of the transaction.
* isDefaultDonation (optional) - Whether or not the donation should be saved as a future default donation. If not specified, will default to `false`.
* printDonationReceipt (optional) - Whether or not a receipt should be generated for the donation. If not specified, will default to `true`.
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.
* autoCalculateShipping (optional; defaults to `true`) - Only applicable when the transaction has `orders`. A value of `false`, indicates that the provided `shippingAmount` on each of the `orders` is an overriden amount rather than an amount calculated by StudioEnterprise's shipping rate calculation. This is primarily meaningful if overriding shipping amounts so that the overridden shipping amounts remain when editing non-deposited transactions within StudioEnterprise. A primary use case for providing a value of `false` is if the `shippingAmount` was calculated outside of StudioEnterprise.
* accessorOverrideAuditInformationRecordIds (optional) - List of PCI Pal Accessor Override Audit Information Ids. This is to add the transaction document number to the Accessor Override Audit Information records that were created while entering the transaction.

##### Returns

Returns a transaction object if the call succeeded and created a transaction. Returns 204 No Content if the call succeeded but no transaction was created, such as recurring donations only. Returns an error if create parameters are invalid (e.g. specifying an undefined currency code or failing to specify a batch).

#### Retrieve a transaction

```
DEFINITION
GET http://apiserver/transactions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445");

EXAMPLE RESPONSE
{
    "id": "25445",
    "account": "7",
    "batch": "17098",
    "currency": "USD",
    "isTaxExempt": false,
    "mediaOutlet": null,
    "dma": null,
    "contactMethod": null,
    "status": "A",
    "amount": 200,
    "amountDue": 0,
    "remainingAmountDue": 0,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "autoCalculateShipping": true,
    "company": "4",
    "companyDescription": "DonorDirect",
    "recurringHeaderId": null
}

```

Retrieves the details of an existing transaction. You need only supply the transaction code.

If the T01\_GetAdditionalTransactionInformation\_ClientExtension SPROC contains logic, additional response data name in the format of additionalDetail1, additionalDetail2, etc. will be returned.

##### Arguments

* id (required) - The transaction code of the transaction to retrieve.

##### Returns

Returns a transaction object if a valid id was provided.

#### Update a transaction

```
DEFINITION
POST http://apiserver/transactions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445", {
    "isTaxExempt": true
});

EXAMPLE RESPONSE
{
    "id": "25445",
    "account": "7",
    "batch": "17098",
    "currency": "USD",
    "isTaxExempt": true,
    "mediaOutlet": null,
    "dma": null,
    "contactMethod": null,
    "status": "A",
    "amount": 200,
    "amountDue": 0,
    "remainingAmountDue": 0,
    "assignedToAccessor": null,
    "assignedToAccessorDescription": null,
    "autoCalculateShipping": true,
    "company": "4",
    "companyDescription": "DonorDirect",
    "recurringHeaderId": null
}


```

Updates the specified transaction by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an invalid transaction type or an undefined transaction status).

#### Delete a transaction

```
DEFINITION
DELETE http://apiserver/transactions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/25445", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a transaction. It cannot be undone.

##### Arguments

* id (required) - The document number of the transaction to be deleted.

##### Returns

Returns a 204 No Content response on success. If the document number does not exist, this call returns an error.

#### List all transactions

```
DEFINITION
GET http://apiserver/transactions

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions?account=16230");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 18
    },
    "items": [
        {
            "id": "83309",
            "account": "16230",
            "batch": "6503",
            "date": "2014-08-18",
            "status": "Y",
            "isTaxExempt": false,
            "mediaOutlet": null,
            "dma": null,
            "currency": "USD",
            "contactMethod": "EMAIL",
            "amount": 1123,
            "amountDue": 0,
            "remainingAmountDue": 0,
            "deposit": "0",
            "depositStatus": "Y",
            "donationTotal": 1103,
            "productTotal": 0,
            "shippingTotal": 0,
            "taxTotal": 0,
            "eventTotal": 0,
            "subscriptionTotal": 20,
            "arPaymentTotal": 0,
            "depositTotal": 0,
            "accountName": "Joe Smith",
            "letter": "LGR",
            "completionText": null,
            "response": 307550,
            "assignedToAccessor": null,
            "assignedToAccessorDescription": null,
            "autoCalculateShipping": true,
            "company": "4",
            "companyDescription": "DonorDirect",
            "recurringHeaderId": null,
            "couponCode": null,
            "couponDescription": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transactions matching the provided filter criteria.

If the T01\_GetAdditionalTransactionInformation\_ClientExtension SPROC contains logic, additional response data name in the format of additionalDetail1, additionalDetail2, etc. will be returned. See note with hasCreditAvailable and hasRemainingAmountDue arguments.

##### Arguments

It is not supported to do `GET /transactions` without any criteria. At minimum, `account`, `batch`, or `deposit` must be provided as criteria arguments in order to search transactions. It is not supported to provide `account` and `batch` and `deposit` as criteria arguments; only 1 can be specified.

* account (conditionally required) - Filter list by exact match on transaction account number.
* batch (conditionally required) - Filter list by exact match on transaction batch number
* deposit (conditionally required) - Filter list by exact match on deposit number
* forQuickEntry () - `forQuickEntry=true` is intended to be used for listing transactions on the same screen as a quick entry screen. The `batch` argument is required in conjunction with `forQuickEntry=true`.
* id () - Filter list by partial match in document number
* status () - Filter list by partial match in transaction status code
* remainingAmountDue () - Filter list based on one of two possible values: `<0` and `>0`. Neither value will include transactions with no remaining amount due. `>0` means there is a balance due. `<0` means there is a credit available.
* hasDonations () - Filter list based on whether or not the transaction has any donations.
* hasEvents () - Filter list based on whether or not the transaction has any events.
* hasOrders () - Filter list based on whether or not the transaction has any orders.
* hasSubscriptions () - Filter list based on whether or not the transaction has any subscriptions.
* hasCreditAvailable () - Filter list based on whether or not the transaction has credit available. When `hasCreditAvailable=true`, `source` and `sourceDescription` will also be returned as properties in the response. Will not return additional detail properties with this argument.
* hasRemainingAmountDue () - Filter list based on whether or not the transaction has a remaining amount due. When `hasRemainingAmountDue=true`, `source` and `sourceDescription` will also be returned as properties in the response. Will not return additional detail properties with this argument.
* getPageContainingId (optional) - Will return the page of transactions that contains the transaction with this id. (Only used when deposit is populated.)
* viewDeclined (optional) - Will only returned the decliend transactions (Only used when deposit is populated. Paging is not supported when this is true; all declined transactions are returned.)
* assignedToAccessor (optional) - The accessor of the user or authorized account assigned to the account.

##### Returns

A dictionary with an items property that contains an array of up to limit transactions, starting at index offset. Each entry in the array is a separate transaction object. If no more transactions are available, the resulting array will be empty. This request should never return an error.

#### Cancel declined parts of a transaction

```
DEFINITION
POST http://apiserver/transactions/:id/canceldeclined

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/144353/canceldeclined", {
});

EXAMPLE RESPONSE
204 No Content

```

This will cancel the declined payments of a declined transaction.

##### Arguments

##### Returns

Returns a 204 No Content response on success.

#### Retrieve a transactions isRealTimeRefundAllowed flag

```
DEFINITION
GET http://apiserver/transactions/:id/realtimerefund

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/144353/realtimerefund");

EXAMPLE RESPONSE
{
    "isRealTimeRefundAllowed": true
}

```

Retrieves the isRealTimeRefundAllowed flag of an existing transaction. You need only supply the transaction id.

##### Arguments

* id (required) - The id of the transaction for the isRealTimeRefundAllowed flag to be retrieved.

#### Returns

Returns isRealTimeRefundAllowed flag with the value 'true' or 'false'

### Transaction Applied AR Payments

#### List all transaction applied AR payments

```
DEFINITION
GET http://apiserver/transactions/:id/appliedarpayments

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/appliedarpayments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10790",
            "transaction": "184700",
            "amount": 500,
            "shortComment": null,
            "account": "16230"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction applied AR payments.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction applied AR payments, starting at index offset. Each entry in the array is a separate transaction applied AR payment object. If no more transaction applied AR payments are available, the resulting array will be empty. This request should never return an error.

### Transaction AR Payments

#### Create a transaction AR payment

```
DEFINITION
POST http://apiserver/transactions/:id/arpayments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/arpayments", {
    "transaction": "184703",
    "amount": 9
});

EXAMPLE RESPONSE
{
    "id": "110790",
    "transaction": "184703",
    "amount": 9,
    "shortComment": null,
    "account": "16230"

}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction AR payment can only be created as part of a transaction create POST.

##### Arguments

* transaction (required) - The document number to which the transaction AR payment should be applied.
* amount (required) - The amount of the transaction AR payment.
* shortComment (optional) - The short comment of the transaction AR payment.

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction AR payment

```
DEFINITION
GET http://apiserver/transactions/:id/arpayments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/arpayments/110790");

EXAMPLE RESPONSE
{
    "id": "110790",
    "transaction": "184703",
    "amount": 9,
    "shortComment": null,
    "account": "16230"
}

```

Retrieves the details of an existing transaction AR payment. You need only supply the transaction AR payment id.

##### Arguments

* id (required) - The id of the transaction AR payment to be retrieved.

##### Returns

Returns a transaction AR payment object if a valid id was provided.

#### Update a transaction AR payment

```
DEFINITION
POST http://apiserver/transactions/:id/arpayments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/arpayments/110790", {
    "shortComment": "AR payment"
});

EXAMPLE RESPONSE
{
    "id": "110790",
    "transaction": "184703",
    "amount": 9,
    "shortComment": "a comment",
    "account": "16230"
}


```

Updates the specified transaction AR payment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction AR payment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### Delete a transaction AR payment

```
DEFINITION
POST http://apiserver/transactions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688", {
    "arpayments": [{
        "id": "110790",
        "delete": true
    },
    { ... }]
});

```

Deleting an AR payment requires updating the transaction resource and specifying the id of the AR payment which should be deleted. This will permanently delete a transaction AR payment from the transaction.

Notice, it is not allowed to directly delete an AR payment. For example, the following will fail.

```
NOT ALLOWED:
$.ajax("http://localhost:49195/transactions/184688/arpayments/110790", { type: "DELETE" });

```

##### Arguments

* id (required) - The id of the transaction AR payment to be deleted.
* delete (required) - `"delete": true` is required in order to delete the AR payment.

##### Returns

Returns a 200 OK response on success. If the transaction AR Payment id does not exist or if the transaction is in a state where deleting the AR Payment is not allowed, then this call returns an error.

#### List all transaction AR payments

```
DEFINITION
GET http://apiserver/transactions/:id/arpayments

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/arpayments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "110790",
            "transaction": "184703",
            "amount": 9,
            "shortComment": null,
            "account": "16230",
            "originalArPayment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction AR payments.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction AR payments, starting at index offset. Each entry in the array is a separate transaction AR payment object. If no more transaction AR payments are available, the resulting array will be empty. This request should never return an error.

#### Cancel transaction AR payments

```
DEFINITION
POST http://apiserver/transactions/:id/arpayments/cancel

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/174815/arpayments/cancel", {
    items: [
        {
            id: "176572"
        },
        {
            id: "176574"
        }
    ],
    cancelDate: "2016-08-16",
    repaymentMethod: "REFUND"
});

EXAMPLE RESPONSE
{
    "Success": true,
    "FriendlyUIMessage": null,
    "AdditionalUIMessages": [],
    "CCResult":
        [
            {
                "Success": true,
                "ReferenceNumber": "VISA-1111 12/2016 Marc Smith",
                "ProcessorErrorCode": 0,
                "FriendlyUICCMessage": null,
                "TechnicalErrorMessage": null,
                "Amount": 10.0000,
                "Tax": 0.0
            }
        ],
    "TechnicalErrorMessage": null,
    "NewDocumentNumber": null
}


```

Cancels the specified transaction AR payments(s).

##### Arguments

* items (required) - Array of AR payments cancellation detail objects. Each object must contain the `id` of an AR payment.
* cancelDate (optional; defaults to current date) - Date for the cancellation. Used for identifying the correct deposit.
* repaymentMethod (required) - Method for repayment. Valid values: `REFUND`, `CREDIT`, or any valid value for the `DDCPAYTYPE` code type.
* isProcessed (optional; defaults to `false`) - Only applicable when `repaymentMethod` is `REFUND` and the original transaction payment was with a `CC`. When `true`, the cancellation will process in StudioEnterprise, but the funds will not be returned to the CC. This should only be used in scenarios where the funds have already been refunded to the CC such as by an external system.

##### Returns

Returns a result object, containing various messages regarding the result of the AR payment cancellation.

### Transaction Attachments

#### Create a transaction attachment

```
DEFINITION
POST http://apiserver/transactions/:id/attachments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/attachments", {
    "type":"IMAGE",
    "typeDescription":"Image",
    "file":"data:image/png;base64,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",
    "fileName":"logo64.png"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Creates a new transaction attachment object.

##### Arguments

* type (required) - The attachment type code. Must be a defined attachment type code.
* url (required when `fileName` is not specified) - The url where the attachment is located. Typically this is a network location or web link to a file.
* fileName (required when `url` is not specified) - The name of the file that is being uploaded to StudioEnterprise.
* file (required when `fileName` is specified) - The base64 encoded string of the file contents. The mime-type is prepended to the front of the base64 encoded string.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns a transaction attachment object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined attachment type or not specifying a url).

#### Retrieve a transaction attachment

```
DEFINITION
GET http://apiserver/transactions/:id/attachments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/attachments/49");

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "IMAGE",
    "typeDescription": "Image",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}

```

Retrieves the details of an existing transaction attachment. You need only supply the transaction attachment id.

##### Arguments

* id (required) - The id of the attachment to retrieve.
* download (optional) - `download=true` will force the `file` to be retrieved as a base64 string. `download=false` will cause the `file` property to be `null`.

##### Returns

Returns a transaction attachment object if a valid id was provided.

#### Update a transaction attachment

```
DEFINITION
POST http://apiserver/transactions/:id/attachments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/attachments/49", {
    "type": "LOGO"
});

EXAMPLE RESPONSE
{
    "longComment": "long comment text",
    "dateCreated": "2018-03-12",
    "id": "49",
    "type": "LOGO",
    "typeDescription": "Logo",
    "url": null,
    "fileName": "logo64.png",
    "file": null,
    "fileMimeType": "image/png"
}


```

Updates the specified transaction attachment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The attachment type. Must be a defined attachment type.
* url (optional) - The url of the attachment type.
* fileName (optional) - the name of the uploaded file.
* longComment (optional) - The long comment of the attachment.

##### Returns

Returns the transaction attachment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined transaction attachment type code).

#### Delete a transaction attachment

```
DEFINITION
DELETE http://apiserver/transactions/:id/attachments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/25445/attachments/49", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a transaction attachment. It cannot be undone.

##### Arguments

* id (required) - The id of the transaction attachment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the transaction attachment id does not exist, this call returns an error.

#### List all transaction attachments

```
DEFINITION
GET http://apiserver/transactions/:id/attachments

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/attachments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "longComment": "long comment text",
            "dateCreated": "2018-03-12",
            "id": "49",
            "type": "LOGO",
            "typeDescription": "Logo",
            "url": null,
            "fileName": "logo64.png",
            "file": null,
            "fileMimeType": "image/png"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all attachments for the specified transaction.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction attachments, starting at index offset. Each entry in the array is a separate transaction attachment. If no more transaction attachments are available, the resulting array will be empty. This request should never return an error.

### Transaction Credits

#### Create a transaction credit

```
DEFINITION
POST http://apiserver/transactions/:id/credits

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/154471/credits", {
    "transaction": "184705",
    "amount": 30
});

EXAMPLE RESPONSE
{
    "id": "10930",
    "transaction": "154468",
    "amount": 30,
    "shortComment": null,
    "account": "22697"
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction credit can only be created as part of a transaction create POST.

##### Arguments

* transaction (required) - The document number to which the transaction AR payment should be applied.
* amount (required) - The amount of the transaction AR payment.
* shortComment (optional) - The short comment of the transaction AR payment.

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction credit

```
DEFINITION
GET http://apiserver/transactions/:id/credits/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/credits/10930");

EXAMPLE RESPONSE
{
    "id": "10930",
    "transaction": "154468",
    "amount": -30,
    "shortComment": null,
    "account": "22697"
}

```

Retrieves the details of an existing transaction credit. You need only supply the transaction credit id.

##### Arguments

* id (required) - The id of the transaction credit to be retrieved.

##### Returns

Returns a transaction credit object if a valid id was provided.

#### Update a transaction credit

```
DEFINITION
POST http://apiserver/transactions/:id/credit/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/credit/10930", {
    "shortComment": "a comment"
});

EXAMPLE RESPONSE
{
    "id": "10930",
    "transaction": "154468",
    "amount": -30,
    "shortComment": "a comment",
    "account": "22697"
}


```

Updates the specified transaction credit by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction credit object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### Delete a transaction credit

```
DEFINITION
POST http://apiserver/transactions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688", {
    "credits": [{
        "id": "10930",
        "delete": true
    }]
});

```

Deleting a credit requires updating the transaction resource and specifying the id of the credit which should be deleted. This will permanently delete a transaction credit from the transaction.

Notice, it is not allowed to directly delete a credit. For example, the following will fail.

```
NOT ALLOWED:
$.ajax("http://localhost:49195/transactions/184688/credits/1810026", {"type": "DELETE"});

```

##### Arguments

* id (required) - The id of the transaction credit to be deleted.
* delete (required) - `"delete": true` is required in order to delete the credit.

##### Returns

Returns a 200 OK response on success. If the transaction credit id does not exist or if the transaction is in a state where deleting the credit distribution is not allowed, then this call returns an error.

#### List all transaction credits

```
DEFINITION
GET http://apiserver/transactions/:id/credits

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/credits");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "10930",
            "transaction": "154468",
            "amount": -30,
            "shortComment": "a comment",
            "account": "22697",
            "originalArPayment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction credits.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction credits, starting at index offset. Each entry in the array is a separate transaction credit object. If no more transaction credits are available, the resulting array will be empty. This request should never return an error.

### Transaction Donations

#### Create a transaction donation

```
DEFINITION
POST http://apiserver/transactions/:id/donations

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/donations", {
    "amount": 500,
    "source": "ABC08",
    "project": "220000"
});

EXAMPLE RESPONSE
{
    "id": "1810026",
    "amount": 500,
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "relatedAccount": null,
    "accountPledge": null,
    "isDeductible": true,
    "isAnonymous": false,
    "shortComment": null
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction donation can only be created as part of a transaction create POST.

##### Arguments

* amount (required) - The amount of the transaction donation.
* source (required) - The source code of the transaction donation.
* project (required) - The project code of the transaction donation.
* subaccount (optional) - The subaccount code of the transaction donation.
* relatedAccount (optional) - The associated account number of the transaction donation.
* response (optional) - The response of the transaction donation. Only permitted if relatedAccount is specified.
* accountPledge (optional) - The account pledge id of the transaction donation.
* isDeductible (optional) - Whether or not the transaction donation is deductible. If not specified, will default to true.
* isAnonymous (optional) - Whether or not the transaction donation is anonymous. If not specified, will default to false.
* shortComment (optional) - The short comment of the transaction donation.
* isRecurring (optional) - Whether or not the transaction donation is recurring. If not specified, will default to false.
* chargeToday (optional) - Whether or not the recurring donation should have a one-time charge as well. If not specified, will default to true.
* frequency (optional) - The frequency for the recurring donation.
* useOnDay (optional) - The day of the month to charge the recurring donation.
* category (optional) - The category code of the recurring donation. Must be a defined recurring transaction category code.
* startDate (optional) - The start date of the recurring donation.
* catalogItemRecordId (optional) - If the donation was for a catalog item, the unique identifier of that item (recordId)

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction donation

```
DEFINITION
GET http://apiserver/transactions/:id/donations/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/donations/1810026");

EXAMPLE RESPONSE
{
    "id": "1810026",
    "amount": 500,
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "relatedAccount": null,
    "accountPledge": null,
    "isDeductible": true,
    "isAnonymous": false,
    "shortComment": null,
    "originalDonation": null,
    "catalogItemRecordId": null,
    "catalog": null,
    "catalogDescription": null,
    "catalogItem": null,
    "catalogItemDescription": null,
    "catalogItemSuggestedPrice": null,
    "catalogItemMinimumAmount": null
}

```

Retrieves the details of an existing transaction donation. You need only supply the transaction donation id.

##### Arguments

* id (required) - The id of the transaction donation to be retrieved.

##### Returns

Returns a transaction donation object if a valid id was provided.

#### Update a transaction donation

```
DEFINITION
POST http://apiserver/transactions/:id/donations/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/donations/1810026", {
    "isAnonymous": true
});

EXAMPLE RESPONSE
{
    "id": "1810026",
    "amount": 500,
    "source": "ABC08",
    "project": "220000",
    "subaccount": null,
    "relatedAccount": null,
    "accountPledge": null,
    "isDeductible": true,
    "isAnonymous": true,
    "shortComment": null,
    "originalDonation": null,
    "catalogItemRecordId": null,
    "catalog": null,
    "catalogDescription": null,
    "catalogItem": null,
    "catalogItemDescription": null,
    "catalogItemSuggestedPrice": null,
    "catalogItemMinimumAmount": null
}


```

Updates the specified transaction donation by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction donation object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### Delete a transaction donation

```
DEFINITION
POST http://apiserver/transactions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688", {
    "donations": [{
        "id": "1810026",
        "delete": true
    },
    { ... }]
});


```

Deleting a donation requires updating the transaction resource and specifying the id of the donation which should be deleted. This will permanently delete a transaction donation from the transaction.

Notice, it is not allowed to directly delete a donation. For example, the following will fail.

```
NOT ALLOWED:
$.ajax("http://localhost:49195/transactions/184688/donations/1810026", {"type": "DELETE"});

```

##### Arguments

* id (required) - The id of the transaction donation to be deleted.
* delete (required) - `"delete": true` is required in order to delete the donation.

##### Returns

Returns a 200 OK response on success. If the transaction donation id does not exist or if the transaction is in a state where deleting the donation distribution is not allowed, then this call returns an error.

#### List all transaction donations

```
DEFINITION
GET http://apiserver/transactions/:id/donations

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83309/donations");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "125676",
            "amount": 502,
            "source": "G12GENERAL",
            "sourceDescription": "General Source Code",
            "elementGroup": null,
            "elementGroupDescription": null,
            "project": "110102",
            "projectDescription": "Special Endowment",
            "subaccount": null,
            "subaccountDescription": null,
            "relatedAccount": "16234",
            "relatedAccountName": "Jane Smith",
            "accountPledge": null,
            "pledgeCode": null,
            "pledgeDescription": null,
            "isDeductible": true,
            "isAnonymous": false,
            "shortComment": null,
            "response": {
                "id": 307552,
                "type": "RECEIPT",
                "method": null,
                "status": "H",
                "profileGroup": null,
                "printGroup": null,
                "printDate": null,
                "orderId": null,
                "addressLine1": "1234 North Lights Way",
                "letter": "0613APPLNO"
            },
            "suggestedDonation": null,
            "originalDonation": null,
            "catalogItemRecordId": null,
            "catalog": null,
            "catalogDescription": null,
            "catalogItem": null,
            "catalogItemDescription": null,
            "catalogItemSuggestedPrice": null,
            "catalogItemMinimumAmount": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction donations.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction donations, starting at index offset. Each entry in the array is a separate transaction donation object. If no more transaction donations are available, the resulting array will be empty. This request should never return an error.

#### Cancel transaction donations

```
DEFINITION
POST http://apiserver/transactions/:id/donations/cancel

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/174815/donations/cancel", {
    donations: [
        {
            id: "176426"
        },
        {
            id: "176427"
        }
    ],
    cancelDate: "2014-11-17",
    repaymentMethod: "REFUND"
});

EXAMPLE RESPONSE
{
    "Success": true,
    "FriendlyUIMessage": null,
    "AdditionalUIMessages": [],
    "CCResult":
        [
            {
                "Success": true,
                "ReferenceNumber": "VISA-1111 12/2014 Marc Smith",
                "ProcessorErrorCode": 0,
                "FriendlyUICCMessage": null,
                "TechnicalErrorMessage": null,
                "Amount": 10.0000,
                "Tax": 0.0
            }
        ],
    "TechnicalErrorMessage": null,
    "NewDocumentNumber": null
}


```

Cancels the specified transaction donation(s). If no ids are specified, all donations on the transaction will be canceled.

##### Arguments

* donations (required) - Array of donation cancellation detail objects. Each object must contain the `id` of a donation detail.
* cancelDate (optional; defaults to current date) - Date for the cancellation. Used for identifying the correct deposit.
* repaymentMethod (required) - Method for repayment. Valid values: `REFUND`, `CREDIT`, `CONVERTTODONATION` or any valid value for the `DDCPAYTYPE` code type.
* isProcessed (optional; defaults to `false`) - Only applicable when `repaymentMethod` is `REFUND` and the original transaction payment was with a `CC`. When `true`, the cancellation will process in StudioEnterprise, but the funds will not be returned to the CC. This should only be used in scenarios where the funds have already been refunded to the CC such as by an external system.

##### Returns

Returns a result object, containing various messages regarding the result of the transaction cancellation.

### Transaction Donation Acknowledgments

#### Create a transaction donation acknowledgment

```
DEFINITION
POST http://apiserver/transactions/:id/donationacknowledgments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/donationacknowledgments", {
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "zipPostal": "54364",
    "letterCode": "HONOR",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": false,
    "donorAddress": "465536"
});

EXAMPLE RESPONSE
{
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "addressLine1": "800 F St NW",
    "addressLine2": null,
    "addressLine3": null,
    "addressLine4": null,
    "city": "Washington",
    "state": "DC",
    "zipPostal": "20004",
    "country": "US",
    "responseId": "63546",
    "letterCode": "HONOR",
    "letterCodeDescription": "In honor of",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": false,
    "donorAddress": "465536",
    "donorAddressLine1": "119 Hemenway St",
    "donorAddressLine2": null,
    "donorAddressLine3": null,
    "donorAddressLine4": null,
    "donorCity": "Boston",
    "donorState": "MA",
    "donorZipPostal": "02115",
    "donorCountry": "US",
    "responseStatus": "H",
    "profileGroupId": "5847",
    "printGroupId": null,
    "printDate": null
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction donation acknowledgment can only be created as part of a transaction create POST.

##### Arguments

* documentNumber (required) - The document number (transactionId) of the donation acknowledgment
* recipientAccountNumber (required) - The account number of the recipient of the donation acknowledgment
* recipientAddress (required) - The addressId of the recipient of the donation acknowledgment
* letterCode (required) - The letter code used in the response for the donation acknowledgment
* fromName (required) - The name used in the from line of the donation acknowledgment
* toName (required) - The name used in the to line of the donation acknowledgment
* message (optional) - The message put on the donation acknowledgment
* sendToDonor (required) - Whether to send the donation acknowledgment to the recipient or the donor
* donorAddress (required if sendToDonor is true) - The address of the donor, used if we are sending the acknowledgment to the donor

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction donation acknowledgment

```
DEFINITION
GET http://apiserver/transactions/:id/donationacknowledgments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/donationacknowledgments/45");

EXAMPLE RESPONSE
{
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "addressLine1": "800 F St NW",
    "addressLine2": null,
    "addressLine3": null,
    "addressLine4": null,
    "city": "Washington",
    "state": "DC",
    "zipPostal": "20004",
    "country": "US",
    "responseId": "63546",
    "letterCode": "HONOR",
    "letterCodeDescription": "In honor of",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": false,
    "donorAddress": "465536",
    "donorAddressLine1": "119 Hemenway St",
    "donorAddressLine2": null,
    "donorAddressLine3": null,
    "donorAddressLine4": null,
    "donorCity": "Boston",
    "donorState": "MA",
    "donorZipPostal": "02115",
    "donorCountry": "US",
    "responseStatus": "H",
    "profileGroupId": "5847",
    "printGroupId": null,
    "printDate": null
}

```

Retrieves the details of an existing transaction donation acknowledgment. You need only supply the transaction donation acknowledgment id.

##### Arguments

* id (required) - The id of the transaction donation acknowledgment to be retrieved.

##### Returns

Returns a transaction donation acknowledgment object if a valid id was provided.

#### Update a transaction donation acknowledgment

```
DEFINITION
POST http://apiserver/transactions/:id/donationacknowledgments/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/donationacknowledgments/45", {
    "sendToDonor": true
});

EXAMPLE RESPONSE
{
    "id": "45",
    "documentNumber": "44635",
    "recipientAccountNumber": "6345",
    "recipientAccountName": "Robert Franklin",
    "recipientAddress": "87649",
    "addressLine1": "800 F St NW",
    "addressLine2": null,
    "addressLine3": null,
    "addressLine4": null,
    "city": "Washington",
    "state": "DC",
    "zipPostal": "20004",
    "country": "US",
    "responseId": "63546",
    "letterCode": "HONOR",
    "letterCodeDescription": "In honor of",
    "fromName": "Bobby",
    "toName": "Jack",
    "message": "Thanks for speaking at our event!",
    "sendToDonor": true,
    "donorAddress": "465536",
    "donorAddressLine1": "119 Hemenway St",
    "donorAddressLine2": null,
    "donorAddressLine3": null,
    "donorAddressLine4": null,
    "donorCity": "Boston",
    "donorState": "MA",
    "donorZipPostal": "02115",
    "donorCountry": "US",
    "responseStatus": "H",
    "profileGroupId": "5847",
    "printGroupId": null,
    "printDate": null
}


```

Updates the specified transaction donation acknowledgment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction donation acknowledgment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### Delete a transaction donation acknowledgment

```
DEFINITION
DELETE http://apiserver/transactions/:id/donationacknowledgments/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/184688/donationacknowledgments/45", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Deleting a donation acknowledgment requires updating the transaction resource and specifying the id of the donation acknowledgment which should be deleted. This will permanently delete a transaction donation acknowledgment from the transaction.

Notice, it is not allowed to directly delete a donation acknowledgment. For example, the following will fail.

```
NOT ALLOWED:
$.ajax("http://localhost:49195/transactions/184688/donationacknowledgments/45", {"type": "DELETE"});

```

##### Arguments

* id (required) - The id of the transaction donation acknowledgment to be deleted.

##### Returns

Returns a 200 OK response on success. If the transaction donation acknowledgment id does not exist or if the response has been printed, then this call returns an error.

#### List all transaction donation acknowledgments

```
DEFINITION
GET http://apiserver/transactions/:id/donationacknowledgments

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83309/donationacknowledgments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "45",
            "documentNumber": "44635",
            "recipientAccountNumber": "6345",
            "recipientAccountName": "Robert Franklin",
            "recipientAddress": "87649",
            "addressLine1": "800 F St NW",
            "addressLine2": null,
            "addressLine3": null,
            "addressLine4": null,
            "city": "Washington",
            "state": "DC",
            "zipPostal": "20004",
            "country": "US",
            "responseId": "63546",
            "letterCode": "HONOR",
            "letterCodeDescription": "In honor of",
            "fromName": "Bobby",
            "toName": "Jack",
            "message": "Thanks for speaking at our event!",
            "sendToDonor": false,
            "donorAddress": "465536",
            "donorAddressLine1": "119 Hemenway St",
            "donorAddressLine2": null,
            "donorAddressLine3": null,
            "donorAddressLine4": null,
            "donorCity": "Boston",
            "donorState": "MA",
            "donorZipPostal": "02115",
            "donorCountry": "US",
            "responseStatus": "H",
            "profileGroupId": "5847",
            "printGroupId": null,
            "printDate": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction donation acknowledgments.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction donation acknowledgments, starting at index offset. Each entry in the array is a separate transaction donation acknowledgment object. If no more transaction donation acknowledgments are available, the resulting array will be empty. This request should never return an error.

### Transaction Donation Acknowledgment Items

#### Create a transaction donation acknowledgment item

```
DEFINITION
POST http://apiserver/transactions/:id/donationacknowledgments/:id/items

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/donationacknowledgments/45/items", {
    "donationId": "6596"
});

EXAMPLE RESPONSE
{
    "id": "53",
    "donationAcknowledgmentId": "45",
    "donationId": "6596",
    "amount": 20.5,
    "description": "Water Wells in Africa"
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction donation acknowledgment item can only be created as part of a transaction create POST.

##### Arguments

* donationId (required) - The identifier (or temporary identifier) of the donation within the same transaction that is being acknowledged.

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction donation acknowledgment item

```
DEFINITION
GET http://apiserver/transactions/:id/donationacknowledgments/:id/items/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/donationacknowledgments/45/items/53");

EXAMPLE RESPONSE
{
    "id": "53",
    "donationAcknowledgmentId": "45",
    "donationId": "6596",
    "amount": 20.5,
    "description": "Water Wells in Africa"
}

```

Retrieves the details of an existing transaction donation acknowledgmentitem. You need only supply the transaction donation acknowledgment item id.

##### Arguments

* id (required) - The id of the transaction donation acknowledgment item to be retrieved.

##### Returns

Returns a transaction donation acknowledgment item object if a valid id was provided.

#### Delete a transaction donation acknowledgment item

```
DEFINITION
DELETE http://apiserver/transactions/:id/donationacknowledgments/:id/items/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/184688/donationacknowledgments/45/items/53", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Deleting a donation acknowledgment item requires updating the transaction resource and specifying the id of the donation acknowledgment item which should be deleted. This will permanently delete a transaction donation acknowledgment item from the transaction.

Notice, it is not allowed to directly delete a donation acknowledgment item. For example, the following will fail.

```
NOT ALLOWED:
$.ajax("http://localhost:49195/transactions/184688/donationacknowledgments/45/items/53", {"type": "DELETE"});

```

##### Arguments

* id (required) - The id of the transaction donation acknowledgment to be deleted.

##### Returns

Returns a 200 OK response on success. If the transaction donation acknowledgment item id does not exist or if the response has been printed, then this call returns an error.

#### List all transaction donation acknowledgment items

```
DEFINITION
GET http://apiserver/transactions/:id/donationacknowledgments/:id/items

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83309/donationacknowledgments/45/items");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "53",
            "donationAcknowledgmentId": "45",
            "donationId": "6596",
            "amount": 20.5,
            "description": "Water Wells in Africa"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction donation acknowledgment items.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction donation acknowledgment items, starting at index offset. Each entry in the array is a separate transaction donation acknowledgment item object. If no more transaction donation acknowledgment items are available, the resulting array will be empty. This request should never return an error.

### Account Donation Acknowledgment Items

#### Create an account donation acknowledgment item

```
DEFINITION
POST http://apiserver/accounts/:id/donationacknowledgments/:id/items

EXAMPLE REQUEST
$.post("http://localhost:49195/accounts/184688/donationacknowledgments/45/items", {
    "donationId": "6596"
});

EXAMPLE RESPONSE
{
    "id": "53",
    "donationAcknowledgmentId": "45",
    "donationId": "6596",
    "amount": 20.5,
    "description": "Water Wells in Africa"
}

```

##### Arguments

* donationId (required) - The identifier (or temporary identifier) of the donation that is being acknowledged.

##### Returns

Returns the account donation acknowledgment item object the was created.

#### Retrieve an account donation acknowledgment item

```
DEFINITION
GET http://apiserver/accounts/:id/donationacknowledgments/:id/items/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/184688/donationacknowledgments/45/items/53");

EXAMPLE RESPONSE
{
    "id": "53",
    "donationAcknowledgmentId": "45",
    "donationId": "6596",
    "amount": 20.5,
    "description": "Water Wells in Africa"
}

```

Retrieves the details of an existing account donation acknowledgment item. You need only supply the donation acknowledgment item id.

##### Arguments

* id (required) - The id of the account donation acknowledgment item to be retrieved.

##### Returns

Returns a account donation acknowledgment item object if a valid id was provided.

#### Delete an account donation acknowledgment item

```
DEFINITION
DELETE http://apiserver/accounts/:id/donationacknowledgments/:id/items/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/accounts/184688/donationacknowledgments/45/items/53", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

This will permanently delete a account donation acknowledgment item from the account.

##### Arguments

* id (required) - The id of the account donation acknowledgment to be deleted.

##### Returns

Returns a 200 OK response on success. If the account donation acknowledgment item id does not exist or if the response has been printed, then this call returns an error.

#### List all account donation acknowledgment items

```
DEFINITION
GET http://apiserver/accounts/:id/donationacknowledgments/:id/items

EXAMPLE REQUEST
$.get("http://localhost:49195/accounts/83309/donationacknowledgments/45/items");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "53",
            "donationAcknowledgmentId": "45",
            "donationId": "6596",
            "amount": 20.5,
            "description": "Water Wells in Africa"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all account donation acknowledgment items.

##### Returns

A dictionary with an items property that contains an array of up to limit account donation acknowledgment items, starting at index offset. Each entry in the array is a separate account donation acknowledgment item object. If no more account donation acknowledgment items are available, the resulting array will be empty. This request should never return an error.

#### Transaction Editable Status

##### Retrieve a transaction editable status

```
DEFINITION
GET http://localhost:49195/transactions/:id/editablestatus

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/editablestatus");

EXAMPLE RESPONSE
{
    "isEditable": true,
    "depositStatus": "OPEN"
}

```

##### Returns

Returns the edit status of a transaction.

### Transaction Events

#### Create a transaction event

```
DEFINITION
POST http://apiserver/transactions/:id/events

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/events", {
    "event": "WTR6",
    "priceCode": "I",
    "amount": 55,
    "quantity": 1
});

EXAMPLE RESPONSE
{
    "id": "5149",
    "event": "WTR6",
    "priceCode": "I",
    "amount": 55,
    "quantity": 1,
    "source": "AD1D2234A",
    "account": "7",
    "status": "W",
    "group": null,
    "hasAttended": false,
    "shortComment": null
}

```

Creates a new transaction event object.

##### Arguments

* event (required) - The event code of the transaction event.
* priceCode (required) - The price code of the transaction event. Must be a defined price code for events.
* amount (required) - The amount of the transaction event.
* quantity (required) - The quantity of the transaction event.
* source (optional) - The source code of the transaction event.
* account (optional) - The account number of the attendee of the transaction event.
* group (optional) - The group id of the transaction event.
* shortComment (optional) - The short comment of the transaction event.
* sessions (optional) - An array of transaction event session objects to be created as part of the transaction event. See [transaction event sessions](#create-a-transaction-event-session) for required fields.

##### Returns

Returns a transaction event object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying **\_\_\_**).

#### Retrieve a transaction event

```
DEFINITION
GET http://apiserver/transactions/:id/events/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/events/5149");

EXAMPLE RESPONSE
{
    "id": "5149",
    "event": "WTR6",
    "priceCode": "I",
    "amount": 55,
    "quantity": 1,
    "source": "AD1D2234A",
    "account": "7",
    "status": "W",
    "group": null,
    "hasAttended": false,
    "shortComment": null
}

```

Retrieves the details of an existing transaction event. You need only supply the transaction event id.

##### Arguments

* id (required) - The id of the transaction event to be retrieved.

##### Returns

Returns a transaction event object if a valid id was provided.

#### Transfer a transaction event

```
DEFINITION
POST http://apiserver/transactions/:id/events/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/events/5149", {
    "attendeeAccount": "5"
});

EXAMPLE RESPONSE
{
    attendeeAccount : "5",
    attendeeAccountName : "Miss Stephanie Aurora",
    elementGroup : null,
    elementGroupDescription : null,
    event : "Ministries Rock",
    eventDescription : null,
    extendedAmount : null,
    group : null,
    hasAttended : false,
    id : "1000008724",
    price : 0,
    priceCode : "EMPLOYEE",
    quantity : 1,
    response : null,
    shortComment : null,
    source : "TEST",
    sourceDescription : null,
    status : "C"
}


```

Transfers the specified transaction event by setting the attendee account.

##### Returns

Returns the transaction event object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### List all transaction events

```
DEFINITION
GET http://apiserver/transactions/:id/events

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83284/events");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000007810",
            "hasAttended": false,
            "event": "WTRCS1014",
            "eventDescription": "Family Savers",
            "priceCode": "I",
            "price": 500,
            "quantity": 1,
            "extendedAmount": 800,
            "source": "G12GENERAL",
            "sourceDescription": "General Source Code",
            "elementGroup": null,
            "elementGroupDescription": null,
            "attendeeAccount": "16230",
            "attendeeAccountName": "Joe Smith",
            "status": "C",
            "group": null,
            "shortComment": null,
            "response": {
                "id": 307524,
                "type": "EVENTACK",
                "method": null,
                "status": "H",
                "profileGroup": null,
                "printGroup": null,
                "printDate": null,
                "orderId": 7209,
                "addressLine1": "1234 Gondola Way",
                "letter": "LGR"
            }
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction events.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction events, starting at index offset. Each entry in the array is a separate transaction event object. If no more transaction events are available, the resulting array will be empty. This request should never return an error.

#### Cancel transaction events

```
DEFINITION
POST http://apiserver/transactions/:id/events/cancel

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/174815/events/cancel", {
    items: [
        {
            id: "176426"
        },
        {
            id: "176427"
        }
    ],
    cancelDate: "2014-12-08",
    cancellationFee: 5.00
    repaymentMethod: "REFUND"
});

EXAMPLE RESPONSE
{
    "Success": true,
    "FriendlyUIMessage": null,
    "AdditionalUIMessages": [],
    "CCResult":
        [
            {
                "Success": true,
                "ReferenceNumber": "VISA-1111 12/2014 Marc Smith",
                "ProcessorErrorCode": 0,
                "FriendlyUICCMessage": null,
                "TechnicalErrorMessage": null,
                "Amount": 10.0000,
                "Tax": 0.0
            }
        ],
    "TechnicalErrorMessage": null,
    "NewDocumentNumber": null
}


```

Cancels the specified transaction event(s). If no ids are specified, all events on the transaction will be canceled.

##### Arguments

* items (required) - Array of event cancellation detail objects. Each object must contain the `id` of an event registration.
* cancelDate (optional; defaults to current date) - Date for the cancellation. Used for identifying the correct deposit.
* cancellationFee (optional; defaults to `0`) - A fee to apply to the event registration cancellation.
* repaymentMethod (required) - Method for repayment. Valid values: `REFUND`, `CREDIT`, `CONVERTTODONATION` or any valid value for the `DDCPAYTYPE` code type.
* isProcessed (optional; defaults to `false`) - Only applicable when `repaymentMethod` is `REFUND` and the original transaction payment was with a `CC`. When `true`, the cancellation will process in StudioEnterprise, but the funds will not be returned to the CC. This should only be used in scenarios where the funds have already been refunded to the CC such as by an external system.

##### Returns

Returns a result object, containing various messages regarding the result of the transaction cancellation.

### Transaction Event Sessions

#### Create a transaction event session

```
DEFINITION
POST http://apiserver/transactions/:id/events/:id/sessions

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/events/5149/sessions", {
    "session": "BUD",
    "priceCode": "I",
    "amount": 55,
    "quantity": 1
});

EXAMPLE RESPONSE
{
    "id": "7404",
    "session": "BUD",
    "priceCode": "I",
    "amount": 55,
    "quantity": 1,
    "status": "C",
    "shortComment": null
}

```

Creates a new transaction event session object.

##### Arguments

* session (required) - The session code of the transaction event session. Must be a defined session code for the specified event.
* priceCode (required) - The price code of the transaction event session. Must be a defined price code for events.
* amount (required) - The amount of the transaction event session.
* quantity (required) - The quantity of the transaction event session.
* shortComment (optional) - The short comment of the transaction event session.
* status (optional) - The status code of the transaction event session. This value is blank if not provided.

##### Returns

Returns a transaction event session object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined session code).

#### Retrieve a transaction event session

```
DEFINITION
GET http://apiserver/transactions/:id/events/:id/sessions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/events/5149/sessions/7404");

EXAMPLE RESPONSE
{
    "id": "7404",
    "session": "BUD",
    "priceCode": "I",
    "amount": 55,
    "quantity": 1,
    "status": "C",
    "shortComment": null
}

```

Retrieves the details of an existing transaction event session. You need only supply the transaction event session id.

##### Arguments

* id (required) - The id of the transaction event session to be retrieved.

##### Returns

Returns a transaction event session object if a valid id was provided.

#### Update a transaction event session

```
DEFINITION
POST http://apiserver/transactions/:id/events/:id/sessions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/events/5149/sessions/7404", {
    "shortComment": "The attendee registered late."
});

EXAMPLE RESPONSE
{
    "id": "7404",
    "session": "BUD",
    "priceCode": "I",
    "amount": 55,
    "quantity": 1,
    "status": "C",
    "shortComment": "The attendee registered late."
}


```

Updates the specified transaction event session by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction event session object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### Delete a transaction event session

```
DEFINITION
DELETE http://apiserver/transactions/:id/events/:id/sessions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/25445/events/5149/sessions/7404", { type: "DELETE" });

EXAMPLE
204 No Content

```

Permanently deletes a transaction event session. It cannot be undone.

##### Arguments

* id (required) - The id of the transaction event session to be deleted.

##### Returns

Returns a 204 No Content response on success. If the transaction event session id does not exist, this call returns an error.

#### List all transaction event sessions

```
DEFINITION
GET http://apiserver/transactions/:id/events/:id/sessions

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83284/events/1000007810/sessions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "265",
            "session": "S101",
            "sessionDescription": "Laying the Foundation",
            "priceCode": "I",
            "price": 100,
            "quantity": 1,
            "status": "C",
            "shortComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction event sessions.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction event sessions, starting at index offset. Each entry in the array is a separate transaction event session object. If no more transaction event sessions are available, the resulting array will be empty. This request should never return an error.

#### Cancel transaction event sessions

```
DEFINITION
POST http://apiserver/transactions/:id/events/:id/sessions/cancel

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/174815/events/12124/sessions/cancel", {
    items: [
        {
            id: "176426"
        },
        {
            id: "176427"
        }
    ],
    attendeeId: "12434"
    cancelDate: "2014-12-08",
    cancellationFee: 5.50,
    repaymentMethod: "REFUND"
});

EXAMPLE RESPONSE
{
    "Success": true,
    "FriendlyUIMessage": null,
    "AdditionalUIMessages": [],
    "CCResult":
        [
            {
                "Success": true,
                "ReferenceNumber": "VISA-1111 12/2014 Marc Smith",
                "ProcessorErrorCode": 0,
                "FriendlyUICCMessage": null,
                "TechnicalErrorMessage": null,
                "Amount": 10.0000,
                "Tax": 0.0
            }
        ],
    "TechnicalErrorMessage": null,
    "NewDocumentNumber": null
}


```

Cancels the specified transaction event(s). If no ids are specified, all event sessions on the event will be canceled.

##### Arguments

* items (required) - Array of event session cancellation detail objects. Each object must contain the `id` of an event session registration.
* cancelDate (optional; defaults to current date) - Date for the cancellation. Used for identifying the correct deposit.
* cancellationFee (optional; defaults to `0`) - A fee to apply to the event session cancellation.
* repaymentMethod (required) - Method for repayment. Valid values: `REFUND`, `CREDIT`, `CONVERTTODONATION` or any valid value for the `DDCPAYTYPE` code type.
* isProcessed (optional; defaults to `false`) - Only applicable when `repaymentMethod` is `REFUND` and the original transaction payment was with a `CC`. When `true`, the cancellation will process in StudioEnterprise, but the funds will not be returned to the CC. This should only be used in scenarios where the funds have already been refunded to the CC such as by an external system.

##### Returns

Returns a result object, containing various messages regarding the result of the transaction cancellation.

### Transaction Notes

#### Create a transaction note

```
DEFINITION
POST http://apiserver/transactions/:id/notes

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/104094/notes", {
    "type": "TRANNOTE",
    "shortComment": "This is a special case."
});

EXAMPLE RESPONSE
{
    "id": "4081",
    "type": "TRANNOTE",
    "shortComment": "This is a special case.",
    "longComment": null
}

```

Creates a new transaction note object.

##### Arguments

* type (required) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns a transaction note object if the call succeeded. Returns an error if create parameters are invalid (e.g. specifying an undefined note type).

#### Retrieve a transaction note

```
DEFINITION
GET http://apiserver/transactions/:id/notes/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/104094/notes/4081");

EXAMPLE RESPONSE
{
    "id": "4081",
    "type": "TRANNOTE",
    "shortComment": "This is a special case.",
    "longComment": null
}

```

Retrieves the details of an existing transaction note. You need only supply the transaction note id.

##### Arguments

* id (required) - The id of the transaction note to retrieve.

##### Returns

Returns a transaction note object if a valid id was provided.

#### Update a transaction note

```
DEFINITION
POST http://apiserver/transactions/:id/notes/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/104094/notes/4081", {
    "shortComment": null,
    "longComment": "This is a special case."
});

EXAMPLE RESPONSE
{
    "id": "4081",
    "type": "TRANNOTE",
    "shortComment": null,
    "longComment": "This is a special case."
}


```

Updates the specified transaction note by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* type (optional) - The note type. Must be a defined note type.
* shortComment (optional) - The short comment of the note.
* longComment (optional) - The long comment of the note.

##### Returns

Returns the transaction note object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined note type or note type value).

#### Delete a transaction note

```
DEFINITION
DELETE http://apiserver/transactions/:id/notes/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/104094/notes/4081", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a transaction note. It cannot be undone.

##### Arguments

* id (required) - The id of the transaction note to be deleted.

##### Returns

Returns a 204 No Content response on success. If the transaction note id does not exist, this call returns an error.

#### List all transaction notes

```
DEFINITION
GET http://apiserver/transactions/:id/notes

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/104094/notes");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "4081",
            "type": "TRANNOTE",
            "shortComment": "This is a special case.",
            "longComment": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all notes for the specified transaction.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction notes, starting at index offset. Each entry in the array is a separate transaction note. If no more transaction notes are available, the resulting array will be empty. This request should never return an error.

### Transaction Orders

#### Create a transaction order

```
DEFINITION
POST http://apiserver/transactions/:id/orders

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/orders", {
    "warehouse": "UKWH",
    "shippingMethod": "2DAY",
    "shippingAmount": 15.50,
    "salesTaxAmount1" : 5.40,
    "salesTaxAmount2" : 1.20,
    "salesTaxAmount3" : 0.80,
    "details": [
        {...},
        {...}
    ],
    "response": {
        "letter": "ORDER"
    }
});

EXAMPLE RESPONSE
{
    "id": "7255",
    "address": "230529",
    "warehouse": "UKWH",
    "shippingMethod": "2DAY",
    "shippingTotal": 15.50,
    "salesTaxAmount1" : 5.40,
    "salesTaxAmount2" : 1.20,
    "salesTaxAmount3" : 0.80,
    "salesTaxAmount4" : 0,
    "salesTaxAmount5" : 0,
    "response": {
        "letter": "ORDER",
        "inserts": []
    },
    "handling": null,
    "comment": null,
    "needBy": null
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction order can only be created as part of a transaction create POST.

##### Arguments

* warehouse (required) - The warehouse code of the transaction order.
* shippingMethod (required) - The shipping method of the transaction order.
* shippingAmount (optional) - The shipping amount of the transation order. If `shippingAmount` is not provided or is `null`, then the shipping amount will be calculate based on the `shippingMethod`.
* salesTaxAmount1-5 (optional) - The five sales tax buckets of the transation order. If `salesTaxAmount1` is not provided or is `null`, then sales tax will be calculate based on the product category and the tax region of the shipping address postal code.
* taxArea (optional) - The tax area used for sales tax. If `taxArea` is not provided or is `null`, then `taxArea` will be defaulted based on the shipping address.
* details (required) - An array of one or more transaction order detail objects. See [transaction order detail](#create-a-transaction-order-detail) for required fields.
* response (optional) - The response object of the transaction order.
* account (optional) - The 2nd party account number for this order. If not specified, the order is for the account set on the transaction header.
* address (optional) - When specifying an account on the order header, `address` must be a valid address id for the 2nd party account. When not specifying an account on the order header, `address` must be a valid address id for the account on the transaction header. If not specified, the order's ship-to address will be the primary address of the account set on the transaction header.
* handling (optional) - The handling code of the transaction order.
* comment (optional) - The comment of the transaction order.
* needBy (optional) - The date by which the transaction order is needed.

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction order

```
DEFINITION
GET http://apiserver/transactions/:id/orders/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/orders/7255");

EXAMPLE RESPONSE
{
    "id": "7255",
    "address": "230529",
    "warehouse": "UKWH",
    "shippingMethod": "2DAY",
    "shippingAmount": 15,
    "handling": null,
    "comment": null,
    "needBy": null
}

```

Retrieves the details of an existing transaction order. You need only supply the transaction order id.

##### Arguments

* id (required) - The id of the transaction order to retrieve.

##### Returns

Returns a transaction order object if a valid id was provided.

#### Update a transaction order

```
DEFINITION
POST http://apiserver/transactions/:id/orders/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/orders/7255", {
    "needBy": "2013-04-03"
});

EXAMPLE RESPONSE
{
    "id": "7255",
    "address": "230529",
    "warehouse": "UKWH",
    "shippingMethod": "2DAY",
    "shippingAmount": 15,
    "handling": null,
    "comment": null,
    "needBy": "2013-04-03"
}


```

Updates the specified transaction order by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction order object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined transaction order type code).

#### Delete a transaction order

```
DEFINITION
DELETE http://apiserver/transactions/:id/orders/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/25445/orders/7255", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a transaction order. It cannot be undone.

##### Arguments

* id (required) - The id of the transaction order to be deleted.

##### Returns

Returns a 204 No Content response on success. If the transaction order id does not exist, this call returns an error.

#### List all transaction orders

```
DEFINITION
GET http://apiserver/transactions/:id/orders

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83324/orders");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "7231",
            "account": "16230",
            "address": "1000015850",
            "warehouse": "10",
            "shippingMethod": null,
            "shippingAmount": 0,
            "taxArea": null,
            "salesTaxAmount1": 0,
            "salesTaxAmount2": 0,
            "salesTaxAmount3": 0,
            "salesTaxAmount4": 0,
            "salesTaxAmount5": 0,
            "handlingCode": null,
            "needBy": null,
            "response": {
                "id": 307575,
                "type": "ORDER",
                "method": null,
                "status": "P",
                "profileGroup": 2720,
                "printGroup": 3427,
                "printDate": null,
                "orderId": 7231,
                "addressLine1": "1234 Gondola Way",
                "letter": "PACU"
            },
            "shipment": {
                "method": "FEDEX",
                "amount": 6.4,
                "trackingNumber": null,
                "group": "654",
                "date": "2014-08-22"
            }
        },
        {...},
        {...}
    ]
}

```

Returns a list of all orders for the specified transaction.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction orders, starting at index offset. Each entry in the array is a separate transaction order. If no more transaction orders are available, the resulting array will be empty. This request should never return an error.

#### Cancel/Return products in an order

```
DEFINITION
POST http://apiserver/transactions/:id/orders/cancel

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/174836/orders/cancel", {
    items: [
        {
            id: "107532",
            quantity: 1,
            shippingAmount: 1.90
        },
        {
            id: "107530",
            quantity: 1,
            shippingAmount: 2
        }
    ],
    cancelDate: "2014-12-08",
    repaymentMethod: "REFUND"
});

EXAMPLE RESPONSE
{
    "Success": true,
    "FriendlyUIMessage": null,
    "AdditionalUIMessages": [],
    "CCResult": [
        {
            "Success": true,
            "ReferenceNumber": "VISA-1111 12/2014 Marc Smith",
            "ProcessorErrorCode": 0,
            "FriendlyUICCMessage": null,
            "TechnicalErrorMessage": null,
            "Amount": 11.99,
            "Tax": 0.0
        }
    ],
    "TechnicalErrorMessage": null,
    "NewDocumentNumber": null
}


```

Cancels the specified products(s). If no ids are specified, all products on the transaction will be canceled.

##### Arguments

* items (required) - Array of order detail cancellation objects. Each object must contain the `id` of the order detail to return as well as the `quantity` and `shippingAmount`.
* cancelDate (optional; defaults to current date) - Date for the cancellation. Used for identifying the correct deposit.
* repaymentMethod (required) - Method for repayment. Valid values: `REFUND`, `CREDIT`, `CONVERTTODONATION` or any valid value for the `DDCPAYTYPE` code type.
* isProcessed (optional; defaults to `false`) - Only applicable when `repaymentMethod` is `REFUND` and the original transaction payment was with a `CC`. When `true`, the cancellation will process in StudioEnterprise, but the funds will not be returned to the CC. This should only be used in scenarios where the funds have already been refunded to the CC such as by an external system.

##### Returns

Returns a result object, containing various messages regarding the result of the transaction cancellation.

### Transaction Order Details

#### Create a transaction order detail

```
DEFINITION
POST http://apiserver/transactions/:id/orders/:id/details

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/orders/7255/details", {
    "product": "BK-5SLVG",
    "quantity": 1,
    "priceCode": "B",
    "price": 25,
    "source": "AD1D2234A"
});

EXAMPLE RESPONSE
{
    "id": "47901",
    "product": "BK-5SLVG",
    "quantity": 1,
    "priceCode": "B",
    "price": 25,
    "expenseType": "B",
    "source": "AD1D2234A",
    "discount": null,
    "shortComment": null
}

```

Creates a new transaction order detail object.

##### Arguments

* product (required) - The product code of the transaction order detail.
* quantity (required) - The quantity of the transaction order detail.
* priceCode (required) - The price code of the transaction order detail. Must be a defined price code for products.
* price (required) - The price per each product of the transaction order detail.
* expenseType (required) - The expense type of the transaction order detail. Must be a valid expense type if the amount is 0, otherwise can be null.
* source (required) - The source code of the transaction order detail.
* discount (optional) - The discount of the transaction order detail.
* status (optional) - The status of the transaction order detail.
* fairMarketValue (optional) - The fair market value of the transaction order detail.
* cost (optional) - The cost of the transaction order detail.
* commitDate (optional) - The commit date of the transaction order detail.
* backorderDate (optional) - The backorder date of the transaction order detail.
* cancelDate (optional) - The cancel date of the transaction order detail.
* returnDate (optional) - The return date of the transaction order detail.
* isSuggestedDonation (optional) - Whether or not the transaction order detail was created from a suggested donation.
* shortComment (optional) - The short comment of the transaction order detail.

##### Returns

Returns a transaction order detail object if the call succeeded. Returns an error if create parameters are invalid (e.g. failing to specify a quantity or a defined fulfillment activity).

#### Retrieve a transaction order detail

```
DEFINITION
GET http://apiserver/transactions/:id/orders/:id/details/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/orders/7255/details/47901");

EXAMPLE RESPONSE
{
    "id": "47901",
    "product": "BK-5SLVG",
    "quantity": 1,
    "priceCode": "B",
    "price": 25,
    "expenseType": "B",
    "discount": null,
    "shortComment": null,
    "status": "C",
    "fairMarketValue": 25,
    "cost": 0,
    "commitDate": null,
    "backorderDate": null,
    "cancelDate": null,
    "returnDate": null,
    "isSuggestedDonation": false,
    "source": "AD1D2234A"
}

```

Retrieves the details of an existing transaction order detail. You need only supply the transaction order detail id.

##### Arguments

* id (required) - The id of the transaction order detail to retrieve.

##### Returns

Returns a transaction order detail object if a valid id was provided.

#### Update a transaction order detail

```
DEFINITION
POST http://apiserver/transactions/:id/orders/:id/details/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/orders/7255/details/47901", {
    "quantity": 2
});

EXAMPLE RESPONSE
{
    "id": "47901",
    "product": "BK-5SLVG",
    "quantity": 2,
    "priceCode": "B",
    "price": 25,
    "expenseType": "B",
    "discount": null,
    "shortComment": null,
    "status": "C",
    "fairMarketValue": 25,
    "cost": 0,
    "commitDate": null,
    "backorderDate": null,
    "cancelDate": null,
    "returnDate": null,
    "isSuggestedDonation": false,
    "source": "AD1D2234A"
}


```

Updates the specified transaction order detail by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Returns

Returns the transaction order detail object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined fulfillment activity or shipping method).

#### Delete a transaction order detail

```
DEFINITION
DELETE http://apiserver/transactions/:id/orders/:id/details/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/25445/orders/7255/details/47901", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a transaction order detail. It cannot be undone.

##### Arguments

* id (required) - The id of the transaction order detail to be deleted.

##### Returns

Returns a 204 No Content response on success. If the transaction order detail id does not exist, this call returns an error.

#### List all transaction order details

```
DEFINITION
GET http://apiserver/transactions/:id/orders/:id/details

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83324/orders/7231/details");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "66962",
            "product": "BK-ATC",
            "productDescription": "Alone In The Crowd",
            "quantity": 1,
            "priceCode": "RP",
            "price": 0,
            "source": "PH8002013",
            "sourceDescription": "800 Phone Line - 2013",
            "elementGroup": "TS04ABP",
            "elementGroupDescription": null,
            "discount": 0,
            "shortComment": null,
            "status": "S",
            "fairMarketValue": 4,
            "cost": 4.75,
            "commitDate": "2014-08-22",
            "backorderDate": null,
            "cancelDate": null,
            "returnDate": null,
            "expenseType": "P",
            "isSuggestedDonation": false,
            "response": 307575,
            "quantityReturned": 2,
            "shippingAmountReturned": 5.00,
            "discountCategory": null
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction order details.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction order details, starting at index offset. Each entry in the array is a separate transaction order detail object. If no more transaction order details are available, the resulting array will be empty. This request should never return an error.

### Transaction Payments

#### Create a transaction payment

```
DEFINITION
POST http://apiserver/transactions/:id/payments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/payments", {
    "type": "CA",
    "amount": 1739,
    "paymentOrigin": "SE"
});

EXAMPLE RESPONSE
{
    "id": "2026590",
    "type": "CA",
    "amount": 1739,
    "merchant": "DDC",
    "remark": null,
    "deposit": "0",
    "depositStatus": "Y"
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction payment can only be created as part of a transaction create POST.

##### Arguments

* type (required) - The payment type of the transaction payment.
* amount (required) - The amount of the transaction payment.
* remark (optional) - The remark of the transaction payment.
* saveForLater (optional) - If type is `CC` or `EFT` then true will save the payment for later.
* useAsPrimary (optional) - If type is `CC` or `EFT` and 'saveForLater' is true, then true will save the payment as the new primary.
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.

##### Additional arguments if type is `CC`

* cardNumber (required) - The card number of the transaction payment.
* cardName (required) - The card name of the transaction payment.
* expMonth (required) - The expiration month of the transaction payment.
* expYear (required) - The expiration year of the transaction payment.
* cvv (required) - The cvv of the transaction payment.

##### Additional arguments if type is `EFT`

* accountNumber (required) - The account number of the transaction payment.
* routingNumber (required) - The routing number of the transaction payment.
* accountType (required) - The account type of the transaction payment. Must be either `CHECKING` or `SAVINGS`

##### Additional arguments if type is `CK`

* checkNumber (required) - The check number of the transaction payment.

##### Additional arguments if type is `GCR`

* cardNumber (required) - The card number of the transaction payment.
* pin (required) - The pin of the transaction payment.

##### Additional arguments if type is `GL` (and control record `INTRCMPMOD` has value `F02AI`)

* glAccount (required) - The accounting instruction detail sub code of the transaction payment.

##### Additional arguments if type is `GL` (and control record `INTRCMPMOD` has value `X02CODES`)

* glSegment1 (required) - The first GL segment of the transaction payment.
* glSegment2 (optional) - The second GL segment of the transaction payment. Cannot be provided if the first is not provided.
* glSegment3 (optional) - The third GL segment of the transaction payment. Cannot be provided if the second is not provided.
* glSegment4 (optional) - The fourth GL segment of the transaction payment. Cannot be provided if the third is not provided.
* glSegment5 (optional) - The fifth GL segment of the transaction payment. Cannot be provided if the fourth is not provided.

##### Returns

405 Not Allowed. (see note above)

#### Create an already deposited CC transaction

```
DEFINITION
POST http://apiserver/transactions/:id/payments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/payments", {
    "type":"CC",
    "amount":39.72,
    "cardNumber":"4444xxxxxxxx1111",
    "expMonth":"01",
    "expYear":"2018",
    "cardName":"Dave Duncan",
    "isProcessed": true,
    "token": "120492895923",
    "saveForLater": false,
    "paymentOrigin": "SE"
});

EXAMPLE RESPONSE
{
    "id": "464627",
    "type": "CC",
    "amount": 39.72,
    "merchant": "BLUE",
    "cardNumber": "VISA-1111",
    "cardName": "Dave Duncan",
    "expMonth": "01",
    "expYear": "2018",
    "cvv": null,
    "token": "120492895923",
    "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
    "deposit": "4641",
    "depositStatus": "C",
    "depositDate": "2016-03-01",
    "savedPaymentId": 0,
    "savedPaymentReferenceNumber": null
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction payment can only be created as part of a transaction create POST.

When creating an already deposited CC transaction through the API, the date of the deposit will be the same as the transaction date. The transaction date is determined by the date of the transaction's `batch`.

##### Arguments

* type (required) - `CC`
* isProcessed (required) - `true`
* token (required) - The transaction id returned by the payment gateway when the CC funds were captured
* amount (required) - The amount of the transaction payment
* cardNumber (required) - The card card number mask
* cardName (required) - The name on card
* expMonth (required) - Expiration month
* expYear (required) - Expiration year
* cvv (optional) - The cvv of the transaction payment
* saveForLater (optional) - If type is `CC` or `EFT` then true will save the payment for later
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.

##### Returns

405 Not Allowed. (see note above)

#### Create a transaction using an EFT token

```
DEFINITION
POST http://apiserver/transactions/:id/payments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/payments", {
    "amount":39.72,
    "type":"EFT",
    "accountNumber":"xxxxxxxx1321",
    "accountType":"CHECKING",
    "token":"000000201041",
    "saveForLater": false
});

EXAMPLE RESPONSE
{
    "id": "464629",
    "type": "EFT",
    "amount": 39.72,
    "merchant": "BLUE",
    "routingNumber": "xxxxxxxxx",
    "accountNumber": "xxxxxxxx1321",
    "accountType": "CHECKING",
    "token": "000000201041",
    "referenceNumber": "xxxxxxxx1321-C",
    "deposit": "0",
    "depositStatus": "F",
    "depositDate": null,
    "savedPaymentId": 0,
    "savedPaymentReferenceNumber": null
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction payment can only be created as part of a transaction create POST.

##### Arguments

* amount (required) - The amount of the transaction payment
* type (required) - `EFT`
* accountNumber (required) - mask of bank account number
* accountType (required) - `CHECKING` or `SAVINGS`
* token (required) - The token returned by the payment gateway when the EFT information was tokenized

##### Returns

405 Not Allowed. (see note above)

#### Create a transaction using a hosted payment page token

```
DEFINITION
POST http://apiserver/transactions/:id/payments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/payments", {
    "hostedPageToken": "1234567890",
    "cardName": "Dave Duncan,
    "type": "CC"
});

EXAMPLE RESPONSE
{
    "id": "464627",
    "type": "CC",
    "amount": 39.72,
    "merchant": "BLUE",
    "cardNumber": "VISA-1111",
    "cardName": "Dave Duncan",
    "expMonth": "01",
    "expYear": "2018",
    "cvv": null,
    "token": "120492895923",
    "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
    "deposit": "4641",
    "depositStatus": "C",
    "depositDate": "2016-03-01",
    "savedPaymentId": 0,
    "savedPaymentReferenceNumber": null
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction payment can only be created as part of a transaction create POST.

##### Arguments

If payment `type` is `CC`, then provide:

* hostedPageToken - the hosted payment page token returned by the payment gateway
* cardName - the name on card

##### Returns

405 Not Allowed. (see note above)

#### Create a transaction using a saved payment

```
DEFINITION
POST http://apiserver/transactions/:id/payments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/payments", {
    "savedPaymentId":10
});

EXAMPLE RESPONSE
{
    "id": "464629",
    "type": "EFT",
    "amount": 39.72,
    "merchant": "BLUE",
    "routingNumber": "xxxxxxxxx",
    "accountNumber": "xxxxxxxx1321",
    "accountType": "CHECKING",
    "token": "000000201041",
    "referenceNumber": "xxxxxxxx1321-C",
    "deposit": "0",
    "depositStatus": "F",
    "depositDate": null,
    "savedPaymentId": 10,
    "savedPaymentReferenceNumber": "xxxxxxxx1321-C"
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction payment can only be created as part of a transaction create POST.

##### Arguments

* savedPaymentId - The id of the saved payment to use for the transaction

##### Returns

405 Not Allowed. (see note above)

#### Create an On Hold transaction with a tokenized CC/EFT payment

```
DEFINITION
POST http://apiserver/transactions/:id/payments

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184698/payments", {
    "type":"CC",
    "amount":39.72,
    "cardNumber":"4xxxxxxxxxxx1111",
    "expMonth":"01",
    "expYear":"2018",
    "cardName":"Dave Duncan",
    "token": "120492895432",
    "paymentOrigin": "SE"
});

EXAMPLE RESPONSE
{
    "id": "464645",
    "type": "CC",
    "amount": 39.72,
    "merchant": "BLUE",
    "cardNumber": "VISA-1111",
    "cardName": "Dave Duncan",
    "expMonth": "01",
    "expYear": "2018",
    "cvv": null,
    "token": "120492895432",
    "referenceNumber": "VISA-1111 01/2018 Dave Duncan",
    "deposit": "0",
    "depositStatus": "H",
    "depositDate": null,
    "savedPaymentId": null,
    "savedPaymentReferenceNumber": null
}


EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184699/payments", {
    "type":"EFT",
    "amount":39.72,
    "accountNumber": "xxxxx3123",
    "accountType": "SAVINGS",
    "token": "120492805433"
});

EXAMPLE RESPONSE
{
    "id": "464645",
    "type": "EFT",
    "amount": 39.72,
    "merchant": "BLUE",
    "routingNumber": "xxxxxxxxx",
    "accountNumber": "xxxxx3123",
    "accountType": "SAVINGS",
    "token": "120492805433",
    "referenceNumber": "xxxxx3123-S",
    "deposit": "0",
    "depositStatus": "H",
    "depositDate": null,
    "savedPaymentId": null,
    "savedPaymentReferenceNumber": null
}


```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction payment can only be created as part of a transaction create POST.

When a CC/EFT token is already known (tokenized outside of StudioEnterprise) and if the transaction being created is on hold `"status": "H"`, then the token will NOT be charged and the transaction deposits will also remain on hold. Later, when the transaction is released, the CC/EFT token that was provided will be charged.

##### Arguments

Credit Card

* type (required) - `CC`
* token (required) - The tokenized CC
* amount (required) - The amount of the transaction payment
* cardNumber (required) - The card card number mask
* cardName (required) - The name on card
* expMonth (required) - Expiration month
* expYear (required) - Expiration year
* paymentOrigin (optional) - Used to communicate to the payment gateway whether this payment is used for a Web transaction. Current values are `ASO` (for Web transactions) and `SE` for all others.

EFT

* type (required) - `EFT`
* token (required) - The tokenized EFT
* amount (required) - The amount of the transaction payment
* accountNumber (required) - The EFT bank account mask
* routingNumber - Do not provide a value since the EFT has been tokenized
* accountType (required) - `CHECKING` or `SAVINGS`

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction payment

```
DEFINITION
GET http://apiserver/transactions/:id/payments/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/payments/2026590");

EXAMPLE RESPONSE
{
    "id": "2026590",
    "type": "CA",
    "amount": 1739,
    "merchant": "DDC",
    "remark": null,
    "deposit": "0",
    "depositStatus": "Y",
    "digitalWalletCode": null,
    "digitalWalletDescription": null,
    "formattedBillingAddress": "2435 N. Central Expressway, Ste. 950, Richardson, TX, 75080",
    "billingAddress": {
        "line1": "2435 N. Central Expressway",
        "line2": "Ste. 950",
        "line3": null,
        "line4": null,
        "city": "Richardson",
        "state": "TX",
        "stateDescription": "Texas",
        "postalCode": "75080",
        "country": "USA",
        "countryDescription": "United States of America"
    }
}

```

Retrieves the details of an existing transaction payment. You need only supply the transaction payment id.

##### Arguments

* id (required) - The id of the transaction payment.

##### Returns

Returns a transaction payment object if a valid id was provided.

#### Update a transaction payment

```
DEFINITION
POST http://apiserver/transactions/:id/payments/:paymentId

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/184688/payments/2026590", {
    "remark": "Payment made in-person"
});

EXAMPLE RESPONSE
{
    "id": "2026590",
    "type": "CA",
    "amount": 1739,
    "merchant": "DDC",
    "remark": "Payment made in-person",
    "deposit": "0",
    "depositStatus": "Y"
}


```

Updates the specified transaction payment by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* id (required) - The id of the transaction to update a payment detail for.
* paymentId (required) - The id of the transaction payment to update.

##### Returns

Returns the transaction payment object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined type).

#### Delete a transaction payment

```
DEFINITION
DELETE http://apiserver/transactions/:id/payments/:paymentId

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/184688/payments/2026590", { type: "DELETE" });

EXAMPLE
204 No Content

```

Permanently deletes a transaction payment. It cannot be undone.

##### Arguments

* id (required) - The id of the transaction to delete a payment detail from.
* paymentId (required) - The id of the transaction payment to be deleted.

##### Returns

Returns a 204 No Content response on success. If the transaction payment id does not exist, this call returns an error.

#### List all transaction payments

```
DEFINITION
GET http://apiserver/transactions/:id/payments

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/184688/payments");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "2026590",
            "type": "CA",
            "amount": 1739,
            "merchant": "DDC",
            "remark": "Payment made in-person",
            "deposit": "0",
            "depositStatus": "Y",
            "digitalWalletCode": null,
            "digitalWalletDescription": null,
            "formattedBillingAddress": "2435 N. Central Expressway, Ste. 950, Richardson, TX, 75080",
            "billingAddress": {
                "line1": "2435 N. Central Expressway",
                "line2": "Ste. 950",
                "line3": null,
                "line4": null,
                "city": "Richardson",
                "state": "TX",
                "stateDescription": "Texas",
                "postalCode": "75080",
                "country": "USA",
                "countryDescription": "United States of America"
            }
        },
        {...},
        {...}
    ]
}

```

Returns a list of all transaction payments.

##### Arguments

* id (required) - The id of the transaction to retrieve payment details for.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction payments, starting at index offset. Each entry in the array is a separate transaction payment object. If no more transaction payments are available, the resulting array will be empty. This request should never return an error.

### Transaction Responses (read only collection)

#### List all transaction responses

```
DEFINITION
GET http://apiserver/transactions/:id/responses

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83309/responses");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 4
    },
    "items": [
        {
            "responseId": 307552,
            "communicationType": "RECEIPT",
            "responseMethod": null,
            "status": "H",
            "profileGroup": null,
            "printGroup": null,
            "printDate": null,
            "orderId": null,
            "addressLine1": "1234 North Lights Way",
            "letter": "0613APPLNO",
            "paragraphs": [
                {
                    "id": 123231,
                    "type": "ABC",
                    ""
                }
            ]
        },
        {...},
        {...}
    ]
}

```

Returns a list of all responses for the specified transaction.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction responses, starting at index offset. Each entry in the array is a separate transaction responses. If no more transaction responses are available, the resulting array will be empty. This request should never return an error.

### Transaction Subscriptions

#### Create a transaction subscription

```
DEFINITION
POST http://apiserver/transactions/:id/subscriptions

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/subscriptions", {
    "subscription": "WARK",
    "start": "2010-08-01",
    "source": "11DRA100",
    "response": {
        "letter": "SUBLETTER"
    },
    "priceCode": "ST12",
    "amount": 240,
    "address": 123,
    "salesTaxAmount1":0.12,
    "salesTaxAmount2":0.24,
    "salesTaxAmount3":0.36,
    "salesTaxAmount4":0,
    "salesTaxAmount5":0,
    "taxArea":"TX"
});

EXAMPLE RESPONSE
{
    "id": "751",
    "subscription": "WARK",
    "recipientAccount": "7"
    "status": "P",
    "start": "2010-08-01",
    "copyCount": 1,
    "numberOfIssues": 4,
    "numberRemaining": 4,
    "source": "11DRA100",
    "priceCode": "ST12",
    "amount": 240,
    "response": {
        "letter": "SUBLETTER",
        "inserts": []
    },
    "fulfillmentMethod": "MAIL",
    "address": 123,
    "email": null,
    "remainingDeferredAmount": 240,
    "shortComment": null,
    "cancelReason": null,
    "cancelDate": null,
    "end": null,
    "lastIssue": null,
    "lastDate": null,
    "salesTaxAmount1":0.12,
    "salesTaxAmount2":0.24,
    "salesTaxAmount3":0.36,
    "salesTaxAmount4":0,
    "salesTaxAmount5":0,
    "taxArea":"TX",
    "autoRenew": null,
    "renewalPriceCode": null
}

```

Note: This method cannot be called directly and is shown as above for demonstration purposes only. A transaction subscription can only be created as part of a transaction create POST.

##### Arguments

* subscription (required) - The subscription code. Must be a defined subscription code.
* start (required) - The start date of the transaction subscription.
* copyCount (required) - The copy count of the transaction subscription.
* numberOfIssues (required) - The number of issu
* source (required) - The source code of the transaction subscription.
* priceCode (required) - The price code of the transaction subscription.
* amount (required) - The amount of the transaction subscription.
* recipientAccount (optional) - The account number of the subscriber. Defaults to the account number on the transaction.
* address (optional) - The address id of where the subscription should go. Required if fulfillmentMethod is `MAIL`.
* email (optional) - The email address id of where the subscription should go. Required if fulfillmentMethod is `EMAIL`.
* response (optional) - A response object for the transaction subscription. Must include at least a letter code.
* end (optional) - The end date of the transaction subscription.
* shortComment (optional) - The short comment of the transaction subscription.
* salesTaxAmount1-5 (optional) - The five sales tax buckets of the transation subscription. If `salesTaxAmount1` is not provided or is `null`, then sales tax will be calculate based on the tax region of the recipient address postal code.
* taxArea (optional) - The tax area used for sales tax. If `taxArea` is not provided or is `null`, then `taxArea` will be defaulted based on the recipient address.
* autoRenew (see description) - If the subscription is going to auto-renew. Should be `true` or `false` - if `null` will be defaulted based on the subscription master's `autoRenewDefault`.
* renewalPriceCode (see description) - Should be a valid subscription price code for this auto-renewing subscription - if `null` will be defaulted based on the `priceCode` provided.
* externalId (optional) - An external identifier for the subscription.

##### Returns

405 Not Allowed. (see note above)

#### Retrieve a transaction subscription

```
DEFINITION
GET http://apiserver/transactions/:id/subscriptions/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/25445/subscriptions/751");

EXAMPLE RESPONSE
{
    "id": "751",
    "subscription": "WARK",
    "recipientAccount": "7"
    "status": "P",
    "start": "2010-08-01",
    "copyCount": 1,
    "numberOfIssues": 4,
    "numberRemaining": 4,
    "source": "11DRA100",
    "priceCode": "ST12",
    "amount": 240,
    "response": {
        "letter": "SUBLETTER",
        "inserts": []
    },
    "fulfillmentMethod": "MAIL",
    "address": 123,
    "email": null,
    "remainingDeferredAmount": 240,
    "shortComment": null,
    "cancelReason": null,
    "cancelDate": null,
    "end": null,
    "lastIssue": null,
    "lastDate": null
}

```

Retrieves the details of an existing transaction subscription. You need only supply the transaction subscription id.

##### Arguments

* id (required) - The id of the transaction subscription to retrieve.

##### Returns

Returns a transaction subscription object if a valid id was provided.

#### Update a transaction subscription

```
DEFINITION
POST http://apiserver/transactions/:id/subscriptions/:id

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/25445/subscriptions/751", {
    "source": "AD1D2234A"
});

EXAMPLE RESPONSE
{
    "id": "751",
    "subscription": "WARK",
    "recipientAccount": "7"
    "status": "P",
    "start": "2010-08-01",
    "copyCount": 1,
    "numberOfIssues": 4,
    "numberRemaining": 4,
    "source": "AD1D2234A",
    "priceCode": "ST12",
    "amount": 240,
    "response": {
        "letter": "SUBLETTER",
        "inserts": []
    },
    "fulfillmentMethod": "MAIL",
    "address": 123,
    "email": null,
    "remainingDeferredAmount": 240,
    "shortComment": null,
    "cancelReason": null,
    "cancelDate": null,
    "end": null,
    "lastIssue": null,
    "lastDate": null,
    "autoRenew": null,
    "renewalPriceCode": null,
    "externalId": null
}


```

Updates the specified transaction subscription by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

##### Arguments

* subscription (optional) - The subscription code. Must be a defined subscription code.
* start (optional) - The start date of the transaction subscription.
* source (optional) - The source code of the transaction subscription.
* autoRenew (see description) - If the subscription is going to auto-renew. Should be `true` or `false` - if `null` will be defaulted based on the subscription master's `autoRenewDefault`.
* renewalPriceCode (see description) - Should be a valid subscription price code for this auto-renewing subscription - if `null` will be defaulted based on the `priceCode` provided.
* externalId (optional) - An external identifier for the subscription.

##### Returns

Returns the transaction subscription object if the update succeeded. Returns an error if update parameters are invalid (e.g. specifying an undefined transaction subscription type code).

#### Delete a transaction subscription

```
DEFINITION
DELETE http://apiserver/transactions/:id/subscriptions/:id

EXAMPLE REQUEST
$.ajax("http://localhost:49195/transactions/25445/subscriptions/751", { type: "DELETE" });

EXAMPLE RESPONSE
204 No Content

```

Permanently deletes a transaction subscription. It cannot be undone.

##### Arguments

* id (required) - The id of the transaction subscription to be deleted.

##### Returns

Returns a 204 No Content response on success. If the transaction subscription id does not exist, this call returns an error.

#### List all transaction subscriptions

```
DEFINITION
GET http://apiserver/transactions/:id/subscriptions

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/83309/subscriptions");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1000000104",
            "recipientAccount": "16230",
            "subscription": "CHMPK",
            "status": "P",
            "start": "2014-08-18",
            "copyCount": 1,
            "numberOfIssues": 12,
            "numberRemaining": 12,
            "source": "G12GENERAL",
            "fulfillmentMethod": "MAIL",
            "end": null,
            "priceCode": "1YR",
            "price": 10,
            "remainingDeferredAmount": 10,
            "shortComment": null,
            "cancelDate": null,
            "cancelReason": null,
            "lastIssue": null,
            "lastIssueDate": null,
            "response": {
                "response": 307553,
                "type": "SUBACK",
                "method": null,
                "status": "H",
                "profileGroup": null,
                "printGroup": null,
                "printDate": null,
                "orderId": null,
                "addressLine1": "1234 North Lights Way",
                "letter": "0613APPLNO"
            },
            "recipientAccountName": "Joe Smith",
            "extendedAmount": 10,
            "buyerAccount": "16230",
            "buyerAccountName": "Joe Smith",
            "sourceDescription": "General Source Code",
            "elementGroup": null,
            "elementGroupDescription": null,
            "mediaOutlet": null,
            "willNeverExpire": false,
            "address": null,
            "email": null,
            "taxArea": null,
            "salesTaxAmount1": null,
            "salesTaxAmount2": null,
            "salesTaxAmount3": null,
            "salesTaxAmount4": null,
            "salesTaxAmount5": null,
            "autoRenew": null,
            "renewalPriceCode": null,
            "externalId": "515142"
        },
        {...},
        {...}
    ]
}

```

Returns a list of all subscriptions for the specified transaction.

##### Returns

A dictionary with an items property that contains an array of up to limit transaction subscriptions, starting at index offset. Each entry in the array is a separate transaction subscription. If no more transaction subscriptions are available, the resulting array will be empty. This request should never return an error.

### Transaction Validate For DocumentNumber Entry

```
DEFINITION
GET http://apiserver/transactions/:id/validateForDocumentNumberEntry

EXAMPLE REQUEST
$.get("http://localhost:49195/transactions/230922/validateForDocumentNumberEntry");

EXAMPLE RESPONSE
{
    "account": "16230",
    "status": "H",
    "totalAmount": 116.40
}

```

The primary use case for this resource is for Batch Document Number entry. It validates an existing transaction and returns information to be used on the new transction.

##### Arguments

* id (required) - The id of the transaction to validate for Document Number Entry.

##### Returns

Returns properties that should be set on the new transaction.

### Response Status

* Y () - Ready
* N () - Never
* P () - Printed
* R () - Profiled
* H () - Hold

### Transaction Response Reprint

```
DEFINITION
POST http://apiserver/transactions/:transactionId/response/:id/reprint

EXAMPLE REQUEST
$.post("http://localhost:49195/transactions/241734/response/476970/reprint");

EXAMPLE RESPONSE
204 No Content

```

Updates a transaction response for reprinting. The response for reprinting must be of type 'RECEIPT', and be in status "P", "N", or "C".

##### Returns

Returns a 204 No Content response on success. If the transaction id or response id does not exist, this call returns an error.