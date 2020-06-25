# Questions

## GET > Get questions and associated multiple choice answers

```shell
curl "https://app.sixpark.com.au/api/v1/questionnaire/questions"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

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
          "id": "4ReX5gCGen2XA13GDQHd",
          "text": "26-35 yrs",
          "description": "Generally, younger investors are considered to have a greater capacity for risk..."
        }
      ],
      "links": {
        "question": "https://..."
      }
    },
    "..."
  ],
  "links": {
    "result": "https://...",
    "next_page": "https://...",
    "previous_page": "https://...",
    "first_page": "https://...",
    "last_page": "https://...",
    "self": "https://..."
  }
```

_Retrieve_ a set of questions and associated answers collection as per the Six Park questionnaire/risk assessment.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/questionnaire/questions`

### URL Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
investor_type | no | string | individual | The investor type to tailor the questionnaire for - one of either [ individual, group ]

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no | 

## GET > Retrieve a question and associated multiple choice answers

```shell
curl "https://app.sixpark.com.au/api/v1/questionnaire/questions/:id"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

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
        "id": "4ReX5gCGen2XA13GDQHd",
        "text": "26-35 yrs",
        "description": "Generally, younger investors are considered to have a greater capacity for risk..."
      }
    ]
  },
  "links": {
    "questions": "https://...",
    "self": "https://..."
  }
```

_Retrieve_ the details of a question.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/questionnaire/questions/:id`

### Parameters

Not applicable.

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no |