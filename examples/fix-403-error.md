При получении ошибки 403 на различных сайтах, Вы можете настройтить роутинг на ipv4


## Вариант 1: Настраваем роутинг
Открываем `xray_config.conf`

```bash
sudo nano /var/lib/marzban/xray_config.json
```

### Часть OUTBOUND
```json
{
      "tag": "IPv4",
      "protocol": "freedom",
      "settings": {
      "domainStrategy": "UseIPv4"
      }
    }

```
### Часть RULES
```json
{
        "type": "field",
        "outboundTag": "IPv4",
        "domain": [
          "geosite:google",
          "geoip:google",
          "domain:google.com"
        ]
      }

```

## Вариант 2: Отключаем IPv6 

При получении ошибки 403 на различных сайтах, настоятельно рекомендую отключить IPv6 на вашем сервере.

Открываем `sysctl.conf`

```bash
sudo nano /etc/sysctl.conf
```

Добавляем (изменяем) запись запрещающую использование IPv6 на всех адаптерах

```bash
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1
```

Для применения изменений перезапускаем `sysctl`&#x20;

```bash
sudo sysctl -p
```
