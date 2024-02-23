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
и выводит их в формате ключ: значение, причем все ключи заменить на русские названия. Например, чтобы вместо «Mem: 1024Mb» выводилось «Память: 1024Мб». Для написания скрипта рекомендуется использовать утилиты awk, grep и sed.
4. (**) Cоздать файл immortalfile, запретить его удаление даже пользователем root и попытаться его удалить из под root, результатом должно быть “Operation not permitted”. Подсказка: chattr.
5. (***) Выполнить команду и разобраться, что она делает и что сохраняется в file.log

env -i bash -x -l -c 'echo hello_there!' > file.log 2>&1

** и *** не обязательны к выполнению. Задачи на интерес