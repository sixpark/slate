# Result

## GET > Get questionnaire result

```shell
echo 'AG6DpLkUwLCCNyZRhHEi,tnEKYuedAjPvBC6EFwAL' | base64

QUc2RHBMa1V3TENDTnlaUmhIRWksdG5FS1l1ZWRBalB2QkM2RUZ3QUwK
```

```shell
curl "https://app.sixpark.com.au/api/v1/questionnaire/results/QUc2RHBMa1V3TENDTnlaUmhIRWksdG5FS1l1ZWRBalB2QkM2RUZ3QUwK"
  --header "Accept: application/json"
  --header "Authorization: Bearer <access_token>"
```

> Incomplete questionnaire error

```json
{
    "code": "bad_request",
    "message": "Bad Request."
}

```
> A successful (200 HTTP status code) example JSON response body:

```json
"data": {
  "id": "QUc2RHBMa1V3TENDTnlaUmhIRWksdG5FS1l1ZWRBalB2QkM2RUZ3QUwK",
  "type": "results",
  "attributes": {
    "name": "Balanced",
    "performance": {
      "window": "3 years",
      "annualised_return_percent": 5.49,
      "negative_years": 4,
      "return_over_cpi_percentage": 4.0
    },
    "descriptions": [
      {
        "type": "composition",
        "description": "This portfolio invests in a diversified portfolio of growth and income ...",
      },
      {
        "type": "rating",
        "description": "We rate this portfolio as \"Medium Risk\". This means...",
      }
    ],
    "categories": [
      {
        "type": "growth",
        "percentage": 50.00
      },
      {
        "type": "defensive",
        "percentage": 50.00
      }
    ],
    "allocations": [
      {
        "name": "Intl Equities (Hedged)",
        "ticker": "VGAD",
        "category_type": "growth",
        "issuer_name": "Vanguard",
        "portfolio_percentage": 10.00,
        "documents": {
          "pds": {
            "content_type": "application/pdf",
            "url": "https://assets.sixpark.com.au/pds/vgad.pdf"
          },
          "fact_sheet": {
            "content_type": "application/pdf",
            "url": "https://assets.sixpark.com.au/factsheets/vgad.pdf"
          }
        }
      },
      "..."
    ],
    "answers": [
      {
        "id": "AG6DpLkUwLCCNyZRhHEi",
        "text": "18-25 yrs",
        "question": {
          "data": {
            "id": "tnEKYuedAjPvB",
            "type": "question",
            "attributes": {
              "text": "What is your age?",
              "description": "Generally, younger investors have a greater appetite for..."
            }
            "links": {
              "self": "http://app.sixpark.com.au/api/v1/questionnaire/questions/tnEKYuedAjPvB",
              "related": "http://app.sixpark.com.au/api/v1/questionnaire/questions"
            }
          }
        }
      },
      {
        "id": "tnEKYuedAjPvBC6EFwAL",
        "text": "$125,000 to $249,999",
        "question": {
          "data": {
            "id": "znEPYuedAjPva",
            "type": "question",
            "attributes": {
              "text": "What is the total value of your liquid assets...",
              "description": "Generally, the greater the liquid assets you have, the more capacity you have to take on risk...",
            },
            "links": {
              "self": "http://app.sixpark.com.au/api/v1/questionnaire/questions/tnEKYuedAjPvBC6EFwAL",
              "related": "http://app.sixpark.com.au/api/v1/questionnaire/questions"
            }
          }
        }
      },
      "..."
    ],
    "conflicts": [
      {
        "text": "It is unusual to seek high-risk investments when...",
        "answers": [
          {
            "id": "EGJkOzOij5PUhMZsjUno",
            "text": "Mostly concerned with potential...",
            "question": {
              "data": {
                "id": "tnEKYuedAjPvB",
                "type": "question",
                "attributes": {
                  "text": "Which statement best describes your primary concern...",
                  "description": "This question helps assess your desire for risk..."
                },
                "links": {
                  "self": "http://app.sixpark.com.au/api/v1/questionnaire/questions/EGJkOzOij5PUhMZsjUno",
                  "related": "http://app.sixpark.com.au/api/v1/questionnaire/questions"
                }
              }
            }
          },
          {
            "id": "QrVhgp9VAw2LOMC7kMPh",
            "text": "I want to play it safe and protect...",
            "question": {
              "data": {
                "id": "tnEKYuedAjPvB",
                "type": "question",
                "attributes": {
                  "text": "Which statement BEST describes your current...",
                  "description": "This question helps assess your desire for risk..."
                },
                "links": {
                  "self": "http://app.sixpark.com.au/api/v1/questionnaire/questions/EGJkOzOij5PUhMZsjUno",
                  "related": "http://app.sixpark.com.au/api/v1/questionnaire/questions"
                }
              }
            },
            "...",
          },
          "...",
        ],
      },
    ],
  },
  "links": {
    "self": "http://app.sixpark.com.au/api/v1/questionnaire/results/QUc2RHBMa1V3TENDTnlaUmhIRWksdG5FS1l1ZWRBalB2QkM2RUZ3QUwK",
    "sign_up": "sign-up"
  }
}
```

