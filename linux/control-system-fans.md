# Control the system fans

```sh
# Install it
sudo apt update
sudo apt install macfanctld
sudo systemctl start macfanctld
sudo systemctl enable macfanctld

# See the status:
sudo systemctl status macfanctld
```

#linux