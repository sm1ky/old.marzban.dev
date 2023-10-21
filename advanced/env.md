---
order: 898
label: Переменные окружения
icon: eye
---

Вы можете установить значения для всех этих переменных в файле .env.

{% hint style="info" %}
Если вы установили Marzban с помощью быстрого установщика, вы можете найти файл .env по пути `/opt/marzban/.env`
{% endhint %}

## UVICORN\_HOST&#x20;

Привязка приложения к хосту (по умолчанию: `0.0.0.0`)                                                   
{% hint style="info" %}
0.0.0.0 означает все доступные адреса на машине.
{% endhint %}

## UVICORN\_PORT&#x20;

Привязка приложения к порту (по умолчанию: `8000`) 


## UVICORN\_UDS:

Привязка приложения к UNIX domain socket

{% hint style="info" %}
Если значение установлено, переменные `UVICORN_HOST` и `UVICORN_PORT` игнорируются.
{% endhint %}

## UVICORN\_SSL\_CERTFILE:&#x20;

Адрес файла сертификата SSL.

{% hint style="info" %}
Пример: `/var/lib/marzban/certs/fullchain.pem`
{% endhint %}

## UVICORN\_SSL\_KEYFILE:&#x20;

Адрес файла ключа SSL.

{% hint style="info" %}
Пример: `/var/lib/marzban/cert/key.pem`
{% endhint %}

## XRAY\_JSON:&#x20;

Адрес файла JSON конфигурации Xray. (по умолчанию: `xray_config.json`)                                         

## XRAY\_SUBSCRIPTION\_URL\_PREFIX:&#x20;

Префикс адреса подписки.

{% hint style="warning" %}
Если эта переменная не задана, ссылки на подписки в Telegram-боте не будут отправляться правильно.
{% endhint %}

## XRAY\_EXECUTABLE\_PATH:&#x20;

Адрес исполняемого файла Xray.

Значение по умолчанию: `/usr/local/bin/xray`&#x20;

## XRAY\_ASSETS\_PATH:&#x20;

Путь к папке с файлами ресурсов для Xray (файлы geoip.dat и geosite.dat)

Значение по умолчанию: `/usr/local/share/xray`&#x20;

## XRAY\_EXCLUDE\_INBOUND\_TAGS:&#x20;

Теги входящих соединений, которые не требуют управления и не должны быть включены в список прокси.

{% hint style="info" %}
Пример: "`IBOUND_X INBOUND_Y INBOUND_Z`"
{% endhint %}

## XRAY\_FALLBACKS\_INBOUND\_TAG:

Если вы используете входящее соединение с несколькими резервными вариантами, укажите здесь его тег.

## TELEGRAM\_API\_TOKEN:&#x20;

Токен Telegram-бота (полученный от @botfather)

## TELEGRAM\_ADMIN\_ID:&#x20;

Числовой идентификатор администратора в Telegram (полученный от @userinfobot)

## TELEGRAM\_PROXY\_URL:&#x20;

URL прокси для запуска Telegram-бота (если серверы Telegram заблокированы на вашем сервере).

{% hint style="info" %}
Пример: "`socks5://127.0.0.1:1080`"
{% endhint %}

## CUSTOM\_TEMPLATES\_DIRECTORY:&#x20;

Путь к папке с пользовательскими шаблонами.

Значение по умолчанию: `app/templates`&#x20;

## CLASH\_SUBSCRIPTION\_TEMPLATE:&#x20;

Шаблон для создания конфигурации Clash.

Значение по умолчанию: `clash/default.yml`&#x20;

{% hint style="info" %}
Пример: `default.yml`
{% endhint %}

## SUBSCRIPTION\_PAGE\_TEMPLATE:&#x20;

Шаблон для страницы  подписки.

Значение по умолчанию: `subscription/index.html`&#x20;

## HOME\_PAGE\_TEMPLATE:&#x20;

Шаблон главной страницы.

Значение по умолчанию: `home/index.html`&#x20;

## SQLALCHEMY\_DATABASE\_URL:&#x20;

URL базы данных для SQLAlchemy.

Значение по умолчанию: `sqlite:///db.sqlite3`&#x20;

## WEBHOOK\_ADDRESS:

Значение по умолчанию: `DEFAULT`

## WEBHOOK\_SECRET:&#x20;

Значение по умолчанию: `DEFAULT`

## SUDO\_USERNAME:&#x20;

{% hint style="warning" %}
Настоятельно рекомендуется использовать CLI-интерфейс для создания администратора и не использовать эту переменную.
{% endhint %}

## SUDO\_PASSWORD:&#x20;

{% hint style="warning" %}
Настоятельно рекомендуется использовать CLI-интерфейс для создания администратора и не использовать эту переменную.
{% endhint %}

## DOCS:&#x20;

Активация документации API по адресам `/docs` и `/redoc`.

Значение по умолчанию: `false`&#x20;

## JWT\_ACCESS\_TOKEN\_EXPIRE\_MINUTES:&#x20;

Время истечения срока действия доступного токена в минутах.

Значение по умолчанию: `1440`&#x20;

{% hint style="info" %}
0 означает "без истечения срока действия".
{% endhint %}

## DEBUG:

Активация режима разработки (development).

Значение по умолчанию: `false`&#x20;

## VITE\_BASE\_API:&#x20;

Префикс пути API для использования в панели управления (фронт-энд).

Значение по умолчанию: `/api/`&#x20;
