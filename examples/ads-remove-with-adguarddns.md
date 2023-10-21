# Убираем рекламу с AdGuardDNS

Для блокировки рекламы на стороне сервера, предлагается использовать программное решение AdGuard DNS

> AdGuard DNS — это приложение для блокировки рекламы и интернет-трекеров на уровне сети Linux, которое действует как приемник DNS и, при необходимости, DHCP-сервер, предназначенный для использования в частной сети.

Для начала нам нужно обновить сервер

```bash
sudo apt update && apt upgrade -y
```

Скачайте и распакуйте AdGuard DNS

```bash
wget https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz

tar -xzf AdGuardHome_linux_amd64.tar.gz
```

Устанавливаем

```
cd AdGuardHome
sudo ./AdGuardHome -s install
```

Adguard Home будет доступен по следующим адресам

`http://127.0.0.1:3000`

`http://X.X.X.X:3000`

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

Готово! Теперь вы можете настроить сам AdGuard DNS

настраиваем фильтры и ДНС

```
https://dns.cloudflare.com/dns-query
https://dns-unfiltered.adguard.com/dns-query
tls://1dot1dot1dot1.cloudflare-dns.com
```

Активируем шифрование и активируем ранее полученные сертификаты

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
