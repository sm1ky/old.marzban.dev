# Переход на MySQL

Если у Вас есть потребность в использовании базы данных MySQL, а не SQLite, Вы можете сделать следующим образом

Обновление Linux:

```bash
apt-get update
```

Изменение содержимого файла `docker-compose.yml`:

```bash
nano /opt/marzban/docker-compose.yml
```

Замените содержимое файла на&#x20;

```yaml
services:
  marzban:
    image: gozargah/marzban:latest
    restart: always
    env_file: .env
    network_mode: host
    volumes:
      - /var/lib/marzban:/var/lib/marzban
    depends_on:
      - mysql

  mysql:
    image: mysql:latest
    restart: always
    env_file: .env
    network_mode: host
    command: --bind-address=127.0.0.1 --mysqlx-bind-address=127.0.0.1
    environment:
      MYSQL_DATABASE: marzban
    volumes:
      - /var/lib/marzban/mysql:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    restart: always
    env_file: .env
    network_mode: host
    environment:
      PMA_HOST: 127.0.0.1
      APACHE_PORT: 8010
    depends_on:
      - mysql

```

Обновление Marzban

```
marzban update
```

Перезагрузка Marzban

```
marzban restart
```

Подождите 1 минуту, пока старая база данных не будет перенесена (Если вы видите ошибку, игнорируйте ее)

Подключение к базе данных mysql и удаление соединения с помощью sqlite:

Откройте файл окружения

```bash
nano /opt/marzban/.env
```

Прокомментируйте строку ниже `#SQLALCHEMY_DATABASE_URL="sqlite:////var/lib/marzban/db.sqlite3"`

Поместите следующий код в `env` и введите желаемый пароль вместо слова `DB_PASSWORD` (повторяется дважды).

`SQLALCHEMY_DATABASE_URL = "mysql+pymysql://root:DB_PASSWORD@127.0.0.1/marzban"`&#x20;

`MYSQL_ROOT_PASSWORD = DB_PASSWORD`

Остановите и запустите Marzban и подождите 1 минуту (не обращайте внимания на ошибки)

```bash
marzban restart
```

Создание дампа из старой базы:

```bash
sqlite3 /var/lib/marzban/db.sqlite3 '.dump --data-only' | sed "s/INSERT INTO \([^ ]*\)/REPLACE INTO \ \\1\ /g " > /tmp/dump.sql
```

Представляем путь дампа к mysql:

```
cd /opt/marzban && docker compose cp /tmp/dump.sql mysql:/dump.sql
```

Переносим данные из sqlite в mysql:

```bash
docker compose exec mysql mysql -u root -p -h 127.0.0.1 marzban -e "SET FOREIGN_KEY_CHECKS = 0; SET NAMES utf8mb4; SOURCE dump.sql;"
```

Введите свой пароль, чтобы начать процесс изменения базы данных

После окончания работы перезапустите Marzban

Адрес панели phpmyadmin (управление базой данных): `http://ваш домен:8010`

Будьте внимательны, чтобы адрес страницы не содержал https.
