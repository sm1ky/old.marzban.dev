# Сниппеты

На данной странице приведены короткие примеры, формат которых не позволяет публикацию в отдельную статью

## Фикс двустороннего пинга

Вы пытаетесь максимально замаскировать свой VPN ? Тогда вам наверняка необходимо убрать определение туннеля (двусторонний пинг).

Переходим к редактированию настроек ufw c помощью nano:

```
nano /etc/ufw/before.rules
```

Добавляем новую строку(а если они уже есть, то меняем значение) и сохраняем результат:

```
# ok icmp codes
-A ufw-before-input -p icmp --icmp-type destination-unreachable -j DROP
-A ufw-before-input -p icmp --icmp-type source-quench -j DROP
-A ufw-before-input -p icmp --icmp-type time-exceeded -j DROP
-A ufw-before-input -p icmp --icmp-type parameter-problem -j DROP
-A ufw-before-input -p icmp --icmp-type echo-request -j DROP
```

Перезапускаем фаервол ufw

```
ufw disable && ufw enable
```

## Получение ключей для Reality

Выполняем команду

```
docker exec marzban-marzban-1 xray x25519
```

На выходе получаем связку ключей private/public, которые Вы можете указать в  xray\_core

## &#x20;Генерация ShortID для Reality

Выполните команду для генерации правильных коротких идентификаторов

```
openssl rand -hex 8
```
