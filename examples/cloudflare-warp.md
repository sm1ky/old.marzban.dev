# CloudFlare Warp

Используя это руководство, вы можете снять некоторые ограничения, налагаемые крупными компаниями, такими как Google, Spotify и т.п., на ваш IP-адрес и без проблем пользоваться ими.

{% hint style="info" %}
Обратите внимание, что для конфигураций Warp существует максимальное ограничение на подключение — 5 устройств одновременно, для решения проблемы вы можете использовать несколько конфигураций.
{% endhint %}

## Создание конфигурации Wireguard[​](https://gozargah.github.io/marzban/examples/warp#%D9%82%D8%AF%D9%85-%D8%A7%D9%88%D9%84-%D8%B3%D8%A7%D8%AE%D8%AA-%DA%A9%D8%A7%D9%86%D9%81%DB%8C%DA%AF-wireguard)

[​](https://gozargah.github.io/marzban/examples/warp#%D9%82%D8%AF%D9%85-%D8%A7%D9%88%D9%84-%D8%B3%D8%A7%D8%AE%D8%AA-%DA%A9%D8%A7%D9%86%D9%81%DB%8C%DA%AF-wireguard)Для начала вам необходимо скачать `Asset`нужный из раздела [релизов , этот файл разный в зависимости от процессора.](https://github.com/ViRb3/wgcf/releases)

```bash
wget https://github.com/ViRb3/wgcf/releases/download/v2.2.16/wgcf_2.2.18_linux_amd64
```

Измените путь к файлу на `/usr/bin/` и и его имя  на`wgcf`

```bash
mv wgcf_2.2.18_linux_amd64 /usr/bin/wgcf
```

Затем создайте конфигурацию, используя эти две команды

```bash
wgcf register
wgcf generate
```

Вы создали файл конфигурации `wgcf-profile.conf`

## Использование Warp+ (необязательно)

Чтобы получить лицензию и использовать Warp+, вы можете получить `license key` через [этого](https://t.me/generatewarpplusbot) Telegram-бота&#x20;

После его получения необходимо заменить `license_key` в файле `wgcf-account.toml`

Затем вам необходимо обновить информацию о конфигурации.

```bash
wgcf update
```

Затем вам нужно создать новый файл конфигурации.

```bash
wgcf generate
```

### Активация WARP  в Marzban[​](https://gozargah.github.io/marzban/examples/warp#%D9%82%D8%AF%D9%85-%D8%B3%D9%88%D9%85-%D9%81%D8%B9%D8%A7%D9%84%D8%B3%D8%A7%D8%B2%DB%8C-warp-%D8%B1%D9%88%DB%8C-%D9%85%D8%B1%D8%B2%D8%A8%D8%A7%D9%86) <a href="#qdm-swm-faalsazy-warp-rwy-mrzban" id="qdm-swm-faalsazy-warp-rwy-mrzban"></a>

{% hint style="info" %}
Этот метод рекомендуется только для Xray версии 1.8.3 или выше. В более старых версиях вы, вероятно, столкнетесь с проблемой утечки памяти.
{% endhint %}

Вам необходимо отредактировать ваш `xray_config.json` добавив в него новый `INBOUND` как в примере ниже, заполнив его данными из`wgcf-profile.conf`

```json
{
  "tag": "warp",
  "protocol": "wireguard",
  "settings": {
    "secretKey": "Your_Secret_Key",
    "DNS": "1.1.1.1",
    "address": ["172.16.0.2/32", "2606:4700:110:8756:9135:af04:3778:40d9/128"],
    "peers": [
      {
        "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
        "endpoint": "engage.cloudflareclient.com:2408"
      }
    ]
  }
}
```

## Настройки раздела маршрутизации[​](https://gozargah.github.io/marzban/examples/warp#%D9%82%D8%AF%D9%85-%DA%86%D9%87%D8%A7%D8%B1%D9%85-%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D8%A8%D8%AE%D8%B4-routing)

Вам необходимо отредактировать ваш `xray_config.json` добавив в него новый `OUTBOUND` как в примере ниже, указав, какие сайты будут отправлять через `WARP`

```bash
{
    "outboundTag": "warp",
    "domain": [
        "geosite:google"
        "openai.com",
        "ai.com",
        "ipinfo.io",
        "iplocation.net",
        "spotify.com"
    ],
    "type": "field"
}
```
