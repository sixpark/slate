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
      "id": "3a8610d7-988f-47f1-9130-6c6662950855",
      "type": "question",
      "attributes": {
        "text": "What is your age?",
        "description": "Generally, younger investors have a...",
        "answers": [
          {
            "id": "edfa8ab2-d35a-448a-b731-f1607396d164",
            "text": "18-25 yrs"
          },
          {
            "id": "e8b6469a-8bf3-4691-90bd-caf197aced3c",
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
    "self": "https://app.sixpark.com.au/api/v1/questionnaire/questions",
    "results": "https://app.sixpark.com.au/api/v1/questionnaire/results/:id"
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
data[type] | string | The resource type - `question`
data[attributes[text]] | string | The question text
data[attributes[description]] | string | Context as to why this question is asked
data[attributes[answers]] | collection | Multiple choice answers associated with the question
data[attributes[answers[id]]] | string | Unique identifier for the answer object
data[attributes[answers[text]]] | string | The answer text
links | object | Links to related endpoints
links[self] | string | Link to questions
links[results] | string | The endpoint where to submit answers, and solicit a result


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
    "id": "3a8610d7-988f-47f1-9130-6c6662950855",
    "type": "question",
    "attributes": {
      "text": "What is your age?",
      "description": "Generally, younger investors have a...",
      "answers": [
        {
          "id": "7cef5e95-6606-4cac-b121-6b99f56cebb4",
          "text": "18-25 yrs"
        },
        {
          "id": "cce4adcf-f91d-40dd-9f44-66a344910778",
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
data[type] | string | The resource type - `question`
data[attributes[text]] | string | The question text
data[attributes[description]] | string | Context as to why this question is asked
data[attributes[answers]] | collection | Multiple choice answers associated with the question
data[attributes[answers[id]]] | string | Unique identifier for the answer object
data[attributes[answers[text]]] | string | The answer text
data[links] | object | Links to related endpoints
data[links[self]] | string | Link to question
data[links[related]] | string | Link to all questions
