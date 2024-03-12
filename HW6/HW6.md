## 1. Определить все IP адреса, маски подсетей и соответствующие MAC адреса Linux VM. Определите класс и адреса подсетей, в которых находится VM.
- Определяем все ip адреса
```console
root@dev:~# ip a
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
       valid_lft 45100sec preferred_lft 45100sec
    inet6 fe80::20c:29ff:fe21:33/64 scope link
       valid_lft forever preferred_lft forever
```
- lo
```console
IPv4
IP-address: 127.0.0.1
Mask: 255.0.0.0
MAC-address: - 
Network class: А
Network address: 127.0.0.0
```
- ens34
```console
IPv4
IP-address: 192.168.120.130
Mask: 255.255.255.0
MAC-address: 00:0c:29:21:00:33
Network class: С
Network address: 192.168.120.0
```
- ens34
```console
IPv6
Expanded Address	- fe80:0000:0000:0000:020c:29ff:fe21:0033
Compressed address	- fe80::20c:29ff:fe21:33
Subnet prefix (masked)	- fe80:0:0:0:0:0:0:0/64
Address ID (masked)	- 0:0:0:0:20c:29ff:fe21:33/64
Prefix address		- ffff:ffff:ffff:ffff:0:0:0:0
Prefix length		- 64
Address type		- Link-Local Unicast Addresses
Network range		- fe80:0000:0000:0000:0000:0000:0000:0000 - fe80:0000:0000:0000:ffff:ffff:ffff:ffff
```

## 2. Определить публичный IP адрес хоста и Linux VM? Чем они отличаются?
- Адрес VM
```console
root@dev:~# curl 2ip.ru
37.17.51.196
```
- Внешний адрес хоста определить не удастся так как на esxi нет curl. Но он ничем не будет отличаться от внешнего адреса VM.
## 3. Вывести ARP таблицу на хосте и найти там запись, соответствующую MAC адресу с предыдущего задания. Если её нет, то объяснить почему.
- В таблице нет mac адреса из предыдущего задания, так как по умолчанию esxi показывает только адреса физических интерфейсов хоста. 
```console
[root@esxi1:~] esxcli network ip neighbor list
Neighbor         Mac Address        Vmknic    Expiry  State  Type
---------------  -----------------  ------  --------  -----  ----
192.168.120.18   00:50:56:ad:1e:e5  vmk0    1199 sec         Dynamic
192.168.120.21   00:50:56:ad:51:69  vmk0     943 sec         Dynamic
192.168.120.33   00:0c:29:3c:1e:80  vmk0      24 sec         Dynamic
192.168.120.1    64:d1:54:e0:47:dd  vmk0    1200 sec         Dynamic
192.168.120.237  00:50:56:ad:b9:cc  vmk0     893 sec         Dynamic
172.22.2.10      ac:1f:6b:24:61:8a  vmk1    1025 sec         Dynamic
172.22.1.10      ac:1f:6b:24:61:8b  vmk2     351 sec         Dynamic
```
## 4. Выполнить разбиение сети 172.20.0.0/16 на подсети с маской /24 и ответить на следующие вопросы:
- Сколько всего подсетей будет в сети?
```console
Всего будет 256 подсетей, 0 - 255
```
- Сколько узлов будет в каждой подсети?
```console
254 узла в каждой подсети
```
- Каким будет сетевой адрес первой и второй подсети?
```console
Первая подсеть: 172.20.0.0
Вторая подсеть: 172.20.1.0
```
- Каким будут адреса первого и последнего хостов в первой и второй подсетях?

