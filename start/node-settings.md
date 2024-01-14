---
order: 994
label: Настройки узла
icon: apps
---
{% hint style="info" %}
Если Вы не планируете использовать дополнительные узлы (например для расширения географии Вашего сервиса), можете пропустить данный этап
{% endhint %}
{% hint style="warning" %}
узел - продолжение вашего сервиса и расширение панели, дублировать установку панели на сервер узла не нужно.
{% endhint %}

## Введение
**Marzban Node** - это приложение на Python, предоставляющее сервис для управления экземпляром ядра Xray. Оно использует RPyC для удаленных вызовов процедур и Docker для контейнеризации. Приложение разработано с учетом требований безопасности и использует самоподписанные SSL-сертификаты для связи между сервисом и его клиентами. 
С помощью этого руководства вы можете создать узел Marzban Node на дополнительном сервере и подключить его к панели.
{% hint style="info" %}
В связи с изменением принципа взаимодействия между **Центральной панелью** и **Узлом**, и переходом на **mTLS**, алгоритм подключения узла к центральной панели теперь отличается от уже всеми нами привычного.
{% endhint %}
### Отличие TLS от mTLS 
старый **TLS**
![](/static/tls.jpg)
новый **mTLS**
![](/static/mtls.jpg)
## Установка

### Получение ключа
Открываем **настройка узлов** и переходим в меню **добавление нового узла**.

![](/static/node_connect.png)

Скачиваем сертификат в файловую систему вашего устройства по нажатию на кнопку **скачать сертификат**
![](/static/node_download.png)
или, как еще один вариант, вы можете нажать значок **просмотреть** и скопировать полученное значение.
![](/static/node_show.png)

Теперь переходим на наш узел. 

### Настройка узла

Обновляем сервер

```bash
sudo apt-get update && sudo apt-get upgrade
```

Устанавливаем нужный софт

```bash
apt install socat -y && apt install curl socat -y && apt install git -y
```

Клонируем репозиторий

```bash
git clone https://github.com/Gozargah/Marzban-node
```

Входим в рабочую папку узла

```bash
cd Marzban-node
```

Устанавливаем Docker

```bash
curl -fsSL https://get.docker.com | sh
```
Создаем папку, куда поместим наш сертификат
```bash
mkdir -p /var/lib/marzban-node/
```

Теперь нам необходимо разместить ключ центальной панели на узле, для этого мы можем скопировать ранее полученный ключ по пути `/var/lib/marzban-node/ssl_client_cert.pem`

если Вы скопировали значение ключа ранее просто вставив его в нужный файл.
```bash
nano /var/lib/marzban-node/ssl_client_cert.pem
```

![](/static/node6.jpg)

Обьявляем в `docker-compose.yml` файле нашего проекта, о используемых сертификатах, открыв его через `nano` 
```bash
nano docker-compose.yml
```
приведя его к такому виду:
```yaml
services:
  marzban-node:
    image: gozargah/marzban-node:latest
    restart: always
    network_mode: host

    volumes:
      - /var/lib/marzban-node:/var/lib/marzban-node

    environment:
      SSL_CLIENT_CERT_FILE: "/var/lib/marzban-node/ssl_client_cert.pem"
```

После этого, теперь, Вы сможете запустить узел.

```bash
docker compose up -d
```

Теперь вернемся в основную панель

### Настройка панели 

Открываем настройки узлов

![](/static/node_add.png)

Заполняем данные узла:

* Name - Имя узла;
* Adress - IP адрес/домен/поддомен узла.
* Port - Оставляем по умолчанию, если не изменяли их.

Оставляем галку, если хотим добавить узел в качестве нового хоста во все входящие


Жмем `Добавить узел`

Если Вы не нажали галку `добавить узел в качестве нового хоста во все входящие`, Вы всегда сможете добавить узел в любой inbound, после ее подключения, просто указав ее адрес (IP или домен/суб-домен)


## Использование ноды на нескольких панелях 

Иногда, может возникнуть потребность запуска нескольких экзепляров узла на одном сервере, для подключения к нескольким панелям.
Для этого получаем сертификаты панели, и размещаем их на узле в папке  `/var/lib/marzban-node/`.

Например:

