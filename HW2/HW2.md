## 1. Создать новый виртуальный жёсткий диск, присоеденить его к VM, создать раздел (partition) и инициализировать на нём файловую системую.

  - Создаём новый виртуальный диск

![добавление нового виртуального диска](/HW2/images/HW2_1.png)

 - Перечисляем разделы после добавления диска, новый раздел называется /dev/sdb
 ```console
        root@dev:~# fdisk -l 
            Disk /dev/loop0: 63.91 MiB, 67014656 bytes, 130888 sectors
            Units: sectors of 1 * 512 = 512 bytes
            Sector size (logical/physical): 512 bytes / 512 bytes
            I/O size (minimum/optimal): 512 bytes / 512 bytes


            Disk /dev/loop1: 86.99 MiB, 91213824 bytes, 178152 sectors
            Units: sectors of 1 * 512 = 512 bytes
            Sector size (logical/physical): 512 bytes / 512 bytes
            I/O size (minimum/optimal): 512 bytes / 512 bytes


            Disk /dev/loop2: 40.43 MiB, 42393600 bytes, 82800 sectors
            Units: sectors of 1 * 512 = 512 bytes
            Sector size (logical/physical): 512 bytes / 512 bytes
            I/O size (minimum/optimal): 512 bytes / 512 bytes


            Disk /dev/sda: 100 GiB, 107374182400 bytes, 209715200 sectors
            Disk model: Virtual disk
            Units: sectors of 1 * 512 = 512 bytes
            Sector size (logical/physical): 512 bytes / 512 bytes
            I/O size (minimum/optimal): 512 bytes / 512 bytes
            Disklabel type: gpt
            Disk identifier: 589789F0-264E-4254-9984-4FF722923454

            Device       Start       End   Sectors  Size Type
            /dev/sda1     2048   2203647   2201600    1G EFI System
            /dev/sda2  2203648 209713151 207509504 98.9G Linux filesystem


            Disk /dev/sdb: 50 GiB, 53687091200 bytes, 104857600 sectors
            Disk model: Virtual disk
            Units: sectors of 1 * 512 = 512 bytes
            Sector size (logical/physical): 512 bytes / 512 bytes
            I/O size (minimum/optimal): 512 bytes / 512 bytes
```
- Размечаем диск
```console
        root@dev:~# fdisk /dev/sdb 

                Welcome to fdisk (util-linux 2.37.2).
                Changes will remain in memory only, until you decide to write them.
                Be careful before using the write command.

                Device does not contain a recognized partition table.
                Created a new DOS disklabel with disk identifier 0xd421e355.

                Command (m for help): p 
                Disk /dev/sdb: 50 GiB, 53687091200 bytes, 104857600 sectors
                Disk model: Virtual disk
                Units: sectors of 1 * 512 = 512 bytes
                Sector size (logical/physical): 512 bytes / 512 bytes
                I/O size (minimum/optimal): 512 bytes / 512 bytes
                Disklabel type: dos
                Disk identifier: 0xd421e355

                Command (m for help): n 
                Partition type
                p   primary (0 primary, 0 extended, 4 free)
                e   extended (container for logical partitions)
                Select (default p): p
                Partition number (1-4, default 1):
                First sector (2048-104857599, default 2048):
                Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-104857599, default 104857599):

                Created a new partition 1 of type 'Linux' and of size 50 GiB.

                Command (m for help): w 
                The partition table has been altered.
                Calling ioctl() to re-read partition table.
                Syncing disks.
```
- Форматируем раздел
```console
        root@dev:~# mkfs.ext4 /dev/sdb1  
            mke2fs 1.46.5 (30-Dec-2021)
            Creating filesystem with 13106944 4k blocks and 3276800 inodes
            Filesystem UUID: 98159aed-5829-4a8e-a5fc-b7b6d6447617
            Superblock backups stored on blocks:
                    32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
                    4096000, 7962624, 11239424

            Allocating group tables: done
            Writing inode tables: done
            Creating journal (65536 blocks): done
            Writing superblocks and filesystem accounting information: done
```

## 2. Смонтировать директорию /mnt/home на только что созданный раздел.

   - Монтируем дирректорию на новый раздел
```console
root@dev:/mnt# mount /dev/sdb1 /mnt/home/

```
- Проверяем резльтат:
```console
root@dev:/mnt# df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           794M  1.2M  793M   1% /run
/dev/sda2        97G  7.2G   85G   8% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/sda1       1.1G  6.1M  1.1G   1% /boot/efi
tmpfs           794M  4.0K  794M   1% /run/user/1000
/dev/sdb1        49G   24K   47G   1% /mnt/home
```

## 3. Создать нового пользователя penguin с home-директорией /mnt/home/penguin.
- Создаём нового пользователя penguin
```console
    root@dev:/mnt# adduser penguin 
        Adding user `penguin' ...
        Adding new group `penguin' (1002) ...
        Adding new user `penguin' (1002) with group `penguin' ...
        Creating home directory `/home/penguin' ...
        Copying files from `/etc/skel' ...
        New password:
        Retype new password:
        passwd: password updated successfully
        Changing the user information for penguin
        Enter the new value, or press ENTER for the default
                Full Name []: penguin
                Room Number []:
                Work Phone []:
                Home Phone []:
                Other []:
        Is the information correct? [Y/n] y
```
- Меняем его домашнюю дирректорию
```console
    root@dev:/mnt# usermod -d /mnt/home/penguin penguin  
```
## 4. Создать новую группу пользователей birds, перенести в нее пользователя penguin.
- Создаём новую группу
```console
root@dev:/mnt# addgroup birds
```
- Добавляем пользователя penguin в birds
```console
root@dev:/mnt# usermod -aG birds penguin
```
## 5. Cоздать директорию /var/wintering и выдать права на нее только группе birds.
- Создаём дирректорию
```console
root@dev:/mnt# mkdir /var/wintering
```
- Выдаём на неё права группе birds
```console
root@dev:/mnt# chgrp birds /var/wintering/
root@dev:/mnt# chmod 070 /var/wintering/
root@dev:/mnt# ls -la /var/wintering/
total 8
d---rwx---  2 root birds 4096 Feb 23 15:43 .
drwxr-xr-x 14 root root  4096 Feb 23 15:43 ..
```
## 6. Установить ntpd (или chrony) и разрешить пользователю penguin выполнять команду systemctl restart chronyd (нужны права sudo). Больше узнать о том, что такое NTP и почему он важен можно из следующей статьи.
- Устанавливаем ntpd
```console
root@dev:~# apt install ntp
```
- Редактируем файл /etc/sudoers.tmp
```console
root@dev:~# visudo
```
- Добавляем в него следующую строку, для того что бы пользователь penguin мог выполнять команду systemctl restart ntp
```console
penguin  ALL=NOPASSWD: /bin/systemctl restart ntp
```

7. (**) Вывод команды iostat -x в последней колонке показывает загрузку дисков в процентах. Откуда утилита это понимает?
Достаточно ли вывода команды iostat -x для того, чтобы оценить реальную нагрузку на диски, или нужны дополнительные условия или ключи?
8. (***) Подумать, что сделает команда chmod -x $(which chmod). Выполнить её на виртуальной машине и вернуть всё как было не прибегая к скачиванию\копированию chmod с другого хоста.

** и *** не обязательны к выполнению. Задачи на интерес