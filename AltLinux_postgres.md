# Установка и настройка 

## Системные требования

```bash
~# cat /etc/os-release
NAME="ALT SPServer"
VERSION="8.2"
ID=altlinux
VERSION_ID=8.2
PRETTY_NAME="ALT 8 SP Server (cliff)"
ANSI_COLOR="1;33"
CPE_NAME="cpe:/o:alt:spserver:8.2"

# uname -a
Linux db-pgsql-n01 5.4.68-std-def-alt1.4.c9f #1 SMP Thu Nov 19 04:35:08 UTC 2020 x86_64 GNU/Linux
```

В случае работы на Virtualbox и подобных при клонировании машины могут смениться наименования сетевых интерфейсов. Чтобы этого избежать, нужно выполнить: 

```bash
~# rm -f /etc/udev/rules.d/70-persistent-net.rules
~# sudo ln -s /dev/null /etc/udev/rules.d/70-persistent-net.rules
```

Рекомендовано под данные СУБД выделить отдельный диск.

## Установка обновлений и пакетов

```bash 
~# su -
~# apt-get update && apt-get --enable-upgrade upgrade -y && apt-get install sudo nano tmux tzdata wget atop htop sysstat 
~# apt-get install gcc python3-dev python3-module-pip python3-module-setuptools -y
```