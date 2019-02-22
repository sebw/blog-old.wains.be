# Random 502 Bad Gateway on Docker CE

For a long time I was getting random 502 errors "Bad Gateway" on my Docker instance running on a small VPS.

I run my containers behind a reverse proxy, with Let's Encrypt.

Initially I was using Nginx, then moved on to Traefik, but the problem remained.

I was thinking it was related to the number of containers (16 for 2GB of RAM), but that was a network issue according to logs (cannot connect to host).

The phenomenon was going away when I was stopping the Nextcloud container.

I had Nextcloud configured to connect to the MySQL DB container using the `--link` option.

While investigating, I learned the option is deprecated.

That's only then that I realized that it is recommended to create a user defined bridge.

With a user defined bridge, you automatically get name resolution.

After moving all my containers to the new bridge, I no longer have issues.

**Conclusion:** don't put your container in the default bridge, create a user defined bridge, and don't use the `--link` option.