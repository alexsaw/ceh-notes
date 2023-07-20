# Day 2

## 1. Host Discovery

**METHOD 1**
```
sudo netdiscover -r 10.0.0.0/16
```
OUTPUT:
```
 Currently scanning: Finished!   |   Screen View: Unique Hosts                 
                                                                               
 110 Captured ARP Req/Rep packets, from 109 hosts.   Total size: 4620          
 _____________________________________________________________________________ 
   IP            At MAC Address      Count  Len   MAC Vendor                   
 ----------------------------------------------------------------------------- 
 10.0.0.2        06:6c:0c:f8:6a:1c    01    042   Unknown vendor               
 10.0.128.1      06:6c:0c:f8:6a:1c    02    084   Unknown vendor               
 10.0.128.19     06:c7:8c:10:f1:c3    01    042   Unknown vendor               
 10.0.128.145    06:e2:60:76:88:c3    01    042   Unknown vendor               
 10.0.128.155    06:6e:06:28:e4:8b    01    042   Unknown vendor               
 10.0.128.195    06:41:3c:22:cc:d3    01    042   Unknown vendor               
 10.0.129.175    06:56:93:2b:a2:cf    01    042   Unknown vendor               
 10.0.130.169    06:3b:ff:10:3f:37    01    042   Unknown vendor               
 10.0.131.197    06:8d:f3:cf:59:a3    01    042   Unknown vendor               
 10.0.131.228    06:8e:44:0f:72:99    01    042   Unknown vendor               
 10.0.132.99     06:79:d7:9f:b7:47    01    042   Unknown vendor               
 10.0.133.210    06:69:de:84:d3:2f    01    042   Unknown vendor               
 10.0.134.180    06:05:2d:b6:67:3d    01    042   Unknown vendor               
 10.0.136.156    06:33:77:ea:49:8b    01    042   Unknown vendor               
 10.0.136.181    06:af:7d:b5:50:69    01    042   Unknown vendor               
 10.0.137.30     06:88:82:e2:aa:3b    01    042   Unknown vendor               
 10.0.137.35     06:c4:e3:34:26:53    01    042   Unknown vendor    
```

**METHOD 2**
```
sudo netdiscover -r 10.0.0.0/16 -P > discovered_hosts.txt
```
OUTPUT:
```
discovered_hosts.txt
```

### Discovering port 80 on each host

```
awk '{print $1}' filename.txt > ipaddresses.txt

```

```
nmap -iL ip_addresses -p 80 -oG hosts_with_80_open

```

### TCP/IP handshake using Nmap
```
nmap -sT -p80 skillsetlocal.com
```


## 2. TCP Port Scanning with Nmap

**METHOD 1**
```
nmap -sT skillsetlocal.com
```
OUTPUT:
```
Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-18 20:09 UTC
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.000039s latency).
rDNS record for 127.0.0.1: localhost
Not shown: 989 closed ports
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
25/tcp    open  smtp
53/tcp    open  domain
80/tcp    open  http
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3306/tcp  open  mysql
5432/tcp  open  postgresql
12345/tcp open  netbus

Nmap done: 1 IP address (1 host up) scanned in 0.20 seconds
```
### Ping sweep with Nmap
**METHOD 1**
```
nmap -sn 10.0.128.0/18
```
OUTPUT:
```
Nmap scan report for ip-10-0-128-145.us-west-2.compute.internal (10.0.128.145)
Host is up (0.0012s latency).
Nmap scan report for ip-10-0-128-155.us-west-2.compute.internal (10.0.128.155)
Host is up (0.0014s latency).
Nmap scan report for ip-10-0-128-195.us-west-2.compute.internal (10.0.128.195)
Host is up (0.0015s latency).
Nmap scan report for ip-10-0-129-46.us-west-2.compute.internal (10.0.129.46)
Host is up (0.0012s latency).
Nmap scan report for ip-10-0-129-108.us-west-2.compute.internal (10.0.129.108)
Host is up (0.0019s latency).
...
```

### Run TCP Connect scan on devices

