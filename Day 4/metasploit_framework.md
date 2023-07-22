# Metasploit

## Nmap scan for metasploitable ports
```
https://app.infosecinstitute.com/portal/skills/content/asset/17160
```

## Open Metasploit
```
msfconsole
```

## Nmap scan
```
search __
info __
use __
```

## Post exploit
once a shell is open, do the following
```
ctrl+z
y
```
```
sessions
```
#### upgrade the meterpreter
```
sessions -u 2
```
```
sessions
```
## Interact with the new sessions
```
sessions -i 3
```
```
help
```
## use follow on exploits
```
use exploit/linux/local/su_login
```
```
set session 3
```