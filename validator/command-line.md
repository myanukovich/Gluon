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



