---
description: Техническая часть
---

# API

### API для подключения к Gluon с клиентской стороны

Используется набор функций сходный с функциями обычного обменника.

Техническая документация и playground для тестов [http://dc.quantbrothers.com/index.html\#/](http://dc.quantbrothers.com/index.html#/)

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/get\_exchange\_announcementStatus" %}
{% api-method-summary %}
announcementStatus
{% endapi-method-summary %}

{% api-method-description %}
Returns status of a given announcement using a transaction hash provided.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="tx" type="string" required=true %}
Transaction hash
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
list of exchange orders with states
{% endapi-method-response-example-description %}

```
[
  {
    "announced_source_amount": 0,
    "authority_order_status": "accepted",
    "collateral": 0,
    "deposited_destination_amount": 0,
    "deposited_source_amount": 0,
    "destination_accept_height": 0,
    "destination_address": "string",
    "destination_currency": "string",
    "error_message": "string",
    "min_destination_amount": 0,
    "order_source_amount": 0,
    "signature": [
      0
    ],
    "source_accept_height": 0,
    "source_address": "string",
    "source_currency": "string"
  }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/get\_exchange\_currencies" %}
{% api-method-summary %}
currencies
{% endapi-method-summary %}

{% api-method-description %}
Returns a list of supported currencies as a flat array
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
List of supported currencies as a flat array
{% endapi-method-response-example-description %}

```
[
  "string"
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/get\_exchange\_estimatedExchangeAmount" %}
{% api-method-summary %}
estimatedExchangeAmount
{% endapi-method-summary %}

{% api-method-description %}
Returns estimated exchange value with your API partner fee included.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="from" required=true type="string" %}
Source currency
{% endapi-method-parameter %}

{% api-method-parameter name="to" required=true type="string" %}
Destination currency
{% endapi-method-parameter %}

{% api-method-parameter name="amount" required=true type="number" %}
Source currency amount to exchangecurrency
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
estimated amount
{% endapi-method-response-example-description %}

```
0
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/get\_exchange\_minAmount" %}
{% api-method-summary %}
minAmount
{% endapi-method-summary %}

{% api-method-description %}
Returns a minimum allowed payin amount required for a currency pair. Amounts less than a minimal will most likely fail the transaction.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="from" type="string" required=true %}
Source currency
{% endapi-method-parameter %}

{% api-method-parameter name="to" required=true type="string" %}
Destination currency
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
minimum allowed payin amount required for a currency pair \(from/to\)
{% endapi-method-response-example-description %}

```
0
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/post\_exchange\_newAnnouncement" %}
{% api-method-summary %}
newAnnouncement
{% endapi-method-summary %}

{% api-method-description %}
Creates a new exchange announcement and returns transaction hash
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="from" type="string" required=true %}
Source currency
{% endapi-method-parameter %}

{% api-method-parameter name="to" type="string" required=true %}
Destination currency
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="number" required=true %}
Source currency amount to exchange
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=true %}
User payout address to recieve destination currency amount
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
transaction hash
{% endapi-method-response-example-description %}

```
{
  "tx": "string"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

​

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/get\_exchange\_validateAddress" %}
{% api-method-summary %}
validateAddress
{% endapi-method-summary %}

{% api-method-description %}
Returns if a given address is valid or not for a given currency
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="currency" type="string" required=true %}
Currency of given address
{% endapi-method-parameter %}

{% api-method-parameter name="address" type="string" required=true %}
Address string
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/get\_exchange\_version" %}
{% api-method-summary %}
version
{% endapi-method-summary %}

{% api-method-description %}
Returns API version
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
API version string 'x.y.z'
{% endapi-method-response-example-description %}

```
string
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Models

```text
main.TxHashReply{
    tx	string
}
```

```text
model.ExchangeOrder{
    announced_source_amount	number
    authority_order_status	string
    Enum:
    Array [ 5 ]
    collateral	number
    deposited_destination_amount	number
    deposited_source_amount	number
    destination_accept_height	integer
    destination_address	string
    destination_currency	string
    error_message	string
    min_destination_amount	number
    order_source_amount	number
    signature	[...]
    source_accept_height	integer
    source_address	string
    source_currency	string
}
```

