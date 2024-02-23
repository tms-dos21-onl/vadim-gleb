## 1. Познакомиться с утилитой Midnight Commander, установить её на VM и узнать с помощью неё все папки верхнего уровня файловой системы.
- Устанавливаем команду
```console
root@dev:~# apt install -y mc
```
- Все папки верхнего уровня
![Все папки верхнего уровня](/HW3/images/HW3_1.png)
## 2. Установить PowerShell на VM и проверить, что он работаёт путем выполнения каких-нибудь простейших команд.
- Устанавливаем powershell
```console
root@dev:~# snap install powershell --classic
```
- Выполнение простой команды powershell
```console
root@dev:~# powershell
PowerShell 7.4.1
PS /root> Get-Command

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           Get-PSResource                                     1.0.1      Microsoft.PowerShell.PSResourceGet
Function        cd..
Function        cd\
Function        cd~
Function        Clear-Host
Function        Compress-Archive                                   1.2.5      Microsoft.PowerShell.Archive
Function        exec
Function        Expand-Archive                                     1.2.5      Microsoft.PowerShell.Archive
Function        Find-Command                                       2.2.5      PowerShellGet
.......
```
## 3. Создать простейший bash-скрипт sysinfo.sh, который собирает данные о:
- количестве свободной оперативной памяти
- текущей загрузке процессора
- текущем IP адресе(ах)
```console
#!/bin/bash

cpu=$(top -n1 | grep "Cpu(s)"| awk '{print $2}')
echo "Нагрузка на CPU: $cpu%"

mem_free=$(free -h | grep "Mem"| awk '{print $4}')
echo "Свободная память: $mem_free"

ip=$(hostname -I)
echo "IP адрес: $ip"
```
- Результат запуска скрипта
```console
root@dev:/home/scripts# sh sysinfo.sh
Нагрузка на CPU: 1.4%
Свободная память: 6.5Gi
IP адрес: 192.168.120.130
```
## 4. (**) Cоздать файл immortalfile, запретить его удаление даже пользователем root и попытаться его удалить из под root, результатом должно быть “Operation not permitted”. Подсказка: chattr.
- Создаём файл immortalfile и запрещаем его удаление для всех пользователей включая root
```console
root@dev:/home# touch immortalfile
root@dev:/home# chattr +i immortalfile
```
- Проверяем, можно ли удалить созданный файл
```console
root@dev:/home# rm -R immortalfile
rm: cannot remove 'immortalfile': Operation not permitted
```

## 5. (***) Выполнить команду и разобраться, что она делает и что сохраняется в file.log

- env -i bash -x -l -c 'echo hello_there!' > file.log 2>&1
```console
env -i   # команда игорирующая окружение
bash -x  # вывод команд по мере их выполнения
     -l  # bash выступает как оболочка для входа в систему
     -с  # выполняет команду внутри ковычек 'echo hello_there!'
echo hello_there! # выводит в консоль текст hello_there!
> file.log  # записывает вывод предыдущих команд в файл file.log
2>&1  # перенаправление stderr в stdout
```
- В итоге, команда показывает весь список процессов которые происходят в системе, когда требуется выполнить команду echo hello_there!. Если я правильно понял.


** и *** не обязательны к выполнению. Задачи на интерес