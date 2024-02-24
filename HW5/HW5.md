## 1. Распределить основные сетевые протоколы (перечислены ниже) по уровням модели TCP/IP:
- Прикладной 
```
FTP
DNS
HTTP
NTP
SSH
```
- Транспортный
```
UDP
TCP
RTP
```
- Сетевой
```
ICMP
```
## 2. Узнать pid процесса и длительность подключения ssh с помощью утилиты ss
- Узнаем pid процесса SSH
```console
root@dev:~# ss -ltnup 'sport = :22'
Netid                 State                  Recv-Q                 Send-Q              Local Address:Port            Peer Address:Port                       Process
tcp                   LISTEN                 0                      128                    0.0.0.0:22                     0.0.0.0:*                  users:(("sshd",pid=820,fd=3))
tcp                   LISTEN                 0                      128                       [::]:22                        [::]:*                  users:(("sshd",pid=820,fd=4))
```
- Узнаём длительность поджключения по ssh
```console
root@dev:/home/scripts# ss -o state established '( dport = :ssh or sport = :ssh )'
Netid              Recv-Q              Send-Q                             Local Address:Port                              Peer Address:Port              Process
tcp                0                   0                                192.168.120.130:ssh                            192.168.120.237:59674              timer:(keepalive,109min,0)
```
## 3. Закрыть все порты для входящих подключений, кроме ssh
- Включаем фаервол, так как по дефолту в ubuntu 22.04 он выключен
```console
root@dev:~# ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
```
- Закрываем все порты для входящих соединений
```console
root@dev:~# ufw default deny incoming
Default incoming policy changed to 'deny'
(be sure to update your rules accordingly)
```
- Разрешаем подключение на 22 порт
```console
root@dev:~## ufw allow 22
Rules updated
Rules updated (v6)
```
## 4. Установить telnetd на VM, зайти на нее с другой VM с помощью telnet и отловить вводимый пароль и вводимые команды при входе c помощью tcpdump
- Устанавливаем  telnetd 
```console
root@dev:~# apt install telnetd -y
```
- Разрешаем подключение к VM c установленной службой telnetd
```console
root@dev:~# ufw allow 23
Rule added
Rule added (v6)
```
- Запускаем tcpdump на машине, с которой будем отлавливать. И пытаемся войти на неё с другой машины через telnet.
```console
root@dev:~# tcpdump port telnet -l -A | egrep -i -B5 'pass=|pwd=|log=|login=|user=|username=|pw=|passw=|passwd=|password=|pass:|user:|username:|password:|login:|pass |user ' 
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on ens34, link-type EN10MB (Ethernet), snapshot length 262144 bytes
.....x..<..\>.D.u.i....@l.....
.dLU....
00:18:07.156376 IP dev.telnet > 10.25.157.20.57404: Flags [P.], seq 69:80, ack 74, win 508, options [nop,nop,TS val 10151972 ecr 2825145429], length 11  #ввод логина
E..?h4@.@.....x.
......<.u.i\>.D...........
...$.dLUdev login:                             
--
.....x..<..\>.H.u.x...........
.dU!....
00:18:09.408070 IP dev.telnet > 10.25.157.20.57404: Flags [P.], seq 84:94, ack 78, win 508, options [nop,nop,TS val 10154224 ecr 2825147681], length 10  #ввод пароля
E..>h8@.@.....x.
......<.u.x\>.H...........
.....dU!Password:
--


####################################################
Hello World!!!
####################################################
Last login: Sun Feb 25 00:17:30 +03 2024 from 10.25.157.20 on pts/4       #Успешный вход на VM
```
## 5. (***) Открыть порт 222/tcp и обеспечить прослушивание порта с помощью netcat, проверить доступность порта 222 с помощью telnet и nmap.
- Открывает порт 222
```console
root@dev:~# ufw allow 222
Rule added
Rule added (v6)
```
- Обеспечиваем прослушивание порта 222 c помощью netcat
```console
netcat -l 222
```
- Проверяем открыт ли порт с другого хоста с помощью telnet
```console
vg@dev:~$ telnet 192.168.120.130 222
Trying 192.168.120.130...
Connected to 192.168.120.130.
Escape character is '^]'.  # соединение прошло успешно
```
- Проверяем открыт ли порт с другого хоста с помощью nmap 
```console
root@dev:~# nmap -sV 192.168.120.130
Starting Nmap 7.93 ( https://nmap.org ) at 2024-02-25 00:36 +03
Nmap scan report for 192.168.120.130
Host is up (0.0061s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)
23/tcp  open  telnet   Linux telnetd
222/tcp open  rsh-spx?
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.91 seconds
```