---
order: 893
label: Соблюдение законодательства
icon: blocked
---

{% hint style="info" %}
Статья находится в разработке
{% endhint %}

При осуществлении своей дейтельности, Вы обязаны выполнять требования и законы той страны, резидентом которой Вы являетесь, в частности, Вы обязаны ограничить посещение рессурсов запрешенных на территории РФ.

Для упрощения выполнения требований законодательства, подотовлен фильтр, который обновляется автоматически и регулярно, подгружая последние списки запрета РКН.

Актуальная версия всегда доступна по адресу 
```bash
wget -O https://s3.marzban.dev/files/zapret.dat
```

Имеет две ветки:
1) zapret.dat:zapret - Все что заблокировано РКН
1) zapret.dat:zapret-zapad - Ресурсы не обслуживающие Русских 

## Установка для сервера

Создаем папку 
```bash
mkdir -p /var/lib/marzban/assets/
```
Скачиваем 
```bash
wget -O /var/lib/marzban/assets/zapret.dat https://s3.marzban.ru/files/zapret.dat
```
Устанавливаем значение в .env файле

`XRAY_ASSETS_PATH = "/var/lib/marzban/assets/"`

Редактируем xray_config.json
```json
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "outboundTag": "BLOCK",
                "domain": [
                    "ext:zapret.dat:zapret",
                    "ext:zapret.dat:zapret-zapad"
                ],
                "type": "field"
            }
        ]
    }
```
