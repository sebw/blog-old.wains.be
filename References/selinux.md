# SELinux

**Troubleshooting SELinux easily from CLI**

On Fedora use dnf instead of yum

```
yum install setroubleshoot setroubleshoot-server
systemctl restart auditd.service
```

Then run `journalctl -b -0` while attempting access to the ressource that is being blocked by SELinux.

Run sealert as advised in the logs.

**Troubleshooting with GUI**

Get an overview of SELinux status, booleans, file labels, user mapping, users, network ports, policy module and process domains in one interface.

On your server install those (this will install about 170MB of stuff):

```
yum install xorg-x11-xauth bitmap-fixed-fonts policycoreutils-gui
```

From your workstation:

`ssh -Y` to the server and run `system-config-selinux`

**Displaying all SELinux rules applied to a service**

For example for haproxy:

```
setenforce 0 (if service doesn't start and you need to troubleshoot)
systemctl start haproxy
ps auxZ haproxy | grep haproxy
  --> returns system_u:system_r:haproxy_t:s0
sesearch -d -A -s haproxy_t

If you are getting a `name_bind` error in audit logs:

sesearch -d -A -s haproxy_t -p "name_bind"

setenforce 1
```

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

**Check context for specific files**

Let's assume you install BIND and want to check where logs should be sent.

`semanage fcontext -l | grep named | grep log`

**Change context**

Changes made with chcon would not survive a relabel!

`chcon -t ${context} /var/www/html/index.html`

Using the context of directory to index.html:

`chcon --reference /var/www/html /var/www/html/index.html`

**Change context so it survives a relabel**

`semanage fcontext -a -t ${context} "/var/www/html(/.*)?"`

**Getting SELinux booleans**

`getsebool -a`

**Setting SELinux booleans**

`setsebool -P httpd_enable_homedirs 1`

1 = persist

**Getting ports applied to a context**

semanage port -l
