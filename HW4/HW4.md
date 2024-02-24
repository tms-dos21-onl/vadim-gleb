## 1. Отобразить все процессы в системе.
```console
root@dev:/home# ps -aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1 167612 13040 ?        Ss   Feb23   0:20 /sbin/init
root           2  0.0  0.0      0     0 ?        S    Feb23   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   Feb23   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   Feb23   0:00 [rcu_par_gp]
root           5  0.0  0.0      0     0 ?        I<   Feb23   0:00 [slub_flushwq]
root           6  0.0  0.0      0     0 ?        I<   Feb23   0:00 [netns]
root           8  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/0:0H-events_highpri]
root          10  0.0  0.0      0     0 ?        I<   Feb23   0:00 [mm_percpu_wq]
root          11  0.0  0.0      0     0 ?        S    Feb23   0:00 [rcu_tasks_rude_]
root          12  0.0  0.0      0     0 ?        S    Feb23   0:00 [rcu_tasks_trace]
root          13  0.0  0.0      0     0 ?        S    Feb23   0:00 [ksoftirqd/0]
root          14  0.0  0.0      0     0 ?        I    Feb23   0:36 [rcu_sched]
root          15  0.0  0.0      0     0 ?        S    Feb23   0:00 [migration/0]
root          16  0.0  0.0      0     0 ?        S    Feb23   0:00 [idle_inject/0]
root          18  0.0  0.0      0     0 ?        S    Feb23   0:00 [cpuhp/0]
root          19  0.0  0.0      0     0 ?        S    Feb23   0:00 [cpuhp/1]
root          20  0.0  0.0      0     0 ?        S    Feb23   0:00 [idle_inject/1]
root          21  0.0  0.0      0     0 ?        S    Feb23   0:00 [migration/1]
root          22  0.0  0.0      0     0 ?        S    Feb23   0:00 [ksoftirqd/1]
root          24  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/1:0H-events_highpri]
root          25  0.0  0.0      0     0 ?        S    Feb23   0:00 [cpuhp/2]
root          26  0.0  0.0      0     0 ?        S    Feb23   0:00 [idle_inject/2]
root          27  0.0  0.0      0     0 ?        S    Feb23   0:00 [migration/2]
root          28  0.0  0.0      0     0 ?        S    Feb23   0:00 [ksoftirqd/2]
root          30  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/2:0H-events_highpri]
root          31  0.0  0.0      0     0 ?        S    Feb23   0:00 [cpuhp/3]
root          32  0.0  0.0      0     0 ?        S    Feb23   0:00 [idle_inject/3]
root          33  0.0  0.0      0     0 ?        S    Feb23   0:00 [migration/3]
root          34  0.0  0.0      0     0 ?        S    Feb23   0:00 [ksoftirqd/3]
root          36  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/3:0H-events_highpri]
root          37  0.0  0.0      0     0 ?        S    Feb23   0:00 [kdevtmpfs]
root          38  0.0  0.0      0     0 ?        I<   Feb23   0:00 [inet_frag_wq]
root          39  0.0  0.0      0     0 ?        S    Feb23   0:00 [kauditd]
root          40  0.0  0.0      0     0 ?        S    Feb23   0:00 [khungtaskd]
root          41  0.0  0.0      0     0 ?        S    Feb23   0:00 [oom_reaper]
root          42  0.0  0.0      0     0 ?        I<   Feb23   0:00 [writeback]
root          43  0.0  0.0      0     0 ?        S    Feb23   0:04 [kcompactd0]
root          44  0.0  0.0      0     0 ?        SN   Feb23   0:00 [ksmd]
root          45  0.0  0.0      0     0 ?        SN   Feb23   0:00 [khugepaged]
root          92  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kintegrityd]
root          94  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kblockd]
root          95  0.0  0.0      0     0 ?        I<   Feb23   0:00 [blkcg_punt_bio]
root          97  0.0  0.0      0     0 ?        I<   Feb23   0:00 [tpm_dev_wq]
root          98  0.0  0.0      0     0 ?        I<   Feb23   0:00 [ata_sff]
root          99  0.0  0.0      0     0 ?        I<   Feb23   0:00 [md]
root         100  0.0  0.0      0     0 ?        I<   Feb23   0:00 [edac-poller]
root         101  0.0  0.0      0     0 ?        I<   Feb23   0:00 [devfreq_wq]
root         102  0.0  0.0      0     0 ?        S    Feb23   0:00 [watchdogd]
root         105  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/1:1H-kblockd]
root         107  0.0  0.0      0     0 ?        S    Feb23   0:00 [kswapd0]
root         108  0.0  0.0      0     0 ?        S    Feb23   0:00 [ecryptfs-kthrea]
root         110  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kthrotld]
root         111  0.0  0.0      0     0 ?        I<   Feb23   0:00 [acpi_thermal_pm]
root         112  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_0]
root         113  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_0]
root         114  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_1]
root         115  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_1]
root         117  0.0  0.0      0     0 ?        I<   Feb23   0:00 [vfio-irqfd-clea]
root         119  0.0  0.0      0     0 ?        I<   Feb23   0:00 [mld]
root         120  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/0:1H-kblockd]
root         121  0.0  0.0      0     0 ?        I<   Feb23   0:00 [ipv6_addrconf]
root         132  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kstrp]
root         135  0.0  0.0      0     0 ?        I<   Feb23   0:00 [zswap-shrink]
root         136  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/u9:0]
root         143  0.0  0.0      0     0 ?        I<   Feb23   0:00 [charger_manager]
root         166  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/2:1H-kblockd]
root         203  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kworker/3:1H-kblockd]
root         208  0.0  0.0      0     0 ?        I<   Feb23   0:00 [cryptd]
root         231  0.0  0.0      0     0 ?        I<   Feb23   0:00 [mpt_poll_0]
root         232  0.0  0.0      0     0 ?        I<   Feb23   0:00 [mpt/0]
root         234  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_2]
root         235  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_2]
root         236  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_3]
root         237  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_3]
root         238  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_4]
root         239  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_4]
root         240  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_5]
root         241  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_5]
root         242  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_6]
root         243  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_6]
root         244  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_7]
root         245  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_7]
root         246  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_8]
root         247  0.0  0.0      0     0 ?        I<   Feb23   0:00 [ttm_swap]
root         248  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_8]
root         249  0.0  0.0      0     0 ?        S    Feb23   0:17 [irq/16-vmwgfx]
root         250  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_9]
root         251  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_9]
root         252  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc0]
root         253  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc1]
root         254  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc2]
root         255  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_10]
root         256  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc3]
root         257  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_10]
root         258  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc4]
root         259  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc5]
root         260  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc6]
root         261  0.0  0.0      0     0 ?        S    Feb23   0:00 [card0-crtc7]
root         262  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_11]
root         263  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_11]
root         264  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_12]
root         265  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_12]
root         266  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_13]
root         267  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_13]
root         268  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_14]
root         269  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_14]
root         270  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_15]
root         271  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_15]
root         272  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_16]
root         273  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_16]
root         274  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_17]
root         275  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_17]
root         276  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_18]
root         277  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_18]
root         278  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_19]
root         279  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_19]
root         280  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_20]
root         281  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_20]
root         282  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_21]
root         283  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_21]
root         284  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_22]
root         285  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_22]
root         286  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_23]
root         287  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_23]
root         288  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_24]
root         289  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_24]
root         290  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_25]
root         291  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_25]
root         292  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_26]
root         293  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_26]
root         294  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_27]
root         295  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_27]
root         296  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_28]
root         297  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_28]
root         298  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_29]
root         299  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_29]
root         300  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_30]
root         301  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_30]
root         302  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_31]
root         303  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_31]
root         330  0.0  0.0      0     0 ?        S    Feb23   0:00 [scsi_eh_32]
root         331  0.0  0.0      0     0 ?        I<   Feb23   0:00 [scsi_tmf_32]
root         369  0.0  0.0      0     0 ?        I<   Feb23   0:00 [raid5wq]
root         416  0.0  0.0      0     0 ?        S    Feb23   0:00 [jbd2/sda2-8]
root         417  0.0  0.0      0     0 ?        I<   Feb23   0:00 [ext4-rsv-conver]
root         488  0.0  0.2  80604 23764 ?        S<s  Feb23   0:01 /lib/systemd/systemd-journald
root         519  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kaluad]
root         520  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kmpath_rdacd]
root         522  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kmpathd]
root         523  0.0  0.0      0     0 ?        I<   Feb23   0:00 [kmpath_handlerd]
root         527  0.0  0.3 354888 27100 ?        SLsl Feb23   0:12 /sbin/multipathd -d -s
root         531  0.0  0.0  11916  6672 ?        Ss   Feb23   0:00 /lib/systemd/systemd-udevd
root         701  0.0  0.1  51152 11776 ?        Ss   Feb23   0:00 /usr/bin/VGAuthService
root         702  0.1  0.1 241416  9460 ?        Ssl  Feb23   2:25 /usr/bin/vmtoolsd
systemd+     746  0.0  0.1  16376  8472 ?        Ss   Feb23   1:29 /lib/systemd/systemd-networkd
systemd+     748  0.0  0.1  25536 12624 ?        Ss   Feb23   0:00 /lib/systemd/systemd-resolved
root         759  0.0  0.0   6904  2880 ?        Ss   Feb23   0:00 /usr/sbin/cron -f -P
message+     762  0.0  0.0   8912  4980 ?        Ss   Feb23   0:01 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
root         767  0.0  0.0  82768  4004 ?        Ssl  Feb23   0:08 /usr/sbin/irqbalance --foreground
root         768  0.0  0.2  32744 19144 ?        Ss   Feb23   0:00 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
root         769  0.0  0.1 239388  9376 ?        Ssl  Feb23   0:00 /usr/libexec/polkitd --no-debug
syslog       770  0.0  0.0 222404  5716 ?        Ssl  Feb23   0:00 /usr/sbin/rsyslogd -n -iNONE
root         776  0.0  0.3 1467184 31524 ?       Ssl  Feb23   0:21 /usr/lib/snapd/snapd
root         779  0.0  0.0  15668  7888 ?        Ss   Feb23   0:00 /lib/systemd/systemd-logind
root         782  0.0  0.1 392672 13004 ?        Ssl  Feb23   0:00 /usr/libexec/udisks2/udisksd
root         795  0.0  0.1 244228 12252 ?        Ssl  Feb23   0:00 /usr/sbin/ModemManager
root         820  0.0  0.1  15432  9380 ?        Ss   Feb23   0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root         821  0.0  0.0   6184  1084 tty1     Ss+  Feb23   0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
root         823  0.0  0.2 109760 21624 ?        Ssl  Feb23   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         876  0.0  0.1  17184 10964 ?        Ss   Feb23   0:00 sshd: vg [priv]
vg           888  0.0  0.1  17060  9740 ?        Ss   Feb23   0:00 /lib/systemd/systemd --user
vg           889  0.0  0.0 169144  3672 ?        S    Feb23   0:00 (sd-pam)
vg           970  0.0  0.1  17316  8136 ?        R    Feb23   0:02 sshd: vg@pts/0
vg           971  0.0  0.0   8740  5528 pts/0    Ss   Feb23   0:00 -bash
root         981  0.0  0.0  11680  6284 pts/0    R+   Feb23   0:01 sudo -i
root         995  0.0  0.0  11680  2568 pts/1    Ss   Feb23   0:00 sudo -i
root         996  0.0  0.2  19468 16424 pts/1    S    Feb23   0:03 -bash
root        1935  0.0  0.0      0     0 ?        S    Feb23   0:00 [jbd2/sdb1-8]
root        1936  0.0  0.0      0     0 ?        I<   Feb23   0:00 [ext4-rsv-conver]
root        2644  0.0  0.2 295592 20492 ?        Ssl  Feb23   0:00 /usr/libexec/packagekitd
root        3833  0.0  0.1  17184 10948 ?        Ss   Feb23   0:00 sshd: penguin [priv]
penguin     3836  0.0  0.1  17064  9596 ?        Ss   Feb23   0:00 /lib/systemd/systemd --user
penguin     3837  0.0  0.0 170524  5092 ?        S    Feb23   0:00 (sd-pam)
penguin     3938  0.0  0.0  17320  8004 ?        S    Feb23   0:00 sshd: penguin@pts/2
penguin     3939  0.0  0.0   8664  5436 pts/2    Ss+  Feb23   0:00 -bash
ntp         3964  0.0  0.0  76092  6084 ?        Ssl  Feb23   0:08 /usr/sbin/ntpd -p /var/run/ntpd.pid -g -u 115:120
root        5354  0.0  0.1 239624  9008 ?        Ssl  Feb23   0:00 /usr/libexec/upowerd
root        7193  0.0  0.0      0     0 ?        I    Feb23   0:21 [kworker/2:0-events]
root        7470  0.0  0.0      0     0 ?        I    02:48   0:08 [kworker/1:1-events]
root        7571  0.0  0.0      0     0 ?        I    04:11   0:11 [kworker/3:3-events]
root        7687  0.0  0.0      0     0 ?        I    06:24   0:03 [kworker/1:0-events]
root        7744  0.0  0.0      0     0 ?        I    06:24   0:28 [kworker/0:0-events]
root        8362  0.0  0.0      0     0 ?        I    10:23   0:00 [kworker/2:1]
root        8480  0.0  0.0      0     0 ?        I    13:10   0:00 [kworker/3:1-events]
root        8492  0.0  0.0      0     0 ?        I    13:20   0:00 [kworker/0:2-events]
root        8769  0.0  0.0      0     0 ?        R    19:22   0:00 [kworker/u8:0-events_unbound]
root        8774  0.0  0.0      0     0 ?        I    19:28   0:00 [kworker/u8:2-flush-8:0]
root        8788  0.0  0.0      0     0 ?        I    19:50   0:00 [kworker/u8:1-events_unbound]
root        8794  0.0  0.0  10344  3792 pts/1    R+   20:00   0:00 ps -aux

```
## 2. Запустить бесконечный процесс в фоновом режиме используя nohup.
- Запуск процесса, который будет пингвать google.com 
```
root@dev:~# nohup ping google.com &
[1] 8922
```
## 3. Убедиться, что процесс продолжил работу после завершения сессии.
- Ищем процесс с pid 8922 в выводе команды ps -aux
```
root@dev:~# ps -aux | grep 8922
root        8922  0.0  0.0   7728  1292 pts/1    S    20:10   0:00 ping google.com
```
## 4. Убить процесс, запущенный в фоновом режиме.
- Убиваем процесс с помощью команды kill
```
root@dev:~# kill 8922
root@dev:~# ps -aux | grep 8922
root        8933  0.0  0.0   6488  2356 pts/1    S+   20:15   0:00 grep --color=auto 8922
[1]+  Terminated              nohup ping google.com
```
## 5. Написать свой сервис под управлением systemd, добавить его в автозагрузку (можно использовать процесс из п.2).
- Пишем маленький скрипт который будет пинговать google.com, назовём google.sh
```
#!/bin/bash
ping google.com
```
- После того, как сохранили скрипт ( у меня путь к скрипту будет /home/service/google.sh), заходим по пути /etc/systemd/system и создём службу google.service
```
[Unit]
Description=google service
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
Restart=always
RestartSec=1
User=vg
ExecStart=/home/service/google.sh

[Install]
WantedBy=multi-user.target
```
- Так как служба будет запускаться от пользователя vg, мы сделаем его владельцем файла /home/service/google.sh и выдадим ему все права на него, забрав их у остальных пользователей
```
root@dev:/etc/systemd/system# chown vg /home/service/google.sh
root@dev:/etc/systemd/system# chmod 700 /home/service/google.sh
root@dev:/etc/systemd/system# ls -l /home/service/google.sh
-rwx------ 1 vg root 28 Feb 24 20:21 /home/service/google.sh
```
- Запускаем служба, смотрим её статус и добавляем её в автозагрузку
```
root@dev:/etc/systemd/system# systemctl start  google.service
root@dev:/etc/systemd/system# systemctl status  google.service
● google.service - google service
     Loaded: loaded (/etc/systemd/system/google.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2024-02-24 20:37:11 +03; 3s ago
   Main PID: 9352 (google.sh)
      Tasks: 2 (limit: 9388)
     Memory: 628.0K
        CPU: 14ms
     CGroup: /system.slice/google.service
             ├─9352 /bin/bash /home/service/google.sh
             └─9353 ping google.com

Feb 24 20:37:11 dev systemd[1]: Started google service.
Feb 24 20:37:11 dev google.sh[9353]: PING google.com (142.250.186.206) 56(84) bytes of data.
Feb 24 20:37:11 dev google.sh[9353]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=1 ttl=113 time=42.3 ms
Feb 24 20:37:12 dev google.sh[9353]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=2 ttl=113 time=42.1 ms
Feb 24 20:37:13 dev google.sh[9353]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=3 ttl=113 time=42.2 ms
Feb 24 20:37:14 dev google.sh[9353]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=4 ttl=113 time=42.1 ms
root@dev:/etc/systemd/system# systemctl enable  google.service
Created symlink /etc/systemd/system/multi-user.target.wants/google.service → /etc/systemd/system/google.service.
```
## 6. Посмотреть логи своего сервиса.
- Для проверки логов службы обратимся к файлу /var/log/syslog
```
root@dev:~# cat /var/log/syslog | grep "google"
Feb 24 20:36:21 dev systemd[1]: Started google service.
Feb 24 20:36:22 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=143 ttl=113 time=42.3 ms
Feb 24 20:36:23 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=144 ttl=113 time=42.2 ms
Feb 24 20:36:24 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=145 ttl=113 time=42.3 ms
Feb 24 20:36:25 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=146 ttl=113 time=42.3 ms
Feb 24 20:36:26 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=147 ttl=113 time=42.3 ms
Feb 24 20:36:27 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=148 ttl=113 time=42.2 ms
Feb 24 20:36:28 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=149 ttl=113 time=42.2 ms
Feb 24 20:36:29 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=150 ttl=113 time=42.3 ms
Feb 24 20:36:30 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=151 ttl=113 time=42.0 ms
Feb 24 20:36:31 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=152 ttl=113 time=42.3 ms
Feb 24 20:36:32 dev google.sh[9322]: 64 bytes from waw07s05-in-f14.1e100.net (142.250.186.206): icmp_seq=153 ttl=113 time=42.3 ms
```
## 7. (**) Написать скрипт, который выводит следующую информацию (можно переиспользовать предыдущее дз):
- кол-во процессов запущенных из под текущего пользователя
- load average за 15 минут
- кол-во свободной памяти
- свободное место в рутовом разделе /
```
#!/bin/bash

proc=$(ps -aux | awk '{print $1}' | grep "$USER" | wc -l)
echo "Количество процессов запущенных от текущего пользователя: $proc"

load_av=$(top -n1 | grep "load average"| awk '{print $14}')
echo "Средняя нагрузка на CPU за 15 минут: $load_av%"

mem_free=$(free -h | grep "Mem"| awk '{print $4}')
echo "Свободная память: $mem_free"

space=$(df -h | grep "/$"| awk '{print $4}')
echo "Свободное место в разделе /: $space"
```
## 8. (**) Добавить в cron задачу, которая будет каждые 10 минут писать в файл результаты выполнения скрипта из п.7
- Заходим в крон с помощью команды crontab -e
```
*/10 * * * * sh /home/scripts/hw4.sh > /home/scripts/hw4.log
```
## 9. (***) Сделать п. 5 для Prometheus Node Exporter
- Качаем и распаковываем Prometheus Node Exporter
```
root@dev:/home/service# wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-386.tar.gz
--2024-02-24 21:21:18--  https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-386.tar.gz
Resolving github.com (github.com)... 140.82.121.3
Connecting to github.com (github.com)|140.82.121.3|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/9524057/e81548d5-2d3b-4110-8027-dc7d0c146bbc?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240224%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240224T182118Z&X-Amz-Expires=300&X-Amz-Signature=cf889390ffcd969817d01dc1edb86c993a77627a36728c69fa7d9ca2594249b6&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=9524057&response-content-disposition=attachment%3B%20filename%3Dnode_exporter-1.7.0.linux-386.tar.gz&response-content-type=application%2Foctet-stream [following]
--2024-02-24 21:21:18--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/9524057/e81548d5-2d3b-4110-8027-dc7d0c146bbc?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240224%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240224T182118Z&X-Amz-Expires=300&X-Amz-Signature=cf889390ffcd969817d01dc1edb86c993a77627a36728c69fa7d9ca2594249b6&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=9524057&response-content-disposition=attachment%3B%20filename%3Dnode_exporter-1.7.0.linux-386.tar.gz&response-content-type=application%2Foctet-stream
Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.109.133, 185.199.108.133, 185.199.110.133, ...
Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10054801 (9.6M) [application/octet-stream]
Saving to: ‘node_exporter-1.7.0.linux-386.tar.gz’

node_exporter-1.7.0.linux-386.tar.gz        100%[=========================================================================================>]   9.59M  8.29MB/s    in 1.2s

2024-02-24 21:21:20 (8.29 MB/s) - ‘node_exporter-1.7.0.linux-386.tar.gz’ saved [10054801/10054801]

root@dev:/home/service# tar -xvf node_exporter-1.7.0.linux-386.tar.gz
node_exporter-1.7.0.linux-386/
node_exporter-1.7.0.linux-386/LICENSE
node_exporter-1.7.0.linux-386/node_exporter
node_exporter-1.7.0.linux-386/NOTICE

```
- Выдаём права на папку для пользователя vg
```
root@dev:/home/service# chown vg node_exporter-1.7.0.linux-386
root@dev:/home/service# chmod 700 node_exporter-1.7.0.linux-386
```
- Создаём файл node_exporter.service в дирректории /etc/systemd/system
```
[Unit]
Description=google service
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
Restart=always
RestartSec=1
User=vg
ExecStart=/home/service/node_exporter-1.7.0.linux-386/node_exporter

[Install]
WantedBy=multi-user.target
```
- Перезапускаем службу systemd для регистрации службы node_exporter и запустить службу node_exporter.
```
root@dev:/home/service# sudo systemctl daemon-reload
root@dev:/home/service# systemctl start node_exporter
root@dev:/home/service# systemctl status node_exporter
● node_exporter.service - google service
     Loaded: loaded (/etc/systemd/system/node_exporter.service; disabled; vendor preset: enabled)
     Active: active (running) since Sat 2024-02-24 21:25:58 +03; 5s ago
   Main PID: 10239 (node_exporter)
      Tasks: 5 (limit: 9388)
     Memory: 1.8M
        CPU: 20ms
     CGroup: /system.slice/node_exporter.service
             └─10239 /home/service/node_exporter-1.7.0.linux-386/node_exporter

Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=thermal_zone
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=time
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=timex
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=udp_queues
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=uname
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=vmstat
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=xfs
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=node_exporter.go:117 level=info collector=zfs
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.932Z caller=tls_config.go:274 level=info msg="Listening on" address=[::]:9100
Feb 24 21:25:58 dev node_exporter[10239]: ts=2024-02-24T18:25:58.933Z caller=tls_config.go:277 level=info msg="TLS is disabled." http2=false address=[::]:9100

```