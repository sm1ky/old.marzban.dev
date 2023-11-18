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
wget -O https://github.com/Iambabyninja/ru_gov_zapret/releases/latest/download/zapret.dat
```

Имеет две ветки:
1) zapret.dat:zapret - Все что заблокировано РКНы
1) zapret.dat:zapret-zapad - Рессурсы не обслуживающие Русские IP

## Установка для сервера

Создаем папку 
```bash
mkdir -p /var/lib/marzban/assets/
```
Скачиваем 
```bash
wget -O /var/lib/marzban/assets/zapret.dat https://github.com/Iambabyninja/ru_gov_zapret/releases/latest/download/zapret.dat
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