_Retrieve_ the Six Park questionnaire/risk assessment result.

The response will reflect back a collection of `answers` as provided by the originating request.

As part of the response, a collection of `conflicts` may be returned. Conflicts _must_ be shown as part of the customer journey and acknowledged or the answer(s) that raised the conflict, changed (until no further conflicts exist).

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/questionnaire/results/:id`

### ID generation

The ID to be sent to the results endpoint is a comma separated Base64 safe encoded string of answer Ids

### Validation

All questions must be answered with no duplicates otherwise a 400 Bad request will be returned.

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no |

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
data | object | The result object
data[id] | string | Unique identifier for the result object
data[type] | string | Type string for the result object
data[attributes[name]] | string | The name of Portfolio - one of [ 'Conservative', 'Conservative Balanced', 'Balanced', 'Balanced Growth', 'Aggressive Growth' ]
data[attributes[performance]] | object | The performance object
data[attributes[performance[window]]] | string | For how many years performance is being reported - one of [ '1 year', '3 years', '5 years' ]
data[attributes[performance[annualised_return_percent]]] | float | Percentage return - precision to 2 decimal places
data[attributes[performance[negative_years]]] | Integer | Average amount of years that will be negative out of 20 years
data[attributes[performance[return_over_cpi_percentage]]] | float | Percentage return over cpi - precision to 2 decimal places
data[attributes[descriptions]] | collection | Portfolio descriptions
data[attributes[descriptions[type]]] | string | The type of the description - one of [ 'composition', 'rating' ]
data[attributes[descriptions[description]]] | string | A description about the related type
data[attributes[categories]] | collection | Portfolio categories
data[attributes[categories[type]]] | string | The category - one of [ 'growth', 'defensive' ]
data[attributes[categories[percentage]]] | float | How much of the Portfolio the category is assigned - precision to 2 decimal places
data[attributes[allocations]] | collection | A collection of equities the Portfolio is comprised of
data[attributes[allocations[name]]] | string | Name of the equity
data[attributes[allocations[ticker]]] | string | The ASX symbol
data[attributes[allocations[category_type]]] | string | The category - one of [ 'growth', 'defensive' ]
data[attributes[allocations[issuer_name]]] | string | The issuer of the ETF
data[attributes[allocations[portfolio_percentage]]] | float | How much of the Portfolio this equity is assigned - precision to 2 decimal places
data[attributes[allocations[documents]]] | object | A collection of financial documents
data[attributes[allocations[documents[pds]]]] | string | The product disclosure statement
data[attributes[allocations[documents[pds[content_type]]]]] | string | The content type of the document
data[attributes[allocations[documents[pds[url]]]]] | string | The link to the document
data[attributes[allocations[documents[fact_sheet]]]] | string | The fact sheet document
data[attributes[allocations[documents[fact_sheet[content_type]]]]] | string | The content type of the document
data[attributes[allocations[documents[fact_sheet[url]]]]] | string | The link to the document
data[attributes[answers]] | collection | The set of answers reflected back as part of the originating request
data[attributes[answers[id]]] | string | Unique identifier for the answer object
data[attributes[answers[text]]] | string | The answer text
data[attributes[answers[question[data[id]]]]] | string | Unique identifier for the question object
data[attributes[answers[question[data[type]]]]] | string | Type string for the question object
data[attributes[answers[question[attributes[text]]]]] | string | The question text
data[attributes[answers[question[attributes[description]]]]] | string | Context as to why this question is asked
data[attributes[answers[question[links]]]] | object | Links related to question
data[attributes[answers[question[links][self]]]] | object | Link to question
data[attributes[answers[question[links][related]]]] | object | Link to all questions
data[attributes[conflicts]] | collection | The set of conflicts that may have arisen from conflicting answers
data[attributes[conflicts[text]]] | string | The conflict text
data[attributes[conflicts[answers]]] | collection | A collection of the conflicted answers
data[attributes[conflicts[answers[id]]]] | string | Unique identifier for the answer object
data[attributes[conflicts[answers[text]]]] | string | The answer text
data[attributes[conflicts[answers[question[id]]]]] | string | Unique identifier for the question object
data[attributes[conflicts[answers[question[text]]]]] | string | The question text
data[attributes[conflicts[answers[question[description]]]]] | string | Context as to why this question is asked
data[attributes[conflicts[answers[question[links]]]]] | object | Links related to question
data[attributes[conflicts[answers[question[links][self]]]]] | object | Link to question
data[attributes[conflicts[asnwers[question[links][related]]]]] | object | Link to all questions
data[links] | object | Links to related endpoints
data[links[sign_up]] | string | Where to submit the result to create a Six Park user and associations
data[links[self]] | string | link to result
