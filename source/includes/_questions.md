# Questions

## GET > Get questions and associated multiple choice answers

```shell
curl "https://app.sixpark.com.au/api/v1/questionnaire/questions"
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "data": [
    {
      "id": "tnEKYuedAjPvB",
      "type": "question",
      "attributes": {
        "text": "What is your age?",
        "description": "Generally, younger investors have a...",
        "answers": [
          {
            "id": "AG6DpLkUwLCCNyZRhHEi",
            "text": "18-25 yrs"
          },
          {
            "id": "K/7M/F24W8aMRlymNF3U",
            "text": "36-50 yrs"
          },
          "..."
        ]
      },
      "links": {
        "self": "https://app.sixpark.com.au/api/v1/questionnaire/questions/tnEKYuedAjPvB"
      }
    },
    "..."
  ],
  "links": {
    "self": "https://app.sixpark.com.au/api/v1/questionnaire/questions"
  }
}
```

_Retrieve_ a set of questions and multiple choice answers as per the Six Park questionnaire/risk assessment.

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

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
data | collection | A collection of questions
data[id] | string | Unique identifier for the question object
data[text] | string | The question text
data[description] | string | Context as to why this question is asked
data[answers] | collection | Multiple choice answers associated with the question
data[answers[id]] | string | Unique identifier for the answer object
data[answers[text]] | string | The answer text
links | object | Links to related endpoints
links[self] | string | Link to questions
links[result] | string | The endpoint where to submit answers, and solicit a result


## GET > Retrieve a question and associated multiple choice answers

```shell
curl "https://app.sixpark.com.au/api/v1/questionnaire/questions/:id"
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "data": {
    "id": "tnEKYuedAjPvB",
    "type": "question",
    "attributes": {
      "text": "What is your age?",
      "description": "Generally, younger investors have a...",
      "answers": [
        {
          "id": "AG6DpLkUwLCCNyZRhHEi",
          "text": "18-25 yrs"
        },
        {
          "id": "K/7M/F24W8aMRlymNF3U",
          "text": "36-50 yrs"
        },
        "..."
      ]
    },
    "links": {
      "self": "https://app.sixpark.com.au/api/v1/questionnaire/questions/tnEKYuedAjPvB",
      "related": "https://app.sixpark.com.au/api/v1/questionnaire/questions"
    }
  }
}
```

_Retrieve_ details of a question and multiple choice answers as per the Six Park questionnaire/risk assessment.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/questionnaire/questions/:id`

### Parameters

Not applicable.

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no |

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
data | object | The question object
data[id] | string | Unique identifier for the question object
data[text] | string | The question text
data[description] | string | Context as to why this question is asked
data[answers] | collection | Multiple choice answers associated with the question
data[answers[id]] | string | Unique identifier for the answer object
data[answers[text]] | string | The answer text
links | object | Links to related endpoints
links[related] | string | Link to all questions
links[self] | string | Link to question
