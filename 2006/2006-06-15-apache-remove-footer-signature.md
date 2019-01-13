# 'Apache : remove footer signature'

This will remove the signature added at the bottom of index pages :

/etc/httpd/conf/httpd.conf

```
ServerTokens Prod
ServerSignature Off 
```