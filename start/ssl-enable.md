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
{% hint style="info" %}
знак `#` в начале каждой изменяемой переменной нужно удалить, иначе значение переменной не будет установленно, так как будет считаться закомментированным
{% endhint %}
::: tip СОВЕТ
если Вы испольузете wildcard домен, Вы можете использовать установить знак `*` в переменной `XRAY_SUBSCRIPTION_URL_PREFIX`,
например `https://*.DOMAIN.com`, вместо которого, система будет подставлять случайное значение, например  `https://830aa395df41ae5a.DOMAIN.com`
:::
```
UVICORN_PORT = 443
UVICORN_SSL_CERTFILE = "/var/lib/marzban/certs/fullchain.pem"
UVICORN_SSL_KEYFILE = "/var/lib/marzban/certs/key.pem"
XRAY_SUBSCRIPTION_URL_PREFIX = https://YOUR_DOMAIN
```
Сохраняем внесенные изменения.

Для того, что бы изменения вступили в силу, необходимо перезапустить панель 
```bash
marzban restart
``` 
Теперь панель управления Marzban будет доступна на вашем домене или субдомене по https.
