Развернул виртуальную машину:
- Ubuntu


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

        root@dev:~# timedatectl set-timezone Europe/Minsk   //Меняем временную зону, что бы время совпадало с локальным временем в стране

        root@dev:~# timedatectl     //Проверяем изменения времени

                    Local time: Fri 2024-02-23 12:18:37 +03
                Universal time: Fri 2024-02-23 09:18:37 UTC
                        RTC time: Fri 2024-02-23 09:18:37
                        Time zone: Europe/Minsk (+03, +0300)
                    System clock synchronized: yes
                    NTP service: active
                RTC in local TZ: no

        root@dev:~# localectl  //Узнаём текущую локаль

            System Locale: LANG=en_US.UTF-8
            VC Keymap: n/a
            X11 Layout: us
            X11 Model: pc105

        root@dev:~# localectl list-locales //Смотрим доступные локали

            C.UTF-8
            en_US.UTF-8

        root@dev:~# apt -y install language-pack-ru-base language-pack-ru  //Устонавливаем русскую локаль

        root@dev:~# localectl list-locales //Проверяем, всё ли хорошо установилось

            C.UTF-8
            en_US.UTF-8
            ru_RU.UTF-8
            ru_UA.UTF-8

        root@dev:~# localectl set-locale ru_RU.UTF-8 //Меняем локаль

        root@dev:~# localectl //Проверяем изменения

            System Locale: LANG=ru_RU.UTF-8
            VC Keymap: n/a
            X11 Layout: us
            X11 Model: pc105

        root@dev:~# nano /etc/motd //Редактируем файл motd, добавляем туда запись

            ####################################################
                Hello World!!!
            ####################################################

        root@dev:~# reboot now   //Проверяем изменения

                Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-97-generic x86_64)

                * Documentation:  https://help.ubuntu.com
                * Management:     https://landscape.canonical.com
                * Support:        https://ubuntu.com/pro

                System information as of Пт 23 фев 2024 12:47:03 +03

                System load:  1.7265625         Processes:              226
                Usage of /:   7.3% of 96.83GB   Users logged in:        0
                Memory usage: 3%                IPv4 address for ens34: 
                Swap usage:   0%


                Expanded Security Maintenance for Applications is not enabled.

                0 updates can be applied immediately.

                Enable ESM Apps to receive additional future security updates.
                See https://ubuntu.com/esm or run: sudo pro status


                ####################################################
                Hello World!!!
                ####################################################



2. Определить точную версию ядра.

            root@dev:~# hostnamectl | grep -i kernel  //Узнаем точную версию ядра

                    Kernel: Linux 5.15.0-97-generic


