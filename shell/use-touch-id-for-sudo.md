# Using touch-id for SUDO

You can use sudo for touch id. This idea comes from [this video](https://www.youtube.com/watch?v=qOrlYzqXPa8&t=633s)


```sh
sudo nano /etc/pam.d/sudo
```

Then add this line at the top of the file

```sh
auth suffient pam_tid.so
```

#shell