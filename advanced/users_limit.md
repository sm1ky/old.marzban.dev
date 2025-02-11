---
order: 897
label: Ограничение пользователей
icon: people
---

Вы можете ограничить количество подключений с одного конфига несколькими способами, и их способы функционирования полностью различаются.

## V2IpLimit
{% hint style="warning" %}
Для корректной работы вне Ирана, требуется [Фикс](https://github.com/houshmand-2005/V2IpLimit/issues/18)
{% endhint %}

[!file](/static/fix_v2_ip_limit.zip)
Получить значение `DATE_TIME_ZONE` можно [тут](https://ip-api.com/)


Этот скрипт,  для ограничения IP в Marzban, работает следующим образом: если количество подключенных IP-адресов для пользователя превышает установленный вами лимит, эта учетная запись будет отключена на указанный период времени, а затем снова активирована после истечения этого времени.

[https://github.com/houshmand-2005/V2IpLimit](https://github.com/houshmand-2005/V2IpLimit)


## luIP-marzban

Этот скрипт работает иначе. Например, если ограничение IP установлено на одно подключение, и два пользователя пытаются подключиться к одной учетной записи, второй IP будет заблокирован через таблицу IP на указанный период времени, но первый IP останется подключенным. Таким образом,  будет отключен только второй пользователь, а не будет отключена вся учетная запись

[https://github.com/mmdzov/luIP-marzban](https://github.com/mmdzov/luIP-marzban)

## RU_luIP-UFW

Этот скрипт является прямым продолжением предыдущего, но с применением UFW и множеством других отличных изменений.

[https://github.com/sm1ky/luIP-marzban/tree/main](https://github.com/sm1ky/luIP-marzban/tree/main)

[https://github.com/sm1ky/luIP-marzban-node/tree/main](https://github.com/sm1ky/luIP-marzban-node/tree/main)
