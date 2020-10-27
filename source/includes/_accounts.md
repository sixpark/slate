# Accounts

## GET > Retrieve a user's accounts

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts"
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"

```

> A successful (200 HTTP status code) example JSON response body:

```json
[
  {
    "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
    "display_name": "FirstName LastName",
    "open": false,
    "links": {
      "portfolio": "https://...",
      "self": "https://..."
    }
  },
  "..."
]
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

### 201 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
id | string | Unique identifier for the account object
display_name | string | A display name for this account
open | boolean | Whether this account is open
links | object | Links to related endpoints
links[portfolio] | string | The endpoint where to retrieve details about the portfolio

## POST > Create a new account for a user

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts"
  --request POST
  --header "Accept: application/json"
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Bearer <access_token>"
  --data-urlencode "answers=[X,Y]"

```

> A successful (201 HTTP status code) example JSON response body:

```json
{
  "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
  "display_name": "FirstName LastName",
  "open": false,
  "links": {
    "portfolio": "https://...",
    "user": "https://...",
    "self": "https://..."
  }
}
```

A successful request to this endpoint will create a Six Park account resource and associate it with the resource owner.

This endpoint is flexible in the parameters it accepts and caters for the following scenarios:

* **Create a new account**: a newly created and associated account is returned in the response. The account has no associated result and so the questionnaire must be finished before onboarding can commence.
* **Create a new account and assign a result**: the account has an associated result and onboarding can commence.


### HTTP Request

`POST https://app.sixpark.com.au/api/v1/users/:user_id/accounts`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
answers | no | collection | `no default` | A collection of Six Park answer **ids** as reflected back from the `result` endpoint

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no | 

### 201 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
id | string | Unique identifier for the account object
display_name | string | A display name for this account
open | boolean | Whether this account is open
links | object | Links to related endpoints
links[portfolio] | string | The endpoint where to retrieve details about the portfolio

## POST > Create a new result for an account

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts/:account_id/results"
  --request POST
  --header "Accept: application/json"
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Bearer <access_token>"
  --data-urlencode "answers=[X,Y]"
```

> A successful (201 HTTP status code) example JSON response body:

```json
{
  "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
  "display_name": "FirstName LastName",
  "open": false,
  "links": {
    "portfolio": "https://...",
    "user": "https://...",
    "self": "https://..."
  }
}
```

A successful request to this endpoint will assign a new result to an existing account resource owned by the resource owner.

### HTTP Request

`POST https://app.sixpark.com.au/api/v1/users/:user_id/accounts/:account_id/results`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
answers | yes | collection | `no default` | A collection of Six Park answer **ids** as reflected back from the `result` endpoint

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no | 

### 201 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
id | string | Unique identifier for the account object
display_name | string | A display name for this account
open | boolean | Whether this account is open
links | object | Links to related endpoints
links[portfolio] | string | The endpoint where to retrieve details about the portfolio
links[user] | string | The endpoint where to retrieve details about the user


## GET > Retrieve an account's details

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/accounts/:account_id"
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "id": "5cbcb043-4e20-46d6-9d85-71018debad6c",
  "display_name": "FirstName LastName",
  "open": false,
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

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
id | string | Unique identifier for the account object
display_name | string | A display name for this account
open | boolean | Whether this account is open
links | object | Links to related endpoints
links[portfolio] | string | The endpoint where to retrieve details about the portfolio
links[user] | string | The endpoint where to retrieve details about the user
