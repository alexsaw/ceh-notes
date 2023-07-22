# SET

## Open hosts file
```
sudo nano /etc/hosts
```

## add spoofed google.com entry
```
127.0.0.1        google.com
google.com   127.0.0.1
```

#### ping to check
```
ping -c 1 google.com
```

## Start up SET toolkit
```
sudo setoolkit
[enter]
```

Output:
```
[---]        Follow me on Twitter: @HackingDave        [---]
[---]       Homepage: https://www.trustedsec.com       [---]

        Welcome to the Social-Engineer Toolkit (SET). 
         The one stop shop for all of your SE needs.

     Join us on irc.freenode.net in channel #setoolkit

   The Social-Engineer Toolkit is a product of TrustedSec.

             Visit: https://www.trustedsec.com

 Select from the menu:

   1) Social-Engineering Attacks
   2) Fast-Track Penetration Testing
   3) Third Party Modules
   4) Update the Social-Engineer Toolkit
   5) Update SET configuration
   6) Help, Credits, and About

  99) Exit the Social-Engineer Toolkit

set> 
```

## Use the social engineering attacks
```
1
[enter]
```

## Select using web template for credential harvesting attack
```Select the website attack vectors (2) and then the credential harvesting vector (3) then select the templates option (1)```

## Enter loopback address for return traffic
```
127.0.0.1
```

## Template selection
```select Google (2)```

## Attempt to login to Google
```
w3m google.com
```
```
[ctrl + c]
q
y
```
## Read harvested credentials
```
cat /var/www/html/harvester_<timestamp>.txt
```
