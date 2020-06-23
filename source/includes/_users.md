# Users

## POST > Create a new Six Park user

```shell
curl "https://app.sixpark.com.au/api/v1/users"
  -H "Content-Type: application/json"
  -H "Authorization: Bearer <access_token>"
  --data "{\"email\": \"email@email.com\", \"first_name\": \"FirstName\", \"last_name\": \"LastName\", \"phone_number\": \"0410000000\", \"password\": \"my password is strong\", \"terms_accepted\": true, \"newsletter_signup\": true}"

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
      "onboarded": false,
      "links": {
        "performance": "https://..."
      }
    }
  ],
  "authentication": {
    "access_token": "8-2kNsh0CoPn8-_hFVQa5r7W14KqNgdwtwi2j-DAc1I",
    "token_type": "Bearer",
    "expires_in": 194220,
    "refresh_token": "8-2kNsh0CoPn8-_hFVQa5r7W14KqNgdwtwi2j-DAc1I",
    "scope": "read write",
    "created_at": 1592809139
  }
}
```

A successful request to this endpoint will create a Six Park user resource. Once created, the user becomes automatically authorized for your application.

As part of the response, an `authentication` property is returned which includes the `access token` and `refresh token`.

These credentials are to be persisted within your application and associated to the user so they can be used for resource owner authenticated API endpoints.

### HTTP Request

`POST https://app.sixpark.com.au/api/v1/users`

### Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
email | yes | string | `no default` | The user's email
first_name | yes | string | `no default` | The user's first name
last_name | yes | string | `no default` | The user's last name
phone_number | yes | string | `no default` | The user's phone number
password | yes | string | `no default` | A password
terms_accepted | no | boolean | false | Whether the terms have been accepted - one of either [ true, false ]
newsletter_signup | no | boolean | false | Whether to add the user to the Six Park mailing list - one of either [ true, false ]


### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no | 

## GET > Retrieve a user's details

```shell
curl "https://app.sixpark.com.au/api/v1/users/:id"
  -H "Content-Type: application/json"
  -H "Authorization: Bearer <access_token>"
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
      "onboarded": false,
      "links": {
        "performance": "https://..."
      }
    }
  ]
}
```

_Get_ a user's details.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/users/:id`

### Parameters

Parameter | Description
--------- | -----------

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no |