---
label: 403 ошибка
icon: bug
---

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
{% hint style="info" %}
С версии ядра 1.8.6 рекомендуется использовать значение `ForceIPv4` вместо `UseIPv4`
Разница между “UseIPv4”, “UseIPv6” и “ForceIPv4”, “ForceIPv6” заключается в том, что первые при неудачной попытке разрешения переходят на AsIs, в то время как вторые при неудаче блокируются. Это делает всю стратегию domainStrategy более гибкой.
{% endhint %}
```
### Часть RULES
```json
{
        "type": "field",
        "outboundTag": "IPv4",
        "domain": [
          "geosite:google"
        ]
      }

```

## Вариант 2: Отключаем IPv6 
{% hint style="warning" %}
Не рекомендуется. Используйте только тогда, когда понимаете что делаете
{% endhint %}
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
