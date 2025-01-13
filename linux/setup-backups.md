# Setup backups for the system


```sh
# Install rsnapshot
sudo apt-get install rsnapshot

# End the config file
# NOTE This must use TABS to seperate arguments
sudo nano /etc/rsnapshot.conf

# Add the root
snapshot_root /mnt/internal/
# Add retain time
retain weekly 7
# Add relative path support
no_create_root 1
# Add backup points
backup /etc/ localhost/etc/
backup /home/ localhost/home/
backup /var/lib/casaos localhost/var/lib/casaos
backup /root/ localhost/root/
backup /usr/local/ localhost/usr/local/
backup /DATA/ localhost/DATA/

# Exit and test the configuration
sudo rsnapshot configtest

# Run a backup
sudo rsnapshot weekly

# Edit crontab to schedule the backups weekly
sudo crontab -e

0 3 * * 5 /usr/bin/rsnapshot weekly
```

#linux 