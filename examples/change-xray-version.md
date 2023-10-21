# Меняем ядро xray

С помощью следующих инструкций вы можете изменить ядро вашего Xray-core в Marzban или Marzban Node.

{% hint style="info" %}
Во всех приведенных ниже примерах файлы `docker-compose.yml` и `.env` можно найти по пути `/opt/marzban`, а файл `xray_config.json` - по пути `/var/lib/marzban`

Если вы установили Marzban вручную, вам нужно будет внести соответствующие изменения самостоятельно.
{% endhint %}

Загрузка Xray-core

{% hint style="info" %}
Для продолжения вам понадобятся пакеты unzip и wget.&#x20;
{% endhint %}

Чтобы установить их, используйте следующую команду.

```bash
apt install wget unzip
```

Сначала скопируйте ссылку на загрузку нужной версии Xray-core с страницы загрузок Xray-core и загрузите ее на сервер в папку /var/lib/marzban/xray-core.

Например, для загрузки версии 1.8.3 выполните следующие шаги:

Создайте папку для Xray и перейдите в нее.

```bash
mkdir -p /var/lib/marzban/xray-core && cd /var/lib/marzban/xray-core
```

Скачайте файл Xray с помощью wget.

```bash
wget https://github.com/XTLS/Xray-core/releases/download/v1.8.3/Xray-linux-64.zip
```

Извлеките файл из архива и удалите сам архив.

```bash
unzip Xray-linux-64.zip && rm Xray-linux-64.zip
```

Изменение ядра Marzban

Установите значение переменной `XRAY_EXECUTABLE_PATH` в файле `.env`

`XRAY_EXECUTABLE_PATH = "/var/lib/marzban/xray-core/xray"`

Перезапустите Marzban.

```
marzban restart
```

Изменение ядра в Marzban Node:

В Marzban Node также необходимо установить значение `XRAY_EXECUTABLE_PATH` и добавить папку /var/lib/marzban в службу, как показано ниже.

```bash
nano /Marzban-node/docker-compose.yml
```

```yaml
services:
  marzban-node:
    # build: .
    image: gozargah/marzban-node:latest
    restart: always
    network_mode: host
    environment:
      XRAY_EXECUTABLE_PATH: "/var/lib/marzban/xray-core/xray"
    volumes:
      - /var/lib/marzban-node:/var/lib/marzban-node
      - /var/lib/marzban:/var/lib/marzban
```

Затем перезапустите службу.
