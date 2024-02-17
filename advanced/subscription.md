---
order: 1000
label: Система подписки
icon: people
---

# Система подписки
{% hint style="warning" %}
Статья находится в режиме написания. Со временем будет дополняться и изменяться. 
{% endhint %}
Marzban включает в себя уникальную возможность, предоставления конфигов для подключения пользователя в удобном формате - так называемая система подписки.

## Ссылка
Подписка доступна для пользователя по опредленному пути (ссылке), которая складывается из следующих частей:
```
https://{XRAY_SUBSCRIPTION_URL_PREFIX}/{XRAY_SUBSCRIPTION_PATH}/{JWT_TOKEN}/{KEY}
```
{% hint style="danger" %}
Используйте только `https`
{% endhint %}
Разберем составляющие этой ссылки:

### XRAY_SUBSCRIPTION_URL_PREFIX
{% hint style="info" %}
Является обязательным значением.
{% endhint %}

Префикс адреса подписки. 

Значение задается в `.env`

Пример: `"https://domain.com"`

В случае, если Вы используете wildcard домены, Вы можете определить соль для  XRAY_SUBSCRIPTION_URL_PREFIX. 

Пример: `"https://*.domain.com"`

Получив при генерации случайную строку (соли) длиной 16 символов

Пример: `"830aa395df41ae5a.domain.com"` или `"b7559f58668ab457.domain.com"` 


### XRAY_SUBSCRIPTION_PATH
{% hint style="info" %}
Является обязательным значением.
{% endhint %}

Префикс адреса подписки. 

Значение задается в `.env`

значение по умолчанию: `sub` 

Пример: `"sub"`

### JWT_TOKEN
{% hint style="info" %}
Является обязательным значением.
{% endhint %}

JWT токен

Значение генерируется автоматически

Пример: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJZdWV1IiwiYWNjZXNzIjoic3Vic2NyaXB0aW9uIiwiaWF0IjoxNzA3NTc5ODU3fQ.gSKSElCKb_8eZ8AeXGDh6r_ylg7KZQG6xlN-j2lDY6A`

### KEY
{% hint style="info" %}
Опциональное значение
{% endhint %}
С помощью обьявленных в конце ссылки ключей, Вы можете воспользоваться дополнительными возможностями

#### /info
```
https://{XRAY_SUBSCRIPTION_URL_PREFIX}/{XRAY_SUBSCRIPTION_PATH}/{JWT_TOKEN}/info
```
Формат вывода: JSON

C помощью данного ключа Вы можете получить всю информацию о пользовательской подписке, включая все данные сущности `user` этого пользователя.
#### /usage
```
https://{XRAY_SUBSCRIPTION_URL_PREFIX}/{XRAY_SUBSCRIPTION_PATH}/{JWT_TOKEN}/usage
```
Формат вывода: JSON

C помощью данного ключа Вы можете получить всю информацию о потребленном трафике пользователя, включая все данные узлов.
#### /CLIENT_TYPE
```
https://{XRAY_SUBSCRIPTION_URL_PREFIX}/{XRAY_SUBSCRIPTION_PATH}/{JWT_TOKEN}/{CLIENT_TYPE}
```
Доступные типы клиентов: `sing-box`,`clash-meta`,`clash`,`outline`,`v2ray`

Получение опредленного типа подписки, сгенерированного для указанного потребителя 

## Подписка 
Система подписки, динамически отдает содержимое в зависимости  от USER-Agent устройства от которого поступает запрос.

Ниже, мы рассмотрим все доступные варианты:

### WEB
При запросе к ссылке через веб браузер, на выходе, Вы получите рендер шаблона по умолчанию (или заданного Вами, кастомного шаблона) в виде html файла.
[!ref target="blank" text="Шаблон по умолчанию"](https://github.com/Gozargah/Marzban/blob/master/app/templates/subscription/index.html)
Для применения собственного шаблона, Вам необходимо использовать 2 перменные в файле `.env`:
- `CUSTOM_TEMPLATES_DIRECTORY`
- `SUBSCRIPTION_PAGE_TEMPLATE`

В данном виде шаблона для рендера используется шаблонизатор jinja, с полной поддержкой его синтаксиса.

Доступная сущность для взаимодействия: `user`

Пример: 
```html
<center>
{% if user.status == 'active' %}
    <b>Ваша подписка активна</b>
 {% endif %}
</center>
```
### V2ray
При запросе к ссылке через v2ray клиенты, или с испольованием ключа `/v2ray`, на выходе, Вы получите сгенериванный plain текст, c закодированными в base64 ссылками подключения
```
{protocol}://{detailts}
{protocol}://{detailts}
```  
Так же, вместе с ссылками, будут переданны заголовки, которые, в свою очередь, в том или инном обьеме, будут интерпретированы клиентом.
#### profile-web-page-url
Заголовок включающий ссылку-подписки

Пример:
```
profile-web-page-url: https://{XRAY_SUBSCRIPTION_URL_PREFIX}/{XRAY_SUBSCRIPTION_PATH}/{JWT_TOKEN}
```
#### support-url
Заголовок включающий ссылку позволяющая пользователю перейти на соответствующую домашнюю страницу.

Для применения собственного значения, Вам необходимо задать перменную `SUB_SUPPORT_URL` в файле `.env`:

Пример:
```
support-url: https://mybestvpnintheworld.com
```
#### profile-title
Имя профиля в кодировке base64 UTF8

Пример:
```
profile-title: base64:0YXRg9C5
```
#### profile-update-interval
Интервал автоматического обновления файла конфигурации

Для применения собственного значения, Вам необходимо задать перменную `SUB_UPDATE_INTERVAL` в файле `.env`:

Пример:
```
profile-update-interval: 1
```
#### subscription-userinfo
Информация о трафике и истечении срока действия

Значения генерируются автоматическии

Пример:
```
subscription-userinfo: upload=0; download=4460105213; total=2147483648; expire=1710442799
```
### Sing-Box
При запросе к ссылке через клиент на базе Sing-box, или с испольованием ключа `/sing-box`, пользователь получит валидный json, построенный на шаблоне 
[!ref target="blank" text="Шаблон по умолчанию"](https://github.com/Gozargah/Marzban/blob/master/app/templates/singbox/default.json)
Для применения собственного шаблона, Вам необходимо использовать 2 перменные в файле `.env`:
- `CUSTOM_TEMPLATES_DIRECTORY`
- `SINGBOX_SUBSCRIPTION_TEMPLATE`

### Clash
[!ref target="blank" text="Шаблон по умолчанию"](https://github.com/Gozargah/Marzban/blob/master/app/templates/clash/default.yml )
### OUTLINE

