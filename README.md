---
title: Introduction
description: обзор Gluon системы
---

# Introduction

Gluon это onchain платформа для обмена токенов между различными блокчейнами. Обмен происходит напрямую между участниками системы. Все стадии обмена контролируются смарт-контактом ethereum и tendermint сетью валидаторов. Обмен гарантируется страховым депозитом со стороны исполнителя обмена. Общий размер страхового депозита, находящего на смарт-контракте, отображает общую ликвидность платформы.

* [DeFi App](./#defi-app)
  * open source code
  * **sharing profit**
  * DAO project
  * TCR token
* [Onchain Swap](./#onchain-swap)
  * Interblockchain обмен через Doublechain consensus
  * поддержка большого количества блокчейнов
  * **анонимный обмен**
  * обмен по **индексной цене** \(лучшая возможная цена обмена\)
    * конкуренция исполнителей, рейтинги
    * страховой депозит и компенсация
    * отсутствие проскальзывания
  * застрахованный смарт-контакт

### DeFi App

Gluon внешне являясь обычном обменником криптовалют, внутри реализован как DeFi сервис, что является его основной отличительной чертой. Строго следуя идеям криптосообщества Gluon, придерживается основных принципов децентрализованных приложений.

Цель проекта создать DAO систему в которой происходит распределения прибылей среди участников, когда нет одной компании получающей и распределяющей прибыль. Мы не выпускаем свой токенов, не собираем денег, не делаем обменник, который аккумулирует комиссию на себе. Вся комиссия системы делится между участниками системы. Мы, как начальные разработчики, являемся наравне с остальными, частью этой системы. И не получаем никаких финансовых привилегий. Система может существовать без нашего вмешательства. Core разработчики могут меняться.

{% hint style="success" %}
Мы не выпускаем свой централизованный токен, не собираем денег, не делаем обменник, который аккумулирует комиссию.
{% endhint %}

В системе существует три типа участников:

1. **Клиент** - тот кто создаёт запрос на обмен токенов 
2. **Исполнитель \(relayer\)** - тот кто реализует обмен
3. **Валидатор** - тот кто проверяет корректность исполнителя

Валидаторы объединены в блокчейн-сеть валидаторов. И именно сеть валидаторов подтверждает исполнение сделки. Исполнители конкурируют между собой за право выполнения сделки. И исполнителем и валидатором может стать любой человек или проект.

Все части система является open source проектом. Механизм обмена токенов и финансовая часть написана на смарт-контрактах Ethereum. Часть связанная с валидацией обмена реализована через протокол консенсуса [Tendermint](https://tendermint.com/static/docs/tendermint.pdf). Такой подход совмещения блокчейнов мы назвали [Doublechain consensus](technical/doublechain-consensus.md). Он позволяет реализовать Interblockchain взаимодействие без непосредственного вмешательство в блокчейны токенов. Для поддержки обмена нового токена достаточно только развернуть full-ноды для чтения сети этого токена и обновить валидатор.

{% hint style="info" %}
Open source проект.
{% endhint %}

Экономика системы работает по схеме [TCR](https://hackernoon.com/token-curated-registry-tcr-design-patterns-4de6d18efa15) и удовлетворяет принципам [Mike’s Cryptosystems Manifesto](https://docs.google.com/document/d/1TcceAsBlAoFLWSQWYyhjmTsZCp0XqRhNdGMb6JbASxc/edit?usp=sharing). Принцип TCR необходим, чтобы стимулировать валидаторов поддерживать правильную работу системы. В процессе развития системы валидаторы будут получать как доход от комиссий системы, так и прибыль от возможного увеличения цены токена. В случае неверной работы валидатора или попытки атаки на систему валидатором, он лишается части своих токенов.

Кто угодно может приобрести токены системы через механизм DAO. Принцип DAO построен в соответствие с правилами системы MolochDAO \([moloch-dao-explained](https://concourseopen.com/blog/moloch-dao-explained/)\) - чтобы получить токен системы, необходимо внести определённое кол-во ETH в DAO. Доступ к внесённым в DAO ETH происходит через совместное голосование участников DAO. Таким образом ни токен, ни ETH в DAO не принадлежат какой-то компании и не могут выпускаться неограниченно или по желанию. Управление параметрами системы происходит так же через DAO путём голосования.

Чтобы участвовать в валидации сделок и получать комиссию сети валидаторов, необходимо приобрести токен проекта, скачать код валидатора и настроить подключнеие к full-нодам блокчейнов поддержанных в системе.

Чтобы стать исполнителем, необходимо реализовать протокол взаимодействия с центральным смарт-контрактом и сетью валидаторов. Для этого может взять пример реализации Relayer или реализовать свой. Для возможности обмена токенов, исполнитель должен заблокировать в смарт-контракте депозит полностью покрывающий сумму сделки на период обмена \(страховой депозит\).

### Onchain swap

{% hint style="info" %}
Взаимная согласованность участников системы позволяет системе действовать в децентрализованном режиме. Такая согласованность реализуется через механизмы доступные в блокчейне и близкие к идеям radical markets и [mechanism design](https://en.wikipedia.org/wiki/Mechanism_design).
{% endhint %}

Дизайн системы позволяет извлечь ряд преимуществ над другими системами обмена токенов

* За счёт конкуренции исполнителей, а так же страхового депозита, можно добиться исполнения обмена по индексной цене, т.е. лучшей цене исполнения без проскальзывания на любой объём сделки. Если исполнитель меняет токены по цене хуже индексной, с его страхового депозита удерживается компенсация в пользу клиента. Таким образом клиент может быть уверен, что получает обмен по лучшей цене, либо получит компенсацию покрывающую возможное отклонение от лучшей цены.
* Система является полностью анонимной, не требующей идентификации для всех участников системы. Это open source проект, поэтому система может быть развёрнута любым участником. Каждая из нод валидаторов также предоставляет Web интерфейс к смарт-контракту системы, поэтому в случае блокировки или атаки на одну из нод, остаются доступны другие ноды валидаторов.

