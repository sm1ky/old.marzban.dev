---
order: 897
label: Переход на DEV  версию
icon: git-branch
---

С помощью данного руководства Вы сможете перейти на версию Marzban для разработчиков

{% hint style="danger" %}
В версии для разработчиков возможны ошибки, если вы хотите избежать их - не переходите на неё.
{% endhint %}

## Введение <a href="#intro" id="intro"></a>

Панель Marzban имеет две версии:

**`LATEST`** - Версия Marzban по умолчанию, является самой стабильной версией. &#x20;

Вы можете увидеть последние изменения последней версии по ссылке ниже:

[https://github.com/Gozargah/Marzban/commits/master](https://github.com/Gozargah/Marzban/commits/master)

**`DEV`** - Версия Marzban для разработчиков.  является постоянно изменяющейся версией, для тестирования всех новых функций, которые попадут в стабильную **`LATEST`** версию

Вы можете увидеть последние изменения в версии для разработчиков по ссылке ниже.

[https://github.com/Gozargah/Marzban/commits/dev](https://github.com/Gozargah/Marzban/commits/dev)

## Переход на версию для разработчиков (dev) <a href="#change-version" id="change-version"></a>

Войдите на свой сервер и выполните следующие команды

```bash
cd /opt/marzban
```

```bash
nano docker-compose.yml
```

Измените третью строку с `marzban:latest` на `marzban:dev`  и сохраните изменения

выполните обновление

```bash
marzban update 
```
