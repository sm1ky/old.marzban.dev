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
    alembic_version {
        string version_num PK
    }
    system {
        integer id PK
        bigint uplink
        bigint downlink
    }
    jwt {
        integer id PK
        string secret_key
    }
    proxies {
        integer id PK
        integer user_id
        string type
        json settings
    }
    admins {
        integer id PK
        string username
        string hashed_password
        datetime created_at
        boolean is_sudo
        datetime password_reset_at
        bigint telegram_id
        string discord_webhook
    }
    inbounds {
        integer id PK
        string tag
    }
    exclude_inbounds_association {
        integer proxy_id FK
        string inbound_tag FK
    }
    user_usage_logs {
        integer id PK
        integer user_id FK
        bigint used_traffic_at_reset
        datetime reset_at
    }
    hosts {
        integer id PK
        string remark
        string address
        integer port
        string inbound_tag FK
        string sni
        string host
        string security
        string alpn
        string fingerprint
        boolean allowinsecure
        boolean is_disabled
        string path
    }
    template_inbounds_association {
        integer user_template_id FK
        string inbound_tag FK
    }
    node_usages {
        integer id PK
        integer user_id FK
        string type
        datetime expires_at
        datetime created_at
    }
    tls {
        integer id PK
        string key
        string certificate
    }
    nodes {
        integer id PK
        string name
        string address
        integer port
        integer api_port
        string status
        datetime last_status_change
        string message
        datetime created_at
        bigint uplink
        bigint downlink
        string xray_version
        float usage_coefficient
    }
    user_templates {
        integer id PK
        string name
        integer data_limit
        integer expire_duration
        string username_prefix
        string username_suffix
    }
    users {
        integer id PK
        string username
        string status
        bigint used_traffic
        bigint data_limit
        integer expire
        datetime created_at
        integer admin_id FK
        string data_limit_reset_strategy
        datetime sub_revoked_at
        string note
        datetime sub_updated_at
        string sub_last_user_agent
        datetime online_at
        datetime edit_at
        datetime on_hold_timeout
        bigint on_hold_expire_duration
    }

    proxies }|--|{ users : "belongsTo"
    user_usage_logs }|--|{ users : "logsFor"
    node_usages }|--|{ users : "usageFor"
    exclude_inbounds_association }|--|| inbounds : "excludes"
    template_inbounds_association }|--|| inbounds : "includes"
    users }|--|{ admins : "managedBy"```
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