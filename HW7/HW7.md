## 1. Ознокомился с веб-приложением
- backend
- frontend
## 2. Ознокомился с вариантами хостинга этого веб-приложения:

## 3. Установить веб-приложение (backend + frontend) на Linux VM и настроить запуск через SystemD
- Устанавливаем гит на сервер
```console
root@dev:~# apt install git
```
- Забираем фронтэнд и бэкэнд из github
```console
root@dev:~# git clone https://github.com/bezkoder/django-rest-api.git
root@dev:~# git clone https://github.com/bezkoder/react-crud-web-api.git
```
- Устанавливаем недостающие пакеты 
```console
root@dev:~# apt update -y && sudo apt upgrade -y
root@dev:~# apt install python3 python3-pip -y
root@dev:~# apt install dnsutils systemd systemd-cron curl nginx -y
root@dev:~# apt install npm -y
root@dev:~# sudo curl -fsSL https://deb.nodesource.com/setup_18.x | sudo bash -
root@dev:~# sudo apt install nodejs -y
root@dev:~# pip install Django==3.2.10 django-cors-headers djangorestframework --break-system-packages
```
- Создаём понятную структуру папок для приложения
```console
root@dev:~# mkdir /etc/bezkoder
root@dev:~# mkdir /etc/bezkoder/frontend
root@dev:~# mkdir /etc/bezkoder/backend
root@dev:~# cp -r django-rest-api/. /etc/bezkoder/backend
root@dev:~# cp -r react-crud-web-api/. /etc/bezkoder/frontend/

```
- Создаём юзера под которым будет работать демон и даём ему права на базу данных
```console
root@dev:~# adduser bezkoder
root@dev:~# chown bezkoder:bezkoder /etc/bezkoder/backend/DjangoRestApi/db.sqlite3 /etc/bezkoder/backend/DjangoRestApi/
```
- Создаём демона
```console
root@dev:~# cd /etc/systemd/system
root@dev:/etc/systemd/system# cat bezkoder.service
[Unit]
Description=backend service bezkoder
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
WorkingDirectory=/etc/bezkoder/backend/DjangoRestApi
ExecStartPre=python3 manage.py migrate
ExecStart=python3 manage.py runserver 0.0.0.0:8080
User=bezkoder

[Install]
WantedBy=multi-user.target
```
- Запускаем демона и проверяем его работу
```console
root@dev:/etc/systemd/system# systemctl enable bezkoder.service
Created symlink /etc/systemd/system/multi-user.target.wants/bezkoder.service → /etc/systemd/system/bezkoder.service.
root@dev:/etc/systemd/system# systemctl start bezkoder.service
root@dev:/etc/systemd/system# systemctl status bezkoder.service
● bezkoder.service - backend service bezkoder
     Loaded: loaded (/etc/systemd/system/bezkoder.service; disabled; preset: enabled)
     Active: active (running) since Thu 2024-07-04 11:20:58 +03; 4s ago
    Process: 10832 ExecStartPre=python3 manage.py migrate (code=exited, status=0/SUCCESS)
   Main PID: 10833 (python3)
      Tasks: 3 (limit: 4644)
     Memory: 73.9M
        CPU: 1.799s
     CGroup: /system.slice/bezkoder.service
             ├─10833 python3 manage.py runserver 0.0.0.0:8080
             └─10834 /usr/bin/python3 manage.py runserver 0.0.0.0:8080
Jul 04 11:20:58 dev python3[10832]:   Applying auth.0011_update_proxy_permissions... OK
Jul 04 11:20:58 dev python3[10832]:   Applying auth.0012_alter_user_first_name_max_length... OK
Jul 04 11:20:58 dev python3[10832]:   Applying sessions.0001_initial... OK
Jul 04 11:20:58 dev systemd[1]: Started bezkoder.service - backend service bezkoder.
Jul 04 11:20:59 dev python3[10834]: Watching for file changes with StatReloader
Jul 04 11:20:59 dev python3[10834]: System check identified some issues:
Jul 04 11:20:59 dev python3[10834]: WARNINGS:
Jul 04 11:20:59 dev python3[10834]: tutorials.Tutorial: (models.W042) Auto-created primary key used when not defining a primary key type, by default 'django.db.models.AutoFi>
Jul 04 11:20:59 dev python3[10834]:         HINT: Configure the DEFAULT_AUTO_FIELD setting or the TutorialsConfig.default_auto_field attribute to point to a subclass of Auto>
Jul 04 11:20:59 dev python3[10834]: System check identified 1 issue (0 silenced).
...skipping...
● bezkoder.service - backend service bezkoder
     Loaded: loaded (/etc/systemd/system/bezkoder.service; disabled; preset: enabled)
     Active: active (running) since Thu 2024-07-04 11:20:58 +03; 4s ago
    Process: 10832 ExecStartPre=python3 manage.py migrate (code=exited, status=0/SUCCESS)
   Main PID: 10833 (python3)
      Tasks: 3 (limit: 4644)
     Memory: 73.9M
        CPU: 1.799s
     CGroup: /system.slice/bezkoder.service
             ├─10833 python3 manage.py runserver 0.0.0.0:8080
             └─10834 /usr/bin/python3 manage.py runserver 0.0.0.0:8080

Jul 04 11:20:58 dev python3[10832]:   Applying auth.0011_update_proxy_permissions... OK
Jul 04 11:20:58 dev python3[10832]:   Applying auth.0012_alter_user_first_name_max_length... OK
Jul 04 11:20:58 dev python3[10832]:   Applying sessions.0001_initial... OK
Jul 04 11:20:58 dev systemd[1]: Started bezkoder.service - backend service bezkoder.
Jul 04 11:20:59 dev python3[10834]: Watching for file changes with StatReloader
Jul 04 11:20:59 dev python3[10834]: System check identified some issues:
Jul 04 11:20:59 dev python3[10834]: WARNINGS:
Jul 04 11:20:59 dev python3[10834]: tutorials.Tutorial: (models.W042) Auto-created primary key used when not defining a primary key type, by default 'django.db.models.AutoFi>
Jul 04 11:20:59 dev python3[10834]:         HINT: Configure the DEFAULT_AUTO_FIELD setting or the TutorialsConfig.default_auto_field attribute to point to a subclass of Auto>
Jul 04 11:20:59 dev python3[10834]: System check identified 1 issue (0 silenced).

```
- Ошибка при запуске backend
![Ошибка при запуске backend](/HW7/images/backend_start_error.png)

