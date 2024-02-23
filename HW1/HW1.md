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
5. Получить информацию о жестком диске
6. Добавить в виртуальную машину второй сетевой интерфейс (вывести информацию о нем в виртуалках)
7. (**) Узнать полную информацию об использованной и неиспользованной оперативной памяти
8. (**) Создать пользователя new_admin_user, Настроить ssh доступ пользователю по ключу на VM, запретить ему авторизацию по паролю
9. (**) Вывести список файловых систем, которые поддерживаются ядром

** и *** не обязательны к выполнению. Задачи на интерес