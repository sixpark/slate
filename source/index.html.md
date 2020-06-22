---
title: Six Park API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

---

# Basics

> The API base URL:

```
https://app.sixpark.com.au
```

> The API base URL including version:

```
https://app.sixpark.com.au/api/v1
```

Welcome to the Six Park API. You can use this API to access the Six Park API endpoints.

The Six Park API is a [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure) only, [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)ful API, meaning URLs are resource-oriented. 
It returns [JSON](https://www.json.org/json-en.html) encoded responses and uses standard [HTTP response codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) and [OAuth2](https://en.wikipedia.org/wiki/OAuth) for authorisation/authentication.

You must be pre-approved to use the API. You can request approval by emailing [developers@sixpark.com.au](mailto:developers@sixpark.com.au?subject=API%20access).

The API specification version is currently V1 (draft), therefore all endpoints will contain `/api/v1` in the URL path.

We've provided language bindings in Shell but recommend [Postman](https://www.postman.com) and have included a Postman collection with this documentation. You can view Shell code examples in the dark area to the right.

# Authentication

> To authenticate, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Bearer access_token"
```

> Make sure to replace `access token` with the token returned via the client credentials or the modified authorization code flow.

Access to the API is provided via [OAuth2](https://en.wikipedia.org/wiki/OAuth) using the [client credentials](https://tools.ietf.org/html/draft-ietf-oauth-v2-22#section-4.4) flow and a modified [authorization code](https://tools.ietf.org/html/draft-ietf-oauth-v2-22#section-4.1) flow.

Applications that request an access token via the client credentials flow will be granted access to all non-resource owner (user) endpoints.

Applications that have acquired a resource owner access token will be granted access to resource owner (user) endpoints.

Other than Authorization requests, the API expects a valid access token to be included in all othre API requests via a Bearer header:

`Authorization: Bearer access_token`

<aside class="notice">
You must replace <code>access_token</code> with the token returned via the client credentials or the modified authorization code flow.
</aside>

# Errors

> Error API responses may look like this:

```json
{
  "code": "url_invalid",
  "message": "Sorry, that page does not exist.",
  "links": {
    "error_url": "https://..."
  }
}
```

The Six Park API returns standard [HTTP response codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) to indicate the result of an API request.

Some unsuccessful API responses will include a human readable error message as part of the response which may indicate the action required to remedy a subsequent request.

Below is the standard set of HTTP status code summary.

Error Code | Description
---------- | -------
400 | Bad Request - The request is invalid, often due to a missing parameter.
401 | Unauthorized - The access token is missing or invalid.
403 | Forbidden - The access token does not have the permissions to perform the request.
404 | Not Found - The specified resource could not be found.
406 | Not Acceptable - The requested a format that isn't json.
422 | Unprocessable Entity - The request was well-formed but was unable to be completed.
429 | Too Many Requests - The rate at which the API is being accessed is too fast.
500 | Internal Server Error - We had a problem with our application/API. Try again later.
503 | Service Unavailable - We're temporarily offline. Please try again later.

# HATEOAS

> HATEOAS responses may contain links like these:

```json
{
  "..."
  "links": {
    "questionnaire_url": "https://...",
    "results_url": "https://..."
  }
}
```

Where possible, and generally found as part of resource owner (user) responses, the API will adhere to the [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS) REST extension. Clients are strongly encouraged to follow the HATEOAS guidelines to loosly couple their integration to the API.

# Pagination

```shell
curl "https://app.com/api/v1/users?page=1&per_page=100"
  -H "Authorization: Bearer access_token"
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

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | The page number
per_page | 50 | The number of results returned per page

Paginated results will contain at minimum 4 [links](https://tools.ietf.org/html/rfc5988) to related pages, including `next_page`, `previous_page`, `first_page` and `last_page`.


# Rate Limiting

> An example of a HTTP 429 - Too Many Requests JSON response body

```json
{
  "code": "rate_limit_exceeded",
  "message": "Too many requests, too quickly. We recommend an exponential backoff.",
  "links": {
    "error_url": "https://..."
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

<aside>As of 06/2020 the API does not enforce rate limits.</aside>


# Versioning

> The API base URL including version:

```
https://app.sixpark.com.au/api/v1
```

The API specification version is currently V1 (draft), therefore all endpoints will contain `/api/v1` in the URL path.

When backwards-incompatible changes are made to the API, a new version is released.

We consider backwards-<em>compatible</em> changes to include:

* Adding new API resources.
* Adding new optional request parameters to existing API methods.
* Adding new properties to existing responses.
* Changing the order of properties in existing API responses.
* Changing the length or format of object IDs.

# Validation

> The API base URL including version:

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

# Questions

## GET > Get questions and associated muliple choice answers


```shell
curl "https://app.sixpark.com.au/api/v1/questions"
  -H "Authorization: Bearer <access_token>"
```

> The above returns JSON structured like this:

```json
{
  "questions": [
    {
      "id": "tnEKYuedAjPvB",
      "text": "What is your age?",
      "description": "Generally, younger investors have a greater appetite for...",
      "answers": [
        {
          "id": "AG6DpLkUwLCCNyZRhHEi",
          "text": "18-25 yrs",
          "description": "Generally, younger investors are considered to have a greater capacity for risk..."
        },
        {
          "id": "AG6DpLkUwLCCNyZRhHEi",
          "text": "$125,000 to $249,999",
          "description": "Generally, the greater the liquid assets you have..."
        }
      ],
      "links": {
        "question_url": "https://..."
      }
    }
  ],
  "links": {
    "results_url": "https://...",
    "next_page": "https://...",
    "previous_page": "https://...",
    "first_page": "https://...",
    "last_page": "https://..."
  }
```

_Get_ a set of questions and associated answers collection as per the Six Park questionnaire/risk assessment.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/questions`

### URL Parameters

Parameter | Default | Description
--------- | ----------- | -----------
investor_type | individual | The investor type to tailor the questionnaire for - one of either [ individual, group ]
page | 1 | The nth-chunk of `per_page` resources.
per_page | 10 | Include this number of resources in the response.

### Summary

Concept | Value | Description
--------- | ------- | -----------
authenticated | yes | Access is granted via a client credentials access token
paginated | yes | 


## GET > Get a singular question and associated multiple choice answers


```shell
curl "https://app.sixpark.com.au/api/v1/questions/{id}"
  -H "Authorization: Bearer <access_token>"
```

> The above command returns JSON structured like this:

```json
{
  "question": {
    "id": "tnEKYuedAjPvB",
    "text": "What is your age?",
    "description": "Generally, younger investors have a greater appetite for...",
    "answers": [
      {
        "id": "AG6DpLkUwLCCNyZRhHEi",
        "text": "18-25 yrs",
        "description": "Generally, younger investors are considered to have a greater capacity for risk..."
      },
      {
        "id": "AG6DpLkUwLCCNyZRhHEi",
        "text": "$125,000 to $249,999",
        "description": "Generally, the greater the liquid assets you have..."
      }
    ]
  },
  "links": {
    "questions_url": "https://..."
  }
```

_Get_ a singular question and the associated answers collection as per the Six Park questionnaire/risk assessment.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/questions/{id}`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the question

