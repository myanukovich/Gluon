---
description: обзор похода в разработке Gluon
---

# Overview

Gluon внешне являясь по своей сути обычном обменником криптовалют, внутри реализован как DeFi сервис, что является его основной отличительной чертой. Очень строго придерживаясь идей криптосообщества он отражает основные принципы децентрализованных приложений.

`На данный момент существует большое множество сервисов  обмена криптовалют, но все они реализованы через централизованную часть. Децентрализованные обменники используют подход AtomicSwap что заставляет их вмешиваться в устройство каждого блокчейна к которому они подключаются.`

Это полностью open source проект, все части системы находится в открытом доступе. Весь механизм обмена токенов и финансовая часть написана на смарт-контрактах Ethereum, часть связанная с валидацией обмена реализована через Tendermind протокол. Такой подход мы назвали Doublechain consensus. Он позволяет реализовать Interblockchain взаимодействие без непосредственно вмешательство в блокчейны, при этом оставаясь полностью децентрализованным, удовлетворяя требования DeFi систем.

Вся комиссия системы делиться между всеми участниками системы. Чтобы участвовать в валидации обмена и получения комиссии кто-то угодно может приобрести токены системы через механизм DAO. Принцип DAO такой же как в [MolochDAO](https://molochdao.com/), чтобы получить токен системы необходимо внести определённое кол-во ETH в DAO. Таким образом токен не принадлежит какой-то компании и не может выпускаться неограниченно. Управление параметрами системы происходит так через DAO путём голосования.

Токен работает схеме [TCR](https://hackernoon.com/token-curated-registry-tcr-design-patterns-4de6d18efa15) и удовлетворяет принципам [Mike’s Cryptosystems Manifesto](https://docs.google.com/document/d/1TcceAsBlAoFLWSQWYyhjmTsZCp0XqRhNdGMb6JbASxc/edit?usp=sharing). Он необходим чтобы стимулировать валидаторов поддерживать правильную работу системы. В случаи развития системы валидаторы будут получать как доход от комиссий системы, так и прибыль от возможного увеличения цены токена. В случаи неверной работы или попытки атаки на систему валидатор штрафуется за эти действия своими токенами.

Кто-угодно так же может стать исполнителем заказов на обмен токенов, получая комиссию с обмена. Для этого он реализует свою Relay систему для взаимодействия со смарт-контактами системы.

Взаимная согласованность участников системы позволяет системе действовать в децентрализованном режиме. Это согласованность реализуется через механизмы доступные в блокчейне и близкие к идеям radical markets и [mechanism design](https://en.wikipedia.org/wiki/Mechanism_design).

### Дизайн системы позволяет реализовать некоторые особенности. 

Так за счёт конкуренции Исполнителей и страхового депозита можно добиться исполнения обмена по индексной цене, т.е. лучшей цене исполнения без проскальзывания на любой объём сделки. Если Исполнитель меняет токены по цене хуже индексной с его страхового депозита удерживается компенсация в пользу Клиента. Таким образом Клиент может быть уверен что получает обмен по лучшей цене, либо получит компенсацию покрывающую возможное отклонение от лучшей цены.

Система является полностью анонимной, не требующей идентификации для всех участников системы. Т.к. проект open source со стороны регуляторов нет возможности закрыть систему, т.к. она может быть развёрнута любым участником в блокчейне. Есть возможно реализации поддержка хостинга сайта каждым валидатором системы.



### Features

* DeFi project
  * open source проект
  * sharing profit
  * DAO проект
  * TCR token
* on-chain swap
  * Interblockchain обмен без изменения смарт-контрактов
    * поддержка большого количества блокчейнов
    * для поддержки обмена нового токена достаточно только поднять ноды для чтения сети этого токена и обновить валидаторов
  * Doublechain consensus
* особенности
  * анонимный обмен
  * обмен происходит по индексной цене
    * лучшая цена и для покупки и для продажи
      * конкуренция исполнителей, рейтинги
      * страховой депозит и компенсация
    * нет проскальзывания
  * застрахованный смарт-контакт



### Обзор DeFi

В последнее время наблюдается сильный взлёт сектора криптоэкономики связанного с DecentralizeFinance \(DeFi\). 

Количество денег находящихся в DeFi превысило 1 млрд. долларов.

![&#x41A;&#x43E;&#x43B;&#x438;&#x447;&#x435;&#x441;&#x442;&#x432;&#x43E; &#x434;&#x435;&#x43D;&#x435;&#x433; &#x43D;&#x430;&#x445;&#x43E;&#x434;&#x44F;&#x449;&#x435;&#x433;&#x43E; &#x432; DeFi](.gitbook/assets/image%20%281%29.png)

Объемы торгов на бирже Uniswap заметно растут в последнее время и доходят до до 5 млн. долларов в день.

![&#x41E;&#x431;&#x44A;&#x451;&#x43C;&#x44B; &#x442;&#x43E;&#x440;&#x433;&#x43E;&#x432; &#x43D;&#x430; uniswap &#x431;&#x438;&#x440;&#x436;&#x435;](.gitbook/assets/image%20%286%29.png)



### Устройство сервиса

Сервис удовлетворяет всем требованиям DeFi, является полностью opensource проектом, вся прибыль распределяется между участниками проекта. 



## Техническая часть

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

{% api-method method="get" host="/exchange/currencies" path="" %}
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

{% api-method method="get" host="" path="" %}
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

![](.gitbook/assets/image.png)

​

