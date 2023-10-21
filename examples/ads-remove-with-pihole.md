# Убираем рекламу с Pi-Hole

Для блокировки рекламы на стороне сервера, предлагается использовать программное решение Pi-Hole

> Pi-hole — это приложение для блокировки рекламы и интернет-трекеров на уровне сети Linux, которое действует как приемник DNS и, при необходимости, DHCP-сервер, предназначенный для использования в частной сети.

Для начала нам нужно обновить сервер

```bash
sudo apt update && apt upgrade -y
```

Установите pi-hole

```bash
curl -sSL https://install.pi-hole.net | bash
```

При достижения этапа STATIC IP, нам необходимо выбрать вариант "Продолжить" слева Продолжайте вводить "Yes" до завершения установки&#x20;

![](<../.gitbook/assets/image (1) (1).png>)

В конце установки вы получите адрес и пароль (вы можете изменить пароль)

![](<../.gitbook/assets/image (2) (1).png>)

Запустите pi-hole

```bash
sudo systemctl start pihole-FTL
```

Измените пароль

```bash
pihole -a -p
```

Адрес входа в панель управления pi-hole

`IP-ADDRESS/admin`

![](<../.gitbook/assets/image (3).png>)

Перейдите в настройки Pi-Hole

`Tools - Update Gravity -Update`

![](<../.gitbook/assets/image (4).png>)

Обновите и затем перейдите к

`Setting - DNS`

![](<../.gitbook/assets/image (5).png>)

Примените изменения и сохраните внизу страницы

Измените DNS-сервер

```bash
nano /etc/resolv.conf
```

`nameserver 127.0.0.1`

![](<../.gitbook/assets/image (6).png>)

Измените DNS-сервер в файле конфигурации вашего `xray-config.json`

```bash
nano /var/lib/marzban/xray_config.json
```

добавив туда

{% code lineNumbers="true" %}
```json
"dns": {
    "servers": [
      "127.0.0.1"
    ]
  },
```
{% endcode %}

или сделав тоже самое через WebUI

![](<../.gitbook/assets/image (7).png>)

Перезагрузить marzban

```bash
marzban restart
```

Готово! Теперь вы можете настроить сам Pi-Hole

![](<../.gitbook/assets/image (12).png>)
