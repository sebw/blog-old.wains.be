


date: 2006-12-18 17:40:23+00:00


# Transparent Squid proxy

categories:
- Howto
- Linux
- Proxy


How to run squid as a transparent squid proxy :

**Squid 2.5 and earlier :**

Edit /etc/squid/squid.conf and add this :

`httpd_accel_host virtual
httpd_accel_port 80
httpd_accel_with_proxy on
httpd_accel_uses_host_header on`

<!-- more -->

To enable the transparent proxying, type this :

`iptables -t nat -A PREROUTING -i eth0 -s 192.168.1.0/24 -p tcp --dport 80 -j REDIRECT --to-port 3128`

"-s 192.168.1.0/24" is optional but needed if you run a webserver on the squid machine. The web visitor request would be piped in squid without it.

**Squid 2.6 and later :**

[http://blog.wains.be/post/squid-26-transparent-proxy/](http://blog.wains.be/post/squid-26-transparent-proxy/)
