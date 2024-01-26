---
order: 999
label: Получение SSL
icon: shield
---
::: tip СОВЕТ

Хоть это и не обязательно, но я настоятельно рекомендую Вам получить и настроить SSL сертификаты для Вашей панели.
В частности, для безопастности передаваемых данных панели и исключения атаки "человек-по-середине", для работы TLS подключений, функционирования подписок, создания зашифрованного канала и множества других функций.
:::

{% hint style="info" %}
Файлы сертификатов должны быть доступны по адресу `/var/lib/marzban/certs`, чтобы Marzban мог получить к ним доступ.
{% endhint %}

{% hint style="warning" %}
Прежде чем приступить к получению SSL-сертификата, вы должны настроить DNS-записи домена(A и(или) АААА записи)

В случае, если Вы только зарегистрировали домен и тут же вписали A и(или) AAAA записи вашего домена, необходимо немного подождать для обновления всех записей.
проверить статус Вы всегда можете на https://www.whatsmydns.net
{% endhint %}

## Получение сертификата с acme.sh

### Устанавливаем нужный софт

```bash
sudo apt install cron  && apt install socat
```

### Устанавливаем acme.sh

EMAIL = Ваш email(можно любую случайную почту)

```bash
curl https://get.acme.sh | sh -s email=EMAIL
```

### Создаем директорию для сертификатов

```bash
sudo mkdir -p /var/lib/marzban/certs/
```

### Получаем сертификаты

Введите ваш домен или субдомен в поле `DOMAIN`

```bash
~/.acme.sh/acme.sh --set-default-ca --server letsencrypt  --issue --standalone -d DOMAIN \
--key-file /var/lib/marzban/certs/key.pem \
--fullchain-file /var/lib/marzban/certs/fullchain.pem
```

## Получение wildcard сертификата с acme.sh
В случае, если вам необходимо получить wildcard сертификаты для всех ваших поддоменов

### Устанавливаем нужный софт

```bash
sudo apt install cron  && apt install socat
```

### Устанавливаем acme.sh

EMAIL = Ваш email(можно любую случайную почту)

```bash
curl https://get.acme.sh | sh -s email=EMAIL
```

### Создаем директорию для сертификатов

```bash
sudo mkdir -p /var/lib/marzban/certs/
```

### Получаем ключ API  Cloudflare

Войдите в свой аккаунт Cloudflare и получите Global API Key. Этот ключ понадобится для автоматической настройки DNS записей
Настройка переменных окружения

### Настраиваем переменные окружения

```bash
export CF_Key="ваш_cloudflare_api_key"
export CF_Email="ваш_email"
```
### Выпуск wildcard сертификата
Введите ваш домен в поле `DOMAIN`

```bash
~/.acme.sh/acme.sh --set-default-ca --server letsencrypt --issue --dns dns_cf  \
-d DOMAIN \
-d *.DOMAIN \
--key-file /var/lib/marzban/certs/key.pem \
--fullchain-file /var/lib/marzban/certs/fullchain.pem 
```

## Посмотреть список выпущенных сертификатов

```bash
~/.acme.sh/acme.sh --list
```
## Продлить сертификаты, до момента авто продления
```bash
~/.acme.sh --renew -d DOMAIN --force
``` 