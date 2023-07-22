# skillsetlocal.com

## Scan Endpoint
```
nmap -A skillsetlocal.com -p- -oN nmap_scan_result
```
```
Nmap scan report for skillsetlocal.com (127.0.0.1)
Host is up (0.000029s latency).
rDNS record for 127.0.0.1: localhost
Not shown: 65517 closed ports
PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         vsftpd 3.0.2
22/tcp    open  ssh         OpenSSH 6.7p1 Debian 5 (protocol 2.0)
| ssh-hostkey: 
|   1024 77:ba:e8:aa:14:87:47:a0:b4:f5:83:22:86:9a:47:b4 (DSA)
|   2048 31:5f:92:a2:0e:c5:ad:d6:6f:f6:8b:d0:85:a5:aa:fa (RSA)
|_  256 88:cf:f8:96:08:8a:68:2a:b0:2c:04:88:48:fa:1c:fd (ECDSA)
23/tcp    open  telnet      Linux telnetd
25/tcp    open  smtp        Exim smtpd 4.84_2
| smtp-commands: ip-10-0-174-139.us-west-2.compute.internal Hello localhost [127
.0.0.1], SIZE 52428800, 8BITMIME, PIPELINING, HELP, 
|_ Commands supported: AUTH HELO EHLO MAIL RCPT DATA NOOP QUIT RSET HELP 
53/tcp    open  domain
| dns-nsid: 
|_  bind.version: 9.9.5-9+deb8u6-Debian
80/tcp    open  http        Apache httpd 2.4.10 ((Debian))
|_http-server-header: Apache/2.4.10 (Debian)
|_http-title: Apache2 Debian Default Page: It works
139/tcp   open  netbios-ssn Samba smbd 3.X (workgroup: IP-10-0-174-139)
445/tcp   open  netbios-ssn Samba smbd 3.X (workgroup: IP-10-0-174-139)
953/tcp   open  rndc?
3004/tcp  open  ssl/http    WEBrick httpd 1.3.1 (Ruby 2.1.5 (2014-11-13); OpenSS
L 1.0.1k)
|_http-title: Did not follow redirect to https://skillsetlocal.com/login
| ssl-cert: Subject: commonName=dradis/organizationName=Dradis Framework [dradis
framework.org]/stateOrProvinceName=Some-State/countryName=AU
| Not valid before: 2011-02-10T17:35:17
|_Not valid after:  2012-02-10T17:35:17
3306/tcp  open  mysql       MySQL 5.5.5-10.1.22-MariaDB-
| mysql-info: 
|   Protocol: 53
|   Version: .5.5-10.1.22-MariaDB-
|   Thread ID: 7
|   Capabilities flags: 63487
|   Some Capabilities: IgnoreSigpipes, ConnectWithDatabase, DontAllowDatabaseTab
leColumn, SupportsLoadDataLocal, SupportsCompression, LongColumnFlag, ODBCClient
, IgnoreSpaceBeforeParenthesis, FoundRows, LongPassword, Support41Auth, Supports
Transactions, InteractiveClient, Speaks41ProtocolNew, Speaks41ProtocolOld
|   Status: Autocommit
|_  Salt: n<~*O1GSIVS~AhiUNd1e
5432/tcp  open  postgresql  PostgreSQL DB
5984/tcp  open  http        CouchDB httpd 1.6.2 (Erlang OTP/19)
|_http-server-header: CouchDB/1.6.2 (Erlang OTP/19)
|_http-title: Site doesn't have a title (text/plain; charset=utf-8).
9390/tcp  open  ssl/unknown
| ssl-cert: Subject: commonName=ip-10-0-0-85/organizationName=OpenVAS Users Unit
ed/stateOrProvinceName=none/countryName=DE
| Not valid before: 2016-06-16T19:00:17
|_Not valid after:  2017-06-16T19:00:17
|_ssl-date: 2023-07-21T02:19:20+00:00; -1m29s from scanner time.
9391/tcp  open  ssl/unknown
|_ssl-date: 2023-07-21T02:21:40+00:00; +49s from scanner time.
9392/tcp  open  ssl/http    Greenbone Security Assistant
|_hadoop-datanode-info: 
|_hadoop-jobtracker-info: 
|_hadoop-tasktracker-info: 
|_hbase-master-info: 
|_http-title: Did not follow redirect to https://skillsetlocal.com/login/login.h
tml
| ssl-cert: Subject: commonName=ip-10-0-0-85/organizationName=OpenVAS Users Unit
ed/stateOrProvinceName=none/countryName=DE
| Not valid before: 2016-06-16T19:00:17
|_Not valid after:  2017-06-16T19:00:17
|_ssl-date: 2023-07-21T02:19:26+00:00; -1m19s from scanner time.
12345/tcp open  tcpwrapped
65412/tcp open  http        BaseHTTPServer 0.3 (Python 2.7.13)
|_http-server-header: BaseHTTP/0.3 Python/2.7.13
|_http-title: Damn Small Vulnerable Web (DSVW) &lt; 100 LoC (Lines of Code)
1 service unrecognized despite returning data. If you know the service/version, 
please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?n
ew-service :
SF-Port5432-TCP:V=7.01%I=7%D=7/21%Time=64B9EB68%P=x86_64-pc-linux-gnu%r(SM
SF:BProgNeg,85,"E\0\0\0\x84SFATAL\0C0A000\0Munsupported\x20frontend\x20pro
SF:tocol\x2065363\.19778:\x20server\x20supports\x201\.0\x20to\x203\.0\0Fpo
SF:stmaster\.c\0L1986\0RProcessStartupPacket\0\0");
Service Info: Host: ip-10-0-174-139.us-west-2.compute.internal; OSs: Unix, Linux
; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: IP-10-0-174-139, NetBIOS user: <unknown>, NetBIOS MAC: <
unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.5.8-Debian)
|   Computer name: ip-10-0-174-139
|   NetBIOS computer name: IP-10-0-174-139
|   Domain name: us-west-2.compute.internal
|   FQDN: ip-10-0-174-139.us-west-2.compute.internal
|_  System time: 2023-07-21T02:20:45+00:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smbv2-enabled: Server supports SMBv2 protocol
```
