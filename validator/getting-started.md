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

Распаковываем загруженный архив и устанавливаем в систему. В данном примере используется глобальный каталог /usr/local. Но возможно установить в домашнюю папку, на тот случай если вам не доступны права администратора.

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

```text
yum update
yum install -y git
yum groupinstall -y 'Development Tools'
```

```text
cd ~
git clone -b stable https://github.com/quantbrothers/dex.git
```

```text
cd ~/dex/authority
./build-standalone.sh MAINNET
```

```text
ls -la ./bin
total 87076
drwxrwxr-x.  2 fpv fpv       47 Feb 28 08:44 .
drwxrwxr-x. 11 fpv fpv      216 Feb 28 08:32 ..
-rwxrwxr-x.  1 fpv fpv 19753256 Feb 28 09:15 dexcli
-rwxrwxr-x.  1 fpv fpv 32518072 Feb 28 09:15 dexsvc
-rwxrwxr-x.  1 fpv fpv 36892096 Feb 28 09:15 vnode
```

Шаг 3. Конфигурирование и запуск валидатора

```text
mkdir ~/vnode
cd ~/vnode
mkdir ~/vnode/config
mkdir ~/vnode/data
```

```text
~/dex/authority/bin/vnode init
Initalize node configuration files
I[2020-02-28|09:21:53.003] Generated private validator                  keyFile=config/priv_validator_key.json stateFile=data/priv_validator_state.json
I[2020-02-28|09:21:53.003] Generated node key                           path=config/node_key.json
I[2020-02-28|09:21:53.003] Generated genesis file                       path=config/genesis.json
```



