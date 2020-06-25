# Portfolio

## GET > Retrieve a user's portfolio details

```shell
curl "https://app.sixpark.com.au/api/v1/users/:id/portfolio"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "value": 13724.0,
  "capital_gain": 1046.74,
  "capital_gain_percent": 7.48,
  "payout_gain": 17.65,
  "payout_gain_percent": 0.13,
  "currency_gain": -18.93,
  "currency_gain_percent": -0.14,
  "total_gain": 1045.46,
  "total_gain_percent": 7.48,
  "start_date": "2020-01-01",
  "end_date": "2020-07-01",
  "holdings": [
    {
      "ticker": "VGAD",
      "name": "Intl Equities (Hedged",
      "value": 500.0,
      "quantity": 100,
      "capital_gain": -2.0,
      "capital_gain_percent": -0.4,
      "payout_gain": 0.0,
      "payout_gain_percent": 0.0,
      "currency_gain": 0.0,
      "currency_gain_percent": 0.0,
      "total_gain": -2.0,
      "total_gain_percent": -0.4
    },
    "..."
  ],
  "cash_accounts": [
    {
      "name": "Macquarie...",
      "value": -1289.3,
      "currency": "AU$"
    }
  ]
}
```

_Retrieve_ details of a user's portfolio and performance.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/users/:id/portfolio`

### URL Parameters

Parameter | Required | Type | Default | Description
--------- | ----------- | ----------- | ----------- | -----------
start_date | no | date | inception | Start date (format `YYYY-MM-DD`)
end_date | no | date | today | End date (format `YYYY-MM-DD`)

### Summary

Configuration | Value | Description
--------- | ------- | -----------
authenticated | resource owner | Access is granted via the resource owner's access token
paginated | no |