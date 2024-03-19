---
order: 990
label: Получение SSL
icon: shield
---

::: tip СОВЕТ

Рекомендуется получить и настроить сертификат для обеспечения безопасности передачи данных панели и защиты от атак "человек-по-середине", работы TLS подключений, функционирования подписок и многого другого.
:::

{% hint style="info" %}
Для доступа Marzban к файлам сертификатов они должны быть размещены в `/var/lib/marzban/certs`.
{% endhint %}

{% hint style="warning" %}
Перед получением SSL-сертификата настройте DNS-записи вашего домена (A и/или AAAA записи).

Если вы только что зарегистрировали домен и добавили DNS-записи, возможно, потребуется время для их обновления. Статус можно проверить на https://www.whatsmydns.net.
{% endhint %}

::: tip СОВЕТ
Для новых и существующих доменов рекомендуется использовать NS сервера Cloudflare и управлять DNS-записями через их сервисы.
:::

## Получение сертификата с acme.sh

### Установка необходимого ПО

```bash
sudo apt install cron socat
```

### Установка acme.sh

EMAIL — ваш email (можно указать любой).

```bash
curl https://get.acme.sh | sh -s email=EMAIL
```

### Создание директории для сертификатов

```bash
sudo mkdir -p /var/lib/marzban/certs/
```

### Получение сертификатов

Замените `DOMAIN` на ваш домен или субдомен.

```bash
~/.acme.sh/acme.sh --set-default-ca --server letsencrypt --issue --standalone -d DOMAIN \
--key-file /var/lib/marzban/certs/key.pem \
--fullchain-file /var/lib/marzban/certs/fullchain.pem
```

## Получение wildcard сертификата с acme.sh

Если вам нужны wildcard сертификаты для всех поддоменов.

### Установка необходимого ПО

```bash
sudo apt install cron socat
```

### Установка acme.sh

EMAIL — ваш email (можно указать любой).

```bash
curl https://get.acme.sh | sh -s email=EMAIL
```

### Создание директории для сертификатов

```bash
sudo mkdir -p /var/lib/marzban/certs/
```

### Получение ключа API Cloudflare

Получите Global API Key в аккаунте Cloudflare для автоматической настройки DNS-записей.

### Настройка переменных окружения

```bash
export CF_Key="ваш_cloudflare_api_key"
export CF_Email="ваш_cloudflare_email"
```

### Выпуск wildcard сертификата

Замените `DOMAIN` на ваш домен.

```bash
~/.acme.sh/acme.sh --set-default-ca --server letsencrypt --issue --dns dns_cf \
-d DOMAIN \
-d *.DOMAIN \
--key-file /var/lib/marzban/certs/key.pem \
--fullchain-file /var/lib/marzban/certs/fullchain.pem
```

::: tip ПОДСКАЗКА
Для просмотра списка выпущенных сертификатов:

```bash
~/.acme.sh/acme.sh --list
```
:::

::: tip ПОДСКАЗКА
Для ручного продления сертификатов:

Вы должны перечислить все домены, которые хотите продлить
```bash
~/.acme.sh/acme.sh --renew -d DOMAIN --force
```
:::