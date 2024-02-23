Развернуть две виртуальные машины (кто еще не сделал, можно последовательно)
- Ubuntu
- Centos

Затем:
1. Произвести минимальную настройку (время, локаль, custom motd)
root@dev:~# timedatectl
               Local time: Fri 2024-02-23 09:16:47 UTC
           Universal time: Fri 2024-02-23 09:16:47 UTC
                 RTC time: Fri 2024-02-23 09:16:47
                Time zone: Etc/UTC (UTC, +0000)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
root@dev:~# timedatectl set-timezone Europe/Minsk
root@dev:~# timedatectl
               Local time: Fri 2024-02-23 12:18:37 +03
           Universal time: Fri 2024-02-23 09:18:37 UTC
                 RTC time: Fri 2024-02-23 09:18:37
                Time zone: Europe/Minsk (+03, +0300)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no


2. Определить точную версию ядра.
3. Вывести список модулей ядра и записать в файл
4. Просмотреть информацию о процессоре и модулях оперативной памяти
5. Получить информацию о жестком диске
6. Добавить в виртуальную машину второй сетевой интерфейс (вывести информацию о нем в виртуалках)
7. (**) Узнать полную информацию об использованной и неиспользованной оперативной памяти
8. (**) Создать пользователя new_admin_user, Настроить ssh доступ пользователю по ключу на VM, запретить ему авторизацию по паролю
9. (**) Вывести список файловых систем, которые поддерживаются ядром

** и *** не обязательны к выполнению. Задачи на интерес