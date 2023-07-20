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
