# Openssl oneliners

_Generate a private key_

```
openssl genrsa -out ssl.key 1024
```

_Generate a self-signed certificate_     

```
openssl req -new -x509 -days 3650 -key ssl.key -out ssl.crt
```

_Verification_

```
openssl x509 -in ssl.crt -text -noout
```

_Checking certificate validity (put this in your .bashrc)_

```
alias cert-check="openssl s_client -CApath /etc/ssl/certs/ -connect $1"
alias cert-check-date="ssl-check-date $1"
function ssl-check-date ()
{
openssl s_client -CApath /etc/ssl/certs/ -connect $1 2>/dev/null | 
openssl x509 -noout -dates
}
```
