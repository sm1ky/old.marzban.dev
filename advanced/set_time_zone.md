---
order: 893
label: Установка часового пояса
icon: clock
---

Для корректного отображения информации в панели, нам необходимо установить привычный для нас часовой пояс.


Устанавливаем часовой пояс, в данном примере Москва 

```bash
timedatectl set-timezone Europe/Moscow
```

Открываем файл docker-compose.yml
```bash
nano /var/lib/marzban/docker-compose.yml
```

добавляем значение `/etc/localtime:/etc/localtime:ro` в раздел `volumes`
![](/static/time.jpg)
```yaml

...
	volumes:
		- /etc/localtime:/etc/localtime:ro
...

```


Перезагружаем контейнер 
```bash
marzban restart
``` 