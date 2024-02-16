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
    ALEMBIC_VERSION {
        varchar version_num "Version Number"
    }

    SYSTEM {
        integer id
        bigint uplink "Uplink Traffic"
        bigint downlink "Downlink Traffic"
    }

    JWT {
        integer id
        varchar secret_key "Secret Key"
    }

    PROXIES {
        integer id
        integer user_id
        varchar type
        json settings
    }

    ADMINS {
        integer id
        varchar username
        varchar hashed_password
        datetime created_at
        boolean is_sudo
        datetime password_reset_at
        bigint telegram_id
        varchar discord_webhook
    }

    INBOUNDS {
        integer id
        varchar tag
    }

    EXCLUDE-INBOUNDS-ASSOCIATION {
        integer proxy_id
        varchar inbound_tag
    }

    USER-USAGE-LOGS {
        integer id
        integer user_id
        bigint used_traffic_at_reset
        datetime reset_at
    }

    USERS {
        integer id
        varchar username
        varchar status
        bigint used_traffic
        bigint data_limit
        integer expire
        datetime created_at
        integer admin_id
        varchar data_limit_reset_strategy
        datetime sub_revoked_at
        varchar note
        datetime sub_updated_at
        varchar sub_last_user_agent
        datetime online_at
        datetime edit_at
        datetime on_hold_timeout
        bigint on_hold_expire_duration
    }

    USERS ||--o{ ADMINS : "admin_id"
    USERS ||--o{ PROXIES : "user_id"
    PROXIES ||--o{ EXCLUDE-INBOUNDS-ASSOCIATION : "proxy_id"
    INBOUNDS ||--o{ EXCLUDE-INBOUNDS-ASSOCIATION : "inbound_tag"
    USERS ||--o{ USER-USAGE-LOGS : "user_id"
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