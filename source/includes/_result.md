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
    "annualised_return_percent": "5.49",
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
      "percentage": "50"
    },
    {
      "type": "defensive",
      "percentage": "50"
    }
  ],
  "allocations": [
    {
      "name": "Intl Equities (Hedged)",
      "ticker": "VGAD",
      "category_type": "growth",
      "provider_name": "Vanguard",
      "portfolio_percentage": "10",
      "links": {
        "pds": {
          "content_type": "application/pdf",
          "url": "https://assets.sixpark.com.au/pds/vgad.pdf"
        },
        "fact_sheet":  {
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
        "description": "Generally, younger investors have a greater appetite for..."
      }
    },
    {
      "id": "tnEKYuedAjPvBC6EFwAL",
      "text": "$125,000 to $249,999",
      "question": {
        "id": "znEPYuedAjPva",
        "text": "What is the total value of your liquid assets...",
        "description": "Generally, the greater the liquid assets you have, the more capacity you have to take on risk..."
      }
    },
    "..."
  ],
  "tripwires": [
    {
      "text": "It is unusual to seek high-risk investments when...",
      "answers": [
        {
          "id": "EGJkOzOij5PUhMZsjUno",
          "text": "Mostly concerned with potential...",
          "question": {
            "id": "tnEKYuedAjPvB",
            "text": "Which statement best describes your primary concern...",
            "description": "This question helps assess your desire for risk..."
          }
        },
        {
          "id": "QrVhgp9VAw2LOMC7kMPh",
          "text": "I want to play it safe and protect...",
          "question": {
            "id": "tnEKYuedAjPvB",
            "text": "Which statement BEST describes your current...",
            "description": "This question helps assess your desire for risk..."
          }
        }
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

As part of the response, a collection of `tripwires` may be returned. Tripwires _must_ be shown as part of the customer journey and acknowledged or the answer(s) related to the tripwire, changed.

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

