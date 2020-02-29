---
description: Работа с системой из коммандной строки
---

# Command line

Подробности сборки утилиты dexcli описаны на странице [Getting Started](getting-started.md)  
Данна утилита содержит набор комманд для взаимодействия с системой Gluon

* Занесение либо вывод токенов Gluon на депозит Валидатора
* Занесение либо вывод гарантийного депозита для Исполнителя
* Просмотр состояния депозитов
* Создание заказа на обмен токенов
* Просмотр состояния заказа
* Вспомогательные команды

dexcli использует конфигурационный файл для идентификации системы.   
Пример файла dexcli.toml

```text
ethereum_node = "ethereum node:port" # путь к Ethereum rpc api server
eth_keystore_file = "keystore_file.json" # keystore файл вашего Ethereum кошелька
authority_nodes = ["http://<validator node>:26657"] # адрес или слисок адресов любого узла валидатора
verbose_log = true # выводить подробный лог
```

dexcli help выдает справку по всему списку команд

```text
./dexcli help
Usage:
        ./dexcli <command> <sub command> ...

Commands allowed:
root\
+-----------+-----------------------+-------+
|  Command  |      Description      | Usage |
+-----------+-----------------------+-------+
| announce  | Order update commands |       |
| order     | Order update commands |       |
| vault     | Vault commands        |       |
| authority | Vault commands        |       |
+-----------+-----------------------+-------+
```

Команды имеют древовидную структуру, например для вывода справки о разделе "order" можно воспользоваться командой ./dexcli order help

```text
./dexcli order help
Usage:
        ./dexcli <command> <sub command> ...

Commands allowed:
order\
+--------------------------------+-------------------------------------------------+--------------------------------------------------------------------------+
|            Command             |                   Description                   |                                  Usage                                   |
+--------------------------------+-------------------------------------------------+--------------------------------------------------------------------------+
| get                            | Get order information                           | <order identifier>                                                       |
| accept                         | Accept order with specified announce identifier | <announce identifier> <source currency amount> <source currency address> |
| source_currency_deposited      | Update order deposited source currency          | <order identifier> <deposit transaction hash>                            |
| destination_currency_deposited | Update order deposited destination currency     | <order identifier> <deposit transaction hash>                            |
| completed                      | Mark order as completed                         | <order identifier>                                                       |
| failed                         | Fail order                                      | <order identifier> <"error message">                                     |
+--------------------------------+-------------------------------------------------+--------------------------------------------------------------------------+
```

### Пример: публикация заказа

В качестве примера использования рассмотрим пример публикации заказа.  
Попросим сеть поменять 0.1 BTC на ETH и укажем минимальный объем который мы хотим получить в ETH.

```text
./dexcli announce publish BTC ETH 0.1 3.8 0x1390c55b5bce89019aabc36f1d4bcc281ea4bcee

INFO: 2020/02/21 04:06:34 network_client.go:81: Ethereum node connected (address=0x... header=16902927, nonce=1447, gasprice=8000000000)
DEBUG: 2020/02/21 04:06:36 network_client.go:387: Transaction 0x... succesfully mined
DEBUG: 2020/02/21 04:06:36 network_client.go:115: Exchange announce published (announcementId=16886779, tx=0x..., size=303.00 B, cost=0.008 ETH)
INFO: 2020/02/21 04:06:36 main.go:283: Announcement identifier 16886779

```

Данной комадой мы сообщаем, что хотим обменять 0.1 BTC как минимум на 3.8 ETH и передаем Ethereum адрес, куда будут начислены ETH.

В результате выполнения команда вернет Announcement identifier этот идентификатор в дальнейшем позволит следить за выполнением заказа при помощи команды ./dexcli announce get &lt;id&gt;

```text
./dexcli announce get 16886779

DEBUG: 2020/02/29 08:30:59 authority_client.go:190: abci_query(7b22636f6e7472616374223a2265786368616e6765222c226f7065726174696f6e223a226765745f616e6e6f756e63656d656e74222c22706172616d6574657273223a7b22616e6e6f756e63656d656e745f6964223a223136383836373739227d7d)
INFO: 2020/02/29 08:31:00 main.go:257: {
  "announced_source_amount": 0.1,
  "announcement_id": 16886779,
  "client": "0x...",
  "destination_address": "0x1390c55b5bce89019aabc36f1d4bcc281ea4bcee",
  "destination_currency": "ETH",
  "min_destination_amount": 3.8,
  "residual_amount": 0.1,
  "source_currency": "BTC"
}

```



