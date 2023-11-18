---
order: 886
label: API
icon: beaker
---
## Описание 
![](/static/19.png)
Marzban предоставляет REST API, который позволяет разработчикам программно взаимодействовать со службами Marzban. Чтобы просмотреть документацию по API в Swagger UI или ReDoc, установите переменную в файле env:

```bash
nano /opt/marzban/.env
```

Изменяем в нем следующие переменные

```
`DOCS=True`
```
Перейдите в браузере  `http://YOUR_DOMAIN/docs` или `http://YOUR_DOMAIN/redoc`.
