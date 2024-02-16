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
    SYSTEM ||--o{ JWT : ""
    SYSTEM ||--o{ EXCLUDE_INBOUNDS_ASSOCIATION : ""
    SYSTEM ||--o{ PROXIES : ""
    SYSTEM ||--o{ NODE_USER_USAGES : ""
    SYSTEM ||--o{ NODES : ""
    SYSTEM ||--o{ NOTIFICATION_REMINDERS : ""
    SYSTEM ||--o{ USER_USAGE_LOGS : ""
    SYSTEM ||--o{ USERS : ""
    SYSTEM ||--o{ ADMINS : ""
    JWT ||--o{ EXCLUDE_INBOUNDS_ASSOCIATION : ""
    JWT ||--o{ PROXIES : ""
    JWT ||--o{ NODE_USER_USAGES : ""
    JWT ||--o{ NODES : ""
    JWT ||--o{ NOTIFICATION_REMINDERS : ""
    JWT ||--o{ USER_USAGE_LOGS : ""
    JWT ||--o{ USERS : ""
    JWT ||--o{ ADMINS : ""
    EXCLUDE_INBOUNDS_ASSOCIATION ||--o{ PROXIES : ""
    EXCLUDE_INBOUNDS_ASSOCIATION ||--o{ NODE_USER_USAGES : ""
    EXCLUDE_INBOUNDS_ASSOCIATION ||--o{ NODES : ""
    EXCLUDE_INBOUNDS_ASSOCIATION ||--o{ NOTIFICATION_REMINDERS : ""
    EXCLUDE_INBOUNDS_ASSOCIATION ||--o{ USER_USAGE_LOGS : ""
    EXCLUDE_INBOUNDS_ASSOCIATION ||--o{ USERS : ""
    EXCLUDE_INBOUNDS_ASSOCIATION ||--o{ ADMINS : ""
    PROXIES ||--o{ NODE_USER_USAGES : ""
    PROXIES ||--o{ NODES : ""
    PROXIES ||--o{ NOTIFICATION_REMINDERS : ""
    PROXIES ||--o{ USER_USAGE_LOGS : ""
    PROXIES ||--o{ USERS : ""
    PROXIES ||--o{ ADMINS : ""
    NODE_USER_USAGES ||--o{ NODES : ""
    NODE_USER_USAGES ||--o{ NOTIFICATION_REMINDERS : ""
    NODE_USER_USAGES ||--o{ USER_USAGE_LOGS : ""
    NODE_USER_USAGES ||--o{ USERS : ""
    NODE_USER_USAGES ||--o{ ADMINS : ""
    NODES ||--o{ NOTIFICATION_REMINDERS : ""
    NODES ||--o{ USER_USAGE_LOGS : ""
    NODES ||--o{ USERS : ""
    NODES ||--o{ ADMINS : ""
    NOTIFICATION_REMINDERS ||--o{ USER_USAGE_LOGS : ""
    NOTIFICATION_REMINDERS ||--o{ USERS : ""
    NOTIFICATION_REMINDERS ||--o{ ADMINS : ""
    USER_USAGE_LOGS ||--o{ USERS : ""
    USER_USAGE_LOGS ||--o{ ADMINS : ""
    USERS ||--|| ADMINS : ""
    INBOUNDS ||--o{ HOSTS : ""
    HOSTS ||--|| TLS : ""
    USER_TEMPLATES ||--o{ TEMPLATE_INBOUNDS_ASSOCIATION : ""
    TEMPLATE_INBOUNDS_ASSOCIATION ||--|| INBOUNDS : ""
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