- Для исправления ошибки вносим изменения в файл по пути etc/bezkoder/backend/DjangoRestApi/DjangoRestApi/settings.py

```console
root@dev:/etc/systemd/system# nano /etc/bezkoder/backend/DjangoRestApi/DjangoRestApi/settings.py

ALLOWED_HOSTS = ['192.168.120.133'] # Добавляем свой IP
```
- Вывод страницы после исправления ошибки
![Ошибка при запуске backend](/HW7/images/hw7_backend.png)

- Настраиваем frontend

```console
root@dev:~$ sudo sed -i "s/try_files \$uri \$uri\/ =404;/try_files \$uri \$uri\/ \$uri.html \/index.html;/" /etc/nginx/sites-available/default
root@dev:~$ cd /etc/bezkoder/frontend
root@dev:/etc/bezkoder/frontend$ sudo npm install
root@dev:/etc/bezkoder/frontend$ sudo npm run build
root@dev:/etc/bezkoder/frontend$ sudo cp -r /etc/bezkoder/frontend/build/. /var/www/html
root@dev:/etc/bezkoder/frontend$ sudo npm start
```
- Проверяем запуск фронтенда

![Старт npm](/HW7/images/hw7_npm.png)
![Проверка frontend](/HW7/images/hw7_frontend.png)

## 4. (**) Познакомиться с инструментом для создания образов VM - Packer - на примерах создания образов для Virtualbox & Hyper-V. Попробовать написать свой шаблон для создания образа VM.



