# Rename a volume

```sh
# Install tools
sudo apt install exfatprogs

# Unmount
sudo umount /mnt/vault

# Change name
sudo exfatlabel /dev/sdX new-label

# Remount
sudo mount -a
```

#linux