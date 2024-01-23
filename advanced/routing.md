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
%%{init: { 'theme': 'neutral' }}%%
graph LR

    S(запрос) .-> I[inbound]

    subgraph Xray
    I --> R[Маршрутизация] --> O[outbound]
    end

    O .-> V(запрос)

    V:::greyclass
    S:::greyclass
    R:::routingclass
    classDef greyclass fill:#C0C0C0
    classDef routingclass fill:#FFFFDE
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