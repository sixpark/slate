# Users

## POST > Create a new user

```shell
curl "https://app.sixpark.com.au/api/v1/users"
  --request POST
  --header "Accept: application/json"
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Bearer <access_token>"
  --data-urlencode "email=email@email.com"
  --data-urlencode "first_name=FirstName"
  --data-urlencode "last_name=LastName"
  --data-urlencode "phone_number=0410000000"
  --data-urlencode "password=my password is strong"
  --data-urlencode "terms_accepted=true"
  --data-urlencode "newsletter_signup=true"
  --data-urlencode "phone_number=0410000000"
  --data-urlencode "'result': { 'answers': ['X','X'], 'conflicts_accepted': true }"

```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "id": "33047f9a-8be9-41e0-82b5-d6f265f69bea",
  "email": "email@email.com",
  "first_name": "FirstName",
  "last_name": "LastName",
  "phone_number": "0410000000",
  "accounts": [
    {
      "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
      "display_name": "FirstName LastName",
      "open": false,
      "links": {
        "portfolio": "https://...",
        "self": "https://..."
      }
    }
  ],
  "authentication": {
    "access_token": "8-2kNsh0CoPn8-_hFVQa5r7W14KqNgdwtwi2j-DAc1I",
    "token_type": "Bearer",
    "expires_in": 194220,
    "refresh_token": "8-2kNsh0CoPn8-_hFVQa5r7W14KqNgdwtwi2j-DAc1I",
    "scope": "users.read",
    "created_at": 1592809139
  },
  "links": {
    "self": "https://..."
  }
}
```

A successful request to this endpoint will create a Six Park user resource. Once created, the user becomes automatically authorized for your application.

As part of the response, an `authentication` property is returned which includes the `access token` and `refresh token`.

These credentials are to be persisted within your application (for the user) so they can be used for resource owner authenticated API endpoints.

This endpoint is flexible in the parameters it accepts and caters for the following scenarios:

* **Create a user**: a newly created and associated account is returned in the response. The account has no associated result and so the questionnaire must be finished before onboarding can commence.
* **Create a user and assign a result to the newly created account**: the account has an associated result and onboarding can commence.

### Validations

Outside of general property validation:

- If the parameter `terms_accepted` is not provided, or provided as `false`, the response will return a HTTP 400 - Bad Request status code.

- If the `result[answers]` parameter is provided and the `result[conflicts_accepted]` is not provided, or provided as `false` and the `result` endpoint returned a hydrated `conflicts` property, the response will return a HTTP 400 - Bad Request status code.


### HTTP Request

`POST https://app.sixpark.com.au/api/v1/users`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
email | yes | string | `no default` | The user's email
first_name | yes | string | `no default` | The user's first name
last_name | yes | string | `no default` | The user's last name
phone_number | yes | string | `no default` | The user's phone number
password | yes | string | `no default` | A password
terms_accepted | no | boolean | false | Whether the terms have been accepted - one of either [ true, false ]
newsletter_signup | no | boolean | false | Whether to add the user to the Six Park mailing list - one of either [ true, false ]
result[answers] | no | collection | `no default` | A collection of Six Park answer **ids** as reflected back from the `result` endpoint
result[conflicts_accepted] | no | boolean | false | If conflicts were returned via the `result` endpoint, whether they were accepted [ true, false ]

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no | 

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
id | string | Unique identifier for the user object
email | string | The user's email
first_name | string | The user's first name
last_name | string | The user's last name
phone_number | string | The user's phone number
accounts | collection | The collection of accounts associated to the user
accounts[id] | string | Unique identifier for the account object
accounts[display_name] | string | A display name for this account
accounts[open] | boolean | Whether this account is open
accounts[links] | object | Links to related endpoints
accounts[links[portfolio]] | string | The endpoint where to retrieve details about the portfolio
authentication | object | The authentication object
authentication[access_token] | string | The access token to include in authorized requests
authentication[token_type] | string | Always `Bearer`
authentication[expires_in] | integer | The number of seconds the access token is valid for
authentication[refresh_token] | string | The refresh token which is exchanged for a new access token
authentication[scope] | string | One or more scopes listed under authentication
authentication[created_at] | integer | the [Unix time](https://en.wikipedia.org/wiki/Unix_time) of when the token was issued


## GET > Retrieve the resource owner's details

```shell
curl "https://app.sixpark.com.au/api/v1/users/me"
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "data": {
    "id": "33047f9a-8be9-41e0-82b5-d6f265f69bea",
    "type": "user",
    "attributes": {
      "email": "email@email.com",
      "first_name": "FirstName",
      "last_name": "LastName",
      "phone_number": "0410000000"
    },
    "links": {
      "self": "https://..."
    }
  }
}
```

_Retrieve_ details of the resource owner.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/users/me`

### Parameters

Not applicable.

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no |

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
id | string | Unique identifier for the user object
type | string | The object type - always `user`
attributes[email] | string | The user's email
attributes[first_name] | string | The user's first name
attributes[last_name] | string | The user's last name
attributes[phone_number] | string | The user's phone number
links | object | Links to related endpoints
