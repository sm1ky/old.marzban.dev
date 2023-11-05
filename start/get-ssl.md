---
order: 999
label: Получение SSL
icon: shield
---

Хоть это и не обязательно, но я настоятельно рекомендую Вам получить и настроить SSL сертификаты для Вашей панели.
В частности, для работы TLS подключений, функционирования подписок, создания зашифрованного канала и многих других функций.

{% hint style="info" %}
Файлы сертификатов должны быть доступны по адресу `/var/lib/marzban/certs`, чтобы Marzban мог получить к ним доступ.
{% endhint %}

{% hint style="info" %}
Прежде чем приступить к получению SSL-сертификата, вы должны настроить DNS-записи домена.
{% endhint %}

## Получение сертификата с acme.sh

Устанавливаем нужный софт

```sh
apt install cron  && apt install socat
```

Устанавливаем acme.sh

EMAIL = Ваш email(можно любую случайную почту)

```sh
curl https://get.acme.sh | sh -s email=EMAIL
```

Создаем директорию для сертификатов

```sh
mkdir -p /var/lib/marzban/certs/
```

Получаем сертификаты

Введите ваш домен или субдомен в поле `DOMAIN`

```sh
~/.acme.sh/acme.sh --set-default-ca --server letsencrypt  --issue --standalone -d DOMAIN \
--key-file /var/lib/marzban/certs/key.pem \
--fullchain-file /var/lib/marzban/certs/fullchain.pem
```

В случае, если вам необходимо получить сертификаты для ваших поддоменов, команда получения сертификата будет выглядеть так

```sh
~/.acme.sh/acme.sh --set-default-ca --server letsencrypt --issue --standalone \
-d DOMAIN \
-d SUBDOMAIN1.DOMAIN \
-d SUBDOMAIN2.DOMAIN \
--key-file /var/lib/marzban/certs/key.pem \
--fullchain-file /var/lib/marzban/certs/fullchain.pem
```

### Посмотреть список выпущенных сертификатов

```sh
~/.acme.sh/acme.sh --list
```
