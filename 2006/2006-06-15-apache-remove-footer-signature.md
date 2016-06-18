


date: 2006-06-15 09:41:05+00:00


# 'Apache : remove footer signature'

categories:
- Apache
- Linux
- Security


This will remove the signature added at the bottom of index pages :

**/etc/httpd/conf/httpd.conf :**
ServerTokens Prod
ServerSignature Off 
