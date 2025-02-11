---
label: Пользовательский шаблон
icon: person
---
С помощью этого руководства вы можете создать пользовательские шаблоны для Telegram бота и на основе шаблонов создавать или редактировать пользователей Marzban.

Для начала, заходим на сервер, где установлен Marzban и открываем конфигурационный файл:

```bash
nano /opt/marzban/.env
```

Убираем комментарий `#` со строчки `DOCS=TRUE`, сохраняем файл:
![](</static/old/image (13).png>)


Перезагружаем marzban:

```bash
marzban restart
```

Далее, в браузере переходим по адресу `https:/YOUR_DOMAIN.COM/docs`

Нажимаем на кнопку авторизации и вводим свои данные администратора:
![](</static/old/image (16).png>)

![](</static/old/image (15).png>)


Идем в раздел «`user_templates`» И выбираем «`Add User Template`». Внутри открытого спойлера нажимаем  «`Try it out`»
![](</static/old/image (2).png>)

Вводим конфигурацию для пользовательского шаблона:

Например:

```json
{
  "name": "30days/ unlimited gb",
  "inbounds": {
    "vless": [
      "VLESS TCP REALITY"
    ]
  },
  "data_limit": 0,
  "expire_duration": 2592000,
  "username_prefix": "prefix",
  "username_suffix": "suffix"
}

```

где:

`«name»` - имя шаблона пользователя. В дальнейшем, оно будет отображаться в Telegram боте.

`«inbounds»` - теги inbounds, которые мы хотим добавить к пользовательскому шаблону. В данном случае, пользователь будет создаваться с VLESS TCP REALITY.

`«data_limit»` - ограничения по размеру трафика (в байтах). Например, 10 Гигабайт = 10737418240 Байт.  Значение «0» не ставит ограничения. Если строчку убрать совсем, то ограничений также не будет.

`«expire_duration»` - срок подписки пользователя (в секундах). Например, 30 дней = 2592000 секундам. Значение «0» не ставит ограничения. Если строчку убрать совсем, то ограничений также не будет.

`«username_prefix»` и `«username_suffix»` - это префикс и суффикс, которые, соответственно, будут добавляться к имени пользователя в начале и в конце. Например: `«prefix_username_suffix»`, где  `«username»` — имя пользователя,  `«prefix_»` — префикс и  `«_suffix»` – суффикс, соответственно. Префикс и суффикс также не являются обящательными полями при создании шаблона пользователя и строки с ними можн оне добавлять, если в этом нет необходимости.



Как только закончили править шаблон, нажимаем на «`Execute`» и шаблон сохраняется в базу данных и его можно использовать в Telegram боте:
![](</static/old/image (26).png>)

Далее, нам необходим рабочий Telegram бот Marzban. Если он уже установлен, можно переходить к следующего шагу.

Для установки Telegram бота:

Открываем конфигурационный файл Marzban:

```bash
nano /opt/marzban/.env
```

Вводим данные от своего бота, созданного в @BotFather

Ваш ID профиля можно узнать у бота @getmyid\_bot

```
TELEGRAM_API_TOKEN = YOUR_BOT_TOKEN
TELEGRAM_ADMIN_ID = YOUR_ID
```

Переходим в бота и нажимаем «`Create User From Template`»:
![](</static/old/image (18).png>)

Выбираем созданный ранее шаблон пользователя:
![](</static/old/image (19).png>)

Вводим имя пользователя или генерируем рандомное:
![](</static/old/image (22).png>)

После отправки имени пользователя, проверяем данные и нажимаем «`Done`»:
![](</static/old/image (23).png>)

Готово! Пользователь по шаблону создан. Теперь он должен отобразиться как в боте, так и в самой панели Marzban:
![](</static/old/image (24).png>)