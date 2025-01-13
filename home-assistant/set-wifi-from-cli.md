# Set the Wifi details from the CLI

1. Connect monitor and keyboard
2. at the ha> prompt, enter: login  
    (literally type in the word login, this will get you to a # prompt)
3. To assure wifi is functioning, enter: nmcli radio
4. Scan available wifi access enter: nmcli device wifi rescan
5. List available wifi access enter: nmcli device wifi
6. Connect to your wifi (incude quotes) enter: nmcli device wifi connect “YOUR_SSID” password “YOUR_WIFI_PASSWORD”  
    This will try to connect to your SSID and will generate a network profile for you if successfull.  
    The output will be similar to  
    `"Device 'wlan0' successfully activated with...."`
7. Show connections enter: nmcli con show  
    There may be two separate ip addresses on your network: one for ethernet, one for wifi.
8. Check the ip addresses enter: ip addr show  
    Now connect to `http(s)://your_wifi_ip:8123` in your browser.

#homeassistant