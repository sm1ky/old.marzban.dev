---
order: 892
label: Маршрутизация
icon: iterations
visibility: hidden
---
{% hint style="warning" %}
Статья находится в режиме написания. Со временем будет дополняться и изменяться. 
{% endhint %}

Модуль маршрутизации позволяет нам отправлять входящие данные через различные исходящие соединения в соответствии с обьявленными правилами правилами.

## Введение в маршрутизацию

Для понимания маршрутизации необходимо осознать, что полноценная функциональность маршрутизации требует совместной работы трех компонентов: 
```mermaid
erDiagram
    SYSTEM {
        id INTEGER
        uplink BIGINT
        downlink BIGINT
    }
    JWT {
        id INTEGER
        secret_key VARCHAR(64)
    }
    PROXIES {
        id INTEGER
        user_id INTEGER
        type VARCHAR(11)
        settings JSON
    }
    ADMINS {
        id INTEGER
        username VARCHAR(34)
        hashed_password VARCHAR(128)
        created_at DATETIME
        is_sudo BOOLEAN
        password_reset_at DATETIME
        telegram_id BIGINT
        discord_webhook VARCHAR(1024)
    }
    INBOUNDS {
        id INTEGER
        tag VARCHAR(256)
    }
    EXCLUDE_INBOUNDS_ASSOCIATION {
        proxy_id INTEGER
        inbound_tag VARCHAR(256)
    }
    USER_USAGE_LOGS {
        id INTEGER
        user_id INTEGER
        used_traffic_at_reset BIGINT
        reset_at DATETIME
    }
    HOSTS {
        id INTEGER
        remark VARCHAR(256)
        address VARCHAR(256)
        port INTEGER
        inbound_tag VARCHAR(256)
        sni VARCHAR(256)
        host VARCHAR(256)
        security VARCHAR(15)
        alpn VARCHAR(11)
        fingerprint VARCHAR(10)
        allowinsecure BOOLEAN
        is_disabled BOOLEAN
        path VARCHAR(256)
    }
    TEMPLATE_INBOUNDS_ASSOCIATION {
        user_template_id INTEGER
        inbound_tag VARCHAR(256)
    }
    NODE_USAGES {
        id INTEGER
        user_id INTEGER
        uplink BIGINT
        downlink BIGINT
        xray_version VARCHAR(32)
        usage_coefficient FLOAT
    }
    USER_TEMPLATES {
        id INTEGER
        name VARCHAR(64)
        data_limit INTEGER
        expire_duration INTEGER
        username_prefix VARCHAR(20)
        username_suffix VARCHAR(20)
    }
    USERS {
        id INTEGER
        username VARCHAR(34)
        status VARCHAR(8)
        used_traffic BIGINT
        data_limit BIGINT
        expire INTEGER
        created_at DATETIME
        admin_id INTEGER
        data_limit_reset_strategy VARCHAR(8)
        sub_revoked_at DATETIME
        note VARCHAR(500)
        sub_updated_at DATETIME
        sub_last_user_agent VARCHAR(64)
        online_at DATETIME
        edit_at DATETIME
        on_hold_timeout DATETIME
        on_hold_expire_duration BIGINT
    }
    SETTINGS {
        id INTEGER
        dashboard_path VARCHAR(256)
        subscription_url_prefix VARCHAR(256)
        subscription_page_title VARCHAR(128)
        subscription_support_url_header VARCHAR(256)
        subscription_update_interval_header INTEGER
        webhook_url VARCHAR(256)
        webhook_secret VARCHAR(256)
        telegram_api_token VARCHAR(64)
        telegram_admin_ids VARCHAR(256)
        telegram_logs_channel_id VARCHAR(64)
        discord_webhook_url VARCHAR(256)
        jwt_token_expire_minutes INTEGER
    }

    USERS ||--o{ PROXIES : "has"
    ADMINS ||--o{ USERS : "manages"
    USERS ||--o{ USER_USAGE_LOGS : "logs"
    PROXIES ||--o{ EXCLUDE_INBOUNDS_ASSOCIATION : "excludes"
    HOSTS ||--o{ INBOUNDS : "hosts"
    USER_TEMPLATES ||--o{ TEMPLATE_INBOUNDS_ASSOCIATION : "templates"
    USERS ||--o{ NODE_USAGES : "uses"
```
1. Входящий трафик (inbound)
2. Маршрутизация
3. Исходящий трафик (outbound)

Эти компоненты работают вместе и важно понимать: любая ошибка в одном из этих элементов может привести к сбою в работе маршрутизации.






```mermaid
%%{init: { 'theme': 'neutral' }}%%
graph LR
    S(Запрос) .-> I[inbound]

    subgraph Xray
    I --> R[Маршрутизация] -- "geosite:category-ads-all" --> O1[блокируем]
    R[Маршрутизация] -- "geoip:ru" --> O3[проксируем]
    R[Маршрутизация] -. "Весь остальной" .-> O4[Напрямую]

    end

    O3 .-> V(Русский сервер)
    O4 .-> D(Запрос)

    O1:::redclass
    V:::greyclass
    R:::routingclass
    classDef redclass fill:#FF0000
    classDef greyclass fill:#C0C0C0
    classDef routingclass fill:#FFFFDE,stroke:#000000

```