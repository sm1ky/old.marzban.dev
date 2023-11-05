---
order: 998
label: Подключение SSL
icon: shield-check
---

## Подключение SSL сертификатов

Если включить SSL в Marzban, панель управления и ссылка на подписку будут доступны через https. 

{% hint style="info" %}
Во всех примерах ниже вы можете найти файлы `docker-compose.yml` и `.env` по пути `/opt/marzban‍‍‍`, а `xray_config.json`по пути `/var/lib/marzban`
{% endhint %}

## SSL с помощью Uvicorn

Marzban запускается по умолчанию с помощью`Uvicorn`, он же позволяет вам определять файлы сертификатов SSL.

После создания файлов сертификатов SSL установите в файле `.env` следующие переменные .

{% hint style="info" %}
`YOUR_DOMAIN` - ваш домен или субдомен
{% endhint %}

```bash
nano /opt/marzban/.env
```

Изменяем в нем следующие переменные

```
UVICORN_PORT = 443
UVICORN_SSL_CERTFILE = "/var/lib/marzban/certs/fullchain.pem"
UVICORN_SSL_KEYFILE = "/var/lib/marzban/certs/key.pem"
XRAY_SUBSCRIPTION_URL_PREFIX = https://YOUR_DOMAIN
```

Теперь панель управления Marzban будет доступна на вашем домене или субдомене по https.
