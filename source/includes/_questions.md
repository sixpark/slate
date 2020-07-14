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
  "questions": [
    {
      "id": "tnEKYuedAjPvB",
      "text": "What is your age?",
      "description": "Generally, younger investors have a greater appetite for...",
      "answers": [
        {
          "id": "AG6DpLkUwLCCNyZRhHEi",
          "text": "18-25 yrs",
        },
        {
          "id": "4ReX5gCGen2XA13GDQHd",
          "text": "26-35 yrs",
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
questions | collection | A collection of questions
questions[id] | string | Unique identifier for the question object
questions[text] | string | The question text
questions[description] | string | Context as to why this question is asked
questions[answers] | collection | Multiple choice answers associated with the question
questions[answers[id]] | string | Unique identifier for the answer object
questions[answers[text]] | string | The answer text
links | object | Links to related endpoints
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
  "question": {
    "id": "tnEKYuedAjPvB",
    "text": "What is your age?",
    "description": "Generally, younger investors have a greater appetite for...",
    "answers": [
      {
        "id": "AG6DpLkUwLCCNyZRhHEi",
        "text": "18-25 yrs",
      },
      {
        "id": "4ReX5gCGen2XA13GDQHd",
        "text": "26-35 yrs",
      }
    ]
  },
  "links": {
    "questions": "https://...",
    "self": "https://..."
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
question | object | The question object
question[id] | string | Unique identifier for the question object
question[text] | string | The question text
question[description] | string | Context as to why this question is asked
question[answers] | collection | Multiple choice answers associated with the question
question[answers[id]] | string | Unique identifier for the answer object
question[answers[text]] | string | The answer text
links | object | Links to related endpoints
links[questions] | string | Link to all questions
