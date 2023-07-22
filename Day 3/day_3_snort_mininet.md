

## Run mininet
```
sudo mn
```

## Run snort on one mininet host
```
mininet/util/m h1 snort -A console -c /etc/snort/snort.conf -i h1-eth0
```

## Run an intrusive scan that snort should pick up
```
h2 nmap -sX h1
```

## Open snort rule to snort config
```
sudo nano /etc/snort/rules/local.rules
```

## Add snort rule
```
alert icmp any any -> $HOME_NET any (msg:"ICMP test"; sid:1000001;)
```

## Start snort with the new rule
```
mininet/util/m h1 snort -A console -c /etc/snort/snort.conf1 -i h1-eth0
```

## Condupt Pings to see if they trigger the new rule
```

```

Output:
```
07/19-21:47:17.493661  [**] [1:1000001:0] ICMP test [**] [Priority: 0] {ICMP} 10.0.0.2 -> 10.0.0.1
07/19-21:47:17.493673  [**] [1:1000001:0] ICMP test [**] [Priority: 0] {ICMP} 10.0.0.1 -> 10.0.0.2
```

## Create specific port rules in Snort
```
sudo nano /etc/snort/rules/local.rules
```
```
alert tcp any any -> $HOME_NET 21 (msg:"FTP connection attempt"; sid:1000002;)
```

## Start up snort with new rule
```

```

## Trigger ftp port alert
```
mininet> h2 ftp h1
```
Output:
```
07/19-21:50:05.880530  [**] [1:1000002:0] FTP connection attempt [**] [Priority: 0] {TCP} 10.0.0.2:39710 -> 10.0.0.1:21
```

## Rule for monitoring packet data
```
sudo nano /etc/snort/rules/local.rules
```
```
alert tcp any any -> $HOME_NET any (msg:"System file access"; content:"cat /etc/passwd"; sid:1000003;)
```

## Start up mininet with new snort rule
```
mininet/util/m h1 snort -A console -c /etc/snort/snort.conf1 -i h1-eth0
```

## Simulate attack which triggers new rule
```
mininet> h1 ncat -l -p 999 -e /bin/sh &
```
```
mininet> h2 ncat h1 999
cat /etc/passwd
```
Output:
```
07/19-22:03:45.677456  [**] [1:1000003:0] System file access [**] [Priority: 0] {TCP} 10.0.0.2:44690 -> 10.0.0.1:999
```