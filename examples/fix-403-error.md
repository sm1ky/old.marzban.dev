# Исправляем ошибку 403

## Отключаем IPv6 <a href="#disable-ipv6" id="disable-ipv6"></a>

При получении ошибки 403 на различных сайтах, настоятельно рекомендую отключить IPv6 на вашем сервере.

Открываем `sysctl.conf`

```bash
sudo nano /etc/sysctl.conf
```

Добавляем (изменяем) запись запрещающую использование IPv6 на всех адаптерах

```bash
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1
```

Для применения изменений перезапускаем `sysctl`&#x20;

```bash
sudo sysctl -p
```