Сертификат Панель 1:

```/var/lib/marzban-node/server_1.pem```

Сертификат Панель 2:

```/var/lib/marzban-node/server_2.pem```


После необходимо отредактировать файл `docker-compose.yml`  следующим образом

```yaml
services:
  node-1:
    image: gozargah/marzban-node:latest
    restart: always
    network_mode: host

    volumes:
      - /var/lib/marzban-node:/var/lib/marzban-node
      - /var/lib/marzban:/var/lib/marzban

    environment:
      SERVICE_PORT: 2000
      XRAY_API_PORT: 2001
      SSL_CLIENT_CERT_FILE: "/var/lib/marzban-node/server_1.pem"


  node-2:
    image: gozargah/marzban-node:latest
    restart: always
    network_mode: host

    volumes:
      - /var/lib/marzban-node:/var/lib/marzban-node
      - /var/lib/marzban:/var/lib/marzban

    environment:
      SERVICE_PORT: 3000
      XRAY_API_PORT: 3001
      SSL_CLIENT_CERT_FILE: "/var/lib/marzban-node/server_2.pem"
```

После перезагрузки контейнера,мы будем иметь следующее:

| Переменная    | Node-1 | Node-2 |
| ------------- | ------ | ------ |
| SERVICE PORT  | 2000   | 3000   |
| XRAY API PORT | 2001   | 3001   |


И добавляем наши узлы исходя из вышеперечисленных данных
## Использование ноды на нескольких панелях с использованием Port Mapping
В этом случае для каждого экземпляра узла доступны только определенные порты, что предотвращает их повторение.
Обратите внимание, что вы должны указать порты, используемые в ваших входящих соединениях, в файле `docker-compose.yml`, как показано в примере.
Используйте следующий пример для добавления двух сервисов нода в файл `docker-compose.yml`:

*Пример настройки файла `docker-compose.yml`*

```yaml
services:
  marzban-node-1:
    image: gozargah/marzban-node:latest
    restart: always

    environment:
      SSL_CLIENT_CERT_FILE: "/var/lib/marzban-node/ssl_client_cert_1.pem"

    volumes:
      - /var/lib/marzban-node:/var/lib/marzban-node
      - /var/lib/marzban:/var/lib/marzban

    ports:
      - 2000:62050
      - 2001:62051
      - 2053:2053
      - 2054:2054


  marzban-node-2:
    image: gozargah/marzban-node:latest
    restart: always

    environment:
      SSL_CLIENT_CERT_FILE: "/var/lib/marzban-node/ssl_client_cert_2.pem"

    volumes:
      - /var/lib/marzban-node:/var/lib/marzban-node
      - /var/lib/marzban:/var/lib/marzban

    ports:
      - 3000:62050
      - 3001:62051
      - 2096:2096
      - 2097:2097
```

После получения необходимых сертификатов от панелей и размещения их в указанных местах, запустите узлы.

Порты подключения узлов к панелям и порты, доступные для входящих соединений, будут следующими:

| Переменная | Панель 1 | Панель 2 |
|------------|----------|----------|
| SERVICE PORT | 2000     | 3000     |
| XRAY API PORT   | 2001     | 3001     |
| Inbound PORTS | 2053, 2054 | 2096, 2097 |

### Дополнительные советы

**Совет первый**
Если для лучшего управления узлами вы хотите назначить каждому узлу отдельный inbound, вам нужно добавить новый inbound с уникальным тегом и портом в настройках ядра (Core Settings).

**Совет третий**
Если вы планируете использовать конфигурации с TLS, вам нужно получить сертификат для вашего суб-домена узла. Кроме того, вместо нескольких сертификатов для разных субдоменов, вы можете получить один Wildcard сертификат для основного домена, чтобы использовать его для всех субдоменов.

**Совет четвертый**
Файл `docker-compose.yml` чувствителен к выравниванию строк и пробелам. Для проверки правильности настройки вы можете использовать инструмент `yamlchecker`.

**Совет пятый**
Если вы внесли изменения в файл `docker-compose.yml`, перезапустите узлы с помощью следующей команды:

```bash
cd ~/Marzban-node
docker compose down --remove-orphans; docker compose up -d
```
