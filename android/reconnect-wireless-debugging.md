# Reconnect wireless debugging devices

Connect your device via a USB cable. USB debugging option needs to be turned on.
In the Android studio terminal type:

```sh
adb devices
```

The output will be something like:

```sh
List of devices attached
9APAY1EM6H      device
emulator-5554   device
```

Find your device in the list, then in the wireless debugging page of the settings find your IP address and port, then run

```
adb connect <IP-ADDRESS>:<PORT>
```

And then finally:

```sh
adb -s 9APAY1EM6H tcpip 5555 
```

Once you have done this your wireless debugging should be connected