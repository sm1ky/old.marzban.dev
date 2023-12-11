---
order: 892
label: Установка xanmod kernel
icon: tools
---

Для того, что бы воспользоваться BBR3, Вам нужно перейти на ядро XanMod kernel.

{% hint style="warning" %}
Вы должны понимать что меняете ЯДРО
{% endhint %}

## Авто установка
![](/static/xanmod.jpg)
Для установки Вы можете воспользоваться двумя простыми скриптами

Устанавливаем ядро
```bash
sudo python3 -c "$(curl -sL https://s3.marzban.ru/scripts/optimiser/xanmod_install.py)"
``` 
перезагрузка
```bash
reboot now
```
Применяем изменения
```bash
sudo python3 -c "$(curl -sL https://s3.marzban.ru/scripts/optimiser/xanmod_apply.py)"
``` 


## Ручная установка
Добавляем Ключ
```bash
wget -qO - https://gitlab.com/afrd.gpg | sudo gpg --dearmor -o /usr/share/keyrings/xanmod-archive-keyring.gpg
``` 
Добавляем репо
```bash
echo 'deb [signed-by=/usr/share/keyrings/xanmod-archive-keyring.gpg] http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-release.list
``` 
Устанавливаем ядро
```bash
sudo apt update && sudo apt install linux-xanmod-x64v3
``` 
перезагрузка
```bash
reboot now
```
Подгружаем модули
```bash
depmod -a
``` 
Проверяем корректность загрузки модуля
```bash
modinfo tcp_bbr
```  	
Открываем файл
```bash
sudo nano /etc/sysctl.conf
```  	
Добавляем необходимые переменные
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```  	
Выполняем
```bash
sysctl -p
```  	