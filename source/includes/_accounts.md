# Accounts

## GET > Retrieve a user's accounts

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts"
  --header "Authorization: Bearer <access_token>"

```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
  "display_name": "FirstName LastName",
  "onboarded": false,
  "links": {
    "portfolio": "https://...",
    "self": "https://..."
  }
},
"..."
```

_Retrieve_ a collection of the resource owner's accounts.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/users/:user_id/accounts`

### Parameters

Not Applicable

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no | 

## POST > Create a new account for a user

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts"
  --request POST
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Bearer <access_token>"
  --data-urlencode "answers=[X,Y]"
  --data-urlencode "tripwires_accepted=true"

```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
  "display_name": "FirstName LastName",
  "onboarded": false,
  "links": {
    "portfolio": "https://...",
    "user": "https://...",
    "self": "https://..."
  }
}
```

A successful request to this endpoint will create a Six Park account resource and associate it with the resource owner.

### Validations

Outside of general property validation:

- If the parameter `result[tripwires_accepted]` is not provided, or provided as `false` and the `result` endpoint returned a hydrated `tripwires` property, the response will return a HTTP 400 - Bad Request status code.


### HTTP Request

`POST https://app.sixpark.com.au/api/v1/users`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
answers | yes | collection | `no default` | A collection of Six Park answer **ids** as reflected back from the `result` endpoint
tripwires_accepted | no | boolean | false | If tripwires were returned via the `result` endpoint, whether they were accepted [ true, false ]

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no | 

## POST > Create a new result for an account

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts/:account_id/results"
  --request POST
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Bearer <access_token>"
  --data-urlencode "answers=[X,Y]"
  --data-urlencode "tripwires_accepted=true"

```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
  "display_name": "FirstName LastName",
  "onboarded": false,
  "links": {
    "portfolio": "https://...",
    "user": "https://...",
    "self": "https://..."
  }
}
```

A successful request to this endpoint will create a Six Park account resource associated with the resource owner.

### Validations

Outside of general property validation:

- If the parameter `result[tripwires_accepted]` is not provided, or provided as `false` and the `result` endpoint returned a hydrated `tripwires` property, the response will return a HTTP 400 - Bad Request status code.


### HTTP Request

`POST https://app.sixpark.com.au/api/v1/users`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
answers | yes | collection | `no default` | A collection of Six Park answer **ids** as reflected back from the `result` endpoint
tripwires_accepted | no | boolean | false | If tripwires were returned via the `result` endpoint, whether they were accepted [ true, false ]

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no | 

## GET > Retrieve an account's details

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts/:account_id"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
  "display_name": "FirstName LastName",
  "onboarded": false,
  "links": {
    "portfolio": "https://...",
    "user": "https://...",
    "self": "https://..."
  }
}
```

_Retrieve_ details of an account.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/users/:user_id/accounts/:account_id`

### Parameters

Not applicable.

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no |