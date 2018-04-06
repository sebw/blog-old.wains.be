# systemd

### Default directories

- /usr/lib/systemd/system
- /etc/systemd/system

### List units (current snapshot of the system)

`systemctl list-units --type=service --all`

`systemctl list-units --type=target --all`

### List units at startup

`systemctl list-unit-files`

### Get default "runlevel" (known as target in systemd)

`systemctl get-default`

See symlink /etc/systemd/system/default.target

### Set default target

`systemctl set-default multi-user.target`

### Change target from GUI to CLI

`systemctl isolate multi-user.target`

### Power off/reboot

```
systemctl isolate poweroff.target
systemctl poweroff
systemctl reboot
```

### Consult journal since last boot

`journalctl -b 0`

### List cgroup hierarchy

`systemd-cgls`

### Manage service target

```
systemctl start postfix.service
systemctl stop postfix.service
systemctl status postfix.service
systemctl enable postfix.service
systemctl disable postfix.service
```