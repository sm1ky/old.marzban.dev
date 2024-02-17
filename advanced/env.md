---
order: 898
label: Переменные окружения
icon: eye
---

Вы можете установить значения для всех этих переменных в файле .env.

{% hint style="info" %}
Если вы установили Marzban с помощью быстрого установщика, вы можете найти файл .env по пути `/opt/marzban/.env`
{% endhint %}

## UVICORN_HOST

Привязка приложения к хосту (по умолчанию: `0.0.0.0`)                                                   
{% hint style="info" %}
0.0.0.0 означает все доступные адреса на машине.
{% endhint %}

## UVICORN_PORT

Привязка приложения к порту (по умолчанию: `8000`) 


## UVICORN_UDS:

Привязка приложения к UNIX domain socket

{% hint style="info" %}
Если значение установлено, переменные `UVICORN_HOST` и `UVICORN_PORT` игнорируются.
{% endhint %}

## UVICORN_SSL_CERTFILE:

Адрес файла сертификата SSL.

{% hint style="info" %}
Пример: `/var/lib/marzban/certs/fullchain.pem`
{% endhint %}

## UVICORN_SSL_KEYFILE:

Адрес файла ключа SSL.

{% hint style="info" %}
Пример: `/var/lib/marzban/cert/key.pem`
{% endhint %}

## XRAY_JSON:

Адрес файла JSON конфигурации Xray. (по умолчанию: `xray_config.json`)                                         

## XRAY_SUBSCRIPTION_URL_PREFIX:

Префикс адреса подписки.

{% hint style="warning" %}
Если эта переменная не задана, ссылки на подписки в Telegram-боте не будут отправляться правильно.
{% endhint %}

## XRAY_SUBSCRIPTION_PATH
значение по умолчанию: `sub` 

Путь к странице полписки 

{% hint style="info" %}
Пример: "SomeRandomSUB"
{% endhint %}
## XRAY_EXECUTABLE_PATH:

Адрес исполняемого файла Xray.

Значение по умолчанию: `/usr/local/bin/xray`

## XRAY_ASSETS_PATH:

Путь к папке с файлами ресурсов для Xray (файлы geoip.dat и geosite.dat)

Значение по умолчанию: `/usr/local/share/xray`

## XRAY_EXCLUDE_INBOUND_TAGS:

Теги входящих соединений, которые не требуют управления и не должны быть включены в список прокси.

{% hint style="info" %}
Пример: "`IBOUND_X INBOUND_Y INBOUND_Z`"
{% endhint %}

## XRAY_FALLBACKS_INBOUND_TAG:

Если вы используете входящее соединение с несколькими резервными вариантами, укажите здесь его тег.

## TELEGRAM_API_TOKEN:

Токен Telegram-бота (полученный от @botfather)

## TELEGRAM_ADMIN_ID:

Числовой идентификатор администратора в Telegram (полученный от @userinfobot)

## TELEGRAM_PROXY_URL:

URL прокси для запуска Telegram-бота (если серверы Telegram заблокированы на вашем сервере).

{% hint style="info" %}
Пример: "`socks5://127.0.0.1:1080`"
{% endhint %}

## CUSTOM_TEMPLATES_DIRECTORY:

Путь к папке с пользовательскими шаблонами.

Значение по умолчанию: `app/templates`

## CLASH_SUBSCRIPTION_TEMPLATE:

Шаблон для создания конфигурации Clash.

Значение по умолчанию: `clash/default.yml`

{% hint style="info" %}
Пример: `default.yml`
{% endhint %}

## SUBSCRIPTION_PAGE_TEMPLATE:

Шаблон страницы подписки 
Значение по умолчанию: `subscription/index.html`

## HOME_PAGE_TEMPLATE:

Шаблон главной страницы.

Значение по умолчанию: `home/index.html`


## SINGBOX_SUBSCRIPTION_TEMPLATE
Шаблон конфига Sing-Box
Значение по умолчанию: `singbox/default.json`


## SINGBOX_MUX_CONFIGURATION:

Настройки MUX для Sing-box

Значение по умолчанию: `singbox/mux_config.json`

## SUB_PROFILE_TITLE 
Заголовок подписки на клиенте

{% hint style="info" %}
Пример: `Susbcription`
{% endhint %}

## SUB_SUPPORT_URL
Ссылка-поддержки в подписке на клиенте

{% hint style="info" %}
Пример: `https://t.me/support`
{% endhint %}

## SUB_UPDATE_INTERVAL
Период авто-обновления подписки на клиенте

{% hint style="info" %}
Пример: `1`

установит период авто-обновления в 1 час
{% endhint %}
## SQLALCHEMY_DATABASE_URL:

URL базы данных для SQLAlchemy.

Значение по умолчанию: `sqlite:///db.sqlite3`

## WEBHOOK_ADDRESS:

Значение по умолчанию: `DEFAULT`
{% hint style="info" %}
Вы можете задать несколько адресов через `,`
{% endhint %}

## WEBHOOK_SECRET:

Значение по умолчанию: `DEFAULT`

## SUDO_USERNAME:

{% hint style="warning" %}
Настоятельно рекомендуется использовать CLI-интерфейс для создания администратора и не использовать эту переменную.
{% endhint %}

## SUDO_PASSWORD:

{% hint style="warning" %}
Настоятельно рекомендуется использовать CLI-интерфейс для создания администратора и не использовать эту переменную.
{% endhint %}

## DOCS:

Активация документации API по адресам `/docs` и `/redoc`.

Значение по умолчанию: `false`

## JWT_ACCESS_TOKEN_EXPIRE_MINUTES:

Время истечения срока действия доступного токена в минутах.

Значение по умолчанию: `1440`

{% hint style="info" %}
0 означает "без истечения срока действия".
{% endhint %}

## DEBUG:

Активация режима разработки (development).

Значение по умолчанию: `false`

## VITE_BASE_API:

Префикс пути API для использования в панели управления (фронт-энд).

Значение по умолчанию: `/api/`
