# SELinux

**Troubleshooting SELinux easily**

On Fedora use dnf instead of yum

```
yum install setroubleshoot setroubleshoot-server
systemctl restart auditd.service
```

Then run `journalctl -b -0` while attempting access to the ressource that is being blocked by SELinux.

**Troubleshooting with GUI**

Get an overview of SELinux status, booleans, file labels, user mapping, users, network ports, policy module and process domains in one interface.

On your server install those (this will install about 170MB of stuff):

```
yum install xorg-x11-xauth bitmap-fixed-fonts policycoreutils-gui
```

From your workstation:

`ssh -Y` to the server and run `system-config-selinux`

**Enabling SELinux on a system that had it disabled**

Set `SELINUX=permissive` in `/etc/sysconfig/selinux`

Run `touch /.autorelabel`

Reboot

Set `SELINUX=enforcing` in `/etc/sysconfig/selinux`

Reboot

**Set and get SELinux status**

```
sestatus
getenforce
```

```
setenforce 0|1
```

**Listing applied context**

Contexts are applied to files, ports, processes, etc.

```
ls -Z  
netstat -Z  
id -Z  
ps -Z
```

**Change context**

`chcon -t context /var/www/html/index.html`

Using the context of directory to index.html:

`chcon --reference /var/www/html /var/www/html/index.html`

**Getting SELinux booleans**

`getsebool -a`

**Setting SELinux booleans**

`setsebool -P httpd_enable_homedirs 1`

1 = persist