3. Вывести список модулей ядра и записать в файл

            root@dev:~# lsmod > /home/kernel.modules //выводим список модулей ядра и записываем их в файл kernel.modules

            root@dev:~# cat /home/kernel.modules  //Выводим содержимое файла

                Module                  Size  Used by
                vsock_loopback         16384  0
                vmw_vsock_virtio_transport_common    40960  1 vsock_loopback
                vmw_vsock_vmci_transport    32768  1
                vsock                  49152  5 vmw_vsock_virtio_transport_common,vsock_loopback,vmw_vsock_vmci_transport
                binfmt_misc            24576  1
                nls_iso8859_1          16384  1
                intel_rapl_msr         20480  0
                intel_rapl_common      40960  1 intel_rapl_msr
                vmw_balloon            24576  0
                joydev                 32768  0
                rapl                   20480  0
                input_leds             16384  0
                serio_raw              20480  0
                vmw_vmci               90112  2 vmw_balloon,vmw_vsock_vmci_transport
                mac_hid                16384  0
                sch_fq_codel           20480  2
                dm_multipath           40960  0
                scsi_dh_rdac           20480  0
                scsi_dh_emc            16384  0
                scsi_dh_alua           20480  0
                msr                    16384  0
                efi_pstore             16384  0
                ip_tables              32768  0
                x_tables               53248  1 ip_tables
                autofs4                49152  2
                btrfs                1560576  0
                blake2b_generic        20480  0
                zstd_compress         229376  1 btrfs
                raid10                 69632  0
                raid456               163840  0
                async_raid6_recov      24576  1 raid456
                async_memcpy           20480  2 raid456,async_raid6_recov
                async_pq               24576  2 raid456,async_raid6_recov
                async_xor              20480  3 async_pq,raid456,async_raid6_recov
                async_tx               20480  5 async_pq,async_memcpy,async_xor,raid456,async_raid6_recov
                xor                    24576  2 async_xor,btrfs
                raid6_pq              122880  4 async_pq,btrfs,raid456,async_raid6_recov
                libcrc32c              16384  2 btrfs,raid456
                raid1                  49152  0
                raid0                  24576  0
                multipath              20480  0
                linear                 20480  0
                hid_generic            16384  0
                vmwgfx                372736  2
                ttm                    86016  1 vmwgfx
                drm_kms_helper        311296  1 vmwgfx
                crct10dif_pclmul       16384  1
                crc32_pclmul           16384  0
                syscopyarea            16384  1 drm_kms_helper
                ghash_clmulni_intel    16384  0
                sysfillrect            20480  1 drm_kms_helper
                sysimgblt              16384  1 drm_kms_helper
                aesni_intel           376832  0
                fb_sys_fops            16384  1 drm_kms_helper
                cec                    61440  1 drm_kms_helper
                crypto_simd            16384  1 aesni_intel
                usbhid                 65536  0
                cryptd                 24576  2 crypto_simd,ghash_clmulni_intel
                rc_core                65536  1 cec
                psmouse               176128  0
                mptsas                 61440  2
                ahci                   49152  0
                mptscsih               49152  1 mptsas
                hid                   151552  2 usbhid,hid_generic
                libahci                49152  1 ahci
                mptbase               106496  2 mptsas,mptscsih
                e1000e                299008  0
                drm                   622592  5 vmwgfx,drm_kms_helper,ttm
                scsi_transport_sas     45056  1 mptsas
                i2c_piix4              32768  0
                pata_acpi              16384  0


4. Просмотреть информацию о процессоре и модулях оперативной памяти

            root@dev:~# dmidecode --type 17  //Информация о модулях памяти

                        # dmidecode 3.3
                Getting SMBIOS data from sysfs.
                SMBIOS 2.7 present.

                Handle 0x0021, DMI type 17, 40 bytes
                Memory Device
                        Array Handle: 0x0020
                        Error Information Handle: No Error
                        Total Width: 64 bits
                        Data Width: 64 bits
                        Size: 8 GB
                        Form Factor: DIMM
                        Set: None
                        Locator: RAM slot #0
                        Bank Locator: RAM slot #0
                        Type: DRAM
                        Type Detail: Synchronous
                        Speed: Unknown
                        Manufacturer: VMware Virtual RAM
                        Serial Number: 00000001
                        Asset Tag: Not Specified
                        Part Number: VMW-8192MB
                        Rank: Unknown
                        Configured Memory Speed: 4800 MT/s
                        Minimum Voltage: 1.2 V
                        Maximum Voltage: 1.2 V
                        Configured Voltage: 1.2 V

            root@dev:~# lscpu  //Узнаём модель CPU

                Architecture:            x86_64
                CPU op-mode(s):        32-bit, 64-bit
                Address sizes:         45 bits physical, 48 bits virtual
                Byte Order:            Little Endian
                CPU(s):                  4
                On-line CPU(s) list:   0-3
                Vendor ID:               GenuineIntel
                Model name:            Intel(R) Xeon(R) CPU E5-2630 v4 @ 2.20GHz
                    CPU family:          6
                    Model:               79
                    Thread(s) per core:  1
                    Core(s) per socket:  4
                    Socket(s):           1
                    Stepping:            1
                    BogoMIPS:            4399.99
                    Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon nopl xto
                                        pology tsc_reliable nonstop_tsc cpuid tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand h
                                        ypervisor lahf_lm abm 3dnowprefetch invpcid_single pti ssbd ibrs ibpb stibp fsgsbase tsc_adjust bmi1 avx2 smep bmi2 invpcid rdseed adx smap xsaveopt arat md_clear flus
                                        h_l1d arch_capabilities
                Virtualization features:
                Hypervisor vendor:     VMware
                Virtualization type:   full
                Caches (sum of all):
                L1d:                   128 KiB (4 instances)
                L1i:                   128 KiB (4 instances)
                L2:                    1 MiB (4 instances)
                L3:                    25 MiB (1 instance)
                NUMA:
                NUMA node(s):          1
                NUMA node0 CPU(s):     0-3
                Vulnerabilities:
                Gather data sampling:  Not affected
                Itlb multihit:         KVM: Mitigation: VMX unsupported
                L1tf:                  Mitigation; PTE Inversion
                Mds:                   Mitigation; Clear CPU buffers; SMT Host state unknown
                Meltdown:              Mitigation; PTI
                Mmio stale data:       Mitigation; Clear CPU buffers; SMT Host state unknown
                Retbleed:              Mitigation; IBRS
                Spec rstack overflow:  Not affected
                Spec store bypass:     Mitigation; Speculative Store Bypass disabled via prctl and seccomp
                Spectre v1:            Mitigation; usercopy/swapgs barriers and __user pointer sanitization
                Spectre v2:            Mitigation; IBRS, IBPB conditional, STIBP disabled, RSB filling, PBRSB-eIBRS Not affected
                Srbds:                 Not affected
                Tsx async abort:       Not affected



