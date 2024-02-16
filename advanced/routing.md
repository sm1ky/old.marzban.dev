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
    ALEMBIC_VERSION ||--o{ SYSTEM : ""
    JWT ||--o{ SYSTEM : ""
    EXCLUDE_INBOUNDS_ASSOCIATION {
        string proxy_id
        string inbound_tag
    }
    SYSTEM ||--o{ EXCLUDE_INBOUNDS_ASSOCIATION : ""
    PROXIES ||--o{ EXCLUDE_INBOUNDS_ASSOCIATION : ""
    INBOUNDS ||--o{ EXCLUDE_INBOUNDS_ASSOCIATION : ""
    TEMPLATE_INBOUNDS_ASSOCIATION {
        string user_template_id
        string inbound_tag
    }
    USER_TEMPLATES ||--o{ TEMPLATE_INBOUNDS_ASSOCIATION : ""
    INBOUNDS ||--o{ TEMPLATE_INBOUNDS_ASSOCIATION : ""
    TLS ||--o{ HOSTS : ""
    HOSTS ||--o{ INBOUNDS : ""
    NODE_USER_USAGES {
        string user_id
        string node_id
        string used_traffic
    }
    USERS ||--o{ NODE_USER_USAGES : ""
    NODES ||--o{ NODE_USER_USAGES : ""
    USERS ||--o{ PROXIES : ""
    NODE_USAGES ||--o{ NODES : ""
    NOTIFICATION_REMINDERS ||--o{ USERS : ""
    USER_USAGE_LOGS ||--o{ USERS : ""
    ADMINS ||--o{ USERS : ""
}
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