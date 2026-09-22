# <ins>**Labbmiljö, Git, CLI och AI**</ins>
## 1. Titel & Introduktion
- **Kurs:** Introduktion till yrkesrollen och grunderna i IT-infrastruktur (MYH 2025/4008)
- **Student:** Joakim Tran
- **Datum:** 2026-09-22
- **Beskrivning av labben:** Vi ska redovisa vår kunskap och problemlösning som visas upp på labbmiljöerna och uppgifter. Första är att vi uppgör en teknisk dokumentation som ska fullfölja dokumentationens/uppgiftens hänvisningar

## 2. Labbmiljö & Nätverk (Kursmål 8)
### Felsökning
Windows 11 har oftast standard att inte tillåta ping/ICMP in till sig själv men ut går bra. Fick köra kommandot "netsh advfirewall firewall add rule name="Let ping in" protocol=icmpv4:any,any dir=in action=allow"<sup>1</sup> i CMD

### VMs och nätverk
| Hostname                     | Operativsystem     | IP-adress       | Subnätmask    | Standard Gateway |
| ---------------------------- | ------------------ | --------------- | ------------- | ---------------- |
| Chas                         | Windows 11         | 192.168.136.128 | 255.255.255.0 | 192.168.136.1    |
| Chas-VMware-Virtual-Platform | Ubuntu 26.04.1 LTS | 192.168.136.129 | 255.255.255.0 | 192.168.136.1    |

#### PING/ICMP
**Ubuntu -> Windows**
```
chas@chas-VMware-Virtual-Platform:~$ ping -c 4 192.168.136.128
PING 192.168.136.128 (192.168.136.128) 56(84) bytes of data.
64 bytes from 192.168.136.128: icmp_seq=1 ttl=128 time=0.482 ms
64 bytes from 192.168.136.128: icmp_seq=2 ttl=128 time=0.452 ms
64 bytes from 192.168.136.128: icmp_seq=3 ttl=128 time=0.417 ms
64 bytes from 192.168.136.128: icmp_seq=4 ttl=128 time=0.511 ms

--- 192.168.136.128 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3092ms
rtt min/avg/max/mdev = 0.417/0.465/0.511/0.034 ms
```
**Windows -> Ubuntu**
```
Microsoft Windows [Version 10.0.26200.9168]
(c) Microsoft Corporation. Med ensamrätt.

C:\Users\Chassy>ping 192.168.136.129

Pinging 192.168.136.129 with 32 bytes of data:
Reply from 192.168.136.129: bytes=32 time<1ms TTL=64
Reply from 192.168.136.129: bytes=32 time<1ms TTL=64
Reply from 192.168.136.129: bytes=32 time<1ms TTL=64
Reply from 192.168.136.129: bytes=32 time<1ms TTL=64

Ping statistics for 192.168.136.129:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
## 3. Kommandoradsgenomförande (Kursmål 9)

## 4. Git & Versionshantering (Kursmål 10)

## 5. AI-logg & Reflektion (Kursmål 11)