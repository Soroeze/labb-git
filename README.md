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
##### Ubuntu -> Windows
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
##### Windows -> Ubuntu
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
##### Linux/Ubuntu
```
chas@chas-VMware-Virtual-Platform:~$ sudo mkdir -p /var/systementor/konsultdata
chas@chas-VMware-Virtual-Platform:~$ cd /var/systementor/konsultdata
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ sudo touch anteckningar.txt
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ sudo groupadd konsulter
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ sudo chown -R root:konsulter /var/systementor/konsultdata
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ sudo chmod 750 /var/systementor/konsultdata
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ sudo chmod 640 anteckningar.txt
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ sudo ls -la
total 8
drwxr-x--- 2 root konsulter 4096 Sep 22 20:05 .
drwxr-xr-x 3 root root      4096 Sep 22 20:04 ..
-rw-r----- 1 root konsulter    0 Sep 22 20:05 anteckningar.txt
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:63:b9:43 brd ff:ff:ff:ff:ff:ff
    inet 192.168.136.129/24 brd 192.168.136.255 scope global dynamic noprefixroute ens33
       valid_lft 1180sec preferred_lft 1180sec
chas@chas-VMware-Virtual-Platform:/var/systementor/konsultdata$ ping -c 4 192.168.136.128
PING 192.168.136.128 (192.168.136.128) 56(84) bytes of data.
64 bytes from 192.168.136.128: icmp_seq=1 ttl=128 time=0.987 ms
64 bytes from 192.168.136.128: icmp_seq=2 ttl=128 time=0.345 ms
64 bytes from 192.168.136.128: icmp_seq=3 ttl=128 time=0.500 ms
64 bytes from 192.168.136.128: icmp_seq=4 ttl=128 time=0.695 ms

--- 192.168.136.128 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3079ms
rtt min/avg/max/mdev = 0.345/0.631/0.987/0.239 ms
```
##### Windows 11
###### CMD
```
C:\Users\Chassy>mkdir C:\Systementor\KonsultData
C:\Users\Chassy>ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : Chas
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : localdomain
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-0C-29-F4-73-AE
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::f905:e3fa:669c:b41d%10(Preferred)
   IPv4 Address. . . . . . . . . . . : 192.168.136.128(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : den 22 september 2026 20:11:06
   Lease Expires . . . . . . . . . . : den 22 september 2026 20:56:06
   Default Gateway . . . . . . . . . :
   DHCP Server . . . . . . . . . . . : 192.168.136.254
   DHCPv6 IAID . . . . . . . . . . . : 83889193
   DHCPv6 Client DUID. . . . . . . . : 00-01-01-00-32-28-DD-AF-00-0C-29-F4-73-AE
   DNS Servers . . . . . . . . . . . : 192.168.136.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
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
###### Powershell
```
PS C:\WINDOWS\system32> Get-Acl -Path "C:\Systementor\KonsultData" | Format-List


Path   : Microsoft.PowerShell.Core\FileSystem::C:\Systementor\KonsultData
Owner  : Chas\Chassy
Group  : Chas\Ingen
Access : BUILTIN\Administratörer Allow  FullControl
         NT instans\SYSTEM Allow  FullControl
         BUILTIN\Användare Allow  ReadAndExecute, Synchronize
         NT instans\Autentiserade användare Allow  Modify, Synchronize
         NT instans\Autentiserade användare Allow  -536805376
Audit  :
Sddl   : O:S-1-5-21-4132158795-2060570990-1823972835-1001G:S-1-5-21-4132158795-2060570990-1823972835-513D:AI(A;OICIID;F
         A;;;BA)(A;OICIID;FA;;;SY)(A;OICIID;0x1200a9;;;BU)(A;ID;0x1301bf;;;AU)(A;OICIIOID;SDGXGWGR;;;AU)



```
## 4. Git & Versionshantering (Kursmål 10)

## 5. AI-logg & Reflektion (Kursmål 11)
### Förtext
***Jag kör på "tillfällig" eller inkognito-session på Gemini AI för att utesluta minne eller personliga referenser.***

```

```