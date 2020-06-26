# Result

## GET > Get questionnaire result

```shell
curl "https://app.sixpark.com.au/api/v1/questionnaire/result"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "name": "Balanced",
  "performance": {
    "window": "3 years",
    "annualised_return_percent": 5.49,
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
        "id": "tnEKYuedAjPvB",
        "text": "What is your age?",
        "description": "Generally, younger investors have a greater appetite for...",
        "links": {
          "self": "https://..."
        }
      }
    },
    {
      "id": "tnEKYuedAjPvBC6EFwAL",
      "text": "$125,000 to $249,999",
      "question": {
        "id": "znEPYuedAjPva",
        "text": "What is the total value of your liquid assets...",
        "description": "Generally, the greater the liquid assets you have, the more capacity you have to take on risk...",
        "links": {
          "self": "https://..."
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
            "id": "tnEKYuedAjPvB",
            "text": "Which statement best describes your primary concern...",
            "description": "This question helps assess your desire for risk...",
            "links": {
              "self": "https://..."
            }
          }
        },
        {
          "id": "QrVhgp9VAw2LOMC7kMPh",
          "text": "I want to play it safe and protect...",
          "question": {
            "id": "tnEKYuedAjPvB",
            "text": "Which statement BEST describes your current...",
            "description": "This question helps assess your desire for risk...",
            "links": {
              "self": "https://..."
            }
          }
        },
        "..."
      ]
    },
    "..."
  ],
  "links": {
    "sign_up": "https://...",
    "self": "https://..."
  }
```

_Retrieve_ the Six Park questionnaire/risk assessment result.

The response will reflect back a collection of `answers` as provided by the originating request.

As part of the response, a collection of `conflicts` may be returned. Conflicts _must_ be shown as part of the customer journey and acknowledged or the answer(s) that raised the conflict, changed (until no further conflicts exist).

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/questionnaire/result`

### URL Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
answers | yes | collection | `no default` | A collection of Six Park answer **ids** as returned from the `questions` endpoint

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no | 

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
name | string | The name of Portfolio - one of [ 'Conservative', 'Conservative Balanced', 'Balanced', 'Balanced Growth', 'Aggressive Growth' ]
performance | object | The performance object
performance[window] | string | For how many years performance is being reported - one of [ '1 year', '3 years', '5 years' ]
performance[annualised_return_percent] | float | Percentage return - precision to 2 decimal places
descriptions | collection | Portfolio descriptions
descriptions[type] | string | The type of the description - one of [ 'composition', 'rating' ]
descriptions[description] | string | A description about the related type
categories | collection | Portfolio categories
categories[type] | string | The category - one of [ 'growth', 'defensive' ]
categories[percentage] | float | How much of the Portfolio the category is assigned - precision to 2 decimal places
allocations | collection | A collection of equities the Portfolio is comprised of
allocations[name] | string | Name of the equity
allocations[ticker] | string | The ASX symbol
allocations[category_type] | string | The category - one of [ 'growth', 'defensive' ]
allocations[provider_name] | string | The issuer of the ETF
allocations[portfolio_percentage] | float | How much of the Portfolio this equity is assigned - precision to 2 decimal places
documents | object | A collection of financial documents
documents[pds] | string | The product disclosure statement
documents[pds[content_type]] | string | The content type of the document
documents[pds[url]] | string | The link to the document
documents[fact_sheet] | string | The fact sheet document
documents[fact_sheet[content_type]] | string | The content type of the document
documents[fact_sheet[url]] | string | The link to the document
answers | collection | The set of answers reflected back as part of the originating request
answers[id] | string | Unique identifier for the answer object
answers[text] | string | The answer text
answers[question[id]] | string | Unique identifier for the question object
answers[question[text]] | string | The question text
answers[question[description]] | string | Context as to why this question is asked
answers[question[links]] | object | Links to related endpoints
conflicts | collection | The set of conflicts that may have arisen from conflicting answers
conflicts[text] | string | The conflict text
conflicts[answers] | collection | A collection of the conflicted answers
conflicts[answers[id]] | string | Unique identifier for the answer object
conflicts[answers[text]] | string | The answer text
conflicts[answers[question[id]]] | string | Unique identifier for the question object
conflicts[answers[question[text]]] | string | The question text
conflicts[answers[question[description]]] | string | Context as to why this question is asked
conflicts[answers[question[links]]] | object | Links to related endpoints
links | object | Links to related endpoints
links[sign_up] | string | Where to submit the result to create a Six Park user and associations
