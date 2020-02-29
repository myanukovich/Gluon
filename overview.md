---
description: Обзор DeFi и существующих решений onchain swaps
---

# DeFi & Onchain swaps

## Обзор DeFi

В последнее время наблюдается сильный рост сектора криптоэкономики связанного с Decentralized Finance \(DeFi\).

Количество денег находящихся в DeFi превысило 1 млрд. долларов.

![&#x41A;&#x43E;&#x43B;&#x438;&#x447;&#x435;&#x441;&#x442;&#x432;&#x43E; &#x434;&#x435;&#x43D;&#x435;&#x433; &#x43D;&#x430;&#x445;&#x43E;&#x434;&#x44F;&#x449;&#x438;&#x445;&#x441;&#x44F; &#x432; DeFi](.gitbook/assets/image%20%281%29.png)

Объемы торгов на бирже Uniswap заметно растут в последнее время и доходят до 5 млн. долларов в день.

![&#x41E;&#x431;&#x44A;&#x451;&#x43C;&#x44B; &#x442;&#x43E;&#x440;&#x433;&#x43E;&#x432; &#x43D;&#x430; uniswap &#x431;&#x438;&#x440;&#x436;&#x435;](.gitbook/assets/image%20%2812%29.png)

Растёт кол-во проектов

![The financial system builds itself on top of what is available.](.gitbook/assets/image%20%282%29.png)

{% embed url="https://medium.com/coinmonks/network-effects-in-an-open-financial-world-251152b9467d" caption="" %}

## Текущий подход к Onchain swap

На данный момент существует большое множество сервисов обмена криптовалют, но все они реализованы через централизованную часть. Минус такого подхода заключается в том, что практически нет возможности узнать фактические условия обмена, обменники могут скрывать дополнительные комиссии аргументируя плохой курс обмена проскальзыванием объема.

Децентрализованные обменники используют подход AtomicSwap. В случае cross-blockchain, это часто реализуется через Hashed Timelock Contracts, что, ограничивает число возможных блокчейнов, так как требует поддержки полнофункционального тюринг совместимого языка смарт-контрактов. Кроме того, такие алгоритмы часто носят академический характер поэтому требуется время для стабилизации и проверки всей их вариативности, для того, чтобы быть уверенным в криптографической стойкости.

{% embed url="https://medium.com/@OAX\_Foundation/tl-dr-atomic-swaps-cross-chain-swaps-on-chain-off-chain-f428512e1d2a" caption="" %}

{% embed url="https://blockgeeks.com/guides/atomic-swaps/" caption="" %}

{% embed url="https://hackernoon.com/are-there-any-dexs-with-a-good-cross-chain-mechanism-wg1od316l" caption="" %}

