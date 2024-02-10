---
label: 403 ошибка
icon: bug
---

При получении ошибки 403 на различных сайтах, Вы можете настройтить роутинг на ipv4

Открываем `xray_config.conf`

```bash
sudo nano /var/lib/marzban/xray_config.json
```

### Часть OUTBOUND

{% hint style="info" %}
С версии ядра 1.8.6 рекомендуется использовать значение `ForceIPv4` вместо `UseIPv4`
Разница между “UseIPv4”, “UseIPv6” и “ForceIPv4”, “ForceIPv6” заключается в том, что первые при неудачной попытке разрешения переходят на AsIs, в то время как вторые при неудаче блокируются. Это делает всю стратегию domainStrategy более гибкой.
{% endhint %}

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
{% hint style="info" %}
Убедитесь что в части `routing` обьявлено 
```
"domainStrategy": "IPIfNonMatch",
```
{% endhint %}
```json
{
        "type": "field",
        "outboundTag": "IPv4",
        "domain": [
          "geosite:google"
        ]
      }

```
