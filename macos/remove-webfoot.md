# How to remove webfoot

```sh
sudo launchctl unload /Library/LaunchDaemons/com.webroot.security.mac.plist
sudo kextunload /System/Library/Extensions/SecureAnywhere.kext
sudo rm /usr/local/bin/WSDaemon
sudo rm /usr/local/bin/WFDaemon
sudo killall -9 WSDaemon
sudo killall -9 WfDaemon
sudo killall -9 "Webroot SecureAnywhere"
sudo rm -rf /System/Library/Extensions/SecureAnywhere.kext
sudo rm -rf "/Applications/Webroot SecureAnywhere.app"
sudo rm /Library/LaunchAgents/com.webroot.WRMacApp.plist
sudo rm /Library/LaunchDaemons/com.webroot.security.mac.plist
```

#macos