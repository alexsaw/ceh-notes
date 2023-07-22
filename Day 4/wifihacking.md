# Wifi Hacking

## Begin WEP packet capture
```
tshark -r wifihacking/wepcapture.cap | more
```

## Capture packets with WEP tool for aircrack-ng
```
aircrack-ng wifihacking/wepcapture.cap
```

## Crack WPA2 passwords with rockyou.txt
```
aircrack-ng -w /usr/share/wordlists/rockyou.txt wifihacking/wpa2capture.cap
```