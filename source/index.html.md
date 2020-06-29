---
title: Six Park API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:
  - questions
  - result
  - users
  - accounts
  - portfolio
---

# Basics

> The API base URL:

```
https://app.sixpark.com.au
```

> The API base URL including version (for resource or client credentials authorized endpoints):

```
https://app.sixpark.com.au/api/v1
```

Welcome to the Six Park API. You can use this API to access the Six Park API endpoints.

The Six Park API is a [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure) only, [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)ful API, meaning (generally) URLs are resource-oriented. 
It accepts [form-encoded](https://en.wikipedia.org/wiki/POST_(HTTP)#Use_for_submitting_web_forms) request bodies, returns [JSON](https://www.json.org/json-en.html) encoded responses and uses standard [HTTP response codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), [HTTP headers](https://en.wikipedia.org/wiki/Header_(computing)) and [OAuth2](https://en.wikipedia.org/wiki/OAuth) for authorisation/authentication.

You must be pre-approved to use the API. If you are approved you will be assigned a `client_id` and a `client_secret`, synonymous to a username/password combination, which you will exchange for a client credentials access token to access certain API endpoints.

The API specification version is currently V1, meaning most endpoints will contain `/api/v1` in the URL path.

We've provided language bindings in Shell but recommend [Postman](https://www.postman.com) and have included a Postman collection with this documentation. You can view Shell code examples in the dark area to the right.

# Authentication

> To access authenticated endpoints, add the Authorization header as shown below:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  --header "Authorization: Bearer access_token"
```

> Make sure to replace `access token` with the token returned via the client credentials or the modified authorization code flow.

Access to the API is provided via [OAuth2](https://en.wikipedia.org/wiki/OAuth) using the [client credentials](https://tools.ietf.org/html/draft-ietf-oauth-v2-22#section-4.4) flow and a modified [authorization code](https://tools.ietf.org/html/draft-ietf-oauth-v2-22#section-4.1) flow.

Applications that request an access token via the client credentials flow will be granted access to all non-resource owner (user) endpoints.

Applications that have acquired a resource owner access token will be granted access to resource owner (user) endpoints.

Other than Authorization requests, the API expects a valid access token to be included in all other API requests via a Bearer header:

`Authorization: Bearer access_token`

<aside class="notice">
You must replace <code>access_token</code> with the Bearer token returned via the client credentials or the modified authorization code flow.
</aside>

## POST > Client credentials Bearer access token

```shell
curl "https://app.sixpark.com.au/oauth/token"
  --request POST
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Basic HVnUjFOMWh2aGVYMWxRNkVPeWhqelRCaDdzaS1w"
  --data-urlencode 'grant_type=client_credentials'
```


> A successful (200 HTTP status code) example JSON response body:

```json
{
    "access_token": "8-2kNsh0CoPn8-_hFVQa5r7W14KqNgdwtwi2j-DAb",
    "token_type": "Bearer",
    "expires_in": 7200,
    "scope": "read",
    "created_at": 1592809139
}
```

_Retrieve_ a client credentials (application) access token to authenticate against client credentials API endpoints.

The endpoint accepts one parameter and a [Basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) header which must be in the following format:

`Authorization: Basic <Base64('client_id:client_secret')>`

### HTTP Request

`POST https://app.sixpark.com.au/oauth/token`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
grant_type | yes | string | `no default` | Must be `client_credentials`

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | no | Not authenticated

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
access_token | string | The access token to include in authorized requests
token_type | string | Always `Bearer`
expires_in | integer | The number of seconds the access token is valid for
scope | string | The scopes, either `[ read, write ]`, the access token is/are valid for
created_at | integer | the [Unix time](https://en.wikipedia.org/wiki/Unix_time) of when the token was issued

## POST > Refresh resource owner access token

```shell
curl "https://app.sixpark.com.au/oauth/token"
  --request POST
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Basic HVnUjFOMWh2aGVYMWxRNkVPeWhqelRCaDdzaS1w"
  --data-urlencode 'grant_type=refresh_token'
  --data-urlencode 'refresh_token=<refresh_token>' \
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
    "access_token": "8-2kNsh0CoPn8-_hFVQa5r7W14KqNgdwtwi2j-DAb",
    "token_type": "Bearer",
    "expires_in": 7200,
    "refresh_token": "ik8StCrDnKrI5uLWdxaTx3bOWHIipDnwTl5Pn2ozpRs",
    "scope": "read",
    "created_at": 1592809139
}
```

_Retrieve_ a resource owner access token to authenticate against resource owner API endpoints via a refresh token.

The endpoint accepts two parameters and a [Basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) header which must be in the following format:

`Authorization: Basic <Base64('client_id:client_secret')>`

### HTTP Request

`POST https://app.sixpark.com.au/oauth/token`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
grant_type | yes | string | `no default` | Must be `refresh_token`
refresh_token | yes | string | `no default` | The `refresh_token`

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | yes | Access is granted via [Basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
access_token | string | The access token to include in authorized requests
token_type | string | Always `Bearer`
expires_in | integer | The number of seconds the access token is valid for
refresh_token | string | The refresh token which is exchanged for a new access token
scope | string | The scopes, either `[ read, write ]`, the access token is/are valid for
created_at | integer | the [Unix time](https://en.wikipedia.org/wiki/Unix_time) of when the token was issued

<aside class="notice">
You must replace <code>refresh_token</code> with the refresh token returned via the modified authorization code flow.
</aside>

# Errors

> Error API responses may look like this:

```json
{
  "code": "url_invalid",
  "message": "Sorry, that page does not exist.",
  "links": {
    "error": "https://..."
  }
}
```

The Six Park API returns standard [HTTP response codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) to indicate the result of an API request.

Some unsuccessful API responses will include a human readable error message as part of the response which may indicate the action required to remedy a subsequent request.

Provided is the standard set of HTTP status code:

Error Code | Description
---------- | -------
400 | Bad Request - The request is invalid, often due to a missing parameter.
401 | Unauthorized - The access token is missing or invalid.
403 | Forbidden - The access token does not have the permissions to perform the request.
404 | Not Found - The specified resource could not be found.
406 | Not Acceptable - The requested format was not JSON.
422 | Unprocessable Entity - The request was well-formed but was unable to be completed.
429 | Too Many Requests - The rate at which the API is being accessed is too fast.
500 | Internal Server Error - We had a problem with our application/API. Try again later.
503 | Service Unavailable - We're temporarily offline. Please try again later.

# HATEOAS

> HATEOAS responses may contain links similar to the below:

```json
{
  "..."
  "links": {
    "questions": "https://...",
    "results": "https://..."
  }
}
```

Where possible, the API will adhere to the [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS) REST extension. Clients are strongly encouraged to follow the HATEOAS guidelines to loosely couple their integration to the API.

# Pagination

```shell
curl "https://app.com/api/v1/users?page=1&per_page=100"
  --header "Authorization: Bearer access_token"
```

> An example of an API request using pagination parameters and the response body containing links to related pages

```json
{
  "...",
  "links": {
    "next_page": "https://...",
    "previous_page": "https://...",
    "first_page": "https://...",
    "last_page": "https://..."
  }
}
```

API Endpoints that return a collection of resources will always be paginated. The API will accept the following parameters for these endpoints:

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
page | no | integer | 1 | The page number
per_page | no | integer | 50 | The number of results returned per page

Paginated results will contain at minimum 4 [links](https://tools.ietf.org/html/rfc5988) to related pages, including `next_page`, `previous_page`, `first_page` and `last_page`.


# Rate Limiting

> An example of a HTTP 429 - Too Many Requests JSON response body:

```json
{
  "code": "rate_limit_exceeded",
  "message": "Too many requests, too quickly. We recommend an exponential backoff.",
  "links": {
    "error": "https://..."
  }
}
```

The Six Park API uses [HTTP headers](https://en.wikipedia.org/wiki/Header_(computing)) to communicate rate limits and consumption rates.

Applications should parse and respect the following 3 headers:

Header | Description
---------- | -------
x-rate-limit-limit | the limit on number of request for the endpoint
x-rate-limit-remaining | the number of requests remaining for the rate limit window
x-rate-limit-reset | the [Unix time](https://en.wikipedia.org/wiki/Unix_time) at which the rate limit window is reset

When an application exceeds the rate limit for an endpoint, the API will return a [HTTP 429 - Too Many Requests](https://tools.ietf.org/html/rfc6585) status code and associated response body.

<aside class="notice">As of 06/2020 the API does <strong>not</strong> enforce rate limits.</aside>


# Versioning

> The API base URL including version:

```
https://app.sixpark.com.au/api/v1
```

The API specification version is currently V1, therefore all endpoints will contain `/api/v1` in the URL path.

When backwards-incompatible changes are made to the API, a new version is released.

We consider backwards-<em>compatible</em> changes to include:

* Adding new API resources.
* Adding new optional request parameters to existing API methods.
* Adding new properties to existing responses.
* Changing the order of properties in existing API responses.
* Changing the length or format of object IDs.

# Validation

> An example of a HTTP 422 - Unprocessable Entity JSON response body:

```json
{
  "code": "validation_failed",
  "message": "Validation failed due to ...",
  "errors": [
    {
      "message": "Must be one of ...",
      "field": "type"
    }
  ]
}
```

Resource mutation API requests will trigger resource validations.

For failed requests, the API will return a [HTTP 422 - Unprocessable Entity](https://tools.ietf.org/html/rfc4918) status code and associated body containing a collection of errors.
