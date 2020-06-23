# Result

## GET > Get questionnaire result

```shell
curl "https://app.sixpark.com.au/api/v1/result"
  -H "Content-Type: application/json"
  -H "Authorization: Bearer <access_token>"
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
    }
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
  "links": {
    "sign_up": "https://...",
    "self": "https://..."
  }
```

_Get_ the Six Park questionnaire/risk assessment result.

The response will reflect back a collection of `answer_ids` as provided in the original request.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/result`

### Parameters

Parameter | Default | Description
--------- | ----------- | -----------
answer_ids | `no default` | A collection of answer ids, ie: `[AG6DpLkUwLCCNyZRhHEi, 4ReX5gCGen2XA13GDQHd]`

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | client credentials | Access is granted via a client credentials access token
paginated | no | 

