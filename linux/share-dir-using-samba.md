# Share a directory

```sh
#Install samba
sudo apt update
sudo apt install samba

# Edit samba conf
sudo nano /etc/samba/smb.conf

#Add share
[3D Printing]
path = "/mnt/usb/3D Printing"
valid users = paulchana
read only = no
browseable = yes
create mask = 0700
directory mask = 0700

# ... etc ...

# Add password to account
sudo smbpasswd -a paulchana

# Restart samba
sudo systemctl restart smbd
sudo systemctl restart nmbd

# Start samba on boot
sudo systemctl enable smbd
sudo systemctl enable nmbd

```

#linux 