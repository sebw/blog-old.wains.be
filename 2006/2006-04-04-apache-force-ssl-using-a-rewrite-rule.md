


date: 2006-04-04 18:24:07+00:00


# 'Apache : force SSL using a rewrite rule'

categories:
- Apache
- Linux
- Security


**This rewrite rule will redirect the requests to https (SSL) :**

`RewriteEngine on
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^.*$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]`

The module mod_rewrite is needed.

Something like "LoadModule rewrite_module modules/mod_rewrite.so" in your apache config should enable it.
