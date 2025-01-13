# File backup script

Write this to `/usr/local/bin/sync_files.sh`

```sh
#!/bin/bash

# Define source and target mappings
declare -A VAULT_MAPPINGS=(
["3D Printing"]="/mnt/vault/3D Printing"
["Books"]="/mnt/vault/Books"
["Comics"]="/mnt/vault/Comics"
["Development"]="/mnt/vault/Development"
["Games"]="/mnt/vault/Games"
["Model Rail"]="/mnt/vault/Model Rail"
["Music"]="/mnt/vault/Music"
["Photos"]="/mnt/vault/Photos"
["Rave Packs"]="/mnt/vault/Rave Packs"
)

declare -A VIDEO_MAPPINGS=(
["Films"]="/mnt/videos/Films"
["TV Shows"]="/mnt/videos/TV Shows"
["Rips"]="/mnt/videos/Rips"
["Modelling"]="/mnt/videos/Modelling"
)

# Base path for source disk
SOURCE_BASE="/mnt/usb"

# Sync to /dev/sdd2
for DIR in "${!VAULT_MAPPINGS[@]}"; do
SRC="$SOURCE_BASE/$DIR"
DEST="${VAULT_MAPPINGS[$DIR]}"
echo "Syncing $SRC to $DEST"
rsync -av --delete --progress "$SRC/" "$DEST/"
done

# Sync to /dev/sde2
for DIR in "${!VIDEO_MAPPINGS[@]}"; do
SRC="$SOURCE_BASE/$DIR"
DEST="${VIDEO_MAPPINGS[$DIR]}"
echo "Syncing $SRC to $DEST"
rsync -av --delete --progress "$SRC/" "$DEST/"
done

echo "Synchronization complete."
```

Then...

```sh
# Change ownership
sudo chmod +x /usr/local/bin/sync_disks.sh

# setup a chron job
sudo crontab -e

0 3 * * * /usr/local/bin/sync_disks.sh >> /var/log/sync_disks.log 2>&1
```

#linux