5. Получить информацию о жестком диске
        
        root@dev:~# lshw -class disk //Выводим информацию о дисках

            *-disk
                description: SCSI Disk
                product: Virtual disk
                vendor: VMware
                physical id: 0.0.0
                bus info: scsi@32:0.0.0
                logical name: /dev/sda
                version: 2.0
                size: 100GiB (107GB)
                capabilities: gpt-1.00 partitioned partitioned:gpt
                configuration: ansiversion=6 guid=589789f0-264e-4254-9984-4ff722923454 logicalsectorsize=512 sectorsize=512
            *-cdrom
                description: DVD-RAM writer
                product: VMware SATA CD00
                vendor: NECVMWar
                physical id: 0.0.0
                bus info: scsi@2:0.0.0
                logical name: /dev/cdrom
                logical name: /dev/sr0
                version: 1.00
                capabilities: removable audio cd-r cd-rw dvd dvd-r dvd-ram
                configuration: ansiversion=5 status=open


6. Добавить в виртуальную машину второй сетевой интерфейс (вывести информацию о нем в виртуалках)

        root@dev:~# ip a //Информация о текущих интерфейсах

            1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
                link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
                inet 127.0.0.1/8 scope host lo
                valid_lft forever preferred_lft forever
                inet6 ::1/128 scope host
                valid_lft forever preferred_lft forever
            2: ens34: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
                link/ether 00:0c:29:21:00:33 brd ff:ff:ff:ff:ff:ff
                altname enp2s2
                inet 192.168.120.130/24 metric 100 brd 192.168.120.255 scope global dynamic ens34
                valid_lft 84406sec preferred_lft 84406sec
                inet6 fe80::20c:29ff:fe21:33/64 scope link
                valid_lft forever preferred_lft forever

    Добавляем новый сетевой адаптер в виртуальную машину

    ![добавление нового сетевого интерфейса](/hw1/images/hw1_1.png)


    ![добавление нового сетевого интерфейса](/Hw1/images/hw1_2.png)

        root@dev:~# ip a //Проверяем добавление нового сетевого интерфейса

            1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
                link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
                inet 127.0.0.1/8 scope host lo
                valid_lft forever preferred_lft forever
                inet6 ::1/128 scope host
                valid_lft forever preferred_lft forever
            2: ens34: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
                link/ether 00:0c:29:21:00:33 brd ff:ff:ff:ff:ff:ff
                altname enp2s2
                inet 192.168.120.130/24 metric 100 brd 192.168.120.255 scope global dynamic ens34
                valid_lft 84186sec preferred_lft 84186sec
                inet6 fe80::20c:29ff:fe21:33/64 scope link
                valid_lft forever preferred_lft forever
            3: ens37: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
                link/ether 00:0c:29:21:00:3d brd ff:ff:ff:ff:ff:ff
                altname enp2s5