```console
Первая подсеть:
172.20.0.1
172.20.0.254
```
```console
Вторая подсеть:
172.20.1.1
172.20.1.254
```
- Каким будет широковещательный адрес в последней подсети?
```console
172.20.255.255
```
## 5. Найти IP адрес соответствующий доменному имени ya.ru. Выполнить HTTP запрос на указанный IP адрес, чтобы скачать страницу с помощью утилиты curl. В результате должна вывестись HTML страничка в консоль. Подсказка: https://stackoverflow.com/questions/46563730/can-i-access-to-website-using-ip-address
- Получаем ip адрес домена ya.ru
```console
root@dev:~# ping ya.ru
PING ya.ru (5.255.255.242) 56(84) bytes of data.
64 bytes from ya.ru (5.255.255.242): icmp_seq=1 ttl=245 time=28.2 ms
64 bytes from ya.ru (5.255.255.242): icmp_seq=2 ttl=245 time=27.9 ms
64 bytes from ya.ru (5.255.255.242): icmp_seq=3 ttl=245 time=27.5 ms
^C
--- ya.ru ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 27.520/27.887/28.233/0.291 ms
```
- Получаем страницу ya.ru с помощью ip адреса.
```console
root@dev:~# curl -kvLH 'Host: ya.ru' 'https://5.255.255.242'
*   Trying 5.255.255.242:443...
* Connected to 5.255.255.242 (5.255.255.242) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* TLSv1.0 (OUT), TLS header, Certificate Status (22):
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.2 (IN), TLS header, Certificate Status (22):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS header, Finished (20):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.2 (OUT), TLS header, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* ALPN, server accepted to use h2
* Server certificate:
*  subject: C=RU; ST=Moscow; L=Moscow; O=YANDEX LLC; CN=*.xn--d1acpjx3f.xn--p1ai
*  start date: Mar  4 10:29:07 2024 GMT
*  expire date: Sep  1 20:59:59 2024 GMT
*  issuer: C=BE; O=GlobalSign nv-sa; CN=GlobalSign ECC OV SSL CA 2018
*  SSL certificate verify result: unable to get local issuer certificate (20), continuing anyway.
* Using HTTP2, server supports multiplexing
* Connection state changed (HTTP/2 confirmed)
* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* Using Stream ID: 1 (easy handle 0x557d659eeeb0)
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
> GET / HTTP/2
> Host: ya.ru
> user-agent: curl/7.81.0
> accept: */*
>
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* Connection state changed (MAX_CONCURRENT_STREAMS == 128)!
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
< HTTP/2 302
< x-yandex-eu-request: 0
< location: https://ya.ru/showcaptcha?cc=1&mt=2975C9C1116A170E7A96EAAB650C98A0782AF71A266D74EDF55F0114B30B974C5C8CD6F661E58588EE4CBB9D86DCEFCFAFE15478676A9884F359823402236ECE6F6AD8285C9896E79AE106FEFD222664FD4287131C414FD4024501E52FEBE479D7E45B4AB9BCB786537CE27C17B9848AC9BF21DF874DFC1E35669DA76FAFDA912CCB9D0D5085C8C12FB4DA87E25E135BE34034719A7A0C47C554CED1253E6F786AFDAA5AE4D00A372CE277571E5D5A936249D340E35DE871BF1A836113E845C476813EDDE856D81F08F8A4B6A7D42A51BDD0A25A2C0CF8938D0471ED97&retpath=aHR0cHM6Ly95YS5ydS8__5b12f4bf9b8c461b15a0fcaf7113a10e&t=2/1710239032/80b2bae3eb4302bf2456692decaac70d&u=7ef90623-c33e6d99-e130c8c1-62341e24&s=abcda24338bacc796ac38a8ec6c5a3fd
< nel: {"report_to": "network-errors", "max_age": 100, "success_fraction": 0.001, "failure_fraction": 0.1}
< x-content-type-options: nosniff
< x-yandex-captcha: captcha
< set-cookie: spravka=dD0xNjc4NzAzMDMyO2k9ODYuNTcuMjQ3LjI0OTtEPTE0MzQ1OEVEOTUxREJFRjQwRjU2NUFDN0U5MjdDREZCMjIwREFGODg1N0VFRTdFODcwMDNDNjAwRUE5RDdBNTU5QTZCOUIzNzkzN0ZGQzE4O3U9MTY3ODcwMzAzMjUxMTE3OTA1MztoPTJkY2UzZjZiNDQ5MWQ2ZTg1NzQxM2UxNDlhZTNjOTI2; domain=.ya.ru; path=/; expires=Thu, 11 Apr 2024 10:23:52 GMT
< set-cookie: _yasc=bmgFJVG7EGKX+qx9h8bNyHw+Ofh3vofDAiR8js53cDbuiCOSE3GuotKGh5M/BtgJCq4=; domain=.ya.ru; path=/; expires=Fri, 10 Mar 2034 10:23:52 GMT; secure
< set-cookie: i=EbNz0CW70xPn00caI5CkrkO9goVJbqFtnokski0SUaZg31E4NcE6FHRDj7dXPwZTW8Q7e9X9uU49OEw+m7euHGEWago=; Expires=Thu, 12-Mar-2026 10:23:52 GMT; Domain=.ya.ru; Path=/; Secure; HttpOnly
< set-cookie: yandexuid=2428839681710239032; Expires=Thu, 12-Mar-2026 10:23:52 GMT; Domain=.ya.ru; Path=/; Secure
< set-cookie: yashr=3835807991710239032; Path=/; Domain=.ya.ru; Expires=Wed, 12 Mar 2025 10:23:52 GMT; Secure; HttpOnly
< set-cookie: receive-cookie-deprecation=1; Path=/; Domain=.ya.ru; Expires=Wed, 12 Mar 2025 10:23:52 GMT; SameSite=None; Secure; HttpOnly; Partitioned
< x-yandex-req-id: 1710239032510009-1266949536442883968-balancer-l7leveler-kubr-yp-vla-41-BAL
< accept-ch: Sec-CH-UA-Platform-Version, Sec-CH-UA-Mobile, Sec-CH-UA-Model, Sec-CH-UA, Sec-CH-UA-Full-Version-List, Sec-CH-UA-WoW64, Sec-CH-UA-Arch, Sec-CH-UA-Bitness, Sec-CH-UA-Platform, Sec-CH-UA-Full-Version, Viewport-Width, DPR, Device-Memory, RTT, Downlink, ECT
< report-to: { "group": "network-errors", "max_age": 100, "endpoints": [{"url": "https://dr.yandex.net/nel", "priority": 1}, {"url": "https://dr2.yandex.net/nel", "priority": 2}]}
<
* Connection #0 to host 5.255.255.242 left intact
* Issue another request to this URL: 'https://ya.ru/showcaptcha?cc=1&mt=2975C9C1116A170E7A96EAAB650C98A0782AF71A266D74EDF55F0114B30B974C5C8CD6F661E58588EE4CBB9D86DCEFCFAFE15478676A9884F359823402236ECE6F6AD8285C9896E79AE106FEFD222664FD4287131C414FD4024501E52FEBE479D7E45B4AB9BCB786537CE27C17B9848AC9BF21DF874DFC1E35669DA76FAFDA912CCB9D0D5085C8C12FB4DA87E25E135BE34034719A7A0C47C554CED1253E6F786AFDAA5AE4D00A372CE277571E5D5A936249D340E35DE871BF1A836113E845C476813EDDE856D81F08F8A4B6A7D42A51BDD0A25A2C0CF8938D0471ED97&retpath=aHR0cHM6Ly95YS5ydS8__5b12f4bf9b8c461b15a0fcaf7113a10e&t=2/1710239032/80b2bae3eb4302bf2456692decaac70d&u=7ef90623-c33e6d99-e130c8c1-62341e24&s=abcda24338bacc796ac38a8ec6c5a3fd'
*   Trying 5.255.255.242:443...
* Connected to ya.ru (5.255.255.242) port 443 (#1)
* ALPN, offering h2
* ALPN, offering http/1.1
* TLSv1.0 (OUT), TLS header, Certificate Status (22):
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.2 (IN), TLS header, Certificate Status (22):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS header, Finished (20):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.2 (OUT), TLS header, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* ALPN, server accepted to use h2
* Server certificate:
*  subject: C=RU; ST=Moscow; L=Moscow; O=YANDEX LLC; CN=*.xn--d1acpjx3f.xn--p1ai
*  start date: Mar  4 10:29:07 2024 GMT
*  expire date: Sep  1 20:59:59 2024 GMT
*  issuer: C=BE; O=GlobalSign nv-sa; CN=GlobalSign ECC OV SSL CA 2018
*  SSL certificate verify result: unable to get local issuer certificate (20), continuing anyway.
* Using HTTP2, server supports multiplexing
* Connection state changed (HTTP/2 confirmed)
* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* Using Stream ID: 1 (easy handle 0x557d659eeeb0)
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
> GET /showcaptcha?cc=1&mt=2975C9C1116A170E7A96EAAB650C98A0782AF71A266D74EDF55F0114B30B974C5C8CD6F661E58588EE4CBB9D86DCEFCFAFE15478676A9884F359823402236ECE6F6AD8285C9896E79AE106FEFD222664FD4287131C414FD4024501E52FEBE479D7E45B4AB9BCB786537CE27C17B9848AC9BF21DF874DFC1E35669DA76FAFDA912CCB9D0D5085C8C12FB4DA87E25E135BE34034719A7A0C47C554CED1253E6F786AFDAA5AE4D00A372CE277571E5D5A936249D340E35DE871BF1A836113E845C476813EDDE856D81F08F8A4B6A7D42A51BDD0A25A2C0CF8938D0471ED97&retpath=aHR0cHM6Ly95YS5ydS8__5b12f4bf9b8c461b15a0fcaf7113a10e&t=2/1710239032/80b2bae3eb4302bf2456692decaac70d&u=7ef90623-c33e6d99-e130c8c1-62341e24&s=abcda24338bacc796ac38a8ec6c5a3fd HTTP/2
> Host: ya.ru
> user-agent: curl/7.81.0
> accept: */*
>
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* Connection state changed (MAX_CONCURRENT_STREAMS == 128)!
* TLSv1.2 (OUT), TLS header, Supplemental data (23):
* TLSv1.2 (IN), TLS header, Supplemental data (23):
< HTTP/2 200
< content-length: 13414
< x-yandex-eu-request: 0
< nel: {"report_to": "network-errors", "max_age": 100, "success_fraction": 0.001, "failure_fraction": 0.1}
< x-content-type-options: nosniff
< access-control-allow-origin: yastatic.net
< x-yandex-captcha: captcha
< set-cookie: _yasc=/7jGDVJAMrChXCyKGYFkWtNL1DS8Y0q7a+Nq5g8d8JZFwvRmqTfYn5mm2g1a62uXzBc=; domain=.ya.ru; path=/; expires=Fri, 10 Mar 2034 10:23:52 GMT; secure
< set-cookie: i=2PIp08BMbzHhR5cuZWg7onWPLDnCUEZK+sK8dZsJkCcP//fRe+JquBVJZgu3dLADG3cSGvTdzIconRWrfawUQjE8HcU=; Expires=Thu, 12-Mar-2026 10:23:52 GMT; Domain=.ya.ru; Path=/; Secure; HttpOnly
< set-cookie: yandexuid=2307303801710239032; Expires=Thu, 12-Mar-2026 10:23:52 GMT; Domain=.ya.ru; Path=/; Secure
< set-cookie: yashr=3572986811710239032; Path=/; Domain=.ya.ru; Expires=Wed, 12 Mar 2025 10:23:52 GMT; Secure; HttpOnly
< set-cookie: receive-cookie-deprecation=1; Path=/; Domain=.ya.ru; Expires=Wed, 12 Mar 2025 10:23:52 GMT; SameSite=None; Secure; HttpOnly; Partitioned
< x-yandex-req-id: 1710239032566827-4859122354330730380-balancer-l7leveler-kubr-yp-vla-242-BAL
< accept-ch: Sec-CH-UA-Platform-Version, Sec-CH-UA-Mobile, Sec-CH-UA-Model, Sec-CH-UA, Sec-CH-UA-Full-Version-List, Sec-CH-UA-WoW64, Sec-CH-UA-Arch, Sec-CH-UA-Bitness, Sec-CH-UA-Platform, Sec-CH-UA-Full-Version, Viewport-Width, DPR, Device-Memory, RTT, Downlink, ECT
< report-to: { "group": "network-errors", "max_age": 100, "endpoints": [{"url": "https://dr.yandex.net/nel", "priority": 1}, {"url": "https://dr2.yandex.net/nel", "priority": 2}]}
< content-type: text/html
<
<!doctype html><html prefix="og: http://ogp.me/ns#"><meta http-equiv="X-UA-Compatible" content="IE=edge"><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
    <link rel="icon" href="https://yastatic.net/s3/home-static/_/a6/a6a296b741b51880ae8a9b04a67cfe3f.png" sizes="16x16">
    <link rel="icon" href="https://yastatic.net/s3/home-static/_/f4/f47b1b3d8194c36ce660324ab55a04fe.png" sizes="32x32">
    <link rel="icon" href="https://yastatic.net/s3/home-static/_/f0/f0597b6727cc67dceebc4e3a87caf571.png" sizes="192x192">
    <link rel="apple-touch-icon" href="https://yastatic.net/s3/home-static/_/a7/a79b81aa025e9edb2244e38581c868ad.png" sizes="152x152">
    <link rel="apple-touch-icon" href="https://yastatic.net/s3/home-static/_/46/462e92b9e3792be37a1c3fdefb26af28.png" sizes="180x180">
<title data-react-helmet="true">Ой, Капча!</title><meta data-react-helmet="true" property="og:title" content="Яндекс"><meta data-react-helmet="true" property="og:description" content="Найдётся всё"><meta data-react-helmet="true" property="og:image" content="https://yastatic.net/s3/home-static/_/37/37a02b5dc7a51abac55d8a5b6c865f0e.png"><link rel="stylesheet" href="/captcha_smart.da515c9dea7ca689654d.min.css?k=1709106734276"><style>@media only screen and (min-width:651px){body{background-image:url('https://captcha-backgrounds.s3.yandex.net/static/default-background.jpg')}}.LogoLink{background-image:url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iODYiIGhlaWdodD0iMzYiIHZpZXdCb3g9IjAgMCAzNzggOTEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgZmlsbD0ibm9uZSI+PHBhdGggZD0iTTI0OS43ODkgODQuODY4OVY3Mi40MTQ2QzI0NSA3NS42MjQ1IDIzNi45NzYgNzguNDQ5MiAyMjkuNDY5IDc4LjQ0OTJDMjE4LjIxIDc4LjQ0OTIgMjEzLjkzOSA3My4xODUgMjEzLjI5MSA2Mi4zOTk4SDI1MC40MzZWNTQuMzEwOUMyNTAuNDM2IDMxLjg0MTcgMjQwLjQ3MSAyMy4zNjc3IDIyNS4wNjkgMjMuMzY3N0MyMDYuMzAzIDIzLjM2NzcgMTk3LjM3MiAzNy42MTk1IDE5Ny4zNzIgNTcuMTM1NkMxOTcuMzcyIDc5LjYwNDcgMjA4LjUwMyA5MC41MTgzIDIyOC4xNzUgOTAuNTE4M0MyMzguMDExIDkwLjUxODMgMjQ1LjI1OSA4Ny45NTA0IDI0OS43ODkgODQuODY4OVpNMzQ2LjA4MSA5MC41MTgzQzM1My4xOTkgOTAuNTE4MyAzNTguMjQ3IDg5LjIzNDMgMzYyIDg2LjUzOFY3NC4wODM3QzM1OC4xMTcgNzYuNzggMzUzLjQ1OCA3OC40NDkyIDM0Ni45ODcgNzguNDQ5MkMzMzUuOTg2IDc4LjQ0OTIgMzMxLjQ1NiA2OS45NzUxIDMzMS40NTYgNTYuNjIyQzMzMS40NTYgNDIuNjI2OSAzMzcuMDIxIDM1LjQzNjggMzQ3LjExNiAzNS40MzY4QzM1My4wNyAzNS40MzY4IDM1OC44OTQgMzcuNDkxMSAzNjIgMzkuNDE3MVYyNi40NDkyQzM1OC43NjQgMjQuNjUxNiAzNTMuMDcgMjMuMzY3NyAzNDUuNDM0IDIzLjM2NzdDMzI1Ljc2MSAyMy4zNjc3IDMxNS41MzcgMzcuMzYyNyAzMTUuNTM3IDU3LjAwNzJDMzE1LjUzNyA3OC41Nzc2IDMyNS41MDIgOTAuNTE4MyAzNDYuMDgxIDkwLjUxODNaTTEwOC43MTcgMjQuNjUxNlY1MC4yMDIySDg4LjEzODJWMjQuNjUxNkg3Mi43MzY3Vjg5LjIzNDNIODguMTM4MlY2Mi4yNzE0SDEwOC43MTdWODkuMjM0M0gxMjQuMTE4VjI0LjY1MTZIMTA4LjcxN1pNMTkzLjYxOSA3Ny4xNjUySDE4Ni43NTlWMjQuNjUxNkgxNDEuODQ5VjMwLjE3MjZDMTQxLjg0OSA0NS45NjUyIDE0MC44MTQgNjYuMzggMTM1LjM3OCA3Ny4xNjUySDEzMC41ODlWMTA0SDE0NC44MjZWODkuMjM0M0gxNzkuMzgyVjEwNEgxOTMuNjE5Vjc3LjE2NTJaTTI5OC45NyA4OS4yMzQzSDMxNi40NDNMMjkxLjcyMyA1NC40MzkzTDMxMy40NjYgMjQuNjUxNkgyOTcuOTM1TDI3Ni4xOTIgNTQuNDM5M1YyNC42NTE2SDI2MC43OVY4OS4yMzQzSDI3Ni4xOTJWNTcuNTIwOEwyOTguOTcgODkuMjM0M1pNMjI0LjgxIDM1LjQzNjhDMjMyLjQ0NiAzNS40MzY4IDIzNC43NzYgNDEuNzI4MiAyMzQuNzc2IDQ5LjgxNzFWNTEuMTAxSDIxMy4yOTFDMjEzLjY4IDQwLjgyOTQgMjE3LjQzMyAzNS40MzY4IDIyNC44MSAzNS40MzY4Wk0xNzEuMzU4IDc3LjE2NTJIMTQ5LjYxNUMxNTMuODg2IDY3LjQwNzIgMTU1LjA1MSA0OS44MTcxIDE1NS4wNTEgMzguNjQ2N1YzNi43MjA4SDE3MS4zNThWNzcuMTY1MloiIGZpbGw9ImJsYWNrIj48L3BhdGg+CiAgICAgICAgPHBhdGggZD0iTTQ0LjEzMzcgODkuMjM0Nkg1OS43OTRWMEgzNy4wMTUzQzE0LjEwNzIgMCAyLjA3MDc5IDExLjY4NCAyLjA3MDc5IDI4Ljg4ODlDMi4wNzA3OSA0Mi42MjcyIDguNjcxNDMgNTAuNzE2IDIwLjQ0OSA1OS4wNjE3TDAgODkuMjM0NkgxNi45NTQ2TDM5LjczMzMgNTUuNDY2N0wzMS44Mzg0IDUwLjIwMjVDMjIuMjYxIDQzLjc4MjcgMTcuNjAxNyAzOC43NzUzIDE3LjYwMTcgMjcuOTkwMUMxNy42MDE3IDE4LjQ4ODkgMjQuMzMxOCAxMi4wNjkxIDM3LjE0NDggMTIuMDY5MUg0NC4xMzM3Vjg5LjIzNDZaIiBmaWxsPSIjRkMzRjFEIj48L3BhdGg+PC9zdmc+')}</style><div id="root"><div class="Theme Theme_color_yandex-default Theme_root_default"><div class="Container"><div class="Spacer" style="padding-bottom:40px"><a href="https://www.ya.ru" aria-label="Yandex" class="Link Link_view_default LogoLink"></a></div><form method="POST" action="/checkcaptcha?key=c6d8c23d-93f47b18-5e7701e3-faf80edc_2/1710239032/80b2bae3eb4302bf2456692decaac70d_6b0846d1571d64263bd223935c168eab&mt=D1AABFE64B9593024647CC6E46D30AA9E18EBFEC6C4575827EDA407C099441E08E6399B40EE4131C5667E4D75994A17C4D9AC25BE0B00602E9EC8753069A99068A61F414827BF9D6E67BC7F032014127208991E9237768386B46391C3B44FEFC4505EB2887C99014ED2E7C54FE864C19761DE6EB7D48E2BB1B4E8FF5F19E7C312D027CD536C70C002FACE5E3B63D9243F4DA0806134FC43414AE2F4367BCF9E2B61D82713D0AE75BC5BD8F966F2AC0FF958E3ED5DE6251F4E7A92D99BD21D976282CB080376F05845C9B1B74BBC4E4A858FC7341F155FD2E419827ABDD&retpath=aHR0cHM6Ly95YS5ydS8__5b12f4bf9b8c461b15a0fcaf7113a10e&u=7ef90623-c33e6d99-e130c8c1-62341e24&s=4a4f8606b67d020720d96e3a124a7abc" id="checkbox-captcha-form"><div class="Spacer" style="padding-bottom:16px"><span class="Text Text_weight_medium Text_typography_headline-s">Подтвердите, что запросы отправляли вы, а не робот</span></div><div class="Spacer" style="padding-bottom:16px"><span class="Text Text_weight_regular Text_typography_body-long-m">Нам очень жаль, но запросы с вашего устройства похожи на автоматические.   <a href="https://yandex.ru/support/smart-captcha/problems.html?form-unique_key=7ef90623-c33e6d99-e130c8c1-62341e24" class="Link Link_view_default">Почему это могло произойти?</a></span></div><noscript><span class="Text Text_color_alert Text_weight_medium Text_typography_body-long-m">У вас отключено исполнение JavaScript. По нажатию вы будете направлены на дополнительную проверку. <a href="https://yandex.ru/support/common/browsers-settings/browsers-java-js-settings.html" class="Link Link_view_default">Как включить JavaScript?</a></span></noscript><div class="Spacer Spacer_auto-gap_bottom" style="padding-top:40px;padding-bottom:40px"><div class="CheckboxCaptcha" data-testid="checkbox-captcha"><div class="CheckboxCaptcha-Inner"><div class="CheckboxCaptcha-Anchor"><input type="button" id="js-button" class="CheckboxCaptcha-Button" aria-checked="false" aria-labelledby="checkbox-label" aria-describedby="checkbox-description" role="checkbox"><noscript><input type="submit" class="CheckboxCaptcha-Button" aria-checked="false" aria-labelledby="checkbox-label" aria-describedby="checkbox-description" role="checkbox"></noscript><div class="CheckboxCaptcha-Checkbox" data-checked="false"><svg class="SvgIcon CheckIcon" width="24" height="24" viewBox="0 0 24 25" fill="none"><path d="M4 12.5L9.5 18.5L20 6.5" stroke="#000" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"></path></svg></div></div><div class="CheckboxCaptcha-Label"><span class="Text Text_weight_regular Text_typography_control-xxl CheckboxCaptcha-LabelText"><span id="checkbox-label">Я не робот </span></span><span class="Text Text_color_control-secondary Text_weight_regular Text_typography_control-l CheckboxCaptcha-SecondaryText"><span id="checkbox-description">Нажмите, чтобы продолжить</span></span></div></div><div class="Text Text_color_ghost Text_weight_regular Text_typography_control-s CaptchaLinks CheckboxCaptcha-Links"><button aria-label="Показать ссылки" aria-pressed="false" type="button" class="CaptchaButton CaptchaButton_view_clear CaptchaButton_size_m CaptchaLinks-ToggleButton CaptchaLinks-ToggleButton_checkbox"><svg class="SvgIcon" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 22 22" fill="none"><path fill-rule="evenodd" clip-rule="evenodd" d="M11 18.5625C15.1766 18.5625 18.5625 15.1766 18.5625 11C18.5625 6.82334 15.1766 3.4375 11 3.4375C6.82334 3.4375 3.4375 6.82334 3.4375 11C3.4375 15.1766 6.82334 18.5625 11 18.5625ZM11 20.625C16.3157 20.625 20.625 16.3157 20.625 11C20.625 5.68426 16.3157 1.375 11 1.375C5.68426 1.375 1.375 5.68426 1.375 11C1.375 16.3157 5.68426 20.625 11 20.625ZM8.85528 6.24171C9.44645 5.75611 10.2222 5.46546 11 5.46546C12.6736 5.46546 14.2167 6.59336 14.2167 8.409C14.2167 8.92624 14.1095 9.43266 13.8078 9.92185C13.5213 10.3865 13.1023 10.7646 12.6048 11.1132C12.3057 11.3227 12.1569 11.4663 12.0839 11.5642C12.0312 11.6348 12.0312 11.661 12.0313 11.686L12.0313 11.6872C12.0313 12.2567 11.5695 12.7185 11 12.7185C10.4305 12.7185 9.96876 12.2567 9.96876 11.6872C9.96876 10.5945 10.7163 9.9179 11.4214 9.42397C11.806 9.15451 11.9732 8.9675 12.0523 8.83924C12.1163 8.73548 12.1542 8.62111 12.1542 8.409C12.1542 7.9976 11.8192 7.52796 11 7.52796C10.718 7.52796 10.401 7.6411 10.1644 7.83546C9.9342 8.02457 9.84579 8.22978 9.84579 8.409C9.84579 8.97854 9.38408 9.44025 8.81454 9.44025C8.24499 9.44025 7.78329 8.97854 7.78329 8.409C7.78329 7.48351 8.25771 6.73257 8.85528 6.24171ZM11 16.5C11.7594 16.5 12.375 15.8844 12.375 15.125C12.375 14.3656 11.7594 13.75 11 13.75C10.2406 13.75 9.625 14.3656 9.625 15.125C9.625 15.8844 10.2406 16.5 11 16.5Z" fill="currentColor"></path></svg></button><div class="CaptchaLinks-Links"><a color="secondary" target="_blank" href="https://cloud.yandex.ru/services/smartcaptcha?utm_source=captcha&amp;utm_medium=chbx&amp;utm_campaign=security" class="Link Link_color_secondary Link_view_captcha">SmartCaptcha by Yandex Cloud</a></div></div></div></div><input type="hidden" name="rdata"><input type="hidden" name="pdata" value="eyJwb3dDYWxjVGltZSI6LTEsInBvd05vbmNlIjoiIiwicG93UHJlZml4IjoiIn0="><input type="hidden" name="tdata"><input type="hidden" name="picasso"></form><span class="Text Text_color_ghost Text_weight_regular Text_typography_control-xs">Если у вас возникли проблемы, пожалуйста, воспользуйтесь <a href="https://yandex.ru/support/smart-captcha/problems.html?form-unique_key=7ef90623-c33e6d99-e130c8c1-62341e24" class="Link Link_view_default">формой обратной связи</a></span><div class="Spacer" style="padding-top:10px"><span class="Text Text_color_ghost Text_weight_light Text_typography_control-xxs">7ef90623-c33e6d99-e130c8c1-62341e24:1709106734287</span></div></div></div></div><script>const button=document.getElementById("js-button");button.addEventListener("click",function n(t){window.__JS_BUTTON_CLICKED__=!0,this.removeEventListener("click",n,!1)},!1),window.onerror=function(n,t){0===t.indexOf(window.location.origin+"/captcha_smart.da515c9dea7ca689654d.min.js")&&(button.type="submit",window.Ya&&window.Ya.Rum&&window.Ya.Rum.logEventString&&window.Ya.Rum.logEventString("js_fail_force_submit_type",n,{page:"checkbox"}))}</script> <script>window.__SSR_DATA__={url:"/ru/checkbox",invalid:"no",formAction:"/checkcaptcha?key=c6d8c23d-93f47b18-5e7701e3-faf80edc_2/1710239032/80b2bae3eb4302bf2456692decaac70d_6b0846d1571d64263bd223935c168eab&mt=D1AABFE64B9593024647CC6E46D30AA9E18EBFEC6C4575827EDA407C099441E08E6399B40EE4131C5667E4D75994A17C4D9AC25BE0B00602E9EC8753069A99068A61F414827BF9D6E67BC7F032014127208991E9237768386B46391C3B44FEFC4505EB2887C99014ED2E7C54FE864C19761DE6EB7D48E2BB1B4E8FF5F19E7C312D027CD536C70C002FACE5E3B63D9243F4DA0806134FC43414AE2F4367BCF9E2B61D82713D0AE75BC5BD8F966F2AC0FF958E3ED5DE6251F4E7A92D99BD21D976282CB080376F05845C9B1B74BBC4E4A858FC7341F155FD2E419827ABDD&retpath=aHR0cHM6Ly95YS5ydS8__5b12f4bf9b8c461b15a0fcaf7113a10e&u=7ef90623-c33e6d99-e130c8c1-62341e24&s=4a4f8606b67d020720d96e3a124a7abc",captchaKey:"c6d8c23d-93f47b18-5e7701e3-faf80edc_2/1710239032/80b2bae3eb4302bf2456692decaac70d_6b0846d1571d64263bd223935c168eab",imageSrc:"",taskImageSrc:"",task:"",voiceSrc:"",introSrc:"",aesKey:"HqeGqBJepfq6Jccbi2RckwsVF/Ih4Y2kWRVmtPyBAWw=",aesSign:"1_1710239032_12408446463067041841_5788ceb5a2e677f423c172c4b542b3a7",reqId:"1710239032566827-4859122354330730380-balancer-l7leveler-kubr-yp-vla-242-BAL",uniqueKey:"7ef90623-c33e6d99-e130c8c1-62341e24",powPrefix:"743D313731303233393033323B703D393236303166312D38323639373430342D38633434356134352D37633364646665363B633D31353B643D33344438434236414135354539463945423633353941354233423846453332413B",powComplexity:"15",sitekey:"",smartCaptchaHost:""}</script><script src="/captcha_smart_error.da515c9dea7ca689654d.min.js?k=1709106734276" crossorigin=""></script><script src="/captcha_smart_react.min.js?k=1709106734276" crossorigin=""></script><script src="/captcha_smart.da515c9dea7ca689654d.min.js?k=1709106734276" crossorigin=""></script><script>!function(e,n,t,a,c){e.ym=e.ym||function(){(e.ym.a=e.ym.a||[]).push(arguments)},e.ym.l=+new Date,a=n.createElement(t),c=n.getElementsByTagName(t)[0],a.async=1,a.src="https://mc.yandex.ru/metrika/tag.js",c.parentNode.insertBefore(a,c)}(window,document,"script"),ym(10630330,"init",{clickmap:!0,trackLinks:!0,accurateTrackBounce:!0,webvisor:!0,ut:"noindex",params:{req_id:"1710239032566827-4859122354330730380-balancer-l7leveler-kubr-yp-vla-242-BAL",unique_key:"7ef90623-c33e6d99-e130c8c1-62341e24"}})</script><noscript><div><img src="https://mc.yandex.ru/watch/10630330?ut=noindex" style="position:absolute;left:-9999px" alt=""></div></noscript><div><img src="https://adfstat.yandex.ru/captcha?req_id=1710239032566827-4859122354330730380-balancer-l7leveler-kubr-yp-vla-242-BA* Connection #1 to host ya.ru left intact
L&unique_key=7ef90623-c33e6d99-e130c8c1-62341e24" style="position:absolute;left:-9999px" alt=""></div>root@dev:~#

```