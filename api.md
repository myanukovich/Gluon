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
{% api-method-parameter name="Tx" type="string" required=true %}
transaction hash
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
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/currencies" %}
{% api-method-summary %}
/exchange/currencies
{% endapi-method-summary %}

{% api-method-description %}
Returns a list of supported currencies as a flat array
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

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

{% api-method method="get" host="http://dc.quantbrothers.com/index.html" path="\#/exchange/estimatedExchangeAmount" %}
{% api-method-summary %}
/exchange/estimatedExchangeAmount
{% endapi-method-summary %}

{% api-method-description %}
Returns estimated exchange value with your API partner fee included.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="From" required=true type="string" %}
Source currency
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

​

