# Format a drive

```sh
# List all partitioins. Find the disk to mount
lsblk

# Unmount if mounted
sudo umount /mnt/internal

# Format
sudo mkfs.ext4 /dev/sdb2

# Add a label
sudo e2label /dev/sdb2 DataDrive

# Update fstab
UUID=<DEVICE_UUID> /mnt/internal ext4 defaults 0 0

# Update owner
sudo chown -R yourusername:yourusername /mnt/internal
sudo chmod -R 755 /mnt/internal
```

#linux