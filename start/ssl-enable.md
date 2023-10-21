---
order: 998
label: Подключение SSL
icon: shield-check
---

## Подключение SSL сертификатов <a href="#intro" id="intro"></a>

Если включить SSL в Marzban, панель управления и ссылка на подписку будут доступны через https. Существуют разные подходы к включению SSL в Marzban, ниже мы упомянем три метода, от простого к сложному.

{% hint style="info" %}
Во всех примерах ниже вы можете найти файлы `docker-compose.yml`и `.env`по пути `/opt/marzban‍‍‍`, а `xray_config.json`по пути `/var/lib/marzban`
{% endhint %}

## SSL с помощью Uvicorn[​](https://gozargah.github.io/marzban/examples/marzban-ssl#%D9%81%D8%B9%D8%A7%D9%84%E2%80%8C%D8%B3%D8%A7%D8%B2%DB%8C-ssl-%D8%A8%D8%A7-uvicorn) <a href="#uvicorn" id="uvicorn"></a>

Marzban запускается по умолчанию с помощью`Uvicorn` , он же позволяет вам определять файлы сертификатов SSL.

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