7. (**) Узнать полную информацию об использованной и неиспользованной оперативной памяти

        root@dev:~# free

                        total        used        free      shared  buff/cache   available
            Mem:         8127504      222024     7602964        1136      302516     7658608
            Swap:        4194300           0     4194300


8. (**) Создать пользователя new_admin_user, Настроить ssh доступ пользователю по ключу на VM, запретить ему авторизацию по паролю

        root@dev:~# adduser new_admin_user //Создаём нового пользователя

            Adding user `new_admin_user' ...
            Adding new group `new_admin_user' (1001) ...
            Adding new user `new_admin_user' (1001) with group `new_admin_user' ...
            Creating home directory `/home/new_admin_user' ...
            Copying files from `/etc/skel' ...
            New password:
            Retype new password:
            passwd: password updated successfully
            Changing the user information for new_admin_user
            Enter the new value, or press ENTER for the default
                    Full Name []: new_admin_user
                    Room Number []:
                    Work Phone []:
                    Home Phone []:
                    Other []:
            Is the information correct? [Y/n] y

        root@dev:~# ssh-keygen //Генерируем ключ

            Generating public/private rsa key pair.
            Enter file in which to save the key (/root/.ssh/id_rsa):
            Enter passphrase (empty for no passphrase):
            Enter same passphrase again:
            Your identification has been saved in /root/.ssh/id_rsa
            Your public key has been saved in /root/.ssh/id_rsa.pub
            The key fingerprint is:
            SHA256:giqDcyRVu1bfUKLZH5k9DLzu5od/Sq0cDQh19bLV9W4 root@dev
            The key's randomart image is:
            +---[RSA 3072]----+
            |    .   ..+ ... .|
            |   . . + +.B   .+|
            |  . . + + +.+ . =|
            | .   + . =.o . = |
            |. . + . S.+ . . E|
            |.o o   .  .  + . |
            |= o      . .o o  |
            | =        +o.o.  |
            |         o.o=o   |
            +----[SHA256]-----+

        root@dev:~# ssh-copy-id new_admin_user@192.168.120.130  //Копируем ключ

            /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
            /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
            /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
            
            new_admin_user@192.168.120.130's password:

            Number of key(s) added: 1

            Now try logging into the machine, with:   "ssh 'new_admin_user@192.168.120.130'"
            and check to make sure that only the key(s) you wanted were added.

        root@dev:~# nano /etc/ssh/sshd_config //Заходим в конфигурационный файл ssh сервера и добавляем в него строки

            Match User new_admin_user
            PasswordAuthentication no

        root@dev:~# systemctl reload ssh //Перезагружаем службу без полной остановки

9. (**) Вывести список файловых систем, которые поддерживаются ядром

        root@dev:~# cat /proc/filesystems

            nodev   sysfs
            nodev   tmpfs
            nodev   bdev
            nodev   proc
            nodev   cgroup
            nodev   cgroup2
            nodev   cpuset
            nodev   devtmpfs
            nodev   configfs
            nodev   debugfs
            nodev   tracefs
            nodev   securityfs
            nodev   sockfs
            nodev   bpf
            nodev   pipefs
            nodev   ramfs
            nodev   hugetlbfs
            nodev   devpts
                    ext3
                    ext2
                    ext4
                    squashfs
                    vfat
            nodev   ecryptfs
                    fuseblk
            nodev   fuse
            nodev   fusectl
            nodev   efivarfs
            nodev   mqueue
            nodev   pstore
                    btrfs
            nodev   autofs
            nodev   binfmt_misc

** и *** не обязательны к выполнению. Задачи на интерес