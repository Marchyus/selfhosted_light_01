# SMB share
## Install `samba`
```bash
sudo apt update
sudo apt install samba -y
```


## Prepare media dir
```bash
sudo mkdir -p /srv/media
sudo chown -R OWNER:GROUP /srv/media
```

## Config share
```bash
sudo nano /etc/samba/smb.conf
```

add 

```ini
[JellyfinMedia]
   path = /srv/media
   valid users = USER
   read only = no
   browsable = yes
   create mask = 0755

```


## Set network pass

```bash
sudo smbpasswd -a USER
```

## Restart service

```bash
sudo systemctl restart smbd
```

# Firewall
Open 8096 and 7359 ports:
```bash
# Direct local video streaming
sudo ufw allow 8096/tcp
# Local network auto-discovery
sudo ufw allow 7359/udp

```

Open SMB ports:
```bash
sudo ufw allow 139,445/tcp
sudo ufw allow 137,138/udp
sudo ufw reload
```
