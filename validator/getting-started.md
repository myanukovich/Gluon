---
description: Описание процесса развертывания узла сети валидаторов
---

# Getting Started

### Шаг 1. Подготовка системы

Рассмотрим пример развертывания узла сети валидаторов для операционной системы CentOS 8

Для сборки и последущих обновлений валидатора потребуется установить golang. Входим в систему, и скачиваем версию пакета:

```text
# wget https://dl.google.com/go/go1.13.3.linux-amd64.tar.gz
```

Распаковываем загруженный архив и устанавливаем в систему. В данном примере используется глобальный каталог /usr/local. Но вы можете указать домашний каталог, на тот случай если вам не доступны права администратора.

```text
# tar -xzf go1.13.3.linux-amd64.tar.gz
# mv go /usr/local
```

Устанавливаем переменный среды. Для работы golang компилятора требуется настроить переменные **GOROOT**, **GOPATH** и прописаться в **PATH**

Вашим любимым редатором открываем файл ~/.bashrc и добавляем в конец файла строки:

```text
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

Обновляем переменные среды

```text
# source ~/.bashrc
```

Проверяем правилность установки

```text
# go version

go version go1.13.3 linux/amd64
```

### Шаг 2. Загрузка и сборка валидатора

Для загрузки и сборки нам понадобятся такие средства разработчика как git и cpp. Сборка некоторых golang пакетов также потребует установленного gcc. Поэтому установим все необходимое одной командой используя групповой пакет Development Tools

```text
yum update
yum groupinstall -y 'Development Tools'
```

Теперь загружаем стабильную ветку репозитария Gluon 

```text
cd ~
git clone -b stable https://github.com/quantbrothers/dex.git
```

Переходим в каталог утилит для работы с сетью валидации и запускаем срипт для сборки. Параметр MAINNET означает, что наш сервис будет собран для работы с сетью Ethereum mainnet.

```text
cd ~/dex/authority
./build-standalone.sh MAINNET
```

В результате сборки во внутреннем каталоге ./bin должны появиться исполняемые файлы

```text
ls -la ./bin
total 87076
drwxrwxr-x.  2 fpv fpv       47 Feb 28 08:44 .
drwxrwxr-x. 11 fpv fpv      216 Feb 28 08:32 ..
-rwxrwxr-x.  1 fpv fpv 19753256 Feb 28 09:15 dexcli
-rwxrwxr-x.  1 fpv fpv 32518072 Feb 28 09:15 dexsvc
-rwxrwxr-x.  1 fpv fpv 36892096 Feb 28 09:15 vnode
```

**vnode** - сервис узла сети валидации  
**dexsvc** - сервис для локального равертывания [REST API обменника](../developer/api.md)  
**dexcli** - утилита для работа с сетью Gluon в режиме [коммандной строки](command-line.md)

### Шаг 3. Конфигурирование и запуск валидатора

Почти все готово для того, чтобы запустить наш собственный валидатор  
Для начала создадим структуру каталогов для работы сервиса

```text
mkdir ~/vnode
cd ~/vnode
mkdir ~/vnode/config
mkdir ~/vnode/data
```

Создадим новые ключи и файл конфигурации используя команду init

```text
~/dex/authority/bin/vnode init
Initalize node configuration files
I[2020-02-28|09:21:53.003] Generated private validator                  keyFile=config/priv_validator_key.json stateFile=data/priv_validator_state.json
I[2020-02-28|09:21:53.003] Generated node key                           path=config/node_key.json
I[2020-02-28|09:21:53.003] Generated genesis file                       path=config/genesis.json
```

Файл config/node\_key.json содержит приватный ключ, необходимый для подписи новых блоков. Рекомендуем сделать резервную копию этого файла, так как с ним будет ассоциирована ваша запись в глобальной сети валидаторов.

Конфигурация по умолчанию расположена в файле config/node.toml  
Даный файл является стандартным файлом конфигурации узла Tendermint с некоторыми дополнениями, значение полей описано в комментариях. 

Пропишем в конфигурационном файле адреса full-node всех поддерживаемых для валидации блокчейнов таком формате:

```text
[chains.*]
node = "<node address>:<node port>"
rpc_user = "user"
rpc_password = "pass"
```

Где chains.\* означает вид блокчейна, например:

```text
[chains.bitcoin]
node = "<bitcoin node address>:<bitcoin node port>"
rpc_user = "rpc"
rpc_password = "rpc"
```

API валидатора по умолчанию будет доступен на порту 26657, и может быть изменен через поле rpc/laddr

```text
##### rpc server configuration options #####
[rpc]

# TCP or UNIX socket address for the RPC server to listen on
laddr = "tcp://0.0.0.0:26657"
```

Далее нам понадобится keystore файл с ключем Ethereum адреса, от которого будут подписываться сертификаты. Этот же адрес должен быть владельцем минимального необходимого для валидации Gluon токенов. Создать новый keystore файл можно, например при помощи популярного сервиса [MyEtherWallet](https://www.myetherwallet.com)

Для работы валидатора понадобится доступ к сети Ethereum по стандартному [DApps REST API](https://github.com/ethereum/wiki/wiki/JSON-RPC), для этого можно подключиться к любой full-node на базе parity, geth или любому full-node сервису например Infura.

```text
ethereum_node = "<ethereum node RPC address>"
eth_keystore_file = "27bd836595b708956046e127a1fe5c70a08dd7c3.json" # keysore файл 
```

Это все! Теперь можно запустить сервис

```text
~/dex/authority/bin/vnode --config=./config/node.toml
Enter Ethereum keystore passphrase: ********

I[2020-02-28|19:56:55.193] Version info                                 module=main software=0.32.7 block=10 p2p=7
I[2020-02-28|19:56:55.333] Starting Node                                module=main impl=Node
I[2020-02-28|19:56:55.520] Authority node started                       module=main RPC=tcp://w.x.y.z:26657
```

Чтобы валидатор мог использовать ваш Ethereum приватный ключ, будет предложено ввести passphase для keystore файла

### Шаг 4. Обновление валидатора

TODO

