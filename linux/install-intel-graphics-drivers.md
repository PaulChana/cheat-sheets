# Install intel graphics drivers

```sh
sudo apt install libdrm-intel1 intel-media-va-driver-non-free i965-va-driver gstreamer1.0-libav vainfo
```

In Jellyfin set the renderer to QSV and the path to /dev/dri/renderD128

#linux #jellyfin 