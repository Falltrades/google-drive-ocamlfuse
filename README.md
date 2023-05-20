# google-drive-ocamlfuse

Follow https://github.com/astrada/google-drive-ocamlfuse for installation.

For service configuration, run this script with sudo.

```
#!/bin/bash
user=??
group=??
whatever=??
cat << EOF > /etc/systemd/system/google-drive-ocamlfuse.service
[Unit]
Description=FUSE filesystem over Google Drive
After=network.target

[Service]
User=$user
Group=$group
ExecStart=google-drive-ocamlfuse -label ${whatever} /home/user/google-drive/${whatever}
ExecStop=fusermount -u /home/${user}/google-drive/${whatever}
Restart=always
Type=forking
ExecStartPre=/bin/sleep 30

[Install]
WantedBy=multi-user.target
EOF
```

```
sudo systemctl enable google-drive-ocamlfuse.service
sudo systemctl daemon-reload
```
