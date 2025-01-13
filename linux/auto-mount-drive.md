# Auto mount drive as R/W

```sh
# List all partitioins. Find the disk to mount
lsblk

# Check the disk format and copy the UUID
sudo blkid /dev/sdb1

# Create a mount point
sudo mkdir -p /mnt/usb

# Edit fstab
sudo nano /etc/fstab

# and Add this line
UUID=<DEVICE_UUID> /mnt/usb <FORMAT> defaults,rw,uid=1000,gid=1000 0 0

# Test mounting the device
sudo mount -a
df -h
```

# Mount a HFS Disk

```sh
# Install HFS support
sudo apt update
sudo apt install hfsprogs

# List all partitioins. Find the disk to mount
lsblk

# Check the disk format (wanted to be hfsplus) and Copy the UUID
sudo blkid /dev/sdb2

# Create a mount point
sudo mkdir -p /mnt/internal

# Edit fstab
sudo nano /etc/fstab

# and Add this line
UUID=<DEVICE_UUID> /mnt/internal hfsplus ro,uid=1000,gid=1000 0 0

# Test mounting the device
sudo mount -a
df -h
```

#linux