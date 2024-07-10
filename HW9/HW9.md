## 1. Вывести в консоль список всех пользователей системы.
```console
vg@dev:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:997:997:systemd Time Synchronization:/:/usr/sbin/nologin
messagebus:x:100:107::/nonexistent:/usr/sbin/nologin
sshd:x:101:65534::/run/sshd:/usr/sbin/nologin
vg:x:1000:1000:vg,,,:/home/vg:/bin/bash

```
## 2. Найти и вывести в консоль домашние каталоги для текущего пользователя и root.
- Домашняя директория текущего пользователя
```console
vg@dev:~$ echo ~
/home/vg
```
- Домашняя директория root пользователя
```console
root@dev:~# echo ~
/root
```
## 3. Создать Bash скрипт get-date.sh, выводящий текущую дату.
- Скрипт
```console
#!/bin/bash
date
```
## 4. Запустить скрипт через ./get-date.sh и bash get-date.sh. Какой вариант не работает? Сделать так, чтобы оба варианта работали.
- Запуск через bash get-date.sh
```console
vg@dev:~$ bash get-date.sh
Wed Jul 10 11:05:54 AM +03 2024
```
- Второй вариант запуска ./get-date.sh не запускается так как у текущего пользователя нет прав на его выполнение
```console
vg@dev:~$ ./get-date.sh
-bash: ./get-date.sh: Permission denied
```
- Даём права на выполнение скрипта всем пользователям 
```console
vg@dev:~$ sudo chmod +x get-date.sh
```
- Запускаем скрипт
```console
vg@dev:~$ ./get-date.sh
Wed Jul 10 11:10:39 AM +03 2024
```
## 5. Создать пользователей alice и bob с домашними директориями и установить /bin/bash в качестве командной оболочки по умолчанию.
- Создаём пользователей
```console
vg@dev:~$ sudo useradd alice
vg@dev:~$ sudo useradd bob
```
- Проверяем их текущие домашние дирректории и оболочки
```console
vg@dev:~$ sudo useradd bob
vg@dev:~$ cat /etc/passwd | grep alice
alice:x:1001:1001::/home/alice:/bin/sh
vg@dev:~$ cat /etc/passwd | grep bob
bob:x:1002:1002::/home/bob:/bin/sh
```
- Меняем их оболочки с  /bin/sh на /bin/bash и проверяем
```console
vg@dev:~$ sudo chsh -s /bin/bash alice
vg@dev:~$ sudo chsh -s /bin/bash bob
vg@dev:~$ cat /etc/passwd | grep bob
bob:x:1002:1002::/home/bob:/bin/bash
vg@dev:~$ cat /etc/passwd | grep alice
alice:x:1001:1001::/home/alice:/bin/bash
```
## 6. Запустить интерактивную сессию от пользователя alice. Создать файл secret.txt с каким-нибудь секретом в домашней директории при помощи текстового редактора nano.
- Заходим в сессию alice
```console
vg@dev:~$ su alice
Password:
alice@dev:/home/vg$
```
- Создаём файл secret.txt в домашней дирректории
```console
alice@dev:/home/vg$ cd ~
alice@dev:~$ nano sercet.txt
alice@dev:~$ cat sercet.txt
secret
```
## 7. Вывести права доступа к файлу secret.txt.
```console
alice@dev:~$ ls -la sercet.txt
-rw-r--r-- 1 alice alice 7 Jul 10 11:38 sercet.txt
```
## 8. Выйти из сессии от alice и открыть сессию от bob. Вывести содержимое файла /home/alice/secret.txt созданного ранее не прибегая к команде sudo. В случае, если это не работает, объяснить.
- Так как у пользователя bob нет прав для чтения дирректории alice, он не может прочитать файл secret.txt
```console
bob@dev:~$ cat /home/alice/secret.txt
cat: /home/alice/secret.txt: Permission denied
```
##  9. Создать файл secret.txt с каким-нибудь секретом в каталоге /tmp при помощи текстового редактора nano.
```console
bob@dev:~$ nano /tmp/secret.txt
bob@dev:~$ cat /tmp/secret.txt
bob secret
```
## 10. Вывести права доступа к файлу secret.txt. Поменять права таким образом, чтобы этот файл могли читать только владелец и члены группы, привязанной к файлу.
- Права на файл
```console
bob@dev:~$ ls -la /tmp/secret.txt
-rw-r--r-- 1 bob bob 11 Jul 10 12:04 /tmp/secret.txt
```
- Изменяем права на файл
```console
bob@dev:~$ chmod 640 /tmp/secret.txt
bob@dev:~$ ls -la /tmp/secret.txt
-rw-r----- 1 bob bob 11 Jul 10 12:04 /tmp/secret.txt
```
## 11. Выйти из сессии от bob и открыть сессию от alice. Вывести содержимое файла /tmp/secret.txt созданного ранее не прибегая к команде sudo. В случае, если это не работает, объяснить.
- Выходим из сессии bob и заходим в сессию alice
```console
bob@dev:~$ exit
exit
vg@dev:~$ su alice
Password:
alice@dev:/home/vg$
```
- Выводим содержимое файла /tmp/secret.txt. Пользователь не может прочитать файл так как остальным пользователям, не состоящим в группе bob, закрыт доступ на чтение файла.
```console
alice@dev:/home/vg$ cat /tmp/secret.txt
cat: /tmp/secret.txt: Permission denied
```
## 12. Добавить пользователя alice в группу, привязанную к файлу /tmp/secret.txt.
```console
vg@dev:~$ sudo usermod -a -G bob alice
[sudo] password for vg:
vg@dev:~$ su alice
Password:
alice@dev:/home/vg$ groups
alice users bob
```
## 13. Вывести содержимое файла /tmp/secret.txt.
```console
alice@dev:/home/vg$ cat /tmp/secret.txt
bob secret
```
## 14. Скопировать домашнюю директорию пользователя alice в директорию /tmp/alice с помощью rsync.
```console
alice@dev:/tmp$ rsync -r /home/alice/ /tmp/alice
```
```console
alice@dev:/tmp/alice$ ls -la /tmp
total 44
drwxrwxrwt 10 root  root  4096 Jul 10 14:47 .
drwxr-xr-x 18 root  root  4096 Jul  2 16:42 ..
drwx------  3 alice alice 4096 Jul 10 14:47 alice
drwxrwxrwt  2 root  root  4096 Jul 10 10:57 .font-unix
drwxrwxrwt  2 root  root  4096 Jul 10 10:57 .ICE-unix
-rw-rw----  1 bob   bob     11 Jul 10 12:04 secret.txt
```
## 15. Скопировать домашнюю директорию пользователя alice в директорию /tmp/alice на другую VM по SSH с помощью rsync. Как альтернатива, можно скопировать любую папку с хоста на VM по SSH (scp).
```console
alice@dev:/tmp/alice$ scp -r /home/alice/ zabbix@192.168.192.168:/tmp/alice
zabbix@192.168.192.168's password:
.profile                                           100%  807     1.3MB/s   00:00
.bash_history                                      100%  164   407.7KB/s   00:00
.bashrc                                            100% 3526     5.4MB/s   00:00
secret                                             100%    7    11.5KB/s   00:00
.bash_logout                                       100%  220   460.2KB/s   00:00
known_hosts                                        100%  364   542.2KB/s   00:00
known_hosts.old                                    100%  142   291.9KB/s   00:00
```
- Содержимоей папки на другом сервере
```console
zabbix@zabbix:/tmp$ ls -la /tmp/alice/
total 12
drwxrwxr-x  3 zabbix zabbix 4096 Jul 10 14:59 .
drwxrwxrwt 12 root   root   4096 Jul 10 15:00 ..
drwx------  4 zabbix zabbix 4096 Jul 10 14:59 alice
```
## 16. Удалить пользователей alice и bob вместе с домашними директориями.
```console
vg@dev:~$ sudo userdel bob -r
[sudo] password for vg:
userdel: group bob not removed because it has other members.
userdel: bob mail spool (/var/mail/bob) not found
vg@dev:~$ sudo userdel alice -r
userdel: alice mail spool (/var/mail/alice) not found
vg@dev:~$ ls -la /home/
total 12
drwxr-xr-x  3 root root 4096 Jul 10 15:03 .
drwxr-xr-x 18 root root 4096 Jul  2 16:42 ..
drwx------  3 vg   vg   4096 Jul 10 11:17 vg
```
## 17. С помощью утилиты htop определить какой процесс потребляет больше всего ресурсов в системе.
- Устанавливаем htop
```console
vg@dev:~$ sudo apt install htop
```
- Отсторировав список процессов по CPU, видим что первое место делят два процесса vmtoolsd и htop
![Потребление cpu](/HW9/images/htop.png)

## 18. Вывести логи сервиса Firewall с помощью journalctl не прибегая к фильтрации с помощью grep.
- Фильтруем журнал по определённому юниту
```console
root@dev:~# journalctl -u ufw
Jul 10 15:14:51 dev systemd[1]: Starting ufw.service - Uncomplicated firewall...
Jul 10 15:14:51 dev systemd[1]: Finished ufw.service - Uncomplicated firewall.
```
