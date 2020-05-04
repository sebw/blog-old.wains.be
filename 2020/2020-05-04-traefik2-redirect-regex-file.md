# Make a regexp redirect in dynamic configuration file with Traefik v2

`/etc/traefik/traefik.yml`:

```
[...]
providers:
  file:
    directory: "/etc/traefik/dynamic/"
    watch: true
[...]
```

`/etc/traefik/dynamic/redirect.yml`:

```
http:
  middlewares:
    redir:
      redirectRegex:
        permanent: true
        regex: "https://old.wains.be/(.*)"
        replacement: "https://new.wains.be/${1}"

  routers:
    redir:
      rule: "HostRegexp(`old.wains.be`)"
      entrypoints:
      - https
      middlewares: 
      - redir
      tls:
        certresolver: "letsencrypt"
      service: "ThisWillNeverBeUsedByNeedsToBeThere"

  services:
    ThisWillNeverBeUsedByNeedsToBeThere:
      loadBalancer:
        servers:
          - url: "http://127.0.0.1"
```

But if you want to make the same with labels on Docker containers:

```
traefik.http.routers.prsite.rule: "HostRegexp(`old.wains.be`)"
traefik.http.routers.prsite.entrypoints: "https"
traefik.http.routers.prsite.tls: "true"
traefik.http.routers.prsite.middlewares: "pr-redirect"
traefik.http.middlewares.pr-redirect.redirectregex.regex: "^https://old.wains.be/(.*)"
traefik.http.middlewares.pr-redirect.redirectregex.replacement: "https://new.wains.be/$1"
traefik.http.middlewares.pr-redirect.redirectregex.permanent: "true" 
```

The service part should not be defined since the labels are applied to the container which is the service.