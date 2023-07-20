# Day 1

## CTF 1

1. What are the authoritative name servers for `blinkdigitalsecurity.com`

- using `nslookup`
``` bash
nslookup -type=NS blinkdigitalsecurity.com
```
- response
```
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;blinkdigitalsecurity.com.      IN      NS

;; ANSWER SECTION:
blinkdigitalsecurity.com. 281   IN      NS      ns46.worldnic.com.
blinkdigitalsecurity.com. 281   IN      NS      ns45.worldnic.com.

;; Query time: 3 msec
;; SERVER: 10.0.0.2#53(10.0.0.2)
;; WHEN: Tue Jul 18 02:16:45 UTC 2023
;; MSG SIZE  rcvd: 100

(1) Skillset Labs> nslookup -type=NS blinkdigitalsecurity.com
Server:         10.0.0.2
Address:        10.0.0.2#53

Non-authoritative answer:
blinkdigitalsecurity.com        nameserver = ns45.worldnic.com.
blinkdigitalsecurity.com        nameserver = ns46.worldnic.com.

Authoritative answers can be found from:
```

- using `dig`
``` bash
dig NS blinkdigitalsecurity.com
```

- response
```
; <<>> DiG 9.9.5-9+deb8u6-Debian <<>> NS blinkdigitalsecurity.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48632
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;blinkdigitalsecurity.com.      IN      NS

;; ANSWER SECTION:
blinkdigitalsecurity.com. 281   IN      NS      ns46.worldnic.com.
blinkdigitalsecurity.com. 281   IN      NS      ns45.worldnic.com.

;; Query time: 3 msec
;; SERVER: 10.0.0.2#53(10.0.0.2)
;; WHEN: Tue Jul 18 02:16:45 UTC 2023
;; MSG SIZE  rcvd: 100
```

- using `host`
``` bash
host -t NS blinkdigitalsecurity.com
```
- response
```
blinkdigitalsecurity.com name server ns45.worldnic.com.
blinkdigitalsecurity.com name server ns46.worldnic.com.
```

- using `whois`
``` bash
whois blinkdigitalsecurity.com
```
- response
```
bash: whois: command not found
```

2. Who owns `onlineclientreporting.com`

- using `whois`
```
whois onlineclientreporting.com
```
- response
```
bash: whois: command not found
```

- using `nslookup`
```
nslookup -type=MX onlineclientreporting.com
```
- response
```
Server:         10.0.0.2
Address:        10.0.0.2#53

Non-authoritative answer:
*** Can't find onlineclientreporting.com: No answer

Authoritative answers can be found from:
onlineclientreporting.com
        origin = ns2.usbank.com
        mail addr = domainadmin.usbank.com
        serial = 2022041807
        refresh = 28800
        retry = 7200
        expire = 604800
        minimum = 86400

```
- using `dig`
```bash
dig onlineclientreporting.com ANY
dig onlineclientreporting.com MX
dig onlineclientreporting.com SOA
dig onlineclientreporting.com AAAA
```
- response
```bash
```

3. Get the communities for an SNMP server
- using `onesixtyone`
```bash
onesixtyone -c <community_list_file> <target_host>

onesixtyone -c /usr/share/wordlists/metasploit/snmp_default_pass.txt 127.0.1.11
```

1 reults 
```bash
Scanning 1 hosts, 121 communities
127.0.1.11 [pr1v4t3] Hardware: Intel64 Family 6 Model 58 Stepping 9 AT/AT COMPATIBLE - Software: Windows Version 6.3 (Build 9600 Multiprocessor Free)
```

- using `snmp-check`
```
snmp-check -t <target_host> -c <community_list_file>

snmp-check -c /usr/share/wordlists/metasploit/snmp_default_pass.txt -t 127.0.1.11
-result
```bash

```

4. Find the version of FTP server that is present
```bash
snmpwalk -v2c -c <community_string> <target_device>

snmpwalk -v2c -c pr1v4t3 127.0.1.11
```

```bash
snmpwalk -v2c -c pr1v4t3 127.0.1.11 hrSWRunName
```