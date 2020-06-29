# Portfolio

## GET > Retrieve a user's account portfolio details

```shell
curl "https://app.sixpark.com.au/api/v1/users/:user_id/account/:account_id/portfolio"
  --header "Authorization: Bearer <access_token>"
```

> A successful (200 HTTP status code) example JSON response body:

```json
{
  "value": 13724.00,
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
      "name": "Intl Equities (Hedged)",
      "ticker": "VGAD",
      "value": 500.00,
      "quantity": 100,
      "capital_gain": -2.0,
      "capital_gain_percent": -0.40,
      "payout_gain": 0.00,
      "payout_gain_percent": 0.00,
      "currency_gain": 0.00,
      "currency_gain_percent": 0.00,
      "total_gain": -2.00,
      "total_gain_percent": -0.40
    },
    "..."
  ],
  "cash_accounts": [
    {
      "name": "Macquarie...",
      "value": 1289.30
    }
  ],
  "links": {
    "account": "https://...",
    "self": "https://..."
  }
}
```

_Retrieve_ details of a user's currently invested portfolio and performance.

### HTTP Request

`GET https://app.sixpark.com.au/api/v1/users/:user_id/accounts/:account_id/portfolio`

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

### 200 HTTP status code properties

Property | Type | Description
--------- | ----------- | -----------
value | float | The total value of the portfolio - precision to 2 decimal places
capital_gain | float | Capital gain - precision to 2 decimal places
capital_gain_percent | float | Capital gain percent - precision to 2 decimal places
payout_gain | float | Payout gain - precision to 2 decimal places
payout_gain_percent | float | Payout gain percent - precision to 2 decimal places
currency_gain | float | Currency gain - precision to 2 decimal places
currency_gain_percent | float | Currency gain percent - precision to 2 decimal places
total_gain | float | Total gain - precision to 2 decimal places
total_gain_percent | float | Total gain percent - precision to 2 decimal places
start_date | date | Start date (format `YYYY-MM-DD`)
end_date | date | End date (format `YYYY-MM-DD`)
holdings | collection | A collection of equities held
holdings[name] | string | Name of the equity
holdings[ticker] | string | The ASX symbol
holdings[value] | float | The value of the holding - precision to 2 decimal places
holdings[quantity] | string | The number of units held
holdings[capital_gain] | float | Capital gain - precision to 2 decimal places
holdings[capital_gain_percent] | float | Capital gain percent - precision to 2 decimal places
holdings[payout_gain] | float | Payout gain - precision to 2 decimal places
holdings[payout_gain_percent] | float | Payout gain percent - precision to 2 decimal places
holdings[currency_gain] | float | Currency gain - precision to 2 decimal places
holdings[currency_gain_percent] | float | Currency gain percent - precision to 2 decimal places
holdings[total_gain] | float | Total gain - precision to 2 decimal places
holdings[total_gain_percent] | float | Total gain percent - precision to 2 decimal places
cash_accounts | collection | A collection of cash account held
cash_accounts[name] | string | Name of the cash account
cash_accounts[value] | float | The value of the cash account - precision to 2 decimal places