**METHOD 1**
```
nmap -sT 10.0.129.46 10.0.128.155
```
OUTPUT:
```
Nmap scan report for ip-10-0-129-46.us-west-2.compute.internal (10.0.129.46)
Host is up (0.00056s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap scan report for ip-10-0-128-155.us-west-2.compute.internal (10.0.128.155)
Host is up (0.00067s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

### Run TCP scan on range

```
nmap -sT 10.0.129.1-254
```
OUTPUT:
```
Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-18 20:21 UTC
Nmap scan report for ip-10-0-129-46.us-west-2.compute.internal (10.0.129.46)
Host is up (0.00067s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap scan report for ip-10-0-129-108.us-west-2.compute.internal (10.0.129.108)
Host is up (0.00056s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap scan report for ip-10-0-129-175.us-west-2.compute.internal (10.0.129.175)
Host is up (0.00056s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

### Scan a specific port

```
nmap -sT skillsetlocal.com -p 6379
```

OUTPUT:
```
Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-18 20:22 UTC
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.000079s latency).
rDNS record for 127.0.0.1: localhost
PORT     STATE  SERVICE
6379/tcp closed unknown
```

## 3. UDP Port scanning with Nmap

```
sudo nmap -sU skillsetlocal.com
```

OUTPUT:
```
Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-18 20:24 UTC
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.0000020s latency).
rDNS record for 127.0.0.1: localhost
Not shown: 993 closed ports
PORT    STATE         SERVICE
53/udp  open          domain
69/udp  open|filtered tftp
123/udp open          ntp
137/udp open          netbios-ns
138/udp open|filtered netbios-dgm
161/udp open          snmp
513/udp open|filtered who
```

## 4. UDP and TCP Port scanning combination

```
sudo nmap -sU -sT skillsetlocal.com
```

OUTPUT:
```
Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-18 20:26 UTC
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.000041s latency).
rDNS record for 127.0.0.1: localhost
Not shown: 1982 closed ports
PORT      STATE         SERVICE
21/tcp    open          ftp
22/tcp    open          ssh
23/tcp    open          telnet
25/tcp    open          smtp
53/tcp    open          domain
80/tcp    open          http
139/tcp   open          netbios-ssn
445/tcp   open          microsoft-ds
3306/tcp  open          mysql
5432/tcp  open          postgresql
12345/tcp open          netbus
53/udp    open          domain
69/udp    open|filtered tftp
123/udp   open          ntp
137/udp   open          netbios-ns
138/udp   open|filtered netbios-dgm
161/udp   open          snmp
513/udp   open|filtered who

Nmap done: 1 IP address (1 host up) scanned in 1.27 seconds
```

## 5. Outputting to file

```
nmap -sn 10.0.128-130.0/24 -oG pingscan.out
```

OUTPUT:
```
cat pingscan.out

# Nmap 7.01 scan initiated Tue Jul 18 20:27:49 2023 as: nmap -sn -oG pingscan.out 10.0.128-130.0/24
Host: 10.0.128.145 (ip-10-0-128-145.us-west-2.compute.internal) Status: Up
Host: 10.0.128.155 (ip-10-0-128-155.us-west-2.compute.internal) Status: Up
Host: 10.0.128.195 (ip-10-0-128-195.us-west-2.compute.internal) Status: Up
Host: 10.0.129.46 (ip-10-0-129-46.us-west-2.compute.internal)   Status: Up
Host: 10.0.129.175 (ip-10-0-129-175.us-west-2.compute.internal) Status: Up
Host: 10.0.130.169 (ip-10-0-130-169.us-west-2.compute.internal) Status: Up
# Nmap done at Tue Jul 18 20:27:55 2023 -- 768 IP addresses (6 hosts up) scanned in 6.21 seconds
```
```
cat pingscan.out | grep Up > pingscan.out1

cat pingscan.out1

Host: 10.0.128.145 (ip-10-0-128-145.us-west-2.compute.internal) Status: Up
Host: 10.0.128.155 (ip-10-0-128-155.us-west-2.compute.internal) Status: Up
Host: 10.0.128.195 (ip-10-0-128-195.us-west-2.compute.internal) Status: Up
Host: 10.0.129.46 (ip-10-0-129-46.us-west-2.compute.internal)   Status: Up
Host: 10.0.129.175 (ip-10-0-129-175.us-west-2.compute.internal) Status: Up
Host: 10.0.130.169 (ip-10-0-130-169.us-west-2.compute.internal) Status: Up

```
```
cat pingscan.out1 | cut -f2 -d" " > pingscan.out2

10.0.128.145
10.0.128.155
10.0.128.195
10.0.129.46
10.0.129.175
10.0.130.169
```

## 6. Nmap Scan from list file

```
nmap -sT -iL pingscan.out2 -p 80
```

Output:

```

Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-18 20:31 UTC
Nmap scan report for ip-10-0-128-145.us-west-2.compute.internal (10.0.128.145)
Host is up (0.00042s latency).
PORT   STATE  SERVICE
80/tcp closed http

Nmap scan report for ip-10-0-128-155.us-west-2.compute.internal (10.0.128.155)
Host is up (0.00052s latency).
PORT   STATE SERVICE
80/tcp open  http

Nmap scan report for ip-10-0-128-195.us-west-2.compute.internal (10.0.128.195)
Host is up (0.00046s latency).
PORT   STATE  SERVICE
80/tcp closed http

Nmap scan report for ip-10-0-129-46.us-west-2.compute.internal (10.0.129.46)
Host is up (0.00045s latency).
PORT   STATE SERVICE
80/tcp open  http

Nmap scan report for ip-10-0-129-175.us-west-2.compute.internal (10.0.129.175)
Host is up (0.00051s latency).
PORT   STATE SERVICE
80/tcp open  http

Nmap scan report for ip-10-0-130-169.us-west-2.compute.internal (10.0.130.169)
Host is up (0.00053s latency).
PORT   STATE SERVICE
80/tcp open  http
```

## 7. Protocol Scan

```
sudo nmap -sO skillsetlocal.com

Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-18 20:32 UTC
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.0000020s latency).
rDNS record for 127.0.0.1: localhost
Not shown: 248 closed protocols
PROTOCOL STATE         SERVICE
1        open          icmp
2        open|filtered igmp
6        open          tcp
17       open          udp
47       open|filtered gre
103      open|filtered pim
136      open|filtered udplite
255      open|filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 1.21 seconds

```


## 8. Output with --packet-trace option
```

nmap -sn 10.0.128.0/24 --packet-trace
```

## 9. List Scan

```
nmap -sL 10.0.128.0/24 

Nmap scan report for ip-10-0-128-237.us-west-2.compute.internal (10.0.128.237)
Nmap scan report for ip-10-0-128-238.us-west-2.compute.internal (10.0.128.238)
Nmap scan report for ip-10-0-128-239.us-west-2.compute.internal (10.0.128.239)
Nmap scan report for ip-10-0-128-240.us-west-2.compute.internal (10.0.128.240)
Nmap scan report for ip-10-0-128-241.us-west-2.compute.internal (10.0.128.241)
Nmap scan report for ip-10-0-128-242.us-west-2.compute.internal (10.0.128.242)
Nmap scan report for ip-10-0-128-243.us-west-2.compute.internal (10.0.128.243)
...
```

# Device and port enumeration with other tools

## 1. Host discovery with netdiscover
```
sudo netdiscover -r 10.0.0.0/24
```
equivalent to:
```
sudo nmap -sn 10.0.0.0/24
```

## 2. Service discovery with hping3
-a flag makes it look like packets are coming ip address 1.2.3.4
```
sudo hping3 -a 1.2.3.4 -I lo -S 10.0.0.1 --scan 1-81
```
Monitor this with tshark
```
sudo tshark -i lo host 10.0.0.1 and port 80
```

# Stealthy Network Recon

## 1. Variable timing
```
nmap -sT skillsetlocal.com -p 21,80 -T sneaky
nmap -sT skillsetlocal.com -p 21,80 -T insane
nmap -sT skillsetlocal.com -p 21,80 --scan-delay 5s
```

## 2. SYN scan

```
sudo nmap -sS skillsetlocal.com
```

## 3. FIN scan

```
sudo nmap -sF skillsetlocal.com
```

## Decoy
```
sudo nmap -sS -p80 skillsetlocal.com -D10.10.10.10,11.11.11.11,1.1.1.1,8.8.8.8 
```

## Pinging devices with ICMP Type 8 (Ping Response) turned off
```
sudo nmap -sn -PE -PP skillsetlocal.com --send-ip

#with subnet mask request
sudo nmap -sn -PE -PM skillsetlocal.com --send-ip
```

## Fragmentation attack
```
sudo nmap -f -sS skillsetlocal.com
```

# More deatiled Nmap scans

## Service details

```
sudo nmap -sV 10.0.0.1
```

## gathering SSL information
```
nmap --script ssl-enum-ciphers -p 443 skillsetlocal.com
```

## Checking for Shellshock
```
nmap -p 80 --script http-shellshock --script-args uri=/cgi-bin/vulnscript.sh skillsetlocal.com
```
## Brute forcing MySQL
```
nmap -p 3306 --script mysql-brute skillsetlocal.com
```

# Service Identification

## manual service identification

```
telnet skillsetlocal.com 80
```

## Nmap service identification
```
nmap -sV -p3306 skillsetlocal.com

Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-19 12:59 UTC
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.000096s latency).
rDNS record for 127.0.0.1: localhost
PORT     STATE SERVICE VERSION
3306/tcp open  mysql   MySQL 5.5.47-0+deb8u1
```

## Service-specific NSE scripts
```
sudo nmap -sC -sU -p161 skillsetlocal.com --script=snmp-sysdescr --script-args snmpcommunity=secret
```

# Mobile device scanning

## Emulate android device from command line
```
android-sdk-linux/tools/emulator @android17 -no-window
```

## Busybox for basic network reconaissance
```
./busybox pscan 10.0.2.2
```

## Nmap on an android device
```
./nmap -sT 10.0.2.2
```