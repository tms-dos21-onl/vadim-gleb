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
root@dev:~# mkdir /app/bezkoder
root@dev:~# mkdir /app/bezkoder/frontend
root@dev:~# mkdir /app/bezkoder/backend
root@dev:~# cp -r django-rest-api/. /app/bezkoder/backend
root@dev:~# cp -r react-crud-web-api/. /eapp/bezkoder/frontend/

```
- Создаём юзера под которым будет работать демон и даём ему права на базу данных
```console
root@dev:~# adduser bezkoder
root@dev:~# chown bezkoder:bezkoder /app/bezkoder/backend/DjangoRestApi/db.sqlite3 /app/bezkoder/backend/DjangoRestApi/
```
- Создаём демона
```console
[Unit]
Description=bezkoder backend app

[Service]
Restart=on-failure
WorkingDirectory=/app/bezkoder/backend/DjangoRestApi
ExecStartPre=python3 manage.py migrate
ExecStart=python3 manage.py runserver 0.0.0.0:8080
User=backend

[Install]
WantedBy=multi-user.target

```
- Запускаем демона и проверяем его работу
```console
root@dev:/etc/systemd/system# systemctl enable bezkoder.service
Created symlink /etc/systemd/system/multi-user.target.wants/bezkoder.service → /etc/systemd/system/bezkoder.service.
root@dev:/etc/systemd/system# systemctl start bezkoder.service
root@dev:/etc/systemd/system# systemctl status bezkoder.service
vg@dev:/app/bezkoder/backend/DjangoRestApi$ sudo systemctl status  bezkoder.back.service
● bezkoder.back.service - bezkoder backend app
     Loaded: loaded (/etc/systemd/system/bezkoder.back.service; enabled; preset: enabled)
     Active: active (running) since Thu 2024-07-04 13:55:20 +03; 39s ago
    Process: 10366 ExecStartPre=python3 manage.py migrate (code=exited, status=0/SUCCESS)
   Main PID: 10367 (python3)
      Tasks: 5 (limit: 4644)
     Memory: 70.4M
        CPU: 2.561s
     CGroup: /system.slice/bezkoder.back.service
             ├─10367 python3 manage.py runserver 0.0.0.0:8080
             └─10368 /usr/bin/python3 manage.py runserver 0.0.0.0:8080

Jul 04 13:55:19 dev python3[10366]:   Applying auth.0008_alter_user_username_max_length... OK
Jul 04 13:55:19 dev python3[10366]:   Applying auth.0009_alter_user_last_name_max_length... OK
Jul 04 13:55:19 dev python3[10366]:   Applying auth.0010_alter_group_name_max_length... OK
Jul 04 13:55:19 dev python3[10366]:   Applying auth.0011_update_proxy_permissions... OK
Jul 04 13:55:19 dev python3[10366]:   Applying auth.0012_alter_user_first_name_max_length... OK
Jul 04 13:55:19 dev python3[10366]:   Applying sessions.0001_initial... OK
Jul 04 13:55:19 dev python3[10366]:   Applying tutorials.0002_alter_tutorial_id... OK
Jul 04 13:55:20 dev systemd[1]: Started bezkoder.back.service - bezkoder backend app.
Jul 04 13:55:20 dev python3[10368]: Watching for file changes with StatReloader
Jul 04 13:55:46 dev python3[10368]: [04/Jul/2024 10:55:46] "GET /api/tutorials HTTP/1.1" 200 304
```

- Для исправления ошибки при запуске backend вносим изменения в файл по пути etc/bezkoder/backend/DjangoRestApi/DjangoRestApi/settings.py

```console
root@dev:/etc/systemd/system# nano /etc/bezkoder/backend/DjangoRestApi/DjangoRestApi/settings.py

ALLOWED_HOSTS = ['192.168.120.133']
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
```

- Настраиваем frontend

```console
root@dev:~$ sudo sed -i "/try_files \$uri \$uri\/ =404;/try_files \$uri \$uri\/ \$uri.html \/index.html;/" /etc/nginx/sites-available/default
root@dev:~$ cd /etc/bezkoder/frontend
root@dev:/etc/bezkoder/frontend$ sudo npm install
root@dev:/etc/bezkoder/frontend$ sudo npm run build
root@dev:/etc/bezkoder/frontend$ sudo cp -r /etc/bezkoder/frontend/build/. /var/www/html
root@dev:/etc/bezkoder/frontend$ sudo npm start
```
- Создаём юзера под которым будет работать демон и даём ему права на базу данных
```console
root@dev:~# adduser frontend
root@dev:~# chown -R frontend:frontend  /app/bezkoder/frontend
```
- Создаём демона
```console
[Unit]
Description=bezkoder frontend app

[Service]
Restart=on-failure
WorkingDirectory=/app/bezkoder/frontend
ExecStart=npm start
User=frontend

[Install]
WantedBy=multi-user.target
[Install]
WantedBy=multi-user.target
```

- Запускаем демона и проверяем его работу
```console
vg@dev:/app/bezkoder/backend/DjangoRestApi$ sudo systemctl status  bezkoder.front.service
● bezkoder.front.service - bezkoder frontend app
     Loaded: loaded (/etc/systemd/system/bezkoder.front.service; enabled; preset: enabled)
     Active: active (running) since Thu 2024-07-04 13:45:53 +03; 10min ago
   Main PID: 10201 (npm start)
      Tasks: 30 (limit: 4644)
     Memory: 198.2M
        CPU: 6.087s
     CGroup: /system.slice/bezkoder.front.service
             ├─10201 "npm start"
             ├─10212 sh -c "react-scripts start"
             ├─10213 node /app/bezkoder/frontend/node_modules/.bin/react-scripts start
             └─10220 /usr/bin/node /app/bezkoder/frontend/node_modules/react-scripts/scripts/start.js

Jul 04 13:45:56 dev npm[10220]: (Use `node --trace-deprecation ...` to show where the warning was created)
Jul 04 13:45:56 dev npm[10220]: (node:10220) [DEP_WEBPACK_DEV_SERVER_ON_BEFORE_SETUP_MIDDLEWARE] DeprecationWarning: 'onBeforeSetupMiddleware' option is deprecated. Please u>
Jul 04 13:45:56 dev npm[10220]: Starting the development server...
Jul 04 13:45:57 dev npm[10220]: Compiled successfully!
Jul 04 13:45:57 dev npm[10220]: You can now view react-crud in the browser.
Jul 04 13:45:57 dev npm[10220]:   Local:            http://localhost:8081
Jul 04 13:45:57 dev npm[10220]:   On Your Network:  http://192.168.120.133:8081
Jul 04 13:45:57 dev npm[10220]: Note that the development build is not optimized.
Jul 04 13:45:57 dev npm[10220]: To create a production build, use yarn build.
Jul 04 13:45:57 dev npm[10220]: webpack compiled successfully
```


## 4. (**) Познакомиться с инструментом для создания образов VM - Packer - на примерах создания образов для Virtualbox & Hyper-V. Попробовать написать свой шаблон для создания образа VM.



