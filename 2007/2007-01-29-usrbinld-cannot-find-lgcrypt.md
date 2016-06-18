


date: 2007-01-29 16:04:07+00:00


# '/usr/bin/ld: cannot find -lgcrypt'

categories:
- Linux
- Red Hat/CentOS


While trying to compile yaz, I got this error :

"/usr/bin/ld: cannot find -lgcrypt"

Simple fix :

Install this package: libgcrypt-devel

`yum install libgcrypt-devel`
