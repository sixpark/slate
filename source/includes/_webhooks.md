# Webhooks

[Webhooks](https://en.wikipedia.org/wiki/Webhook) are used as a means of notifying your application that a particular event has occurred.

On successfully creating a Webhook, as part of the response, a `signature_token` property is returned. It is to be persisted and used in the verification process.

Six Park will use this property to compute a SHA256 HMAC of each webhook request body. The computed HMAC is passed as the value of the `X-SixPark-Signature` header.

In turn, this header is used by your application to validate the authenticity and completeness of the request, ie: that it hasn't been tampered with and that it has originated from Six Park.

The verification process matches the creation process:

- Your application will compute the SHA256 HMAC of the un-parsed, raw request body using the `signature_token` property as was returned as part of create webhook response.
- Your application will then compare the computed HMAC and the HMAC from the `X-SixPark-Signature` header. If the values match, the request is complete and valid.

Webhook urls must respond with a `200` HTTP status code on a successful request. Unsuccessful responses will yield up to 5 retries using an exponential backoff strategy.


## POST > Create a new webhook

```shell
curl "https://app.sixpark.com.au/api/v1/webhooks"
  --request POST
  --header "Accept: application/json"
  --header "Content-Type: application/x-www-form-urlencoded"
  --header "Authorization: Bearer <access_token>"
  --data-urlencode "url=https://..."
  --data-urlencode "description=This is my webhook..."

```

> A successful (201 HTTP status code) example JSON response body:

```json
{
  "data": {
    "id": "330acf46d-ce50-4788-a219-1de5ae9ac484",
    "type": "webhook",
    "attributes": {
      "url": "https://...",
      "description": "This is my webhook...",
      "signature_token": "b7bcf4a088215ed9396b07c9e8b931a5697bc0c4"
    },
    "links": {
      "self": "https://app.sixpark.com.au/api/v1/webhooks/30acf46d-ce50-4788-a219-1de5ae9ac484"
    }
  }
}
```

A successful request to this endpoint will create a new Webhook.

### HTTP Request

`POST https://app.sixpark.com.au/api/v1/webhooks`

### FORM Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
url | yes | string | `no default` | The HTTP url where the request will be made
description | yes | string | `no default` | The description of the webhook

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no | 

### 201 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
data[id] | string | Unique identifier for the user object
data[type] | string | The resource type - `webhook`
data[attributes[url]] | string | The HTTP url where the request will be made
data[attributes[description]] | string | The description of the webhook
data[attributes[signature_token]] | string | The signature token used to create the SHA256 HMAC


## GET > Retrieve a webhook

```shell
curl "https://app.sixpark.com.au/api/v1/webhook/:id"
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "data": {
    "id": "330acf46d-ce50-4788-a219-1de5ae9ac484",
    "type": "webhook",
    "attributes": {
      "url": "https://...",
      "description": "This is my webhook...",
      "signature_token": "b7bcf4a088215ed9396b07c9e8b931a5697bc0c4"
    },
    "links": {
      "self": "https://app.sixpark.com.au/api/v1/webhooks/30acf46d-ce50-4788-a219-1de5ae9ac484"
    }
  }
}
```

_Retrieve_ webhook with the given `:id`.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/webhooks/:id`

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
data[id] | string | Unique identifier for the user object
data[type] | string | The resource type - `webhook`
data[attributes[url]] | string | The HTTP url where the request will be made
data[attributes[description]] | string | The description of the webhook
data[attributes[signature_token]] | string | The signature token used to create the SHA256 HMAC


## DELETE > Remove a webhook with the given `:id`.

```shell
curl "https://app.sixpark.com.au/api/v1/webhook/:id"
  --request DELETE
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"
```

> A successful (204 HTTP status code) response will contain no response body.

_Delete_ a webhook.

### HTTP Request

`DELETE https://app.sixpark.com.au/api/v1/webhooks/:id`

### Parameters

Not applicable.

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no |

### 204 HTTP status code properties

Not applicable.


## POST > `{url}`


> A sample JSON encoded response body.

```json
{
  "data": {
    "id": "ecb20ef1-a543-4ae5-9446-0661a882a616",
    "type": "webhook-event",
    "attributes": {
      "even_type": "ACCOUNT_ONBOARDED"
    },
    "relationships": {
      "webhook": {
        "data": {
          "type": "webhook",
          "id": "75fe2702-114a-401c-8a5f-61d9fa15e0eb"
        },
        "links": {
          "related": "https://app.sixpark.com.au/api/v1/webhooks/75fe2702-114a-401c-8a5f-61d9fa15e0eb"
        }
      },
      "account": {
        "data": {
          "type": "account",
          "id": "f11b778a-3c83-43b5-a481-6b46e4d8aabb"
        },
        "links": {
          "related": "https://..."
        }
      }
    }
  }
}
```

`POST` requests containing JSON encoded bodies are made to configured webhook URLs.

### HTTP Request

`POST {url}`

### Event Types

Value | Description
--------- | ------- | -----------
ACCOUNT_OPENED | Account has been opened

### Headers

Name | Value | Description
--------- | ------- | -----------
X-SixPark-Signature | SHA256 HMAC of raw request body | Used to verify the completeness and authenticity of the request

### Body Properties

Property | Type | Description
--------- | ----------- | -----------
data[id] | string | Unique identifier for the user object
data[type] | string | The resource type - `webhook`
data[attributes[url]] | string | The HTTP url where the request will be made
data[attributes[description]] | string | The description of the webhook
data[attributes[signature_token]] | string | The signature token used to create the SHA256 HMAC
